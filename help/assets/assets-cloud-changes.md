---
title: Alterações notáveis nos ativos Adobe Experience Manager como um serviço na nuvem
description: Alterações notáveis nos ativos Adobe Experience Manager no serviço da AEM Cloud em comparação ao Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 37ff6912837ba78c90526e8f8322b9002e9a4304
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 4%

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

O Adobe Experience Manager como um serviço em nuvem oferece muitos recursos e possibilidades novos para gerenciar seus projetos do AEM. No entanto, há muitas diferenças entre os Ativos do Experience Manager no local ou no Adobe Managed Service em comparação ao Experience Manager como um Serviço em nuvem. Este documento destaca as diferenças importantes para os recursos do Assets. Para outras alterações, consulte as [alterações genéricas no Experience Manager como um serviço](/help/release-notes/aem-cloud-changes.md)em nuvem.

As principais diferenças em comparação ao Experience Manager 6.5 estão nas seguintes áreas:

* [Inclusão e upload](#asset-ingestion)de ativos.
* [Microserviços de ativos para processamento](#asset-microservices)em nuvem.
* [Remoção da interface do usuário clássica](#classic-ui).

## Inclusão e upload de ativos {#asset-ingestion}

O upload de ativos foi otimizado para proporcionar eficiência, permitindo um melhor dimensionamento da inclusão de ativos e uploads mais rápidos. Os recursos do produto (interfaces de usuário da Web, clientes de desktop) foram atualizados. No entanto, isso pode afetar algumas personalizações existentes.

* O Experience Manager usa o princípio de acesso binário direto para fazer upload e download e usar microserviços de ativos para processamento de ativos. Consulte a [visão geral da ingestão](/help/assets/asset-microservices-overview.md)de ativos.
   * Carregamento de ativos [com acesso](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)binário direto.
   * Para obter detalhes técnicos, consulte o protocolo de carregamento binário [direto e as APIs](/help/assets/developer-reference-material-apis.md#overview-binary-upload).
* O fluxo de trabalho padrão **[!UICONTROL DAM Asset Update]** nas versões anteriores do AEM não está mais disponível. Em vez disso, os microserviços de ativos fornecem um serviço dimensionável e prontamente disponível que abrange a maioria do processamento de ativos padrão (execuções, extração de metadados, extração de texto para indexação).
   * Consulte [configurar e usar microserviços de ativos](/help/assets/asset-microservices-configure-and-use.md)
   * Para ter etapas personalizadas de fluxo de trabalho no processamento, é possível usar workflows [de](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) pós-processamento.
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

As representações padrão geradas com os microserviços de ativos são armazenadas de forma compatível com versões anteriores nos nós do repositório de ativos (mesmas convenções de nomenclatura).

## Desenvolver e testar microserviços de ativos {#asset-microservices}

Os microserviços de ativos fornecem um processamento escalonável e resiliente de ativos usando serviços em nuvem. A Adobe gerencia os serviços em nuvem para obter o melhor tratamento de diferentes tipos de ativos e opções de processamento. Os microserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como o ImageMagick) e a simplificar configurações, além de fornecer uma funcionalidade pronta para uso para tipos de arquivos comuns. Agora você pode processar uma [ampla variedade de tipos](/help/assets/file-format-support.md) de arquivos que abrangem mais formatos prontos para uso do que o que é possível com as versões anteriores do Experience Manager. Por exemplo, a extração em miniatura dos formatos PSD e PSB agora é possível e exigia soluções de terceiros como o ImageMagick. Não é possível usar as configurações complexas do ImageMagick para a configuração de Perfis [!UICONTROL de] processamento. Além disso, use [!DNL Dynamic Media] a transcodificação FFmpeg de vídeos.

Os microserviços de ativos são um serviço nativo da nuvem que é automaticamente provisionado e conectado ao Experience Manager em programas de clientes e ambientes gerenciados no Cloud Manager. Para estender ou personalizar o Experience Manager, os desenvolvedores podem usar o conteúdo ou os ativos existentes com execuções geradas em um ambiente em nuvem, para testar e validar seu código usando, exibindo e baixando ativos.

Para fazer uma validação completa do código e do processo, incluindo a ingestão e o processamento de ativos, implante as alterações de código em um ambiente de desenvolvimento de nuvem usando [o pipeline](/help/implementing/cloud-manager/configure-pipeline.md) e o teste com a execução completa do processamento de microserviços de ativos.

## Remoção da interface do usuário clássica {#classic-ui}

A interface clássica não está mais disponível no Experience Manager como um serviço da nuvem. A interface padrão é a interface habilitada para toque.
