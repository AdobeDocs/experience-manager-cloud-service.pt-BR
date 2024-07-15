---
title: Fase de implementação no Cloud Acceleration Manager
description: Esta página fornece uma visão geral sobre a fase de implementação no Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 5%

---

# Fase de implementação no Cloud Acceleration Manager {#implementation-phase-cam}

A Fase de implementação inclui:

* [Desenvolvimento local](#local-development)
* [Refatoração de código](#code-refactoring)
* [Implantação do AEM as a Cloud Service](#aem-as-a-cloud-service-deployment)
* [Transferência de conteúdo](#content-transfer)


Clique no cartão do projeto para abrir a página de aterrissagem do projeto e navegue até a seção **Implementação**, conforme mostrado na figura a seguir.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Consulte [Criação e gerenciamento de um projeto no Cloud Acceleration Manager](getting-started-cam.md#create-project) para saber mais.


## Usar cartão de desenvolvimento local {#local-development}

O cartão Desenvolvimento local fornece todo o conteúdo relevante que pode ajudá-lo a configurar o ambiente de desenvolvimento local do AEM conforme você inicia a fase de Implementação da jornada de migração.

Siga esta seção para explorar o cartão de atividade de Desenvolvimento local:

1. Clique em **Exibir** do cartão **Desenvolvimento Local**.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. Um carrossel de conteúdo exibe as informações relevantes para essa fase da jornada de migração.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Usando o cartão de refatoração de código {#code-refactoring}

O cartão de atividade de Refatoração de código fornece todas as informações relevantes e destaca as áreas de refatoração de código a serem analisadas e resolvidas ao migrar para o AEM as a Cloud Service.

Siga esta seção para explorar o cartão de atividade de Refatoração de código:

1. Clique em **Revisar** no cartão de atividade **Refatoração de código**.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. A página exibe a lista de atividades de refatoração de código organizadas por nível de severidade. Para saber mais, clique nos dois ícones destacados.

   A página exibe as considerações sobre a refatoração de código em três guias diferentes:

   * Visão geral
   * Dispatcher
   * Testes

>[!NOTE]
>Revise o conteúdo nessas guias para entender algumas áreas adicionais que não são cobertas pelo Analisador de práticas recomendadas.

A guia **Dispatcher** fornece informações sobre como estruturar as configurações do AEM as a Cloud Service Apache e do Dispatcher e como validá-lo e executá-lo localmente antes de implantá-lo em ambientes de Nuvem. Também descreve a depuração em ambientes na nuvem.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

A guia **Testes** fornece informações sobre testes funcionais, de Auditoria de Experiência e de Interface do Usuário.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## Usar o cartão de implantação do AEM as a Cloud Service {#aem-as-a-cloud-service-deployment}

O cartão Implantação do AEM as a Cloud Service fornece todo o conteúdo relevante que ajuda a implantar seu código no AEM as a Cloud Service.

Siga esta seção para explorar o cartão de atividade Cartão de implantação do AEM as a Cloud Service:

1. Clique em **Exibir** no cartão de atividade **Implantação do AEM as a Cloud Service**.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. Um carrossel de conteúdo exibe as informações relevantes para essa fase da jornada de migração.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Usar o cartão de transferência de conteúdo {#content-transfer}

O cartão Transferência de conteúdo permite iniciar e gerenciar a transferência de conteúdo da sua instância atual do AEM para o AEM as a Cloud Service.

Siga esta seção para explorar o cartão de atividade Transferência de conteúdo:

1. Clique em **Revisar** no cartão de atividade **Transferência de conteúdo**.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Para iniciar uma transferência de conteúdo, você deve criar um conjunto de migração. Clique em **Criar conjunto de migração**. Um conjunto de migração permite que o conteúdo seja transferido para o AEM as a Cloud Service.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Um conjunto de migração expira após um período prolongado de inatividade. Consulte [Expiração do Conjunto de Migração](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obter detalhes.

   >[!NOTE]
   >Consulte os [pré-requisitos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=pt-BR) e as [práticas recomendadas e diretrizes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=pt-BR) antes de usar a Ferramenta de transferência de conteúdo.

1. Baixe e instale a ferramenta Transferência de conteúdo para preencher o conjunto de migração e concluir a fase de Extração da transferência de conteúdo. Revise [Introdução à ferramenta de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR) para saber como usar a ferramenta de transferência de conteúdo.

1. Para assimilar conteúdo do conjunto de migração em um ambiente no AEM as a Cloud Service, você deve iniciar uma assimilação. Navegue até **Trabalhos de assimilação** e clique em **Nova assimilação**. Revise [Assimilar conteúdo no Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para que você possa aprender a concluir a fase de Assimilação da transferência de conteúdo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## O que vem a seguir {#whats-next}

Depois de saber como fazer logon no Cloud Acceleration Manager e usar a fase de Implementação, você estará pronto para revisar a próxima etapa da [Fase de ativação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
