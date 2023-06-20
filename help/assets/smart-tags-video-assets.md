---
title: Insira tags inteligentes em seus ativos de vídeo
description: O Experience Manager adiciona automaticamente Tags inteligentes contextuais e descritivas a vídeos usando [!DNL Adobe Sensei].
feature: Smart Tags,Tagging
role: Admin,User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 3%

---

# Insira tags inteligentes em seus ativos de vídeo {#video-smart-tags}

A necessidade cada vez maior de novos conteúdos exige a redução dos esforços manuais para oferecer experiências digitais atraentes rapidamente. [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] O oferece suporte à marcação automática de ativos de vídeo usando inteligência artificial. Marcar os vídeos manualmente pode ser demorado. No entanto, [!DNL Adobe Sensei] o recurso de marcação inteligente de vídeo habilitada usa modelos de inteligência artificial para analisar conteúdo de vídeo e adicionar tags aos ativos de vídeo. Dessa forma, reduz o tempo para que os usuários do DAM forneçam experiências avançadas aos clientes. O serviço de aprendizado de máquina do Adobe gera dois conjuntos de tags para um vídeo. Enquanto, um conjunto corresponde a objetos, cenas e atributos naquele vídeo; o outro conjunto relaciona-se a ações como beber, correr e correr.

A marcação de vídeo é ativada por padrão no [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]. No entanto, é possível [recusar a marcação inteligente de vídeo](#opt-out-video-smart-tagging) em uma pasta. Os vídeos são marcados automaticamente quando você carrega novos vídeos ou reprocessa os existentes. [!DNL Experience Manager] O também cria as miniaturas e extrai metadados dos arquivos de vídeo. As tags inteligentes são exibidas em ordem decrescente de [pontuação de confiança](#confidence-score-video-tag) no ativo [!UICONTROL Propriedades].

## Marcação inteligente de vídeos no upload {#smart-tag-assets-on-ingestion}

Quando você [fazer upload de ativos de vídeo](add-assets.md#upload-assets) para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service], os vídeos são processados. Após concluir o processamento, consulte a [!UICONTROL Básico] guia do ativo [!UICONTROL Propriedades] página. As tags inteligentes são adicionadas automaticamente ao vídeo em [!UICONTROL Tags inteligentes]. Usos dos microsserviços de ativos [!DNL Adobe Sensei] para criar essas tags inteligentes.

![As Tags inteligentes são adicionadas aos vídeos e visualizadas na guia Básico das Propriedades do ativo](assets/smart-tags-added-to-videos.png)

As tags inteligentes aplicadas são classificadas em ordem descendente de [pontuação de confiança](#confidence-score-video-tag), combinados para tags de objeto e ação, em [!UICONTROL Tags inteligentes].

>[!IMPORTANT]
>
>É recomendável revisar essas tags geradas automaticamente para garantir que estejam em conformidade com sua marca e seus valores.

## Marcação inteligente de vídeos existentes no DAM {#smart-tag-existing-videos}

Os ativos de vídeo já existentes no DAM não são marcados automaticamente com tags inteligentes. Você precisa [!UICONTROL Reprocessar ativos] manualmente para gerar tags inteligentes para eles.

Para marcar ativos de vídeo ou pastas (incluindo subpastas) de ativos que já existem no repositório de ativos, siga estas etapas:

1. Selecione o [!DNL Adobe Experience Manager] e selecione os ativos na lista suspensa [!UICONTROL Navegação] página.

1. Selecionar [!UICONTROL Arquivos] para exibir a interface do Assets.

1. Navegue até a pasta à qual deseja aplicar as tags inteligentes.

1. Selecione a pasta inteira ou ativos de vídeo específicos.

1. Selecionar ![Ícone Reprocessar ativos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocessar ativos] e selecione o [!UICONTROL Processo completo] opção.

<!-- TBD: Limit size -->

![Reprocessamento de ativos para adicionar tags ao repositório DAM existente de vídeos](assets/reprocess.gif)

Quando o processo for concluído, navegue até o [!UICONTROL Propriedades] página de qualquer ativo de vídeo na pasta. As tags adicionadas automaticamente são vistas no [!UICONTROL Tags inteligentes] seção em [!UICONTROL Básico] guia. Essas tags inteligentes aplicadas são classificadas em ordem descendente de [pontuação de confiança](#confidence-score-video-tag).

## Pesquisar vídeos marcados {#search-smart-tagged-videos}

Para pesquisar os ativos de vídeo com base nas tags inteligentes geradas automaticamente, use [Omnisearch](search-assets.md#search-assets-in-aem):

1. Selecione o ícone de pesquisa ![ícone de pesquisa](assets/do-not-localize/search_icon.png) para exibir o campo Omnisearch.

1. Especifique uma tag, no campo Omnisearch, que você não adicionou explicitamente a um vídeo.

1. Pesquise com base na tag.

Os resultados da pesquisa exibem os ativos de vídeo com base na tag especificada.

Os resultados da pesquisa são uma combinação de ativos de vídeo com palavras-chave pesquisadas nos metadados e os ativos de vídeo marcados de forma inteligente com as palavras-chave pesquisadas. No entanto, os resultados da pesquisa que correspondem a todos os termos de pesquisa em campos de metadados são exibidos primeiro, seguido pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. Para obter mais informações, consulte [Compreender [!DNL Experience Manager] resultados da pesquisa com tags inteligentes](smart-tags.md#understand-search).

## Tags inteligentes de vídeo moderadas {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] O permite preparar as tags inteligentes para:

* remova as tags imprecisas atribuídas aos vídeos da sua marca.

* refine as pesquisas por vídeos com base em tags, garantindo que o vídeo seja exibido nos resultados da pesquisa para as tags mais relevantes. Portanto, elimina as chances de vídeos não relacionados aparecerem nos resultados de pesquisa.

* atribua uma classificação mais alta a uma tag para aumentar sua relevância com relação a um vídeo. Promover uma tag para um vídeo aumenta as chances do vídeo aparecer nos resultados da pesquisa quando uma pesquisa é realizada com base nessa tag.

Para saber mais sobre como moderar as tags inteligentes para ativos, consulte [Gerenciar tags inteligentes](smart-tags.md#manage-smart-tags-and-searches).

![Tags inteligentes de vídeo moderadas](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Quaisquer tags moderadas usando as etapas em [Gerenciar tags inteligentes](smart-tags.md#manage-smart-tags-and-searches) não são lembrados no reprocessamento do ativo. O conjunto original de tags é exibido novamente.

## Recusar marcação inteligente de vídeo {#opt-out-video-smart-tagging}

Como a marcação automática de vídeos é executada em paralelo a outras tarefas de processamento de ativos, como criação de miniaturas e extração de metadados, pode ser demorada. Para acelerar o processamento de ativos, você pode recusar a marcação inteligente de vídeo ao fazer upload no nível da pasta.

Para recusar a geração de tags inteligentes de vídeo automatizadas para ativos carregados em uma pasta específica:

1. Abertura [!UICONTROL Processamento de ativos] guia na pasta [!UICONTROL Propriedades].

1. Entrada [!UICONTROL Tags inteligentes para vídeos] menu, [!UICONTROL Herdado] for selecionada por padrão e a tag inteligente de vídeo for ativada.

   Quando a variável [!UICONTROL Herdado] for selecionada, o caminho de pasta herdado também estará visível junto com as informações se estiver definido como [!UICONTROL Ativar] ou [!UICONTROL Desativar].

   ![Desativar marcação inteligente de vídeo](assets/disable-video-tagging.png)

1. Selecionar [!UICONTROL Desativar] para recusar a marcação inteligente de vídeos carregados na pasta.

>[!IMPORTANT]
>
>Se você recusou a marcação de vídeos em uma pasta no momento do upload e deseja marcar os vídeos inteligentes após o upload, **[!UICONTROL Ativar tags inteligentes para vídeos]** de [!UICONTROL Processamento de ativos] guia da pasta [!UICONTROL Propriedades] e usar [[!UICONTROL Reprocessar ativo] opção](#smart-tag-existing-videos) para adicionar tags inteligentes ao vídeo.

## Pontuação de confiança {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] O aplica um limite mínimo de confiança para tags inteligentes de objeto e ação para evitar ter muitas tags para cada ativo de vídeo, o que atrasa a indexação. Os resultados da pesquisa de ativos são classificados com base nas pontuações de confiança, que geralmente melhoram os resultados da pesquisa além do que uma inspeção das tags atribuídas de qualquer ativo de vídeo sugere. Tags imprecisas geralmente têm pontuações de confiança baixas, de modo que raramente são exibidas na parte superior da lista de Tags inteligentes para ativos.

O limite padrão para tags de ação e objeto em [!DNL Adobe Experience Manager] é 0,7 (deve ser um valor entre 0 e 1). Se alguns ativos de vídeo não forem marcados por uma tag específica, isso indica que o algoritmo tem menos de 70% de confiança nas tags previstas. O limite padrão nem sempre pode ser o ideal para todos os usuários. Portanto, você pode alterar o valor da pontuação de confiança na configuração do OSGI.

Para adicionar a configuração OSGI da pontuação de confiança ao projeto implantado em [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] até [!DNL Cloud Manager]:

* No [!DNL Adobe Experience Manager] projeto (`ui.config` desde o Arquétipo 24 ou `ui.apps`) o `config.author` Configuração OSGi, inclua um arquivo de configuração chamado `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` com o seguinte conteúdo:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>As tags manuais recebem uma confiança de 100% (confiança máxima). Portanto, se houver ativos de vídeo com tags manuais que correspondam à consulta de pesquisa, eles serão exibidos antes das tags inteligentes que correspondam à consulta de pesquisa.

## Limitações {#video-smart-tagging-limitations}

* Não é possível treinar o serviço que aplica Tags inteligentes a vídeos usando vídeos específicos. Funciona com o padrão [!DNL Adobe Sensei] configurações.

* O progresso da marcação não é exibido.

* Somente os vídeos com tamanho menor que 300 MB são marcados automaticamente. A variável [!DNL Adobe Sensei] o serviço ignora arquivos de vídeo maiores.

* Somente os vídeos nos formatos de arquivo e codecs compatíveis mencionados em [Tags inteligentes](/help/assets/smart-tags.md#smart-tags-supported-file-formats) estão marcados.

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
>* [Treine o serviço Smart Tag e marque suas imagens](smart-tags.md)
