---
title: Fase de preparação no Cloud Acceleration Manager
description: Esta página fornece uma visão geral sobre a fase de Preparação no Cloud Acceleration Manager.
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
source-git-commit: f99395870d076d47ef53b01c9fc6579a9f8788a2
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 6%

---

# Fase de preparação no Cloud Acceleration Manager {#readiness-phase-cam}

Depois de criar um projeto no Cloud Acceleration Manager, você pode iniciar a avaliação de sua implementação atual do Adobe Experience Manager (AEM) na fase de Preparação.

A Fase de preparação inclui:

* [Análise de práticas recomendadas](#best-practices-analysis)
* [Planejamento e configuração](#planning-setup)

Siga as etapas abaixo para acessar a Fase de preparação:

1. Clique no cartão do projeto.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. Na landing page do projeto, navegue até a **Disponibilidade** conforme mostrado na figura abaixo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Consulte Criação e gerenciamento de um projeto no Cloud Acceleration Manager para saber mais.

## Usando o cartão de análise de práticas recomendadas {#best-practices-analysis}

1. Clique em **Revisão** do **Análise de práticas recomendadas** cartão.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. Baixe o Analisador de práticas recomendadas (BPA).

   >[!NOTE]
   >Para evitar um impacto em instâncias críticas para os negócios, a Adobe recomenda executar o BPA em um ambiente de autor. O ambiente deve estar o mais próximo possível do ambiente de produção nas áreas de personalizações, configurações, conteúdo e aplicativos do usuário. Como alternativa, ele pode ser executado em um clone do ambiente de Autor de produção.

   1. Navegue até a [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) e baixe o Analisador de práticas recomendadas como um arquivo zip.

      >[!NOTE]
      >Revisão [Uso do Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html#imp-considerations) para saber como executar o BPA.

   1. Exportar o relatório em um formato CSV

1. Clique em **Carregar novo relatório** para que você possa fazer upload do relatório do BPA no CAM.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >O relatório não pode ser carregado se você estiver no modo Incógnito do navegador.

1. Depois de carregar um novo relatório, você pode ver o relatório Análise de práticas recomendadas.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >Se vários relatórios forem carregados, o relatório exibido em detalhes será sempre o que tiver a data de criação mais recente (não a data de upload).

1. Revise e explore o painel Análise de práticas recomendadas no CAM. Consulte [Revisar o relatório de análise de práticas recomendadas](#analysis-report) para obter mais detalhes.

   >[!NOTE]
   >Fazer upload de um novo relatório redefine todas as avaliações se ele for mais recente que o relatório carregado anteriormente.

### Usando a visualização de impressão {#print-preview-cam}

É possível selecionar a opção de visualização de impressão no Cloud Acceleration Manager para uma visualização imprimível dos relatórios ou para imprimir o relatório em um formato PDF para facilitar o compartilhamento.

Siga as etapas abaixo:

1. Clique em **Visualizar impressão** ícone.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Na nova guia com o relatório exibido em uma visualização imprimível, clique em **Imprimir** para imprimir o relatório no formato PDF.

   >[!IMPORTANT]
   >
   >* A opção **Salvar como PDF** O é recomendado e compatível com a funcionalidade acima.
   >* Se o botão de impressão do navegador for usado, ele imprimirá apenas uma página.

   ![imagem](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### Usando Exibir Linha de Tendência {#trendline-view-cam}

Ao fazer upload de mais de um relatório distinto do Analisador de práticas recomendadas (BPA) em um projeto, você pode selecionar o **Exibir linha de tendência** opção para exibir e comparar resultados dos relatórios históricos do BPA.

Siga as etapas abaixo para exibir relatórios da opção de linha de tendência:

>[!NOTE]
>Ao fazer upload de mais de um relatório BPA distinto em um projeto, você verá a **..** ícone. Os relatórios são considerados iguais (não distintos) se o host e o tempo de criação forem iguais.

1. Navegue até o projeto e clique em **Revisão** do **Análise de práticas recomendadas** no **Disponibilidade** fase.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Clique em **..**.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. Na lista suspensa, clique em **Exibir linha de tendência**, conforme mostrado na figura abaixo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Clicando **Exibir linha de tendência** abre a exibição de linha de tendência do relatório.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >O Relatório de linha de tendência exibe os resultados dos relatórios históricos do BPA em uma representação gráfica.
   >
   >Você verá dois gráficos que exibem a tendência do:
   > 
   >1. **Informar tendência de Achados**
   >1. **Tendência de Componentes e Modelos Personalizados**
   >
   >É possível adicionar ou alterar a exibição gráfica por meio do menu suspenso, conforme mostrado na figura abaixo:
   >![imagem](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### Revisão do relatório do Analisador de práticas recomendadas {#analysis-report}

Explore os seguintes cartões disponíveis na página Relatório de análise de práticas recomendadas:

![imagem](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Com cada cartão, você pode:
>
>* abrir a guia associada
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
>Consulte [Interpretação do relatório do Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html) para saber mais sobre categorias de descobertas e níveis de importância.

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

1. Clique em **Exibir** do **Planejamento e configuração** cartão. Esse cartão fornece todo o conteúdo relevante que ajuda a planejar e configurar a migração do AEM.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. Um carrossel de conteúdo exibe todas as informações relevantes para essa fase da jornada de migração.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Exclusão de um relatório de análise de práticas recomendadas da exibição de linha de tendência {#delete-trendline}

>[!IMPORTANT]
>Um relatório só pode ser excluído quando mais de um relatório foi carregado em um projeto.

1. Navegue até o projeto e clique em **Revisão** do **Análise de práticas recomendadas** no **Disponibilidade** fase.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Clique em **..**.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. Na lista suspensa, clique em **Exibir linha de tendência**, conforme mostrado na figura abaixo.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Clique no ícone de exclusão na **Relatório de linha de tendências** tela.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Clique em **Excluir** para confirmar a exclusão.

   ![imagem](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## O que vem a seguir {#whats-next}

Depois de saber como fazer logon no Cloud Acceleration Manager e criar um projeto, você está pronto para passar a revisar a próxima etapa do [Fase de implementação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html).
