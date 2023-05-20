---
title: Componentes principais do AEM-CIF e integração com o Adobe Experience Platform
description: Saiba como enviar dados do evento da loja de uma página de produto renderizada por AEM para o Experience Platform usando o Conector CIF - Experience Platform.
sub-product: Commerce
version: Cloud Service
activity: setup
feature: Commerce Integration Framework
topic: Commerce
role: Architect, Developer
level: Beginner
kt: 10834
thumbnail: 346811.jpeg
exl-id: 30bb9b2c-5f00-488e-ad5c-9af7cd2c4735
source-git-commit: 73fe6ce5bbdf0ad437ae4b47b892ad05e016ab68
workflow-type: tm+mt
source-wordcount: '2080'
ht-degree: 1%

---

# Componentes principais do AEM-CIF e integração com o Adobe Experience Platform {#aem-cif-aep-integration}

A variável [Commerce Integration Framework (CIF)](https://github.com/adobe/aem-core-cif-components) Os componentes principais fornecem integração perfeita com [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) para encaminhar eventos da loja e seus dados de interações do lado do cliente, como __adicionar ao carrinho__.

A variável [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) O projeto fornece uma biblioteca JavaScript chamada [Conector do Adobe Experience Platform para Adobe Commerce](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) para coletar dados do evento na sua loja do Commerce. Esses dados de evento são enviados para o Experience Platform onde são usados em outros produtos da Adobe Experience Cloud, como Adobe Analytics e Adobe Target, para criar um perfil de 360 graus que cobre uma jornada do cliente. Conectando os dados do Commerce a outros produtos na Adobe Experience Cloud, você pode executar tarefas como analisar o comportamento do usuário no seu site, executar testes AB e criar campanhas personalizadas.

Saiba mais sobre o [Coleta de dados Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) conjunto de tecnologias que permitem coletar dados de experiência do cliente de fontes do lado do cliente.

## Enviar `addToCart` dados do evento para Experience Platform {#send-addtocart-to-aep}

As etapas a seguir mostram como enviar a `addToCart` dados de evento de páginas de produto renderizadas pelo AEM para o Experience Platform usando o Conector CIF - Experience Platform. Usando a extensão de navegador do Adobe Experience Platform Debugger, você pode testar e revisar os dados enviados.

![Revisar dados do evento addToCart no Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)

## Pré-requisitos {#prerequisites}

Você deve usar um ambiente de desenvolvimento local para concluir esta demonstração. Isso inclui uma instância do AEM em execução que está configurada e conectada a uma instância do Adobe Commerce. Revise os requisitos e as etapas para [configuração do desenvolvimento local com o SDK as a Cloud Service do AEM](../develop.md).

Você também precisa de acesso ao [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) e permissões para criar o esquema, o conjunto de dados e as sequências de dados para a coleta de dados. Para obter mais informações, consulte [Gerenciamento de permissões](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Configuração as a Cloud Service do AEM Commerce {#aem-setup}

Para ter uma __AEM Commerce as a Cloud Service__ ambiente local com o código e a configuração necessários, conclua as etapas a seguir.

### Configuração local

Siga as [Configuração local](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) etapas para ter um ambiente as a Cloud Service de comércio AEM em funcionamento.

### Configuração do projeto

Siga as [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) etapas para criar um novo projeto de comércio de AEM (CIF).

>[!TIP]
>
>No exemplo a seguir, o projeto de comércio do AEM é denominado: `My Demo Storefront`No entanto, você pode escolher seu próprio nome de projeto.

![Projeto de comércio AEM](../assets/aep-integration/aem-project-with-commerce.png)


Crie e implante o projeto de comércio do AEM recém-criado no SDK AEM local executando o seguinte comando no diretório raiz do projeto.

```bash
$ mvn clean install -PautoInstallSinglePackage
```

A implantação local `My Demo StoreFront` o site de comércio eletrônico com código e conteúdo padrão é semelhante ao seguinte:

![Site padrão de comércio AEM](../assets/aep-integration/demo-aem-storefront.png)

### Instalar dependências de conectores Peregrine e CIF-AEP

Para coletar e enviar os dados do evento das páginas de categoria e produto deste site do AEM Commerce, é necessário instalar a chave `npm` pacotes na `ui.frontend` módulo do projeto AEM Commerce.

Navegue até a `ui.frontend` e instale os pacotes necessários executando os seguintes comandos na linha de comando.

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
>A variável `--force` O argumento às vezes é necessário, pois [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) é restritivo com as dependências de mesmo nível compatíveis. Normalmente, isso não deve causar problemas.


### Configurar Maven para usar `--force` argumento

Como parte do processo de build do Maven, a instalação npm clean (usando `npm ci`) é acionado. Isso também exige que os `--force` argumento.

Navegue até o arquivo POM raiz do projeto `pom.xml` e localize o `<id>npm ci</id>` bloco de execução. Atualize o bloco para que tenha a seguinte aparência:

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

Alternar do padrão `.babelrc` formato do arquivo de configuração relativo ao arquivo para `babel.config.js` formato. Este é um formato de configuração para todo o projeto e permite que plug-ins e predefinições sejam aplicados à `node_module` com maior controle.

1. Navegue até a `ui.frontend` módulo e excluir o existente `.babelrc` arquivo.

1. Criar um `babel.config.js` arquivo que usa o `peregrine` predefinição.

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

### Configurar o webpack para usar o Babel

Para transcompilar os arquivos JavaScript usando o carregador Babel (`babel-loader`) e webpack, é necessário modificar o `webpack.common.js` arquivo.

Navegue até a `ui.frontend` módulo e atualize o `webpack.common.js` para que a seguinte regra esteja no estado `module` valor da propriedade:

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### Configurar cliente Apollo

A variável [Cliente Apollo](https://www.apollographql.com/docs/react/) O é usado para gerenciar dados locais e remotos com o GraphQL. Ele também armazena os resultados de consultas do GraphQL em um cache local normalizado na memória.

Para [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) para trabalhar com eficiência, você precisa de uma `possibleTypes.js` arquivo. Para gerar esse arquivo, consulte [Gerando possibleTypes automaticamente](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically). Além disso, consulte a [Implementação de referência do PWA Studio](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) e um exemplo de um [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js) arquivo.


1. Navegue até a `ui.frontend` e salve o arquivo como `./src/main/possibleTypes.js`

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

### Inicializar os componentes principais de Peregrine e CIF

Para inicializar os componentes principais do Peregrine e da CIF baseados no React, crie a configuração necessária e os arquivos JavaScript.

1. Navegue até a `ui.frontend` e crie a seguinte pasta: `src/main/webpack/components/commerce/App`

1. Criar um `config.js` arquivo com o seguinte conteúdo:

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
   >Embora você já esteja familiarizado com o [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) arquivo de __Guias do AEM - Projeto CIF Venia__, há algumas alterações que você precisa fazer nesse arquivo. Primeiro, analise qualquer __TODO__ comentários. Em seguida, dentro do `eventsCollector` propriedade, localize o `eventsCollector > aed` objeto e atualizar o `orgId` e `datastreamId` aos valores corretos. [Saiba mais](./aep.md#add-aep-values-to-aem).

1. Criar um `App.js` com o seguinte conteúdo. Esse arquivo se assemelha a um arquivo de ponto de partida típico do aplicativo React e contém ganchos React e personalizados e uso de Contexto React para facilitar a integração de Experience Platform.

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

   A variável `EventCollectorContext` exporta o React Context que:

   - carrega a biblioteca commerce-events-sdk e commerce-events-collector,
   - inicializa com uma determinada configuração para Experience Platform e/ou ACDS
   - assina todos os eventos do Peregrine e os encaminha para o SDK de eventos

   Você pode revisar os detalhes de implementação da `EventCollectorContext` [aqui](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js).

### Criar e implantar o projeto AEM atualizado

Para garantir que as alterações de instalação, código e configuração do pacote acima estejam corretas, recrie e implante o projeto atualizado do Comércio de AEM usando o seguinte comando Maven: `$ mvn clean install -PautoInstallSinglePackage`.

## configuração do Experience Platform {#aep-setup}

Para receber e armazenar os dados do evento provenientes das páginas do AEM Commerce, como categoria e produto, conclua as seguintes etapas:

>[!AVAILABILITY]
>
>Certifique-se de fazer parte do __Perfis de produto__ em __Adobe Experience Platform__ e __Coleta de dados do Adobe Experience Platform__. Se necessário, trabalhe com o administrador do sistema para criar, atualizar ou atribuir __Perfis de produto__ no [Admin Console](https://adminconsole.adobe.com/).

### Criar esquema com o grupo de campos Comércio

Para definir a estrutura para dados de evento de comércio, você deve criar um esquema do Experience Data Model (XDM). Um esquema é um conjunto de regras que representam e validam a estrutura e o formato dos dados.

1. No navegador, navegue até a janela __Adobe Experience Platform__ Página inicial do produto. Por exemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Localize o __Esquemas__ na seção de navegação à esquerda, clique na guia __Criar esquema__ na seção superior direita e selecione __XDM ExperienceEvent__.

   ![Criar esquema da AEP](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. Nomeie seu esquema usando o __Propriedades do esquema > Nome de exibição__ e adicionar Grupos de campos usando o  __Composição > Grupos de campos > Adicionar__ botão.

   ![Definição de esquema da AEP](../assets/aep-integration/AEP-Schema-Definition.png)

1. No __Adicionar grupos de campos__ , pesquisar `Commerce`, selecione o __Detalhes do comércio__ e clique em __Adicionar grupos de campos__.

   ![Definição de esquema da AEP](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>Consulte a [Noções básicas da composição do esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) para obter mais informações.

### Criar conjunto de dados

Para armazenar os dados do evento, você deve criar um Conjunto de dados que esteja em conformidade com a definição do esquema. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas).

1. No navegador, navegue até a janela __Adobe Experience Platform__ Página inicial do produto. Por exemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Localize o __Conjuntos de dados__ na seção de navegação à esquerda e clique no botão __Criar conjunto de dados__ na seção superior direita.

   ![Criar conjuntos de dados da AEP](../assets/aep-integration/AEP-Datasets-Create.png)

1. Na nova página, selecione __Criar conjunto de dados a partir do esquema__ cartão.

   ![Opção Criar esquema de conjuntos de dados da AEP](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

- Na nova página, __pesquisar e selecionar__ o schema criado na etapa anterior e clique em __Próxima__ botão.

   ![Criar conjuntos de dados da AEP Selecionar esquema](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. Nomeie seu conjunto de dados usando o __Configurar conjunto de dados > Nome__ e clique no botão __Concluir__ botão.

   ![Nome do conjunto de dados de criação da AEP](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>Consulte a [Visão geral dos conjuntos de dados](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) para obter mais informações.


### Criar sequência de dados

Conclua as etapas a seguir para criar uma sequência de dados no Experience Platform.

1. No navegador, navegue até a janela __Adobe Experience Platform__ Página inicial do produto. Por exemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Localize o __Datastreams__ na seção de navegação à esquerda e clique no botão __Nova sequência de dados__ na seção superior direita.

   ![Criar fluxos de dados da AEP](../assets/aep-integration/AEP-Datastream-Create.png)

1. Nomeie sua sequência de dados usando o __Nome__ campo obrigatório. No __Esquema de evento__ selecione o esquema recém-criado e clique em __Salvar__.

   ![Definir fluxos de dados AEP](../assets/aep-integration/AEP-Datastream-Define.png)

1. Abra o Datastream recém-criado e clique em __Adicionar serviço__.

   ![Adicionar serviço de fluxos de dados da AEP](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. No __Serviço__ selecione o __Adobe Experience Platform__ opção. Em __Conjunto de dados do evento__ selecione o nome do conjunto de dados na etapa anterior e clique em __Salvar__.

   ![Detalhes do serviço de adição de fluxos de dados da AEP](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>Consulte a [Visão geral da sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) para obter mais informações.

## Adicionar valor de sequência de dados à configuração do AEM Commerce {#add-aep-values-to-aem}

Após concluir a configuração do Experience Platform acima, você deve ter `datastreamId` no painel à esquerda dos detalhes do fluxo de dados e `orgId` no canto superior direito da __Imagem do perfil > Informações da conta > Informações do usuário__ modal.

![ID de fluxos de dados da AEP](../assets/aep-integration/AEP-Datastream-ID.png)

1. No relatório do projeto AEM Commerce `ui.frontend` módulo, atualize o `config.js` arquivo e especificamente o `eventsCollector > aep` propriedades do objeto.

1. Criar e implantar o projeto atualizado do AEM Commerce


## Acionador `addToCart` evento e verificação da coleta de dados {#event-trigger-verify}

As etapas acima concluem a configuração do AEM Commerce e Experience Platform. Agora você pode acionar um `addToCart` evento e verificar a coleta de dados usando o depurador e o conjunto de dados do Experience Platform __Métricas e gráficos__ alternar na interface do usuário do produto.

Para acionar o evento, você pode usar o autor de AEM ou o serviço de publicação da configuração local. Neste exemplo, use o autor de AEM para fazer logon em sua conta.

1. Na página Sites, selecione a __Minha loja de demonstraçãoFront > nós > pt-BR__ e clique em __Editar__ na barra de ação superior.

1. Na barra de ação superior, clique em __Exibir como publicado__, em seguida, clique em qualquer categoria preferencial na navegação da loja.

1. Clique em qualquer cartão de produto preferido no __Página do produto__ e selecione __cor, tamanho__ para habilitar o __Adicionar ao carrinho__ botão.


1. Abra o __Adobe Experience Platform Debugger__ extensão no painel de extensão do navegador e selecione __Experience Platform Wed SDK__ no painel esquerdo.

   ![Depurador da AEP](../assets/aep-integration/AEP-Debugger.png)


1. Retorne para a __Página do produto__ e clique em __Adicionar ao carrinho__ botão. Isso envia dados para o Experience Platform. A variável __Adobe Experience Platform Debugger__ A extensão do mostra os detalhes do evento.

   ![Dados de evento do depurador da AEP adicionados ao carrinho](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. Na interface do produto Experience Platform, navegue até o __Conjuntos de dados > My Demo StoreFront__, no âmbito do __Atividade do conjunto de dados__ guia. Se a variável __Métricas e gráficos__ for ativado, as estatísticas de dados do evento serão exibidas.

   ![Estatísticas de dados do conjunto de dados Experience Platform](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## Detalhes da implementação {#implementation-details}

A variável [Conector de Experience Platform da CIF](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) O é criado sobre o [Conector Experience Platform para Adobe Commerce](https://marketplace.magento.com/magento-experience-platform-connector.html), que faz parte da [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) projeto.

O projeto PWA Studio permite criar vitrines de Progressive Web Application (PWA) alimentadas por Adobe Commerce ou Magento Open Source. O projeto também contém uma biblioteca de componentes chamada [Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) para adicionar lógica aos componentes visuais. A variável [Biblioteca Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) também fornece os ganchos personalizados do React usados pelo [Conector Experience Platform](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) para integrar com o Experience Platform sem interrupções.


## Eventos suportados {#supported-events}

A partir de agora, os seguintes eventos serão compatíveis:

__Eventos XDM da experiência:__

1. Adicionar ao carrinho (AEM)
1. Visualizar página (AEM)
1. Exibir produto (AEM)
1. Solicitação de pesquisa enviada (AEM)
1. Resposta de pesquisa recebida (AEM)

Quando [Componentes Peregrine](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/) são reutilizados no projeto AEM Commerce:

__Eventos XDM da experiência:__

1. Remover do carrinho
1. Abrir carrinho
1. Exibir carrinho
1. Compra instantânea
1. Iniciar check-out
1. Concluir check-out

__Eventos XDM do perfil:__

1. Conectar
1. Criar conta
1. Editar conta


## Recursos adicionais {#additional-resources}

Para obter mais informações, consulte os seguintes recursos:

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [Visão geral do conector Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html)
- [Eventos do conector Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/event-forwarding/events.html)
- [Visão geral do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)
