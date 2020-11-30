---
title: Ferramenta de conversão do Dispatcher do AEM
description: Ferramenta de conversão do Dispatcher do AEM
translation-type: tm+mt
source-git-commit: 50d26dbec8281afec07ca56595b4b2a7b915eca9
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 53%

---


# Conversor do Dispatcher do AEM {#introduction}

O Adobe Experience Manager Dispatcher Converter converte as configurações existentes AEM Dispatcher em AEM como configurações Cloud Service Dispatcher.

## Introdução ao Dispatcher {#introduction-dispatcher}

O Dispatcher é a ferramenta de balanceamento de carga e/ou cache do Adobe Experience Manager. Usar o Dispatcher do AEM também ajuda a proteger seu servidor AEM contra ataques. Portanto, você pode aumentar a segurança da sua instância do AEM usando o Dispatcher em conjunto com um servidor da Web de classe empresarial.

>[!NOTE]
>O uso mais comum do Dispatcher é armazenar em cache as respostas de uma **instância de publicação do AEM**, para aumentar a capacidade de resposta e a segurança de seu site publicado voltado para o exterior.

Consulte [Visão geral do Dispatcher](https://docs.adobe.com/content/help/pt-BR/experience-manager-dispatcher/using/dispatcher.translate.html) para saber como o dispatcher executa o cache, retorna documentos e realiza o Balanceamento de carga.

### Testes e configuração do Apache e Dispatcher {#dispatcher-configurations-cloud}

Você deve aprender a estruturar as configurações do Apache e Dispatcher do AEM as a Cloud Service e também a validá-lo e executá-lo localmente antes de implantá-lo em ambientes de Nuvem.

Consulte [Dispatcher na nuvem](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) para obter mais informações.

## AEM Dispatcher Converter Conversor do Dispatcher do AEM{#aem-dispatcher-converter}

AEM o Dispatcher Converter oferece a capacidade de refatorar configurações existentes no local ou do Adobe Managed Services Dispatcher para AEM como uma configuração do Dispatcher compatível com Cloud Service.

## Uso do Conversor do Dispatcher do AEM{#using-dispatcher-converter}

* Por meio do Adobe I/O CLI: É recomendável usar o AEM Dispatcher Converter via `aio-cli-plugin-aem-cloud-service-migration` (AEM como um plug-in de refatoração de código Cloud Service para o Adobe I/O CLI).

   Consulte Recurso **[Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente: A ferramenta AEM Dispatcher Converter também pode ser executada como um utilitário independente.

   Refer to **[Git Resource: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** to learn about the usage and troubleshooting for this tool.

>[!IMPORTANT]
>AEM Dispatcher Converter é desenvolvido usando NodeJS. É recomendável ter o NodeJS 10.0+ instalado.

