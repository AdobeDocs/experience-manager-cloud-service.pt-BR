---
title: Publicar conteúdo com o editor de páginas
description: Saiba como o Editor de páginas publica conteúdo.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5871e04d3bd78bdd8df55d42e7619c98ea3f38ca
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 44%

---


# Publicar conteúdo com o Editor de sites {#publishing}

Saiba como o Editor de páginas publica conteúdo.

## Publicação por meio do Editor de páginas {#publishing-from-the-page-editor}

Se você estiver editando uma página no [editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md), ela poderá ser publicada diretamente do editor.

1. Selecione o ícone **Informações da página** para abrir o menu e depois a opção **Publicar página**.

   ![Publicação de uma página por meio das opções de página](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. Se a página tiver referências que precisam de publicação:

   * A página é publicada diretamente se não houver referências a serem publicadas.
   * Se a página tiver referências que precisem ser publicadas, elas serão listadas no assistente de **Publicação**, onde você poderá:
      * Especifique quais dos ativos, ou tags etc., você deseja publicar junto com a página. Em seguida, use **Publicar** para concluir o processo.
      * Usar a opção **Cancelar** para suspender a ação.

   ![Publicação de referências com a página](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Se você selecionar **Publicar**, replicará a página no ambiente de publicação. No editor de páginas, será mostrado um banner de informações confirmando a ação de publicação.

   ![Banner de informações do status de publicação](/help/sites-cloud/authoring/assets/publishing-info.png)

   Ao visualizar a mesma página no console, o status da publicação atualizada estará visível.

   ![Status de publicação da página na exibição de coluna no console Sites](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>A publicação por meio do editor de páginas é um processo superficial, ou seja, somente as páginas selecionadas são publicadas, sem incluir páginas filhas.

>[!NOTE]
>
>Páginas acessadas por [aliases](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) no editor não podem ser publicadas. As opções de publicação no editor só estão disponíveis para páginas acessadas por meio de seus caminhos reais.

## Desfazer a publicação por meio do Editor de páginas {#unpublishing}

Ao editar uma página usando o Editor de páginas, se você quiser desfazer a publicação dessa página, selecione **Desfazer a publicação da página** no menu **Informações da página**, da mesma forma que faria para [publicar a página](#publishing-from-the-editor).

>[!NOTE]
>
>Páginas acessadas por [aliases](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced) no editor não podem ter a publicação desfeita. As opções de publicação no editor só estão disponíveis para páginas acessadas por meio de seus caminhos reais.

## Publicar e desfazer a publicação por meio do console Sites {#publishing-sites-console}

Você também pode publicar [no console Sites](/help/sites-cloud/authoring/sites-console/publishing-pages.md), que pode ser útil quando desejar publicar várias páginas de conteúdo ou agendar a publicação ou o cancelamento da publicação.
