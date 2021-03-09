---
title: Criação de um programa - Cloud Service
description: Criação de um programa - Cloud Service
translation-type: tm+mt
source-git-commit: d85c0e9035ee09cf86aeea1cae20d545823eaca0
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---


# Criação de um programa {#create-a-program}

A solução nativa em nuvem fornece ao usuário as permissões necessárias e a capacidade de criar um programa em um modelo de autoatendimento.

Um assistente de criação de programas solicitará que o usuário envie detalhes, dependendo do objetivo do usuário em criar o programa dentro dos limites do que está disponível para o cliente ou organização específica.

No caso de acesso pela primeira vez ao Cloud Manager ou se não houver programas no locatário, o usuário verá a tela **Create your first Program** . Se o usuário selecionar *Esc* ou clicar fora da caixa de diálogo, a tela a seguir será exibida:

![](assets/create-program1.png)


## Usando o Assistente de Criação de Programa {#using-create-program-wizard}

Dependendo do objetivo do usuário ao criar o programa dentro dos limites do que está disponível para o cliente/organização específico, um assistente de criação de programa solicitará que o usuário envie um ou mais detalhes.

![](assets/create-sandbox.png)


## Criação de um programa de sandbox {#create-sandbox-program}

Siga as etapas abaixo para criar um programa sandbox:

1. No assistente criar programa, selecione **Configurar uma sandbox**. O usuário envia o nome do programa antes de selecionar **Criar**.

   ![](assets/create-sandbox.png)

1. O usuário verá o novo cartão de programa sandbox na página de aterrissagem e poderá passar o mouse sobre ele para selecionar o ícone do Cloud Manager e navegar até a página de visão geral do Cloud Manager. O cartão informará o usuário sobre o status da configuração automática do programa sandbox recém-criado. O usuário verá a progressão.

   ![](assets/program-create-setupdemo2.png)

1. Depois que o programa for configurado e a etapa de criação do projeto for concluída, o usuário poderá acessar o link **Gerenciar Git**, conforme mostrado na figura abaixo:

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >Para saber mais sobre como acessar e gerenciar o Repositório Git usando o Gerenciamento de Conta Git de Autoatendimento da interface do usuário do Cloud Manager, consulte [Acessando o Git](/help/implementing/cloud-manager/accessing-git.md).


1. Depois que o ambiente de desenvolvimento é criado, o usuário pode **Acessar o AEM**, conforme mostrado na figura abaixo:

   ![](assets/create-program-5.png)

1. Quando o pipeline de não produção implantado no desenvolvimento estiver concluído, o assistente orientará o usuário a acessar o AEM (no desenvolvimento) ou implantar o código no ambiente de desenvolvimento:

   ![](assets/create-program-setup-deploy.png)

   >[!NOTE]
   >Você também pode editar, alternar ou adicionar um programa na página Visão geral do Cloud Manager , conforme mostrado abaixo:

   ![](assets/create-program-a1.png)

## Excluindo um Programa de sandbox {#delete-sandbox-program}

Um usuário do Programa de sandbox na função *Proprietário comercial* ou *Gerenciador de implantação* no Cloud Manager pode excluir seu conjunto de ambientes de produção e preparo por meio da interface do usuário do Cloud Manager.

>[!NOTE]
>Selecionar a opção de exclusão no ambiente de produção também exclui o ambiente de preparo no mesmo conjunto, e vice-versa.

A opção de exclusão está disponível na landing page, conforme mostrado abaixo:

![](assets/delete-sandbox1.png)

Ou,

Selecione **Excluir programa** na página **Visão geral do programa** para excluir seu programa de sandbox.

![](assets/delete-sandbox2.png)


## Criação de um programa regular {#create-regular-program}

Um programa *Regular* destina-se a um usuário familiarizado com o AEM e o Cloud Manager e está pronto para começar a escrever, criar e testar o código com o objetivo de implantá-lo em produção.

Siga as etapas abaixo para criar um programa regular:

1. Selecione **Configurar para produção** no assistente Criar programa para criar um programa regular. O usuário pode aceitar o nome padrão do programa ou editá-lo antes de selecionar **Continuar**.

   ![](assets/create-prod1.png)

1. O usuário selecionará soluções que serão incluídas no programa na tela que será apresentada após a tela acima.



   >[!NOTE]
   >
   >A tela abaixo é exibida somente para o segmento de clientes que compraram mais de uma solução. Para clientes que compraram apenas uma solução, a tela de seleção de solução abaixo não será exibida.

   ![](assets/set-up-prod2.png)

1. Depois de selecionar as soluções, clique em **Criar**.

   ![](assets/set-up-prod3.png)

1. Depois de ver o cartão do programa na página de aterrissagem, passe o mouse sobre ele para selecionar o ícone do Cloud Manager e navegue até a página **Visão geral** do Cloud Manager.

   ![](assets/set-up-prod4.png)

1. O cartão principal de chamada para ação guiará o usuário para criar um ambiente, criar um pipeline de não produção e, por fim, um pipeline de produção.
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >Um programa regular não tem o recurso **Configuração automática**.





