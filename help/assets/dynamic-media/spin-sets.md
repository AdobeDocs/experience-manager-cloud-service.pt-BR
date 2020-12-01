---
title: Conjuntos de rotação
description: Saiba como trabalhar com conjuntos de rotação no Dynamic Media
translation-type: tm+mt
source-git-commit: 7a1d12a8cff03af660b936bb7d8b045532357f0d
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 12%

---


# Conjuntos de rotação{#spin-sets}

Um Conjunto de rotação simula o ato real de girar um objeto para examiná-lo. Os Conjuntos de rotação possibilitam a visualização de itens de qualquer ângulo, obtendo os detalhes visuais principais de qualquer ângulo.

Um conjunto de rotação simula uma experiência de visualização de 360 graus. O Dynamic Media oferta Conjuntos de rotação de eixo único nos quais os visualizadores podem girar um item. Além disso, os usuários podem aplicar zoom e deslocar qualquer uma das visualizações com apenas alguns cliques do mouse. Dessa forma, os usuários podem examinar um item mais detalhadamente de um ponto de vista específico.

Os Conjuntos de rotação são designados por um banner com a palavra **[!UICONTROL SPINSET]**. Além disso, se o Conjunto de rotação for publicado, a data de publicação, indicada pelo ícone **[!UICONTROL Mundo]**, estará no banner juntamente com a última data de modificação, indicada pelo ícone **[!UICONTROL Lápis]** é exibido.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Para obter informações sobre a interface de usuário do Assets, consulte [Gerenciar ativos com a interface de usuário de toque](/help/assets/manage-digital-assets.md) e aplique-os a uma nova pasta na qual os ativos do conjunto de imagens serão carregados.

## Start rápido: Conjuntos de rotação {#quick-start-spin-sets}

Para colocar você em funcionamento rapidamente com Conjuntos de rotação, siga estas etapas:

1. Opcional. [Crie uma predefinição de conjunto de lotes ](/help/assets/dynamic-media/batch-set-presets-dm.md) e aplique-a a uma nova pasta de ativos.

   Uma predefinição de conjunto de lotes pode ajudar a automatizar a criação do conjunto de rotação.

   >[!IMPORTANT]
   >
   >Os conjuntos de lotes são criados pelo IPS (Image Production System) como parte da ingestão de ativos.

