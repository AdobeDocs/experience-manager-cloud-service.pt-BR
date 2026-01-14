---
title: Insira tags inteligentes em seus ativos de vídeo
description: O Experience Manager adiciona automaticamente Tags inteligentes contextuais e descritivas a vídeos usando o [!DNL Adobe AI].
feature: Smart Tags,Tagging
role: Admin,User
exl-id: 87d0eea2-83a1-4cfa-a4a5-425d0e8abba6
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---

# Insira tags inteligentes em seus ativos de vídeo {#video-smart-tags}

A necessidade cada vez maior de novos conteúdos exige a redução dos esforços manuais para oferecer experiências digitais atraentes rapidamente. O [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] oferece suporte à marcação automática de ativos de vídeo usando inteligência artificial. Marcar os vídeos manualmente pode ser demorado. No entanto, o recurso de marcação inteligente de vídeo [!DNL Adobe AI] usa modelos de inteligência artificial para analisar conteúdo de vídeo e adicionar tags aos ativos de vídeo. Dessa forma, reduz o tempo para que os usuários do DAM forneçam experiências avançadas aos clientes. O serviço de aprendizado de máquina da Adobe gera dois conjuntos de tags para um vídeo. Enquanto, um conjunto corresponde a objetos, cenas e atributos naquele vídeo; o outro conjunto relaciona-se a ações como beber, correr e correr.

