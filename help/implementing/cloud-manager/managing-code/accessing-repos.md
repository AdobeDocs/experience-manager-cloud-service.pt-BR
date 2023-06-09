---
title: Acesso a repositórios
description: Saiba como acessar e gerenciar o repositório Git usando o gerenciamento de conta Git por autoatendimento do Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 9ec45753f56d0576e75f148ca0165c0ccd621f23
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 98%

---

# Acesso a repositórios {#accessing-repos}

Saiba como acessar e gerenciar o repositório Git usando o gerenciamento de conta Git por autoatendimento do Cloud Manager.

## Uso do gerenciamento de conta no repositório de autoatendimento {#self-service-repos}

O Cloud Manager facilita a recuperação das informações do seu repositório usando o botão **Acessar informações do repositório** disponível de forma destacada no cartão de pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse o cartão **Pipelines** a partir da página **Visão geral do programa** e localize o botão **Acessar informações do repositório** para acessar e gerenciar o repositório Git.

   ![Botão Acessar informações do repositório no cartão Ambientes](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Clique no botão **Exibir informações do repositório** para abrir uma caixa de diálogo para exibir:

   * A URL do repositório Git do Cloud Manager.
   * O nome de usuário do Git.
   * A senha do Git, cujo valor é mostrado ao clicar no botão **Gerar senha**.

   ![Exibição de Informações do Repositório](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Usando essas credenciais, o usuário pode clonar uma cópia local do repositório e fazer alterações nele, e quando pronto, pode confirmar qualquer alteração no repositório de códigos remotos no Cloud Manager.

A opção **Acessar informações do repositório** também está disponível na guia **Não produção** do cartão **Pipelines**.

![Botão Acessar informações do repositório na guia Não produção](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>A opção **Acessar informações do repositório** está visível para usuários com funções de **Desenvolvedor** ou **Gerente de implantação**.
