---
title: Tag inteligente de seus ativos de vídeo
description: O Experience Manager adiciona automaticamente tags inteligentes contextuais e descritivas aos vídeos usando [!DNL Adobe Sensei].
feature: Tags inteligentes,Marcação
role: Admin,User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 0%

---

# Tag inteligente de seus ativos de vídeo {#video-smart-tags}

A crescente necessidade de novos conteúdos exige esforços manuais reduzidos para fornecer experiências digitais atraentes em breve. [!DNL Adobe Experience Manager] O as a  [!DNL Cloud Service] suporta a marcação automática de ativos de vídeo usando inteligência artificial. Marcar os vídeos manualmente pode ser demorado. No entanto, o recurso de marcação inteligente de vídeo [!DNL Adobe Sensei] alimentado usa modelos de inteligência artificial para analisar o conteúdo do vídeo e adicionar tags aos ativos do vídeo. Dessa forma, os usuários do DAM podem fornecer experiências avançadas aos clientes. Adobe gera dois conjuntos de tags para um vídeo. Embora, um conjunto corresponda a objetos, cenas e atributos nesse vídeo; o outro conjunto está relacionado a ações como beber, correr e correr.

A marcação de vídeo é ativada por padrão em [!DNL Adobe Experience Manager] como um [!DNL Cloud Service]. No entanto, você pode [recusar a marcação inteligente de vídeo](#opt-out-video-smart-tagging) em uma pasta. Os vídeos são marcados automaticamente ao fazer upload de novos vídeos ou reprocessar os existentes. [!DNL Experience Manager] também cria as miniaturas e extrai metadados dos arquivos de vídeo. As tags inteligentes são exibidas em ordem decrescente de sua [pontuação de confiança](#confidence-score-video-tag) no ativo [!UICONTROL Propriedades].

## Vídeos de marcação inteligente no upload {#smart-tag-assets-on-ingestion}

Ao [fazer upload de ativos de vídeo](add-assets.md#upload-assets) para [!DNL Adobe Experience Manager] como um [!DNL Cloud Service], os vídeos são processados. Quando o processamento estiver concluído, consulte a guia [!UICONTROL Básico] do ativo [!UICONTROL Propriedades]. Tags inteligentes são adicionadas automaticamente ao vídeo em [!UICONTROL Tags inteligentes]. Os microsserviços de ativos aproveitam [!DNL Adobe Sensei] para criar essas tags inteligentes.

![Tags inteligentes são adicionadas aos vídeos e visualizadas na guia Básicas das Propriedades do ativo](assets/smart-tags-added-to-videos.png)

As tags inteligentes aplicadas são classificadas em ordem decrescente de [pontuação de confiança](#confidence-score-video-tag), combinadas para tags de objeto e ação, em [!UICONTROL Tags inteligentes].

>[!IMPORTANT]
>
>É recomendável revisar essas tags geradas automaticamente para garantir que estejam em conformidade com sua marca e seus valores.

## Marcação inteligente de vídeos existentes no DAM {#smart-tag-existing-videos}

Os ativos de vídeo já existentes no DAM não são marcados com tags inteligentes automaticamente. Você precisa [!UICONTROL Reprocessar Ativos] manualmente para gerar tags inteligentes para eles.

Para adicionar tags inteligentes a ativos de vídeo ou pastas (incluindo subpastas) de ativos que já existem no repositório de ativos, siga estas etapas:

1. Selecione o logotipo [!DNL Adobe Experience Manager] e selecione ativos na página [!UICONTROL Navegação].

1. Selecione [!UICONTROL Arquivos] para exibir a interface de Ativos.

1. Navegue até a pasta na qual deseja aplicar tags inteligentes.

1. Selecione a pasta inteira ou ativos de vídeo específicos.

1. Selecione o ícone ![Reprocessar ativos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocessar Ativos] e selecione a opção [!UICONTROL Processo Completo].

<!-- TBD: Limit size -->

![Reprocessar ativos para adicionar tags a vídeos do repositório DAM existente](assets/reprocess.gif)

Quando o processo estiver concluído, navegue até a página [!UICONTROL Propriedades] de qualquer ativo de vídeo dentro da pasta. As tags adicionadas automaticamente são vistas na seção [!UICONTROL Tags inteligentes] na guia [!UICONTROL Básico]. Essas tags inteligentes aplicadas são classificadas em ordem decrescente de [pontuação de confiança](#confidence-score-video-tag).

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
>Quaisquer tags moderadas usando as etapas em [Gerenciar tags inteligentes](smart-tags.md#manage-smart-tags-and-searches) não são lembradas no reprocessamento do ativo. O conjunto original de tags é exibido novamente.

## Rejeitar a marcação inteligente de vídeo {#opt-out-video-smart-tagging}

Como a marcação automatizada de vídeos é executada em paralelo a outras tarefas de processamento de ativos, como a criação de miniaturas e a extração de metadados, ela pode ser demorada. Para agilizar o processamento de ativos, você pode optar por não participar da marcação inteligente de vídeo no upload no nível da pasta.

Para recusar a geração automatizada de tags inteligentes de vídeo para ativos enviados para uma pasta específica:

1. Abra a guia [!UICONTROL Processamento de Ativos] na pasta [!UICONTROL Propriedades].

1. No menu [!UICONTROL Tags inteligentes para vídeos], a opção [!UICONTROL Herdadas] é selecionada por padrão e a tag inteligente de vídeo é ativada.

   Quando a opção [!UICONTROL Herdado] é selecionada, o caminho da pasta herdada também é visível junto com as informações se está definido como [!UICONTROL Ativar] ou [!UICONTROL Desativar].

   ![Desativar a marcação inteligente de vídeo](assets/disable-video-tagging.png)

1. Selecione [!UICONTROL Desativar] para recusar a marcação inteligente de vídeos carregados na pasta.

>[!IMPORTANT]
>
>Se você tiver optado por não marcar vídeos em uma pasta no momento do upload e quiser marcar os vídeos com tags inteligentes depois do upload, em seguida, **[!UICONTROL Ativar tags inteligentes para vídeos]** da guia [!UICONTROL Processamento de ativos] da pasta [!UICONTROL Propriedades] e usar [[!UICONTROL Reprocessar ativo] opção8 > para adicionar tags inteligentes ao vídeo.](#smart-tag-existing-videos)

## Pontuação de confiança {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] O aplica um limite de confiança mínimo para tags inteligentes de objeto e ação, a fim de evitar tags demais para cada ativo de vídeo, o que retarda a indexação. Os resultados da pesquisa de ativos são classificados com base nas pontuações de confiança, o que geralmente melhora os resultados da pesquisa, além do que uma inspeção das tags atribuídas de qualquer ativo de vídeo sugere. Tags imprecisas geralmente têm pontuações de confiança baixa, de modo que raramente aparecem no topo da lista de Tags inteligentes para ativos.

O limite padrão das tags de ação e objeto em [!DNL Adobe Experience Manager] é 0,7 (deve ser um valor entre 0 e 1). Se alguns ativos de vídeo não forem marcados por uma tag específica, isso indica que o algoritmo tem menos de 70% de confiança nas tags previstas. O limite padrão pode nem sempre ser ideal para todos os usuários. Portanto, você pode alterar o valor da pontuação de confiança na configuração OSGI.

Para adicionar a configuração OSGI da pontuação de confiança ao projeto implantado em [!DNL Adobe Experience Manager] como um [!DNL Cloud Service] por [!DNL Cloud Manager]:

* No projeto [!DNL Adobe Experience Manager] (`ui.config` desde o Archetype 24 ou anteriormente `ui.apps`), a configuração `config.author` OSGi, inclua um arquivo de configuração chamado `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` com o seguinte conteúdo:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>As tags manuais recebem uma confiança de 100% (confiança máxima). Portanto, se houver ativos de vídeo com tags manuais que correspondam à consulta de pesquisa, eles serão exibidos antes das tags inteligentes que correspondem à consulta de pesquisa.

## Limitações           {#video-smart-tagging-limitations}

* Não é possível treinar o serviço que aplica tags inteligentes a vídeos usando qualquer vídeo específico. Funciona com as configurações padrão [!DNL Adobe Sensei].

* O progresso da marcação não é exibido.

* Somente os vídeos com menos de 300 MB em tamanho de arquivo são marcados automaticamente. O serviço [!DNL Adobe Sensei] ignora os arquivos de vídeo maiores.

* Somente os vídeos nos formatos de arquivo e os codecs compatíveis mencionados em [Tags inteligentes](/help/assets/smart-tags.md#smart-tags-supported-file-formats) são marcados.

>[!MORELIKETHIS]
>
>* [Gerenciar tags inteligentes e pesquisas de ativos](smart-tags.md#manage-smart-tags-and-searches)
* [Treinar o serviço de Tag inteligente e marcar suas imagens](smart-tags.md)

