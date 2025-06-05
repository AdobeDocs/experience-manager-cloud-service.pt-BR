---
title: Adicionar um pipeline de Edge Delivery
description: Saiba como adicionar um pipeline do Edge Delivery para criar e implantar seu código em ambientes de produção.
index: false
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Primeiros usuários" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: acb919474bfe4285c889b8646f731285f5b759ba
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 35%

---



# Adicionar um pipeline do Edge Delivery {#configure-production-pipeline}

Saiba como configurar pipelines do Edge Delivery para compilar e implantar seu código em ambientes de produção. Um pipeline de produção primeiro implanta o código no ambiente de preparo. Na aprovação, ele implanta o mesmo código no ambiente de produção.

Um usuário deve ter a função **[Gerente de implantação](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar pipelines de produção.

>[!NOTE]
>
>Um pipeline de produção não pode ser configurado até que o seguinte tenha acontecido:
>
>* O programa é criado.
>* O repositório Git tem pelo menos uma ramificação.
>* Os ambientes de produção e de preparo são criados.

Antes de começar a implantar seu código, defina as configurações de pipeline do [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Você poderá [editar as configurações do pipeline](managing-pipelines.md) após a configuração inicial.

## Adicionar um novo pipeline do Edge Delivery {#adding-production-pipeline}

Depois de configurar seu programa e ter pelo menos um ambiente usando a interface do usuário do [!UICONTROL Cloud Manager], você estará pronto para adicionar um pipeline de não produção seguindo essas etapas.

>[!TIP]
>
>Antes de configurar um pipeline de front-end, consulte a [Jornada de Criação rápida de sites do AEM](/help/journey-sites/quick-site/overview.md) para obter um guia completo sobre a ferramenta simples de Criação rápida de sites do AEM. Esta jornada pode ajudá-lo a simplificar o desenvolvimento de front-end do seu site do AEM, permitindo que você personalize seu site rapidamente sem conhecimento de back-end no AEM.

**Para adicionar um novo pipeline do Edge Delivery:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização apropriada

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. Navegue até o cartão **Pipelines** da página **Visão geral do programa** e clique em **Adicionar** para selecionar **Adicionar pipeline de produção**.

   ![O cartão Pipelines na visão geral do Gerenciador de programas](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. A caixa de diálogo **Adicionar pipeline de produção** será exibida. Forneça um **Nome do pipeline** para identificar o pipeline junto com as opções a seguir. Clique em **Continuar**.

   **Acionador da implantação** - Você tem as seguintes opções ao definir os acionadores de implantação para iniciar o pipeline.

   * **Manual** - Iniciar o pipeline manualmente.
   * **Sobre Alterações do Git** - Inicia o pipeline de CI/CD sempre que confirmações são adicionadas à ramificação Git configurada. Com essa opção, ainda é possível iniciar o pipeline manualmente, conforme necessário.

   **Comportamento de falhas importantes da métrica** - Durante a configuração ou edição do pipeline, o **Gerente de implantação** tem a opção de definir o comportamento do pipeline quando uma falha importante é encontrada em qualquer um dos quality gates (portais de qualidade). As opções disponíveis são:

   * **Perguntar sempre** - Configuração padrão. Requer intervenção manual em qualquer falha importante.
   * **Falhar imediatamente**: se selecionado, o pipeline será cancelado sempre que ocorrer uma falha importante. Esse processo é basicamente semelhante a um usuário que rejeita manualmente cada falha.
   * **Continuar imediatamente** - Se selecionado, o pipeline continuará automaticamente sempre que ocorrer uma falha importante. Esse processo é basicamente semelhante a um usuário que aprova manualmente cada falha.

   ![Configuração do pipeline de produção](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. Na guia **Código Source**, selecione o tipo de código que o pipeline deve processar.

   * **[Configurar um pipeline de código de pilha completa](#full-stack-code)**
   * **[Configurar um pipeline de implantação direcionado](#targeted-deployment)**

Consulte [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obter mais informações sobre os tipos de pipelines.

As etapas para concluir a criação do pipeline de produção variam de acordo com o tipo de código-fonte selecionado. Siga os links acima para acessar a próxima seção deste documento e concluir a configuração do pipeline.

