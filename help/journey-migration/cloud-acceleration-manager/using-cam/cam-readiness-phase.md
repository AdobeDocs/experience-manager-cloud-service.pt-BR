---
title: Fase de preparação no Cloud Acceleration Manager
description: Esta página fornece uma visão geral sobre a fase de Preparação no Cloud Acceleration Manager.
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 5%

---

# Fase de preparação no Cloud Acceleration Manager {#readiness-phase-cam}

Depois de criar um projeto no Cloud Acceleration Manager, você pode iniciar a avaliação de sua implementação atual do AEM na fase de preparação.

A Fase de preparação inclui:

* [Análise de práticas recomendadas](#best-practices-analysis)
* [Planejamento e configuração](#planning-setup)

Siga as etapas abaixo para acessar a Fase de preparação:

1. Clique no cartão do projeto para abrir a landing page do projeto.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. Navegue até a **Disponibilidade** conforme mostrado na figura abaixo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Consulte Criação e gerenciamento de um projeto no Cloud Acceleration Manager para saber mais.

## Usando o cartão de análise de práticas recomendadas {#best-practices-analysis}

Siga as etapas abaixo para usar o cartão de Análise de práticas recomendadas:

1. Clique no link **Revisão** botão no **Análise de práticas recomendadas** cartão.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. Siga estas etapas para baixar o Analisador de práticas recomendadas (BPA).

   >[!NOTE]
   >Para evitar um impacto em instâncias críticas para os negócios, é recomendável executar o BPA em um ambiente de Autor o mais próximo possível do ambiente de Produção nas áreas de personalizações, configurações, conteúdo e aplicativos de usuários. Como alternativa, ele pode ser executado em um clone do ambiente de Autor de produção.

   1. Navegue até [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) e baixe o Analisador de práticas recomendadas como um arquivo zip.

      >[!NOTE]
      >Revisão [Uso do Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) para saber como executar o BPA.

   1. Exportar o relatório em um formato CSV

1. Clique em **Carregar novo relatório** para carregar o relatório BPA no CAM.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >O relatório não pode ser carregado se você estiver no modo Incógnito do navegador.

1. Depois de carregar um novo relatório, você verá o relatório Análise de práticas recomendadas.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Revise e explore o painel Análise de práticas recomendadas no CAM. Consulte a seção abaixo [Revisar o relatório de análise de práticas recomendadas](#analysis-report) para obter mais detalhes.

   >[!NOTE]
   >Fazer upload de um novo relatório redefine todas as avaliações.

### Usando a visualização de impressão {#print-preview-cam}

É possível selecionar a opção de visualização de impressão no Cloud Acceleration Manager para uma visualização imprimível dos relatórios ou para imprimir o relatório em um formato PDF para facilitar o compartilhamento.

Siga as etapas abaixo:

1. Clique em **Visualizar impressão** como mostrado abaixo.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Clicando em **Visualizar impressão** abre uma nova guia com o relatório exibido em uma visualização imprimível. Clique em **Imprimir** para imprimir o relatório no formato PDF.

   >[!IMPORTANT]
   >* A opção **Salvar como PDF** O é recomendado e compatível com a funcionalidade acima.
   >* Se o botão de impressão do navegador for usado, ele imprimirá apenas uma página.


   ![imagem](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### Usando Exibir Linha de Tendência {#trendline-view-cam}

Ao fazer upload de mais de um relatório do Analisador de práticas recomendadas (BPA) em um projeto, você pode selecionar o **Exibir linha de tendência** opção para exibir e comparar resultados dos relatórios históricos do BPA.

Siga as etapas abaixo para exibir relatórios da opção de linha de tendência:

>[!NOTE]
>Ao fazer upload de mais de um relatório BPA em um projeto, você verá a **..** ícone.

1. Navegue até o projeto e clique em **Revisão** do **Análise de práticas recomendadas** no **Disponibilidade** fase.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Clique no link **..** ícone para exibir o menu suspenso.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >O relatório exibido é sempre o relatório com a data mais recente.

1. Clique em **Exibir linha de tendência**, conforme mostrado na figura abaixo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Clicando em **Exibir linha de tendência** abre a exibição de linha de tendência do relatório, como mostrado na figura abaixo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >O Relatório de linha de tendência exibe os resultados dos relatórios históricos do BPA em uma representação gráfica.
   >
   >Você verá dois gráficos que exibem a tendência do:
   >1. **Informar tendência de Achados**
   >1. **Tendência de Componentes e Modelos Personalizados**

   >
   >É possível adicionar ou alterar a exibição gráfica por meio do menu suspenso, conforme mostrado na figura abaixo:
   >![imagem](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### Revisar o relatório de análise de práticas recomendadas {#analysis-report}

Explore os seguintes cartões disponíveis na página Relatório de análise de práticas recomendadas:

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Com cada cartão, você tem a capacidade de:
>* clique em cada cartão para abrir a guia associada
>* marcar todas as guias de relatório (incluindo filtragem) para compartilhamento ou recuperação futura
>* use o ícone details para exibir os detalhes de cada descoberta de relatório


#### Propriedades do relatório {#report-properties}

A variável **Propriedades do relatório** O cartão fornece informações sobre as propriedades do relatório, como data, duração, filtros, data de upload e detalhes do Adobe Experience Manager (AEM).

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### Visão geral do relatório {#report-overview}

Este **Visão geral do relatório** fornece as conclusões do relatório e os níveis de gravidade que se aplicam ao avaliar a prontidão para migrar para o AEM as a Cloud Service, conforme mostrado na figura abaixo.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

Clicar nesse relatório abre o **Relatório** guia.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

Você pode filtrar o relatório com base na importância, no subtipo ou na contagem.

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Consulte [Interpretação do relatório do Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) para saber mais sobre categorias de descobertas e níveis de importância.

#### Avaliação de práticas recomendadas {#best-practices-assessment}

A opção Avaliação de práticas recomendadas fornece uma avaliação da instância de AEM atual e orientação sobre as próximas etapas para adotar as práticas recomendadas de AEM. É possível revisar as seguintes informações nessa guia:

* Visão geral da instância do AEM
* Componentes e modelos personalizados
* Achados adicionais
* Consultas lentas
* Tarefas de manutenção

#### Avaliação da complexidade da migração {#migration-complexity-assessment}

A opção Avaliação da complexidade da migração fornece uma avaliação da complexidade para migrar a implementação existente do AEM para o AEM as a Cloud Service.

É possível revisar as seguintes informações nessa guia:

* Visão geral da instância do AEM
* Avaliação
* Considerações sobre a migração de conteúdo

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Usando o Cartão de Planejamento e Configuração {#planning-setup}

Siga esta seção para explorar o cartão de atividade Planejamento e Configuração.

1. Clique no link **Exibir** botão no **Planejamento e configuração** cartão. Esse cartão fornece todo o conteúdo relevante que ajudará você a planejar e configurar a migração do AEM.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. Um carrossel de conteúdo exibe todas as informações relevantes para essa fase da jornada de migração.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Excluindo um relatório de análise de práticas recomendadas {#delete-trendline}

Siga as etapas abaixo para excluir um relatório da exibição Linha de tendência:

>[!IMPORTANT]
>Um relatório só pode ser excluído quando mais de um relatório foi carregado em um projeto.

1. Navegue até o projeto e clique em **Revisão** do **Análise de práticas recomendadas** no **Disponibilidade** fase.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Clique no link **..** ícone para exibir o menu suspenso.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. Clique em **Exibir linha de tendência**, conforme mostrado na figura abaixo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Clique no ícone de exclusão na **Relatório de linha de tendências** tela.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Clique em **Excluir** para confirmar a exclusão.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## O que vem a seguir {#whats-next}

Depois de saber como fazer logon no Cloud Acceleration Manager e criar um projeto, você está pronto para passar a revisar a próxima etapa do [Fase de implementação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
