---
title: Fase de implementação no Cloud Acceleration Manager
description: Esta página fornece uma visão geral da fase de implementação no Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: dbf01e5bd9ee83e378b4297d2f3d341d548f9238
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 4%

---

# Fase de implementação no Cloud Acceleration Manager {#implementation-phase-cam}

A Fase de implementação inclui:

* [Desenvolvimento local](#local-development)
* [Refatoração do código](#code-refactoring)
* [AEM implantação as a Cloud Service](#aem-as-a-cloud-service-deployment)
* [Transferência de conteúdo](#content-transfer)


Clique no cartão do projeto para abrir a página de aterrissagem do projeto e navegue até o **Implementação** conforme mostrado na figura abaixo.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>Consulte [Criação e gerenciamento de um projeto no Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project) para saber mais.


## Usando o cartão de desenvolvimento local {#local-development}

O cartão de Desenvolvimento local fornece todo o conteúdo relevante que ajudará a configurar seu ambiente de desenvolvimento de AEM local à medida que você inicia a fase de Implementação da jornada de migração.

Siga esta seção para explorar o cartão de atividade de Desenvolvimento local :

1. Clique no botão **Exibir** do botão **Desenvolvimento local** cartão.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. Um carrossel de conteúdo exibe as informações relevantes para essa fase da jornada de migração.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## Uso da placa de refatoração de código {#code-refactoring}

O cartão de atividade Refatoração do Código fornece todas as informações relevantes e destaca as áreas de refatoração de código que você precisa revisar e resolver ao mudar para AEM as a Cloud Service.

Siga esta seção para explorar o cartão de atividades Refatoração do código :

1. Clique no botão **Revisão** do botão **Refatoração do código** cartão de atividades.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. A página exibe a lista de atividades de refatoração de código organizadas pelo nível de gravidade. Você pode saber mais clicando nos dois ícones destacados.

   A página exibe as considerações de refatoração de código em três guias diferentes:

   * Visão geral
   * Dispatcher
   * Testes

>[!NOTE]
>Revise o conteúdo dessas guias para entender algumas áreas adicionais que não são abordadas pelo Analisador de práticas recomendadas.

O **Dispatcher** A guia fornece informações sobre como estruturar as AEM configurações as a Cloud Service do Apache e Dispatcher, bem como como validá-las e executá-las localmente antes de implantá-las em ambientes do Cloud. Também descreve a depuração em ambientes do Cloud.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

O **Teste** A guia fornece informações sobre testes funcionais, de auditoria de experiência e de interface do usuário.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## Uso AEM cartão de implantação as a Cloud Service {#aem-as-a-cloud-service-deployment}

AEM cartão de implantação as a Cloud Service fornece todo o conteúdo relevante que ajudará você a implantar seu código AEM as a Cloud Service.

Siga esta seção para explorar AEM cartão de atividade do Cartão de implantação as a Cloud Service:

1. Clique no botão **Exibir** do botão **AEM implantação as a Cloud Service** cartão de atividades.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. Um carrossel de conteúdo exibe as informações relevantes para essa fase da jornada de migração.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## Uso do cartão de transferência de conteúdo {#content-transfer}

O cartão Transferência de conteúdo permite iniciar e gerenciar a transferência de conteúdo da instância de AEM atual para AEM as a Cloud Service.

Siga esta seção para explorar o cartão de atividade Transferência de conteúdo :

1. Clique no botão **Revisão** do botão **Transferência de conteúdo** cartão de atividades.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. Para iniciar uma transferência de conteúdo, será necessário criar um conjunto de Migração. Clique em **Criar conjunto de migração**. Um conjunto de migração permite que o conteúdo seja transferido para AEM as a Cloud Service.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >Revise o [pré-requisitos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) e [práticas recomendadas e diretrizes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) antes de usar a ferramenta Transferência de conteúdo .

1. Você precisará baixar e instalar a ferramenta Transferência de conteúdo para preencher o conjunto de migração e concluir a fase de Extração da transferência de conteúdo. Revisão [Introdução à ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR) para saber como usar a ferramenta Transferência de conteúdo .

1. Para assimilar conteúdo do conjunto de Migração em um ambiente em AEM as a Cloud Service, será necessário iniciar uma assimilação. Navegar para **Trabalhos de assimilação** e clique em **Nova assimilação**. Revisão [Inserção de conteúdo ao Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) para saber como concluir a fase de assimilação da transferência de conteúdo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## O que vem a seguir {#whats-next}

Depois de aprender a fazer logon no Cloud Acceleration Manager e a utilizar a fase de implementação, você estará pronto para passar para a revisão da próxima etapa no [Ir para a Fase Ativa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
