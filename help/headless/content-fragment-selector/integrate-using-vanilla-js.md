---
title: Integrar seletor de fragmento de conteúdo usando o Vanilla JS
description: Integrar o seletor de Fragmento do conteúdo a vários aplicativos da Adobe, que não sejam da Adobe e de terceiros.
role: Admin, User, Developer
source-git-commit: 592e443928f2c9c18ac281027026132b1c877ce3
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---

# Integrar seletor de fragmento de conteúdo usando o Vanilla JS {#integrate-content-fragment-selector-using-vanilla-js}

É possível integrar qualquer aplicativo do Adobe ou que não seja da Adobe ao repositório do Adobe Experience Manager (AEM) as a Cloud e selecionar Fragmentos de conteúdo nesse aplicativo.

A integração é feita importando o pacote do Seletor de fragmento de conteúdo e se conectando ao AEM as a Cloud Service por meio da biblioteca JavaScript do Vanilla. Edite um `index.html` ou qualquer arquivo apropriado em seu aplicativo para:

* Definir os detalhes de autenticação
* Acessar o repositório do AEM as a Cloud Service
* Configurar as propriedades de exibição do Seletor de fragmento de conteúdo

É possível executar a autenticação sem definir algumas das propriedades do IMS, se você:

* estão integrando um aplicativo do Adobe no [Unified Shell](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell)
* já tem um token IMS gerado para autenticação
