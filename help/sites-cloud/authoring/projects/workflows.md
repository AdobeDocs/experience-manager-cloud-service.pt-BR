---
title: Trabalhar com fluxos de trabalho de projeto
description: Vários fluxos de trabalho de projeto estão disponíveis imediatamente.
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 43%

---

# Trabalhar com fluxos de trabalho de projeto {#working-with-project-workflows}

Os fluxos de trabalho de projeto disponíveis prontos para uso incluem o seguinte:

* **Fluxo de trabalho para aprovação de projeto** - Esse fluxo de trabalho permite atribuir conteúdo a um usuário, analisar esse conteúdo e depois aprová-lo.
* **Solicitar inicialização** - um fluxo de trabalho que solicita uma inicialização.
* **Solicitar página de aterrissagem** - esse fluxo de trabalho solicita uma página de aterrissagem.
* **Solicitar email** - Fluxo de trabalho para solicitar um email.
* **Criar e traduzir cópia DAM e Criar cópia de idioma DAM** : cria binários, metadados e tags traduzidos para ativos e pastas.

Dependendo do Modelo de projeto selecionado, há determinados fluxos de trabalho disponíveis:

|   | **Projeto simples** | **Projeto de tradução** |
|---|:-:|:-:|
| Fluxo de trabalho de aprovação de projeto | x |  |
| Solicitar inicialização | x |  |
| Solicitar página de aterrissagem | x |  |
| Solicitar email | x | |
| Criar cópia de idioma do DAM&amp;ast; |  | x |
| Criar e traduzir cópia de idioma do DAM;&amp;ast; |   | x |

>[!NOTE]
>
>&amp;ast; Esses fluxos de trabalho não são iniciados no bloco **Fluxo de trabalho** em Projetos. Consulte [Criação de cópias de idioma para ativos](/help/sites-cloud/administering/translation/managing-projects.md).

As etapas para iniciar e concluir workflows são as mesmas, independentemente do workflow escolhido. Somente as etapas são alteradas.

Você inicia um fluxo de trabalho diretamente nos Projetos (exceto para Criar cópia de idioma DAM ou Criar e traduzir cópia de idioma DAM). Informações sobre quaisquer tarefas pendentes em um projeto estão listadas no **Tarefas** bloco. As notificações para tarefas que precisam ser concluídas são exibidas ao lado do ícone do usuário.

Para obter mais informações sobre como trabalhar com fluxos de trabalho no AEM, consulte o seguinte:

* [Participar de fluxos de trabalho](/help/sites-cloud/authoring/workflows/participating.md)
* [Aplicação de fluxos de trabalho a páginas](/help/sites-cloud/authoring/workflows/applying.md)
* [Configuração de fluxos de trabalho](/help/sites-cloud/administering/workflows-administering.md)

Esta seção descreve os fluxos de trabalho disponíveis para Projetos.

## Fluxo de trabalho para aprovação de projeto {#project-approval-workflow}

No fluxo de trabalho Aprovação de projeto, você atribui o conteúdo a um usuário, revisa-o e o aprova.

1. Em seu projeto simples, selecione o sinal de **`+`** no bloco **Fluxos de trabalho** e selecione **Fluxo de trabalho para aprovação de projeto**.
1. Insira um título e selecione a quem atribuí-lo na lista Equipe. Se aplicável, insira uma descrição, um caminho de conteúdo, uma prioridade de tarefa e uma data de vencimento.

   ![Solicitar aprovação](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. A tarefa aparece na variável **Tarefas** bloco.

## Solicitar fluxo de trabalho de inicialização {#request-launch-workflow}

Esse workflow permite solicitar um lançamento.

1. No projeto simples, selecione o sinal **+** no bloco **Fluxos de trabalho** e selecione **Solicitar fluxo de trabalho de inicialização**.
1. Insira um título para a inicialização e forneça o caminho de origem da inicialização. Você também pode adicionar uma descrição e uma data de ativação, se aplicável. Selecione Herdar dados online da página de origem ou excluir subpáginas, dependendo de como você deseja que o lançamento se comporte.

   ![Solicitar inicialização](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. O fluxo de trabalho aparece na lista **Fluxos de trabalho** (clique nas reticências **...** no bloco **Fluxos de trabalho** para acessar essa lista).

## Criar (e traduzir) fluxo de trabalho de cópia de idioma para ativos {#create-and-translate-language-copy-workflow-for-assets}

Os fluxos de trabalho **Criar cópia de idioma** e **Criar e traduzir cópia de idioma** são abordados detalhadamente na seção [Criar cópias de idioma para ativos](/help/assets/translate-assets.md).
