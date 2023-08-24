---
title: Seletor de ativos para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Use o Seletor de ativos para pesquisar, localizar e recuperar metadados e representações de ativos no aplicativo.
contentOwner: Adobe
role: Admin,User
exl-id: b968f63d-99df-4ec6-a9c9-ddb77610e258
source-git-commit: dd923ae9d63f1ca1379d8e177ff7b00648da052a
workflow-type: tm+mt
source-wordcount: '2373'
ht-degree: 91%

---

# Seletor de ativos de micro front-end {#Overview}

O Seletor de ativos de micro front-end fornece uma interface do usuário que se integra facilmente ao repositório [!DNL Experience Manager Assets as a Cloud Service] para navegar ou pesquisar ativos digitais disponíveis no repositório e usá-los na experiência de criação do aplicativo.

A interface do usuário de micro front-end é disponibilizada em sua experiência de aplicativo usando o pacote de Seletor de ativos. Quaisquer atualizações no pacote são automaticamente importadas e o Seletor de ativos implantado mais recente é automaticamente carregado no aplicativo.

![Visão geral](assets/overview.png)

O Seletor de ativos oferece muitos benefícios, como:

* Facilidade de integração com qualquer um dos aplicativos Adobe ou não-Adobe usando a biblioteca JavaScript Vanilla.
* Manutenção facilitada, pois as atualizações do pacote do Seletor de ativos são implantadas automaticamente no Seletor de ativos disponível para seu aplicativo. Não há atualizações necessárias no aplicativo para carregar as modificações mais recentes.
* Facilidade de personalização, pois há propriedades disponíveis que controlam a exibição do Seletor de ativos no aplicativo.

* Filtros de pesquisa de texto completo, prontos para uso e personalizados que navegam rapidamente até os ativos para uso na experiência de criação.

* Capacidade de alternar repositórios em uma organização IMS para seleção de ativos.

* Capacidade de classificar ativos por nome, dimensões e tamanho e visualizá-los na exibição de Lista, Grade, Galeria ou Cascata.

O escopo deste artigo é demonstrar como usar o Seletor de ativos com um aplicativo [!DNL Adobe] no Unified Shell ou quando já tiver um imsToken gerado para autenticação. Esses fluxos de trabalho são chamados de fluxo não SUSI neste artigo.

Execute as seguintes tarefas para integrar e usar o Seletor de ativos com o seu repositório [!DNL Experience Manager Assets as a Cloud Service]:

