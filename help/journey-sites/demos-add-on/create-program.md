---
title: Criar programa
description: Saiba como configurar um novo programa e pipeline para implantar o complemento.
exl-id: 06287618-0328-40b1-bba8-84002283f23f
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 53%

---


# Criar programa {#creating-a-program}

Saiba como configurar um novo programa e pipeline para implantar o complemento.

## A história até agora {#story-so-far}

No documento anterior da jornada do Complemento de Demonstrações de Referência do Adobe Experience Manager (AEM), [Entender a instalação do Complemento de Demonstração de Referência](installation.md), você aprendeu como funciona o processo de instalação do Complemento de Demonstrações de Referência, ilustrando como as diferentes partes funcionam juntas. Agora você deve:

* Ter uma compreensão básica do Cloud Manager.
* Entender como os pipelines entregam conteúdo e configuração ao AEM.
* Veja como os modelos podem criar novos sites pré-preenchidos com conteúdo de demonstração com apenas alguns cliques.

Este artigo se baseia nesses fundamentos e aborda a primeira etapa de configuração para criar um programa para fins de teste e usa um pipeline para implantar o conteúdo complementar.

## Objetivo {#objective}

Este documento ajuda você a entender como configurar um novo programa e um pipeline para implantar o complemento. Depois de ler, você poderá fazer o seguinte:

* Entenda e explique como usar o Cloud Manager para criar um programa.
* Ative o Complemento de demonstrações de referência para o novo programa.
* Execute um pipeline para poder implantar o conteúdo complementar.

## Criar um programa {#create-program}

Depois de fazer logon no Cloud Manager, você pode criar um programa de sandbox para fins de teste e demonstração.

>[!NOTE]
>
>Seu usuário deve ser um membro da organização com a função **Proprietário da empresa** no Cloud Manager para criar programas.

1. Faça logon no Adobe Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Depois de fazer logon, verifique se você está na organização correta, marcando-a no canto superior direito da tela. Se você for membro apenas de uma organização, essa etapa não será necessária.

   ![Visão geral do Cloud Manager](assets/cloud-manager.png)

1. Selecione **Adicionar programa** na parte superior direita da janela.

1. Na caixa de diálogo **Vamos criar o seu programa**:

   1. Forneça um **Nome de programa** para descrever o programa.
   1. Selecione **Configurar uma sandbox** para seu **Objetivo do Programa**
   1. Selecione **Continuar**.

   ![Caixa de diálogo Criar programa](assets/create-program.png)

1. Na caixa de diálogo **Configurar sua sandbox** na tabela **Soluções e Complementos**, expanda a entrada **Sites** na lista tocando ou clicando nela e marque **Demonstrações de Referência**.

   * Se você também quiser criar demonstrações para o AEM Screens, marque a opção **Screens** na lista. Selecione **Atualizar**.

   ![Seleção de complemento para demonstração de referência na configuração do programa](assets/select-reference-demo-add-on.png)


1. Selecione **Criar** e o Cloud Manager começará a configurar seu programa de sandbox. A tela de visão geral do programa é exibida e um breve banner de notificação indica que o processo foi iniciado. Um cartão foi adicionado à página de visão geral do novo programa. O processo de instalação leva alguns minutos para ser concluído.

1. Quando a configuração for concluída, o cartão do ambiente na página de visão geral mostrará seu status como **Pronto**. Selecione o cartão para poder abrir o ambiente.

   ![Criação do programa concluída](assets/ready.png)

1. Seu ambiente está pronto e o complemento agora está habilitado como uma opção, mas é necessário implantar o conteúdo da demonstração no AEM para que esteja disponível. Para fazer isso, clique no botão de reticências ao lado do pipeline Implantar em Desenvolvimento no cartão **Pipelines** e selecione **Executar**.

   ![Início](assets/run.png)

1. O pipeline é iniciado e você é direcionado a uma página detalhando o progresso da implantação. Você pode sair dessa tela enquanto o programa é criado e retornar posteriormente, se necessário.

   ![Implantação](assets/deployment.png)

O pipeline pode levar vários minutos para ser concluído. Uma vez concluído, o complemento e seu conteúdo de demonstração estarão disponíveis para uso no ambiente de criação do AEM.

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada do complemento de demonstração de referência do AEM, você deve:

* Saiba como usar o Cloud Manager para criar um programa.
* Saber como ativar o Complemento de demonstrações de referência para o programa.
* Poder executar um pipeline para implantar o conteúdo complementar.

Desenvolva esse conhecimento e prossiga com sua jornada de Complementos de Demonstração de Referência de AEM revisando a seguir [Criar um Site de Demonstração](create-site.md). Lá, você aprende a criar um site de demonstração no AEM com base em uma biblioteca de modelos pré-configurados que foram implantados pelo pipeline.

## Recursos adicionais {#additional-resources}

* [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=pt_BR) - Se quiser obter mais detalhes sobre os recursos do Cloud Manager, consulte diretamente os documentos técnicos detalhados.
