---
title: Gerenciamento de projetos
description: O console de Projetos permite organizar o projeto, agrupando os recursos em uma única entidade que pode ser acessada e gerenciada no próprio console
exl-id: be4616e7-18bc-4b2d-89f6-d04178ac7f3a
source-git-commit: 54a098d8986c8bbd740bed50f8625c1025d2f6f4
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 49%

---

# Gerenciamento de projetos {#managing-projects}

Projects permite organizar o projeto agrupando recursos em uma entidade.

No **Projetos** console, você acessa e executa ações em seus projetos:

![O console de Projetos](/help/sites-cloud/authoring/assets/projects-console.png)

Em Projetos, você pode criar um projeto, associar recursos ao projeto e também excluir um projeto ou links de Recursos. Talvez você queira abrir um bloco para exibir seu conteúdo, bem como adicionar itens a um bloco. Este tópico descreve esses procedimentos.

## Criação de um projeto {#creating-a-project}

Imediatamente, o AEM fornece esses modelos para escolher quando você cria um projeto:

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

1. Defina o **Título** e a **Descrição** e adicione uma imagem de **Miniatura** se necessário. Também é possível adicionar ou excluir usuários e a qual grupo eles pertencem. Além disso, **Avançado** para adicionar um nome usado no URL.

   ![Adicionar detalhes do projeto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Toque/clique em **Criar**. A confirmação pergunta se você deseja abrir seu novo projeto ou retornar ao console.

### Associar recursos ao seu projeto {#associating-resources-with-your-project}

Como os projetos permitem agrupar recursos em uma entidade, você deseja associar recursos ao projeto. Esses recursos são chamados de **Ladrilhos**. Os tipos de recursos que você pode adicionar estão descritos em [Mosaico do projeto](/help/sites-cloud/authoring/projects/overview.md#project-tiles).

Para associar recursos ao projeto:

1. Abra o projeto na **Projetos** console.
1. Toque/clique **Adicionar mosaico** e selecione o bloco que deseja vincular ao projeto. É possível selecionar vários tipos de mosaicos.

   ![Adicionar um bloco a um projeto](/help/sites-cloud/authoring/assets/projects-add-tile.png)

   >[!NOTE]
   >
   >Os mosaicos que podem ser associados a um projeto são descritos mais detalhadamente em [Mosaicos do projeto.](/help/sites-cloud/authoring/projects/overview.md#project-tiles)

1. Toque/clique em **Criar**. O recurso é vinculado ao seu projeto e a partir de agora é possível acessá-lo do próprio projeto.

### Excluir um vínculo de projeto ou recurso {#deleting-a-project-or-resource-link}

O mesmo método é usado para excluir um projeto do console ou um recurso vinculado do seu projeto:

1. Navegue até o local apropriado:

   * Para excluir um projeto, vá para o nível superior da **Projetos** console.
   * Para excluir um vínculo de recurso em um projeto, abra o projeto no console **Projetos**.

1. Entre no modo de seleção clicando em **Selecionar** e selecionando o vínculo do projeto ou do recurso.
1. Toque/clique em **Excluir**.

1. Você precisa confirmar a exclusão em uma caixa de diálogo. Se confirmado, o link do projeto ou do recurso será excluído. Toque/clique em **Desmarcar** para sair do modo de seleção.

>[!NOTE]
>
>Ao criar o projeto e adicionar usuários às várias funções, os grupos associados ao projeto são criados automaticamente para gerenciar as permissões associadas. Por exemplo, um projeto chamado Myproject teria três grupos: **Proprietários do Myproject**, **Editores do Myproject**, **Observadores do Myproject**. No entanto, se o projeto for excluído, esses grupos não serão excluídos automaticamente. Um administrador precisa excluir manualmente os grupos em **Ferramentas** > **Segurança** > **Grupos**.

### Adicionar itens a um bloco {#adding-items-to-a-tile}

Em alguns blocos, talvez você queira adicionar mais de um item. Por exemplo, é possível ter mais de um workflow em execução de uma vez ou mais de uma experiência.

Para adicionar itens a um Bloco:

1. Em **Projetos**, navegue até o projeto e toque ou clique na divisa para baixo no bloco ao qual deseja adicionar um item.

   ![Adicionar item a um bloco](/help/sites-cloud/authoring/assets/project-workflows.png)

1. Adicione um item ao bloco da mesma maneira que você faria ao criar um novo bloco. Os mosaicos do projeto estão descritos [aqui](/help/sites-cloud/authoring/projects/overview.md#project-tiles). Neste exemplo, outro workflow foi adicionado.

### Abrir um mosaico {#opening-a-tile}

Talvez você queira ver quais itens estão incluídos em um bloco atual ou modificar ou excluir itens no bloco.

Para abrir um bloco para exibir ou modificar itens:

1. No console Projetos, toque/clique no ícone de reticências (...) na parte inferior do cartão.

   ![Abrir um bloco](/help/sites-cloud/authoring/assets/project-links.png)

1. O AEM lista os itens nesse bloco. Você pode entrar no modo de seleção para modificar ou excluir os itens.

   ![Bloco aberto](/help/sites-cloud/authoring/assets/projects-add-link.png)

## Exibir as estatísticas do projeto {#viewing-project-statistics}

Você pode exibir as estatísticas do projeto no console de **Projetos**.

### Visualizar uma linha do tempo do projeto {#viewing-a-project-timeline}

A linha do tempo do projeto fornece informações sobre quando os ativos do projeto foram usados pela última vez. Para exibir a linha do tempo do projeto, clique/toque em **Linha do tempo**, entre no modo de seleção e selecione o projeto. Os ativos são exibidos no painel esquerdo. Toque/clique em **Linha do tempo** para voltar ao console de **Projetos**.

![Linha do tempo do projeto](/help/sites-cloud/authoring/assets/projects-timeline.png)

### Exibir projetos ativos/inativos {#viewing-active-inactive-projects}

Para alternar entre os projetos ativos e inativos, no console de **Projetos**, clique em **Alternar projetos ativos**. Se o ícone tiver uma marca de seleção, ele exibirá os projetos ativos.

![Botão Alternar projetos ativos](/help/sites-cloud/authoring/assets/projects-active.png)

Se o ícone tiver um X, estará exibindo os projetos inativos.

![Botão Alternar projetos inativos](/help/sites-cloud/authoring/assets/projects-inactive.png)

## Tornando projetos inativos ou ativos {#making-projects-inactive-or-active}

Você pode querer tornar um projeto inativo se já o tiver concluído, mas ainda quiser manter as informações sobre o projeto.

Para tornar um projeto inativo (ou ativo):

1. No **Projetos** console, abra o projeto e localize o **Informações do projeto** bloco.

   >[!NOTE]
   Talvez seja necessário adicionar esse bloco se ele ainda não estiver em seu projeto. Consulte [Adição de Blocos](#adding-items-to-a-tile).

1. Toque/clique em **Editar**.
1. Altere o seletor de **Ativo** para **Inativo** (ou vice-versa).

   ![Ativar um projeto](/help/sites-cloud/authoring/assets/projects-add-team.png)

1. Toque/clique em **Concluído** para salvar as alterações.