* [Integrar o Seletor de ativos usando o Vanilla JS](#integration-with-vanilla-js)
* [Definir propriedades de exibição do Seletor de ativos](#asset-selector-properties)
* [Usar o Seletor de ativos](#using-asset-selector)

## Integrar o Seletor de ativos usando o Vanilla JS {#integration-with-vanilla-js}

É possível integrar qualquer [!DNL Adobe] ou aplicativo fora da Adobe com o repositório [!DNL Experience Manager Assets] as a [!DNL Cloud Service] no aplicativo.

A integração é feita importando o pacote do Seletor de ativos e conectando ao Assets as a Cloud Service usando a biblioteca JavaScript Vanilla. É necessário editar um `index.html` ou qualquer arquivo apropriado em seu aplicativo para:

* Definir os detalhes de autenticação
* Acessar o repositório do Assets as a Cloud Service
* Configurar as propriedades de exibição do Seletor de ativos

<!--
Asset Selector supports authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS) properties such as `imsScope` or `imsClientID`. Authentication using these IMS properties is referred to as SUSI (Sign Up Sign In) flow in this article.

You can perform authentication without defining some of the IMS properties, such as `imsScope` or `imsClientID`, if:

*   You are integrating an [!DNL Adobe] application on [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=en).
*   You already have an IMS token generated for authentication.

Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining `imsScope` or `imsClientID` IMS properties is referred to as a non-SUSI flow in this article.
-->

É possível executar a autenticação sem definir algumas das propriedades do IMS, se:

* Está integrando um aplicativo [!DNL Adobe] no [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=pt-BR).
* Você já tem um token IMS gerado para autenticação.

## Pré-requisitos {#prerequisites}

<!--
If your application requires user based authentication, out-of-the-box Asset Selector also supports a flow for authentication to the [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository using Identity Management System (IMS.)

You can use properties such as `imsScope` or `imsClientID` to retrieve `imsToken` automatically. You can use SUSI (Sign Up Sign In) flow and IMS properties. Also, you can obtain your own imsToken and pass it to Asset Selector by integrating within [!DNL Adobe] application on Unified Shell or if you already have an imsToken obtained via other methods (for example, using technical account). Accessing [!DNL Experience Manager Assets] as a [!DNL Cloud Service] repository without defining IMS properties (For example, `imsScope` and `imsClientID`) is referred to as a non-SUSI flow.
-->

Defina os pré-requisitos no arquivo `index.html` ou em um arquivo semelhante na implementação do aplicativo para definir os detalhes de autenticação e acessar o repositório do [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. Os pré-requisitos incluem:

* imsOrg
* imsToken
* apikey
<!--
The prerequisites vary if you are authenticating using a SUSI flow or a non-SUSI flow.

**Non-SUSI flow**

*   imsOrg
*   imsToken
*   apikey

For more information on these properties, see [Asset Selector Properties](#asset-selector-properties).

**SUSI flow**

*   imsClientId
*   imsScope
*   redirectUrl
*   imsOrg
*   apikey

For more information on these properties, see [Example for the SUSI flow](#susi-vanilla) and [Asset Selector Properties](#asset-selector-properties).
-->

## Instalação {#installation}

Os Seletores de ativos estão disponíveis por meio das versões CDN (por exemplo, [esm.sh](https://esm.sh/)/[Skypack](https://www.skypack.dev/)) e [UMD](https://github.com/umdjs/umd) do ESM.

Nos navegadores usando a **Versão UMD** (recomendado):

```
<script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>

<script>
  const { renderAssetSelector } = PureJSSelectors;
</script>
```

Em navegadores com suporte a `import maps` usando a **Versão CDN do ESM**:

```
<script type="module">
  import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
</script>
```

No Deno/Webpack Module Federation usando a **Versão CDN do ESM**:

```
import { AssetSelector } from 'https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/@assets/selectors/index.js'
```

### Tipo de ativo selecionado {#selected-asset-type}

O Tipo de ativo selecionado é uma matriz de objetos que contém as informações do ativo ao usar as funções `handleSelection`, `handleAssetSelection`, e `onDrop`.

**Sintaxe do esquema**

```
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
```

A tabela a seguir descreve algumas das propriedades importantes do objeto de ativo selecionado.

| Propriedade | Tipo | Explicação |
|---|---|---|
| *repo:repositoryId* | string | Identificador exclusivo do repositório onde o ativo está armazenado. |
| *repo:id* | string | Identificador exclusivo do ativo. |
| *repo:assetClass* | string | A classificação do ativo (por exemplo, imagem, vídeo ou documento). |
| *repo:name* | string | O nome do ativo, incluindo a extensão de arquivo. |
| *repo:size* | número | O tamanho do ativo em bytes. |
| *repo:path* | string | O local do ativo no repositório. |
| *repo:ancestors* | `Array<string>` | Uma matriz de itens ancestrais do ativo no repositório. |
| *repo:state* | string | Estado atual do ativo no repositório (Por exemplo, ativo, excluído etc.). |
| *repo:createdBy* | string | O usuário ou sistema que criou o ativo. |
| *repo:createDate* | string | A data e a hora em que o ativo foi criado. |
| *repo:modifiedBy* | string | O usuário ou sistema que modificou o ativo pela última vez. |
| *repo:modifyDate* | string | A data e a hora em que o ativo foi modificado pela última vez. |
| *dc:format* | string | O formato do ativo, como o tipo de arquivo (por exemplo, JPEG, PNG etc.). |
| *tiff:imageWidth* | número | A largura de um ativo. |
| *tiff:imageLength* | número | A altura de um ativo. |
| *computedMetadata* | `Record<string, any>` | Um objeto que representa um compartimento para todos os metadados do ativo de todos os tipos (repositório, aplicativo ou metadados incorporados). |
| *_links* | `Record<string, any>` | Links de hipermídia do ativo associado. Inclui links para recursos como metadados e representações. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition* | `Array<Object>` | Matriz de objetos que contém informações sobre representações do ativo. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].href* | string | O URI da representação. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].type* | string | O tipo MIME da representação. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].&#39;repo:size&#39;* | número | O tamanho da representação em bytes. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].width* | número | A largura da representação. |
| *_links.http://ns.adobe.com/adobecloud/rel/rendition[].height* | número | A altura da representação. |

Para obter uma lista completa das propriedades e um exemplo detalhado, acesse [Exemplo de código do seletor de ativos](https://github.com/adobe/aem-assets-selectors-mfe-examples).

<!--
### ImsAuthProps {#ims-auth-props}

The `ImsAuthProps` properties define the authentication information and flow that the Asset Selector uses to obtain an `imsToken`. By setting these properties, you can control how the authentication flow should behave and register listeners for various authentication events.

| Property Name | Description|
|---|---|
| `imsClientId`| A string value representing the IMS client ID used for authentication purposes. This value is provided by Adobe and is specific to your Adobe AEM CS organization.|
| `imsScope`| Describes the scopes used in authentication. The scopes determine the level of access that the application has to your organization resources. Multiple scopes can be separated by commas.|
| `redirectUrl` | Represents the URL where the user is redirected after authentication. This value is typically set to the current URL of the application. If a `redirectUrl` is not supplied, `ImsAuthService` will use the redirectUrl used to register the `imsClientId`|
| `modalMode`| A boolean indicating whether the authentication flow should be displayed in a modal (pop-up) or not. If set to `true`, the authentication flow is displayed in a pop-up. If set to `false`, the authentication flow is displayed in a full page reload. _Note:_ for better UX, you can dynamically control this value if the user has browser pop-up disabled. |
| `onImsServiceInitialized`| A callback function that is called when the Adobe IMS authentication service is initialized. This function takes one parameter, `service`, which is an object representing the Adobe IMS service. See [`ImsAuthService`](#imsauthservice-ims-auth-service) for more details.|
| `onAccessTokenReceived`| A callback function that is called when an `imsToken` is received from the Adobe IMS authentication service. This function takes one parameter, `imsToken`, which is a string representing the access token. |
| `onAccessTokenExpired`| A callback function that is called when an access token has expired. This function is typically used to trigger a new authentication flow to obtain a new access token. |
| `onErrorReceived`| A callback function that is called when an error occurs during authentication. This function takes two parameters: the error type and error message. The error type is a string representing the type of error and the error message is a string representing the error message. |

### ImsAuthService {#ims-auth-service}

`ImsAuthService` class handles the authentication flow for the Asset Selector. It is responsible for obtaining an `imsToken` from the Adobe IMS authentication service. The `imsToken` is used to authenticate the user and authorize access to the Adobe Experience Manager (AEM) CS Assets repository. ImsAuthService uses the `ImsAuthProps` properties to control the authentication flow and register listeners for various authentication events. You can use the convenient [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) function to register the _ImsAuthService_ instance with the Asset Selector. The following functions are available on the `ImsAuthService` class. However, if you are using the _registerAssetsSelectorsAuthService_ function, you do not need to call these functions directly.

| Function Name | Description |
|---|---|
| `isSignedInUser` | Determines whether the user is currently signed in to the service and returns a boolean value accordingly.|
| `getImsToken`    | Retrieves the authentication `imsToken` for the currently signed-in user, which can be used to authenticate requests to other services such as generating asset _rendition.|
| `signIn`| Initiates the sign-in process for the user. This function uses the `ImsAuthProps` to show authentication in either a pop-up or a full page reload |
| `signOut`| Signs the user out of the service, invalidating their authentication token and requiring them to sign in again to access protected resources. Invoking this function will reload the current page.|
| `refreshToken`| Refreshes the authentication token for the currently signed-in user, preventing it from expiring and ensuring uninterrupted access to protected resources. Returns a new authentication token that can be used for subsequent requests. |
-->

### Exemplo para o fluxo não SUSI {#non-susi-vanilla}

Este exemplo demonstra como usar o Seletor de ativos com um fluxo não SUSI ao executar um aplicativo [!DNL Adobe] no Unified Shell ou quando você já tiver gereado `imsToken` para autenticação.

Inclua o pacote do Seletor de ativos no código usando o `script` tag, conforme mostrado em _linhas 6-15_ do exemplo abaixo. Depois que o script for carregado, a variável global `PureJSSelectors` estará disponível para uso. Definir o Seletor de ativos [propriedades](#asset-selector-properties) conforme mostrado em _linhas 16-23_. As propriedades `imsOrg` e `imsToken` são necessárias para autenticação em um fluxo não SUSI. A propriedade `handleSelection` é usada para manipular os ativos selecionados. Para renderizar o Seletor de ativos, chame a função `renderAssetSelector` como mencionado na _linha 17_. O Seletor de ativos é exibido no elemento de container `<div>`, conforme mostrado nas _linhas 21 e 22_.

Seguindo essas etapas, é possível usar o Seletor de ativos com um fluxo não SUSI no aplicativo [!DNL Adobe].

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in non-SUSI flow
        const assetSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (assets: SelectedAssetType[]) => {},
        };
        // Call the `renderAssetSelector` available in PureJSSelectors globals to render AssetSelector
        PureJSSelectors.renderAssetSelector(container, assetSelectorProps);
    </script>
</head>

<body>
    <div id="asset-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

Para obter um exemplo detalhado, acesse [Exemplo de código do seletor de ativos](https://github.com/adobe/aem-assets-selectors-mfe-examples).

<!--
### Example for the SUSI flow {#susi-vanilla}

Use this example `index.html` file for authentication if you are integrating your application using SUSI flow.

Access the Asset Selector package using the `Script` Tag, as shown in *line 9* to *line 11* of the example `index.html` file.

*Line 14* to *line 38* of the example describes the IMS flow properties, such as `imsClientId`, `imsScope`, and `redirectURL`. The function requires that you define at least one of the `imsClientId` and `imsScope` properties. If you do not define a value for `redirectURL`, the registered redirect URL for the client ID is used.

As you do not have an `imsToken` generated, use the `registerAssetsSelectorsAuthService` and `renderAssetSelectorWithAuthFlow` functions, as shown in line 40 to line 50 of the example `index.html` file. Use the `registerAssetsSelectorsAuthService` function before `renderAssetSelectorWithAuthFlow` to register the `imsToken` with the Asset Selector. [!DNL Adobe] recommends to call `registerAssetsSelectorsAuthService` when you instantiate the component.

Define the authentication and other Assets as a Cloud Service access-related properties in the `const props` section, as shown in *line 54* to *line 60* of the example `index.html` file.

The `PureJSSelectors` global variable, mentioned in *line 65*, is used to render the Asset Selector in the web browser.

Asset Selector is rendered on the `<div>` container element, as mentioned in *line 74* to *line 81*. The example uses a dialog to display the Asset Selector.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>

<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta charset="utf-8">
    <title>Asset Selectors</title>
    <link rel="stylesheet" href="index.css">
    <script id="asset-selector"
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/asset-selectors.js"></script>
    <script>

        const imsProps = {
            imsClientId: "<obtained from IMS team>",
            imsScope: "openid, <other scopes>",
            redirectUrl: window.location.href,
            modalMode: true, // false to open in a full page reload flow
            onImsServiceInitialized: (service) => {
                // invoked when the ims service is initialized and is ready
                console.log("onImsServiceInitialized", service);
            },
            onAccessTokenReceived: (token) => {
                console.log("onAccessTokenReceived", token);
            },
            onAccessTokenExpired: () => {
                console.log("onAccessTokenError");
                // re-trigger sign-in flow
            },
            onErrorReceived: (type, msg) => {
                console.log("onErrorReceived", type, msg);
            },
        }

        function load() {
            const registeredTokenService = PureJSSelectors.registerAssetsSelectorsAuthService(imsProps);
            imsInstance = registeredTokenService;
        };

        // initialize the IMS flow before attempting to render the asset selector
        load();
        

        //function that will render the asset selector
            const otherProps = {
            // any other props supported by asset selector
            }
            const assetSelectorProps = {
                "imsOrg": "imsorg",
                ...otherProps
            }
             // container element on which you want to render the AssetSelector/DestinationSelector component
            const container = document.getElementById('asset-selector');

            /// Use the PureJSSelectors in globals to render the AssetSelector/DestinationSelector component
            PureJSSelectors.renderAssetSelectorWithAuthFlow(container, assetSelectorProps, () => {
                const assetSelectorDialog = document.getElementById('asset-selector-dialog');
                assetSelectorDialog.showModal();
            });
        }
    </script>

</head>
<body class="asset-selectors">
    <div>
        <button onclick="renderAssetSelectorWithAuthFlowFlow()">Asset Selector - Select Assets with Ims Flow</button>
    </div>
        <dialog id="asset-selector-dialog">
            <div id="asset-selector" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
            </div>
        </dialog>
    </div>
</body>

</html>

```
-->

## Usar propriedades do Seletor de ativos {#asset-selector-properties}

Você pode usar as propriedades do Seletor de ativos para personalizar a forma como o Seletor de ativos é renderizado. A tabela a seguir lista as propriedades que você pode usar para personalizar e usar o Seletor de ativos.

| Propriedade | Tipo | Obrigatório | Padrão | Descrição |
|---|---|---|---|---|
| *painel* | booleano | Não | falso | Se marcado `true`, o Seletor de ativos é renderizado em uma exibição do painel à esquerda. Se estiver marcado `false`, o Seletor de ativos é renderizado na exibição modal. |
| *imsOrg* | string | Sim | | A ID do Adobe Identity Management System (IMS) atribuída durante o provisionamento do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para sua organização. A variável `imsOrg` A chave é necessária para autenticar se a organização que você está acessando está no Adobe IMS ou não. |
| *imsToken* | string | Não | | Token de portador IMS usado para autenticação. O `imsToken` é obrigatório se você estiver usando o fluxo não SUSI. |
| *apiKey* | string | Não | | Chave de API usada para acessar o serviço de Descoberta do AEM. O `apiKey` é obrigatório se você estiver usando o fluxo não SUSI. |
| *rootPath* | string | Não | /content/dam/ | Caminho da pasta na qual o Seletor de ativos exibe seus ativos. O `rootPath` também pode ser usado na forma de encapsulamento. Por exemplo, dado o seguinte caminho, `/content/dam/marketing/subfolder/`, o Seletor de ativos não permite que você navegue por qualquer pasta principal, mas exibe apenas as pastas secundárias. |
| *caminho* | string | Não | | Caminho usado para navegar para um diretório específico de ativos quando o Seletor de ativos é renderizado. |
| *filterSchema* | matriz | Não | | Modelo usado para configurar propriedades de filtro. Isso é útil quando quiser limitar determinadas opções de filtro no Seletor de ativos. |
| *filterFormProps* | Objeto | Não | | Especifique as propriedades de filtro que precisam ser usadas para refinar sua pesquisa. Por exemplo, tipo MIME JPG, PNG, GIF. |
| *selectedAssets* | Matriz `<Object>` | Não |                 | Especifique os ativos selecionados quando o Seletor de ativos for renderizado. É necessária uma matriz de objetos que contenha uma propriedade de id dos ativos. Por exemplo, `[{id: 'urn:234}, {id: 'urn:555'}]` Um ativo deve estar disponível no diretório atual. Se precisar usar um diretório diferente, forneça um valor para a propriedade `path` também. |
| *acvConfig* | Objeto | Não | | A propriedade Exibição da coleção de ativos que contém o objeto com a configuração personalizada para substituir os padrões. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | Não |                 | Se as traduções prontas para uso forem insuficientes para as necessidades do aplicativo, é possível expor uma interface pela qual poderá passar seus próprios valores localizados personalizados pela propriedade `i18nSymbols`. Transmitir um valor por meio dessa interface substitui as traduções padrão fornecidas e usará suas próprias traduções.  Para executar a substituição, deverá transmitir um objeto [Descritor de mensagem](https://formatjs.io/docs/react-intl/api/#message-descriptor) à chave de `i18nSymbols` que deseja substituir. |
| *intl* | Objeto | Não | | O Seletor de ativos fornece traduções padrão prontas para uso. Você pode selecionar o idioma de tradução fornecendo uma string de idioma válida por meio da propriedade `intl.locale`. Por exemplo: `intl={{ locale: "es-es" }}` </br></br> As strings de idioma com suporte seguem os padrões [ISO 639 - Códigos](https://www.iso.org/iso-639-language-codes.html) para a representação de nomes de idiomas. </br></br> Lista de idiomas com suporte: Inglês - “en-us” (padrão) Espanhol - “es-es” Alemão - “de-de” Francês - “fr-fr” Italiano - “it-it” Japonês - “ja-jp” Coreano - “ko-kr” Português - “pt-br” Chinês (Tradicional) - “zh-cn” Chinês (Taiwan) - “zh-tw” |
| *repositoryId* | string | Não | &#39;&#39; | Repositório de onde o Seletor de ativos carrega o conteúdo. |
| *additionalAemSolutions* | `Array<string>` | Não | [ ] | Ela permite adicionar uma lista de repositórios AEM adicionais. Se nenhuma informação for fornecida nessa propriedade, somente a biblioteca de mídia ou os repositórios do AEM Assets serão considerados. |
| *hideTreeNav* | booleano | Não |  | Especifica se deve mostrar ou ocultar a barra lateral de navegação da árvore de ativos. Usada apenas na exibição modal e, portanto, não há efeito dessa propriedade na exibição de painel. |
| *onDrop* | Função | Não | | A propriedade permite a funcionalidade soltar de um ativo. |
| *dropOptions* | `{allowList?: Object}` | Não | | Configura as opções de soltar usando “allowList”. |
| *colorScheme* | string | Não | | Configure o tema (`light` ou `dark`) do Seletor de ativos. |
| *handleSelection* | Função | Não | | Chamado com a matriz de itens do ativo quando os ativos são selecionados e o botão `Select` no modal é clicado. Essa função só é invocada na exibição modal. Para exibição do painel, use as funções `handleAssetSelection` ou `onDrop`. Exemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [Tipo de ativo selecionado](#selected-asset-type) para obter detalhes. |
| *handleAssetSelection* | Função | Não | | Invocado com uma matriz de itens enquanto os ativos estão sendo selecionados ou desmarcados. É útil quando você deseja acompanhar os ativos à medida que o usuário os seleciona. Exemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [Tipo de ativo selecionado](#selected-asset-type) para obter detalhes. |
| *onClose* | Função | Não | | Invocado quando o botão `Close` na exibição modal é pressionado. Somente é chamado na exibição `modal` e desconsiderado na exibição `rail`. |
| *onFilterSubmit* | Função | Não | | Invocado com itens de filtro à medida que o usuário altera critérios de filtro diferentes. |
| *selectionType* | string | Não | individual | Configuração para a seleção `single` ou `multiple` de ativos de cada vez. |

## Exemplos de uso das propriedades do Seletor de ativos {#usage-examples}

É possível definir as [propriedades](#asset-selector-properties) do Seletor de ativos no arquivo `index.html` para personalizar a exibição do Seletor de ativos no aplicativo.

### Exemplo 1: Seletor de ativos na exibição do painel

![rail-view-example](assets/rail-view-example-vanilla.png)

Se o valor do Seletor de ativos `rail` estiver definido como `false` ou não for mencionado nas propriedades, o Seletor de ativos aparecerá na exibição modal por padrão.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### Exemplo 2: popover de metadados

Use várias propriedades para definir os metadados de um ativo que deseja visualizar usando um ícone de informações. O popover de informações fornece a coleção de informações sobre o ativo ou a pasta, incluindo título, dimensões, data de modificação, local e descrição de um ativo. No exemplo abaixo, várias propriedades são usadas para exibir metadados de um ativo, por exemplo, a propriedade `repo:path` especifica o local de um ativo. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)


### Exemplo 3: propriedade de filtro personalizado na exibição do painel

Além da pesquisa facetada, o Seletor de ativos permite personalizar vários atributos para refinar a pesquisa no [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] aplicação. É necessário adicionar o código a seguir para acrescentar filtros de pesquisa personalizados em seu aplicativo. No exemplo abaixo, a pesquisa `Type Filter` que filtra o tipo de ativo entre Imagens, Documentos ou Vídeos ou o tipo de filtro adicionado para a pesquisa.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

<!-- Property details to be added here. Referred the ticket https://jira.corp.adobe.com/browse/ASSETS-19023-->

<!--
## Asset Selector Object Schema {#object-schema}

Schema describes the object properties associated with an asset selected using Asset Selector. It uses the combination of data types and their values to validate the object describing the selected Asset using an Asset Selector.

**Schema Syntax**
````
interface SelectedAsset {
    'repo:id': string;
    'repo:name': string;
    'repo:path': string;
    'repo:size': number;
    'repo:createdBy': string;
    'repo:createDate': string;
    'repo:modifiedBy': string; 
    'repo:modifyDate': string; 
    'dc:format': string; 
    'tiff:imageWidth': number;
    'tiff:imageLength': number;
    'repo:state': string;
    computedMetadata: Record<string, any>;
    _links: {
        'http://ns.adobe.com/adobecloud/rel/rendition': Array<{
            href: string;
            type: string;
            'repo:size': number;
            width: number;
            height: number;
            [others: string]: any;
        }>;
    };
}
````

**Query Parameters**

| Parameter | Type | Description |
|---|---|---|
| repo:id | string | ID of an Asset |
| repo:name | string | The name of an Asset |
| repo:path | string | The path of an Asset |
| repo:size | number | Size of an Asset (in bytes) |
| repo:createdBy | string | ID of a user who created an Asset |
| repo: createdDate | string | The timestamp when an asset was created |
| repo:modifiedBy | string | ID of a user who modified the asset recently |
| repo:modifyDate | string | The timestamp when the asset was last modified |
| dc:format | string | MIME type of an Asset |
| tiff:imageWidth | number | The width of an image type of Asset |
| tiff:imageLength | number | The height of an image type of Asset |
| repo:state | string | The `Approved`, `Rejected`, or `Expired`state of an Asset |
| computedMetadata | string | It is an object that represents a bucket for all the Asset's metadata of all kinds (repository, application or embedded metadata) |
| _links | string | It represents the collection of links used in the Asset Selector. The links are represented in the form of an array. The parameters of an array include: `href`, `type`, `repo:size`, `width`, `height`, and so on  |

For the detailed example of Object Schema, click 
-->

## Lidar com a seleção de ativos usando o esquema de objeto {#handling-selection}

A propriedade `handleSelection` é usada para lidar com seleções únicas ou múltiplas de ativos no Seletor de ativos. O exemplo abaixo declara a sintaxe de uso de `handleSelection`.

![handle-selection](assets/handling-selection.png)

## Utilização do Seletor de ativos {#using-asset-selector}

Depois que o Seletor de ativos estiver configurado e você for autenticado para usar o Seletor de ativos com o aplicativo [!DNL Adobe Experience Manager] as a [!DNL Cloud Service], você poderá selecionar ativos ou executar várias outras operações para pesquisar seus ativos no repositório.

![using-asset-selector](assets/using-asset-selector.png)

* **A**: [Ocultar/Mostrar painel](#hide-show-panel)
* **B**: [Alternador de repositório](#repository-switcher)
* **C**: [Ativos](#repository)
* **D**: [Filtros](#filters)
* **E**: [Barra de pesquisa](#search-bar)
* **F**: [Classificação](#sorting)
* **G**: [Classificação em ordem crescente ou decrescente](#sorting)
* **H**: [Exibição](#types-of-view)

### Ocultar/Mostrar painel {#hide-show-panel}

Para ocultar pastas na navegação à esquerda, clique no ícone **[!UICONTROL Ocultar pastas]**. Para desfazer as alterações, clique no ícone **[!UICONTROL Ocultar pastas]** novamente.

### Alternador de repositório {#repository-switcher}

O Seletor de ativos também permite alternar repositórios para seleção de ativos. Você pode selecionar o repositório de sua escolha no menu suspenso disponível no painel esquerdo. As opções de repositório disponíveis na lista suspensa se baseiam na propriedade `repositoryId` definida no arquivo `index.html`. Tem como base os ambientes da organização IMS selecionada que são acessados pelo usuário conectado. Os consumidores podem transmitir um `repositoryID` de sua preferência e, nesse caso, o Seletor de ativos interrompe a renderização do alternador de repositório e renderiza ativos somente do repositório especificado.
<!--
It is based on the `imsOrg` that is provided in the application. If you want to see the list of repositories, then `repositoryId` is required to view those specific repositories in your application.
-->

### Repositório de ativos

É uma coleção de pastas de ativos que você pode usar para executar operações.

### Filtros prontos para uso {#filters}

O Seletor de ativos também fornece opções de filtro prontas para uso para refinar os resultados da pesquisa. Os filtros disponíveis são os seguintes:

* `File type`: inclui pasta, arquivo, imagens, documentos ou vídeo
* `MIME type`: inclui JPG, GIF, PPTX, PNG, MP4, DOCX, TIFF, PDF, XLSX
* `Image Size`: inclui largura mínima/máxima, altura mínima/máxima da imagem

  ![rail-view-example](assets/filters-asset-selector.png)

### Pesquisa personalizada

Além da pesquisa de texto completo, o Seletor de ativo permite pesquisar ativos em arquivos usando a pesquisa personalizada. Você pode usar filtros de pesquisa personalizados nos modos de exibição Modal e Painel.

![custom-search](assets/custom-search.png)

Também é possível criar um filtro de pesquisa padrão para salvar os campos que você pesquisa com frequência e usá-los depois. Para criar uma pesquisa personalizada para seus ativos, você pode usar a propriedade `filterSchema`.

### Barra de pesquisa {#search-bar}

O Seletor de ativos permite executar uma pesquisa de texto completo dos ativos no repositório selecionado. Por exemplo, se você digitar a palavra-chave `wave` na barra de pesquisa, todos os ativos com a palavra-chave `wave` mencionada em qualquer uma das propriedades de metadados serão exibidos.

### Classificação {#sorting}

Você pode classificar ativos no Seletor de ativos por nome, dimensões ou tamanho de um ativo. Também é possível classificar os ativos em ordem crescente ou decrescente.

### Tipos de visualização {#types-of-view}

O Seletor de ativos permite exibir o ativo em quatro exibições diferentes:

* **![exibição em lista](assets/do-not-localize/list-view.png) [!UICONTROL Exibição em lista]**: a exibição em lista exibe arquivos e pastas roláveis em uma única coluna.
* **![exibição em grade](assets/do-not-localize/grid-view.png) [!UICONTROL Exibição em grade]**: a exibição em grade exibe arquivos e pastas roláveis em uma grade de linhas e colunas.
* **![exibição em galeria](assets/do-not-localize/gallery-view.png) [!UICONTROL Exibição em galeria]**: a exibição em galeria exibe arquivos ou pastas em uma lista horizontal com bloqueio central.
* **![exibição em cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL Exibição em cascata]**: a exibição em cascata exibe arquivos ou pastas no formato de uma ponte.

<!--
### Modes to view Asset Selector

Asset Selector supports two types of out of the box views:

**  Modal view or Inline view:** The modal view or inline view is the default view of Asset Selector that represents Assets folders in the front area. The modal view allows users to view assets in a full screen to ease the selection of multiple assets for import. Use `<AssetSelector rail={false}>` to enable modal view.

    ![modal-view](assets/modal-view.png)

**  Rail view:** The rail view represents Assets folders in a left panel. The drag and drop of assets can be performed in this view. Use `<AssetSelector rail={true}>` to enable rail view.

    ![rail-view](assets/rail-view.png)
-->
<!--

### Application Integration

Asset Selector is flexible and can be integrated within your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application. It is accessible and localized to add, search, and select assets in your application. With Asset Selector you can:
*   **Configure** You can configure the files/folders that you want to show at the upfront. The assets that are chosen to view can be of any supported formats, for example, JPEG. It lets you control the display of various text or symbols as per your choice.
*   **Perfect fit** Asset selector easily fits in your existing [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application and choose the way you want to view. The mode of view can be inline, rail, or modal view.
*   **Accessible** With Asset Selector, you can reach the desired asset in an easy manner.
*   **Localize** Assets can be availed for the various locales available as per Adobe's localization standards.
-->
<!--

### Support for multiple instances

The micro front-end design supports the display of multiple instances of Asset Selector on a single screen.

![multiple-instance](assets/multiple-instance.png)
-->

<!--

### Controlled selection with multi-select

You can make default multi-selection of assets by specifying the assets to the component using `selectedAssets` property. You should specify an array of asset IDs. For example, `[{id: 'urn:234}, {id: 'urn:555'}].`
-->
<!--

### Action buttons

When you customize your application with Asset Selector based on ReactJS, you are provided with the following action buttons to perform various actions:
*   **Open in media library** Lets you open the asset in media library.
*   **Upload** Lets you upload an asset directly.
*   **Download** Downloads the asset in [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
-->
<!--

### Status of an asset

Asset Selector lets you know the status of your uploaded assets. The status can be `Approved`, `Rejected`, or `Expired` of the asset. 
-->
<!--

### Localization

The integration of Asset Selector with [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] allows localized content appear in your application.
-->
