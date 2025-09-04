---
title: Adicionar um pipeline de Edge Delivery
description: Saiba como adicionar um pipeline do Edge Delivery para criar e implantar seu código em ambientes de produção.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: false
index: false
hidefromtoc: false
exl-id: 5ad342fa-dd71-4105-a9cb-2d999d402780
source-git-commit: dbd4ef8d782c9d05e50cab7479adbbc16d6a247d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 4%

---

# Adicionar um pipeline do Edge Delivery {#configure-production-pipeline}

Saiba como configurar pipelines do Edge Delivery para compilar e implantar seu código em ambientes de produção. Um pipeline de produção primeiro implanta o código no ambiente de preparo. Na aprovação, ele implanta o mesmo código no ambiente de produção.

Um usuário deve ter a função **[Gerente de implantação](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar pipelines de produção.

>[!NOTE]
>
>Um pipeline do Edge Delivery não pode ser configurado até que o seguinte tenha acontecido:
>
>* É criado um programa que contém um site do Edge Delivery Services e um domínio mapeado. Caso contrário, a opção **Adicionar pipeline de Edge Delivery** aparecerá desabilitada na interface, e uma dica de ferramenta explica os requisitos ausentes.
>* O repositório Git tem pelo menos uma ramificação.
>* Os ambientes de produção e de preparo são criados.

<!-- CMGR‑69680 -->


Antes de começar a implantar seu código, defina as configurações de pipeline do [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Você pode [editar as configurações do pipeline](managing-pipelines.md) após a configuração inicial.

**Para adicionar um pipeline do Edge Delivery:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização desejada.

1. Na página **Meus Programas**, selecione o programa desejado.

   ![Página Meus programas no Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. Siga uma das seguintes opções:

   * **Adicionar um pipeline do Edge Delivery a partir do cartão Pipelines**

      1. No painel esquerdo, em **Programa**, clique em **![Ícone de visão geral](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) [Visão geral](/help/implementing/cloud-manager/navigation.md#my-programs)**.
      1. Na página **Visão geral do programa**, no cartão **Pipelines**, clique no **![Sinal de adição](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)Adicionar** e selecione **Adicionar pipeline de Edge Delivery**.

         ![O cartão Pipelines na página Visão Geral do Programa](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

   * **Adicionar um pipeline de Edge Delivery da página Pipelines**

      1. No painel à esquerda, em **Programa**, clique em **![ícone de Fluxo de Trabalho ou em ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) Pipelines**.
      1. Na página Pipelines, próximo ao canto superior direito, clique em **Adicionar pipeline** > **Adicionar pipeline de Edge Delivery**.

         ![A página Pipelines com o botão Adicionar Pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

1. Na caixa de diálogo **Adicionar pipeline de Edge Delivery**, no campo de texto **Nome do pipeline**, digite um rótulo de pipeline descritivo.

   ![Caixa de diálogo Adicionar pipeline do Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. Selecione a opção de pipeline **Acionador de implantação** que você deseja.

   * **Manual** - Você inicia a implantação.
   * **Sobre Alterações do Git** - As confirmações do Git iniciam a implantação automaticamente. Com essa opção, ainda é possível iniciar o pipeline manualmente, se necessário.

1. Clique em **Continuar**.

1. Em **Source Code**, defina as seguintes opções:

   * **Ambiente de Implantação** - Exibe o campo do ambiente de destino; permanece como somente leitura.

   * **Repositório** - Use a lista suspensa para apontar o pipeline para o repositório Git exato que armazena a configuração do Edge Delivery.

     Consulte também [Adicionar e gerenciar repositórios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para saber como adicionar e gerenciar repositórios no Cloud Manager.

   * **Ramificação Git** - Use a lista suspensa para selecionar uma ramificação específica dentro do repositório escolhido. Se necessário, clique em ![Ícone de reciclagem ou ícone de atualização](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) para recarregar a lista suspensa da ramificação Git após envios recentes
   * **Localização do código** - Define o caminho da pasta dentro do repositório onde o código pronto para pipeline é iniciado ( `/` é igual à raiz do repositório).

   ![Configurar pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. Clique em **Salvar**.

Agora você pode [gerenciar seu pipeline](managing-pipelines.md) no cartão **Pipelines** na página **Visão geral do programa** ou na página **Pipelines**.
