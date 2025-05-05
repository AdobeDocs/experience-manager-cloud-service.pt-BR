---
title: Execução de um pipeline
description: Esta página descreve a execução de um pipeline para o projeto Screens as Cloud Service no Cloud Manager.
exl-id: 3203cff7-5668-4f50-a2c5-80ae474b439d
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 4%

---

# Execução de um pipeline para o programa as a Cloud Service do Screens no Cloud Manager {#run-pipeline-screens-cloud}

Esta seção descreve como executar o pipeline e implantar seu código para o programa no Cloud Manager.

>[!NOTE]
>Consulte [Configurando o pipeline de CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=pt-BR) e [Implantar código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=pt-BR) para saber como executar o pipeline para o seu programa no Cloud Manager.

## Objetivo {#objective}

A seção a seguir descreve como configurar o pipeline de CI/CD e implantar seu código para o programa no Cloud Manager.

## Etapas para executar um pipeline para seu projeto do Screens no Cloud Manager {#steps-branch-creation}

1. Depois que a configuração de ambiente for concluída com êxito, você verá a atualização do cartão de chamada para ação na página **Visão geral** da Cloud Manager.

   ![imagem](/help/screens-cloud/assets/onboarding/add-environ3.png)

1. Clique em **Configurar pipeline** na página **Visão geral**.

1. Clique em **Avançar** depois de selecionar a ramificação.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline1.png)

1. Selecione suas opções no assistente do **Pipeline de Instalação**. Clique em **Salvar**.

   >[!NOTE]
   >Para saber mais sobre as opções no assistente de Configuração de pipeline, consulte [Definindo as configurações de pipeline do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/configuring-production-pipelines.html?lang=pt-BR) para obter mais detalhes.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline2-a.png)

1. Após a conclusão da configuração do pipeline, o cartão de chamada para ação é atualizado.

   >[!NOTE]
   >Para saber mais sobre os estágios na implantação no Cloud Manager, consulte [Implantando seu Código](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=pt-BR) para obter mais detalhes.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline3.png)

1. Clique em **Implantar**.

1. Clique em **Compilação** para iniciar o processo de compilação.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline4.png)

1. Depois que o processo de compilação for concluído, você poderá ver um link do autor do cartão **Ambientes** na página **Visão geral** da Cloud Manager.

   ![imagem](/help/screens-cloud/assets/onboarding/run-pipeline5.png)

## O que vem a seguir {#whats-next}

Depois de saber como configurar um ambiente para seu programa no Cloud Manager, você estará pronto para avançar para a próxima etapa do processo de integração: [Navegar até o Provedor de Serviços da Screens](/help/screens-cloud/configuring/navigating-to-screens-services-provider.md).