A marcação de vídeo está habilitada por padrão no [!DNL Adobe Experience Manager] como um [!DNL Cloud Service]. No entanto, você pode [recusar a marcação inteligente de vídeo](#opt-out-video-smart-tagging) em uma pasta. Os vídeos são marcados automaticamente quando você carrega novos vídeos ou reprocessa os existentes. [!DNL Experience Manager] também cria as miniaturas e extrai metadados dos arquivos de vídeo. As marcas inteligentes são exibidas em ordem decrescente de sua [pontuação de confiança](#confidence-score-video-tag) no ativo [!UICONTROL Propriedades].

## Marcação inteligente de vídeos no upload {#smart-tag-assets-on-ingestion}

Quando você [carrega ativos de vídeo](add-assets.md#upload-assets) para [!DNL Adobe Experience Manager] como [!DNL Cloud Service], os vídeos são processados. Após concluir o processamento, consulte a guia [!UICONTROL Básico] da página [!UICONTROL Propriedades] do ativo. As tags inteligentes são adicionadas automaticamente ao vídeo em [!UICONTROL Tags inteligentes]. Os microsserviços de ativos usam o [!DNL Adobe AI] para criar essas tags inteligentes.

![As Tags inteligentes são adicionadas aos vídeos e visualizadas na guia Básico das Propriedades do ativo](assets/smart-tags-added-to-videos.png)

As marcas inteligentes aplicadas são classificadas em ordem decrescente de [pontuação de confiança](#confidence-score-video-tag), combinadas para marcas de objeto e ação, em [!UICONTROL Marcas inteligentes].

>[!IMPORTANT]
>
>É recomendável revisar essas tags geradas automaticamente para garantir que estejam em conformidade com sua marca e seus valores.

## Marcação inteligente de vídeos existentes no DAM {#smart-tag-existing-videos}

Os ativos de vídeo já existentes no DAM não são marcados automaticamente com tags inteligentes. Você precisa [!UICONTROL Reprocessar o Assets] manualmente para gerar marcas inteligentes para eles.

Para marcar ativos de vídeo ou pastas (incluindo subpastas) de ativos que já existem no repositório de ativos, siga estas etapas:

1. Selecione o logotipo [!DNL Adobe Experience Manager] e selecione os ativos da página [!UICONTROL Navegação].

1. Selecione [!UICONTROL Arquivos] para exibir a interface do Assets.

1. Navegue até a pasta à qual deseja aplicar as tags inteligentes.

1. Selecione a pasta inteira ou ativos de vídeo específicos.

1. Selecione o ícone ![Reprocessar ativos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocessar Assets] e selecione a opção [!UICONTROL Processo completo].

<!-- TBD: Limit size -->

![Reprocessar ativos para adicionar marcas a vídeos no repositório DAM existente](assets/reprocess.gif)

Quando o processo for concluído, navegue até a página [!UICONTROL Propriedades] de qualquer ativo de vídeo que esteja na pasta. As marcas adicionadas automaticamente são vistas na seção [!UICONTROL Tags inteligentes] da guia [!UICONTROL Básico]. Essas marcas inteligentes aplicadas são classificadas em ordem decrescente de [pontuação de confiança](#confidence-score-video-tag).

## Pesquisar vídeos marcados {#search-smart-tagged-videos}

Para pesquisar os ativos de vídeo com base nas tags inteligentes geradas automaticamente, use o [Omnisearch](search-assets.md#search-assets-in-aem):

1. Selecione o ícone de pesquisa ![ícone de pesquisa](assets/do-not-localize/search_icon.png) para exibir o campo Omnisearch.

1. Especifique uma tag, no campo Omnisearch, que você não adicionou explicitamente a um vídeo.

1. Pesquise com base na tag.

Os resultados da pesquisa exibem os ativos de vídeo com base na tag especificada.

Os resultados da pesquisa são uma combinação de ativos de vídeo com palavras-chave pesquisadas nos metadados e os ativos de vídeo marcados de forma inteligente com as palavras-chave pesquisadas. No entanto, os resultados da pesquisa que correspondem a todos os termos de pesquisa em campos de metadados são exibidos primeiro, seguido pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. Para obter mais informações, consulte [Entender [!DNL Experience Manager] os resultados da pesquisa com marcas inteligentes](smart-tags.md#understand-search).

## Tags inteligentes de vídeo moderadas {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] permite preparar as marcas inteligentes para:

* remova as tags imprecisas atribuídas aos vídeos da sua marca.

* refine as pesquisas por vídeos com base em tags, garantindo que o vídeo seja exibido nos resultados da pesquisa para as tags mais relevantes. Portanto, elimina as chances de vídeos não relacionados aparecerem nos resultados de pesquisa.

* atribua uma classificação mais alta a uma tag para aumentar sua relevância com relação a um vídeo. Promover uma tag para um vídeo aumenta as chances do vídeo aparecer nos resultados da pesquisa quando uma pesquisa é realizada com base nessa tag.

Para saber mais sobre como moderar as marcas inteligentes para ativos, consulte [Gerenciar marcas inteligentes](smart-tags.md#manage-smart-tags-and-searches).

![Moderar marcas inteligentes de vídeo](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>As marcas moderadas usando as etapas em [Gerenciar marcas inteligentes](smart-tags.md#manage-smart-tags-and-searches) não são lembradas no reprocessamento do ativo. O conjunto original de tags é exibido novamente.

## Recusar marcação inteligente de vídeo {#opt-out-video-smart-tagging}

Como a marcação automática de vídeos é executada em paralelo a outras tarefas de processamento de ativos, como criação de miniaturas e extração de metadados, pode ser demorada. Para acelerar o processamento de ativos, você pode recusar a marcação inteligente de vídeo ao fazer upload no nível da pasta.

Para recusar a geração de tags inteligentes de vídeo automatizadas para ativos carregados em uma pasta específica:

1. Abra a guia [!UICONTROL Processamento de ativos] na pasta [!UICONTROL Propriedades].

1. No menu [!UICONTROL Marcas Inteligentes para Vídeos], a opção [!UICONTROL Herdada] é selecionada por padrão e a marca inteligente de vídeo é habilitada.

   Quando a opção [!UICONTROL Herdado] está selecionada, o caminho de pasta herdado também fica visível, juntamente com as informações se ele está definido como [!UICONTROL Habilitar] ou [!UICONTROL Desabilitar].

   ![Desabilitar marcação inteligente de vídeo](assets/disable-video-tagging.png)

1. Selecione [!UICONTROL Desabilitar] para recusar a marcação inteligente de vídeos carregados na pasta.

>[!IMPORTANT]
>
>Se você recusou a marcação de vídeos em uma pasta no momento do carregamento e deseja marcar os vídeos com uma tag inteligente após o carregamento, **[!UICONTROL Habilite as Tags inteligentes para Vídeos]** na guia [!UICONTROL Processamento de ativos] da pasta [!UICONTROL Propriedades] e use a opção [[!UICONTROL Reprocessar ativos]](#smart-tag-existing-videos) para adicionar tags inteligentes ao vídeo.

## Pontuação de confiança {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] aplica um limite mínimo de confiança para marcas inteligentes de objeto e ação para evitar ter muitas marcas para cada ativo de vídeo, o que atrasa a indexação. Os resultados da pesquisa de ativos são classificados com base nas pontuações de confiança, que geralmente melhoram os resultados da pesquisa além do que uma inspeção das tags atribuídas de qualquer ativo de vídeo sugere. Tags imprecisas geralmente têm pontuações de confiança baixas, de modo que raramente são exibidas na parte superior da lista de Tags inteligentes para ativos.

O limite padrão para marcas de ação e objeto em [!DNL Adobe Experience Manager] é 0,7 (deve ser um valor entre 0 e 1). Se alguns ativos de vídeo não forem marcados por uma tag específica, isso indica que o algoritmo tem menos de 70% de confiança nas tags previstas. O limite padrão nem sempre pode ser o ideal para todos os usuários. Portanto, você pode alterar o valor da pontuação de confiança na configuração do OSGI.

Para adicionar a configuração OSGI da pontuação de confiança ao projeto implantado em [!DNL Adobe Experience Manager] como um [!DNL Cloud Service] até [!DNL Cloud Manager]:

* No projeto [!DNL Adobe Experience Manager] (`ui.config` desde o Arquétipo 24, ou anteriormente `ui.apps`) a configuração OSGi `config.author`, inclua um arquivo de configuração chamado `com.adobe.cq.assetcompute.impl.aisdk.AISdkImpl.cfg.json` com o seguinte conteúdo:

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

* Não é possível treinar o serviço que aplica Tags inteligentes a vídeos usando vídeos específicos. Funciona com as configurações padrão [!DNL Adobe AI].

* O progresso da marcação não é exibido.

* Somente os vídeos com tamanho menor que 300 MB são marcados automaticamente. O serviço [!DNL Adobe AI] ignora arquivos de vídeo maiores.

* Somente os vídeos nos formatos de arquivo e codecs suportados mencionados em [Tags inteligentes](/help/assets/smart-tags.md#smart-tags-supported-file-formats) são marcados.

>[!MORELIKETHIS]
>
>* [Gerenciar tags inteligentes e pesquisas de ativos](smart-tags.md#manage-smart-tags-and-searches)
>* [Treine o serviço de Marca Inteligente e marque suas imagens](smart-tags.md)
