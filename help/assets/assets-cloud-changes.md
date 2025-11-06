---
title: Alterações importantes no  [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: Alterações importantes no [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] em comparação ao [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User, Leader, Developer, Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 8%

---

# Alterações importantes para [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#notable-changes}

O [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] traz muitos novos recursos e possibilidades para gerenciar os projetos da Experience Manager. Há muitas diferenças entre o [!DNL Experience Manager Assets] no local ou hospedado como Adobe Managed Service, em comparação ao [!DNL Experience Manager] as a [!DNL Cloud Service]. Este artigo destaca as diferenças importantes para os recursos do [!DNL Assets].

As principais diferenças em relação ao [!DNL Experience Manager] 6.5 estão nas seguintes áreas:

* [Assimilação, carregamento e processamento de ativos](#asset-ingestion).
* [Microsserviços de ativos para processamento nativo em nuvem](#asset-microservices).
* [Remoção da interface clássica](#classic-ui).

## Assimilação, processamento e distribuição de ativos {#asset-ingestion-distribution}

O upload de ativos é otimizado para eficiência, permitindo melhor dimensionamento da assimilação, uploads mais rápidos, processamento mais rápido usando microsserviços e assimilação em massa. Os recursos do produto (interfaces de usuário da Web, clientes de desktop) são atualizados. Além disso, esses itens podem afetar algumas personalizações existentes.

* [!DNL Experience Manager] usa o princípio de acesso binário direto para carregar e baixar ativos e usa microsserviços de ativos para processar ativos. Consulte uma [visão geral dos microsserviços](/help/assets/asset-microservices-overview.md).
   * Carregamento de ativo [com acesso binário direto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obter detalhes técnicos, consulte [protocolo de carregamento binário direto e APIs](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Para obter uma comparação dos métodos de API disponíveis para operações CRUD básicas, consulte [APIs e operações de ativos](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* O fluxo de trabalho padrão **[!UICONTROL Atualização do Ativo DAM]** em versões anteriores do [!DNL Experience Manager] não está mais disponível. Em vez disso, os microsserviços de ativos fornecem um serviço escalável e prontamente disponível que cobre a maioria do processamento de ativos padrão (representações, extração de metadados e extração de texto para indexação).
   * Consulte [configurar e usar microsserviços de ativos](/help/assets/asset-microservices-configure-and-use.md)
   * Para personalizar etapas do fluxo de trabalho no processamento, [fluxos de trabalho de pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) podem ser usados.

* Os componentes do site que fornecem um arquivo binário sem qualquer transformação podem usar o download direto. O servlet Sling GET é atualizado para ativar essa funcionalidade por padrão. Os componentes do site que fornecem um binário com alguma transformação (por exemplo, redimensioná-lo por meio de um servlet) podem continuar a operar como estão.

As representações padrão geradas com os microsserviços de ativos são armazenadas de forma compatível com versões anteriores nos nós do repositório de ativos usando as mesmas convenções de nomenclatura.

## Desenvolver e testar os microsserviços de ativos {#asset-microservices}

Os microsserviços de ativos fornecem um processamento escalável e resiliente de ativos usando serviços em nuvem. A Adobe gerencia os serviços em nuvem para obter o tratamento ideal de diferentes tipos de ativos e opções de processamento. Os microsserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como o [!DNL ImageMagick]) e simplificam as configurações, além de fornecer funcionalidade pronta para uso para tipos de arquivos comuns. Agora você pode processar uma [ampla variedade de tipos de arquivos](/help/assets/file-format-support.md) que abrangem mais formatos prontos para uso do que o possível com versões anteriores do Experience Manager. Por exemplo, a extração de miniaturas dos formatos PSD e PSB agora é possível e anteriormente exigia soluções de terceiros, como o [!DNL ImageMagick]. Você não pode usar as configurações complexas de [!DNL ImageMagick] para a configuração [!UICONTROL Processando Perfis]. Use [!DNL Dynamic Media] para a transcodificação avançada FFmpeg de vídeos e use perfis de processamento para [transcodificação básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Os microsserviços de ativos são um serviço nativo em nuvem provisionado e conectado automaticamente ao [!DNL Experience Manager] em programas e ambientes de clientes gerenciados no Cloud Manager. Para estender ou personalizar o [!DNL Experience Manager], os desenvolvedores podem usar conteúdo ou ativos existentes com representações geradas em um ambiente de nuvem. Essa capacidade permite que eles testem e validem seu código usando, exibindo ou baixando ativos.

Para fazer uma validação completa do código e do processo, incluindo a assimilação e o processamento de ativos, implante as alterações de código em um ambiente de desenvolvimento em nuvem usando o [pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) e teste com a execução completa do processamento de microsserviços de ativos.

## Paridade de recursos com [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

O [!DNL Experience Manager] as a [!DNL Cloud Service] apresenta muitos recursos novos e formas mais eficientes de os recursos existentes funcionarem. No entanto, ao mudar do [!DNL Experience Manager] 6.5 para o [!DNL Experience Manager] como um [!DNL Cloud Service], você pode notar que alguns recursos funcionam de forma diferente, não estão disponíveis ou estão parcialmente disponíveis. Veja a seguir uma lista desses recursos. Além disso, consulte os [recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

| Funcionalidade ou caso de uso | Status em [!DNL Experience Manager] como [!DNL Cloud Service] | Comentários |
|-----|-----|-----|
| [Detecção de ativos duplicados](/help/assets/detect-duplicate-assets.md) | Isso funciona de forma diferente | Consulte [como funcionou em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/assets/managing/duplicate-detection). |
| [Para representações somente de posicionamento (FPO)](/help/assets/configure-fpo-renditions.md) | Isso funciona de forma diferente | Os perfis de processamento usam microsserviços de ativos para gerar representações FPO. No Experience Manager 6.5, uma solução de terceiros, como [!DNL ImageMagick], estava disponível para gerar as representações. |
| Writeback de metadados | Isso funciona de forma diferente | Desabilitado por padrão. Ative o iniciador do fluxo de trabalho correspondente, se necessário. Os microsserviços de ativos lidam com o write-back. |
| Processamento de ativos carregados usando o Gerenciador de pacotes | Isso requer intervenção manual | Reprocessar manualmente usando a ação **[!UICONTROL Reprocessar Ativo]**. |
| Detecção de tipo MIME | Não suportado. | Se você fizer upload de um ativo digital sem uma extensão ou com uma extensão incorreta, talvez ele não seja processado conforme desejado. Os usuários ainda podem armazenar os arquivos binários sem uma extensão no DAM. Consulte [Detecção de tipo MIME em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/assets/administer/detect-asset-mime-type-with-tika). |
| Geração de subativos para um ativo composto | Não suportado. | Casos de uso dependentes, como anotações, podem não ser cumpridos. Consulte [criação de subativos em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/assets/managing/managing-linked-subassets#generate-subassets). A visualização do PDF de alguns tipos de arquivos está disponível a partir da [versão 2021.7.0](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Editar imagens | Não suportado | A edição de ativos não é permitida no Experience Manager as a Cloud Service. Veja [como funcionou no Experience Manager 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/assets/managing/manage-assets#editing-images). |
| Home page | Não suportado | Ver a [[!DNL Assets] experiência da Página Inicial [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/assets/using/assets-home-page) |
| Extrair ativos do arquivo ZIP | Não suportado | Consulte [Extração de ZIP em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/assets/managing/manage-assets#extractzip). |
| Classificações do Assets | Não suportado | O widget de classificação no editor de esquema de metadados não é compatível. |
| Filtro de disposição de conteúdo | Não suportado | Um caso de uso popular do `ContentDispositionFilter` é permitir que os administradores configurem o [!DNL Experience Manager] para fornecer arquivos do HTML e para abrir arquivos do PDF em linha, em vez de baixá-los. Nas instâncias de publicação, é possível gerenciar o descarte usando a configuração do Dispatcher. Nas instâncias de criação, o Adobe não recomenda a modificação do cabeçalho Disposição do conteúdo. Consulte [Filtro de Disposição de Conteúdo em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/security/content-disposition-filter). |
| Modelo de sessão de fotos do produto | Não suportado | Consulte o [modelo de sessão de fotos do produto em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/sites/authoring/projects/managing-product-information). |
| Tradução inteligente | Não suportado | Não há suporte para a tradução inteligente em [!DNL Experience Manager] como [!DNL Cloud Service]. |
| WebDAV | Não suportado | Para obter alternativas, consulte [[!DNL Creative Cloud] Integração](/help/assets/aem-cc-integration-best-practices.md) ou [Material de referência do desenvolvedor](/help/assets/developer-reference-material-apis.md). |
| IU Clássica | Não suportado | Somente uma interface de usuário habilitada para toque está disponível. |

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>Os seguintes recursos estão disponíveis para [!DNL Experience Manager] as a [!DNL Cloud Service]:
>
>* [Lista de recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md)
>* [Uma introdução](/help/overview/introduction.md)
>* [Novidades e diferenças](/help/overview/what-is-new-and-different.md)
>* [A arquitetura](/help/overview/architecture.md)
>* [Alterações importantes](/help/release-notes/aem-cloud-changes.md)
>* [Alterações importantes [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutoriais em vídeo](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/overview)
