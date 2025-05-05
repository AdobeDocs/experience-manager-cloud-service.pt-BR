---
title: Trabalhar com fluxos de trabalho de projeto
description: Vários fluxos de trabalho de projeto estão disponíveis imediatamente.
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 96%

---

# Trabalhar com fluxos de trabalho de projeto {#working-with-project-workflows}

Os fluxos de trabalho de projeto disponíveis prontos para uso incluem o seguinte:

* **Fluxo de trabalho para aprovação de projeto** - Esse fluxo de trabalho permite atribuir conteúdo a um usuário, bem como analisá-lo e aprová-lo.
* **Solicitar inicialização** - um fluxo de trabalho que solicita uma inicialização.
* **Solicitar página de aterrissagem** - esse fluxo de trabalho solicita uma página de aterrissagem.
* **Solicitar email** - Fluxo de trabalho para solicitar um email.
* **Criar e traduzir cópia do DAM e Criar cópia de idioma do DAM** - cria binários, metadados e tags traduzidos para arquivos e pastas.

Dependendo do modelo de projeto selecionado, há determinados fluxos de trabalho disponíveis:

|   | **Projeto simples** | **Projeto de tradução** |
|---|:-:|:-:|
| Fluxo de trabalho de aprovação de projeto | x |  |
| Solicitar inicialização | x |  |
| Solicitar página de aterrissagem | x |  |
| Solicitar email | x | |
| Criar cópia de idioma do DAM&ast; |  | x |
| Criar e traduzir cópia de idioma do DAM;&ast; |   | x |

>[!NOTE]
>
>&ast; Esses fluxos de trabalho não são iniciados no bloco **Fluxo de trabalho** em Projetos. Consulte [Criação de cópias de idioma para arquivos](/help/sites-cloud/administering/translation/managing-projects.md).

As etapas para iniciar e concluir fluxos de trabalho são as mesmas, independentemente do fluxo de trabalho escolhido. Somente as etapas são alteradas.

Um fluxo de trabalho é iniciado diretamente em Projetos (exceto para Criar Cópia de Idioma do DAM ou Criar e Traduzir Cópia de Idioma do DAM). Informações sobre quaisquer tarefas pendentes em um projeto estão listadas no bloco **Tarefas**. As notificações para tarefas que precisam ser concluídas são exibidas ao lado do ícone do usuário.

Para obter mais informações sobre como trabalhar com fluxos de trabalho no AEM, consulte o seguinte:

* [Participar de fluxos de trabalho](/help/sites-cloud/authoring/workflows/participating.md)
* [Aplicação de fluxos de trabalho a páginas](/help/sites-cloud/authoring/workflows/applying.md)
* [Configuração de fluxos de trabalho](/help/sites-cloud/administering/workflows-administering.md)

Esta seção descreve os fluxos de trabalho disponíveis para Projetos.

## Fluxo de trabalho Aprovação de projeto {#project-approval-workflow}

No fluxo de trabalho Aprovação de Projeto, você atribui conteúdo a um usuário, revisa e aprova-o.

1. Em seu projeto simples, selecione o sinal de **`+`** no bloco **Fluxos de trabalho** e selecione **Fluxo de trabalho para aprovação de projeto**.
1. Insira um título e selecione a quem atribuí-lo na lista da equipe. Se aplicável, insira uma descrição, o caminho do conteúdo, uma prioridade pra tarefa e um prazo.

   ![Solicitar aprovação](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. A tarefa aparecerá no bloco **Tarefas**.

## Fluxo de trabalho Solicitar lançamento {#request-launch-workflow}

Esse fluxo de trabalho permite solicitar um lançamento.

1. No projeto simples, selecione o sinal **+** no bloco **Fluxos de trabalho** e selecione **Solicitar fluxo de trabalho de inicialização**.
1. Insira um título para lançamento e forneça o caminho de origem de lançamento. Também é possível adicionar uma descrição e uma data de ativação, se aplicável. Selecione Herdar dados ativos da página de origem ou excluir subpáginas, dependendo de como deseja que o lançamento se comporte.

   ![Solicitar inicialização](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. O fluxo de trabalho aparece na lista **Fluxos de trabalho** (clique nas reticências **...** no bloco **Fluxos de trabalho** para acessar essa lista).

## Criar (e traduzir) fluxo de trabalho de cópia de idioma para ativos {#create-and-translate-language-copy-workflow-for-assets}

Os fluxos de trabalho **Criar cópia de idioma** e **Criar e traduzir cópia de idioma** são abordados detalhadamente na seção [Criar cópias de idioma para arquivos](/help/assets/translate-assets.md).
