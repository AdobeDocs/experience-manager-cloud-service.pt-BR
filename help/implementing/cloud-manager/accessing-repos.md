---
title: Acessar repositórios
seo-title: Acessar repositórios
description: Esta página descreve como você pode acessar e gerenciar o repositório Git.
seo-description: Siga esta página para saber como acessar e gerenciar o repositório Git.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 9898baebfbb43059f2497fa6b4db801eef12a9d0
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 4%

---

# Acessar repositórios {#accessing-repos}

Você pode acessar e gerenciar seu Repositório Git usando o Gerenciamento de conta Git de Autoatendimento da interface do usuário do Cloud Manager.

## Usando Repositórios de Autoatendimento Gerenciamento de Conta {#self-service-repos}

Use o botão **Acessar informações do repositório** disponível na interface do usuário do Cloud Manager, mais proeminentemente no cartão de pipeline.

1. Navegue até o cartão **Pipelines** da página **Visão geral do programa**.

1. Você visualizará a opção **Acessar Informações do Repo** para acessar e gerenciar seu Repositório Git.

   ![](assets/repos/access-repo1.png)

   Além disso, se você selecionar a guia pipeline **Non-Production**, também visualizará a opção **Access Repo Info** lá.

   ![](assets/repos/access-repo-nonprod.png)

   >[!NOTE]
   >A opção **Access Repo Info** está visível para os usuários na função Desenvolvedor ou Gerenciador de Implantação. Clicar nesse botão abre uma caixa de diálogo que permite ao usuário localizar o URL de seu Repositório Git do Cloud Manager junto com seu nome de usuário e senha.

   ![](assets/repos/access-repo-create.png)

   As considerações importantes para gerenciar seu Git no Cloud Manager são:

   * **URL**: O URL do repositório
   * **Nome de usuário**: O nome de usuário
   * **Senha**: o valor exibido quando o botão **Gerar senha** é clicado.


      >[!NOTE]
      >Um usuário pode fazer check-out de uma cópia de seu código e fazer alterações no repositório de código local. Quando pronto, o usuário pode confirmar as alterações de código no repositório de código remoto no Cloud Manager.
