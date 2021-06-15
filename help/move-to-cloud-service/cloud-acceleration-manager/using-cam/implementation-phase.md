---
title: Fase de implementação no Cloud Acceleration Manager
description: Esta página fornece uma visão geral da fase de implementação no Cloud Acceleration Manager.
hide: true
hidefromtoc: true
index: false
source-git-commit: 5af319d30198329fd2312c11d88bf326bc4cdae7
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 2%

---


# Fase de implementação no Cloud Acceleration Manager {#implementation-phase-cam}

A Fase de implementação inclui:

* [Desenvolvimento local](#local-development)
* [Refatoração do código](#code-refactoring)
* [AEM como implantação do Cloud Service](#aem-as-a-cloud-service-deployment)
* [Transferência de conteúdo](#content-transfer)

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-1.png)

## Usando o Cartão de Desenvolvimento Local {#local-development}

O cartão de Desenvolvimento local fornece todo o conteúdo relevante que ajudará a configurar seu ambiente de desenvolvimento de AEM local à medida que você inicia a fase de Implementação da jornada de migração.

Siga esta seção para explorar o cartão de atividade de Desenvolvimento local :

1. Clique no botão **Exibir** no cartão **Desenvolvimento local**.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-2.png)

1. Um carrossel de conteúdo com informações relevantes para essa fase da jornada de migração é exibido.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-3.png)


## Uso da placa de refatoração de código {#code-refactoring}

A placa de atividade Refatoração do código fornece todas as informações relevantes e destaca as áreas de refatoração de código que você precisa analisar ao mudar para AEM como Cloud Service.

Siga esta seção para explorar o cartão de atividades Refatoração do código :

1. Clique no botão **Revisar** no cartão de atividade **Refatoração do código**.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-4.png)

1. A página exibe a lista de atividades de refatoração de código organizadas pelo nível de gravidade. Você pode saber mais clicando nos dois ícones destacados.

   >[!NOTE]
   >Além disso, revise o conteúdo nas guias da página para entender algumas áreas adicionais que não são abordadas pelo Analisador de práticas recomendadas.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5.png)


## Uso do AEM como uma placa de implantação do Cloud Service {#aem-as-a-cloud-service-deployment}

O AEM como cartão de Implantação do Cloud Service fornece todo o conteúdo relevante que ajudará você a implantar seu código no AEM como Cloud Service.

Siga esta seção para explorar o AEM como um cartão de atividade do Cartão de implantação do Cloud Service:

1. Clique no botão **View** do cartão **AEM como Cloud Service Deployment**.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-4.png)

1. Um carrossel de conteúdo com informações relevantes para essa fase da jornada de migração é exibido.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5.png)


## Uso da placa de transferência de conteúdo {#content-transfer}

O cartão de atividade Transferência de conteúdo fornece orientação e considerações que devem ser revisadas ao usar a ferramenta Transferência de conteúdo para mover o conteúdo da instância de AEM atual para o AEM como Cloud Service.

Siga esta seção para explorar o cartão de atividade Transferência de conteúdo :

1. Clique no botão **Exibir** no cartão **Desenvolvimento local**.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-4.png)

1. Um carrossel de conteúdo com informações relevantes para essa fase da jornada de migração é exibido.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5.png)

>[!NOTE]
>Revise os [pré-requisitos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) e as [práticas recomendadas e diretrizes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) antes de usar a ferramenta Transferência de conteúdo.

Uma nova calculadora da ferramenta Transferência de conteúdo foi fornecida para estimar quanto tempo pode ser necessário para concluir a atividade de transferência de conteúdo. Você pode usar o controle deslizante de tamanho do repositório de conteúdo para selecionar o tamanho que se aplica ao seu projeto. Os tempos de transferência variam para as fases de extração e ingestão. Para estimar o tamanho do Repositório de AEM, você pode executar o relatório Uso de Disco em `http://HOST:PORT/etc/reports/diskusage.html`.

Você também pode estimar o tamanho de caminhos de repositório específicos usando o parâmetro `path`, por exemplo, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.
