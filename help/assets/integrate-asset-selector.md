---
title: Integrar o Seletor de ativos usando o Vanilla JS
description: Integrar o seletor de ativos a vários aplicativos da Adobe, que não sejam da Adobe e de terceiros.
role: Admin, User
exl-id: 1c0051a3-549c-4783-9fc1-594f424a70c3
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 46%

---

# Integrar o Seletor de ativos usando o Vanilla JS {#integration-using-vanilla-js}

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

* [Integrar o Seletor de ativos a um aplicativo do  [!DNL Adobe] &#x200B;](/help/assets/integrate-asset-selector-adobe-app.md)
* [Integrar o Seletor de ativos a um aplicativo que não seja da Adobe](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [Integração do Dynamic Media com recursos OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [Personalizações do Seletor de ativos](/help/assets/asset-selector-customization.md)
>* [Propriedades do Seletor de ativos](/help/assets/asset-selector-properties.md)
>* [Integrar o Seletor de ativos ao Dynamic Media com recursos OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
