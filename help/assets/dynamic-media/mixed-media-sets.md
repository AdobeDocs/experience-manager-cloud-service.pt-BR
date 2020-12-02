---
title: Conjuntos de mídia mista
description: Saiba como trabalhar com conjuntos de mídia mista no Dynamic Media
translation-type: tm+mt
source-git-commit: 6b5bfa2bc7b37753e7c63bb2cf52609f352dc1ef
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 28%

---


# Conjuntos de mídia mista{#mixed-media-sets}

Os Conjuntos de mídia mista permitem que você forneça uma combinação de imagens, Conjuntos de imagens, Conjuntos de rotação e vídeos em uma única apresentação.

Os Conjuntos de mídias mistas são designados por um banner com a palavra **[!UICONTROL MixedMediaSet]**. Além disso, se o Conjunto de mídias mistas for publicado, a data de publicação, indicada pelo ícone **[!UICONTROL Mundo]**, estará no banner junto com a última data de modificação, indicada pelo ícone **[!UICONTROL Lápis]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Para obter informações sobre a interface de usuário do Assets, consulte [Gerenciar ativos com a interface de usuário de toque](/help/assets/manage-digital-assets.md).

## Start rápido: Conjuntos de mídia mista {#quick-start-mixed-media-sets}

Para iniciá-lo e executá-lo rapidamente com Conjuntos de mídia mista, siga estas etapas:

