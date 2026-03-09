---
title: Integrar o Seletor de fragmentos do conteúdo a um aplicativo do Adobe
description: Integrar o seletor de Fragmento de conteúdo a vários aplicativos do Adobe.
role: Admin, User, Developer
source-git-commit: a16d9e9fa6483a89283c595372abcc437d1d962e
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# Integrar o seletor de fragmentos do conteúdo ao aplicativo do Adobe {#integrate-content-fragment-selector-with-adobe-application}

O Seletor de fragmentos de conteúdo permite a integração com vários aplicativos do Adobe para que eles trabalhem em conjunto de maneira contínua.

## Pré-requisitos {#prerequisites}

Use os seguintes pré-requisitos se estiver integrando o Seletor de fragmento de conteúdo a um aplicativo do Adobe:

* [Pré-requisitos](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsOrg
* imsToken
* apikey

## Integrar o Seletor de fragmentos do conteúdo a um aplicativo do Adobe {#integrate-content-fragment-selector-with-an-adobe-application}

O exemplo a seguir demonstra o uso do Seletor de fragmento de conteúdo ao executar um aplicativo do Adobe no Unified Shell ou quando você já tem um `imsToken` gerado para autenticação.

Inclua o pacote do Seletor de fragmento de conteúdo no código usando a tag `script`, como mostrado no exemplo abaixo.

* Depois que o script for carregado, a variável global `PureJSContentFragmentSelectors` estará disponível para uso.
* Defina as [propriedades](/help/headless/content-fragment-selector/properties.md) do Seletor de fragmento de conteúdo:

   * as propriedades `imsOrg` e `imsToken` são necessárias para autenticação no aplicativo Adobe
   * a propriedade `handleSelection` é usada para manipular os fragmentos selecionados.

* Para renderizar o Seletor de fragmentos de conteúdo, chame a função `renderFragmentSelector`.
* O Seletor de Fragmento do Conteúdo é exibido no elemento de contêiner `<div>`.

Seguindo essas etapas, é possível usar o Seletor de fragmento de conteúdo com o aplicativo do Adobe.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
    <title>Fragment Selector</title>
    <script src="https://experience.adobe.com/solutions/CQ-fragmentss-selectors/static-fragments/resources/fragments-selectors.js"></script>
    <script>
        // get the container element in which we want to render the FragmentSelector component
        const container = document.getElementById('fragment-selector-container');
        // imsOrg and imsToken are required for authentication in Adobe application
        const fragmentSelectorProps = {
            imsOrg: 'example-ims@AdobeOrg',
            imsToken: "example-imsToken",
            apiKey: "example-apiKey-associated-with-imsOrg",
            handleSelection: (fragmentss: SelectedFragmentType[]) => {},
        };
        // Call the `renderFragmentSelector` available in PureJSContentFragmentSelectors globals to render FragmenttSelector
        PureJSContentFragmentSelectors.renderFragmentSelector(container, fragmentSelectorProps);
    </script>
</head>

<body>
    <div id="fragment-selector-container" style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px;">
    </div>
</body>

</html>
```

### ImsAuthProps {#imsauthprops}

As propriedades `ImsAuthProps` definem as informações de autenticação e o fluxo que o Seletor de fragmento de conteúdo usa para obter um `imsToken`. Ao definir essas propriedades, é possível controlar como o fluxo de autenticação se comporta e registrar ouvintes para vários eventos de autenticação.

Para obter detalhes da propriedade, consulte [Propriedades de ImsAuthProps](/help/headless/content-fragment-selector/properties.md#imsauthprops-properties)

### ImsAuthService {#imsauthservice}

A classe `ImsAuthService` manipula o fluxo de autenticação para o Seletor de fragmentos. Ele é responsável por obter um `imsToken` do serviço de autenticação do Adobe IMS. O `imsToken` é usado para autenticar o usuário e autorizar o acesso ao repositório do AEM as a Cloud Service. `ImsAuthService` usa as propriedades `ImsAuthProps` para controlar o fluxo de autenticação e registrar ouvintes de vários eventos de autenticação. Você pode usar a função `registerFragmentsSelectorsAuthService` para registrar a instância `ImsAuthService` com o Seletor de fragmentos. As seguintes funções estão disponíveis na classe `ImsAuthService`. No entanto, se você estiver usando a função `registerFragmentsSelectorsAuthService`, não será necessário chamar essas funções diretamente.

Para obter detalhes da propriedade, consulte [Propriedades de ImsAuthService](/help/headless/content-fragment-selector/properties.md#imsauthservice-properties)

### Validação com o token IMS fornecido {#validation-with-provided-ims-token}

```javascript
<script>
    const apiToken="<valid IMS token>";
    function handleSelection(selection) {
    console.log("Selected fragment: ", selection);
    };
    function renderFragmentSelectorInline() {
    console.log("initializing Fragment Selector");
    const props = {
    "repositoryId": "delivery-p64502-e544757.adobeaemcloud.com",
    "apiKey": "ngdm_test_client",
    "imsOrg": "<IMS org>",
    "imsToken": apiToken,
    handleSelection,
    hideTreeNav: true
    }
    const container = document.getElementById('fragment-selector-container');
    PureJSContentFragmentSelectors.renderFragmentSelector(container, props);
    }
    $(document).ready(function() {
    renderFragmentSelectorInline();
    });
</script>
```

### Registrar retornos de chamada para o serviço IMS {#register-callbacks-to-ims-service}

```java
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
