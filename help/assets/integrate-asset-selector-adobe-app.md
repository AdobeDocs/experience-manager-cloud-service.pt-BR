---
title: Seletor de ativos para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Integrar o seletor de ativos a vários aplicativos de Adobe, não Adobe e de terceiros.
role: Admin, User
exl-id: a0c030e2-2213-406b-ad92-4761f1e2ee9f
source-git-commit: 7590e0240f3f429831aee5d9620ea4fa6f32847b
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 8%

---

# Integrar o seletor de ativos ao aplicativo Adobe {#integrate-asset-selector-with-adobe-app}

O Seletor de ativos permite a integração usando vários aplicativos Adobe para que eles trabalhem em conjunto de maneira contínua.

## Pré-requisitos{#prereqs-adobe-app}

Use os seguintes pré-requisitos se estiver integrando o Seletor de ativos a um aplicativo do [!DNL Adobe]:

* [Métodos de comunicação](/help/assets/overview-asset-selector.md#prereqs)
* imsOrg
* imsToken
* apikey

## Integrar o Seletor de ativos a um aplicativo do [!DNL Adobe] {#adobe-app-integration-vanilla}

O exemplo a seguir demonstra o uso do Seletor de Ativos ao executar um aplicativo [!DNL Adobe] no Unified Shell ou quando você já gerou `imsToken` para autenticação.

Inclua o pacote do Seletor de ativos no código usando a marca `script`, como mostrado nas _linhas 6-15_ do exemplo abaixo. Depois que o script for carregado, a variável global `PureJSSelectors` estará disponível para uso. Defina o Seletor de ativos [propriedades](/help/assets/asset-selector-properties.md) conforme mostrado em _linhas 16-23_. As propriedades `imsOrg` e `imsToken` são necessárias para autenticação no aplicativo Adobe. A propriedade `handleSelection` é usada para manipular os ativos selecionados. Para renderizar o Seletor de ativos, chame a função `renderAssetSelector` como mencionado na _linha 17_. O Seletor de ativos é exibido no elemento de container `<div>`, conforme mostrado nas _linhas 21 e 22_.

Seguindo essas etapas, você pode usar o Seletor de ativos com seu aplicativo [!DNL Adobe].

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Asset Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
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

### ImsAuthProps {#ims-auth-props}

As propriedades `ImsAuthProps` definem as informações de autenticação e o fluxo que o Seletor de ativos usa para obter um `imsToken`. Ao definir essas propriedades, é possível controlar como o fluxo de autenticação deve se comportar e registrar ouvintes para vários eventos de autenticação.

| Nome de propriedade | Descrição |
|---|---|
| `imsClientId` | Um valor de string que representa a ID do cliente IMS usada para fins de autenticação. Esse valor é fornecido pelo Adobe e é específico para sua organização de Adobe AEM CS. |
| `imsScope` | Descreve os escopos usados na autenticação. Os escopos determinam o nível de acesso que o aplicativo tem aos recursos da organização. Vários escopos podem ser separados por vírgulas. |
| `redirectUrl` | Representa o URL para o qual o usuário é redirecionado após a autenticação. Normalmente, esse valor é definido como o URL atual do aplicativo. Se um `redirectUrl` não for fornecido, `ImsAuthService` usará o redirectUrl usado para registrar o `imsClientId` |
| `modalMode` | Um booleano que indica se o fluxo de autenticação deve ser exibido em um modal (pop-up) ou não. Se definido como `true`, o fluxo de autenticação será exibido em um pop-up. Se definido como `false`, o fluxo de autenticação será exibido em um recarregamento de página completo. _Observação:_ para obter um UX melhor, você pode controlar este valor dinamicamente se o usuário tiver o pop-up do navegador desabilitado. |
| `onImsServiceInitialized` | Uma função de retorno de chamada que é chamada quando o serviço de autenticação do Adobe IMS é inicializado. Essa função recebe um parâmetro, `service`, que é um objeto que representa o serviço Adobe IMS. Consulte [`ImsAuthService`](#imsauthservice-ims-auth-service) para obter mais detalhes. |
| `onAccessTokenReceived` | Uma função de retorno de chamada que é chamada quando um `imsToken` é recebido do serviço de autenticação do Adobe IMS. Esta função recebe um parâmetro, `imsToken`, que é uma cadeia de caracteres que representa o token de acesso. |
| `onAccessTokenExpired` | Uma função de retorno de chamada chamada chamada quando um token de acesso expira. Normalmente, essa função é usada para acionar um novo fluxo de autenticação para obter um novo token de acesso. |
| `onErrorReceived` | Uma função de retorno de chamada que é chamada quando ocorre um erro durante a autenticação. Essa função usa dois parâmetros: o tipo de erro e a mensagem de erro. O tipo de erro é uma cadeia de caracteres que representa o tipo de erro, e a mensagem de erro é uma cadeia de caracteres que representa a mensagem de erro. |

### ImsAuthService {#ims-auth-service}

A classe `ImsAuthService` manipula o fluxo de autenticação para o Seletor de ativos. Ele é responsável por obter um `imsToken` do serviço de autenticação do Adobe IMS. O `imsToken` é usado para autenticar o usuário e autorizar o acesso ao [!DNL Adobe Experience Manager] como um repositório do Assets [!DNL Cloud Service]. O ImsAuthService usa as propriedades `ImsAuthProps` para controlar o fluxo de autenticação e registrar ouvintes de vários eventos de autenticação. Você pode usar a conveniente função [`registerAssetsSelectorsAuthService`](#purejsselectorsregisterassetsselectorsauthservice) para registrar a instância _ImsAuthService_ com o Seletor de ativos. As seguintes funções estão disponíveis na classe `ImsAuthService`. No entanto, se você estiver usando a função _registerAssetsSelectorsAuthService_, não será necessário chamar essas funções diretamente.

| Nome da função | Descrição |
|---|---|
| `isSignedInUser` | Determina se o usuário está conectado ao serviço no momento e retorna um valor booleano correspondente. |
| `getImsToken` | Recupera a autenticação `imsToken` para o usuário conectado no momento, que pode ser usada para autenticar solicitações para outros serviços, como a geração de _representação de ativos. |
| `signIn` | Inicia o processo de entrada do usuário. Esta função usa o `ImsAuthProps` para mostrar autenticação em um pop-up ou em um recarregamento de página completo |
| `signOut` | Desconecta o usuário do serviço, invalidando seu token de autenticação e exigindo que ele entre novamente para acessar recursos protegidos. Chamar essa função recarregará a página atual. |
| `refreshToken` | Atualiza o token de autenticação do usuário conectado no momento, evitando a expiração e garantindo acesso ininterrupto aos recursos protegidos. Retorna um novo token de autenticação que pode ser usado para solicitações subsequentes. |

### Validação com o token IMS fornecido {#validation-ims-token}

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

### Registrar retornos de chamada para o serviço IMS {#register-callback-ims-service}

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

>[!MORELIKETHIS]
>
>* [Integrar o Seletor de ativos a vários aplicativos](/help/assets/integrate-asset-selector.md)
>* [Propriedades do Seletor de ativos](/help/assets/asset-selector-properties.md)
>* [Integrar o Seletor de ativos ao Dynamic Media com recursos OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Personalizações do Seletor de ativos](/help/assets/asset-selector-customization.md)
