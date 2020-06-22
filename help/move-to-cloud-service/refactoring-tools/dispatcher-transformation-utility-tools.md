---
title: Ferramenta AEM Dispatcher ConverterConversor do Dispatcher do AEM
description: Ferramenta AEM Dispatcher ConverterConversor do Dispatcher do AEM
translation-type: tm+mt
source-git-commit: 66cf4fc7b5a336968dd3f8757cc56a11d6e4843e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 94%

---


# AEM Dispatcher ConverterConversor do Dispatcher do AEM {#introduction}

O Conversor do Dispatcher do Adobe Experience Manager Dispatcher Converter converte as configurações existentes do AMS Dispatcher para configurações de Dispatcher do AEM as a Cloud Service.

## Introdução ao Dispatcher {#introduction-dispatcher}

O Dispatcher é a ferramenta de balanceamento de carga e/ou cache do Adobe Experience Manager. Usar o Dispatcher do AEM também ajuda a proteger seu servidor AEM contra ataques. Portanto, você pode aumentar a segurança da sua instância do AEM usando o Dispatcher em conjunto com um servidor da Web de classe empresarial.

>[!NOTE]
>O uso mais comum do Dispatcher é armazenar em cache as respostas de uma **instância de publicação do AEM**, para aumentar a capacidade de resposta e a segurança de seu site publicado voltado para o exterior.

Consulte [Visão geral do Dispatcher](https://docs.adobe.com/content/help/pt-BR/experience-manager-dispatcher/using/dispatcher.translate.html) para saber como o dispatcher executa o cache, retorna documentos e realiza o Balanceamento de carga.

### Testes e configuração do Apache e Dispatcher {#dispatcher-configurations-cloud}

Você deve aprender a estruturar as configurações do Apache e Dispatcher do AEM as a Cloud Service e também a validá-lo e executá-lo localmente antes de implantá-lo em ambientes de Nuvem.

Consulte [Dispatcher na nuvem](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) para obter mais informações.

## AEM Dispatcher Converter Conversor do Dispatcher do AEM{#aem-dispatcher-converter}

O Conversor do Dispatcher do AEM é um utilitário para converter configurações existentes do Dispatcher do AMS em configurações de Dispatcher do AEM as a Cloud Service. Esse utilitário é para instâncias do AMS.

O conversor implementado é o **AEMDispatcherConfigConverter** que segue as diretrizes de transformação.

Consulte [Converter um AMS em uma configuração de Dispatcher do Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) para converter um AMS em uma configuração de Dispatcher do Adobe Experience Manager as a Cloud Service.

## Uso do Conversor do Dispatcher do AEM{#using-dispatcher-converter}

A seção a seguir descreve os recursos e as informações necessárias para usar a ferramenta Conversor do Dispatcher do AEM

Consulte **[Recurso do Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**para saber mais sobre o uso, as limitações e a solução de problemas dessa ferramenta.

>[!IMPORTANT]
>O Conversor do Dispatcher do AEM é desenvolvido usando o Python 3.7.3. É recomendável ter o Python 3.5 ou superior instalado.

## Limitações          {#limitations}

O Conversor do Dispatcher do AEM funciona na hipótese de que a estrutura da pasta de configuração do Dispatcher fornecida é semelhante à descrita na configuração do Dispatcher do Cloud Manager.


