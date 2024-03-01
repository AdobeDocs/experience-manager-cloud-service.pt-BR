---
title: Componentes principais e integração Adobe Experience Platform-CIF AEM
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
source-git-commit: 05e4adb0d7ada0f7cea98858229484bf8cca0d16
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 1%

---


# Componentes principais do AEM-CIF e integração com o Adobe Experience Platform {#aem-cif-aep-integration}

Os [componentes principais da estrutura de integração Comércio (CIF)](https://github.com/adobe/aem-core-cif-components) fornecem integração perfeita com [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) para encaminhar eventos de vitrine e seus dados a partir de interações lado do cliente como __adicionar a carrinho__.

O [projeto AEM Componentes](https://github.com/adobe/aem-core-cif-components) principais de CIF fornece uma JavaScript biblioteca chamada [Adobe Experience Platform conector para Adobe Systems Comércio](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) coletar dados do evento da sua vitrine Comércio. Essa dados do evento é enviada para o Experience Platform onde é usada em outros Adobe Experience Cloud produtos, como Adobe Analytics e Adobe Target para build um perfil de 360 graus que abrange um jornada do cliente. Ao conectar Comércio dados a outros produtos no Adobe Experience Cloud, é possível realizar tarefas curtir analisar usuário comportamento em seu site, realizar Teste AB e criar campanhas personalizadas.

Saiba mais sobre o [conjunto Experience Platform de coleção](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) de dados das tecnologias que permite coletar experiência do cliente dados de fontes lado do cliente.

## Enviar `addToCart` dados do evento para Experience Platform {#send-addtocart-to-aep}

As etapas a seguir mostram como enviar a `addToCart` dados de evento de páginas de produto renderizadas por AEM para o Experience Platform usando o Conector CIF - Experience Platform. Usando a extensão do navegador Adobe Experience Platform Debugger, você pode testar e revisar os dados enviados.

![Revisar dados do evento addToCart no Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)

## Pré-requisitos {#prerequisites}

Use um ambiente de desenvolvimento local para concluir esta demonstração. Isso inclui uma instância de execução de AEM configuradas e conectadas a uma Adobe Systems Comércio instância. Revise os requisitos e as etapas para [configurar o desenvolvimento local com AEM como um SDK](../develop.md) Cloud Service.

Você também precisa de acesso a [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) e permissões para criar schema, conjunto de dados e fluxos de dados para coleção de dados. Para obter mais informações, consulte [Gerenciamento de permissões](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## AEM Comércio como uma configuração Cloud Service {#aem-setup}

Para ter um AEM Comércio de trabalho __como Cloud Service__ ambiente local com o código e a configuração necessários, conclua as seguintes etapas.

### Configuração local

Siga as [Configuração local](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) etapas para que você possa ter um ambiente as a Cloud Service de comércio AEM em funcionamento.

### Configuração do projeto

Siga as [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) etapas para criar um novo projeto de comércio de AEM (CIF).

>[!TIP]
>
>No exemplo a seguir, o AEM Comércio projeto é nomeado: `My Demo Storefront`, no entanto, você pode escolher seu próprio nome de projeto.

![Projeto do AEM Comércio](../assets/aep-integration/aem-project-with-commerce.png)


Crie e implante o projeto de comércio do AEM criado no SDK AEM local executando o seguinte comando no diretório raiz do projeto.

```bash
$ mvn clean install -PautoInstallSinglePackage
```

A implantação local `My Demo StoreFront` o site de comércio eletrônico com código e conteúdo padrão é semelhante ao seguinte:

![Site padrão de comércio AEM](../assets/aep-integration/demo-aem-storefront.png)

### Instalar dependências de conector Peregrine e CIF-AEP

Para coletar e enviar os dados do evento das páginas de categoria e produto deste site do AEM Commerce, instale a chave `npm` pacotes na `ui.frontend` módulo do projeto AEM Commerce.

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
>Às `--force` vezes, o argumento é necessário, pois [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) é restritivo com as dependências de pares suportadas. Normalmente, isso não deve causar problemas.


### Configurar o Maven para usar `--force` o argumento

Como parte do processo de build do Maven, a instalação limpa npm (usando `npm ci`) é acionada. Isso também requer o `--force` argumento.

Navegue até o arquivo `pom.xml` POM raiz do projeto e localize o `<id>npm ci</id>` bloco de execução. Atualize o bloco para que ele tenha uma aparência curtir o seguinte:

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

### Alterar formato de configuração Babel

Alterne do formato de arquivo de configuração relativo do arquivo padrão `.babelrc` para o `babel.config.js` formato. Esse é um formato de configuração para todo o projeto e permite que os plug-ins e predefinições sejam aplicados com `node_module` maior controle.

1. Navegue até o `ui.frontend` módulo e exclua o arquivo existente `.babelrc` .

1. Criar um `babel.config.js` arquivo que usa a predefinição `peregrine` .

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

### Configurar webpack para usar Babel

Para transpilar os arquivos JavaScript usando babel loader (`babel-loader`) e webpack, edite o `webpack.common.js` arquivo.

Navegue até a `ui.frontend` módulo e atualize o `webpack.common.js` arquivo para que você possa ter as seguintes regra dentro do `module` valor propriedade:

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### Configurar o Cliente Apollo

A variável [Cliente Apollo](https://www.apollographql.com/docs/react/) O é usado para gerenciar dados locais e remotos com o GraphQL. Ele também armazena os resultados de consultas do GraphQL em um cache local normalizado na memória.

Para [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) para trabalhar com eficiência, você precisa de uma `possibleTypes.js` arquivo. Para gerar esse arquivo, consulte [Geração de possíveis tipos automaticamente](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically). Além disso, consulte o [PWA Studio de referência implementação](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) e um exemplo de arquivo [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js) .


1. Navegue até o `ui.frontend` módulo e salve o arquivo como `./src/main/possibleTypes.js`

1. Atualize a `webpack.common.js` seção do `DefinePlugin` arquivo para que você possa substituir as variáveis estáticas necessárias durante build tempo.

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

### Inicializar componentes principais de Peregrino e CIF

Para inicializar os componentes principais de Peregrine e CIF baseados em Reação, crie a configuração necessária e os arquivos JavaScript.

1. Navegue até o `ui.frontend` módulo e crie a seguinte pasta: `src/main/webpack/components/commerce/App`

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
           eventForwarding: {
               acds: true,
               aep: false,
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >Embora você já esteja familiarizado com o [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) arquivo de __Guias do AEM - Projeto CIF Venia__, há algumas alterações que você deve fazer nesse arquivo. Primeiro, analise qualquer __TODO__ comentários. Em seguida, dentro do `eventsCollector` propriedade, localize o `eventsCollector > aep` objeto e atualizar o `orgId` e `datastreamId` aos valores corretos. [Saiba mais](./aep.md#add-aep-values-to-aem).

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
           // implement a proper marketing opt-in, for demo purpose you hard-set the consent cookie
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

   Exporta `EventCollectorContext` o Contexto de reação que:

   - carrega o commerce-events-sdk e o commerce-events-collector biblioteca,
   - as inicializa com uma determinada configuração para Experience Platform e/ou ACDS
   - inscreve todos os eventos de Peregrine e os encaminha para o SDK de eventos

   Você pode analisar os detalhes implementação aqui `EventCollectorContext` [](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js).

### Criar e implantar o projeto AEM atualizado

Para garantir que as alterações de instalação, código e configuração do pacote acima estejam corretas, recrie e implante o projeto atualizado do Comércio de AEM usando o seguinte comando Maven: `$ mvn clean install -PautoInstallSinglePackage`.

## configuração do Experience Platform {#aep-setup}

Para receber e armazenamento os dados do evento provenientes das páginas AEM Comércio como categoria e produtos, conclua as seguintes etapas:

>[!AVAILABILITY]
>
>Certifique-se de fazer parte dos Perfis de produto corretos ____ em __Adobe Experience Platform__ e __Adobe Experience Platform coleta__ de dados. Se necessário, trabalhe com o administrador do sistema para criar, atualizar ou atribuir __perfis__ de produto à [Admin Console](https://adminconsole.adobe.com/).

### Criar esquema com o grupo de campos Comércio

Para definir a estrutura para dados de evento de comércio, você deve criar um esquema do Experience Data Model (XDM). Uma schema é um conjunto de regras que representam e validam a estrutura e o formato dos dados.

1. No navegador, navegue até a janela __Adobe Experience Platform__ Página inicial do produto. Por exemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Localize o __Esquemas__ na seção de navegação à esquerda, clique na guia __Criar esquema__ na seção superior direita e selecione __XDM ExperienceEvent__.

   ![Criar esquema da AEP](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. Nomeie sua schema usando o __campo Esquema Propriedades > Nome de exibição__ e adicione grupos de Campos usando os  __grupos de Campo de > composição > Adicionar__ botão.

   ![Definição do esquema AEP](../assets/aep-integration/AEP-Schema-Definition.png)

1. __Na caixa de diálogo Adicionar grupos de campo__, pesquisa for`Commerce`, selecione a caixa de seleção __Comércio Detalhes__ e clique __em Adicionar grupos de campo__.

   ![Definição do esquema AEP](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>Consulte as noções [básicas de schema composição](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) para obter mais informações.

### Criar conjunto de dados

Para armazenar os dados do evento, você deve criar um Conjunto de dados que esteja em conformidade com a definição do esquema. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados — normalmente uma tabela — que contém um esquema (colunas) e campos (linhas).

1. No navegador, navegue até a janela __Adobe Experience Platform__ Página inicial do produto. Por exemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Localize o __menu Conjuntos__ de dados na seção de navegação esquerda e clique na __Criar conjunto de dados__ botão na seção superior direita.

   ![Conjuntos de dados do AEP Criar](../assets/aep-integration/AEP-Datasets-Create.png)

1. Na nova página, selecione __Criar conjunto de dados a partir do esquema__ cartão.

   ![Opção Criar esquema de conjuntos de dados da AEP](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

   Na nova página, __pesquisar e selecionar__ o schema criado na etapa anterior e clique em __Próxima__ botão.

   ![Criar conjuntos de dados da AEP Selecionar esquema](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. Nomeie seu conjunto de dados usando o __Configurar conjunto de dados > Nome__ e clique no botão __Concluir__ botão.

   ![Nome dos conjuntos de dados do AEP Criar](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>Consulte a visão geral](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) dos [conjuntos de dados para obter mais informações.


### Datastream do Criar

Todos os Apps as etapas a seguir para poder criar uma sequência de dados no Experience Platform.

1. No navegador, navegue até o página inicial do __produto Adobe Experience Platform__ . Por exemplo, <https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>.

1. Localize o __menu Datastreams__ na seção de navegação esquerda e clique no __Novo datastream__ botão na seção superior direita.

   ![Fluxos de dados do AEP Criar](../assets/aep-integration/AEP-Datastream-Create.png)

1. Nomeie seu datastream usando o __campo Nome__ obrigatório. __No campo Esquema__ de eventos, selecione a schema criada e clique __Salvar__.

   ![Definir datastreams da AEP](../assets/aep-integration/AEP-Datastream-Define.png)

1. Abra a sequência de dados criada e clique __em Adicionar serviço__.

   ![Serviço de adição de fluxos de dados AEP](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. __No campo Serviço__, selecione a opção __Adobe Experience Platform__. No __campo Conjunto de dados__ do evento, selecione o nome da conjunto de dados na etapa anterior e clique __Salvar__.

   ![Fluxos de dados do AEP adicionam detalhes do serviço](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>Consulte a [Visão geral da sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) para obter mais informações.

## Adicionar valor de sequência de dados à configuração do AEM Commerce {#add-aep-values-to-aem}

Depois de concluir a configuração Experience Platform acima, você deve ter `datastreamId` na painel à esquerda dos detalhes do Datastream e `orgId` no canto superior direito do __perfil Imagem > informações de conta > modal de Informações__ do usuário.

![ID de fluxos de dados do AEP](../assets/aep-integration/AEP-Datastream-ID.png)

1. Na módulo do `ui.frontend` projeto AEM Comércio, atualize o `config.js` arquivo e especificamente as propriedades do `eventsCollector > aep` objeto.

1. Criar e implantar o projeto de AEM Comércio atualizado


## Acione `addToCart` evento e verifique coleção de dados {#event-trigger-verify}

As etapas acima completam o AEM Comércio e a configuração Experience Platform. Agora você pode acionar uma `addToCart` evento e verificar coleção de dados usando a extensão _Google Cromo Snowplow Inspector_ e conjunto de dados __Metrics and graphs__ alternar no interface do produto.

Para acionar o evento, você pode usar o autor de AEM ou o serviço de publicação da configuração local. Para este exemplo, use AEM autor fazendo logon na conta.

1. Na página Sites, selecione a __Minha loja de demonstraçãoFront > nós > pt-BR__ e clique em __Editar__ na barra de ação superior.

1. Na barra de ação superior, clique em __Exibir como publicado__, em seguida, clique em qualquer categoria preferencial na navegação da loja.

1. Clique em qualquer cartão de produto preferido no __Página do produto__ e selecione __cor, tamanho__ para habilitar o __Adicionar ao carrinho__ botão.


1. Abra a __extensão Inspetor__ Snowplow no painel de extensão do navegador e selecione __Experience Platform SDK__ do Wed na painel esquerda.


1. Retorne ao __Página__ Produto e clique __em Adicionar ao carrinho botão__ . Isso envia dados para o Experience Platform. A __extensão Adobe Experience Platform Debugger__ mostra os detalhes do evento.

   ![Dados de evento do depurador da AEP adicionados ao carrinho](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. Na interface do usuário do produto Experience Platform, acesse __Conjuntos de dados > My Demo StoreFront__, no âmbito do __Atividade do conjunto de dados__ guia. Se __Métricas e gráficos__ for ativado, as estatísticas de dados do evento serão exibidas.

   ![Estatísticas de dados do conjunto de dados Experience Platform](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## Detalhes da implementação {#implementation-details}

O [CIF Experience Platform Connector](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) é construído sobre a [Conexão de dados para Adobe Systems Comércio](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html), que faz parte do [projeto PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) .

O projeto PWA Studio permite criar vitrines Progressive Web Application (PWA) fornecidas por Adobe Systems Comércio ou Magento Open Source. O projeto também contém um componente biblioteca chamado [Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) para adicionar lógica a componentes visuais. O [biblioteca](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) Peregrin também fornece os ganchos React personalizados que são usados pelo [CIF Experience Platform Connector](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) para integrar a Experience Platform perfeitamente.


## Eventos suportados {#supported-events}

A partir de agora, os seguintes eventos são suportados:

__Eventos de experiência XDM:__

1. Adicionar ao carrinho (AEM)
1. Visualizar página (AEM)
1. Exibir produto (AEM)
1. Solicitação Search enviada (AEM)
1. Resposta Search recebida (AEM)

Quando [os componentes Peregrinos](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/) são reutilizados no projeto AEM Comércio:

__Eventos de experiência XDM:__

1. Remover do carrinho
1. Abrir carrinho
1. Exibir carrinho
1. Compra instantânea
1. Check-out do Início
1. Check-out do Todos os Apps

__Eventos XDM de perfil:__

1. Fazer logon
1. Criar conta
1. Editar conta


## Recursos adicionais {#additional-resources}

Para obter mais informações, consulte os seguintes recursos:

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [[!DNL Data Connection] Visão geral](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html)
- [[!DNL Data Connection] Eventos](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)
- [Visão geral Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)
