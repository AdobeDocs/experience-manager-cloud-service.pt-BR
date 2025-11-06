---
title: Adicionar um pipeline de Edge Delivery
description: Saiba como adicionar um pipeline do Edge Delivery para criar e implantar seu código em ambientes de produção.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
hide: false
index: false
hidefromtoc: false
exl-id: 5ad342fa-dd71-4105-a9cb-2d999d402780
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 3%

---

# Adicionar um pipeline do Edge Delivery {#configure-production-pipeline}

<!--badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket" -->

Saiba como configurar pipelines do Edge Delivery para compilar e implantar seu código em ambientes de produção. Os pipelines do Edge Delivery permitem configurar recursos, incluindo encaminhamento de logs e o CDN gerenciado pela Adobe.

Para obter uma lista de configurações com suporte, consulte [Usar pipelines de configuração - configurações com suporte](/help/operations/config-pipeline.md#configurations).

Um usuário deve ter a função **[Gerente de implantação](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar pipelines de produção.

>[!IMPORTANT]
>
>Um pipeline do Edge Delivery não pode ser configurado até que o seguinte tenha acontecido:
>
>* É criado um programa que contém um site do Edge Delivery Services e um domínio mapeado. Caso contrário, a opção **Adicionar pipeline de Edge Delivery** aparecerá desabilitada na interface, e uma dica de ferramenta explica os requisitos ausentes. Consulte [Criar um site do Edge Delivery no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)
>* O repositório Git tem pelo menos uma ramificação. Consulte [Gerenciar repositórios no Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).
>* Os ambientes de produção e de preparo são criados. Consulte [Introdução aos pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

<!-- CMGR‑69680 -->

Antes de começar a implantar seu código, defina as configurações de pipeline do [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Você pode [editar as configurações do pipeline](managing-pipelines.md) após a configuração inicial.

**Para adicionar um pipeline do Edge Delivery:**

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
1. Na seção **Acesso rápido**, clique em **Experience Manager**.
1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização desejada.
1. No console **Meus Programas**, clique em um programa.

   ![Página Meus programas no Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. Siga uma das seguintes opções:

   * **Adicionar um pipeline do Edge Delivery a partir do cartão Pipelines**

      1. No painel esquerdo, em **Programa**, clique em **![Ícone de visão geral](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) [Visão geral](/help/implementing/cloud-manager/navigation.md#my-programs)**.
      1. Na página **Visão geral do programa**, no cartão **Pipelines**, clique no **![Sinal de adição](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)Adicionar** e selecione **Adicionar pipeline de Edge Delivery**.

         ![O cartão Pipelines na página Visão Geral do Programa](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

         >[!TIP]
         >
         >Além de usar o cartão **Pipeline** como visto na captura de tela acima, você também pode gerenciar seu pipeline na página **Pipelines**.
         >
         >![Widget de pipeline do Edge Delivery mostrando o nome do pipeline, o status, o repositório e a ramificação](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

   * **Adicionar um pipeline de Edge Delivery da página Pipelines**

      1. No painel à esquerda, em **Programa**, clique em **![ícone de Fluxo de Trabalho ou em &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) Pipelines**.
      1. Na página Pipelines, próximo ao canto superior direito, clique em **Adicionar pipeline** > **Adicionar pipeline de Edge Delivery**.

         ![A página Pipelines com o botão Adicionar Pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

         >[!TIP]
         >
         >Próximo ao canto superior esquerdo, clique em **Filtros** e, na seção **Tipo de entrega**, marque a caixa de seleção **Entrega do Edge** para filtrar a lista somente para pipelines do Edge Delivery (ou seja, pipelines que usam o Edge Delivery Services). <!-- (CMGR-69682) -->
         >
         >![Painel de filtros mostrando o novo tipo de entrega do Edge e de publicação](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

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

   * **Ramificação Git** - Use a lista suspensa para selecionar uma ramificação específica dentro do repositório escolhido. Se necessário, clique em ![Ícone de Reciclagem ou ícone de Atualização](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) para recarregar a lista suspensa da ramificação Git após envios recentes.
   * **Localização do código** - Define o caminho da pasta dentro do repositório onde o código pronto para pipeline é iniciado ( `/` é igual à raiz do repositório).

   ![Configurar pipeline](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. Clique em **Salvar**.

Agora você pode [gerenciar seu pipeline](managing-pipelines.md) do cartão **Pipelines** na página **Visão geral do programa** ou da página **Pipelines**.


![Widget de pipeline do Edge Delivery mostrando o nome do pipeline, o status, o repositório e a ramificação](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)



