---
title: Alterações notáveis nos ativos Adobe Experience Manager como um serviço na nuvem
description: Alterações notáveis nos ativos Adobe Experience Manager no serviço da AEM Cloud em comparação ao Experience Manager 6.5
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

O Adobe Experience Manager como um serviço em nuvem oferece muitos recursos e possibilidades novos para gerenciar seus projetos do AEM. No entanto, há diversas diferenças entre os ativos do Experience Manager no local ou no Adobe Managed Service em comparação ao Experience Manager como um serviço em nuvem. Este documento destaca as diferenças importantes.

>[!NOTE]
>
>Este documento destaca as alterações notáveis que são específicas dos Ativos do Experience Manager como um Serviço em nuvem. Consulte as [alterações genéricas do Experience Manager como um serviço](/help/release-notes/aem-cloud-changes.md)em nuvem.

As principais diferenças em comparação ao Experience Manager 6.5 estão nas seguintes áreas:

* [Inclusão de ativos](#asset-ingestion)
* [Remoção da interface do usuário clássica](#classic-ui)

## Inclusão de ativos {#asset-ingestion}

O upload de ativos foi otimizado para ser mais eficiente, permitindo um melhor dimensionamento da inclusão de ativos e uploads mais rápidos. Os recursos do produto (interfaces de usuário da Web, clientes de desktop) foram atualizados. No entanto, isso pode afetar alguns códigos personalizados existentes.

* O Experience Manager usa o princípio de acesso binário direto para fazer upload e download e usar microserviços de ativos para processamento de ativos. Consulte [visão geral da ingestão de ativos](/help/assets/asset-microservices-overview.md)
   * Carregamento de ativos [com acesso binário direto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)
   * Para obter detalhes técnicos, consulte o protocolo de upload binário [direto e as APIs](/help/assets/developer-reference-material-apis.md#overview-binary-upload)
* O fluxo de trabalho padrão **[!UICONTROL DAM Asset Update]** nas versões anteriores do AEM não está mais disponível. Em vez disso, os microserviços de ativos fornecem um serviço dimensionável e prontamente disponível que abrange a maioria do processamento de ativos padrão (execuções, extração de metadados, extração de texto para indexação)
   * Consulte [configurar e usar microserviços de ativos](/help/assets/asset-microservices-configure-and-use.md)
   * Para ter etapas personalizadas de fluxo de trabalho no processamento, é possível usar workflows [de](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) pós-processamento
* Os ativos que entram pelo Gerenciador de pacotes exigem reprocessamento manual usando a ação **[!UICONTROL Reprocessar ativos]** na interface Ativos.

As representações padrão geradas com os microserviços de ativos são armazenadas de forma compatível com versões anteriores nos nós do repositório de ativos (mesmas convenções de nomenclatura).

## Desenvolver e testar microserviços de ativos {#developing-testing-asset-microservices}

Os microserviços de ativos são um serviço em nuvem nativo que é automaticamente provisionado e conectado ao Experience Manager em programas de clientes e ambientes gerenciados no Cloud Manager. Os desenvolvedores que trabalham para estender o Experience Manager ou fazer personalização podem usar o conteúdo existente (ou ativos com execuções geradas em um ambiente em nuvem) para testar e validar seu código usando, exibindo e baixando ativos.

Para fazer uma validação completa do código e do processo, incluindo a ingestão e o processamento de ativos, implante as alterações de código em um ambiente de desenvolvimento de nuvem usando o pipeline e o teste com a execução completa do processamento de microserviços de ativos.

## Remoção da interface do usuário clássica {#classic-ui}

A interface clássica não está mais disponível no Experience Manager como um serviço da nuvem.
