---
title: Fase de preparação no Cloud Acceleration Manager
description: Esta página fornece uma visão geral sobre a fase de Preparação no Cloud Acceleration Manager.
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
feature: Migration
role: Admin
source-git-commit: 3a0576e62518240b89290a75752386128b1ab082
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 7%

---

# Fase de preparação no Cloud Acceleration Manager {#readiness-phase-cam}

Depois de criar um projeto no Cloud Acceleration Manager (CAM), você pode iniciar a avaliação da implementação atual do Adobe Experience Manager (AEM) na fase de Preparação.

A Fase de preparação inclui:

* [Análise de práticas recomendadas](#best-practices-analysis)
* [Planejamento e Instalação](#planning-setup)

Siga as etapas abaixo para acessar a Fase de preparação:

1. Clique no cartão do projeto.

   ![Cartão do projeto](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. Na página de aterrissagem do projeto, navegue até a seção **Disponibilidade**, conforme mostrado na figura abaixo.

   ![Disponibilidade](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Consulte Criação e gerenciamento de um projeto no Cloud Acceleration Manager para saber mais.

## Uso do cartão de análise de práticas recomendadas {#best-practices-analysis}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa"
>title="Relatório do analisador de práticas recomendadas"
>abstract="O relatório do BPA pode ser enviado para o CAM para fornecer uma análise em relação à migração para o AEM as a Cloud Service."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer" text="Utilização do Analisador de práticas recomendadas"

1. Clique em **Revisar** no cartão **Análise de práticas recomendadas**.

   ![Análise de práticas recomendadas - Revisão](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. Baixe o Analisador de práticas recomendadas (BPA).

   >[!NOTE]
   >Para evitar um impacto em instâncias críticas para os negócios, a Adobe recomenda executar o BPA em um ambiente de autor. O ambiente deve estar o mais próximo possível do ambiente de produção nas áreas de personalizações, configurações, conteúdo e aplicativos do usuário. Como alternativa, ele pode ser executado em um clone do ambiente de Autor de produção.

   1. Navegue até o portal [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=best*) e baixe o Analisador de práticas recomendadas como um arquivo zip.

      >[!NOTE]
      >Revise [Usando o Analisador de Práticas Recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=pt-BR#imp-considerations) para saber como executar o BPA.

1. No CAM, clique em **Obter chave de carregamento**, para que você possa obter a chave usada para configurar seu sistema para carregar automaticamente relatórios do BPA diretamente para o CAM.

   ![Obter chave de carregamento](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3b.png)

   >[!IMPORTANT]
   >O relatório ainda pode ser carregado manualmente, mas usar a tecla Upload simplifica a operação. Observe que o relatório não pode ser carregado manualmente se seu tamanho for de aproximadamente 200 MB ou superior. O relatório também não pode ser carregado usando o modo Incógnito do navegador.

1. Depois que um novo relatório for carregado, você poderá ver o relatório de Análise de práticas recomendadas no CAM.

   ![Relatório de análise de práticas recomendadas](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >Se vários relatórios diferentes forem carregados, o relatório exibido em detalhes será sempre o que tiver a data de criação mais recente (não a data do upload).

1. Revise e explore o painel Análise de práticas recomendadas no CAM. Consulte [Revisando o Relatório de Análise de Práticas Recomendadas](#analysis-report) para obter mais detalhes.

   >[!NOTE]
   >Fazer upload de um novo relatório redefine todas as avaliações se ele for mais recente que o relatório carregado anteriormente.

### Usando a visualização de impressão {#print-preview-cam}

É possível selecionar a opção de visualização de impressão no Cloud Acceleration Manager para uma visualização imprimível dos relatórios ou para imprimir o relatório em um formato PDF para facilitar o compartilhamento.

Siga as etapas abaixo:

1. Clique na ação **Visualizar impressão**.

   ![Visualizar impressão](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1b.png)

1. Na nova guia com o relatório exibido em uma visualização imprimível, clique em **Imprimir** para imprimir o relatório no formato PDF.

   >[!IMPORTANT]
   >
   >* A opção **Salvar como PDF** é recomendada e tem suporte para a funcionalidade acima.
   >* Se o botão de impressão do navegador for usado, ele imprimirá apenas uma página.

   ![Imprimir](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### Usando Exibir Linha de Tendência {#trendline-view-cam}

Ao fazer upload de mais de um relatório distinto do Analisador de práticas recomendadas (BPA) em um Projeto, você pode selecionar a opção **Exibir linha de tendência** para exibir e comparar os resultados dos relatórios históricos do BPA.

Siga as etapas abaixo para exibir relatórios da opção de linha de tendência:

>[!NOTE]
>Ao carregar mais de um relatório BPA distinto em um Projeto, você verá o ícone **...**. Os relatórios são considerados iguais (não distintos) se o host e o tempo de criação forem iguais.

1. Navegue até o seu projeto e clique em **Revisão** no cartão **Análise de Práticas Recomendadas** na fase **Preparação**.

   ![Análise de práticas recomendadas - Revisão](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Na lista suspensa **Exibir**, clique em **Relatório de linha de tendências**, conforme mostrado na figura abaixo.

   ![Relatório de linha de tendências](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. Clicar em **Relatório de linha de tendências** abre a exibição de linha de tendências do relatório.

   ![Modo de Exibição de Linha de Tendência](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >O Relatório de linha de tendência exibe os resultados dos relatórios históricos do BPA em uma representação gráfica.
   >
   >Você verá dois gráficos que exibem a tendência do:
   > 
   >1. **Informar tendência de Achados**
   >1. **Tendência de Componentes e Modelos Personalizados**
   >
   >É possível adicionar ou alterar a exibição gráfica por meio do menu suspenso, conforme mostrado na figura abaixo:
   >![Selecione a exibição gráfica](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### Revisão do relatório do Analisador de práticas recomendadas {#analysis-report}

Explore os seguintes cartões disponíveis na página Relatório de análise de práticas recomendadas:

![Relatório de análise de práticas recomendadas](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Com cada cartão, você pode:
>
>* abrir a guia associada
>* marcar todas as guias de relatório (incluindo filtragem) para compartilhamento ou recuperação futura
>* use o ícone details para exibir os detalhes de cada descoberta de relatório

#### Propriedades do relatório {#report-properties}

O cartão **Propriedades do relatório** fornece informações sobre as propriedades do relatório, como data do relatório, duração, filtros, data de carregamento e detalhes do Adobe Experience Manager (AEM).

![Propriedades do Relatório](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### Visão geral do relatório {#report-overview}

Este cartão **Visão geral do relatório** fornece os resultados do relatório e os níveis de gravidade que se aplicam ao avaliar a prontidão para mover para o AEM as a Cloud Service, conforme mostrado na figura abaixo.

![Visão geral do relatório](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

Clicar neste relatório abre a guia **Relatório**.

![Guia Relatório](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

Você pode filtrar o relatório com base na importância, no subtipo ou na contagem.

![Filtros de relatório](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Consulte [Interpretando o Relatório do Analisador de Práticas Recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=pt-BR) para saber mais sobre categorias de descobertas e níveis de importância.

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

  ![Avaliação da complexidade da migração](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Usando o Cartão de Planejamento e Configuração {#planning-setup}

1. Clique em **Exibir** do cartão **Planejamento e Configuração**. Esse cartão fornece todo o conteúdo relevante que ajuda a planejar e configurar a migração do AEM.

   ![Planejamento E Configuração - Exibição](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. Um carrossel de conteúdo exibe todas as informações relevantes para essa fase da jornada de migração.

   ![Carrossel De Planejamento E Instalação](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Exclusão de um relatório de análise de práticas recomendadas da exibição de linha de tendência {#delete-trendline}

>[!IMPORTANT]
>Um relatório só pode ser excluído quando mais de um relatório foi carregado em um projeto.

1. Navegue até o seu projeto e clique em **Revisão** no cartão **Análise de Práticas Recomendadas** na fase **Preparação**.

   ![Análise de práticas recomendadas - Revisão](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Clique em **...**.

   ![Elipse](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. Na lista suspensa, clique em **Exibir linha de tendência**, conforme mostrado na figura abaixo.

   ![Exibir Linha de Tendência](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. Clique no ícone excluir da tela **Relatório de linha de tendências**.

   ![Relatório de linha de tendências - Excluir](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Clique em **Excluir** para confirmar a exclusão.

   ![Excluir](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## O que vem a seguir {#whats-next}

Depois de saber como fazer logon no Cloud Acceleration Manager e criar um projeto, você está pronto para revisar a próxima etapa da [Fase de implementação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=pt-BR).
