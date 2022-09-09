---
title: Acesso a repositórios
description: Saiba como acessar e gerenciar o repositório Git usando o gerenciamento de conta Git de autoatendimento do Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 4729574eb31e01077f0d2a35efcef6d134f6aa5c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---

# Acesso a repositórios {#accessing-repos}

Saiba como acessar e gerenciar o repositório Git usando o gerenciamento de conta Git de autoatendimento do Cloud Manager.

## Usando o Gerenciamento de Conta do Repositório de Autoatendimento {#self-service-repos}

O Cloud Manager facilita a recuperação das informações do repositório usando o **Acessar informações do repositório** botão disponível de forma destacada na placa de pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegar para **Pipelines** cartão de seu **Visão geral do programa** e localize a **Acessar informações do repositório** para acessar e gerenciar o repositório Git.

   ![Botão Acessar informações do repositório no cartão Ambientes](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Clique no botão **Exibir informações do acordo de recompra** para abrir uma caixa de diálogo para exibir:

   * O URL para o repositório Git do Cloud Manager.
   * O nome de usuário do git.
   * A senha git, cujo valor é mostrado quando a variável **Gerar senha** é clicado.

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Usando essas credenciais, o usuário pode clonar uma cópia local do repositório e fazer alterações nesse repositório local, e quando pronto pode confirmar qualquer alteração de código no repositório de código remoto no Cloud Manager.

O **Acessar informações do repositório** também está disponível no **Não produção** guia pipeline da **Pipelines** cartão.

![Botão Acessar informações do acordo de recompra na guia não produção](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>O **Acessar informações do repositório** está visível para usuários com **Desenvolvedor** ou **Gerenciador de implantação** funções.
