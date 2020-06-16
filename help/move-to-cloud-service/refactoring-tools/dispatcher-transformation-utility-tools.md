---
title: AEM Dispatcher Converter Tool
description: AEM Dispatcher Converter Tool
translation-type: tm+mt
source-git-commit: 66cf4fc7b5a336968dd3f8757cc56a11d6e4843e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---


# AEM Dispatcher Converter {#introduction}

O Adobe Experience Manager Dispatcher Converter converte as configurações existentes do AMS Dispatcher para o AEM como configurações do Cloud Service Dispatcher.

## Introdução ao Dispatcher {#introduction-dispatcher}

O Dispatcher é a ferramenta de balanceamento de carga e/ou cache do Adobe Experience Manager. Usar o Dispatcher do AEM também ajuda a proteger seu servidor AEM contra ataques. Portanto, você pode aumentar a segurança da sua instância do AEM usando o Dispatcher em conjunto com um servidor da Web de classe empresarial.

>[!NOTE]
>The most common use of Dispatcher is to cache responses from an **AEM publish instance**, to increase the responsiveness and security of your externally facing published website.

Consulte Visão geral [da](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) Dispatcher para saber como o dispatcher executa o cache, retorna documentos e executa o Balanceamento de carga.

### Configuração e teste do Apache e Dispatcher {#dispatcher-configurations-cloud}

Você deve aprender como estruturar o AEM como um Cloud Service Apache e configurações do Dispatcher, bem como como como validá-lo e executá-lo localmente antes de implantá-lo em ambientes do Cloud.

Consulte a [Dispatcher na Cloud](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) para obter mais informações.

## AEM Dispatcher Converter {#aem-dispatcher-converter}

O AEM Dispatcher Converter é um utilitário para converter as configurações existentes do AMS Dispatcher para o AEM como configurações Cloud Service Dispatcher. Este utilitário é para instâncias do AMS.

O conversor implementado é o **AEMDispatcherConfigConverter** que segue as diretrizes de transformação.

Consulte [Converter um AMS em um Adobe Experience Manager como uma Configuração](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) Dispatcher Cloud Service para converter um AMS em um Adobe Experience Manager como uma configuração Dispatcher Cloud Service.

## Uso do AEM Dispatcher Converter {#using-dispatcher-converter}

A seção a seguir descreve os recursos e as informações necessárias para usar a ferramenta AEM Dispatcher Converter.

Consulte Recurso **[Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**para saber mais sobre o uso, as limitações e a solução de problemas desta ferramenta.

>[!IMPORTANT]
>O AEM Dispatcher Converter é desenvolvido usando Python 3.7.3. É recomendável ter o Python 3.5 ou superior instalado.

## Limitações         {#limitations}

O AEM Dispatcher Converter funciona na hipótese de que a estrutura da pasta de configuração do dispatcher fornecida é semelhante à descrita na configuração do dispatcher do Cloud Manager.


