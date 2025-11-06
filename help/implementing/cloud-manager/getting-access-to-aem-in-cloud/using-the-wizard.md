---
title: Assistente de criação de projeto
description: Saiba mais sobre o assistente de criação de projetos para ajudar você a configurar rapidamente seu projeto após criar seu programa de produção.
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 96%

---

# Assistente de criação de projeto {#project-creation-wizard}

Após criar o programa de produção, o Cloud Manager oferece um assistente para criar um projeto AEM mínimo com base no [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) para começar rapidamente.

Siga estas etapas para criar um projeto de aplicativo AEM no Cloud Manager usando o assistente.

1. Crie um programa de produção seguindo as etapas descritas no documento [Criação de programas de produção](creating-production-programs.md)

1. Quando a configuração do programa for concluída, acesse a tela **Visão geral** do seu programa e veja o cartão de chamada para ação **Criar ramificação e projeto** na parte superior.

   ![Cartão de chamada para ação do assistente](assets/create-wizard1.png)

1. Clique em **Criar** para iniciar o assistente e confirmar o **Título** e o **Novo nome da ramificação** na janela **Criar ramificação e projeto**.

   ![Criar ramificação e projeto](assets/create-wizard2.png)

1. Opcionalmente, clique no divisor para revelar os parâmetros adicionais do seu projeto. Os valores padrão são fornecidos pelo Arquétipo de projeto AEM e geralmente não precisam ser alterados.

   ![Parâmetros adicionais do projeto](assets/create-wizard5.png)

1. Clique em **Criar** para iniciar o processo de criação do projeto.


O cartão **Criação de projeto em andamento** substitui o cartão de chamada para ação **Criar ramificação e projeto** na parte superior da tela **Visão geral do programa**.

![Criação do projeto em andamento](assets/create-wizard3.png)

Uma vez concluída a criação do programa, o cartão **Adicionar ambiente** substitui o cartão **Criação de projeto em andamento** na parte superior da tela **Visão geral do programa**.

![Adicionar ambiente](assets/create-wizard4.png)

Agora, você tem um projeto AEM com base no arquétipo que foi adicionado ao seu repositório Git para servir como base para o desenvolvimento do seu próprio projeto. Em seguida, você pode criar seus ambientes, nos quais pode implantar o código do projeto.

Consulte [Gerenciamento de ambientes](/help/implementing/cloud-manager/manage-environments.md) para saber como adicionar ou gerenciar ambientes.

>[!NOTE]
>
>O assistente está disponível somente para programas de produção. Como os [programas de sandbox](introduction-sandbox-programs.md#auto-creation) incluem criação automática de projeto, o assistente não é necessário.