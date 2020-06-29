---
title: Alterações notáveis nos ativos Adobe Experience Manager como um Cloud Service
description: Alterações notáveis nos ativos Adobe Experience Manager no Cloud Service do AEM em comparação ao Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 10%

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

O Adobe Experience Manager como Cloud Service oferece muitos novos recursos e possibilidades para gerenciar seus projetos do AEM. No entanto, há muitas diferenças entre os ativos Experience Manager no local ou no serviço gerenciado da Adobe em comparação ao Experience Manager como Cloud Service. Este documento destaca as diferenças importantes para os recursos do Assets.

As principais diferenças em relação ao Experience Manager 6.5 são as seguintes:

* [Inclusão e upload](#asset-ingestion)de ativos.
* [Microserviços de ativos para processamento](#asset-microservices)em nuvem.
* [Remoção da interface do usuário clássica](#classic-ui).

>[!NOTE]
>Este documento destaca as mudanças notáveis nos AEM Assets. Para obter as alterações gerais no AEM como Cloud Service e em outros módulos, consulte:
>
>* [Uma introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* Uma [visão geral do AEM como um Cloud Service - Novidades e diferentes](/help/overview/what-is-new-and-different.md)
>* A [Arquitetura](/help/core-concepts/architecture.md) do Adobe Experience Manager as a Cloud Service
>* [Alterações notáveis no AEM como Cloud Service (Notas de versão)](/help/release-notes/aem-cloud-changes.md)
>* [Alterações importantes no Sites as a AEM Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutoriais do Adobe Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/br/experience-manager-learn/cloud-service/overview.html)


## Inclusão e upload de ativos {#asset-ingestion}

O upload de ativos foi otimizado para proporcionar eficiência, permitindo um melhor dimensionamento da inclusão de ativos e uploads mais rápidos. Os recursos do produto (interfaces de usuário da Web, clientes de desktop) foram atualizados. No entanto, isso pode afetar algumas personalizações existentes.

* O Experience Manager usa o princípio de acesso binário direto para fazer upload e download e para fazer o processamento de ativos em microserviços. Consulte a [visão geral da ingestão](/help/assets/asset-microservices-overview.md)de ativos.
   * Carregamento de ativos [com acesso](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)binário direto.
   * Para obter detalhes técnicos, consulte o protocolo de carregamento binário [direto e as APIs](/help/assets/developer-reference-material-apis.md#overview-binary-upload).
* O fluxo de trabalho padrão **[!UICONTROL DAM Asset Update]** nas versões anteriores do AEM não está mais disponível. Em vez disso, os microserviços de ativos fornecem um serviço dimensionável e prontamente disponível que abrange a maioria do processamento de ativos padrão (execuções, extração de metadados, extração de texto para indexação).
   * Consulte [configurar e usar microserviços de ativos](/help/assets/asset-microservices-configure-and-use.md)
   * Para ter etapas personalizadas de fluxo de trabalho no processamento, é possível usar workflows [de](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) pós-processamento.
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

As representações padrão geradas com os microserviços de ativos são armazenadas de forma compatível com versões anteriores nos nós do repositório de ativos (mesmas convenções de nomenclatura).

## Desenvolver e testar microserviços de ativos {#asset-microservices}

Os microserviços de ativos fornecem um processamento escalonável e resiliente de ativos usando serviços em nuvem. A Adobe gerencia os serviços em nuvem para obter o melhor tratamento de diferentes tipos de ativos e opções de processamento. Os microserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como o ImageMagick) e a simplificar configurações, além de fornecer uma funcionalidade pronta para uso para tipos de arquivos comuns. Agora é possível processar uma [ampla variedade de tipos](/help/assets/file-format-support.md) de arquivos que abrangem mais formatos prontos para uso do que o que é possível com as versões anteriores do Experience Manager. Por exemplo, a extração em miniatura dos formatos PSD e PSB agora é possível e exigia soluções de terceiros como o ImageMagick. Não é possível usar as configurações complexas do ImageMagick para a configuração de Perfis [!UICONTROL de] processamento. Além disso, use [!DNL Dynamic Media] a transcodificação FFmpeg de vídeos.

Os microserviços de ativos são um serviço nativo da nuvem que é automaticamente provisionado e conectado ao Experience Manager nos programas e ambientes do cliente gerenciados no Cloud Manager. Para estender ou personalizar o Experience Manager, os desenvolvedores podem usar o conteúdo ou os ativos existentes com execuções geradas em um ambiente em nuvem, para testar e validar seu código usando, exibindo e baixando ativos.

Para fazer uma validação completa do código e do processo, incluindo a ingestão e o processamento de ativos, implante as alterações de código em um ambiente de desenvolvimento de nuvem usando [o pipeline](/help/implementing/cloud-manager/configure-pipeline.md) e o teste com a execução completa do processamento de microserviços de ativos.

## Remoção da interface do usuário clássica {#classic-ui}

A interface clássica não está mais disponível no Experience Manager como Cloud Service. A interface padrão é a interface habilitada para toque.
