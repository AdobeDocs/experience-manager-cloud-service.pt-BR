---
title: Alterações importantes no [!DNL Adobe Experience Manager Assets] como [!DNL Cloud Service]
description: Alterações importantes no [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] as compared to [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: fe662a515a52bcf4648585366422064edce1a7fd
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 5%

---

# Alterações importantes no [!DNL Experience Manager Assets] como [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] como [!DNL Cloud Service] O oferece muitos novos recursos e possibilidades para gerenciar seus projetos do Experience Manager. Há muitas diferenças entre [!DNL Experience Manager Assets] no local ou hospedado como Adobe Managed Service em comparação ao [!DNL Experience Manager] como [!DNL Cloud Service]. Este artigo destaca as diferenças importantes para [!DNL Assets] recursos.

As principais diferenças em comparação com [!DNL Experience Manager] 6.5 estão nos seguintes domínios:

* [Assimilação, upload e processamento de ativos](#asset-ingestion).
* [Microserviços de ativos para processamento nativo em nuvem](#asset-microservices).
* [Remoção da interface do usuário clássica](#classic-ui).

## Assimilação, processamento e distribuição de ativos {#asset-ingestion-distribution}

O upload de ativos é otimizado para maior eficiência, permitindo uma melhor escala de assimilação, uploads mais rápidos, processamento mais rápido usando microsserviços e assimilação em massa. Os recursos do produto (interfaces de usuário da Web, clientes de desktop) são atualizados. Além disso, isso pode afetar algumas personalizações existentes.

* [!DNL Experience Manager] O usa o princípio de acesso binário direto para fazer upload e download de ativos e usa microsserviços de ativos para processar ativos. Consulte [visão geral dos microsserviços](/help/assets/asset-microservices-overview.md).
   * Upload de ativo [com acesso binário direto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Para obter detalhes técnicos, consulte [protocolo e APIs de upload binário direto](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Para obter uma comparação dos métodos de API disponíveis para operações básicas de CRUD, consulte [APIs e operações de ativos](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* O fluxo de trabalho padrão **[!UICONTROL DAM Asset Update]** nas versões anteriores do não está mais disponível. [!DNL Experience Manager] Em vez disso, os microsserviços de ativos fornecem um serviço escalável e prontamente disponível que abrange a maior parte do processamento de ativos padrão (representações, extração de metadados e extração de texto para indexação).
   * Consulte [configurar e usar microsserviços de ativos](/help/assets/asset-microservices-configure-and-use.md)
   * Para personalizar as etapas do fluxo de trabalho no processamento, [fluxos de trabalho de pós-processamento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) pode ser usada.

* Os componentes do site que fornecem um arquivo binário sem qualquer transformação podem usar o download direto. O servlet Sling GET é atualizado para permitir que os desenvolvedores façam isso por padrão. Os componentes do site que fornecem um binário com alguma transformação (por exemplo, redimensioná-lo por meio de um servlet) podem continuar a funcionar como estão.

As representações padrão geradas com os microsserviços de ativos são armazenadas de forma compatível com versões anteriores nos nós do repositório de ativos usando as mesmas convenções de nomenclatura.

## Desenvolver e testar microsserviços de ativos {#asset-microservices}

Os microsserviços de ativos fornecem um processamento escalável e resiliente de ativos usando serviços em nuvem. O Adobe gerencia os serviços em nuvem para obter o tratamento ideal de diferentes tipos de ativos e opções de processamento. Os microsserviços de ativos ajudam a evitar a necessidade de ferramentas e métodos de renderização de terceiros (como [!DNL ImageMagick]) e simplificar as configurações, além de fornecer funcionalidade pronta para uso para tipos de arquivos comuns. Agora você pode processar um [grande variedade de tipos de arquivos](/help/assets/file-format-support.md) cobrindo mais formatos prontos para uso do que o possível com versões anteriores do Experience Manager. Por exemplo, a extração em miniatura de formatos PSD e PSB agora é possível que tenha exigido anteriormente soluções de terceiros, como [!DNL ImageMagick]. Não é possível usar as configurações complexas de [!DNL ImageMagick] para [!UICONTROL Processando perfis] configuração. Use [!DNL Dynamic Media] para transcodificação avançada de vídeos do FFmpeg e use perfis de processamento para [transcodificação básica de vídeos MP4](/help/assets/manage-video-assets.md#transcode-video).

Os microsserviços de ativos são um serviço nativo em nuvem que é automaticamente provisionado e conectado [!DNL Experience Manager] em programas e ambientes do cliente gerenciados no Cloud Manager. Para estender ou personalizar [!DNL Experience Manager], os desenvolvedores podem usar o conteúdo ou ativos existentes com representações geradas em um ambiente de nuvem, para testar e validar seu código usando, exibindo e baixando ativos.

Para fazer uma validação completa do código e do processo, incluindo a assimilação e o processamento de ativos, implante as alterações de código em um ambiente de desenvolvimento em nuvem usando [o pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) e testar com a execução total do processamento de microsserviços de ativos.

## Paridade de recursos com [!DNL Experience Manager] 6,5 {#cloud-service-feature-status}

[!DNL Experience Manager] como [!DNL Cloud Service] apresenta vários recursos novos e maneiras mais eficientes de os recursos existentes funcionarem. No entanto, ao mudar de [!DNL Experience Manager] 6.5 a [!DNL Experience Manager] como [!DNL Cloud Service], você pode notar que alguns recursos funcionam de forma diferente, não estão disponíveis ou estão disponíveis parcialmente. Veja a seguir uma lista desses recursos. Além disso, consulte o [recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

| Recurso ou caso de uso | Status em [!DNL Experience Manager] como [!DNL Cloud Service] | Comentários |
|-----|-----|-----|
| [Detecção de ativos duplicados](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | Funciona de forma diferente | Consulte [como funcionava [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [Representações somente para posicionamento (FPO)](/help/assets/configure-fpo-renditions.md) | Funciona de forma diferente | Os Perfis de processamento usam microsserviços de ativos para gerar representações de FPO. No Experience Manager 6.5, uma solução de terceiros, como [!DNL ImageMagick] estava disponível para gerar as renderizações. |
| Write-back de metadados | Funciona de forma diferente | Desativado por padrão. Ative o iniciador do fluxo de trabalho correspondente, se necessário. O write-back é realizado pelos microsserviços de ativos. |
| Processamento de ativos carregados usando o Gerenciador de pacotes | Precisa de intervenção manual | Reprocessar manualmente usando o **[!UICONTROL Reprocessar ativo]** ação. |
| Detecção de tipo MIME | Não suportado. | Se você carregar um ativo digital sem uma extensão ou com uma extensão incorreta, ele poderá não ser processado conforme desejado. Os usuários ainda podem armazenar os arquivos binários sem uma extensão no DAM. Consulte [Detecção de tipo MIME em [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Geração de subconjunto para ativos compostos | Não suportado. | Casos de uso dependentes como anotações podem não ser cumpridos. Consulte [criação de subativos em [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). A visualização de PDF de alguns tipos de arquivos está disponível a partir de [Versão 2021.7.0](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Editar imagens | Não suportado | A edição de ativos não é suportada no Experience Manager as a Cloud Service. Consulte [como funcionava no Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| Página inicial | Não suportado | Consulte [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Extrair ativos do arquivo ZIP | Não suportado | Consulte [Extração de ZIP em [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| Classificações de ativos | Não suportado | Não há suporte para o widget de classificação no editor de esquema de metadados. |
| Filtro de disposição de conteúdo | Não suportado | Um caso de uso popular de `ContentDispositionFilter` é permitir que os administradores configurem [!DNL Experience Manager] para enviar arquivos HTML e abrir arquivos PDF em linha, em vez de baixá-los. Nas instâncias de Publicação, é possível gerenciar a disposição usando a configuração do Dispatcher. Nas instâncias de Autor, o Adobe não recomenda a modificação do cabeçalho de Disposição de Conteúdo. Consulte [Filtro Content Disposition em [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| [Baixar relatório](/help/assets/asset-reports.md) | Não suportado | Por enquanto, o relatório de download que informa o uso de ativos não está disponível. Consulte [baixar relatório em [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html). |
| Modelo de sessão fotográfica do produto | Não suportado | Consulte [modelo de sessão de fotos do produto em [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| Tradução inteligente | Não suportado | [Tradução inteligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) não é compatível com o [!DNL Experience Manager] como [!DNL Cloud Service]. |
| WebDAV | Não suportado | Para obter alternativas, consulte [[!DNL Creative Cloud] integração](/help/assets/aem-cc-integration-best-practices.md) ou [Material de referência do desenvolvedor](/help/assets/developer-reference-material-apis.md). |
| Interface do usuário clássica | Não suportado | Somente a interface habilitada para toque está disponível. |

>[!MORELIKETHIS]
>
>Os seguintes recursos estão disponíveis para [!DNL Experience Manager] como [!DNL Cloud Service]:
>
>* [Lista de recursos obsoletos e removidos](/help/release-notes/deprecated-removed-features.md)
>* [Uma introdução](/help/overview/introduction.md)
>* [Novidades e diferenças](/help/overview/what-is-new-and-different.md)
>* [A arquitetura](/help/overview/architecture.md)
>* [Alterações importantes](/help/release-notes/aem-cloud-changes.md)
>* [Alterações importantes [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutoriais em vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=pt-BR)