1. [Carregue suas imagens para várias visualizações.](#uploading-assets-for-spin-sets)

   No mínimo, você precisa de 8 a 12 fotos de um item para um Conjunto de rotação unidimensional e 16 a 24 para um Conjunto de rotação bidimensional. As fotos devem ser tiradas a intervalos regulares para dar a impressão de que o item está girando e sendo virado. Por exemplo, se um Conjunto de rotação unidimensional incluir 12 fotos, gire o item 30 graus (360/12) para cada tomada.

1. [Criar Conjuntos de rotação.](#creating-spin-sets)

   Para criar um Conjunto de rotação, selecione **[!UICONTROL Criar > Conjunto de rotação]** e nomeie o conjunto, escolha os ativos e escolha a ordem em que as imagens serão exibidas.

   Consulte [Trabalhando com seletores](/help/assets/dynamic-media/working-with-selectors.md).

1. Configure [predefinições do visualizador do Spin Set](/help/assets/dynamic-media/managing-viewer-presets.md), conforme necessário.

   Os administradores podem criar ou modificar as Predefinições do visualizador de conjunto de rotação. Para ver seu conjunto de rotação com uma predefinição do visualizador, selecione o conjunto de rotação e, no menu suspenso do painel à esquerda, selecione **Visualizadores**.

   Consulte **[!UICONTROL Ferramentas > Ativos > Predefinições do visualizador]** para criar ou editar predefinições do visualizador.

   Consulte [Adicionar e editar predefinições do visualizador.](/help/assets/dynamic-media/managing-viewer-presets.md)

   Você pode visualização e acessar conjuntos criados por meio de predefinições de conjuntos de lotes de três maneiras diferentes. (Os conjuntos criados usando predefinições de conjuntos de lotes, do *not* aparecem na interface do usuário.)

1. [Conjuntos de rotação de pré-visualização.](/help/assets/dynamic-media/previewing-assets.md)

   Selecione o Conjunto de rotação e você pode pré-visualização-lo. Gire o conjunto de rotação. Você pode escolher visualizadores diferentes no menu **[!UICONTROL Visualizadores]**, disponível no menu suspenso do painel esquerdo.

1. [Publicar Conjuntos de rotação.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   A publicação de um conjunto de rotação ativa o URL e a string Incorporada. Além disso, você deve [publicar a predefinição do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

1. [Vincule URLs ao seu ](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) aplicativo da Web ou  [Incorpore o visualizador](/help/assets/dynamic-media/embed-code.md) de vídeo ou imagem.

   A AEM Assets cria chamadas de URL para Conjuntos de rotação e as ativa depois que você publica os conjuntos de rotação. Você pode copiar esses URLs ao pré-visualização de ativos. Como alternativa, você pode incorporá-los ao seu site.

   Selecione o Conjunto de rotação e, no menu suspenso do painel à esquerda, selecione **[!UICONTROL Visualizadores]**.

   Consulte [Vincular um conjunto de rotação a uma página da Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incorporar o visualizador de vídeo ou imagem](/help/assets/dynamic-media/embed-code.md).

Se necessário, você pode [editar Conjuntos de rotação](#editing-spin-sets). Além disso, você pode visualização e modificar [as propriedades do Spin Set](/help/assets/manage-digital-assets.md#editing-properties).

## Fazer upload de ativos para conjuntos de rotação {#uploading-assets-for-spin-sets}

No mínimo, você precisa de 8 a 12 fotos de um item para um Conjunto de rotação unidimensional e 16 a 24 para um Conjunto de rotação bidimensional. As fotos devem ser tiradas a intervalos regulares para dar a impressão de que o item está girando e sendo virado. Por exemplo, se um Conjunto de rotação unidimensional incluir 12 fotos, gire o item 30 graus (360/12) para cada tomada.

Você pode fazer upload de imagens para os Conjuntos de rotação da mesma maneira que faria [fazer upload de qualquer outro ativo no AEM Assets](/help/assets/manage-digital-assets.md).

### Diretrizes para capturar imagens para seu Conjunto de rotação {#guidelines-for-shooting-spin-set-images}

Veja a seguir algumas práticas recomendadas para imagens de conjunto de rotação. Em geral, quanto mais imagens você tiver em um Conjunto de rotação, melhor será o efeito de rotação da imagem. No entanto, a inclusão de muitas imagens no conjunto também aumenta a quantidade de tempo necessário para carregar as imagens. AEM recomenda estas diretrizes para fotografar imagens para uso em Conjuntos de rotação:

* No mínimo, use 8 a 12 imagens em um conjunto de rotação unidimensional e 16 a 24 imagens em um conjunto de rotação bidimensional. É necessário um mínimo de 8 imagens para rodar 360 graus. Conjuntos de rotação unidimensionais são mais comuns, pois a criação de Conjuntos de rotação bidimensionais exige muita mão de obra.
* Usar um formato sem perdas; TIFF e PNG são recomendados.
* Mascarar todas as imagens para que o item apareça em um fundo branco puro ou em outro plano de alto contraste. Como opção, adicione sombras.
* Verifique se os detalhes do produto estão bem iluminados e em foco.
* Leve imagens de rotação para roupas de moda com um manequim ou modelo. Muitas vezes o manequim é completamente mascarado (utilizando um manequim de vidro) ou na imagem é apresentado um manequim/forma estilizada. É possível criar um conjunto de rotação no modelo definindo o número de ângulos. Marque cada ângulo com uma fita no chão para guiar o modelo a pisar e olhe na direção de cada tomada.

## Criação de Conjuntos de rotação {#creating-spin-sets}

Esta seção descreve como criar Conjuntos de rotação.

>[!NOTE]
>
>Também é possível criar conjuntos de rotação automaticamente por meio de [predefinições de conjuntos em lotes](/help/assets/dynamic-media/config-dm.md). **Importante:** os conjuntos em lotes são criados pelo IPS (Sistema de produção de imagem) como parte da ingestão de ativos.
>
>Consulte &quot;Criando predefinições de conjuntos de lotes para gerar automaticamente Conjuntos de imagens e Conjuntos de rotação&quot; em [Configurando Mídia dinâmica](/help/assets/dynamic-media/config-dm.md).

>[!NOTE]
>
>A ordem em que as imagens aparecem em um conjunto de rotação é importante. Certifique-se de ordená-los de modo que a rotação seja uma visualização suave de 360 graus.

**Para criar Conjuntos de rotação**

1. No Assets, navegue até o local em que deseja criar um conjunto de rotação, clique em **[!UICONTROL Criar]** e selecione **[!UICONTROL Conjunto de rotação]**. Além disso, crie o conjunto de dentro de uma pasta que contenha seus ativos. O Editor de conjunto de rotação é exibido.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. No Editor de conjunto de rotação, no campo **[!UICONTROL Title]**, digite um nome para o conjunto de rotação. O nome aparece no banner no Conjunto de rotação. Opcionalmente, informe uma descrição.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >Ao criar o conjunto de rotação, você pode alterar a miniatura do conjunto de rotação ou permitir que AEM selecione a miniatura automaticamente com base nos ativos no conjunto de rotação. Para selecionar uma miniatura, clique em **[!UICONTROL Alterar miniatura]** e selecione qualquer imagem (você também pode navegar para outras pastas para localizar imagens). Se você tiver selecionado uma miniatura e decidir que deseja AEM gerar uma do conjunto de rotação, selecione **[!UICONTROL Alternar para miniatura automática]**.

1. Execute um dos procedimentos a seguir:

   * Perto do canto superior esquerdo da página do Editor de conjunto de rotação, toque em **[!UICONTROL Adicionar ativo]**.

   * Próximo ao meio da página do Editor de conjunto de rotação, toque em **[!UICONTROL Toque para abrir o Seletor de ativos]**.
   Toque em para selecionar ativos que deseja incluir no Conjunto de rotação. Os ativos selecionados têm um ícone de marca de seleção sobre eles. Quando terminar, próximo ao canto superior direito da página, toque em **[!UICONTROL Selecionar]**.

   Com o Seletor de ativos, procure por ativos ao digitar uma palavra-chave e tocar em **[!UICONTROL Retornar]**. Aplique filtros para refinar os resultados da pesquisa. Filtre por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e toque no ícone **[!UICONTROL Filtro]**, na barra de ferramentas. Altere a exibição ao tocar no ícone Exibir e selecionar **[!UICONTROL Exibição em coluna]**, **[!UICONTROL Exibição de cartão]** ou **[!UICONTROL Exibição em lista]**.

   Consulte [Trabalhando com seletores](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Quando você adiciona ativos ao seu conjunto, eles são adicionados automaticamente em ordem alfanumérica. Você pode reordenar ou classificar manualmente os ativos depois de adicioná-los.

   Se necessário, arraste o ícone Reordenar de um ativo à direita do nome do arquivo do ativo para reordenar as imagens para cima ou para baixo na lista definida.

   ![Reorganização do quadro 11 no conjunto de rotação arrastando-o para um novo local.](assets/6_5_spinset-reorderassets.png)

   Reorganização do quadro 11 no conjunto de rotação arrastando-o para um novo local.

1. (Opcional) Execute um dos procedimentos a seguir:

   * Para excluir uma imagem, selecione-a e toque em **[!UICONTROL Excluir ativo]**.

   * Para aplicar uma predefinição, próximo ao canto superior direito da página, toque em **[!UICONTROL Predefinir]** e selecione uma predefinição para aplicar a todos os ativos ao mesmo tempo.

1. Clique em **[!UICONTROL Salvar]**. Seu Spin Set recém-criado é exibido na pasta em que você o criou.

## Exibindo Conjuntos de rotação {#viewing-spin-sets}

Você pode criar conjuntos de rotação na interface do usuário ou automaticamente usando [predefinições de conjuntos de lotes](/help/assets/dynamic-media/config-dm.md). No entanto, os conjuntos criados usando predefinições de conjuntos de lotes, faça com que *not* apareçam na interface do usuário. É possível acessar conjuntos criados por meio de predefinições de conjuntos de lotes de três maneiras diferentes. (Esses métodos estão disponíveis mesmo se você tiver criado os conjuntos de rotação na interface do usuário).

>[!NOTE]
>
>Você também pode visualização conjuntos por meio da interface do usuário, conforme descrito em [Editando Conjuntos de rotação](#editing-spin-sets).

**Para Conjuntos de rotação de visualização**

1. Ao abrir as propriedades de um ativo individual. As propriedades indicam os conjuntos dos quais o ativo selecionado é membro (em **[!UICONTROL Membro dos conjuntos]**). Clique no nome do conjunto para ver o conjunto inteiro.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. A partir de uma imagem de membro de qualquer conjunto. Selecione o menu **[!UICONTROL Conjuntos]** para exibir os conjuntos dos quais o ativo é membro.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. Na pesquisa, você pode selecionar **[!UICONTROL Filtros]**, expandir o **[!UICONTROL Dynamic Media]** e selecionar **[!UICONTROL Conjuntos]**.

   A pesquisa retorna conjuntos correspondentes que foram criados manualmente na interface do usuário ou criados automaticamente por meio de predefinições de conjuntos de lotes. Para conjuntos automatizados, o query de pesquisa é realizado usando `Starts with` critérios de pesquisa diferentes AEM pesquisa que se baseia no uso de `Contains` critérios de pesquisa. Definir o filtro como **[!UICONTROL Conjuntos]** é a única maneira de pesquisar conjuntos automatizados.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## Edição de conjuntos de rotação {#editing-spin-sets}

É possível executar várias tarefas de edição em Conjuntos de rotação, como:

* Adicione imagens ao conjunto de rotação.
* Reordene as imagens no Conjunto de rotação.
* Exclua ativos no Conjunto de rotação.
* Aplicar predefinições do visualizador.
* Exclua o conjunto de rotação.

**Para editar um conjunto de giros**

1. Execute um dos procedimentos a seguir:

   * Passe o mouse sobre um ativo do Conjunto de rotação e, em seguida, toque em **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o cursor do mouse sobre um ativo do Conjunto de rotação, toque em **[!UICONTROL Selecionar]** (ícone de marca de seleção) e, em seguida, toque em **[!UICONTROL Editar]** na barra de ferramentas.

   * Toque em um ativo do Conjunto de rotação e, em seguida, toque em **[!UICONTROL Editar]** (ícone de lápis) na barra de ferramentas.

1. Para editar o Conjunto de rotação, execute um dos procedimentos a seguir:

   * Para reordenar imagens, arraste uma imagem para um novo local (selecione o ícone de reordenação para mover itens).
   * Para classificar itens em ordem crescente ou decrescente, clique no cabeçalho da coluna.
   * Para adicionar um ativo ou atualizar um ativo existente, clique em **[!UICONTROL Adicionar ativo]**. Navegue até um ativo, selecione-o e, em seguida, toque em **[!UICONTROL Selecionar]** próximo ao canto superior direito.
Se você excluir a imagem que AEM usa para a miniatura substituindo-a por outra imagem, o ativo original ainda será exibido.
   * Para excluir um ativo, selecione-o e clique ou toque em **[!UICONTROL Excluir ativo]**.
   * Para aplicar uma predefinição, toque ou clique no ícone Predefinir e selecione uma predefinição.
   * Para excluir um conjunto de rotação inteiro, navegue até o conjunto de rotação, selecione-o e selecione **[!UICONTROL Excluir]**

   >[!NOTE]
   >
   >Você pode editar as imagens em um Conjunto de rotação navegando até o conjunto, tocar em **[!UICONTROL Definir membros]** no painel esquerdo e tocar no ícone Lápis em um ativo individual para abrir a janela de edição.

1. Clique em **[!UICONTROL Salvar]** ao concluir a edição.

## Visualizando conjuntos de rotação {#previewing-spin-sets}

Consulte [Visualizar ativos](/help/assets/dynamic-media/previewing-assets.md).

## Publicar conjuntos de rotação {#publishing-spin-sets}

Consulte [Publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).