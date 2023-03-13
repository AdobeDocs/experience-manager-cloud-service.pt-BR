---
title: Alterações importantes no [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: Alterações importantes no [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] em comparação a [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: 86941606cba81ebff21e3db70967f862eabf7515
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 9%

---

# Alterações importantes no [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] O traz muitos novos recursos e possibilidades para gerenciar os projetos do Experience Manager. Há muitas diferenças entre [!DNL Experience Manager Assets] local ou hospedado como Adobe Managed Service em comparação com o [!DNL Experience Manager] as a [!DNL Cloud Service]. Este artigo destaca as diferenças importantes para [!DNL Assets] recursos.

As principais diferenças [!DNL Experience Manager] 6.5 estão nas seguintes áreas:

* [Assimilação, upload e processamento de ativos](#asset-ingestion).
* [Microsserviços de ativos para processamento nativo em nuvem](#asset-microservices).
* [Remoção da interface do usuário clássica](#classic-ui).

## Assimilação, processamento e distribuição de ativos {#asset-ingestion-distribution}

O upload de ativos é otimizado para eficiência, permitindo melhor dimensionamento da assimilação, uploads mais rápidos, processamento mais rápido usando microsserviços e assimilação em massa. Os recursos do produto (interfaces de usuário da Web, clientes de desktop) são atualizados. Além disso, isso pode afetar algumas personalizações existentes.

* [!DNL Experience Manager] O usa o princípio de acesso binário direto para carregar e baixar ativos e o usa microsserviços de ativos para processar ativos. Consulte [visão geral dos microsserviços](/help/assets/asset-microservices-overview.md).
   * Upload de ativo [com acesso binário direto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obter detalhes técnicos, consulte [APIs e protocolo de upload binário direto](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Para obter uma comparação dos métodos de API disponíveis para operações CRUD básicas, consulte [APIs e operações de ativos](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* O fluxo de trabalho padrão **[!UICONTROL DAM Asset Update]** nas versões anteriores do não está mais disponível. [!DNL Experience Manager] Em vez disso, os microsserviços de ativos fornecem um serviço escalável e prontamente disponível que cobre a maioria do processamento de ativos padrão (representações, extração de metadados e extração de texto para indexação).
   * Consulte [configurar e usar microsserviços de ativos](/help/assets/asset-microservices-configure-and-use.md)
   * Para personalizar etapas do fluxo de trabalho no processamento, [fluxos de trabalho de pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) pode ser usado.

* Os componentes do site que fornecem um arquivo binário sem qualquer transformação podem usar o download direto. O servlet Sling GET é atualizado para permitir que os desenvolvedores façam isso por padrão. Os componentes do site que fornecem um binário com alguma transformação (por exemplo, redimensioná-lo por meio de um servlet) podem continuar a operar como estão.

As representações padrão geradas com os microsserviços de ativos são armazenadas de forma compatível com versões anteriores nos nós do repositório de ativos usando as mesmas convenções de nomenclatura.

## Desenvolver e testar os microsserviços de ativos {#asset-microservices}

Os microsserviços de ativos fornecem um processamento escalável e resiliente de ativos usando serviços em nuvem. A Adobe gerencia os serviços em nuvem para obter o tratamento ideal de diferentes tipos de ativos e opções de processamento. Os microsserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como [!DNL ImageMagick]) e simplificar as configurações, ao mesmo tempo em que fornece funcionalidade pronta para uso para tipos de arquivos comuns. Agora você pode processar um [ampla variedade de tipos de arquivos](/help/assets/file-format-support.md) abrange mais formatos prontos para uso do que o possível com versões anteriores do Experience Manager. Por exemplo, a extração em miniatura dos formatos PSD e PSB agora é possível, pois anteriormente as soluções de terceiros necessárias, como [!DNL ImageMagick]. Não é possível usar as configurações complexas de [!DNL ImageMagick] para o [!UICONTROL Processamento de perfis] configuração. Uso [!DNL Dynamic Media] transcodificação FFmpeg avançada de vídeos e utilização de perfis de processamento para [transcodificação básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Os microsserviços de ativos são um serviço nativo em nuvem provisionado e conectado automaticamente [!DNL Experience Manager] em programas e ambientes de clientes gerenciados no Cloud Manager. Para estender ou personalizar [!DNL Experience Manager], os desenvolvedores podem usar o conteúdo ou os ativos existentes com representações geradas em um ambiente de nuvem para testar e validar o código usando, exibindo e baixando ativos.

Para fazer uma validação completa do código e do processo, incluindo a assimilação e o processamento de ativos, implante as alterações de código em um ambiente de desenvolvimento em nuvem usando [o pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) e teste com a execução completa do processamento de microsserviços de ativos.

## Paridade de recursos com [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service] A apresenta muitos novos recursos e maneiras mais eficientes de os recursos existentes funcionarem. No entanto, ao mudar de [!DNL Experience Manager] 6.5 a [!DNL Experience Manager] as a [!DNL Cloud Service], você pode notar que alguns recursos funcionam de forma diferente, não estão disponíveis ou estão parcialmente disponíveis. Veja a seguir uma lista desses recursos. Além disso, consulte a seção [recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

| Funcionalidade ou caso de uso | Status em [!DNL Experience Manager] as a [!DNL Cloud Service] | Comentários |
|-----|-----|-----|
| [Detecção de ativos duplicados](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | Funciona de forma diferente | Consulte [como funcionava no [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [Representações Somente para posicionamento (FPO)](/help/assets/configure-fpo-renditions.md) | Funciona de forma diferente | Os perfis de processamento usam microsserviços de ativos para gerar representações FPO. No Experience Manager 6.5, uma solução de terceiros, como [!DNL ImageMagick] estava disponível para gerar as representações. |
| Writeback de metadados | Funciona de forma diferente | Desativado por padrão. Ative o iniciador do fluxo de trabalho correspondente, se necessário. O Writeback é manipulado pelos microsserviços de ativos. |
| Processamento de ativos carregados usando o Gerenciador de pacotes | Requer intervenção manual | Reprocessar manualmente usando o **[!UICONTROL Reprocessar ativo]** ação. |
| Detecção de tipo MIME | Não suportado. | Se você fizer upload de um ativo digital sem uma extensão ou com uma extensão incorreta, talvez ele não seja processado conforme desejado. Os usuários ainda podem armazenar os arquivos binários sem uma extensão no DAM. Consulte [Detecção de tipo MIME em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Geração de subativos para um ativo composto | Não suportado. | Casos de uso dependentes, como anotações, podem não ser cumpridos. Consulte [criação de subativos no [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). A visualização de PDF de alguns tipos de arquivos está disponível a partir de [Versão 2021.7.0](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Editar imagens | Não suportado | A edição de ativos não é permitida no Experience Manager as a Cloud Service. Consulte [como funcionava no Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| Página inicial | Não suportado | Consulte [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Extrair ativos do arquivo ZIP | Não suportado | Consulte [Extração do ZIP em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| Classificações de ativos | Não suportado | O widget de classificação no editor de esquema de metadados não é compatível. |
| Filtro de disposição de conteúdo | Não suportado | Um caso de uso popular de `ContentDispositionFilter` é permitir que os administradores configurem [!DNL Experience Manager] para fornecer arquivos de HTML e abrir arquivos de PDF em linha em vez de baixá-los. Nas instâncias de Publicação, é possível gerenciar o descarte usando a configuração do Dispatcher. Nas instâncias do Autor, o Adobe não recomenda a modificação do cabeçalho Disposição de conteúdo. Consulte [Filtro de Disposição de Conteúdo em [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| Modelo de sessão de fotos do produto | Não suportado | Consulte [modelo de sessão de fotos do produto no [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| Tradução inteligente | Não suportado | [Tradução inteligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) não é compatível com o [!DNL Experience Manager] as a [!DNL Cloud Service]. |
| WebDAV | Não suportado | Para obter alternativas, consulte [[!DNL Creative Cloud] integração](/help/assets/aem-cc-integration-best-practices.md) ou [Material de referência do desenvolvedor](/help/assets/developer-reference-material-apis.md). |
| Interface do usuário clássica | Não suportado | Somente a interface de usuário habilitada para toque está disponível. |

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
>* [Tutoriais em vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=pt-BR)

