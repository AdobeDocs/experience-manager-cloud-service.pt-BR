---
title: Seletor de ativos para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Integrar o seletor de ativos a vários aplicativos de Adobe, não Adobe e de terceiros.
role: Admin, User
source-git-commit: fb1350c91468f9c448e34b66dc938fa3b5a3e9a9
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 47%

---


# Integrar o Seletor de ativos usando o Vanilla JS {#integration-using-vanilla-js}

É possível integrar qualquer aplicativo [!DNL Adobe] ou não-Adobe ao repositório [!DNL Experience Manager Assets] e selecionar ativos no aplicativo. Consulte [Integração do Seletor de ativos com vários aplicativos](#integrate-asset-selector.md).

A integração é feita importando o pacote do Seletor de ativos e conectando ao Assets as a Cloud Service usando a biblioteca JavaScript Vanilla. Edite um `index.html` ou qualquer arquivo apropriado em seu aplicativo para:

* Definir os detalhes de autenticação
* Acessar o repositório do Assets as a Cloud Service
* Configurar as propriedades de exibição do Seletor de ativos

É possível executar a autenticação sem definir algumas das propriedades do IMS, se:

* Está integrando um aplicativo [!DNL Adobe] no [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=pt-BR).
* Você já tem um token IMS gerado para autenticação.

## Integrar o Seletor de ativos a vários aplicativos {#asset-selector-integration-with-apps}

É possível integrar o Seletor de ativos a vários aplicativos, como:

* [Integrar o Seletor de ativos a um aplicativo do  [!DNL Adobe] ](#integrate-asset-selector.md)
* [Integrar o Seletor de ativos a um aplicativo não-Adobe](#integrate-asset-selector-non-adobe.md)
* [Integração do Dynamic Media com recursos OpenAPI](#integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [Personalização do Seletor de ativos](/help/assets/asset-selector-customization.md)
>* [Propriedades do Seletor de ativos](/help/assets/asset-selector-properties.md)
>* [Integrar APIs abertas de mídia dinâmica do Seletor de ativos](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)

