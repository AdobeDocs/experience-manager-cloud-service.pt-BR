---
title: Ferramenta de conversão do AEM Dispatcher
description: Ferramenta de conversão do AEM Dispatcher
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---


# Conversor do Dispatcher AEM {#introduction}

O Adobe Experience Manager Dispatcher Converter converte as configurações existentes do AMS Dispatcher para AEM como configurações do Cloud Service Dispatcher.

## Introdução ao Dispatcher {#introduction-dispatcher}

O Dispatcher é a ferramenta de balanceamento de carga e/ou cache do Adobe Experience Manager. Usar o Dispatcher do AEM também ajuda a proteger seu servidor AEM contra ataques. Portanto, você pode aumentar a segurança da sua instância do AEM usando o Dispatcher em conjunto com um servidor da Web de classe empresarial.

>[!NOTE]
>The most common use of Dispatcher is to cache responses from an **AEM publish instance**, to increase the responsiveness and security of your externally facing published website.

Consulte Visão geral [do](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) Dispatcher para saber como o dispatcher executa o cache, retorna documentos e executa o Balanceamento de carga.

### Configuração e teste do Apache e do Dispatcher {#dispatcher-configurations-cloud}

Você deve aprender como estruturar o AEM como um Apache de serviço em nuvem e configurações do Dispatcher, bem como como como validá-lo e executá-lo localmente antes de implantá-lo em ambientes em nuvem.

Consulte o [Dispatcher na Cloud](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html) para obter mais informações.

## Conversor do Dispatcher AEM {#aem-dispatcher-converter}

O AEM Dispatcher Converter é um utilitário para converter configurações existentes do AMS Dispatcher para AEM como configurações do Cloud Service Dispatcher. Este utilitário é para instâncias do AMS.

O conversor implementado é o **AEMDispatcherConfigConverter** que segue as diretrizes de transformação.

Consulte [Converter um AMS em um Adobe Experience Manager como uma Configuração](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) do Dispatcher do Serviço em Nuvem para converter um AMS em um Adobe Experience Manager como uma configuração do Dispatcher do Serviço em Nuvem.

## Uso do AEM Dispatcher Converter {#using-dispatcher-converter}

A seção a seguir descreve os recursos e as informações necessárias para usar a ferramenta Conversor do Dispatcher AEM.

Consulte Recurso **[Git: Conversor](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**do Dispatcher Service da AEM Cloud para saber mais sobre o uso, as limitações e a solução de problemas desta ferramenta.

>[!IMPORTANT]
>O AEM Dispatcher Converter é desenvolvido usando Python 3.7.3. É recomendável ter o Python 3.5 ou superior instalado.

## Limitações         {#limitations}

O AEM Dispatcher Converter funciona na hipótese de que a estrutura da pasta de configuração do dispatcher fornecida é semelhante à descrita na configuração do dispatcher do Cloud Manager.


