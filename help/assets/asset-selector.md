---
title: Seletor de ativos para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Use o Seletor de ativos para pesquisar, localizar e recuperar metadados e representações de ativos no aplicativo.
contentOwner: KK
feature: Selectors
role: Admin,User
exl-id: 5f962162-ad6f-4888-8b39-bf5632f4f298
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '5357'
ht-degree: 29%

---

# Seletor de ativos de micro front-end {#Overview}

O Seletor de ativos de micro front-end fornece uma interface do usuário que se integra facilmente ao repositório [!DNL Experience Manager Assets] para navegar ou pesquisar ativos digitais disponíveis no repositório e usá-los na experiência de criação do aplicativo.

A interface do usuário de micro front-end é disponibilizada em sua experiência de aplicativo usando o pacote de Seletor de ativos. Quaisquer atualizações no pacote são automaticamente importadas e o Seletor de ativos implantado mais recente é automaticamente carregado no aplicativo.

![Visão geral](assets/overview.png)

O Seletor de ativos oferece muitos benefícios, como:

* Facilidade de integração com qualquer um dos aplicativos [Adobe](#asset-selector-ims) ou [não-Adobe](#asset-selector-non-ims) usando a biblioteca JavaScript Vanilla.
* Manutenção facilitada, pois as atualizações do pacote do Seletor de ativos são implantadas automaticamente no Seletor de ativos disponível para seu aplicativo. Não há atualizações necessárias no aplicativo para carregar as modificações mais recentes.
* Facilidade de personalização, pois há propriedades disponíveis que controlam a exibição do Seletor de ativos no aplicativo.
* Filtros de pesquisa de texto completo, prontos para uso e personalizados que navegam rapidamente até os ativos para uso na experiência de criação.
* Capacidade de alternar repositórios em uma organização IMS para seleção de ativos.
* Capacidade de classificar ativos por nome, dimensões e tamanho e visualizá-los na exibição de Lista, Grade, Galeria ou Cascata.

<!--Perform the following tasks to integrate and use Asset Selector with your [!DNL Experience Manager Assets] repository:

1. [Install Asset Selector](#installation)
2. [Integrate Asset Selector using Vanilla JS](#integration-using-vanilla-js)
3. [Use Asset Selector](#using-asset-selector)
-->

<!--
## Setting up Asset Selector {#asset-selector-setup}

![Asset Selector set up](assets/asset-selector-prereqs.png)
-->

## Pré-requisitos{#prereqs}

Você deve garantir os seguintes métodos de comunicação:

* O aplicativo está sendo executado em HTTPS.
* O URL do aplicativo está na lista de permissões de URLs de redirecionamento do cliente IMS.
* O fluxo de logon do IMS é configurado e renderizado usando um pop-up no navegador da Web. Portanto, os pop-ups devem ser ativados ou permitidos no navegador de destino.

Use os pré-requisitos acima se você precisar de um fluxo de trabalho de autenticação IMS do Seletor de ativos. Como alternativa, se você já estiver autenticado com o fluxo de trabalho do IMS, é possível adicionar as informações do IMS.

>[!IMPORTANT]
>
> Este repositório serve como uma documentação complementar que descreve as APIs disponíveis e exemplos de uso para integração do Seletor de ativos. Antes de tentar instalar ou usar o Seletor de ativos, verifique se sua organização recebeu o acesso ao Seletor de ativos como parte do perfil do Experience Manager Assets as a Cloud Service. Se não tiver sido provisionado, você não poderá integrar ou usar esses componentes. Para solicitar o provisionamento, o administrador do programa deve levantar um tíquete de suporte marcado como P2 do Admin Console e incluir as seguintes informações:
>
>* Nomes de domínio em que o aplicativo de integração está hospedado.
>* Após o provisionamento, sua organização receberá `imsClientId`, `imsScope` e um `redirectUrl` correspondentes aos ambientes solicitados que são essenciais para a configuração do Seletor de ativos. Sem essas propriedades válidas, não é possível executar as etapas de instalação.

## Instalação {#installation}

O Seletor de ativos está disponível por meio da CDN do ESM (por exemplo, [esm.sh](https://esm.sh/)/[skypack](https://www.skypack.dev/)) e da versão [UMD](https://github.com/umdjs/umd).

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

## Integrar o Seletor de ativos usando o Vanilla JS {#integration-using-vanilla-js}

É possível integrar qualquer aplicativo do [!DNL Adobe] ou que não seja da Adobe ao repositório do [!DNL Experience Manager Assets] e selecionar ativos no aplicativo. Consulte [Integração do Seletor de ativos com vários aplicativos](#asset-selector-integration-with-apps).

A integração é feita importando o pacote do Seletor de ativos e conectando ao Assets as a Cloud Service usando a biblioteca JavaScript Vanilla. Edite um `index.html` ou qualquer arquivo apropriado em seu aplicativo para:

* Definir os detalhes de autenticação
* Acessar o repositório do Assets as a Cloud Service
* Configurar as propriedades de exibição do Seletor de ativos

É possível executar a autenticação sem definir algumas das propriedades do IMS, se:

* Está integrando um aplicativo [!DNL Adobe] no [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=pt-BR).
* Você já tem um token IMS gerado para autenticação.

## Integrar o Seletor de ativos a vários aplicativos {#asset-selector-integration-with-apps}

É possível integrar o Seletor de ativos a vários aplicativos, como:

* [Integrar o Seletor de ativos a um aplicativo do  [!DNL Adobe] ](#adobe-app-integration-vanilla)
* [Integrar o Seletor de ativos a um aplicativo que não seja da Adobe](#adobe-non-app-integration)
* [Integração do Dynamic Media com recursos OpenAPI](#adobe-app-integration-polaris)

>[!BEGINTABS]

<!--Integration with an Adobe application content starts here-->

>[!TAB Integração com um aplicativo do Adobe]

### Pré-requisitos{#prereqs-adobe-app}

Use os seguintes pré-requisitos se estiver integrando o Seletor de ativos a um aplicativo do [!DNL Adobe]:

* [Métodos de comunicação](#prereqs)
* imsOrg
* imsToken
* apikey

### Integrar o Seletor de ativos a um aplicativo do [!DNL Adobe] {#adobe-app-integration-vanilla}

O exemplo a seguir demonstra o uso do Seletor de Ativos ao executar um aplicativo [!DNL Adobe] no Unified Shell ou quando você já gerou `imsToken` para autenticação.

Inclua o pacote do Seletor de ativos no código usando a marca `script`, como mostrado nas _linhas 6-15_ do exemplo abaixo. Depois que o script for carregado, a variável global `PureJSSelectors` estará disponível para uso. Defina o Seletor de ativos [propriedades](#asset-selector-properties) conforme mostrado em _linhas 16-23_. As propriedades `imsOrg` e `imsToken` são necessárias para autenticação no aplicativo Adobe. A propriedade `handleSelection` é usada para manipular os ativos selecionados. Para renderizar o Seletor de ativos, chame a função `renderAssetSelector` como mencionado na _linha 17_. O Seletor de ativos é exibido no elemento de container `<div>`, conforme mostrado nas _linhas 21 e 22_.

Seguindo essas etapas, você pode usar o Seletor de ativos com seu aplicativo [!DNL Adobe].

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/assets/resources/assets-selectors.js"></script>
    <script>
        // get the container element in which we want to render the AssetSelector component
        const container = document.getElementById('asset-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
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

<!--For detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

+++**ImsAuthProps**
As propriedades `ImsAuthProps` definem as informações de autenticação e o fluxo que o Seletor de ativos usa para obter um `imsToken`. Ao definir essas propriedades, é possível controlar como o fluxo de autenticação deve se comportar e registrar ouvintes para vários eventos de autenticação.

| Nome de propriedade | Descrição |
|---|---|
| `imsClientId` | Um valor de string que representa a ID do cliente IMS usada para fins de autenticação. Esse valor é fornecido pela Adobe e é específico para a sua organização do Adobe AEM CS. |
| `imsScope` | Descreve os escopos usados na autenticação. Os escopos determinam o nível de acesso que o aplicativo tem aos recursos da organização. Vários escopos podem ser separados por vírgulas. |
| `redirectUrl` | Representa o URL para o qual o usuário é redirecionado após a autenticação. Normalmente, esse valor é definido como o URL atual do aplicativo. Se um `redirectUrl` não for fornecido, `ImsAuthService` usará o redirectUrl usado para registrar o `imsClientId` |
| `modalMode` | Um booleano que indica se o fluxo de autenticação deve ser exibido em um modal (pop-up) ou não. Se definido como `true`, o fluxo de autenticação será exibido em um pop-up. Se definido como `false`, o fluxo de autenticação será exibido em um recarregamento de página completo. _Observação :_para melhor UX, você pode controlar dinamicamente esse valor se o usuário tiver o pop-up do navegador desabilitado. |
| `onImsServiceInitialized` | Uma função de retorno de chamada que é chamada quando o serviço de autenticação do Adobe IMS é inicializado. Essa função recebe um parâmetro, `service`, que é um objeto que representa o serviço Adobe IMS. Consulte [`ImsAuthService`](#imsauthservice-ims-auth-service) para obter mais detalhes. |
| `onAccessTokenReceived` | Uma função de retorno de chamada que é chamada quando um `imsToken` é recebido do serviço de autenticação do Adobe IMS. Esta função recebe um parâmetro, `imsToken`, que é uma cadeia de caracteres que representa o token de acesso. |
| `onAccessTokenExpired` | Uma função de retorno de chamada chamada chamada quando um token de acesso expira. Normalmente, essa função é usada para acionar um novo fluxo de autenticação para obter um novo token de acesso. |
| `onErrorReceived` | Uma função de retorno de chamada que é chamada quando ocorre um erro durante a autenticação. Essa função usa dois parâmetros: o tipo de erro e a mensagem de erro. O tipo de erro é uma cadeia de caracteres que representa o tipo de erro, e a mensagem de erro é uma cadeia de caracteres que representa a mensagem de erro. |

+++

+++**ImsAuthService**
A classe `ImsAuthService` manipula o fluxo de autenticação para o Seletor de ativos. Ele é responsável por obter um `imsToken` do serviço de autenticação do Adobe IMS. O `imsToken` é usado para autenticar o usuário e autorizar o acesso ao [!DNL Adobe Experience Manager] como um repositório do Assets [!DNL Cloud Service]. O ImsAuthService usa as propriedades `ImsAuthProps` para controlar o fluxo de autenticação e registrar ouvintes de vários eventos de autenticação. Você pode usar a conveniente função [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) para registrar a instância _ImsAuthService_ com o Seletor de ativos. As seguintes funções estão disponíveis na classe `ImsAuthService`. No entanto, se você estiver usando a função _registerAssetsSelectorsAuthService_, não será necessário chamar essas funções diretamente.

| Nome da função | Descrição |
|---|---|
| `isSignedInUser` | Determina se o usuário está conectado ao serviço no momento e retorna um valor booleano correspondente. |
| `getImsToken` | Recupera a autenticação `imsToken` para o usuário conectado no momento, que pode ser usada para autenticar solicitações para outros serviços, como a geração de _representação de ativos. |
| `signIn` | Inicia o processo de entrada do usuário. Esta função usa o `ImsAuthProps` para mostrar autenticação em um pop-up ou em um recarregamento de página completo |
| `signOut` | Desconecta o usuário do serviço, invalidando seu token de autenticação e exigindo que ele entre novamente para acessar recursos protegidos. Chamar essa função recarregará a página atual. |
| `refreshToken` | Atualiza o token de autenticação do usuário conectado no momento, evitando a expiração e garantindo acesso ininterrupto aos recursos protegidos. Retorna um novo token de autenticação que pode ser usado para solicitações subsequentes. |

+++

+++**Validação com o token IMS fornecido**

```
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected asset: ", selection);
    };
    function renderAssetSelectorInline() {
    console.log("initializing Asset Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('asset-selector-container');
    PureJSSelectors.renderAssetSelector(container, props);
    }
    $(document).ready(function() {
    renderAssetSelectorInline();
    });
</script>
```

+++

+++**Registrar retornos de chamada para o serviço IMS**

```
// object `imsProps` to be defined as below 
let imsProps = {
    imsClientId: <IMS Client Id>,
        imsScope: "openid",
        redirectUrl: window.location.href,
        modalMode: true,
        adobeImsOptions: {
            modalSettings: {
            allowOrigin: window.location.origin,
},
        useLocalStorage: true,
},
onImsServiceInitialized: (service) => {
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
```

+++

<!--Integration with non-Adobe application content starts here-->

>[!TAB Integração com um aplicativo que não seja da Adobe]

<!--### Integrate Asset Selector with a [!DNL non-Adobe] application {#adobe-non-app-integration}-->

### Pré-requisitos {#prereqs-non-adobe-app}

Use os seguintes pré-requisitos se estiver integrando o Seletor de ativos a um aplicativo que não seja da Adobe:

* [Métodos de comunicação](#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

O Seletor de ativos oferece suporte à autenticação para o repositório [!DNL Experience Manager Assets] usando propriedades do Identity Management System (IMS) como `imsScope` ou `imsClientID` quando você o integra a um aplicativo que não seja da Adobe.

+++**Configurar o Seletor de Ativos para um aplicativo que não seja da Adobe**
Para configurar o Seletor de ativos para um aplicativo que não seja da Adobe, primeiro você deve registrar um tíquete de suporte para provisionamento, seguido das etapas de integração.

**Registrando um tíquete de suporte**
Etapas para registrar um tíquete de suporte pela Admin Console:

1. Adicionar **Seletor de ativos com AEM Assets** no título do tíquete.

1. Na descrição, forneça os seguintes detalhes:

   * [!DNL Experience Manager Assets] como uma URL [!DNL Cloud Service] (ID do Programa e ID do Ambiente).
   * Nomes de domínio em que o aplicativo Web que não é da Adobe está hospedado.
+++

+++**Etapas de integração**
Use este exemplo de arquivo `index.html` para autenticação ao integrar o Seletor de ativos a um aplicativo que não seja da Adobe.

Acesse o pacote do Seletor de ativos usando a Marca `Script`, conforme mostrado na *linha 9* para a *linha 11* do arquivo de exemplo `index.html`.

A *Linha 14* a *linha 38* do exemplo descreve as propriedades do fluxo IMS, como `imsClientId`, `imsScope` e `redirectURL`. A função requer a definição de pelo menos uma das propriedades `imsClientId` e `imsScope`. Se você não definir um valor para `redirectURL`, a URL de redirecionamento registrada para a ID do cliente será usada.

Como você não tem um `imsToken` gerado, use as funções `registerAssetsSelectorsAuthService` e `renderAssetSelectorWithAuthFlow`, conforme mostrado na linha 40 para a linha 50 do arquivo de exemplo `index.html`. Use a função `registerAssetsSelectorsAuthService` antes de `renderAssetSelectorWithAuthFlow` para registrar `imsToken` com o Seletor de ativos. A [!DNL Adobe] recomenda chamar `registerAssetsSelectorsAuthService` ao instanciar o componente.

Defina a autenticação e outras propriedades relacionadas ao acesso do Assets as a Cloud Service na seção `const props`, conforme mostrado na *linha 54* a *linha 60* do arquivo de exemplo `index.html`.

A variável global `PureJSSelectors`, mencionada em *linha 65*, é usada para renderizar o Seletor de ativos no navegador da Web.

O Seletor de ativos é renderizado no elemento de contêiner `<div>`, como mencionado na *linha 74* para *linha 81*. O exemplo usa uma caixa de diálogo para exibir o Seletor de ativos.

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

+++

+++**Não é possível acessar o repositório de entrega**

>[!TIP]
>
>Se você tiver integrado o Seletor de ativos usando o fluxo de trabalho Inscrever-se, mas ainda não conseguir acessar o repositório de entrega, verifique se os cookies do navegador foram limpos. Caso contrário, você acaba recebendo o erro `invalid_credentials All session cookies are empty` no console.

+++

<!--Integration with Polaris application content starts here-->

>[!TAB Integração do Dynamic Media com recursos OpenAPI]

### Pré-requisitos {#prereqs-polaris}

Use os seguintes pré-requisitos se estiver integrando o Seletor de ativos ao Dynamic Media com recursos OpenAPI:

* [Métodos de comunicação](#prereqs)
* Para acessar o Dynamic Media com recursos OpenAPI, você deve ter licenças para:
   * Repositório do Assets (por exemplo, Experience Manager Assets as a Cloud Service).
   * AEM Dynamic Media.
* Somente [ativos aprovados](#approved-assets.md) estão disponíveis para uso, garantindo a consistência da marca.

### Integração do Dynamic Media com recursos OpenAPI{#adobe-app-integration-polaris}

A integração do Seletor de ativos com o processo OpenAPI do Dynamic Media envolve várias etapas que incluem a criação de um URL de mídia dinâmica personalizado ou pronto para escolher o URL de mídia dinâmica etc.

+++**Integrar o Seletor de ativos para Dynamic Media aos recursos de OpenAPI**

As propriedades `rootPath` e `path` não devem fazer parte do Dynamic Media com recursos OpenAPI. Em vez disso, você pode configurar a propriedade `aemTierType`. Veja a seguir a sintaxe da configuração:

```
aemTierType:[1: "delivery"]
```

Essa configuração permite visualizar todos os ativos aprovados sem pastas ou como uma estrutura simples. Para obter mais informações, navegue até a propriedade `aemTierType` em [Propriedades do Seletor de ativos](#asset-selector-properties)

+++

+++**Criar uma URL de Entrega Dinâmica a partir de ativos aprovados**
Depois de configurar o Seletor de ativos, um esquema de objetos será usado para criar um URL de entrega dinâmico dos ativos selecionados.
Por exemplo, um esquema de um objeto de uma matriz de objetos que é recebido após a seleção de um ativo:

```
{
"dc:format": "image/jpeg",
"repo:assetId": "urn:aaid:aem:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"repo:name": "image-7.jpg",
"repo:repositoryId": "delivery-pxxxx-exxxxxx.adobe.com",
...
}
```

Todos os ativos selecionados são carregados pela função `handleSelection` que atua como um objeto JSON. Por exemplo, `JsonObj`. O URL dinâmico de entrega é criado pela combinação das seguintes operadoras:

| Objeto | JSON |
|---|---|
| Host | `assetJsonObj["repo:repositoryId"]` |
| Raiz da API | `/adobe/assets` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"].split(".").slice(0,-1).join(".")` |
| formato | `.jpg` |

**Especificação da API de entrega de ativos aprovada**

Formato de URL:
`https://<delivery-api-host>/adobe/assets/<asset-id>/as/<seo-name>.<format>?<image-modification-query-parameters>`

Onde,

* O host é `https://delivery-pxxxxx-exxxxxx.adobe.com`
* A raiz da API é `"/adobe/assets"`
* `<asset-id>` é o identificador do ativo
* `as` é a parte constante da especificação da API aberta indicando como o ativo deve ser referido
* `<seo-name>` é o nome de um ativo
* `<format>` é o formato de saída
* `<image modification query parameters>` como suporte pela especificação da API de entrega dos ativos aprovados

**API de entrega de representação original de ativos aprovados**

O URL do delivery dinâmico possui a seguinte sintaxe:
`https://<delivery-api-host>/adobe/assets/<asset-id>/original/as/<seo-name>`, onde,

* O host é `https://delivery-pxxxxx-exxxxxx.adobe.com`
* A raiz da API para Entrega de Representação Original é `"/adobe/assets"`
* `<asset-id>` é um identificador de ativo
* `/original/as` é a parte constante da especificação de API aberta indicando como a representação original deve ser chamada
* `<seo-name>`é o nome do ativo que pode ou não ter uma extensão

+++

+++**Pronto para escolher a URL de entrega dinâmica**
Todos os ativos selecionados são carregados pela função `handleSelection` que atua como um objeto JSON. Por exemplo, `JsonObj`. O URL dinâmico de entrega é criado pela combinação das seguintes operadoras:

| Objeto | JSON |
|---|---|
| Host | `assetJsonObj["repo:repositoryId"]` |
| Raiz da API | `/adobe/assets/deliver` |
| asset-id | `assetJsonObj["repo:assetId"]` |
| seo-name | `assetJsonObj["repo:name"]` |

Abaixo estão duas maneiras de percorrer o objeto JSON:

![URL de entrega dinâmica](assets/dynamic-delivery-url.png)

* **Miniatura:** Miniaturas podem ser imagens e ativos são PDF, vídeo, imagens e assim por diante. Embora, você possa usar os atributos de altura e largura da miniatura de um ativo como a representação dinâmica da entrega.
O seguinte conjunto de representações pode ser usado para os ativos do tipo PDF:
Depois que um pdf é selecionado no sidekick, o contexto de seleção oferece as informações abaixo. Abaixo está a maneira de percorrer o objeto JSON:

  <!--![Thumbnail dynamic delivery url](image-1.png)-->

  Consulte `selection[0].....selection[4]` para obter a matriz de link de representação na captura de tela acima. Por exemplo, as principais propriedades de uma das representações de miniatura incluem:

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/as/algorithm design.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

Na captura de tela acima, o URL de entrega da representação original do PDF precisará ser incorporado à experiência do Target, se o PDF for necessário, e não sua miniatura. Por exemplo, `https://delivery-pxxxxx-exxxxx-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:8560f3a1-d9cf-429d-a8b8-d81084a42d41/original/as/algorithm design.pdf`

* **Vídeo:** Você pode usar a URL do player de vídeo para os ativos do tipo vídeo que usam um iFrame inserido. Você pode usar as seguintes representações de matriz na experiência do target:
  <!--![Video dynamic delivery url](image.png)-->

  ```
  { 
      "height": 319, 
      "width": 319, 
      "href": "https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/as/asDragDrop.2.jpg?width=319&height=319", 
      "type": "image/webp" 
  } 
  ```

  Consulte `selection[0].....selection[4]` para obter a matriz de link de representação na captura de tela acima. Por exemplo, as principais propriedades de uma das representações de miniatura incluem:

  O trecho de código na captura de tela acima é um exemplo de um ativo de vídeo. Inclui a matriz de links de representações. O `selection[5]` no trecho é o exemplo de miniatura de imagem que pode ser usada como o espaço reservado da miniatura de vídeo na experiência de destino. O `selection[5]` na matriz das representações é para o reprodutor de vídeo. Ele serve uma HTML e pode ser definido como `src` do iframe. Suporta transmissão adaptável de taxa de bits, que é a entrega do vídeo otimizada para a Web.

  No exemplo acima, a URL do reprodutor de vídeo é `https://delivery-pxxxxx-exxxxx.adobeaemcloud.com/adobe/assets/urn:aaid:aem:2fdef732-a452-45a8-b58b-09df1a5173cd/play`

+++**Interface de usuário do Seletor de ativos para Dynamic Media com recursos OpenAPI**

Após a integração com o Seletor de ativos de microfront-end do Adobe, é possível visualizar a estrutura somente de ativos de todos os ativos aprovados disponíveis no repositório de ativos da Experience Manager.

![Dynamic Media com interface de recursos OpenAPI](assets/polaris-ui.png)

* **A**: [Ocultar/Mostrar painel](#hide-show-panel)
* **B**: [Assets](#repository)
* **C**: [Classificação](#sorting)
* **D**: [Filtros](#filters)
* **E**: [Barra de pesquisa](#search-bar)
* **F**: [Classificando em ordem crescente ou decrescente](#sorting)
* **G**: Cancelar Seleção
* **H**: selecionar um ou vários ativos

+++

+++**Configurar filtros personalizados**
O Seletor de ativos do Dynamic Media com recursos OpenAPI permite configurar propriedades personalizadas e filtros com base nelas. A propriedade `filterSchema` é usada para configurar essas propriedades. A personalização pode ser exposta como `metadata.<metadata bucket>.<property name>.` em relação à qual os filtros podem ser configurados, onde,

* `metadata` são as informações de um ativo
* `embedded` é o parâmetro estático usado para configuração e
* `<propertyname>` é o nome do filtro que você está configurando

Para a configuração, as propriedades definidas no nível `jcr:content/metadata/` são expostas como `metadata.<metadata bucket>.<property name>.` para os filtros que você deseja configurar.

Por exemplo, no Seletor de ativos para Dynamic Media com recursos OpenAPI, uma propriedade em `asset jcr:content/metadata/client_name:market` é convertida em `metadata.embedded.client_name:market` para configuração de filtro.

Para obter o nome, é necessário realizar uma atividade única. Faça uma chamada de API de pesquisa para o ativo e obtenha o nome da propriedade (o bucket, essencialmente).

+++

>[!ENDTABS]

## Propriedades do Seletor de ativos {#asset-selector-properties}

Você pode usar as propriedades do Seletor de ativos para personalizar a forma como o Seletor de ativos é renderizado. A tabela a seguir lista as propriedades que você pode usar para personalizar e usar o Seletor de ativos.

| Propriedade | Tipo | Obrigatório | Padrão | Descrição |
|---|---|---|---|---|
| *painel* | Booleano | Não | Falso | Se marcado como `true`, o Seletor de ativos será renderizado em um modo de exibição de painel esquerdo. Se estiver marcado como `false`, o Seletor de ativos será renderizado na exibição modal. |
| *imsOrg* | String | Sim | | A ID do Adobe Identity Management System (IMS) atribuída durante o provisionamento do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] para sua organização. A chave `imsOrg` é necessária para autenticar se a organização que você está acessando está no Adobe IMS ou não. |
| *imsToken* | String | Não | | Token de portador IMS usado para autenticação. `imsToken` é necessário se você estiver usando um aplicativo [!DNL Adobe] para a integração. |
| *apiKey* | String | Não | | Chave de API usada para acessar o serviço de Descoberta do AEM. `apiKey` é necessário se você estiver usando uma integração de aplicativos [!DNL Adobe]. |
| *filterSchema* | Matriz | Não | | Modelo usado para configurar propriedades de filtro. Isso é útil quando quiser limitar determinadas opções de filtro no Seletor de ativos. |
| *filterFormProps* | Objeto | Não | | Especifique as propriedades de filtro que precisam ser usadas para refinar sua pesquisa. Para! exemplo, tipo MIME JPG, PNG, GIF. |
| *selectedAssets* | Matriz `<Object>` | Não |                 | Especifique os ativos selecionados quando o Seletor de ativos for renderizado. É necessária uma matriz de objetos que contenha uma propriedade de id dos ativos. Por exemplo, `[{id: 'urn:234}, {id: 'urn:555'}]` Um ativo deve estar disponível no diretório atual. Se precisar usar um diretório diferente, forneça um valor para a propriedade `path` também. |
| *acvConfig* | Objeto | Não | | A propriedade Exibição da coleção do ativo que contém o objeto com a configuração personalizada para substituir os padrões. Além disso, essa propriedade é usada com a propriedade `rail` para habilitar a exibição do painel do visualizador de ativos. |
| *i18nSymbols* | `Object<{ id?: string, defaultMessage?: string, description?: string}>` | Não |                 | Se as traduções OOTB forem insuficientes para as necessidades do aplicativo, você poderá expor uma interface pela qual poderá passar seus próprios valores localizados e personalizados pela prop `i18nSymbols`. Transmitir um valor por meio dessa interface substitui as traduções padrão fornecidas e, em vez disso, usa suas próprias traduções. Para executar a substituição, deverá transmitir um objeto [Descritor de mensagem](https://formatjs.io/docs/react-intl/api/#message-descriptor) à chave de `i18nSymbols` que deseja substituir. |
| *intl* | Objeto | Não | | O Seletor de ativos fornece traduções OOTB padrão. Você pode selecionar o idioma de tradução fornecendo uma string de localidade válida por meio da propriedade `intl.locale`. Por exemplo: `intl={{ locale: "es-es" }}` </br></br> As strings de idioma com suporte seguem os padrões [ISO 639 - Códigos](https://www.iso.org/iso-639-language-codes.html) para a representação de nomes de idiomas. </br></br> Lista de localidades compatíveis: Inglês - “en-us” (padrão) Espanhol - “es-es” Alemão - “de-de” Francês - “fr-fr” Italiano - “it-it” Japonês - “ja-jp” Coreano - “ko-kr” Português - “pt-br” Chinês (Tradicional) - “zh-cn” Chinês (Taiwan) - “zh-tw” |
| *repositoryId* | String | Não | &#39;&#39; | Repositório de onde o Seletor de ativos carrega o conteúdo. |
| *additionalAemSolutions* | `Array<string>` | Não | [ ] | Ele permite adicionar uma lista de repositórios AEM adicionais. Se nenhuma informação for fornecida nessa propriedade, somente a biblioteca de mídia ou os repositórios do AEM Assets serão considerados. |
| *hideTreeNav* | Booleano | Não |  | Especifica se deve mostrar ou ocultar a barra lateral de navegação da árvore de ativos. Usada apenas na exibição modal e, portanto, não há efeito dessa propriedade na exibição de painel. |
| *onDrop* | Função | Não | | A propriedade permite a funcionalidade soltar de um ativo. |
| *dropOptions* | `{allowList?: Object}` | Não | | Configura as opções de soltar usando “allowList”. |
| *colorScheme* | String | Não | | Configure o tema (`light` ou `dark`) do Seletor de ativos. |
| *handleSelection* | Função | Não | | Chamado com a matriz de itens do ativo quando os ativos são selecionados e o botão `Select` no modal é clicado. Essa função só é invocada na exibição modal. Para exibição do painel, use as funções `handleAssetSelection` ou `onDrop`. Exemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [Tipo de ativo selecionado](#selected-asset-type) para obter detalhes. |
| *handleAssetSelection* | Função | Não | | Invocado com uma matriz de itens enquanto os ativos estão sendo selecionados ou desmarcados. É útil quando você deseja acompanhar os ativos à medida que o usuário os seleciona. Exemplo: <pre>handleSelection=(assets: Asset[])=> {...}</pre> Consulte [Tipo de ativo selecionado](#selected-asset-type) para obter detalhes. |
| *onClose* | Função | Não | | Invocado quando o botão `Close` na exibição modal é pressionado. Somente é chamado na exibição `modal` e desconsiderado na exibição `rail`. |
| *onFilterSubmit* | Função | Não | | Invocado com itens de filtro à medida que o usuário altera critérios de filtro diferentes. |
| *selectionType* | String | Não | Solteiro | Configuração para a seleção `single` ou `multiple` de ativos de cada vez. |
| *arrastarOpções.incluir na lista de permissões* | booleano | Não | | A propriedade é usada para permitir ou negar a ação de arrastar ativos que não podem ser selecionados. |
| *aemTierType* | String | Não |  | Ela permite selecionar se você deseja mostrar ativos do nível de entrega, do nível de criação ou de ambos. Sintaxe de <br><br>: `aemTierType:[0]: "author" 1: "delivery"` <br><br> Por exemplo, se ambos `["author","delivery"]` forem usados, o alternador de repositório exibirá opções para o autor e para a entrega. |
| *handleNavigateToAsset* | Função | Não | | É uma função de Retorno de chamada para lidar com a seleção de um ativo. |
| *noWrap* | Booleano | Não | | A propriedade *noWrap* ajuda a renderizar o Seletor de ativos no painel lateral. Se essa propriedade não for mencionada, ela renderizará a *Exibição da caixa de diálogo* por padrão. |
| *tamanhoDaCaixaDeDiálogo* | controle pequeno, médio, grande, tela cheia ou tela cheia | String | Opcional | Você pode controlar o layout especificando seu tamanho com as opções fornecidas. |
| *colorScheme* | Claro ou escuro | Não | | Essa propriedade é usada para definir o tema de um aplicativo Seletor de ativos. Você pode escolher entre um tema claro ou escuro. |
| *filterRepoList* | Função | Não |  | Você pode usar a função de retorno de chamada `filterRepoList` que chama o repositório do Experience Manager e retorna uma lista filtrada de repositórios. |
| *OpçõesDeExpiração* | Função | | | Você pode usar entre as duas propriedades a seguir: **getExpiryStatus** que fornece o status de um ativo expirado. A função retorna `EXPIRED`, `EXPIRING_SOON` ou `NOT_EXPIRED` com base na data de expiração de um ativo fornecido. Consulte [personalizar ativos expirados](#customize-expired-assets). Além disso, você pode usar **allowSelectionAndDrag**, no qual o valor da função pode ser `true` ou `false`. Quando o valor é definido como `false`, o ativo expirado não pode ser selecionado ou arrastado na tela. |
| *mostrarNotificação* | | Não | | Ele permite que o Seletor de ativos mostre uma mensagem em caixa de informações personalizada para o ativo expirado. |

<!--
| *rootPath* | String | No | /content/dam/ | Folder path from which Asset Selector displays your assets. `rootPath` can also be used in the form of encapsulation. For example, given the following path, `/content/dam/marketing/subfolder/`, Asset Selector does not allow you to traverse through any parent folder, but only displays the children folders. |
| *path* | String | No | | Path that is used to navigate to a specific directory of assets when the Asset Selector is rendered. |
| *expirationDate* | Function | No | | This function is used to set the usability period of an asset. |
| *disableDefaultBehaviour* | Boolean | No | False | It is a function that is used to enable or disable the selection of an expired asset. You can customize the default behavior of an asset that is set to expire. See [customize expired assets](#customize-expired-assets). |
-->

## Exemplos de uso das propriedades do Seletor de ativos {#usage-examples}

É possível definir as [propriedades](#asset-selector-properties) do Seletor de ativos no arquivo `index.html` para personalizar a exibição do Seletor de ativos no aplicativo.

### Exemplo 1: Seletor de ativos na exibição do painel

![rail-view-example](assets/rail-view-example-vanilla.png)

Se o valor do AssetSelector `rail` estiver definido como `false` ou não for mencionado nas propriedades, o Seletor de ativos é exibido na exibição Modal por padrão. A propriedade `acvConfig` permite algumas configurações detalhadas, como Arrastar e Soltar. Visite [habilitar ou desabilitar a ação de arrastar e soltar](#enable-disable-drag-and-drop) para entender o uso da propriedade `acvConfig`.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

### Exemplo 2: popover de metadados

Use várias propriedades para definir os metadados de um ativo que deseja visualizar usando um ícone de informações. O popover de informações fornece a coleção de informações sobre o ativo ou a pasta, incluindo título, dimensões, data de modificação, local e descrição de um ativo. No exemplo abaixo, várias propriedades são usadas para exibir metadados de um ativo, por exemplo, a propriedade `repo:path` especifica o local de um ativo. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)

### Exemplo 3: propriedade de filtro personalizado na exibição do painel

Além da pesquisa facetada, o Seletor de Assets permite personalizar vários atributos para refinar sua pesquisa do [!DNL Adobe Experience Manager] como um aplicativo do [!DNL Cloud Service]. Adicione o código a seguir para adicionar filtros de pesquisa personalizados em seu aplicativo. No exemplo abaixo, a pesquisa `Type Filter` que filtra o tipo de ativo entre Imagens, Documentos ou Vídeos ou o tipo de filtro adicionado para a pesquisa.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->

## Trechos de código de configuração funcional{#code-snippets}

Defina os pré-requisitos no arquivo `index.html` ou em um arquivo semelhante na implementação do aplicativo para definir os detalhes de autenticação para acessar o repositório [!DNL Experience Manager Assets]. Depois de concluído, você pode adicionar trechos de código de acordo com sua exigência.

### Personalizar painel de filtro {#customize-filter-panel}

Você pode adicionar o seguinte trecho de código no objeto `assetSelectorProps` para personalizar o painel de filtro:

```
filterSchema: [
    {
    header: 'File Type',
    groupKey: 'TopGroup',
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    {
    label: 'Images',
    value: '<comma separated mimetypes, without space, that denote all images, for e.g., image/>',
    },
    {
    label: 'Videos',
    value: '<comma separated mimetypes, without space, that denote all videos for e.g., video/,model/vnd.mts,application/mxf>'
    }
    ]
    }
    ]
    },
    {
    fields: [
    {
    element: 'checkbox',
    name: 'type',
    options: [
    { label: 'JPG', value: 'image/jpeg' },
    { label: 'PNG', value: 'image/png' },
    { label: 'TIFF', value: 'image/tiff' },
    { label: 'GIF', value: 'image/gif' },
    { label: 'MP4', value: 'video/mp4' }
    ],
    columns: 3,
    },
    ],
    header: 'Mime Types',
    groupKey: 'MimeTypeGroup',
    }},
    {
    fields: [
    {
    element: 'checkbox',
    name: 'property=metadata.application.xcm:keywords.value',
    options: [
    { label: 'Fruits', value: 'fruits' },
    { label: 'Vegetables', value: 'vegetables'}
    ],
    columns: 3,
    },
    ],
    header: 'Food Category',
    groupKey: 'FoodCategoryGroup',
    }
],
```

### Personalizar informações na exibição modal {#customize-info-in-modal-view}

Você pode personalizar a exibição detalhada de um ativo ao clicar no ícone ![informações](assets/info-icon.svg). Execute o código abaixo:

```
// Create an object infoPopoverMap and set the property `infoPopoverMap` with it in assetSelectorProps
const infoPopoverMap = (map) => {
// for example, to skip `path` from the info popover view
let defaultPopoverData = PureJSSelectors.getDefaultInfoPopoverData(map);
return defaultPopoverData.filter((i) => i.label !== 'Path'
};
assetSelectorProps.infoPopoverMap = infoPopoverMap;
```

### Ativar ou desativar o modo arrastar e soltar {#enable-disable-drag-and-drop}

Adicione as seguintes propriedades a `assetSelectorProp` para habilitar o modo arrastar e soltar. Para desabilitar arrastar e soltar, substitua o parâmetro `true` por `false`.

```
rail: true,
acvConfig: {
dragOptions: {
allowList: {
'*': true,
},
},
selectionType: 'multiple'
}

// the drop handler to be implemented
function drop(e) {
e.preventDefault();
// following helps you get the selected assets – an array of objects.
const data = JSON.parse(e.dataTransfer.getData('collectionviewdata'));
}
```

### Seleção do Assets {#selection-of-assets}

O Tipo de ativo selecionado é uma matriz de objetos que contém as informações do ativo ao usar as funções `handleSelection`, `handleAssetSelection`, e `onDrop`.

Execute as seguintes etapas para configurar a seleção de um ou vários ativos:

```
acvConfig: {
selectionType: 'multiple' // 'single' for single selection
}
// the `handleSelection` callback, always gets you the array of selected assets
```

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
        'https://ns.adobe.com/adobecloud/rel/rendition': Array<{
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

| Propriedade | Tipo | Descrição |
|---|---|---|
| *repositório:repositoryId* | string | Identificador exclusivo do repositório onde o ativo está armazenado. |
| *repositório:id* | string | Identificador exclusivo do ativo. |
| *repositório:assetClass* | string | A classificação do ativo (por exemplo, imagem, vídeo ou documento). |
| *repositório:name* | string | O nome do ativo, incluindo a extensão de arquivo. |
| *repositório:size* | número | O tamanho do ativo em bytes. |
| *repositório:path* | string | O local do ativo no repositório. |
| *repositório:ancestors* | `Array<string>` | Uma matriz de itens ancestrais do ativo no repositório. |
| *repositório:state* | string | Estado atual do ativo no repositório (Por exemplo, ativo, excluído etc.). |
| *repositório:createdBy* | string | O usuário ou sistema que criou o ativo. |
| *repositório:createDate* | string | A data e a hora em que o ativo foi criado. |
| *repositório:modifiedBy* | string | O usuário ou sistema que modificou o ativo pela última vez. |
| *repositório:modifyDate* | string | A data e a hora em que o ativo foi modificado pela última vez. |
| *dc:format* | string | O formato do ativo, como o tipo de arquivo (por exemplo, JPEG, PNG etc.). |
| *tiff:imageWidth* | número | A largura de um ativo. |
| *tiff:imageLength* | número | A altura de um ativo. |
| *computedMetadata* | `Record<string, any>` | Um objeto que representa um compartimento para todos os metadados do ativo de todos os tipos (repositório, aplicativo ou metadados incorporados). |
| *_links* | `Record<string, any>` | Links de hipermídia do ativo associado. Inclui links para recursos como metadados e representações. |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition>* | `Array<Object>` | Matriz de objetos que contém informações sobre representações do ativo. |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].href>* | string | O URI da representação. |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].type>* | string | O tipo MIME da representação. |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].repo:size>&#39;* | número | O tamanho da representação em bytes. |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].width>* | número | A largura da representação. |
| *_links.<https://ns.adobe.com/adobecloud/rel/rendition[].height>* | número | A altura da representação. |

<!--For a complete list of properties and detailed example, visit [Asset Selector Code Example](https://github.com/adobe/aem-assets-selectors-mfe-examples).-->

### Personalizar ativos expirados {#customize-expired-assets}

O Seletor de ativos permite controlar o uso de um ativo expirado. Você pode personalizar o ativo expirado com um selo **Expirando em breve** que pode ajudá-lo a saber com antecedência sobre os ativos que expirarão em 30 dias a partir da data atual. Além disso, isso pode ser personalizado de acordo com a exigência. Você também pode permitir a seleção de um ativo expirado na tela ou vice-versa. A personalização de um ativo expirado pode ser feita usando alguns snippets de código de várias maneiras:

<!--{
    getExpiryStatus: function, // to control Expired/Expiring soon badges of the asset
    allowSelectionAndDrag: boolean, // set true to allow the selection of expired assets on canvas, set false, otherwise.
}-->

```
expiryOptions: {
    getExpiryStatus: getExpiryStatus;
}
```

#### Seleção de um ativo expirado {#selection-of-expired-asset}

Você pode personalizar o uso de um ativo expirado para torná-lo selecionável ou não selecionável. É possível personalizar se deseja permitir ou não o arrastar e soltar de um ativo expirado na tela Seletor de ativos. Para fazer isso, use os seguintes parâmetros para tornar um ativo não selecionável na tela:

```
expiryOptions:{
    allowSelectionAndDrop: false;
}
```

<!--
Additionally, To do this, navigate to **[!UICONTROL Disable default expiry behavior]** under the [!UICONTROL Controls] tab and set the boolean value to `true` or `false` as per the requirement. If `true` is selected, you can see the select box over the expired asset, otherwise it remains unselected. You can hover to the info icon of an asset to know the details of an expired asset. 

![Disable default expiry behavior](assets/disable-default-expiry-behavior.png)-->

#### Configuração da duração de um ativo expirado {#set-duration-of-expired-asset}

O trecho de código a seguir ajuda a definir o selo **Expirando em Breve** para os ativos que expiram nos próximos cinco dias: <!--The `expirationDate` property is used to set the expiration duration of an asset. Refer to the code snippet below:-->

```
/**
  const getExpiryStatus = async (asset) => {
  if (!asset.expirationDate) {
    return null;
  }
  const currentDate = new Date();
  const millisecondsInDay = 1000 * 60 * 60 * 24;
  const fiveDaysFromNow = new Date(value: currentDate.getTime() + 5 * millisecondsInDay);
  const expirationDate = new Date(asset.expirationDate);
  if (expirationDate.getTime() < currentDate.getTime()) {
    return 'EXPIRED';
  } else if (expirationDate.getTime() < fiveDaysFromNow.getTime()) {
    return 'EXPIRING_SOON';
  } else {
    return 'NOT_EXPIRED';
  }
};
```

<!--In the above code snippet, the `getExpiryStatus` function is used to show the **Expiring soon** badge that have expiration date stored in `customExpirationDate`. Additionally, it sets the expiration date of an asset to five days from the current date. The `millisecondsInDay` helps you set expiry of an asset by specifying the time range in milliseconds. You can replace milliseconds with hours directly or customize function as per the requirement. Whereas, the `getTime()` function returns the number of milliseconds for the mentioned date. See [properties](#asset-selector-properties) to know about `expirationDate` property.-->

Consulte o exemplo a seguir para entender como a propriedade funciona para buscar a data e hora atuais:

```
const currentData = new Date();
currentData.getTime(),
```

retorna `1718779013959` que é o formato de data 2024-06-19T06:36:53.959Z.

#### Personalizar mensagem em caixa de informações de um ativo expirado {#customize-toast-message}

A propriedade `showToast` é usada para personalizar a mensagem do sistema que você deseja mostrar em um ativo expirado.

Sintaxe:

```
{
    type: 'ERROR', 'NEUTRAL', 'INFO', 'SUCCESS',
    message: '<message to be shown>',
    timeout: optional,
}
```

O tempo limite padrão é de 500 milissegundos. Ao passo que, você pode modificá-lo de acordo com o requisito. Além disso, passar o valor `timeout: 0` mantém a janela aberta até que você clique no botão cruzado.

Veja abaixo um exemplo para mostrar uma mensagem em caixa de informações quando é necessário proibir a seleção de uma pasta e mostrar uma mensagem correspondente:

```
const showToast = {
    type: 'ERROR',
    message: 'Folder cannot be selected',
    timeout: 5000,
}
```

Use o seguinte trecho de código para mostrar uma mensagem do sistema para o uso de um ativo expirado:

![mensagem em caixa de informações](assets/toast-message.png)

### Filtro de invocação contextual{#contextual-invocation-filter}

O Seletor de ativos permite adicionar um filtro seletor de tags. Ela é compatível com um grupo de tags que combina todas as tags relevantes a um grupo de tags específico. Além disso, permite selecionar tags adicionais correspondentes ao ativo que você está procurando. Além disso, você também pode definir os grupos de tags padrão no filtro de chamada contextual que são usados principalmente por você para que sejam acessíveis a você em qualquer lugar.

>[!NOTE]
>
> * É necessário adicionar um trecho de código de invocação contextual para ativar o filtro de marcação na pesquisa.
> * É obrigatório usar a propriedade de nome correspondente ao tipo de grupo de marcas `(property=xcm:keywords.id=)`.

Sintaxe:

```
const filterSchema=useMemo(() => {
    return: [
        {
            element: 'taggroup',
            name: 'property=xcm:keywords.id='
        },
    ];
}, []);
```

Para adicionar grupos de tags no painel Filtros, é obrigatório adicionar pelo menos um grupo de tags como padrão. Além disso, use o trecho de código abaixo para adicionar as tags padrão pré-selecionadas do grupo de tags.

```
export const WithAssetTags = (props) = {
const [selectedTags, setSelectedTags] = useState (
new Set(['orientation', 'color', 'facebook', 'experience-fragments:', 'dam', 'monochrome'])
const handleSelectTags = (selected) => {
setSelectedTags (new Set (selected)) ;
};
const filterSchema = useMemo ((); => {
    return {
        schema: [
            ｛
                fields: [
                    {
                    element: 'checkbox', 
                    name: 'property=xcm:keywords=', 
                    defaultValue: Array. from(selectedTags), 
                    options: assetTags, 
                    orientation: 'vertical',
                    },
                ],
    header: 'Asset Tags', 
    groupkey: 'AssetTagsGroup',
        ],
    },
｝；
}, [selectedTags]);
```

![filtro de grupo de marcas](assets/tag-group.gif)

## Lidar com a seleção de ativos usando o esquema de objeto {#handling-selection}

A propriedade `handleSelection` é usada para lidar com seleções únicas ou múltiplas de ativos no Seletor de ativos. O exemplo abaixo declara a sintaxe de uso de `handleSelection`.

![handle-selection](assets/handling-selection.png)

## Desabilitação da seleção de Assets {#disable-selection}

Desativar seleção é usado para ocultar ou desativar a seleção de ativos ou pastas. Ela oculta a caixa de seleção de seleção do cartão ou ativo, impedindo-o de ser selecionado. Para usar esse recurso, você pode declarar a posição de um ativo ou pasta que deseja desativar em uma matriz. Por exemplo, se você quiser desativar a seleção de uma pasta que aparece na primeira posição, poderá adicionar o seguinte código:
`disableSelection: [0]:folder`

Você pode fornecer à matriz uma lista de tipos MIME (como imagem, pasta, arquivo ou outros tipos MIME, por exemplo, image/jpeg) que deseja desativar. Os tipos MIME declarados são mapeados em `data-card-type` e `data-card-mimetype` atributos de um ativo.

Além disso, o Assets com seleção desativada é arrastável. Para desabilitar a ação de arrastar e soltar um tipo de ativo específico, você pode usar a propriedade `dragOptions.allowList`.

A sintaxe de desabilitar seleção é a seguinte:

```
(args)=> {
    return(
        <ASDialogWrapper
            {...args}
            disableSelection={args.disableSelection}
            handleAssetSelection={action('handleAssetSelection')}
            handleSelection={action('handleSelection')}
            selectionType={args.selectionType}
        />
    );
}
```

>[!NOTE]
>
> No caso de um ativo, a caixa de seleção Selecionar fica oculta, enquanto no caso de uma pasta, a pasta não pode ser selecionada, mas a navegação da pasta mencionada ainda é exibida.

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

O Seletor de ativos também permite alternar repositórios para seleção de ativos. Você pode selecionar o repositório de sua escolha no menu suspenso disponível no painel esquerdo. As opções de repositório disponíveis na lista suspensa se baseiam na propriedade `repositoryId` definida no arquivo `index.html`. Ela se baseia no ambiente da organização IMS selecionada que é acessado pelo usuário conectado. Os consumidores podem transmitir um `repositoryID` de sua preferência e, nesse caso, o Seletor de ativos interrompe a renderização do alternador de repositório e renderiza ativos somente do repositório especificado.

### Repositório de ativos

É uma coleção de pastas de ativos que você pode usar para executar operações.

### Filtros prontos para uso {#filters}

O Seletor de ativos também fornece opções de filtro prontas para uso para refinar os resultados da pesquisa. Os filtros disponíveis são os seguintes:

* **[!UICONTROL Status]:** inclui o estado atual do ativo entre `all`, `approved`, `rejected` ou `no status`.
* **[!UICONTROL Tipo de arquivo]:** inclui `folder`, `file`, `images`, `documents` ou `video`.
* **[!UICONTROL Status de expiração]:** menciona os ativos com base em sua duração de expiração. Você pode marcar a caixa de seleção `[!UICONTROL Expired]` para filtrar ativos que expiraram ou definir `[!UICONTROL Expiration Duration]` de um ativo para exibir ativos com base em sua duração de expiração. Quando um ativo já expirou ou está prestes a expirar, um selo é exibido representando o mesmo. Além disso, você pode controlar se deseja permitir o uso (ou arrastar e soltar) de um ativo expirado. Veja mais sobre [personalizar ativos expirados](#customize-expired-assets). Por padrão, o selo **Expirando em breve** é exibido para ativos que expiram nos próximos 30 dias. No entanto, você pode configurar a expiração usando a propriedade `expirationDate`.

  >[!TIP]
  >
  > Para visualizar ou filtrar ativos com base em suas datas de expiração futuras, mencione o intervalo de datas futuro no campo `[!UICONTROL Expiration Duration]`. Ele exibe os ativos com o selo **expirando em breve** neles.

* **[!UICONTROL Tipo MIME]:** inclui `JPG`, `GIF`, `PPTX`, `PNG`, `MP4`, `DOCX`, `TIFF`, `PDF`, `XLSX`.
* **[!UICONTROL Tamanho da Imagem]:** inclui largura mínima/máxima, altura mínima/máxima da imagem.

  ![rail-view-example](assets/filters-asset-selector.png)

### Pesquisa personalizada

Além da pesquisa de texto completo, o Seletor de ativo permite pesquisar ativos em arquivos usando a pesquisa personalizada. Você pode usar filtros de pesquisa personalizados nos modos de exibição Modal e Painel.

![custom-search](assets/custom-search1.png)

Também é possível criar um filtro de pesquisa padrão para salvar os campos que você pesquisa com frequência e usá-los depois. Para criar uma pesquisa personalizada para seus ativos, você pode usar a propriedade `filterSchema`.

### Barra de pesquisa {#search-bar}

O Seletor de ativos permite executar uma pesquisa de texto completo dos ativos no repositório selecionado. Por exemplo, se você digitar a palavra-chave `wave` na barra de pesquisa, todos os ativos com a palavra-chave `wave` mencionada em qualquer uma das propriedades de metadados serão exibidos.

### Classificação {#sorting}

Você pode classificar ativos no Seletor de ativos por nome, dimensões ou tamanho de um ativo. Também é possível classificar os ativos em ordem crescente ou decrescente.

### Tipos de visualização {#types-of-view}

O Seletor de ativos permite exibir o ativo em quatro exibições diferentes:

* **![exibição de lista](assets/do-not-localize/list-view.png) [!UICONTROL Exibição de Lista]** A exibição de lista exibe arquivos e pastas roláveis em uma única coluna.
* **![exibição de grade](assets/do-not-localize/grid-view.png) [!UICONTROL Exibição de grade]** A exibição de grade exibe arquivos e pastas com rolagem em uma grade de linhas e colunas.
* **![exibição de galeria](assets/do-not-localize/gallery-view.png) [!UICONTROL exibição de galeria]** A exibição de galeria exibe arquivos ou pastas em uma lista horizontal bloqueada no centro.
* **![exibição em cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL exibição em cascata]** A exibição em cascata exibe arquivos ou pastas no formato de uma Bridge.

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



<!--Best Practice-->
<!--
+++**Control default selection of the filter**
You can make the selection of filter default by implementing the following code snippet:

```
"defaultValue": [
    "image/*",
    "application/*"
],

{
    "label": "Documents",
    "value": "application/*"
}
```

+++
-->
