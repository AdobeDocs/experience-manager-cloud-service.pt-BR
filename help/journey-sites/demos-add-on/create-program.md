---
title: Criar programa
description: Saiba como configurar um novo programa e pipeline para implantar o complemento.
exl-id: 06287618-0328-40b1-bba8-84002283f23f
source-git-commit: 7c33a618f474914ca80dff525552017c55a32517
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 68%

---


# Criar programa {#creating-a-program}

Saiba como configurar um novo programa e pipeline para implantar o complemento.

## A história até agora {#story-so-far}

No documento anterior da jornada do Complemento de demonstrações de referência do AEM, [Entender a instalação do complemento de demonstração de referência,](installation.md) você aprendeu como funciona o processo de instalação do Complemento de demonstrações de referência, ilustrando como as diferentes partes funcionam juntas. Agora você deve:

* Ter uma compreensão básica do Cloud Manager.
* Entender como os pipelines entregam conteúdo e configuração ao AEM.
* Veja como os modelos podem criar novos sites pré-preenchidos com conteúdo de demonstração com apenas alguns cliques.

Este artigo se baseia nesses fundamentos e aborda a primeira etapa de configuração para criar um programa para fins de teste e usa um pipeline para implantar o conteúdo complementar.

## Objetivo {#objective}

Este documento ajuda você a entender como configurar um novo programa e um pipeline para implantar o complemento. Depois de ler esse documento, você deverá:

* Entender como usar o Cloud Manager para criar um novo programa.
* Saber como ativar o complemento de demonstrações de referência para o novo programa.
* Poder executar um pipeline para implantar o conteúdo complementar.

## Criar um programa {#create-program}

Depois de fazer logon no Cloud Manager, você pode criar um novo programa de sandbox para fins de teste e demonstração.

>[!NOTE]
>
>Seu usuário deve ser membro do **Proprietário da empresa** no Cloud Manager em sua organização para criar programas.

1. Faça logon no Adobe Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. Depois de fazer logon, verifique se você está na organização correta, marcando-a no canto superior direito da tela. Se você for membro apenas de uma organização, essa etapa não será necessária.

   ![Visão geral do Cloud Manager](assets/cloud-manager.png)

1. Toque ou clique em **Adicionar programa** na parte superior direita da janela.

1. No **Vamos criar o seu programa** diálogo:

   1. Forneça um **Nome de programa** para descrever o programa.
   1. Toque ou clique em **Configurar uma sandbox** para o **Objetivo do programa**
   1. Toque ou clique em **Continuar**.

   ![Caixa de diálogo Criar programa](assets/create-program.png)

1. No **Configurar sua sandbox** no **Soluções e complementos** , expanda a **Sites** entrada na lista tocando ou clicando nela e, em seguida, marque **Demonstrações de referência**.

   * Se você também quiser criar demonstrações para o AEM Screens, marque a opção **Screens** na lista também. Toque ou clique em **Atualizar**.

   ![Seleção de complemento para demonstração de referência na configuração do programa](assets/select-reference-demo-add-on.png)


1. Toque ou clique **Criar** O e o Cloud Manager começam a configurar seu programa de sandbox. Você é levado à tela de visão geral do programa e uma breve notificação de banner indica que o processo foi iniciado. Um cartão foi adicionado à página de visão geral do novo programa. O processo de instalação levará alguns minutos para ser concluído.

1. Quando a configuração for concluída, o cartão do ambiente na página de visão geral mostrará seu status como **Pronto**. Toque ou clique no cartão para abrir o ambiente.

   ![Criação do programa concluída](assets/ready.png)

1. Seu ambiente está pronto e o complemento agora está habilitado como uma opção, mas o conteúdo da demonstração deve ser implantado no AEM para estar disponível. Para fazer isso, toque ou clique no botão de reticências ao lado do pipeline Implantar no desenvolvimento na **Pipelines** e selecione **Executar**.

   ![Início](assets/run.png)

1. O pipeline é iniciado e você é direcionado a uma página detalhando o progresso da implantação. Você pode sair dessa tela enquanto o programa é criado e retornar posteriormente, se necessário.

   ![Implantação](assets/deployment.png)

O pipeline pode levar vários minutos para ser concluído. Uma vez concluído, o complemento e seu conteúdo de demonstração estarão disponíveis para uso no ambiente de criação do AEM.

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada do complemento de demonstração de referência do AEM, você deve:

* Entender como usar o Cloud Manager para criar um novo programa.
* Saber como ativar o complemento de demonstrações de referência para o novo programa.
* Poder executar um pipeline para implantar o conteúdo complementar.

Aproveite esse conhecimento e prossiga com sua jornada de Complementos de demonstração de referência do AEM revendo o documento [Criar um site de demonstração,](create-site.md) em que você aprenderá a criar um site de demonstração no AEM com base em uma biblioteca de modelos pré-configurados que foram implantados pelo pipeline.

## Recursos adicionais {#additional-resources}

* [Documentação do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=pt_BR) - Se quiser obter mais detalhes sobre os recursos do Cloud Manager, consulte diretamente os documentos técnicos detalhados.
