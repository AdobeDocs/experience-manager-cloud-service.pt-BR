---
title: Trabalhar com fluxos de trabalho de projeto
description: Há uma variedade de fluxos de trabalho de projeto disponíveis para uso imediato.
exl-id: a5c9a6df-7def-43f3-b41b-524a4f4211e9
source-git-commit: 89972691dadb9573160ba16a220c5b7cb3ae9742
workflow-type: ht
source-wordcount: '452'
ht-degree: 100%

---

# Trabalhar com fluxos de trabalho de projeto {#working-with-project-workflows}

Os fluxos de trabalho de projeto disponíveis para uso imediato incluem os seguintes:

* **Fluxo de trabalho para aprovação de projeto** - esse fluxo de trabalho permite atribuir conteúdo a um usuário, analisar esse conteúdo e depois aprová-lo.
* **Solicitar inicialização** - um fluxo de trabalho que solicita uma inicialização.
* **Solicitar página de aterrissagem** - esse fluxo de trabalho solicita uma página de aterrissagem.
* **Solicitar email** - Fluxo de trabalho para solicitar um email.
* **Criar e traduzir cópia DAM e Criar cópia de idioma DAM** - Cria binários, metadados e tags traduzidos para ativos e pastas.

Dependendo de qual modelo de projeto você selecionar, certos fluxos de trabalho estarão disponíveis:

|  | **Projeto simples** | **Projeto de tradução** |
|---|:-:|:-:|
| Fluxo de trabalho de aprovação de projeto | x |  |
| Solicitar inicialização | x |  |
| Solicitar página de aterrissagem | x |  |
| Solicitar email | x |  |
| Criar cópia de idioma do DAM&amp;ast; |  | x |
| Criar e traduzir cópia de idioma do DAM;&amp;ast; |  | x |

>[!NOTE]
>
>&amp;ast; Esses fluxos de trabalho não são iniciados no bloco **Fluxo de trabalho** em Projetos. Consulte [Criação de cópias de idioma para ativos.](/help/sites-cloud/administering/translation/managing-projects.md)

As etapas para iniciar e concluir fluxos de trabalho são as mesmas, independentemente do fluxo de trabalho escolhido. Apenas as etapas mudam.

Você inicia um fluxo de trabalho diretamente em Projetos (exceto para Criar cópia de idioma DAM ou Criação e tradução DAM da cópia de idioma). Informações sobre quaisquer tarefas pendentes em um projeto são listadas no bloco **Tarefas**. Notificações de tarefas que precisam ser concluídas aparecem ao lado do ícone de usuário.

Para obter mais informações sobre como trabalhar com fluxos de trabalho no AEM, consulte o seguinte:

* [Participar de fluxos de trabalho](/help/sites-cloud/authoring/workflows/participating.md)
* [Aplicação de fluxos de trabalho a páginas](/help/sites-cloud/authoring/workflows/applying.md)
* [Configuração de fluxos de trabalho](/help/sites-cloud/administering/workflows-administering.md)

Esta seção descreve os fluxos de trabalho disponíveis para Projetos.

## Fluxo de trabalho para aprovação do projeto {#project-approval-workflow}

No fluxo de trabalho Aprovação de projeto, você atribui conteúdo a um usuário e depois revisa e aprova esse conteúdo.

1. Em seu projeto simples, selecione o sinal de **`+`** no bloco **Fluxos de trabalho** e selecione **Fluxo de trabalho para aprovação de projeto**.
1. Insira um título e selecione a quem ele deve ser atribuído na lista Equipe. Se aplicável, insira uma descrição, um caminho de conteúdo, uma prioridade de tarefa e uma data de vencimento.

   ![Solicitar aprovação](/help/sites-cloud/authoring/assets/projects-approval.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. A tarefa é exibida no bloco **Tarefas**.

## Fluxo de trabalho Solicitar lançamento {#request-launch-workflow}

Esse fluxo de trabalho permite solicitar um lançamento.

1. No projeto simples, selecione o sinal **+** no bloco **Fluxos de trabalho** e selecione **Solicitar fluxo de trabalho de inicialização**.
1. Insira um título para o lançamento e forneça o caminho da origem de lançamento. Você também pode adicionar uma descrição e uma data de colocação ao vivo, se aplicável. Selecione Herdar dados online de página fonte ou Excluir subpáginas, dependendo de como você deseja que o lançamento se comporte.

   ![Solicitar inicialização](/help/sites-cloud/authoring/assets/projects-request-launch.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. O fluxo de trabalho aparece na lista **Fluxos de trabalho** (clique nas reticências **...** no bloco **Fluxos de trabalho** para acessar essa lista).

## Criar (e traduzir) fluxo de trabalho de cópia de idioma para ativos {#create-and-translate-language-copy-workflow-for-assets}

Os fluxos de trabalho **Criar cópia de idioma** e **Criar e traduzir cópia de idioma** são abordados detalhadamente na seção [Criar cópias de idioma para ativos](/help/assets/translate-assets.md).
