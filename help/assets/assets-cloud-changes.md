---
title: Alterações notáveis no Adobe Experience Manager Assets como um Cloud Service
description: Mudanças notáveis nos Adobe Experience Manager Assets no Cloud Service AEM em comparação ao Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 18%

---


# Alterações notáveis nos ativos Experience Manager como Cloud Service {#notable-changes}

O Adobe Experience Manager as a Cloud Service oferece muitos novos recursos e possibilidades para gerenciar projetos do AEM. No entanto, há muitas diferenças entre os ativos Experience Manager no local ou no serviço gerenciado pelo Adobe em comparação ao Experience Manager como Cloud Service. Este documento destaca as diferenças importantes para os recursos do Assets.

Estas são as principais diferenças em relação ao Experience Manager 6.5:

* [Inclusão e upload](#asset-ingestion) de ativos.
* [Microserviços de ativos para processamento](#asset-microservices) nativo na nuvem.
* [Remoção da interface do usuário clássica](#classic-ui).

>[!NOTE]
>
>Este documento destaca as mudanças notáveis no AEM Assets. Para obter as alterações gerais para AEM como Cloud Service, e outros módulos, consulte:
>
>* [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* a [Visão geral do AEM as a Cloud Service: novidades e diferenças](/help/overview/what-is-new-and-different.md)
>* A [Arquitetura](/help/core-concepts/architecture.md) do Adobe Experience Manager as a Cloud Service
>* [Alterações importantes no AEM as a Cloud Service (notas de versão)](/help/release-notes/aem-cloud-changes.md)
>* [Alterações importantes no AEM Sites as a  Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutoriais do Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


## Inclusão e carregamento de ativos {#asset-ingestion}

O upload de ativos foi otimizado para proporcionar eficiência, permitindo um melhor dimensionamento da inclusão de ativos e uploads mais rápidos. Os recursos do produto (interfaces de usuário da Web, clientes de desktop) foram atualizados. No entanto, isso pode afetar algumas personalizações existentes.

* O Experience Manager usa o princípio de acesso binário direto para fazer upload e download e para fazer o processamento de ativos em microserviços. Consulte [visão geral da ingestão de ativos](/help/assets/asset-microservices-overview.md).
   * Carregamento de ativos [com acesso binário direto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obter detalhes técnicos, consulte [protocolo de carregamento binário direto e APIs](/help/assets/developer-reference-material-apis.md#upload-binary).
* O fluxo de trabalho padrão **[!UICONTROL DAM Asset Update]** nas versões anteriores do AEM não está mais disponível. Em vez disso, os microserviços de ativos fornecem um serviço dimensionável e prontamente disponível que abrange a maioria do processamento de ativos padrão (execuções, extração de metadados, extração de texto para indexação).
   * Consulte [configurar e usar os microserviços de ativos](/help/assets/asset-microservices-configure-and-use.md)
   * Para ter etapas personalizadas de fluxo de trabalho no processamento, [workflows pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) podem ser usados.
* Os ativos que entram pelo Gerenciador de pacotes exigem o reprocessamento manual usando a ação **[!UICONTROL Reprocessar ativo]** na interface de Ativos.

As representações padrão geradas com os microserviços de ativos são armazenadas de forma compatível com versões anteriores nos nós do repositório de ativos (mesmas convenções de nomenclatura).

## Desenvolver e testar microserviços de ativos {#asset-microservices}

Os microserviços de ativos fornecem um processamento escalonável e resiliente de ativos usando serviços em nuvem. O Adobe gerencia os serviços em nuvem para uma manipulação ideal de diferentes tipos de ativos e opções de processamento. Os microserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como o ImageMagick) e a simplificar configurações, além de fornecer uma funcionalidade pronta para uso para tipos de arquivos comuns. Agora você pode processar uma [ampla variedade de tipos de arquivos](/help/assets/file-format-support.md) cobrindo mais formatos prontos para uso do que o possível com versões anteriores do Experience Manager. Por exemplo, a extração em miniatura dos formatos PSD e PSB agora é possível e exigia soluções de terceiros como o ImageMagick. Não é possível usar as configurações complexas do ImageMagick para a configuração [!UICONTROL Perfis de processamento]. Use [!DNL Dynamic Media] para a transcodificação FFmpeg de vídeos e use perfis de processamento para [transcodificação básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Os microserviços de ativos são um serviço nativo da nuvem que é automaticamente provisionado e conectado ao Experience Manager nos programas e ambientes do cliente gerenciados no Cloud Manager. Para estender ou personalizar o Experience Manager, os desenvolvedores podem usar o conteúdo ou os ativos existentes com execuções geradas em um ambiente em nuvem, para testar e validar seu código usando, exibindo e baixando ativos.

Para fazer uma validação completa do código e do processo, incluindo a ingestão e o processamento de ativos, implante as alterações de código em um ambiente de desenvolvimento de nuvem usando [o pipeline](/help/implementing/cloud-manager/configure-pipeline.md) e teste com a execução completa do processamento de microserviços de ativos.

## Remoção da interface do usuário clássica {#classic-ui}

A interface clássica não está mais disponível no Experience Manager como Cloud Service. A interface padrão é a interface habilitada para toque.
