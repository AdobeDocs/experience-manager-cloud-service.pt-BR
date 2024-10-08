---
title: Seletor de ativos para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Integrar o seletor de ativos a vários aplicativos de Adobe, não Adobe e de terceiros.
role: Admin, User
exl-id: 55848de0-aff2-42a0-b959-c771235d9425
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# Integração com um aplicativo não-Adobe {#integrate-asset-selector-non-adobe-app}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

O Seletor de ativos permite a integração usando vários aplicativos de terceiros ou que não sejam de Adobe para que eles trabalhem em conjunto de maneira contínua.

## Pré-requisitos {#prereqs-non-adobe-app}

Use os seguintes pré-requisitos se estiver integrando o Seletor de ativos a um aplicativo não-Adobe:

* [Métodos de comunicação](/help/assets/overview-asset-selector.md#prereqs)
* imsClientId
* imsScope
* redirectUrl
* imsOrg
* apikey

O Seletor de ativos oferece suporte à autenticação para o repositório [!DNL Experience Manager Assets] usando propriedades do Sistema Identity Management (IMS) como `imsScope` ou `imsClientID` quando você o integra com um aplicativo que não seja Adobe.

## Configurar o Seletor de ativos para um aplicativo não-Adobe {#configure-non-adobe-app}

Para configurar o Seletor de ativos para um aplicativo não-Adobe, primeiro registre um tíquete de suporte para provisionamento, seguido das etapas de integração.

### Registro de um tíquete de suporte {#log-a-support-ticket}

Etapas para registrar um tíquete de suporte pela Admin Console:

1. Adicionar **Seletor de ativos com AEM Assets** no título do tíquete.

1. Na descrição, forneça os seguintes detalhes:

   * [!DNL Experience Manager Assets] como uma URL [!DNL Cloud Service] (ID do Programa e ID do Ambiente).
   * Nomes de domínio em que o aplicativo Web não-Adobe está hospedado.

## Etapas de integração {#non-adobe-app-integration-steps}

Use este exemplo de arquivo `index.html` para autenticação ao integrar o Seletor de ativos a um aplicativo não-Adobe.

Acesse o pacote do Seletor de ativos usando a Marca `Script`, conforme mostrado na *linha 9* para a *linha 11* do arquivo de exemplo `index.html`.

A *Linha 14* a *linha 38* do exemplo descreve as propriedades do fluxo IMS, como `imsClientId`, `imsScope` e `redirectURL`. A função requer a definição de pelo menos uma das propriedades `imsClientId` e `imsScope`. Se você não definir um valor para `redirectURL`, a URL de redirecionamento registrada para a ID do cliente será usada.

Como você não tem um `imsToken` gerado, use as funções `registerAssetsSelectorsAuthService` e `renderAssetSelectorWithAuthFlow`, conforme mostrado na linha 40 para a linha 50 do arquivo de exemplo `index.html`. Use a função `registerAssetsSelectorsAuthService` antes de `renderAssetSelectorWithAuthFlow` para registrar `imsToken` com o Seletor de ativos. A [!DNL Adobe] recomenda chamar `registerAssetsSelectorsAuthService` ao instanciar o componente.

Defina a autenticação e outras propriedades relacionadas ao as a Cloud Service do Assets na seção `const props`, conforme mostrado na *linha 54* a *linha 60* do arquivo de exemplo `index.html`.

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
        src="https://experience.adobe.com/solutions/CQ-assets-selectors/static-assets/resources/assets-selectors.js"></script>
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

## Não foi possível acessar o repositório de entrega {#unable-to-access-delivery-repository}

>[!TIP]
>
>Se você tiver integrado o Seletor de ativos usando o fluxo de trabalho Inscrever-se, mas ainda não conseguir acessar o repositório de entrega, verifique se os cookies do navegador foram limpos. Caso contrário, você acaba recebendo o erro `invalid_credentials All session cookies are empty` no console.

>[!MORELIKETHIS]
>
>* [Integrar o Seletor de ativos a vários aplicativos](/help/assets/integrate-asset-selector.md)
>* [Propriedades do Seletor de ativos](/help/assets/asset-selector-properties.md)
>* [Integrar o Seletor de ativos ao Dynamic Media com recursos OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
>* [Personalizações do Seletor de ativos](/help/assets/asset-selector-customization.md)
