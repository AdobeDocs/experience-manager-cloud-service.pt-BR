---
title: Insira tags inteligentes em seus ativos de vídeo
description: O Experience Manager adiciona automaticamente tags inteligentes contextuais e descritivas a vídeos usando [!DNL Adobe Sensei].
feature: Smart Tags,Tagging
role: Admin,User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 2%

---

# Insira tags inteligentes em seus ativos de vídeo {#video-smart-tags}

A crescente necessidade de novos conteúdos exige esforços manuais reduzidos para fornecer experiências digitais atraentes em breve. [!DNL Adobe Experience Manager] como [!DNL Cloud Service] O suporta marcação automática de ativos de vídeo usando inteligência artificial. Marcar os vídeos manualmente pode ser demorado. No entanto, [!DNL Adobe Sensei] O recurso de marcação inteligente de vídeo alimentado usa modelos de inteligência artificial para analisar o conteúdo do vídeo e adicionar tags aos ativos do vídeo. Dessa forma, os usuários do DAM podem fornecer experiências avançadas aos clientes. Adobe gera dois conjuntos de tags para um vídeo. Embora, um conjunto corresponda a objetos, cenas e atributos nesse vídeo; o outro conjunto está relacionado a ações como beber, correr e correr.

A marcação de vídeo é ativada por padrão em [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. No entanto, é possível [rejeição da marcação inteligente de vídeo](#opt-out-video-smart-tagging) em uma pasta. Os vídeos são marcados automaticamente ao fazer upload de novos vídeos ou reprocessar os existentes. [!DNL Experience Manager] também cria as miniaturas e extrai metadados dos arquivos de vídeo. As tags inteligentes são exibidas em ordem decrescente de suas [pontuação de confiança](#confidence-score-video-tag) no ativo [!UICONTROL Propriedades].

## Vídeos de marcação inteligente no upload {#smart-tag-assets-on-ingestion}

Quando você [fazer upload de ativos de vídeo](add-assets.md#upload-assets) para [!DNL Adobe Experience Manager] como [!DNL Cloud Service], os vídeos são processados. Quando o processamento estiver concluído, consulte o [!UICONTROL Básico] guia de ativo [!UICONTROL Propriedades] página. As tags inteligentes são adicionadas automaticamente ao vídeo em [!UICONTROL Tags inteligentes]. Os microsserviços de ativos aproveitam [!DNL Adobe Sensei] para criar essas tags inteligentes.

![Tags inteligentes são adicionadas aos vídeos e visualizadas na guia Básicas das Propriedades do ativo](assets/smart-tags-added-to-videos.png)

As tags inteligentes aplicadas são classificadas em ordem decrescente de [pontuação de confiança](#confidence-score-video-tag), combinados para tags de objeto e ação, em [!UICONTROL Tags inteligentes].

>[!IMPORTANT]
>
>É recomendável revisar essas tags geradas automaticamente para garantir que estejam em conformidade com sua marca e seus valores.

## Marcação inteligente de vídeos existentes no DAM {#smart-tag-existing-videos}

Os ativos de vídeo já existentes no DAM não são marcados com tags inteligentes automaticamente. Você precisa [!UICONTROL Reprocessar ativos] para gerar tags inteligentes manualmente.

Para adicionar tags inteligentes a ativos de vídeo ou pastas (incluindo subpastas) de ativos que já existem no repositório de ativos, siga estas etapas:

1. Selecione o [!DNL Adobe Experience Manager] e, em seguida, selecione ativos no [!UICONTROL Navegação] página.

1. Selecionar [!UICONTROL Arquivos] para exibir a interface do Assets.

1. Navegue até a pasta na qual deseja aplicar tags inteligentes.

1. Selecione a pasta inteira ou ativos de vídeo específicos.

1. Selecionar ![Ícone Reprocessar ativos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocessar ativos] e selecione o [!UICONTROL Processo completo] opção.

<!-- TBD: Limit size -->

![Reprocessar ativos para adicionar tags a vídeos do repositório DAM existente](assets/reprocess.gif)

Depois que o processo for concluído, navegue até a [!UICONTROL Propriedades] de qualquer ativo de vídeo dentro da pasta. As tags adicionadas automaticamente são vistas em [!UICONTROL Tags inteligentes] seção em [!UICONTROL Básico] guia . Essas tags inteligentes aplicadas são classificadas em ordem decrescente de [pontuação de confiança](#confidence-score-video-tag).

## Pesquisar vídeos marcados {#search-smart-tagged-videos}

Para pesquisar os ativos de vídeo com base nas tags inteligentes geradas automaticamente, use [Omnisearch](search-assets.md#search-assets-in-aem):

1. Selecione o ícone de pesquisa ![ícone de pesquisa](assets/do-not-localize/search_icon.png) para exibir o campo Omnisearch.

1. Especifique uma tag, no campo Omnisearch , que você não adicionou explicitamente a um vídeo.

1. Pesquisar com base na tag .

Os resultados da pesquisa exibem os ativos do vídeo com base na tag especificada.

Os resultados da pesquisa são uma combinação de ativos de vídeo com palavras-chave pesquisadas nos metadados e nos ativos de vídeo que são marcados de forma inteligente com as palavras-chave pesquisadas. No entanto, os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. Para obter mais informações, consulte [Entender [!DNL Experience Manager] resultados de pesquisa com tags inteligentes](smart-tags.md#understand-search).

## Moderar tags inteligentes de vídeo {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] O permite preparar as tags inteligentes para:

* remover tags imprecisas atribuídas aos vídeos da sua marca.

* refine pesquisas baseadas em tags para vídeos, garantindo que seu vídeo apareça nos resultados da pesquisa para obter as tags mais relevantes. Portanto, elimina as chances de vídeos não relacionados aparecerem nos resultados da pesquisa.

* atribua uma classificação mais alta a uma tag para aumentar sua relevância em relação a um vídeo. Promover uma tag para um vídeo aumenta a probabilidade de o vídeo aparecer nos resultados da pesquisa quando uma pesquisa é realizada com base nessa tag.

Para saber mais sobre como moderar as tags inteligentes para ativos, consulte [Gerenciar tags inteligentes](smart-tags.md#manage-smart-tags-and-searches).

![Moderar tags inteligentes de vídeo](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Qualquer tag que seja moderada usando as etapas em [Gerenciar tags inteligentes](smart-tags.md#manage-smart-tags-and-searches) não são lembradas no reprocessamento do ativo. O conjunto original de tags é exibido novamente.

## Rejeitar a marcação inteligente de vídeo {#opt-out-video-smart-tagging}

Como a marcação automatizada de vídeos é executada em paralelo a outras tarefas de processamento de ativos, como a criação de miniaturas e a extração de metadados, ela pode ser demorada. Para agilizar o processamento de ativos, você pode optar por não participar da marcação inteligente de vídeo no upload no nível da pasta.

Para recusar a geração automatizada de tags inteligentes de vídeo para ativos enviados para uma pasta específica:

1. Abrir [!UICONTROL Processamento de ativos] guia na pasta [!UICONTROL Propriedades].

1. Em [!UICONTROL Tags inteligentes para vídeos] menu, [!UICONTROL Herdado] é selecionada por padrão e a tag inteligente de vídeo é ativada.

   Quando a variável [!UICONTROL Herdado] for selecionada, o caminho da pasta herdada também será visível junto com as informações se estiver definido como [!UICONTROL Habilitar] ou [!UICONTROL Desativar].

   ![Desativar a marcação inteligente de vídeo](assets/disable-video-tagging.png)

1. Selecionar [!UICONTROL Desativar] para recusar a marcação inteligente de vídeos carregados na pasta.

>[!IMPORTANT]
>
>Se você recusou a marcação de vídeos em uma pasta no momento do upload e deseja adicionar uma tag inteligente aos vídeos após o upload, então **[!UICONTROL Ativar Tags inteligentes para vídeos]** from [!UICONTROL Processamento de ativos] da pasta [!UICONTROL Propriedades] e uso [[!UICONTROL Reprocessar ativo] opção](#smart-tag-existing-videos) para adicionar tags inteligentes ao vídeo.

## Pontuação de confiança {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] O aplica um limite de confiança mínimo para tags inteligentes de objeto e ação, a fim de evitar tags demais para cada ativo de vídeo, o que retarda a indexação. Os resultados da pesquisa de ativos são classificados com base nas pontuações de confiança, o que geralmente melhora os resultados da pesquisa, além do que uma inspeção das tags atribuídas de qualquer ativo de vídeo sugere. Tags imprecisas geralmente têm pontuações de confiança baixa, de modo que raramente aparecem no topo da lista de Tags inteligentes para ativos.

O limite padrão para tags de ação e objeto em [!DNL Adobe Experience Manager] é 0,7 (deve ser um valor entre 0 e 1). Se alguns ativos de vídeo não forem marcados por uma tag específica, isso indica que o algoritmo tem menos de 70% de confiança nas tags previstas. O limite padrão pode nem sempre ser ideal para todos os usuários. Portanto, você pode alterar o valor da pontuação de confiança na configuração OSGI.

Para adicionar a configuração OSGI da pontuação de confiança ao projeto implantado em [!DNL Adobe Experience Manager] como [!DNL Cloud Service] through [!DNL Cloud Manager]:

* No [!DNL Adobe Experience Manager] projeto (`ui.config` desde o Archetype 24 ou anteriormente `ui.apps`) `config.author` Configuração do OSGi, inclua um arquivo de configuração chamado `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` com o seguinte conteúdo:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>As tags manuais recebem uma confiança de 100% (confiança máxima). Portanto, se houver ativos de vídeo com tags manuais que correspondam à consulta de pesquisa, eles serão exibidos antes das tags inteligentes que correspondem à consulta de pesquisa.

## Limitações {#video-smart-tagging-limitations}

* Não é possível treinar o serviço que aplica tags inteligentes a vídeos usando qualquer vídeo específico. Funciona com o padrão [!DNL Adobe Sensei] configurações.

* O progresso da marcação não é exibido.

* Somente os vídeos com menos de 300 MB em tamanho de arquivo são marcados automaticamente. O [!DNL Adobe Sensei] O serviço ignora arquivos de vídeo maiores.

* Somente os vídeos nos formatos de arquivo e os codecs compatíveis mencionados em [Tags inteligentes](/help/assets/smart-tags.md#smart-tags-supported-file-formats) são marcados.

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

>[!MORELIKETHIS]
>
>* [Gerenciar tags inteligentes e pesquisas de ativos](smart-tags.md#manage-smart-tags-and-searches)
>* [Treinar o serviço de Tag inteligente e marcar suas imagens](smart-tags.md)

