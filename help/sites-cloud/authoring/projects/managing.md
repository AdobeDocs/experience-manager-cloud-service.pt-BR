---
title: Gerenciamento de projetos
description: O console de Projetos permite organizar o projeto, agrupando os recursos em uma única entidade que pode ser acessada e gerenciada no próprio console
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
source-git-commit: 54a098d8986c8bbd740bed50f8625c1025d2f6f4
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 100%

---

# Gerenciamento de projetos {#managing-projects}

O console Projetos permite que você organize seu projeto, agrupando os recursos em uma entidade.

No console **Projetos**, você acessa e toma medidas nos seus projetos:

![O console de Projetos](/help/sites-cloud/authoring/assets/projects-console.png)

Em Projetos, é possível criar um projeto, associar recursos ao projeto e também excluir um projeto ou vínculos de recursos. Você pode querer abrir um mosaico para exibir seu conteúdo, bem como adicionar itens a um mosaico. Este tópico descreve esses procedimentos.

## Criação de um projeto {#creating-a-project}

Pronto para uso, o AEM permite escolher os seguintes modelos ao criar um projeto:

* Projeto simples
* Projeto de mídia
* Projeto de tradução

<!-- Hiding product photoshoot via cqdoc-18072 as it is not available in Skyline.
* Product Photo Shoot Project 
-->

O procedimento de criação de um projeto é o mesmo em todos os projetos. A diferença entre os tipos de projetos inclui [funções de usuário](/help/sites-cloud/authoring/projects/overview.md) e [fluxos de trabalho](/help/sites-cloud/authoring/projects/workflows.md) disponíveis.  Para criar um novo projeto:

1. Em **Projetos**, toque/clique em **Criar** para abrir o assistente **Criar projeto**:
1. Selecione um modelo e clique em **Próximo**.

   ![Criação de um projeto](/help/sites-cloud/authoring/assets/projects-create.png)

