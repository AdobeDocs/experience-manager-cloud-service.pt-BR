---
title: Fase de implementação no Cloud Acceleration Manager
description: Esta página fornece uma visão geral sobre a fase de implementação no Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 4%

---

# Fase de implementação no Cloud Acceleration Manager {#implementation-phase-cam}

A Fase de implementação inclui:

* [Desenvolvimento local](#local-development)
* [Refatoração do código](#code-refactoring)
* [Implantação as a Cloud Service do AEM](#aem-as-a-cloud-service-deployment)
* [Transferência de conteúdo](#content-transfer)


Clique no cartão do projeto para abrir a landing page do projeto e navegar até a **Implementação** conforme mostrado na figura a seguir.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Consulte [Criação e gerenciamento de um projeto no Cloud Acceleration Manager](getting-started-cam.md#create-project) para saber mais.


## Usar cartão de desenvolvimento local {#local-development}

O cartão Desenvolvimento local fornece todo o conteúdo relevante que pode ajudá-lo a configurar o ambiente de desenvolvimento local do AEM conforme você inicia a fase de Implementação da jornada de migração.

Siga esta seção para explorar o cartão de atividade de Desenvolvimento local:

1. Clique em **Exibir** do **Desenvolvimento local** cartão.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. Um carrossel de conteúdo exibe as informações relevantes para essa fase da jornada de migração.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Usando o cartão de refatoração de código {#code-refactoring}

O cartão de atividade de Refatoração de código fornece todas as informações relevantes e destaca as áreas de refatoração de código a serem analisadas e resolvidas ao migrar para o AEM as a Cloud Service.

Siga esta seção para explorar o cartão de atividade de Refatoração de código:

1. Clique em **Revisão** do **Refatoração do código** Cartão de atividade.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. A página exibe a lista de atividades de refatoração de código organizadas por nível de severidade. Para saber mais, clique nos dois ícones destacados.

   A página exibe as considerações sobre a refatoração de código em três guias diferentes:

   * Visão geral
   * Dispatcher
   * Testes

>[!NOTE]
>Revise o conteúdo nessas guias para entender algumas áreas adicionais que não são cobertas pelo Analisador de práticas recomendadas.

A variável **Dispatcher** A guia fornece informações sobre como estruturar as configurações do AEM as a Cloud Service Apache e Dispatcher e como validá-lo e executá-lo localmente antes de implantar em ambientes da nuvem. Também descreve a depuração em ambientes na nuvem.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

A variável **Testes** A guia fornece informações sobre testes funcionais, Auditoria de experiência e interface do usuário.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## Uso da placa de implantação as a Cloud Service do AEM {#aem-as-a-cloud-service-deployment}

O cartão Implantação as a Cloud Service do AEM fornece todo o conteúdo relevante que ajuda a implantar seu código no AEM as a Cloud Service.

Siga esta seção para explorar o cartão de atividade Cartão de implantação as a Cloud Service AEM:

1. Clique em **Exibir** do **Implantação as a Cloud Service do AEM** Cartão de atividade.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. Um carrossel de conteúdo exibe as informações relevantes para essa fase da jornada de migração.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Usar o cartão de transferência de conteúdo {#content-transfer}

O cartão Transferência de conteúdo permite iniciar e gerenciar a transferência de conteúdo da sua instância atual do AEM para o AEM as a Cloud Service.

Siga esta seção para explorar o cartão de atividade Transferência de conteúdo:

1. Clique em **Revisão** do **Transferência de conteúdo** Cartão de atividade.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Para iniciar uma transferência de conteúdo, você deve criar um conjunto de migração. Clique em **Criar conjunto de migração**. Um conjunto de migração permite que o conteúdo seja transferido para o AEM as a Cloud Service.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Um conjunto de migração expira após um período prolongado de inatividade. Consulte [Expiração do conjunto de migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obter detalhes.

   >[!NOTE]
   >Consulte [pré-requisitos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html) e a variável [práticas recomendadas e diretrizes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) antes de usar a ferramenta Transferência de conteúdo.

1. Baixe e instale a ferramenta Transferência de conteúdo para preencher o conjunto de migração e concluir a fase de Extração da transferência de conteúdo. Revisão [Introdução à ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html) para saber como usar a ferramenta Transferência de conteúdo.

1. Para assimilar conteúdo do conjunto de migração em um ambiente no AEM as a Cloud Service, você deve iniciar uma assimilação. Navegue até **Tarefas de assimilação** e clique em **Nova assimilação**. Revisão [Assimilar conteúdo no Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html) para que você possa aprender a concluir a fase de assimilação da transferência de conteúdo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## O que vem a seguir {#whats-next}

Depois de saber como fazer logon no Cloud Acceleration Manager e usar a fase de implementação, você estará pronto para passar a revisar a próxima etapa da [Fase Go Live](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
