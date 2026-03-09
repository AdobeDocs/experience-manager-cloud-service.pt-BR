---
title: Integrar o seletor de fragmentos do conteúdo a aplicativos de terceiros ou que não sejam da Adobe
description: Integrar o seletor de Fragmento do conteúdo a vários aplicativos da Adobe, que não sejam da Adobe e de terceiros.
role: Admin, User, Developer
source-git-commit: 3af1a89489af96bf9c9908aea7fb20883956517b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---

# Integração com um aplicativo que não seja da Adobe {#integration-with-non-adobe-application}

O Seletor de fragmentos de conteúdo permite a integração com vários aplicativos que não sejam da Adobe ou de terceiros para que eles trabalhem em conjunto de maneira contínua.

## Pré-requisitos {#prerequisites}

Use os seguintes pré-requisitos se estiver integrando o Seletor de fragmento de conteúdo a um aplicativo que não seja da Adobe:

* [Pré-requisitos](/help/headless/content-fragment-selector/overview.md#prerequisites)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

Ao integrá-lo a um aplicativo que não seja do Adobe, o Seletor de fragmento de conteúdo oferece suporte à autenticação para o repositório do Adobe Experience Manager (AEM) as a Cloud Service usando propriedades do Identity Management System (IMS) como `imsScope` ou `imsClientID`.

## Configurar o Seletor de fragmentos de conteúdo para um aplicativo que não seja do Adobe {#configure-content-fragment-selector-for-a-non-adobe-application}

Para configurar o Seletor de fragmento de conteúdo para um aplicativo que não seja da Adobe, primeiro você deve registrar um tíquete de suporte para provisionamento antes de prosseguir com as etapas de integração.

### Registro de um tíquete de suporte {#logging-a-support-ticket}

Etapas para registrar um tíquete de suporte pela Admin Console:

1. Adicione o **Seletor de fragmento do conteúdo com fragmentos do AEM** no título do tíquete.

1. Na descrição, forneça os seguintes detalhes:

   * URL do Experience Manager as a Cloud Service (ID do programa e ID do ambiente).
   * Nomes de domínio em que o aplicativo Web que não é da Adobe está hospedado.

## Etapas de integração {#integration-steps}

Use o exemplo de arquivo `index.html` a seguir para autenticação ao integrar o Seletor de fragmento de conteúdo a um aplicativo que não seja da Adobe:

* Acesse o pacote do Seletor de fragmentos de conteúdo usando a marca `Script`.

* Defina as propriedades do fluxo IMS, como `imsClientId`, `imsScope` e `redirectURL`.

   * A função requer a definição de pelo menos uma das propriedades `imsClientId` e `imsScope`.
   * Se você não definir um valor para `redirectURL`, a URL de redirecionamento registrada para a ID do cliente será usada.

* Como o exemplo não tem um `imsToken` gerado, use as funções `registerFragmentsSelectorsAuthService` e `renderFragmentSelectorWithAuthFlow`.

   * Use a função `registerFragmentsSelectorsAuthService` antes de `renderFragmentSelectorWithAuthFlow` para registrar `imsToken` com o Seletor de Fragmento de Conteúdo.
   * A Adobe recomenda chamar `registerFragmentsSelectorsAuthService` ao instanciar o componente.

* Defina a autenticação e outras propriedades relacionadas ao acesso do Fragments as a Cloud Service na seção `const props`.
* A variável global `PureJSContentFragmentSelectors` é usada para renderizar o Seletor de fragmento de conteúdo no navegador da Web.
* O Seletor de Fragmento de Conteúdo é renderizado no elemento de contêiner `<div>`. O exemplo usa uma caixa de diálogo para exibir o Seletor de fragmento de conteúdo.

**Exemplo`ìndex.html`**

```html {line-numbers="true"}
<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <link rel="icon" type="image/svg+xml" href="/vite.svg" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>testing-cf-mfe-integration-with-3rd-party-app</title>
        <script
            id="content-fragments-selector"
            src="https://experience.adobe.com/solutions/CQ-sites-content-fragment-selector/static-assets/resources/content-fragment-selector.js"
        ></script>
        <script>
            const imsProps = {
                imsClientId: '<IMS_CLIENT_ID>',
                imsScope:
                    'additional_info.projectedProductContext, AdobeID, openid, read_organizations',
                redirectUrl: window.location.href,
                onImsServiceInitialized: (service) => {
                    // invoked when the ims service is initialized and is ready
                    console.log('onImsServiceInitialized', service);
                },
                onAccessTokenReceived: (token) => {
                    console.log('onAccessTokenReceived', token);
                },
                onAccessTokenExpired: () => {
                    console.log('onAccessTokenError');
                    // re-trigger sign-in flow
                },
                onErrorReceived: (type, msg) => {
                    console.log('onErrorReceived', type, msg);
                },
            };

            function load() {
                const registeredTokenService =
                    PureJSContentFragmentSelectors.registerContentFragmentSelectorAuthService(
                        imsProps
                    );
                imsInstance = registeredTokenService;
            }

            // initialize the IMS flow before attempting to render the content fragment selector
            load();

            // function that will render the content fragment selector
            function renderContentFragmentSelectorWithAuthFlow() {
                const contentFragmentSelectorDialog = document.getElementById(
                    'content-fragment-selector-dialog'
                );

                const contentFragmentSelectorProps = {
                    inventoryViewToggleEnabled: true,
                    isOpen: true,
                    noWrap: false,
                    orgId: 'YOUR_ORG_ID@AdobeOrg',
                    // repoId: "author-p12345-e67890.adobeaemcloud.com", // if wanted to restrict to a specific repo
                    runningInUnifiedShell: false,
                    onDismiss: () => contentFragmentSelectorDialog.close(),
                    onSubmit: ({ contentFragments }) => {
                        const selectedContentFragment = contentFragments[0];
                        alert(selectedContentFragment.path);
                    },
                };
                // container element on which you want to render the ContentFragmentSelector component
                const container = document.getElementById('content-fragment-selector');

                /// Use the PureJSContentFragmentSelectors in globals to render the ContentFragmentSelector component
                PureJSContentFragmentSelectors.renderContentFragmentSelectorWithAuthFlow(
                    container,
                    contentFragmentSelectorProps,
                    () => contentFragmentSelectorDialog.showModal()
                );
            }
        </script>
    </head>
    <body>
        <div>
            <button onclick="renderContentFragmentSelectorWithAuthFlow()">
                Content Fragment Selector - Select Content Fragments with Ims Flow
            </button>
        </div>
        <dialog id="content-fragment-selector-dialog">
            <div
                id="content-fragment-selector"
                style="height: calc(100vh - 80px); width: calc(100vw - 60px); margin: -20px"
            ></div>
        </dialog>
    </body>
</html>
```

## Não foi possível acessar o repositório de entrega {#unable-to-access-delivery-repository}

Se você tiver o Seletor de fragmento de conteúdo integrado usando o fluxo de trabalho Fazer logon, mas ainda não conseguir acessar o repositório de entrega, verifique se os cookies do navegador foram limpos.

Caso contrário, você poderá ver o erro `invalid_credentials All session cookies are empty` no console.
