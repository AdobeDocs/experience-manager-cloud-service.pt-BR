---
title: Componentes principais da AEM-CIF e integração com o Adobe Experience Platform
description: Saiba como enviar dados de evento da loja de uma página de produto renderizada AEM para o Experience Platform usando o Conector CIF - Experience Platform.
sub-product: Commerce
version: Cloud Service
activity: setup
feature: Commerce Integration Framework
topic: Commerce
role: Architect, Developer
level: Beginner
kt: 10834
thumbnail: 346811.jpeg
source-git-commit: 6b91c47f741f12cf66efd6a2ad6d9c1f4531ac70
workflow-type: tm+mt
source-wordcount: '2006'
ht-degree: 1%

---


# Componentes principais da AEM-CIF e integração com o Adobe Experience Platform {#aem-cif-aep-integration}

O [Commerce Integration Framework (CIF)](https://github.com/adobe/aem-core-cif-components) os componentes principais fornecem integração perfeita com [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) para encaminhar eventos de vitrine e seus dados de interações do lado do cliente, como __adicionar ao carrinho__.

O [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) O projeto fornece uma biblioteca de JavaScript chamada [Conector Experience Platform](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) para coletar dados do evento da loja do Commerce. Os dados do evento são enviados para o Experience Platform, onde são usados em outros produtos da Adobe Experience Cloud, como o Adobe Analytics e o Adobe Target, para criar um perfil de 360 graus que cubra uma jornada do cliente. Ao conectar os dados do Commerce a outros produtos na Adobe Experience Cloud, você pode realizar tarefas como analisar o comportamento do usuário no seu site, realizar testes AB e criar campanhas personalizadas.

Saiba mais sobre o [Coleta de dados do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) conjunto de tecnologias que permitem coletar dados de experiência do cliente de fontes do lado do cliente.

## Enviar `addToCart` dados de evento para Experience Platform {#send-addtocart-to-aep}

As etapas a seguir mostram como enviar a variável `addToCart` dados de evento de páginas de produto renderizadas AEM para o Experience Platform usando o Conector CIF - Experience Platform. Ao usar a extensão de navegador do Adobe Experience Platform Debugger, é possível testar e revisar os dados enviados.

![Revisar os dados do evento addToCart no Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)

## Pré-requisitos {#prerequisites}

Você deve usar um ambiente de desenvolvimento local para concluir essa demonstração. Isso inclui uma instância em execução de AEM que é configurada e conectada a uma instância do Adobe Commerce. Revise os requisitos e as etapas para [configuração do desenvolvimento local com AEM SDK as a Cloud Service](../develop.md).

Você também precisa acessar o [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) e permissões para criar o esquema, o conjunto de dados e os conjuntos de dados para a coleta de dados. Para obter mais informações, consulte [Gerenciamento de permissões](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Configuração as a Cloud Service do AEM Commerce {#aem-setup}

Para trabalhar __AEM Commerce as a Cloud Service__ ambiente local com o código e a configuração necessários, conclua as etapas a seguir.

### Configuração local

Siga as [Configuração local](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) etapas para ter um ambiente as a Cloud Service AEM Commerce.

### Configuração do projeto

Siga as [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) etapas para criar um novo projeto do AEM Commerce (CIF).

>[!TIP]
>
>No exemplo a seguir, o projeto AEM Commerce é nomeado como: `My Demo Storefront`, no entanto, você pode escolher seu próprio nome de projeto.

![Projeto de comércio AEM](../assets/aep-integration/aem-project-with-commerce.png)


Crie e implante o projeto recém-criado AEM Commerce no SDK AEM local executando o seguinte comando no diretório raiz do projeto.

```bash
$ mvn clean install -PautoInstallSinglePackage
```

Os `My Demo StoreFront` site de comércio com código e conteúdo padrão é semelhante ao seguinte:

![Site de comércio AEM padrão](../assets/aep-integration/demo-aem-storefront.png)

### Instale as dependências do conector Peregrine e CIF-AEP

Para coletar e enviar os dados do evento das páginas de categoria e produto deste site do AEM Commerce, é necessário instalar a chave `npm` os pacotes no `ui.frontend` módulo do projeto AEM Commerce.

Navegue até o `ui.frontend` e instale os pacotes necessários executando os seguintes comandos a partir da linha de comando.

```bash
npm i --save lodash.get@^4.4.2 lodash.set@^4.3.2
npm i --save apollo-cache-persist@^0.1.1
npm i --save redux-thunk@~2.3.0
npm i --save @adobe/apollo-link-mutation-queue@~1.1.0
npm i --save @magento/peregrine@~12.5.0
npm i --save @adobe/aem-core-cif-react-components --force
npm i --save-dev @magento/babel-preset-peregrine@~1.2.1
npm i --save @adobe/aem-core-cif-experience-platform-connector --force
```

>[!IMPORTANT]
>
>O `--force` às vezes, o argumento é necessário como [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) é restritiva com as dependências de peer compatíveis. Geralmente, isso não deve causar problemas.


### Configure o Maven para usar `--force` argumento

Como parte do processo de compilação Maven, a instalação de limpeza de npm (usando `npm ci`) é acionado. Isso também requer que o `--force` argumento .

Navegue até o arquivo POM raiz do projeto `pom.xml` e localize a `<id>npm ci</id>` bloco de execução. Atualize o bloco para que ele se pareça com o seguinte:

```xml
<execution>
    <id>npm ci</id>
    <goals>
    <goal>npm</goal>
    </goals>
    <configuration>
    <arguments>ci --force</arguments>
    </configuration>
</execution>
```

### Alterar formato de configuração do Babel

Alternar a partir do padrão `.babelrc` formato de arquivo de configuração relativo do arquivo para `babel.config.js` formato. Este é um formato de configuração de todo o projeto e permite que os plug-ins e as predefinições sejam aplicados à variável `node_module` com maior controle.

1. Navegue até o `ui.frontend` e exclua o módulo existente `.babelrc` arquivo.

1. Crie um `babel.config.js` que usa o `peregrine` predefinição.

   ```javascript
   const peregrine = require('@magento/babel-preset-peregrine');
   
   module.exports = (api, opts = {}) => {
       const config = {
           ...peregrine(api, opts),
           sourceType: 'unambiguous'
       } 
   
       config.plugins = config.plugins.filter(plugin => plugin !== 'react-refresh/babel');
   
       return config;
   }
   ```

### Configure o webpack para utilizar o Babel

Para transformar os arquivos JavaScript usando o Babel loader (`babel-loader`) e o webpack, é necessário modificar o `webpack.common.js` arquivo.

Navegue até o `ui.frontend` e atualize o `webpack.common.js` para ter a seguinte regra dentro do `module` valor da propriedade:

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### Configurar o cliente Apollo

O [Cliente Apollo](https://www.apollographql.com/docs/react/) é usada para gerenciar dados locais e remotos com GraphQL. Ele também armazena os resultados de consultas GraphQL em um cache local, normalizado, na memória.

Para [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) para trabalhar com eficácia, você precisa de um `possibleTypes.js` arquivo. Para gerar esse arquivo, consulte [Geração de possibleTypes automaticamente](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically). Além disso, consulte o [Implementação de referência do PWA Studio](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) e um exemplo de um [`possibleTypes.js`](../assets/possibleTypes.js) arquivo.


1. Navegue até o `ui.frontend` e salve o arquivo como `./src/main/possibleTypes.js`

1. Atualize o `webpack.common.js` do arquivo `DefinePlugin` para substituir as variáveis estáticas necessárias durante o tempo de criação.

   ```javascript
   const { DefinePlugin } = require('webpack');
   const { POSSIBLE_TYPES } = require('./src/main/possibleTypes');
   
   ...
   
   plugins: [
       ...
       new DefinePlugin({
           'process.env.USE_STORE_CODE_IN_URL': false,
           POSSIBLE_TYPES
       })
   ]
   ```

### Inicializar componentes principais do Peregrine e da CIF

Para inicializar os componentes principais do React-based Peregrine e da CIF, crie a configuração necessária e os arquivos JavaScript.

1. Navegue até o `ui.frontend` e crie a seguinte pasta: `src/main/webpack/components/commerce/App`

1. Crie um `config.js` arquivo com o seguinte conteúdo:

   ```javascript
   // get and parse the CIF store configuration from the <head>
   const storeConfigEl = document.querySelector('meta[name="store-config"]');
   const storeConfig = storeConfigEl ? JSON.parse(storeConfigEl.content) : {};
   
   // the following global variables are needed for some of the peregrine features
   window.STORE_VIEW_CODE = storeConfig.storeView || 'default';
   window.AVAILABLE_STORE_VIEWS = [
       {
           code: window.STORE_VIEW_CODE,
           base_currency_code: 'USD',
           default_display_currency_code: 'USD',
           id: 1,
           locale: 'en',
           secure_base_media_url: '',
           store_name: 'My Demo StoreFront'
       }
   ];
   window.STORE_NAME = window.STORE_VIEW_CODE;
   window.DEFAULT_COUNTRY_CODE = 'en';
   
   export default {
       storeView: window.STORE_VIEW_CODE,
       graphqlEndpoint: storeConfig.graphqlEndpoint,
       // Can be GET or POST. When selecting GET, this applies to cache-able GraphQL query requests only.
       // Mutations will always be executed as POST requests.
       graphqlMethod: storeConfig.graphqlMethod,
       headers: storeConfig.headers,
   
       mountingPoints: {
           // TODO: define the application specific mount points as they may be used by <Portal> and <PortalPlacer>
       },
       pagePaths: {
           // TODO: define the application specific paths/urls as they may be used by the components
           baseUrl: storeConfig.storeRootUrl
       },
       eventsCollector: {
           // Enable the Experience Platform Connector and define the org and datastream to use
           aep: {
               orgId: // TODO: add your orgId
               datastreamId: // TODO: add your datastreamId
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >Embora já possa estar familiarizado com o [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) arquivo de __Guias de AEM - Projeto CIF Venia__, há algumas alterações que você precisa fazer neste arquivo. Primeiro, revise qualquer __TODO__ comentários. Em seguida, dentro do `eventsCollector` , encontre a `eventsCollector > aed` e atualize o `orgId` e `datastreamId` para os valores corretos. [Saiba mais](./aep.md#add-aep-values-to-aem).

1. Crie um `App.js` com o seguinte conteúdo. Esse arquivo se parece com um arquivo típico de ponto de partida do aplicativo React e contém ganchos React e personalizados e o uso React Context para facilitar a integração do Experience Platform.

   ```javascript
   import config from './config';
   
   import React, { useEffect } from 'react';
   import ReactDOM from 'react-dom';
   import { IntlProvider } from 'react-intl';
   import { BrowserRouter as Router } from 'react-router-dom';
   import { combineReducers, createStore } from 'redux';
   import { Provider as ReduxProvider } from 'react-redux';
   import { createHttpLink, ApolloProvider } from '@apollo/client';
   import { ConfigContextProvider, useCustomUrlEvent, useReferrerEvent, usePageEvent, useDataLayerEvents, useAddToCartEvent } from '@adobe/aem-core-cif-react-components';
   import { EventCollectorContextProvider, useEventCollectorContext } from '@adobe/aem-core-cif-experience-platform-connector';
   import { useAdapter } from '@magento/peregrine/lib/talons/Adapter/useAdapter';
   import { customFetchToShrinkQuery } from '@magento/peregrine/lib/Apollo/links';
   import { BrowserPersistence } from '@magento/peregrine/lib/util';
   import { default as PeregrineContextProvider } from '@magento/peregrine/lib/PeregrineContextProvider';
   import { enhancer, reducers } from '@magento/peregrine/lib/store';
   
   const storage = new BrowserPersistence();
   const store = createStore(combineReducers(reducers), enhancer);
   
   storage.setItem('store_view_code', config.storeView);
   
   const App = () => {
       const [{ sdk: mse }] = useEventCollectorContext();
   
       // trigger page-level events
       useCustomUrlEvent({ mse });
       useReferrerEvent({ mse });
       usePageEvent({ mse });
       // listen for add-to-cart events and enable forwarding to the magento storefront events sdk
       useAddToCartEvent(({ mse }));
       // enable CIF specific event forwarding to the Adobe Client Data Layer
       useDataLayerEvents();
   
       useEffect(() => {
           // implement a proper marketing opt-in, for demo purpose we hard-set the consent cookie
           if (document.cookie.indexOf('mg_dnt') < 0) {
               document.cookie += '; mg_dnt=track';
           }
       }, []);
   
       // TODO: use the App to create Portals and PortalPlaceholders to mount the CIF / Peregrine components to the server side rendered markup
       return <></>;
   };
   
   const AppContext = ({ children }) => {
       const { storeView, graphqlEndpoint, graphqlMethod = 'POST', headers = {}, eventsCollector } = config;
       const { apolloProps } = useAdapter({
           apiUrl: new URL(graphqlEndpoint, window.location.origin).toString(),
           configureLinks: (links, apiBase) =>
               // reconfigure the HTTP link to use the configured graphqlEndpoint, graphqlMethod and storeView header
   
               links.set('HTTP', createHttpLink({
                   fetch: customFetchToShrinkQuery,
                   useGETForQueries: graphqlMethod !== 'POST',
                   uri: apiBase,
                   headers: { ...headers, 'Store': storeView }
               }))
       });
   
       return (
           <ApolloProvider {...apolloProps}>
               <IntlProvider locale='en' messages={{}}>
                   <ConfigContextProvider config={config}>
                       <ReduxProvider store={store}>
                           <PeregrineContextProvider>
                               <EventCollectorContextProvider {...eventsCollector}>
                                   {children}
                               </EventCollectorContextProvider>
                           </PeregrineContextProvider>
                       </ReduxProvider>
                   </ConfigContextProvider>
               </IntlProvider>
           </ApolloProvider>
       );
   };
   
   window.onload = async () => {
       const root = document.createElement('div');
       document.body.appendChild(root);
   
       ReactDOM.render(
           <Router>
               <AppContext>
                   <App />
               </AppContext>
           </Router>,
           root
       );
   };
   ```

   O `EventCollectorContext` exporta o Contexto de Reação que:

   - carrega a biblioteca commerce-events-sdk e commerce-events-collector ,
   - inicializa-os com uma configuração específica para Experience Platform e/ou ACDS
   - se inscreve em todos os eventos do Peregrine e os encaminha para o SDK de eventos

   Você pode revisar os detalhes de implementação da variável `EventCollectorContext` [here](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js).

### Criar e implantar o projeto de AEM atualizado

Para garantir que as alterações de instalação, código e configuração do pacote acima estejam corretas, recrie e implante o projeto AEM Commerce atualizado usando o seguinte comando Maven: `$ mvn clean install -PautoInstallSinglePackage`.

## Configuração do Experience Platform {#aep-setup}

Para receber e armazenar os dados do evento provenientes das páginas de Comércio de AEM, como categoria e produto, execute as seguintes etapas:

>[!AVAILABILITY]
>
>Certifique-se de que você faz parte do __Perfis de produto__ under __Adobe Experience Platform__ e __Coleta de dados do Adobe Experience Platform__. Se necessário, trabalhe com o administrador do sistema para criar, atualizar ou atribuir __Perfis de produto__ nos termos do [Admin Console](https://adminconsole.adobe.com/).

### Criar esquema com grupo de campos Comércio

Para definir a estrutura para dados de evento de comércio, você deve criar um esquema do Experience Data Model (XDM). Um esquema é um conjunto de regras que representam e validam a estrutura e o formato dos dados.

1. No navegador, navegue até o __Adobe Experience Platform__ página inicial do produto. Por exemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Localize a variável __Esquemas__ na seção de navegação à esquerda, clique no botão __Criar esquema__ na seção superior direita e selecione __ExperiênciaEvento XDM__.

   ![Criação de esquema da AEP](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. Nomeie seu esquema usando a variável __Propriedades do esquema > Nome de exibição__ e adicionar Grupos de campos usando o  __Composição > Grupos de campos > Adicionar__ botão.

   ![Definição de esquema AEP](../assets/aep-integration/AEP-Schema-Definition.png)

1. No __Adicionar grupos de campos__ diálogo, pesquisar por `Commerce`, selecione o __Detalhes de comércio__ e clique em __Adicionar grupos de campos__.

   ![Definição de esquema AEP](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>Consulte a [Noções básicas da composição do schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) para obter mais informações.

### Criar conjunto de dados

Para armazenar os dados do evento, você deve criar um Conjunto de dados que esteja em conformidade com a definição do esquema. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas).

1. No navegador, navegue até o __Adobe Experience Platform__ página inicial do produto. Por exemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Localize a variável __Conjuntos de dados__ na seção de navegação à esquerda e clique no botão __Criar conjunto de dados__ na seção superior direita.

   ![Criar conjuntos de dados da AEP](../assets/aep-integration/AEP-Datasets-Create.png)

1. Na nova página, selecione __Criar conjunto de dados a partir do esquema__ cartão.

   ![Opção de esquema Criar conjuntos de dados da AEP](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

- Na nova página, __pesquisar e selecionar__ o esquema criado na etapa anterior e clique no botão __Próximo__ botão.

   ![AEP Criar conjuntos de dados Selecionar esquema](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. Nomeie seu conjunto de dados usando a __Configurar conjunto de dados > Nome__ e clique no botão __Concluir__ botão.

   ![Nome dos conjuntos de dados de criação da AEP](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>Consulte a [Visão geral dos conjuntos de dados](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) para obter mais informações.


### Criar fluxo de dados

Complete as etapas a seguir para criar um Datastream no Experience Platform.

1. No navegador, navegue até o __Adobe Experience Platform__ página inicial do produto. Por exemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Localize a variável __Datastreams__ na seção de navegação à esquerda e clique no botão __Novo fluxo de dados__ na seção superior direita.

   ![Criar conjuntos de dados do AEP](../assets/aep-integration/AEP-Datastream-Create.png)

1. Nomeie seu conjunto de dados usando o __Nome__ campo obrigatório. Em __Esquema do evento__ , selecione o schema recém-criado e clique em __Salvar__.

   ![AEP Define Datastreams](../assets/aep-integration/AEP-Datastream-Define.png)

1. Abra o Datastream recém-criado e clique em __Adicionar Serviço__.

   ![AEP Datastreams Add Service](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. Em __Serviço__ selecione o __Adobe Experience Platform__ opção. Em __Conjunto de dados do evento__ , selecione o nome do conjunto de dados na etapa anterior e clique em __Salvar__.

   ![Detalhes do serviço de adição de conjuntos de dados da AEP](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>Consulte a [Visão geral do fluxo de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) para obter mais informações.

## Adicionar valor de armazenamento de dados à configuração AEM Commerce {#add-aep-values-to-aem}

Após concluir a configuração do Experience Platform acima, você deve ter `datastreamId` no painel à esquerda dos detalhes do Datastream e `orgId` no canto superior direito do __Imagem do perfil > Informações da conta > Informações do usuário__ modal.

![ID de datastreams da AEP](../assets/aep-integration/AEP-Datastream-ID.png)

1. No projeto do AEM Commerce `ui.frontend` , atualize o `config.js` e especificamente o `eventsCollector > aep` propriedades do objeto.

1. Crie e implante o projeto AEM Commerce atualizado


## Acionador `addToCart` evento e verificação da coleta de dados {#event-trigger-verify}

As etapas acima concluem a configuração AEM Commerce e Experience Platform. Agora você pode acionar um `addToCart` e verificar a coleta de dados usando o depurador do Experience Platform e o conjunto de dados __Métricas e gráficos__ alternar na interface do usuário do produto.

Para acionar o evento, você pode usar AEM autor ou o serviço de publicação da configuração local. Neste exemplo, use AEM autor fazendo logon em sua conta.

1. Na página Sites , selecione o __My Demo StoreFront > us > en__ e clique em __Editar__ na barra de ação superior.

1. Na barra de ações superior, clique em __Exibir como publicado__, em seguida, clique em qualquer categoria preferida na navegação da loja.

1. Clique em qualquer cartão de produto preferencial no __Página do produto__, em seguida selecione __cor, tamanho__ para ativar o __Adicionar ao carrinho__ botão.


1. Abra o __Adobe Experience Platform Debugger__ no painel de extensão do navegador e selecione __SDK do Experience Platform Wed__ no painel esquerdo.

   ![Depurador AEP](../assets/aep-integration/AEP-Debugger.png)


1. Retorne ao __Página do produto__ e clique em __Adicionar ao carrinho__ botão. Isso envia dados para o Experience Platform. O __Adobe Experience Platform Debugger__ mostra os detalhes do evento.

   ![Dados de eventos do AEP Debugger Add-To-Cart](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. Na interface do usuário do produto Experience Platform, navegue até o __Conjuntos de dados > Minha loja de demonstraçãoFrente__ nos termos do __Atividade do conjunto de dados__ guia . Se a variável __Métricas e gráficos__ for ativada, as estatísticas de dados de evento serão exibidas.

   ![Estatísticas do conjunto de dados do Experience Platform](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## Detalhes da implementação {#implementation-details}

O [Conector do Experience Platform da CIF](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) é criado sobre o [Conector Experience Platform para Adobe Commerce](https://marketplace.magento.com/magento-experience-platform-connector.html), que faz parte do [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) projeto.

O projeto do PWA Studio permite criar vitrines do Progressive Web Application (PWA) acionadas pela Adobe Commerce ou pelo Magento Open Source. O projeto também contém uma biblioteca de componentes chamada [Peregrino](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) para adicionar lógica aos componentes visuais. O [Biblioteca Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) também fornece os ganchos do React personalizados usados por [Conector Experience Platform](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) para integrar com o Experience Platform sem interrupções.


## Eventos compatíveis {#supported-events}

A partir de agora, os seguintes eventos são compatíveis:

- addToCart
- pageView
- customUrl
- referrerUrl

## Recursos adicionais {#additional-resources}

Para obter mais informações, consulte os seguintes recursos:

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [Visão geral do conector Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html)
- [Visão geral do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)

