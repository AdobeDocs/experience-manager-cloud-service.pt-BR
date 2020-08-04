---
title: Ferramenta Migração de fluxo de trabalho de ativos
description: 'Ferramenta Migração de fluxo de trabalho de ativos '
translation-type: tm+mt
source-git-commit: 3a438de3c460d4dc5a8b8617f0ec0eefc56f1665
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 46%

---


# Ferramenta Migração de fluxo de trabalho de ativos{#asset-workflow-migration}

A ferramenta Migração de fluxo de trabalho de ativos é usada para migrar automaticamente fluxos de trabalho de processamento de ativos originados de implantações do AEM locais ou no AMS para perfis de processamento e Configurações OSGi, para uso no AEM Assets as a Cloud Service.

## Introdução {#introduction}

Esta seção descreve os recursos e os detalhes de implementação sobre a ferramenta Migração de fluxo de trabalho de ativos.

Esse utilitário permite que os desenvolvedores do AEM migrem fluxos de trabalho de processamento de ativos do AEM existentes para o AEM as a Cloud Service.

## workflows suportados {#migration-support-for-workflows}

Os workflows têm um nível variável de suporte à migração. Veja esta [lista de workflows](https://github.com/adobe/aem-cloud-migration/blob/master/src/main/resources/workflowSteps.properties)específicos. Os workflows são classificados nas categorias a seguir, com base no suporte fornecido. O Adobe oferece suporte à migração dos workflows listados no `SUPPORTED`, `REQUIRED`ou no `OPTIONAL` categoria. As etapas de fluxo de trabalho mencionadas nas outras categorias não são suportadas.

* `SUPPORTED`: Funcionalidade suportada em [!DNL Experience Manager Assets] como um Cloud Service.
* `OPTIONAL`: Funcionalidade opcional em [!DNL Experience Manager Assets] como um Cloud Service.
* `REQUIRED`: Uma etapa necessária que é adicionada ao fluxo de trabalho.
* `UNNECESSARY`: A funcionalidade não é necessária como Cloud Service [!DNL Experience Manager Assets] .
* `NUI_OOTB`: Funcionalidade fornecida pelo [Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `DMS7_OOTB`: Funcionalidade fornecida pelos [!DNL Dynamic Media] conectores padrão.
* `NUI_MIGRATED`: Migrado para um perfil [de processamento do Asset Compute Service](/help/assets/asset-microservices-configure-and-use.md).
* `UNSUPPORTED`: Atualmente não é suportado em [!DNL Experience Manager Assets] como um Cloud Service.

## Instalação da ferramenta Migração de fluxo de trabalho de ativos{#installing-tool}

Consulte **[Recurso do Git: AEM Assets as a Cloud Service - Migração de fluxos de trabalho](https://github.com/adobe/aem-cloud-migration)**para saber mais sobre como instalar e desenvolver o código a partir da fonte.
