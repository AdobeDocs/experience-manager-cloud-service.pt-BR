---
title: Fase de implementação no Cloud Acceleration Manager
description: Esta página fornece uma visão geral da fase de implementação no Cloud Acceleration Manager.
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 24331b974ded34ef949cc3d6fb157b124c145dee
workflow-type: tm+mt
source-wordcount: '792'
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

1. Você precisará baixar e instalar a ferramenta Transferência de conteúdo para preencher o conjunto de migração e concluir a fase de Extração da transferência de conteúdo. Revisão [Introdução à ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=br) para saber como usar a ferramenta Transferência de conteúdo .

1. Para assimilar conteúdo do conjunto de Migração em um ambiente em AEM as a Cloud Service, será necessário iniciar uma assimilação. Navegar para **Trabalhos de assimilação** e clique em **Nova assimilação**. Revisão [Inserção de conteúdo ao Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) para saber como concluir a fase de assimilação da transferência de conteúdo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

### Estimando o tempo de transferência de conteúdo {#calculating}

Uma calculadora da ferramenta Transferência de conteúdo foi fornecida para estimar quanto tempo pode ser necessário para concluir a atividade de transferência de conteúdo. Você pode usar o controle deslizante de tamanho do repositório de conteúdo para selecionar o tamanho que se aplica ao seu projeto. Os tempos de transferência variam para as fases de extração e ingestão.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

>[!NOTE]
>Esses tempos são apenas estimativas. Estas estimativas não incluem fatores como as velocidades de rede e o tempo para aumentar as instâncias.

Para estimar o tamanho do Repositório de AEM, você pode executar o relatório Uso de Disco em `http://HOST:PORT/etc/reports/diskusage.html`.

Você também pode estimar o tamanho de caminhos de repositório específicos usando a variável `path` , por exemplo, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.

## O que vem a seguir {#whats-next}

Depois de aprender a fazer logon no Cloud Acceleration Manager e a utilizar a fase de implementação, você estará pronto para passar para a revisão da próxima etapa no [Ir para a Fase Ativa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
