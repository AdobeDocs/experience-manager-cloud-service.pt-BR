---
title: Alterações notáveis em [!DNL Adobe Experience Manager Assets] como a [!DNL Cloud Service]
description: Alterações notáveis em  [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] em comparação com [!DNL Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: db08a4365d264383cc143727e423ac9886bed66c
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 3%

---


# Alterações notáveis em [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] como resultado,  [!DNL Cloud Service] traz muitos novos recursos e possibilidades para gerenciar seus projetos de Experience Manager. Há muitas diferenças entre [!DNL Experience Manager Assets] no local ou hospedado como serviço gerenciado pelo Adobe em comparação a [!DNL Experience Manager] como um [!DNL Cloud Service]. Este artigo destaca as diferenças importantes para os recursos [!DNL Assets].

As principais diferenças em comparação com [Experience Manager] 6.5 estão nas seguintes áreas:

* [Inclusão, upload e processamento](#asset-ingestion) de ativos.
* [Microserviços de ativos para processamento](#asset-microservices) nativo na nuvem.
* [Remoção da interface do usuário clássica](#classic-ui).

## Inclusão e processamento de ativos {#asset-ingestion}

O upload de ativos é otimizado para proporcionar eficiência, permitindo um melhor dimensionamento da ingestão, uploads mais rápidos, processamento mais rápido usando microserviços e ingestão em massa. Os recursos do produto (interfaces de usuário da Web, clientes de desktop) são atualizados. Além disso, isso pode afetar algumas personalizações existentes.

* [!DNL Experience Manager] usa o princípio de acesso binário direto para fazer upload e download de ativos e usa os microserviços de ativos para processar ativos. Consulte [visão geral dos microserviços](/help/assets/asset-microservices-overview.md).
   * Carregamento de ativos [com acesso binário direto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obter detalhes técnicos, consulte [protocolo de carregamento binário direto e APIs](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Para obter uma comparação dos métodos de API disponíveis para operações CRUD básicas, consulte [APIs e operações de ativos](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* O fluxo de trabalho padrão **[!UICONTROL DAM Asset Update]** nas versões anteriores do não está mais disponível. [!DNL Experience Manager] Em vez disso, os microserviços de ativos fornecem um serviço dimensionável e prontamente disponível que abrange a maioria do processamento de ativos padrão (execuções, extração de metadados e extração de texto para indexação).
   * Consulte [configurar e usar os microserviços de ativos](/help/assets/asset-microservices-configure-and-use.md)
   * Para ter etapas personalizadas de fluxo de trabalho no processamento, [workflows pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) podem ser usados.
* Não há suporte para o write-back de metadados. Consulte [write-back de metadados em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html).
* Os ativos que são carregados usando o Gerenciador de pacotes exigem o reprocessamento manual usando a ação **[!UICONTROL Reprocessar ativo]** na interface do usuário [!DNL Assets].
* [!DNL Assets] não detecta automaticamente o tipo MIME de ativos carregados. Um ativo digital sem uma extensão ou com uma extensão incorreta não é processado conforme desejado. Por exemplo, ao fazer upload desses ativos, nada acontece ou um perfil de processamento incorreto pode se aplicar ao ativo. Os usuários ainda podem armazenar os arquivos binários sem uma extensão no DAM. Consulte [Detecção de tipo MIME em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html).
* [!DNL Experience Manager] como um  [!DNL Cloud Service] não gera subativos para ativos compostos. Consulte [criação de subativos em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets).
* [!DNL Assets] A experiência com o home page não está disponível. Consulte [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html).
* A detecção de ativos de duplicado funciona de forma diferente em comparação a [como funcionava em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html).
* Para execuções somente de posicionamento (FPO) são geradas de forma diferente em comparação às versões anteriores [!DNL Experience Manager]. Consulte [representação FPO para [!DNL Experience Manager] como a [!DNL Cloud Service]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html).

As representações padrão geradas com os microserviços de ativos são armazenadas de forma compatível com versões anteriores nos nós do repositório de ativos usando as mesmas convenções de nomenclatura.

## Desenvolver e testar microserviços de ativos {#asset-microservices}

Os microserviços de ativos fornecem um processamento escalonável e resiliente de ativos usando serviços em nuvem. O Adobe gerencia os serviços em nuvem para uma manipulação ideal de diferentes tipos de ativos e opções de processamento. Os microserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como o ImageMagick) e a simplificar configurações, além de fornecer uma funcionalidade pronta para uso para tipos de arquivos comuns. Agora você pode processar uma [ampla variedade de tipos de arquivos](/help/assets/file-format-support.md) cobrindo mais formatos prontos para uso do que o possível com versões anteriores do Experience Manager. Por exemplo, a extração em miniatura dos formatos PSD e PSB agora é possível e exigia soluções de terceiros como o ImageMagick. Não é possível usar as configurações complexas do ImageMagick para a configuração [!UICONTROL Perfis de processamento]. Use [!DNL Dynamic Media] para transcodificação avançada de vídeos FFmpeg e use perfis de processamento para [transcodificação básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Os microserviços de ativos são um serviço nativo da nuvem que é automaticamente provisionado e conectado a [!DNL Experience Manager] em programas de clientes e ambientes gerenciados no Cloud Manager. Para estender ou personalizar [!DNL Experience Manager], os desenvolvedores podem usar o conteúdo ou os ativos existentes com representações geradas em um ambiente em nuvem, para testar e validar seu código usando, exibindo e baixando ativos.

Para fazer uma validação completa do código e do processo, incluindo a ingestão e o processamento de ativos, implante as alterações de código em um ambiente de desenvolvimento de nuvem usando [o pipeline](/help/implementing/cloud-manager/configure-pipeline.md) e teste com a execução completa do processamento de microserviços de ativos.

## Remoção da interface do usuário clássica {#classic-ui}

A interface clássica não está mais disponível em [!DNL Experience Manager] como [!DNL Cloud Service]. Somente a interface habilitada para toque está disponível.

>[!MORELIKETHIS]
>
>Os seguintes recursos estão disponíveis para [!DNL Experience Manager] como um [!DNL Cloud Service]:
>
>* [Uma introdução](/help/overview/introduction.md)
>* [Novidades e diferenças](/help/overview/what-is-new-and-different.md)
>* [A arquitetura](/help/core-concepts/architecture.md)
>* [Alterações notáveis](/help/release-notes/aem-cloud-changes.md)
>* [Alterações notáveis [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutoriais em vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