1. Defina o **Título** e a **Descrição** e adicione uma imagem de **Miniatura** se necessário. Você também adiciona ou exclui os usuários e os grupos aos quais pertencem. Além disso, clique em **Avançado** para adicionar um nome utilizado no URL.

   ![Adicionar detalhes do projeto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Toque/clique em **Criar**. A confirmação pergunta se você deseja abrir o novo projeto ou retornar ao console.

### Associar recursos ao projeto {#associating-resources-with-your-project}

Como os projetos permitem agrupar recursos em uma única entidade, você deseja associar os recursos ao projeto. Esses recursos são chamados de **Mosaicos**. Os tipos de recursos que você pode adicionar são descritos nos [Mosaicos do projeto](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

Para associar recursos ao projeto:

1. Abra o projeto do console **Projetos**.
1. Toque/clique em **Adicionar mosaico** e selecione o mosaico que deseja vincular ao projeto. É possível selecionar vários tipos de mosaicos.

   ![Adicionar um bloco a um projeto](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >Os mosaicos que podem ser associados a um projeto são descritos mais detalhadamente em [Mosaicos do projeto.](/help/sites-cloud/authoring/projects/overview.md#project-tiles)

1. Toque/clique em **Criar**. O recurso é vinculado ao seu projeto e a partir de agora é possível acessá-lo do próprio projeto.

### Excluir um vínculo de projeto ou recurso {#deleting-a-project-or-resource-link}

O mesmo método é usado para excluir um projeto do console ou um recurso vinculado do seu projeto:

1. Navegue até o local apropriado:

   * Para excluir um projeto, acesse o nível superior do console **Projetos**.
   * Para excluir um vínculo de recurso em um projeto, abra o projeto no console **Projetos**.

1. Entre no modo de seleção clicando em **Selecionar** e selecionando o vínculo do projeto ou do recurso.
1. Toque/clique em **Excluir**.

1. Você precisa confirmar a exclusão em uma caixa de diálogo. Se confirmado, o vínculo do projeto ou do recurso será excluído. Toque/clique em **Desmarcar** para sair do modo de seleção.

>[!NOTE]
>
>Ao criar o projeto e adicionar usuários às várias funções, os grupos associados ao projeto são criados automaticamente para gerenciar as permissões associadas. Por exemplo, um projeto chamado Myproject teria três grupos: **Proprietários do Myproject**, **Editores do Myproject**, **Observadores do Myproject**. No entanto, se o projeto for excluído, esses grupos não serão excluídos automaticamente. Um administrador precisa excluir manualmente os grupos em **Ferramentas** > **Segurança** > **Grupos**.

### Adicionar itens a um mosaico {#adding-items-to-a-tile}

Em alguns mosaicos, é possível adicionar mais de um item. Por exemplo, é possível ter mais de um fluxo de trabalho ou experiência em execução simultaneamente.

Para adicionar itens a um mosaico:

1. Em **Projetos**, navegue até o projeto e toque ou clique na divisa para baixo no bloco ao qual deseja adicionar um item.

   ![Adicionar item a um bloco](/help/sites-cloud/authoring/assets/project-workflows.png)

1. Adicione um item ao mosaico da mesma forma que ao criar um novo mosaico. Os mosaicos do projeto são descritos[ aqui](/help/sites-cloud/authoring/projects/overview.md#project-tiles). Neste exemplo, outro fluxo de trabalho foi adicionado.

### Abrir um mosaico {#opening-a-tile}

Você pode querer ver quais itens estão incluídos em um mosaico atual ou modificar ou excluir itens no mosaico.

Para abrir um mosaico para ver ou modificar itens:

1. No console Projetos, toque/clique nas reticências (...) Ícone na parte inferior do cartão.

   ![Abrir um bloco](/help/sites-cloud/authoring/assets/project-links.png)

1. O AEM lista os itens no mosaico. É possível entrar no modo de seleção para modificar ou excluir os itens.

   ![Bloco aberto](/help/sites-cloud/authoring/assets/projects-add-link.png)

## Exibir as estatísticas do projeto {#viewing-project-statistics}

Você pode exibir as estatísticas do projeto no console de **Projetos**.

### Exibir uma linha do tempo do projeto {#viewing-a-project-timeline}

A linha do tempo do projeto fornece informações sobre quando os ativos do projeto foram usados pela última vez. Para exibir a linha do tempo do projeto, clique/toque em **Linha do tempo**, entre no modo de seleção e selecione o projeto. Os ativos são exibidos no painel esquerdo. Toque/clique em **Linha do tempo** para voltar ao console de **Projetos**.

![Linha do tempo do projeto](/help/sites-cloud/authoring/assets/projects-timeline.png)

### Exibir projetos ativos/inativos {#viewing-active-inactive-projects}

Para alternar entre os projetos ativos e inativos, no console de **Projetos**, clique em **Alternar projetos ativos**. Se o ícone tiver uma marca de seleção, ele exibirá os projetos ativos.

![Botão Alternar projetos ativos](/help/sites-cloud/authoring/assets/projects-active.png)

Se o ícone tiver um X, estará exibindo os projetos inativos.

![Botão Alternar projetos inativos](/help/sites-cloud/authoring/assets/projects-inactive.png)

## Tornar os projetos ativo ou inativos {#making-projects-inactive-or-active}

Você pode querer inativar um projeto concluído, mas ainda manter as informações no projeto.

Para tornar um projeto inativo (ou ativo):

1. No console **Projetos**, abra o projeto e, em seguida, localize o mosaico **Informações do projeto**.

   >[!NOTE]
   Talvez seja necessário adicionar este mosaico se ele ainda não estiver no seu projeto. Consulte [Adicionar mosaico](#adding-items-to-a-tile).

1. Toque/clique em **Editar**.
1. Altere o seletor de **Ativo** para **Inativo** (ou vice-versa).

   ![Ativar um projeto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Toque/clique em **Concluído** para salvar as alterações.
