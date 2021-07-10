---
title: Fase de disponibilidade no Cloud Acceleration Manager
description: Esta página fornece uma visão geral sobre a fase Preparação no Cloud Acceleration Manager.
hide: true
hidefromtoc: true
index: false
source-git-commit: b5b6a4a84c57805770ec1c72741c2d56d4711309
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 4%

---


# Fase de disponibilidade no Cloud Acceleration Manager {#readiness-phase-cam}

Depois de criar um projeto no Cloud Acceleration Manager, você pode começar a executar as ferramentas disponíveis na fase Preparação.

A Fase de preparação inclui:

* [Análise de práticas recomendadas](#best-practices-analysis)
* [Planejamento e configuração](#planning-setup)

Siga as etapas abaixo para navegar até a Fase de disponibilidade:

1. Clique no cartão do projeto para abrir a página de aterrissagem do projeto.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. Navegue até a seção **Readiness**, conforme mostrado na figura abaixo.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Consulte [Criação e gerenciamento de um projeto no Cloud Acceleration Manager](/help/move-to-cloud-service/cloud-acceleration-manager/using-cam/getting-started-cam.md) para saber mais.

## Uso do cartão de análise de práticas recomendadas {#best-practices-analysis}

Siga as etapas abaixo para usar o cartão Análise de práticas recomendadas :

1. Clique no botão **Revisar** do cartão **Análise de práticas recomendadas**.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. Siga estas etapas para baixar o BPA (Best Practices Analyzer) e executá-lo em um clone de seu sistema de AEM.

   1. Navegue até o portal [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) e baixe o Analisador de práticas recomendadas como um arquivo zip.

      >[!NOTE]
      >Revise [Usando o Analisador de Práticas Recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) para saber como executar o BPA.

   1. Exportar o relatório em um formato CSV

1. Clique em **Fazer upload do novo relatório** para fazer upload do relatório BPA no CAM.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

1. Após carregar um novo relatório, você verá o relatório de Análise de práticas recomendadas .

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Revise e explore o painel de análise de práticas recomendadas do CAM. Consulte a seção abaixo [Revisando o Relatório de Análise de Práticas Recomendadas](#analysis-report) para obter mais detalhes.

   >[!NOTE]
   >Fazer upload de um novo relatório redefine todas as avaliações.

### Relatório de análise de práticas recomendadas {#analysis-report}

Explore os seguintes cartões disponíveis na página Relatório de análise de práticas recomendadas :

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Com cada placa, você tem a capacidade de:
>* clique em cada cartão para abrir a guia associada
>* marcar todas as guias do relatório (incluindo filtragem) para compartilhamento ou futura recuperação
>* use o ícone de detalhes para exibir os detalhes de cada descoberta de relatório


#### Propriedades do relatório {#report-properties}

O cartão **Propriedades do relatório** fornece informações sobre propriedades do relatório, como data do relatório, duração, filtros, data de upload e detalhes do Adobe Experience Manager (AEM).

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### Visão geral do relatório {#report-overview}

Este cartão **Visão geral do relatório** fornece as conclusões do relatório, conforme mostrado na figura abaixo.

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

Clicar nesse relatório abre a guia **Report**.

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

Você pode filtrar o relatório com base na importância, no subtipo ou na contagem.

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Consulte [Interpretando o Relatório do Analisador de Práticas Recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) para saber mais sobre as categorias de descobertas e os níveis de importância.

#### Avaliação de práticas recomendadas {#best-practices-assessment}

A opção Avaliação de práticas recomendadas fornece uma avaliação da instância de AEM atual e fornece orientação sobre as próximas etapas para adotar AEM práticas recomendadas. Você pode revisar as seguintes informações nesta guia:

* Visão geral da instância de AEM
* Componentes e modelos personalizados
* Conclusões adicionais
* Consultas lentas
* Tarefas de manutenção

#### Avaliação da complexidade da migração {#migration-complexity-assessment}

A opção Avaliação da complexidade da migração fornece uma avaliação da complexidade para migrar a implementação de AEM existente para o AEM como Cloud Service. Você pode revisar as seguintes informações nesta guia:

* Visão geral da instância de AEM
* Avaliação
* Considerações sobre a migração de conteúdo

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Uso do Cartão de Planejamento e Configuração {#planning-setup}

Siga esta seção para explorar o cartão de atividade Planejamento e configuração.

1. Clique no botão **Exibir** do cartão **Planejamento e Configuração** que fornece todo o conteúdo relevante que ajudará você a planejar e configurar sua migração de AEM.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-4.png)

1. Um carrossel de conteúdo com informações relevantes para essa fase da jornada de migração é exibido.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

## O que vem a seguir {#whats-next}

Depois de aprender a fazer logon no Cloud Acceleration Manager e a criar um projeto, agora você está pronto para passar para a próxima etapa, usando a fase de implementação.
