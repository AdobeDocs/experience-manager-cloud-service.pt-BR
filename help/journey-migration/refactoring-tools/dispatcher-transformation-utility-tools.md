---
title: Ferramenta de conversão do Dispatcher do AEM
description: Saiba como converter configurações existentes no AEM Dispatcher em configurações no AEM as a Cloud Service Dispatcher.
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 28%

---

# Conversor do Dispatcher do AEM {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="Conversor do Dispatcher do AEM"
>abstract="O Conversor do Adobe Experience Manager Dispatcher converte as configurações existentes do AEM Dispatcher para configurações do AEM as a Cloud Service Dispatcher."

O Conversor do Adobe Experience Manager Dispatcher converte as configurações existentes do AEM Dispatcher para configurações do AEM as a Cloud Service Dispatcher.

## Introdução ao Dispatcher {#introduction-dispatcher}

O Dispatcher é a ferramenta de armazenamento em cache, balanceamento de carga ou ambos do Adobe Experience Manager. Usar o Dispatcher do AEM também ajuda a proteger seu servidor AEM contra ataques. Portanto, você pode aumentar a segurança da sua instância do AEM usando o Dispatcher com um servidor da Web de classe empresarial.

>[!NOTE]
>O uso mais comum do Dispatcher é armazenar em cache as respostas de uma **instância de publicação do AEM**, para aumentar a capacidade de resposta e a segurança de seu site publicado voltado para o exterior.

Consulte [Visão geral do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) para saber como o Dispatcher executa o cache, retorna documentos e realiza o Balanceamento de Carga.

### Testes e configuração do Apache e Dispatcher {#dispatcher-configurations-cloud}

Saiba como estruturar as configurações do AEM as a Cloud Service Apache e do Dispatcher e como validá-las e executá-las localmente antes de implantá-las em ambientes de nuvem.

Consulte [Dispatcher na nuvem](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=pt-BR) para obter mais informações.

## Conversor do Dispatcher do AEM {#aem-dispatcher-converter}

O Conversor de Dispatcher para AEM fornece a capacidade de refatorar configurações existentes no local ou no Adobe Managed Services Dispatcher para configurações de Dispatcher compatíveis com o AEM as a Cloud Service.

## Uso do Conversor de Dispatcher para AEM {#using-dispatcher-converter}

* Por meio da CLI do Adobe Developer : a Adobe recomenda o uso do conversor de Dispatcher do AEM por meio do `aio-cli-plugin-aem-cloud-service-migration` (plug-in de refatoração de código do AEM as a Cloud Service para a CLI do Adobe Developer).

  Consulte **[Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** para que você possa aprender a instalar e usar o plug-in.

* Como um utilitário independente : a ferramenta Conversor de Dispatcher do AEM também pode ser executada como um utilitário independente.

  Consulte **[Recurso do Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** para que você possa saber mais sobre o uso e a solução de problemas dessa ferramenta.

>[!IMPORTANT]
>O AEM Dispatcher Converter é desenvolvido usando o NodeJS. O Adobe recomenda que você tenha o NodeJS 10.0+ instalado.
