---
title: Conjuntos de mídia mista
description: Saiba como trabalhar com conjuntos de mídia mista no Dynamic Media.
feature: Conjuntos de mídia mista
role: User
exl-id: 7ccde741-38d2-44c9-9378-f2721384aab7
source-git-commit: aba8896e304619fe7e73d61b52b83da40766477a
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 14%

---

# Conjuntos de mídia mista{#mixed-media-sets}

Os Conjuntos de mídias mistas permitem que você forneça uma combinação de imagens, Conjuntos de imagens, Conjuntos de rotação e vídeos em uma apresentação.

Os Conjuntos de mídias mistas são designados por um banner com a palavra **[!UICONTROL MixedMediaSet]**. Além disso, se o Conjunto de mídias mistas for publicado, a data de publicação, indicada pelo ícone **[!UICONTROL Mundo]**, estará no banner junto com a última data de modificação, indicada pelo ícone **[!UICONTROL Lápis]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Para obter informações sobre a interface do usuário do Assets, consulte [Gerenciar ativos com a interface de toque](/help/assets/manage-digital-assets.md).

## Início rápido: Conjuntos de mídia mista {#quick-start-mixed-media-sets}

Para ativar e executar rapidamente com Conjuntos de mídias mistas, siga estas etapas:

1. [Faça upload dos ativos](#uploading-assets).

   Comece carregando as imagens e os vídeos dos Conjuntos de mídias mistas. Se necessário, crie seus [Conjuntos de imagens](/help/assets/dynamic-media/image-sets.md) e [Conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md). Como os usuários podem ampliar imagens no Visualizador de conjunto de mídias mistas, verifique se você considera o zoom ao escolher imagens. Certifique-se de que as imagens tenham pelo menos 2000 pixels no tamanho maior.

1. [Criar conjuntos de mídia mista](#creating-mixed-media-sets).

   Para criar um Conjunto de mídias mistas, na página Ativos, vá para **[!UICONTROL Criar]** > **[!UICONTROL Conjunto de mídias mistas]** e nomeie o conjunto, escolha os ativos e escolha a ordem em que as imagens serão exibidas.

   Consulte [Trabalhar com seletores](/help/assets/dynamic-media/working-with-selectors.md).

1. Configure [Mixed Media Viewer presets](/help/assets/dynamic-media/managing-viewer-presets.md), conforme necessário.

   Os administradores podem criar ou modificar as Predefinições do visualizador de conjunto de mídia mista. Para ver sua mídia mista com uma predefinição do visualizador, selecione o conjunto de mídias mistas e, no menu suspenso do painel à esquerda, selecione **[!UICONTROL Visualizadores]**.

   Para criar ou editar predefinições do visualizador, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições do visualizador]**.

   Consulte [Adicionar e editar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

1. [Visualizar conjuntos de mídia mista](#previewing-mixed-media-sets).

   Selecione o Conjunto de mídias mistas e você pode visualizá-lo. Para examinar seu Conjunto de mídias mistas no Visualizador selecionado, selecione os ícones de miniatura. Você pode escolher visualizadores diferentes do menu **[!UICONTROL Visualizadores]**, disponível no menu suspenso do painel à esquerda.

1. [Publicar conjuntos de mídia mista](#publishing-mixed-media-sets).

   A publicação de um Conjunto de mídias mistas ativa o URL e a cadeia de caracteres de inserção. Além disso, você deve [publicar a predefinição do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

1. [Vincule URLs ao seu ](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) aplicativo web ou  [Incorpore o visualizador](/help/assets/dynamic-media/embed-code.md) de vídeo ou imagem.

   O Adobe Experience Manager Assets cria chamadas de URL para Conjuntos de mídia mista e as ativa após publicar os conjuntos de mídia mista. Você pode copiar esses URLs ao visualizar ativos. Como alternativa, você pode incorporá-los ao seu site.

   Selecione o Conjunto de mídias mistas e, no menu suspenso do painel à esquerda, selecione **[!UICONTROL Visualizadores]**.

   Consulte [Vincular um conjunto de mídias mistas a uma página da Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incorporar o visualizador de vídeo ou imagem](/help/assets/dynamic-media/embed-code.md).

Se necessário, você pode editar [Conjuntos de mídias mistas](#editing-mixed-media-sets). Além disso, você pode exibir e modificar [as propriedades do Conjunto de mídias mistas](/help/assets/manage-digital-assets.md#editing-properties).

>[!NOTE]
>
>Se tiver problemas ao criar conjuntos, consulte [Solucionar problemas do Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).

## Fazer upload de ativos {#uploading-assets}

Comece carregando as imagens e os vídeos dos Conjuntos de mídias mistas. Lembre-se de que os usuários podem ampliar imagens no Visualizador de conjunto de mídias mistas. Assim, escolha imagens com essa capacidade de zoom em mente. Certifique-se de que as imagens tenham pelo menos 2000 pixels no tamanho maior.

Além disso, se você quiser adicionar conjuntos de rotação ou conjuntos de imagens ao conjunto de mídia mista, crie-os também.

## Criar conjuntos de mídia mista {#creating-mixed-media-sets}

Você pode adicionar imagens, conjuntos de imagens, conjuntos de rotação e vídeos ao seu conjunto de mídias mistas. Verifique se os arquivos, os conjuntos de imagens e os conjuntos de rotação estão prontos para publicação antes de adicioná-los ao Conjunto de mídias mistas.

Ao adicionar ativos ao seu conjunto, eles são automaticamente adicionados em ordem alfanumérica. Você pode reorganizar ou classificar ativos manualmente após sua adição.

**Para criar Conjuntos de mídias mistas:**

1. No Assets, navegue até o local em que deseja criar um conjunto de mídia mista, selecione **[!UICONTROL Criar]** e selecione **[!UICONTROL Conjunto de mídias mistas]**. Além disso, crie o conjunto de dentro de uma pasta que contenha seus ativos. O Editor do conjunto de mídias mistas é exibido.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. No Editor do conjunto de mídias mistas, em **[!UICONTROL Title]**, digite um nome para o conjunto de mídias mistas. O nome aparece no banner através do Conjunto de mídias mistas. Opcionalmente, informe uma descrição.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Ao criar o conjunto de mídias mistas, você pode alterar a miniatura do conjunto de mídias mistas ou permitir que o Experience Manager selecione a miniatura automaticamente com base nos ativos no conjunto de mídias mistas. Para selecionar uma miniatura, selecione **[!UICONTROL Change thumbnail]** e selecione qualquer imagem (você também pode navegar para outras pastas para localizar imagens). Se tiver selecionado uma miniatura e decidir que deseja que o Experience Manager gere uma a partir do conjunto de mídias mistas, selecione **[!UICONTROL Alternar para a miniatura automática]**.

1. Para selecionar ativos que deseja incluir no Conjunto de mídias mistas, selecione o Seletor de ativos. Selecione-os e selecione **[!UICONTROL Select]**.

   Com o Seletor de ativos, procure por ativos ao digitar uma palavra-chave e selecionar **[!UICONTROL Retornar]**. Aplique filtros para refinar os resultados da pesquisa. Filtre por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e selecione o ícone **[!UICONTROL Filter]** na barra de ferramentas. Altere a exibição ao clicar no ícone **[!UICONTROL Exibição]** e selecionar **[!UICONTROL Exibição em lista]**, **[!UICONTROL Exibição em coluna]** ou **[!UICONTROL Exibição de cartão]**.

   Consulte [Trabalhar com seletores](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. Reorganize os ativos arrastando-os para cima ou para baixo na lista (deve selecionar o ícone **[!UICONTROL Reorder]**), conforme necessário.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Se desejar adicionar miniaturas, selecione o ícone **+** **[!UICONTROL miniatura]** ao lado da imagem e navegue até a miniatura desejada. Quando terminar de selecionar todas as imagens em miniatura, selecione **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Se desejar adicionar ativos, selecione **[!UICONTROL Adicionar ativo]**.

1. Para excluir um ativo, marque a caixa de seleção correspondente e selecione **[!UICONTROL Excluir ativo]**.
1. Para aplicar uma predefinição, selecione **[!UICONTROL Predefinição]** no canto superior direito e selecione uma predefinição para aplicar aos ativos.
1. Selecione **[!UICONTROL Salvar]**. O Conjunto de mídias mistas recém-criado é exibido na pasta em que você o criou.

## Editar conjuntos de mídia mista {#editing-mixed-media-sets}

Você pode executar várias tarefas de edição em ativos em Conjuntos de mídias mistas diretamente na interface do usuário [da mesma forma que faria com qualquer ativo em Ativos](/help/assets/manage-digital-assets.md). Você também pode executar as seguintes ações em Conjuntos de mídias mistas:

* Adicione ativos ao Conjunto de mídias mistas.
* Reordenar ativos no Conjunto de mídias mistas.
* Exclua ativos no Conjunto de mídias mistas.
* Aplicar predefinições do visualizador.
* Altere a miniatura padrão.

**Para editar Conjuntos de mídias mistas:**

1. Siga um destes procedimentos:

   * Passe o mouse sobre um ativo Conjunto de mídias mistas e selecione **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o mouse sobre um ativo de Conjunto de mídias mistas, selecione **[!UICONTROL Selecionar]** (ícone de marca de seleção) e selecione **[!UICONTROL Editar]** na barra de ferramentas.

   * Selecione um ativo Conjunto de mídias mistas e depois selecione **[!UICONTROL Editar]** (ícone de lápis) na barra de ferramentas.

1. No Editor do conjunto de mídias mistas, siga um destes procedimentos:

   * Para reorganizar ativos - No painel esquerdo, selecione **[!UICONTROL Assets]** (ícone de imagem), arraste um ativo para um novo local.
   * Para adicionar ativos - Na barra de ferramentas, selecione **[!UICONTROL Adicionar ativo]**. Navegue até os ativos. Para cada ativo que deseja adicionar, passe o mouse sobre a imagem do ativo (não o nome do ativo) e selecione o ícone de marca de seleção. No canto superior direito, selecione **[!UICONTROL Selecionar]**.

   * Para excluir um ativo - No painel esquerdo, selecione **[!UICONTROL Assets]** (ícone de imagem) e selecione o ativo. Na barra de ferramentas, selecione **[!UICONTROL Excluir ativo]**.

   * Para classificar ativos pelo nome em ordem crescente ou decrescente, no painel esquerdo, selecione **[!UICONTROL Assets]** (ícone de imagem). À direita do cabeçalho **[!UICONTROL Assets]**, selecione os ícones de cursor para cima ou para baixo.

      >[!NOTE]
      >
      >* Para excluir um Conjunto de mídias mistas inteiro, a partir de qualquer modo de exibição (como **[!UICONTROL Exibição de cartão]** ou **[!UICONTROL Exibição em coluna]**), navegue até o Conjunto de mídias mistas. Passe o mouse sobre o ativo e selecione o ícone de marca de seleção para selecioná-lo. Pressione **[!UICONTROL Backspace]** no teclado ou selecione **[!UICONTROL Mais]** (três pontos) na barra de ferramentas e selecione **[!UICONTROL Excluir]**.
         >
         >
      * Edite os ativos em um Conjunto de mídias mistas ao navegar até o conjunto. No painel à esquerda, selecione **[!UICONTROL Definir membros]** e selecione o ícone **[!UICONTROL Lápis]** em um ativo individual para abrir a janela de edição.


1. Selecione **[!UICONTROL Salvar]** quando terminar a edição.

   >[!NOTE]
   >
   >* Para editar os ativos em um Conjunto de mídias mistas - Navegue até o Conjunto de mídias mistas. Toque (não selecione) no conjunto para abri-lo na página Visualização do conjunto de Experience Manager. No painel à esquerda, selecione o sinal de seta para baixo para abrir a lista suspensa e selecione **[!UICONTROL Definir membros]**. Na página Definir membros , passe o mouse sobre um ativo e selecione **[!UICONTROL Editar]** (ícone de lápis) para abrir a página de edição.
      >
      >
   * Para excluir um conjunto de mídia mista inteiro - A partir de qualquer modo de exibição (como a Exibição de cartão ou em Coluna), navegue até o conjunto de mídias mistas. Passe o mouse sobre o conjunto e selecione **[!UICONTROL Select]** (ícone de marca de seleção). Pressione **[!UICONTROL Backspace]** no teclado ou selecione **[!UICONTROL Mais]** (linha de três pontos) e selecione **[!UICONTROL Excluir]**.


## Visualizar conjuntos de mídia mista {#previewing-mixed-media-sets}

Consulte [Visualizar ativos](/help/assets/dynamic-media/previewing-assets.md) para obter detalhes sobre como visualizar Conjuntos de mídias mistas.

## Publicar conjuntos de mídia mista {#publishing-mixed-media-sets}

Consulte [Publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar Conjuntos de mídias mistas.

>[!NOTE]
>
>Se o conjunto de mídia mista não terminar totalmente no serviço de delivery na primeira vez que você o publicar, publique o conjunto de mídia mista uma segunda vez.
