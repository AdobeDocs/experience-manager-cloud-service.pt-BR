---
title: Execução de um pipeline
description: Esta página descreve a execução de um pipeline para o projeto Screens as Cloud Service no Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# Execução de um pipeline para o programa Screens as a Cloud Service no Cloud Manager {#run-pipeline-screens-cloud}

Esta seção descreve como executar o pipeline e implantar seu código para o programa no Cloud Manager.

>[!NOTE]
>Consulte [Configuração do pipeline de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) e [Implante seu código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) para saber como executar o pipeline do seu programa no Cloud Manager.

## Objetivo {#objective}

A seção a seguir descreve como configurar o pipeline de CI/CD e implantar seu código para o programa no Cloud Manager.

## Etapas para executar um pipeline para seu projeto do Screens no Cloud Manager {#steps-branch-creation}

1. Depois que a configuração do ambiente for concluída com êxito, você verá a atualização do cartão de chamada para ação no Cloud Manager **Visão geral** página.

   ![imagem](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Clique em **Configurar pipeline** do **Visão geral** página.

1. Clique em **Próxima** após selecionar a ramificação.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Selecione suas opções na **Configurar pipeline** assistente. Clique em **Salvar**.

   >[!NOTE]
   >Para saber mais sobre as opções do assistente de Configuração de pipeline, consulte [Definição das configurações de pipeline no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=en) para obter mais detalhes.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. Após a conclusão da configuração do pipeline, o cartão de chamada para ação é atualizado.

   >[!NOTE]
   >Para saber mais sobre os estágios na implantação no Cloud Manager, consulte [Implantação do código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en) para obter mais detalhes.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Clique em **Implantar**.

1. Clique em **Build** para iniciar o processo de criação.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. Depois que o processo de criação for concluído, você poderá ver um link de autor na **Ambientes** Cartão do Cloud Manager **Visão geral** página.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## O que vem a seguir {#whats-next}

Depois de saber como configurar um ambiente para seu programa no Cloud Manager, você está pronto para seguir para a próxima etapa do Processo de integração: [Navegar até o provedor de serviços do Screens](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
