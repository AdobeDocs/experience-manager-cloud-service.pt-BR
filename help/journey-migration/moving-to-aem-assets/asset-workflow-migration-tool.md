---
title: Ferramenta Migração de fluxo de trabalho de ativos
description: Ferramenta Migração de fluxo de trabalho de ativos
exl-id: a95caf5e-e6b2-463f-bebd-b791104fd25c
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 72%

---

# Ferramenta Migração de fluxo de trabalho de ativos {#asset-workflow-migration}

A ferramenta Migração de fluxo de trabalho de ativos é usada para migrar automaticamente fluxos de trabalho de processamento de ativos originados de implantações do AEM locais ou no AMS para perfis de processamento e Configurações OSGi, para uso no AEM Assets as a Cloud Service.

## Introdução {#introduction}

Esta seção descreve os recursos e os detalhes de implementação sobre a ferramenta Migração de fluxo de trabalho de ativos.

Esse utilitário permite que os desenvolvedores do AEM migrem fluxos de trabalho de processamento de ativos do AEM existentes para o AEM as a Cloud Service.

## Fluxos de trabalho compatíveis {#migration-support-for-workflows}

Os fluxos de trabalho têm um nível variável de suporte à migração. Consulte esta [lista de fluxos de trabalho específicos](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties). Os fluxos de trabalho são classificados nas seguintes categorias de acordo com o suporte fornecido. A Adobe oferece suporte à migração dos fluxos de trabalho listados nas categorias `SUPPORTED`, `REQUIRED` ou `OPTIONAL`. Não há suporte para as etapas de fluxo de trabalho mencionadas nas outras categorias.

* `SUPPORTED`: funcionalidade com suporte no [!DNL Experience Manager Assets] as a Cloud Service.
* `OPTIONAL`: funcionalidade opcional no [!DNL Experience Manager Assets] as a Cloud Service.
* `REQUIRED`: uma etapa necessária adicionada ao fluxo de trabalho.
* `UNNECESSARY`: a funcionalidade não é necessária no [!DNL Experience Manager Assets] as a Cloud Service.
* `NUI_OOTB`: funcionalidade fornecida pelo [Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`: funcionalidade fornecida pelos conectores padrão do [!DNL Dynamic Media].
* `NUI_MIGRATED`: movido para um [perfil de processamento do Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `UNSUPPORTED`: no momento não há suporte no [!DNL Experience Manager Assets] as a Cloud Service.

## Usar a ferramenta Migração de fluxo de trabalho de ativos {#use-workflow-migrator}

* **[!DNL Adobe I/O]CLI**: o Adobe recomenda usar a ferramenta Migração de fluxo de trabalho de ativos via `aio-cli-plugin-aem-cloud-service-migration` ([!DNL Experience Manager] as a [!DNL Cloud Service] plug-in de refatoração de código para o [!DNL Adobe I/O] CLI). Para saber como instalar e usar o plug-in, consulte [Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction).

* **Utilitário independente**: a ferramenta Migração de fluxo de trabalho de ativos também pode ser executada como um utilitário independente. Para saber mais sobre como instalar e criar o código a partir da origem, consulte [Recurso do Git: [!DNL Experience Manager Assets] as a [!DNL Cloud Service] - migração de fluxo de trabalho](https://github.com/adobe/aem-cloud-migration).
