---
title: Informações de acesso do repositório
description: Saiba como acessar e gerenciar repositórios Git gerenciados pelo Adobe usando o gerenciamento de conta Git por autoatendimento do Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0b39fc4dcaf86d436547d3941b1f12bca8c5bc9b
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 11%

---


# Informações de acesso do repositório {#accessing-repos}

Saiba como acessar e gerenciar repositórios Git gerenciados pelo Adobe usando o gerenciamento de conta Git por autoatendimento do Cloud Manager.

## Acessando Informações do Repositório na Página Visão Geral {#overview-page}

O Cloud Manager facilita a recuperação das informações de acesso do repositório para repositórios gerenciados pelo Adobe usando o **Acessar informações do repositório** botão disponível de forma destacada no cartão de pipeline.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até **Pipelines** do seu **Visão geral do programa** página.

   ![Botão Acessar informações do repositório no cartão Ambientes](assets/pipelines-card.png)

1. Toque ou clique no **Acessar informações do repositório** botão para abrir o **Informações do repositório** caixa de diálogo e exibição:

   * O nome de usuário do Git.
   * A senha do Git.
   * A URL do repositório Git do Cloud Manager.
   * Comandos Git pré-criados para adicionar rapidamente um controle remoto ao repositório Git e ao código de push.

   ![Janela Informações do repositório](assets/repository-info.png)

1. Para acessar a senha, uma nova senha deve ser gerada. Para fazer isso, toque ou clique no **Gerar senha** botão.

1. Confirme a geração de senha no **Tem certeza...** tocando ou clicando em **Gerar senha**.

   ![Confirmar geração de senha](assets/confirm-password-generation.png)

1. A senha é gerada e está visível para cópia no **Senha** campo.

   * Gerar uma senha invalidará a senha anterior.
   * O Cloud Manager não salvará a senha. É sua responsabilidade salvar esta senha com segurança.
   * Como o Cloud Manager não salva a senha, se você a perder, deverá gerar novamente uma nova senha.

   ![Exemplo de senha gerada](assets/generated-password.png)

Usando essas credenciais, você pode clonar uma cópia local do repositório, fazer alterações nele e, quando pronto, confirmar qualquer alteração de código no repositório de código remoto no Cloud Manager.

>[!NOTE]
>
>* A opção **Acessar informações do repositório** está visível para usuários com funções de **Desenvolvedor** ou **Gerente de implantação**.
>* A variável **Acessar informações do repositório** botão somente exibe as informações de acesso do repositório para repositórios gerenciados pelo Adobe. Acessar informações sobre [repositórios privados](private-repositories.md) não está disponível no Cloud Manager.

## Acessando informações do repositório na janela Repositórios {#repositories-window}

Um **Acessar informações do repositório** também está disponível na barra de ferramentas do [**Repositórios** janela.](managing-repositories.md) ele exibe as mesmas informações sobre o acesso a repositórios gerenciados pelo Adobe.

## Revogação de uma senha de acesso {#revoke-password}

Você pode revogar uma senha de acesso a qualquer momento. Para isso, [crie um tíquete de suporte para esta solicitação.](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support)

O ticket será tratado com alta prioridade e deverá ser revogado dentro de um dia.
