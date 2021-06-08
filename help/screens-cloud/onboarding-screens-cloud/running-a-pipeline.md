---
title: Execução de um pipeline
description: Esta página descreve como executar um pipeline para o Screens como Cloud Service no Cloud Manager.
hide: true
hidefromtoc: true
index: false
source-git-commit: 371cfaeb0e526197fdf98dea65ed5bc2ca0481a2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---


# Execução de um pipeline para Screens as a Cloud Service no Cloud Manager {#run-pipeline-screens-cloud}

Esta seção descreve como executar o pipeline e implantar seu código para o seu programa no Cloud Manager.

>[!NOTE]
>Consulte [Configuração do pipeline de CD-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) e [Implante o código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) para saber como executar o pipeline do seu programa no Cloud Manager.

## Objetivo {#objective}

A seção a seguir descreve como configurar o pipeline de CI/CD e implantar seu código para o seu programa no Cloud Manager.

## Etapas para executar um pipeline para seu projeto do Screens no Cloud Manager {#steps-branch-creation}

1. Quando a configuração do ambiente for concluída com êxito, você verá a atualização do cartão de chamada para ação na página **Visão geral** do Cloud Manager.

   ![imagem](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Clique em **Configurar pipeline** na página **Visão geral**.

1. Clique em **Next** depois de selecionar a ramificação.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Selecione suas opções no assistente **Configurar pipeline**. Clique em **Salvar**.

   >[!NOTE]
   >Para saber mais sobre as opções no assistente Configurar pipeline, consulte [Configurar as configurações do pipeline no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en) para obter mais detalhes.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. Quando o pipeline de configuração for concluído, o cartão de chamada para ação será atualizado, como mostrado na figura abaixo. Clique em Implantar.

   >[!NOTE]
   >Para saber mais sobre os estágios na implantação no Cloud Manager, consulte [Implantação do código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en) para obter mais detalhes.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Clique em **Criar** para iniciar o processo de compilação.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. Quando o processo de build for concluído, você verá um link de autor do cartão **Ambientes** na página **Visão geral** do Cloud Manager.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## O que vem a seguir {#whats-next}

Depois de aprender a executar o pipeline do seu programa no Cloud Manager, você está pronto para seguir para a próxima etapa. A próxima etapa é Configurar e configurar o projeto do Screens.