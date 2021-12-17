---
title: Ferramenta de conversão do Dispatcher do AEM
description: Ferramenta de conversão do Dispatcher do AEM
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 48%

---

# Conversor do Dispatcher do AEM {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="Conversor do Dispatcher do AEM"
>abstract="O Conversor do Dispatcher do Adobe Experience Manager converte AEM configurações existentes do Dispatcher em AEM configurações as a Cloud Service do Dispatcher."

O Conversor do Dispatcher do Adobe Experience Manager converte AEM configurações existentes do Dispatcher em AEM configurações as a Cloud Service do Dispatcher.

## Introdução ao Dispatcher {#introduction-dispatcher}

O Dispatcher é a ferramenta de balanceamento de carga e/ou cache do Adobe Experience Manager. Usar o Dispatcher do AEM também ajuda a proteger seu servidor AEM contra ataques. Portanto, você pode aumentar a segurança da sua instância do AEM usando o Dispatcher em conjunto com um servidor da Web de classe empresarial.

>[!NOTE]
>O uso mais comum do Dispatcher é armazenar em cache as respostas de uma **instância de publicação do AEM**, para aumentar a capacidade de resposta e a segurança de seu site publicado voltado para o exterior.

Consulte [Visão geral do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) para saber como o dispatcher executa o cache, retorna documentos e realiza o Balanceamento de carga.

### Testes e configuração do Apache e Dispatcher {#dispatcher-configurations-cloud}

Você deve aprender a estruturar as configurações do Apache e Dispatcher do AEM as a Cloud Service e também a validá-lo e executá-lo localmente antes de implantá-lo em ambientes de Nuvem.

Consulte [Dispatcher na nuvem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) para obter mais informações.

## Conversor do Dispatcher do AEM {#aem-dispatcher-converter}

AEM Dispatcher Converter fornece a capacidade de refatorar configurações existentes no local ou do Adobe Managed Services Dispatcher para AEM configuração as a Cloud Service compatível do Dispatcher.

## Uso do Conversor do Dispatcher do AEM {#using-dispatcher-converter}

* Via Adobe I/O CLI : Recomenda-se usar o Conversor do Dispatcher do AEM via `aio-cli-plugin-aem-cloud-service-migration` (AEM plug-in de refatoração de código as a Cloud Service para o Adobe I/O CLI).

   Consulte **[Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para saber como instalar e usar o plug-in.

* Como um utilitário independente : A ferramenta Conversor do Dispatcher do AEM também pode ser executada como um utilitário independente.

   Consulte **[Recurso Git: Conversor do Dispatcher do AEM Cloud Service](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** para saber mais sobre o uso e a solução de problemas dessa ferramenta.

>[!IMPORTANT]
>AEM Dispatcher Converter é desenvolvido usando NodeJS. Recomenda-se ter o NodeJS 10.0+ instalado.
