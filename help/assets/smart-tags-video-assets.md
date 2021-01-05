---
title: Marcar com tags inteligentes seus ativos de vídeo
description: A marcação inteligente de ativos de vídeo automatiza a marcação de ativos ao aplicar tags contextuais e descritivas usando os serviços Adobe Sensei.
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 0%

---


# Marcar com tags inteligentes seus ativos de vídeo {#video-smart-tags}

A crescente necessidade de novos conteúdos exige esforços manuais reduzidos para proporcionar experiências digitais atraentes em breve. [!DNL Adobe Experience Manager] como um  [!DNL Cloud Service] suporte à marcação automatizada de ativos de vídeo assistida por inteligência artificial. Marcar os vídeos manualmente pode ser demorado. No entanto, o recurso de marcação inteligente de vídeo equipado com a Adobe Sensei usa modelos de inteligência artificial para analisar o conteúdo de vídeo e adicionar tags aos ativos de vídeo. Dessa forma, reduz o tempo para que os usuários do DAM forneçam experiências avançadas aos seus clientes. O serviço de aprendizado da máquina gera dois conjuntos de tags para um vídeo. Enquanto, um conjunto corresponde a objetos, cenas e atributos nesse vídeo; o outro conjunto está relacionado a ações como beber, correr e correr.

