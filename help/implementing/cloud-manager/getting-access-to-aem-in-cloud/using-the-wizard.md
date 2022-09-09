---
title: Assistente de criação de projeto
description: Saiba mais sobre o assistente de criação de projetos para ajudar você a configurar rapidamente seu projeto após criar seu programa de produção.
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
source-git-commit: 93cb0ffa87f2338518c2a23de4e0a692031e1a71
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 4%

---

# Assistente de criação de projeto {#project-creation-wizard}

Após criar o programa de produção, o Cloud Manager oferece um assistente para criar um projeto de AEM mínimo com base na variável [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt_BR) para começar rapidamente.

Siga estas etapas para criar um projeto de aplicativo AEM no Cloud Manager usando o assistente.

1. Crie um programa de produção seguindo as etapas do documento [Criação de programas de produção](creating-production-programs.md)

1. Quando a configuração do programa for concluída, acesse o **Visão geral** do seu programa e veja o **Criar Ramificação e Projeto** cartão de chamada para ação na parte superior.

   ![Atendimento de chamada para ação do assistente](assets/create-wizard1.png)

1. Clique em **Criar** para iniciar o assistente e confirmar o **Título** e **Novo Nome da Ramificação** no **Criar uma Ramificação e Projeto** janela.

   ![Criar uma ramificação e um projeto](assets/create-wizard2.png)

1. Como opção, clique no divisor para revelar os parâmetros adicionais do seu projeto. Os valores padrão são fornecidos pelo Arquétipo de projeto AEM e geralmente não precisam ser alterados.

   ![Parâmetros adicionais do projeto](assets/create-wizard5.png)

1. Clique em **Criar** para iniciar o processo de criação do projeto.


A **Criação de projeto em progresso** agora substitui **Criar Ramificação e Projeto** cartão de chamada para ação como parte superior do **Visão geral do programa** tela.

![Criação de projeto em andamento](assets/create-wizard3.png)

Uma vez concluída a criação do programa, um **Adicionar ambiente** substitui **Criação de projeto em progresso** na parte superior do **Visão geral do programa** tela.

![Adicionar ambiente](assets/create-wizard4.png)

Agora, você tem um projeto de AEM com base no arquétipo de AEM adicionado ao seu repositório Git para servir como base para o desenvolvimento do seu próprio projeto. Em seguida, você pode criar seus ambientes, onde pode implantar o código do projeto.

Consulte o documento [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para saber como adicionar ou gerenciar ambientes.

>[!NOTE]
>
>O assistente só está disponível para programas de produção. Porque [programas sandbox](introduction-sandbox-programs.md#auto-creation) incluir criação automática de projeto, o assistente não é necessário.