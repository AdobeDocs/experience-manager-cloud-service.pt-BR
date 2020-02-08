---
title: Criação de um programa - Serviço em nuvem
description: Criação de um programa - Serviço em nuvem
translation-type: tm+mt
source-git-commit: 57206e36725e28051b2468d47da726e318bd763b

---


# Criação de um programa {#create-a-program}

A solução nativa da nuvem fornece ao usuário as permissões necessárias e a capacidade de criar um programa em um modelo de autoatendimento.

Um assistente de criação de programa solicitará que o usuário envie detalhes, dependendo do objetivo do usuário de criar o programa dentro dos limites do que está disponível para o cliente ou organização específica.

Se o acesso ao Cloud Manager for iniciado pela primeira vez ou se não houver programas no locatário, o usuário verá a tela **Criar seu primeiro programa** . Se o usuário selecionar *Esc* ou clicar fora da caixa de diálogo, a seguinte tela será exibida:

![](assets/create-program1.png)


## Usando o Assistente para Criar Programa {#using-create-program-wizard}

Dependendo do objetivo do usuário de criar o programa dentro dos limites do que está disponível para o cliente/organização específico, um assistente de criação de programa solicitará que o usuário envie um ou mais detalhes.

![](assets/create-program-2.png)

>[!NOTE]
>Se um programa já existir, você verá **Adicionar programa** na parte superior direita da página de aterrissagem, como mostrado na figura abaixo.

![](assets/create-program-add.png)

## Criação de um programa de demonstração {#create-demo-program}

>[!NOTE]
>
Um programa de demonstração é análogo a um programa sandbox na interface do usuário do Cloud Manager.

Siga as etapas abaixo para criar um programa sandbox:

1. No assistente de criação de programa, selecione **Configurar uma demonstração**. O usuário envia o nome do programa antes de selecionar **Criar**.

   ![](assets/create-program-setupdemo.png)

1. O usuário visualizará o novo cartão de programa da caixa de proteção na página de aterrissagem e poderá passar o mouse sobre ele para selecionar o ícone do Gerenciador de nuvem para navegar até a página de visão geral do Gerenciador de nuvem. O cartão informará o usuário sobre o status da configuração automática do programa de sandbox recém-criado. O usuário verá a progressão.

   ![](assets/program-create-setupdemo2.png)

1. Depois que o programa for configurado e a etapa de criação do projeto for concluída, o usuário poderá acessar o link **Gerenciar Git** , como mostra a figura abaixo:

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >Para saber mais sobre como acessar e gerenciar o Repositório Git usando o Gerenciamento de Conta Git de Autoatendimento na interface do usuário do Cloud Manager, consulte [Acesso ao Git](/help/implementing/cloud-manager/accessing-git.md).


1. Depois que o ambiente de desenvolvimento é criado, o usuário pode **acessar o link AEM** , como mostrado na figura abaixo:

   ![](assets/create-program-5.png)

1. Quando a implantação do pipeline de não-produção no desenvolvimento estiver concluída, o assistente orientará o usuário a acessar o AEM (no desenvolvimento) ou a implantar o código no ambiente de desenvolvimento:

   ![](assets/create-program-setup-deploy.png)


## Criando um programa regular {#create-regular-program}

Um programa *regular* destina-se a um usuário familiarizado com o AEM e o Cloud Manager e está pronto para começar a escrever, criar e testar o código com o objetivo de implantá-lo na Produção.

Siga as etapas abaixo para criar um programa regular:

1. Selecione **Configurar para produção** no assistente Criar programa para criar um programa regular. O usuário pode aceitar o nome padrão do programa ou editá-lo antes de selecionar **Continuar**.

   ![](assets/set-up-prod1.png)

1. O usuário selecionará as soluções que serão incluídas no programa na tela que serão apresentadas após a tela acima.



   >[!NOTE]
   >
   >A tela abaixo é exibida somente para o segmento de clientes que compraram mais de uma solução. Para clientes que compraram apenas uma solução, a tela de seleção da solução abaixo não será exibida.

   ![](assets/set-up-prod2.png)

1. Depois de selecionar as soluções, clique em **Criar**.

   ![](assets/set-up-prod3.png)

1. Depois de ver o cartão do programa na página de aterrissagem, passe o mouse sobre ele para selecionar o ícone do Gerenciador de nuvem para navegar até a página **Visão geral** do Gerenciador de nuvem.

   ![](assets/set-up-prod4.png)

1. O cartão principal de chamada para ação guiará o usuário a criar um ambiente, criar um pipeline de não-produção e, finalmente, um pipeline de produção.
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >Um programa regular não tem o recurso de configuração **automática** .