Os formatos de arquivo de vídeo (e seus codecs) suportados para marcação inteligente são MP4 (H264/AVC), MKV (H264/AVC), MOV (H264/AVC, Motion JPEG), AVI (indeo4), FLV (H264/AVC, vp6f) e WMPT V (WMV2). Além disso, a funcionalidade permite a marcação de vídeos até 300 MB. A marcação automatizada de ativos de vídeo ocorre como processamento de ativos padrão (junto com a criação de miniaturas e a extração de metadados) depois que um vídeo é carregado ou quando um novo processamento é acionado. As tags inteligentes são exibidas em ordem decrescente de sua [pontuação de confiança](#confidence-score-video-tag) no ativo [!UICONTROL Propriedades]. A marcação de vídeo está ativada por padrão em [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. No entanto, você pode [optar por não participar da marcação inteligente de vídeo](#opt-out-video-smart-tagging) em uma pasta.

## Vídeos de marcação inteligente no upload {#smart-tag-assets-on-ingestion}

Quando você [faz upload de ativos de vídeo](add-assets.md#upload-assets) para [!DNL Adobe Experience Manager] como um [!DNL Cloud Service], os vídeos passam pelo ![processamento](assets/do-not-localize/assetprocessing.png). Quando o processamento estiver concluído, consulte a guia [!UICONTROL Basic] do ativo [!UICONTROL Propriedades]. Tags inteligentes são automaticamente adicionadas ao vídeo em [!UICONTROL Tags inteligentes]. O Serviço de asset compute aproveita a Adobe Sensei para criar essas tags inteligentes.

![As Tags inteligentes são adicionadas aos vídeos e vistas na guia Básica das Propriedades do ativo](assets/smart-tags-added-to-videos.png)

As tags inteligentes aplicadas são classificadas em ordem decrescente de [pontuação de confiança](#confidence-score-video-tag), combinadas para tags de objeto e ação, em [!UICONTROL Tags inteligentes].

>[!IMPORTANT]
>
>É recomendável revisar essas tags geradas automaticamente para garantir que elas estejam em conformidade com sua marca e seus valores.

## Marcação inteligente de vídeos existentes no DAM {#smart-tag-existing-videos}

Os ativos de vídeo já existentes no DAM não são marcados com tags inteligentes automaticamente. Você precisa [!UICONTROL Reprocessar Ativos] manualmente para gerar tags inteligentes para eles.

Para adicionar tags inteligentes a ativos de vídeo ou pastas (incluindo subpastas) de ativos que já existem no repositório de ativos, siga estas etapas:

1. Selecione o logotipo [!DNL Adobe Experience Manager] e, em seguida, selecione ativos na página [!UICONTROL Navegação].

1. Selecione [!UICONTROL Arquivos] para exibir a interface de Ativos.

1. Navegue até a pasta na qual deseja aplicar tags inteligentes.

1. Selecione a pasta inteira ou ativos de vídeo específicos.

1. Selecione o ícone ![Reprocessar ativos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocessar Ativos] e selecione a opção [!UICONTROL Processo Completo].

![Reprocessar ativos para adicionar tags a vídeos do repositório DAM existente](assets/reprocess.gif)

Quando o processo for concluído, navegue até a página [!UICONTROL Propriedades] de qualquer ativo de vídeo dentro da pasta. As tags adicionadas automaticamente são vistas na seção [!UICONTROL Tags inteligentes] na guia [!UICONTROL Básico]. Essas tags inteligentes aplicadas são classificadas em ordem decrescente de [pontuação de confiança](#confidence-score-video-tag).

## Procurar vídeos marcados {#search-smart-tagged-videos}

Para pesquisar os ativos de vídeo com base nas tags inteligentes geradas automaticamente, use [Omnisearch](search-assets.md#search-assets-in-aem):

1. Selecione o ícone de pesquisa ![ícone de pesquisa](assets/do-not-localize/search_icon.png) para exibir o campo Omnisearch.

1. Especifique uma tag, no campo Omnisearch, que você não adicionou explicitamente a um vídeo.

1. Pesquisar com base na tag .

Os resultados da pesquisa exibem os ativos de vídeo com base na tag especificada.

Os resultados da pesquisa são uma combinação de ativos de vídeo com palavras-chave pesquisadas nos metadados e ativos de vídeo que são marcados com as palavras-chave pesquisadas. No entanto, os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos dos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. Para obter mais informações, consulte [Entender [!DNL Experience Manager] resultados de pesquisa com tags inteligentes](smart-tags.md#understandsearch).

## Moderar tags inteligentes de vídeo {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] permite preparar as tags inteligentes para:

* remova tags imprecisas atribuídas aos vídeos de sua marca.

* refinar pesquisas baseadas em tags para vídeos, garantindo que seu vídeo apareça nos resultados da pesquisa para obter as tags mais relevantes. Portanto, elimina as chances de vídeos não relacionados aparecerem nos resultados da pesquisa.

* atribua uma classificação mais alta a uma tag para aumentar sua relevância em relação a um vídeo. A promoção de uma tag para um vídeo aumenta as chances de o vídeo aparecer nos resultados da pesquisa quando uma pesquisa é realizada com base nessa tag.

Para saber mais sobre como moderar as tags inteligentes para ativos, consulte [Gerenciar tags inteligentes](smart-tags.md#manage-smart-tags-and-searches).

![Moderar tags inteligentes de vídeo](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Quaisquer tags que são moderadas usando as etapas em [Gerenciar tags inteligentes](smart-tags.md#manage-smart-tags-and-searches) não são lembradas no reprocessamento do ativo. O conjunto original de tags é exibido novamente.

## Opt out de marcação inteligente de vídeo {#opt-out-video-smart-tagging}

Como a marcação automatizada de vídeos é executada em paralelo a outras tarefas de processamento de ativos, como criação de miniaturas e extração de metadados, pode ser demorado. Para acelerar o processamento de ativos, é possível opt out a marcação inteligente de vídeo no carregamento no nível da pasta.

Para opt out a geração automatizada de tags inteligentes de vídeo para ativos carregados para uma pasta específica:

1. Abra a guia [!UICONTROL Processamento de ativos] na pasta [!UICONTROL Propriedades].

1. No menu [!UICONTROL Tags inteligentes para vídeos], a opção [!UICONTROL Herdado] está selecionada por padrão e a tag inteligente de vídeo está ativada.

   Quando a opção [!UICONTROL Herdado] estiver selecionada, o caminho da pasta herdada também estará visível juntamente com as informações sobre se está definido para [!UICONTROL Ativar] ou [!UICONTROL Desativar].

   ![Desativar marcação inteligente de vídeo](assets/disable-video-tagging.png)

1. Selecione [!UICONTROL Desativar] para opt out a marcação inteligente de vídeos carregados na pasta.

>[!IMPORTANT]
>
>Se você tiver opt out de marcar vídeos em uma pasta no momento do upload e quiser marcar os vídeos com tags inteligentes depois do upload, em seguida, **[!UICONTROL Habilitar tags inteligentes para vídeos]** na guia [!UICONTROL Processamento de ativos] da pasta [!UICONTROL Propriedades] e usar [[!UICONTROL Reprocessar ativo] opção&lt;a8/ para adicionar tags inteligentes ao vídeo.](#smart-tag-existing-videos)

## Pontuação de confiança {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] aplica um limite mínimo de confiança para tags inteligentes de objeto e ação, a fim de evitar que haja muitas tags para cada ativo de vídeo, o que atrasa a indexação. Os resultados da pesquisa de ativos são classificados com base nas pontuações de confiança, que geralmente melhoram os resultados da pesquisa além do que uma inspeção das tags atribuídas de qualquer ativo de vídeo sugere. Tags imprecisas geralmente têm pontuações de baixa confiança, de modo que raramente aparecem na parte superior da lista de Tags inteligentes para ativos.

O limite padrão para as tags action e object em [!DNL Adobe Experience Manager] é 0,7 (deve ser um valor entre 0 e 1). Se alguns ativos de vídeo não forem marcados por uma tag específica, isso indica que o algoritmo está menos de 70% confiante nas tags previstas. O limite padrão pode não ser sempre o ideal para todos os usuários. Portanto, é possível alterar o valor da pontuação de confiança na configuração do OSGI.

Para adicionar a configuração OSGI de pontuação de confiança ao projeto implantado em [!DNL Adobe Experience Manager] como [!DNL Cloud Service] até [!DNL Cloud Manager]:

* No projeto [!DNL Adobe Experience Manager] (`ui.config` desde o Archetype 24, ou anteriormente `ui.apps`) da configuração `config.author` OSGi, inclua um arquivo de configuração chamado `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` com o seguinte conteúdo:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>As tags manuais recebem uma confiança de 100% (confiança máxima). Portanto, se houver ativos de vídeo com tags manuais que correspondam ao query de pesquisa, eles serão exibidos antes das tags inteligentes correspondentes ao query de pesquisa.

## Limitações           {#video-smart-tagging-limitations}

* Ainda não há suporte para o treinamento do Serviço de tags inteligentes (ou Tags inteligentes aprimoradas) para marcar seus ativos de vídeo.

* O progresso da marcação não é mostrado.

* Somente os vídeos de tamanho não superior a 300 MB são adequados para marcação. O serviço da Adobe Sensei marca os vídeos que atendem a esses critérios e ignora a marcação de outros vídeos em uma pasta.

* Somente os vídeos nesses formatos de arquivo (e os codecs suportados) — MP4 (H264/AVC), MKV (H264/AVC), MOV (H264/AVC, Motion JPEG), AVI (indeo4), FLV (H264/AVC, vp6f) e WMV (WMV2)—pode ser marcado.

>[!MORELIKETHIS]
>
>* [Gerenciar tags inteligentes e pesquisas de ativos](smart-tags.md#manage-smart-tags-and-searches)
>* [Treinar o serviço Smart Tag e marcar suas imagens](smart-tags.md)

