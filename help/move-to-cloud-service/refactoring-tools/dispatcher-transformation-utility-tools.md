---
title: Ferramenta de conversão do Dispatcher do AEM
description: Ferramenta de conversão do Dispatcher do AEM
exl-id: 97eb4f3f-dc03-461a-8d7e-164065bd1e4c
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 51%

---

# Conversor do Dispatcher do AEM {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="Conversor do Dispatcher do AEM"
>abstract="O Conversor do Dispatcher do Adobe Experience Manager converte configurações existentes AEM Dispatcher em AEM como configurações do Dispatcher do Cloud Service."

O Conversor do Dispatcher do Adobe Experience Manager converte configurações existentes AEM Dispatcher em AEM como configurações do Dispatcher do Cloud Service.

## Introdução ao Dispatcher {#introduction-dispatcher}

O Dispatcher é a ferramenta de balanceamento de carga e/ou cache do Adobe Experience Manager. Usar o Dispatcher do AEM também ajuda a proteger seu servidor AEM contra ataques. Portanto, você pode aumentar a segurança da sua instância do AEM usando o Dispatcher em conjunto com um servidor da Web de classe empresarial.

>[!NOTE]
>O uso mais comum do Dispatcher é armazenar em cache as respostas de uma **instância de publicação do AEM**, para aumentar a capacidade de resposta e a segurança de seu site publicado voltado para o exterior.

Consulte [Visão geral do Dispatcher](https://docs.adobe.com/content/help/pt-BR/experience-manager-dispatcher/using/dispatcher.translate.html) para saber como o dispatcher executa o cache, retorna documentos e realiza o Balanceamento de carga.

### Testes e configuração do Apache e Dispatcher {#dispatcher-configurations-cloud}

Você deve aprender a estruturar as configurações do Apache e Dispatcher do AEM as a Cloud Service e também a validá-lo e executá-lo localmente antes de implantá-lo em ambientes de Nuvem.

Consulte [Dispatcher na nuvem](https://docs.adobe.com/content/help/pt-BR/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) para obter mais informações.

## AEM Dispatcher Converter Conversor do Dispatcher do AEM{#aem-dispatcher-converter}

AEM O Dispatcher Converter fornece a capacidade de refatorar configurações existentes no local ou do Adobe Managed Services Dispatcher para AEM como uma configuração do Dispatcher compatível com o Cloud Service.

## Uso do Conversor do Dispatcher do AEM{#using-dispatcher-converter}

* Via Adobe I/O CLI : É recomendável usar o Conversor do Dispatcher AEM via `aio-cli-plugin-aem-cloud-service-migration` (AEM como um plug-in de refatoração de código Cloud Service para a CLI do Adobe I/O).

   Consulte **[Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente : A ferramenta Conversor do Dispatcher do AEM também pode ser executada como um utilitário independente.

   Consulte **[Recurso Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** para saber mais sobre o uso e a solução de problemas dessa ferramenta.

>[!IMPORTANT]
>AEM Dispatcher Converter é desenvolvido usando NodeJS. Recomenda-se ter o NodeJS 10.0+ instalado.
