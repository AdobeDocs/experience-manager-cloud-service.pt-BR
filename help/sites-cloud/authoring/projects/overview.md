---
title: Projetos
description: Projetos permitem agrupar recursos em uma única entidade, cujo ambiente comum e compartilhado facilita o gerenciamento dos seus projetos
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
source-git-commit: 8ea043b4b6424d6922c41c143ca74fd25ac60cf8
workflow-type: ht
source-wordcount: '1259'
ht-degree: 100%

---

# Projetos {#projects}

Projetos permitem agrupar recursos em uma entidade. Um ambiente comum e compartilhado facilita o gerenciamento dos seus projetos. Os tipos de recursos que você pode associar a um projeto são chamados de Mosaicos no AEM. Blocos podem incluir informações do projeto e da equipe, ativos, workflows e outros tipos de informações, conforme descrito detalhadamente em [Blocos de projeto.](#project-tiles)

>[!CAUTION]
>
>Para que os usuários em projetos possam ver outros usuários/grupos enquanto usam a funcionalidade Projetos (como criar projetos, criar tarefas/workflows, ver e gerenciar a equipe), eles precisam ter acesso de leitura a `/home/users` e `/home/groups`. A maneira mais fácil de implementar é fornecer ao grupo **projetos-usuários** acesso de leitura a `/home/users` e `/home/groups`.

Como usuário, você pode fazer o seguinte:

* Criar projetos
* Associar pastas de conteúdo e recursos a um projeto
* Excluir projetos
* Remover links de conteúdo do projeto

Consulte os seguintes tópicos adicionais:

* [Gerenciamento de projetos](/help/sites-cloud/authoring/projects/managing.md)
* [Trabalhar com tarefas](/help/sites-cloud/authoring/projects/tasks.md)
* [Trabalhar com fluxos de trabalho de projeto](/help/sites-cloud/authoring/projects/workflows.md)

## Console Projetos {#projects-console}

O console Projetos é onde você acessa e gerencia seus projetos no AEM.

![O console de projetos](/help/sites-cloud/authoring/assets/projects-console.png)

* Selecione **Linha do tempo** e, em seguida, um projeto para visualizar sua linha do tempo.
* Clique/toque em **Selecionar** para entrar no modo de seleção.
* Clique em **Criar** para adicionar projetos.
* **Alternar projetos ativos** permite alternar entre todos os projetos e somente aqueles que estão ativos.
* **Exibir visualização de estatísticas** permite ver estatísticas de projeto referentes a conclusões de tarefas.

## Blocos de Projetos {#project-tiles}

Com Projetos, você associa diferentes tipos de informações aos seus projetos. Esses informações são chamadas de **Blocos**. Cada um dos blocos e o tipo de informação que eles contêm estão descritos nesta seção.

Você pode ter os seguintes blocos associados ao seu projeto. Cada um está descrito nas seções a seguir:

* Ativos e coleções de ativos
* Experiências
* Links
* Informações do projeto
* Equipe
* Páginas de aterrissagem
* Emails
* Fluxos de trabalhos
* Lançamentos
* Tarefas

### Ativos {#assets}

No bloco **Assets**, você pode reunir todos os ativos que você usa para um projeto específico.

![Bloco de ativos](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

Você faz o upload de recursos diretamente no bloco. Além disso, é possível criar Definições de imagem, Grupos de rotação ou Conjuntos de mix de mídia com o complemento Mídia dinâmica.

![Conjunto de imagens](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### Coleções de ativos {#asset-collections}

Semelhante a ativos, você pode adicionar [coleções de ativos](/help/assets/manage-collections.md) diretamente ao seu projeto. Você define coleções no Assets.

![Coleção de ativos](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

Adicione uma coleção ao clicar em **Adicionar coleção** e selecionar a coleção apropriada na lista.

### Experiências {#experiences}

O bloco **Experiências** permite adicionar um aplicativo para dispositivos móveis, um site ou uma publicação ao projeto.

![Experiências](/help/sites-cloud/authoring/assets/project-experiences.png)

Os ícones indicam que tipo de experiência é representada: site, aplicativo móvel ou publicação. Adicione experiências tocando ou clicando na divisa para baixo, tocando em **Adicionar experiência** e selecionando o tipo de experiência.

![Adicionar uma experiência](/help/sites-cloud/authoring/assets/projects-add-experience.png)

Selecione o caminho para as miniaturas e, se aplicável, altere a miniatura da experiência. As experiências são agrupadas no bloco **Experiências.**

### Links {#links}

O bloco Links permite associar links externos ao seu projeto.

![Links](/help/sites-cloud/authoring/assets/project-links.png)

Você pode nomear o link com um nome fácil de reconhecer, além de alterar a miniatura.

![Adicionar link](/help/sites-cloud/authoring/assets/projects-add-link.png)

### Informações do projeto {#project-info}

O bloco Informações do projeto fornece informações gerais sobre o projeto, incluindo uma descrição, o status do projeto (inativo ou ativo), uma data de vencimento e membros. Além disso, você pode adicionar uma miniatura de projeto, que é exibida na página principal de Projetos.

![Informações do projeto](/help/sites-cloud/authoring/assets/project-info.png)

Os membros da equipe podem ser atribuídos a esse bloco e excluídos dele (ou ter suas funções alteradas), bem como do bloco Equipe.

![Adicionar membros da equipe ao projeto](/help/sites-cloud/authoring/assets/projects-add-team.png)

### Tarefa de tradução {#translation-job}

O bloco Tarefa de tradução é onde você inicia uma tradução e visualiza o status das suas traduções. Para configurar sua tradução, consulte [Criação de projetos de tradução](/help/assets/translate-assets.md).

![Trabalho de tradução](/help/sites-cloud/authoring/assets/projects-translation-job.png)

Clique nas reticências na parte inferior do cartão **Tarefa de tradução** para ver os ativos no fluxo de tarefa de tradução. A lista de tarefas de tradução também exibe entradas para metadados e tags de ativos. Essas entradas indicam que metadados e tags de ativos também são traduzidos.

![Detalhes do trabalho de tradução](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### Equipe {#team}

Nesse bloco, você pode especificar os membros da equipe do projeto. Ao editar, você pode inserir o nome do membro da equipe e atribuir a função do usuário.

![Bloco da equipe](/help/sites-cloud/authoring/assets/projects-team-tile.png)

É possível adicionar e excluir membros da equipe. Além disso, você pode editar a [função de usuário](#user-roles-in-a-project) atribuída ao membro da equipe.

![Adicionar equipe da lista](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### Fluxos de trabalhos {#workflows}

Você pode atribuir seu projeto para seguir certos fluxos de trabalho. Se algum fluxo de trabalho estiver em execução, seu status será exibido no bloco **Fluxos de trabalho**, em Projetos.

![Fluxos de trabalhos](/help/sites-cloud/authoring/assets/project-workflows.png)

Você pode atribuir seu projeto para seguir certos fluxos de trabalho. Dependendo do projeto escolhido, você tem fluxos de trabalho diferentes disponíveis.

Eles estão descritos em [Trabalhar com fluxos de trabalho de projeto](/help/sites-cloud/authoring/projects/workflows.md).

### Lançamentos {#launches}

O bloco Lançamentos mostra todos os lançamentos que foram solicitados com um [fluxo de trabalho Solicitar lançamento](/help/sites-cloud/authoring/projects/workflows.md).

![Lançamentos](/help/sites-cloud/authoring/assets/project-launches.png)

### Tarefas {#tasks}

Tarefas permitem monitorar o status de qualquer tarefa relacionada ao projeto, incluindo fluxos de trabalho. As tarefas são abordadas em detalhes em [Trabalhar com tarefas](/help/sites-cloud/authoring/projects/tasks.md).

![Tarefas](/help/sites-cloud/authoring/assets/projects-tasks.png)

## Modelos de projeto {#project-templates}

O AEM acompanha três modelos diferentes prontos para uso:

* Um projeto simples - Uma amostra de referência para qualquer projeto que não se encaixe em outras categorias (uma categoria genérica). Ele inclui três funções básicas (Proprietários, Editores e Observadores) e quatro fluxos de trabalho (Aprovação de projeto, Solicitar lançamento, Solicitar página de aterrissagem e Solicitar email).
* Um projeto de mídia - Um projeto de amostra de referência para atividades de mídia. Ele inclui várias funções de projeto relacionadas a mídia (Fotógrafos, Editores, Redatores, Designers, Proprietários e Observadores). Ele também solicita o fluxo de trabalho de cópia para solicitar e revisar o texto.
* Um [projeto de tradução](/help/sites-cloud/administering/translation/overview.md) - Uma amostra de referência para o gerenciamento de atividades relacionadas a tradução. Ele inclui três funções básicas (Proprietários, Editores e Observadores). Também inclui dois fluxos de trabalho que são acessados na interface de usuário de Fluxos de trabalho.

Com base no modelo selecionado, você tem diferentes opções disponíveis, principalmente em relação a funções de usuário e fluxos de trabalho.

## Funções de usuário em um projeto {#user-roles-in-a-project}

As diferentes funções de usuário são definidas em um modelo de Projeto e são usadas por dois motivos principais:

1. Permissões. As funções do usuário se enquadram em uma das três categorias listadas: Observador, Editor, Proprietário. Por exemplo, um Fotógrafo ou Redator terá os mesmos privilégios de um Editor. As permissões determinam o que um usuário pode fazer com o conteúdo em um projeto.
1. Fluxos de trabalhos. Os fluxos de trabalho determinam recebe tarefas em um projeto. As tarefas podem ser associadas a uma função de projeto. Por exemplo, uma tarefa pode ser atribuída a Fotógrafos, de forma que todos os membros da equipe com a função Fotógrafo a recebam.

Todos os projetos oferecem suporte às seguintes funções padrão, para permitir que você administre permissões de segurança e controle:

| Função | Descrição | Permissões | Associação de Grupo |
|---|---|---|---|
| Observador | Um usuário nessa função pode visualizar detalhes do projeto, incluindo seu status. | Permissões somente leitura em um projeto | `workflow-users` grupo |
| Editor | Um usuário nessa função pode fazer o upload e a edição do conteúdo de um projeto. | Acesso de leitura e gravação em um projeto, metadados associados e ativos relacionados; privilégios para fazer upload de uma lista de capturas e revisar e aprovar ativos; permissão de gravação em /etc/commerce; modificar permissão em um projeto específico | grupo de usuários de fluxo de trabalho |
| Proprietário | Um usuário nessa função pode iniciar um projeto. Um proprietário pode criar um projeto, iniciar um trabalho em um projeto e também mover ativos aprovados para a pasta Produção. Além disso, todas as outras tarefas no projeto também podem ser visualizadas e executadas pelo proprietário. | Permissão de gravação em `/etc/commerce` | Grupo `dam-users` (para poder criar um projeto) grupo de administradores de projeto (para poder criar um projeto e mover ativos) |

>[!NOTE]
>
>Ao criar o projeto e adicionar usuários às várias funções, os grupos associados ao projeto são criados automaticamente para gerenciar as permissões associadas. Por exemplo, um projeto chamado Myproject teria três grupos: **Proprietários do Myproject**, **Editores do Myproject**, **Observadores do Myproject**. No entanto, se o projeto for excluído, esses grupos não serão excluídos automaticamente. Um administrador precisa excluir manualmente os grupos em **Ferramentas** > **Segurança** > **Grupos**.
