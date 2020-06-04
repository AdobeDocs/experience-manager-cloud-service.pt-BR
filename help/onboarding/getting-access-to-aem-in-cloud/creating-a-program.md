---
title: Criação de um Programa - Serviço em nuvem
description: Criação de um Programa - Serviço em nuvem
translation-type: tm+mt
source-git-commit: b2549ac13f996449bc41ac18ba6afbf22e116597
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---


# Criação de um programa {#create-a-program}

A solução nativa da nuvem fornece ao usuário as permissões necessárias e a capacidade de criar um programa em um modelo de autoatendimento.

Um assistente de criação de programas solicitará que o usuário envie detalhes, dependendo do objetivo do usuário de criar o programa dentro dos limites do que está disponível para o cliente ou organização específica.

No evento do primeiro acesso ao Cloud Manager ou se não houver programas no locatário, o usuário visualizará a tela **Criar seu primeiro Programa** . Se o usuário selecionar *Esc* ou clicar fora da caixa de diálogo, a tela a seguir será exibida:

![](assets/create-program1.png)


## Usando o Assistente para Criar Programa {#using-create-program-wizard}

Dependendo do objetivo do usuário de criar o programa dentro dos limites do que está disponível para o cliente/organização específico, um assistente de criação de programas solicitará que o usuário envie um ou mais detalhes.

![](assets/create-sandbox.png)

>[!NOTE]
>If a program already exists, then you will see **Add Program** on the top right of the landing page, as shown in the figure below.

![](assets/create-program-add.png)

## Criação de um Programa Sandbox {#create-sandbox-program}

Siga as etapas abaixo para criar um programa sandbox:

1. No assistente para criar programas, selecione **Configurar uma caixa de proteção**. O usuário envia o nome do programa antes de selecionar **Criar**.

   ![](assets/create-sandbox.png)

1. O usuário verá o novo cartão de programa da caixa de proteção na landing page e poderá passar o mouse sobre ele para selecionar o ícone do Gerenciador de nuvem para navegar até a página de visão geral do Gerenciador de nuvem. O cartão informará o usuário sobre o status da configuração automática do programa sandbox recém-criado. O usuário verá a progressão.

   ![](assets/program-create-setupdemo2.png)

1. Após a configuração do programa e a etapa de criação do projeto ser concluída, o usuário poderá acessar o link **Gerenciar Git** , como mostra a figura abaixo:

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >Para saber mais sobre como acessar e gerenciar o Repositório Git usando o Gerenciamento de Conta Git de Autoatendimento na interface do usuário do Cloud Manager, consulte [Acesso ao Git](/help/implementing/cloud-manager/accessing-git.md).


1. Depois que o ambiente de desenvolvimento é criado, o usuário pode **acessar o link AEM** , como mostrado na figura abaixo:

   ![](assets/create-program-5.png)

1. Quando a implantação do pipeline de não-produção no desenvolvimento estiver concluída, o assistente orientará o usuário a acessar o AEM (no desenvolvimento) ou a implantar o código no ambiente de desenvolvimento:

   ![](assets/create-program-setup-deploy.png)

   >[!NOTE]
   >Você também pode editar, alternar ou adicionar um programa na página Visão geral do Cloud Manager, como mostrado abaixo:

   ![](assets/create-program-a1.png)

## Excluindo um Programa Sandbox {#delete-sandbox-program}

Um usuário do Programa Sandbox no Proprietário *do* Negócio ou na função *Gerenciador* de Implantação no Gerenciador de Nuvem pode excluir seu conjunto de ambientes de Produção e Estágio por meio da interface do usuário do Gerenciador de Nuvem.

A opção de exclusão está disponível no cartão de Ambiente na página *Visão geral* e na página **Ambientes** . Selecionar a opção de exclusão em Produção ou Estágio também exclui a outra no conjunto.

## Criação de um Programa regular {#create-regular-program}

Um programa *regular* destina-se a um usuário familiarizado com o AEM e o Cloud Manager e que está pronto para o start de escrever, criar e testar o código com o objetivo de implantá-lo na Produção.

Siga as etapas abaixo para criar um programa comum:

1. Selecione **Configurar para produção** no assistente Criar Programa para criar um programa comum. O usuário pode aceitar o nome do programa padrão ou editá-lo antes de selecionar **Continuar**.

   ![](assets/create-prod1.png)

1. O usuário selecionará as soluções a serem incluídas no programa na tela que serão apresentadas após a tela acima.



   >[!NOTE]
   >
   >A tela abaixo é exibida somente para o segmento de clientes que compraram mais de uma solução. Para os clientes que compraram apenas uma solução, a tela de seleção da solução abaixo não será exibida.

   ![](assets/set-up-prod2.png)

1. Depois de selecionar as soluções, clique em **Criar**.

   ![](assets/set-up-prod3.png)

1. Depois de ver seu cartão de programa na landing page, passe o mouse sobre ele para selecionar o ícone do Gerenciador de nuvem para navegar até a página **Visão geral** do Gerenciador de nuvem.

   ![](assets/set-up-prod4.png)

1. O cartão principal de chamada para ação guiará o usuário a criar um ambiente, criar um pipeline de não-produção e, finalmente, um pipeline de produção.
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >A regular program does not have **Auto-setup** feature.





