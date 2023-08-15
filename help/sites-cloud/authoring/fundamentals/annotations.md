---
title: Adição de anotações de página
description: Use o modo de anotação para deixar anotações e rascunhos nas páginas, como você usaria as notas adesivas para auxiliar no processo de revisão do conteúdo
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 85%

---

# Adição de anotações de página {#adding-page-annotations}

Criar conteúdo para sua experiência digital geralmente requer discussão e feedback antes da publicação. Para auxiliar nesse processo de feedback, o AEM permite adicionar anotações ao seu conteúdo.

Uma anotação coloca um rascunho ou nota simples (pense em uma nota autoadesiva real) na página. A anotação permite que você deixe comentários ou perguntas para outros autores e revisores.

>[!TIP]
>
>Não esqueça que [comentários](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) também estão disponíveis para fornecer feedback em uma página.

Um [modo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) é usado para criar e visualizar anotações.

>[!TIP]
>
>Dependendo dos seus requisitos, também é possível desenvolver um [fluxo de trabalho](/help/sites-cloud/authoring/workflows/overview.md) para enviar notificações quando anotações são adicionadas, atualizadas ou excluídas.

## Indicador de anotação {#annotation-indicator}

As anotações não aparecem no modo Editar, mas o selo na parte superior direita da barra de ferramentas mostra quantas anotações existem para a página atual. O selo substitui o ícone de Anotações padrão, mas ainda funciona como um link rápido que alterna de/para o modo Anotar:

![Indicador de anotação](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## Modo Anotação {#annotate-mode}

As anotações são visíveis apenas no modo Anotação.

1. Você pode entrar no modo Anotação usando o ícone na barra de ferramentas (canto superior direito) ao editar uma página:

   ![Botão Anotar](/help/sites-cloud/authoring/assets/annotations.png)

   Agora é possível exibir todas as anotações existentes.

   ![Exemplos de anotação](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Clique ou toque na anotação para abrir a caixa de diálogo de anotação e exibir seus detalhes.

   ![Detalhes da anotação](/help/sites-cloud/authoring/assets/annotation-adding.png)

1. Para sair do modo Anotação e voltar ao modo usado anteriormente, toque/clique no botão x à direita da barra de ferramentas superior.

## Adicionar e editar anotações {#annotating-a-component}

Além de visualizar as anotações, o modo Anotar permite criar, editar, mover ou excluir anotações do seu conteúdo

1. [Iniciar modo Anotação](#annotate-mode) na página.

1. Clique ou toque no ícone Adicionar anotação (símbolo de mais à esquerda da barra de ferramentas) para começar a adicionar as anotações.

1. Clique ou toque no componente desejado (os componentes que podem ser anotados são realçados com uma borda azul) para adicionar a anotação e abrir a caixa de diálogo:

   ![Adição de uma anotação](/help/sites-cloud/authoring/assets/annotation-adding.png)

   Aqui você pode usar o campo e/ou ícone apropriado para:

   * Insira o texto da anotação.
   * Criar um rascunho (linhas e formas) para realçar uma área do componente.

     ![Botão Rascunho de anotação](/help/sites-cloud/authoring/assets/annotation-sketch.png)

     O cursor se transformará em uma cruz durante a criação de um rascunho. Você pode desenhar várias linhas distintas. A linha de rascunho reflete a cor da anotação e pode ser uma seta, círculo ou forma oval.

   * Escolher ou alterar a cor:

     ![Botão Amostra de cor da anotação](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. Você pode fechar a caixa de diálogo de anotação clicando ou tocando fora dela. Uma exibição truncada da anotação, junto com os rascunhos existentes, é mostrada:

   ![Rascunhos de anotação](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Depois que terminar de editar uma anotação específica, você pode:

   * Clique ou toque em um marcador de texto para abrir a anotação. Depois de aberta, você pode exibir o texto completo, fazer alterações ou [excluir a anotação.](#deleting-annotations)
   * Reposicionar o marcador de texto.
   * Clique ou toque em uma linha de rascunho para selecionar esse rascunho e arrastá-lo para a posição desejada.
   * Mover ou copiar um componente
      * As anotações relacionadas e seus rascunhos também serão movidos ou copiados, e sua posição em relação ao parágrafo permanecerá a mesma.


>[!NOTE]
>
>As anotações não podem ser adicionadas a uma página que foi bloqueada por outro usuário.

>[!NOTE]
>
>A definição de um tipo de componente individual determina se é possível adicionar uma anotação (ou não) nas instâncias desse componente.

## Excluir anotações e rascunhos {#deleting-annotations}

As anotações e seus rascunhos associados podem ser excluídos.

1. [Iniciar modo Anotação](#annotate-mode) na página.

1. Clicar/tocar em um marcador de texto para abrir a anotação.

1. Clique ou toque no ícone Excluir.

   ![Excluir anotação](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. A anotação e todos os rascunhos associados são excluídos.

>[!NOTE]
>
>A exclusão de um componente exclui todas as anotações e rascunhos associados a esse recurso, independentemente de sua posição na página como um todo.

## Excluir somente rascunhos {#deleting-sketches}

Você pode excluir somente rascunhos específicos em vez da anotação inteira com todos os rascunhos associados.

1. [Iniciar modo Anotação](#annotate-mode) na página.

1. Clique ou toque no rascunho. O AEM o destaca com uma caixa azul mais escura.

   ![Selecionar rascunho para exclusão](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. Pressione a tecla Delete no teclado.

1. O rascunho é excluído, mas a anotação permanece.

## Anotação em outros recursos {#annotating-other-resources}

Além dos componente, é possível fazer anotações em vários recursos:

* Anotação de ativos [Anotação de ativos](/help/assets/manage-digital-assets.md#annotating)
* Anotação de ativos de vídeo [Anotação de ativos de vídeo](/help/assets/manage-video-assets.md#annotate-video-assets)