1. [Carregue seus ativos](#uploading-assets).

   Comece carregando as imagens e os vídeos dos Conjuntos de mídias mistas. Se necessário, crie seus [Conjuntos de imagens](/help/assets/dynamic-media/image-sets.md) e [Conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md). Como os usuários podem ampliar imagens no Visualizador de conjunto de mídias mistas, considere o zoom ao escolher imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão.

1. [Criar conjuntos de mídia mista.](#creating-mixed-media-sets)

   Para criar um Conjunto de mídia mista, na página Assets, toque em **[!UICONTROL Criar > Conjunto de mídias mistas]** e nomeie o conjunto, selecione os ativos e escolha a ordem em que as imagens serão exibidas.

   Consulte [Trabalhando com seletores.](/help/assets/dynamic-media/working-with-selectors.md)

1. Configure [predefinições do visualizador de mídia mista](/help/assets/dynamic-media/managing-viewer-presets.md), conforme necessário.

   Os administradores podem criar ou modificar as Predefinições do visualizador de conjunto de mídia mista. Para ver sua mídia mista com uma predefinição do visualizador, selecione o conjunto de mídias mistas e, no menu suspenso do painel à esquerda, selecione **[!UICONTROL Visualizadores]**.

   Consulte **[!UICONTROL Ferramentas > Ativos > Predefinições do visualizador]** para criar ou editar predefinições do visualizador.

   Consulte [Adicionar e editar predefinições do visualizador.](/help/assets/dynamic-media/managing-viewer-presets.md)

1. [Pré-visualização de conjuntos de mídia mista.](#previewing-mixed-media-sets)

   Selecione o Conjunto de mídia mista e você pode pré-visualização-lo. Clique nos ícones de miniatura para examinar seu Conjunto de mídia mista no visualizador selecionado. Você pode escolher visualizadores diferentes no menu **[!UICONTROL Visualizadores]**, disponível no menu suspenso do painel esquerdo.

1. [Publicar conjuntos de mídia mista.](#publishing-mixed-media-sets)

   A publicação de um Conjunto de mídia mista ativa o URL e a string Incorporada. Além disso, você deve [publicar a predefinição do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

1. [Vincule URLs ao seu ](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) aplicativo da Web ou  [Incorpore o visualizador](/help/assets/dynamic-media/embed-code.md) de vídeo ou imagem.

   A AEM Assets cria chamadas de URL para Conjuntos de mídia mista e as ativa após a publicação dos conjuntos de mídia mista. Você pode copiar esses URLs ao pré-visualização de ativos. Como alternativa, você pode incorporá-los ao seu site.

   Selecione o Conjunto de mídias mistas e, no menu suspenso do painel esquerdo, selecione **[!UICONTROL Visualizadores]**.

   Consulte [Vincular um conjunto de mídias mistas a uma página da Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incorporar o visualizador de vídeo ou imagem](/help/assets/dynamic-media/embed-code.md).

Se necessário, edite [Conjuntos de mídia mista](#editing-mixed-media-sets). Além disso, você pode visualização e modificar [as propriedades do Conjunto de Mídias Misto](/help/assets/manage-digital-assets.md#editing-properties).

>[!NOTE]
>
>Se tiver problemas ao criar conjuntos, consulte [Resolução de problemas do Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).

## Carregar ativos {#uploading-assets}

Comece carregando as imagens e os vídeos dos Conjuntos de mídias mistas. Como os usuários podem aplicar zoom em imagens no Visualizador de conjunto de mídia mista, lembre-se de levar em conta o zoom ao escolher imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão.

Além disso, se você quiser adicionar conjuntos de rotação ou conjuntos de imagens ao conjunto de mídia mista, crie-os também.

## Criando conjuntos de mídia mista {#creating-mixed-media-sets}

Você pode adicionar imagens, Conjuntos de imagens, Conjuntos de rotação e vídeos ao seu Conjunto de mídia mista. Verifique se os arquivos, os conjuntos de imagens e os conjuntos de rotação estão prontos para publicação antes de adicioná-los ao Conjunto de Mídia Mista.

Quando você adiciona ativos ao seu conjunto, eles são adicionados automaticamente em ordem alfanumérica. Você pode reordenar ou classificar manualmente os ativos depois de adicionados.

**Para criar um conjunto de mídia mista**

1. No Assets, navegue até o local em que deseja criar um conjunto de mídia mista, clique em **[!UICONTROL Criar]** e selecione **[!UICONTROL Conjunto de mídia mista]**. Além disso, crie o conjunto de dentro de uma pasta que contenha seus ativos. O Editor do conjunto de mídias mistas é exibido.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. No Editor de conjunto de mídia mista, em **[!UICONTROL Title]**, digite um nome para o conjunto de mídia mista. O nome é exibido no banner no Conjunto de mídia mista. Opcionalmente, informe uma descrição.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Ao criar o conjunto de mídias mistas, você pode alterar a miniatura do conjunto de mídias mistas ou permitir que AEM selecione a miniatura automaticamente com base nos ativos do conjunto de mídias mistas. Para selecionar uma miniatura, clique em **[!UICONTROL Alterar miniatura]** e selecione qualquer imagem (você também pode navegar para outras pastas para localizar imagens). Se você tiver selecionado uma miniatura e decidir que deseja AEM gerar uma do conjunto de mídias mistas, selecione **[!UICONTROL Alternar para miniatura automática]**.

1. Toque no Seletor de ativos para selecionar os ativos que deseja incluir no Conjunto de mídias mistas. Selecione-os e clique em **[!UICONTROL Select]**.

   Com o Seletor de ativos, procure por ativos ao digitar uma palavra-chave e tocar em **[!UICONTROL Retornar]**. Aplique filtros para refinar os resultados da pesquisa. Filtre por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e toque no ícone **[!UICONTROL Filtro]**, na barra de ferramentas. Altere a exibição ao clicar no ícone **[!UICONTROL Exibição]** e selecionar **[!UICONTROL Exibição em lista]**, **[!UICONTROL Exibição em coluna]** ou **[!UICONTROL Exibição de cartão]**.

   Consulte [Trabalhando com seletores](/help/assets/dynamic-media/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-351.png)

1. Reorganize os ativos arrastando-os para cima ou para baixo na lista (deve selecionar o ícone **[!UICONTROL Reordenar]**), conforme necessário.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Se quiser adicionar miniaturas, clique no ícone de **miniatura** **[!UICONTROL +]** ao lado da imagem e navegue até a miniatura desejada. Quando terminar de selecionar todas as imagens em miniatura, clique em **[!UICONTROL Salvar]**.

   >[!NOTE]
   >
   >Se desejar adicionar ativos, toque em **[!UICONTROL Adicionar ativo]**.

1. Para excluir um ativo, marque a caixa de seleção correspondente e toque em **[!UICONTROL Excluir ativo]**.
1. Para aplicar uma predefinição, toque em **[!UICONTROL Predefinir]** no canto superior direito e selecione uma predefinição para aplicar aos ativos.
1. Clique em **[!UICONTROL Salvar]**. Seu conjunto de mídia mista recém-criado é exibido na pasta em que você o criou.

## Edição de conjuntos de mídia mista {#editing-mixed-media-sets}

Você pode executar várias tarefas de edição em ativos em Conjuntos de mídia mista diretamente na interface do usuário [como faria com qualquer ativo em Ativos](/help/assets/manage-digital-assets.md). Você também pode executar as seguintes ações em Conjuntos de mídia mista:

* Adicione ativos ao Conjunto de mídias mistas.
* Resolicite ativos no Conjunto de mídia mista.
* Exclua ativos no Conjunto de mídias mistas.
* Aplicar predefinições do visualizador.
* Altere a miniatura padrão.

**Para editar um conjunto de mídia mista**

1. Execute um dos procedimentos a seguir:

   * Passe o cursor do mouse sobre um ativo do Conjunto de mídia mista e, em seguida, toque em **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o cursor do mouse sobre um ativo do Conjunto de mídia mista, toque em **[!UICONTROL Selecionar]** (ícone de marca de seleção) e, em seguida, toque em **[!UICONTROL Editar]** na barra de ferramentas.

   * Toque em um ativo Conjunto de mídia mista e, em seguida, toque em **[!UICONTROL Editar]** (ícone de lápis) na barra de ferramentas.

1. No Mixed Media Set Editor, execute um dos procedimentos a seguir:

   * Para reorganizar ativos - No painel esquerdo, toque em **[!UICONTROL Ativos]** (ícone de imagem), arraste um ativo para um novo local.
   * Para adicionar ativos - na barra de ferramentas, toque em **[!UICONTROL Adicionar ativo]**. Navegue até os ativos. Para cada ativo que você deseja adicionar, passe o mouse sobre a imagem do ativo (não o nome do ativo) e toque no ícone de marca de seleção. No canto superior direito, toque em **[!UICONTROL Select]**.

   * Para excluir um ativo - no painel esquerdo, toque em **[!UICONTROL Ativos]** (ícone de imagem) e selecione o ativo. Na barra de ferramentas, toque em **[!UICONTROL Excluir ativo]**.

   * Para classificar os ativos pelo nome em ordem crescente ou decrescente, no painel esquerdo, toque em **[!UICONTROL Ativos]** (ícone de imagem). À direita do cabeçalho **[!UICONTROL Assets]**, toque nos ícones de cursor para cima ou para baixo.

      >[!NOTE]
      >
      >* Para excluir um conjunto de mídia mista inteiro, de qualquer modo de exibição (como **[!UICONTROL Visualização de cartão]** ou **[!UICONTROL Visualização de coluna]**), navegue até o conjunto de mídia mista. Passe o cursor sobre o ativo e toque no ícone de marca de seleção para selecioná-lo. Pressione **[!UICONTROL Backspace]** no teclado ou clique em **[!UICONTROL Mais]** (três pontos) na barra de ferramentas e, em seguida, toque em **[!UICONTROL Excluir]**.
         >
         >
      * Você pode editar os ativos em um Conjunto de Mídias Misto navegando até o conjunto, tocando **[!UICONTROL Definir membros]** no painel esquerdo e tocando no ícone **[!UICONTROL Lápis]** em um ativo individual para abrir a janela de edição.


1. Toque em **[!UICONTROL Salvar]** quando terminar a edição.

   >[!NOTE]
   >
   >* Para editar os ativos em um Conjunto de mídias mistas - Navegue até o Conjunto de mídias mistas. Toque (não selecione) no conjunto para abri-lo na página Visualização do conjunto do AEM. No painel esquerdo, clique no cursor para baixo para abrir a lista suspensa e toque em **[!UICONTROL Definir membros]**. Na página Definir membros, passe o mouse sobre um ativo e toque em **[!UICONTROL Editar]** (ícone de lápis) para abrir a página de edição.
      >
      >
   * Para excluir um conjunto de mídia mista inteiro - A partir de qualquer modo de exibição (como a Exibição de cartão ou em Coluna), navegue até o conjunto de mídias mistas. Passe o mouse sobre o conjunto e toque em **[!UICONTROL Select]** (ícone de marca de seleção). Pressione **[!UICONTROL Backspace]** no teclado ou toque em **[!UICONTROL Mais]** (linha de três pontos) e, em seguida, toque em **[!UICONTROL Excluir]**.


## Visualizando conjuntos de mídia mista {#previewing-mixed-media-sets}

Consulte [Visualizar ativos](/help/assets/dynamic-media/previewing-assets.md) para obter detalhes sobre como pré-visualização conjuntos de mídia mista.

## Publicando conjuntos de mídia mista {#publishing-mixed-media-sets}

Consulte [Publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar Conjuntos de mídia mista.

>[!NOTE]
>
>Se o conjunto de mídias mistas não terminar totalmente no serviço de delivery na primeira vez que você o publicar, talvez seja necessário publicar o conjunto de mídias mistas uma segunda vez.

