---
title: Fase de disponibilidade no Cloud Acceleration Manager
description: Esta página fornece uma visão geral sobre a fase Preparação no Cloud Acceleration Manager.
exl-id: 91a13cae-4934-42e8-9538-896fd72f5acb
source-git-commit: c10d04d6d423529549a760945f72fc3c64ed72ed
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 5%

---

# Fase de disponibilidade no Cloud Acceleration Manager {#readiness-phase-cam}

Depois de criar um projeto no Cloud Acceleration Manager, você pode iniciar a avaliação da implementação de AEM atual na fase Preparação.

A Fase de preparação inclui:

* [Análise de práticas recomendadas](#best-practices-analysis)
* [Planejamento e configuração](#planning-setup)

Siga as etapas abaixo para navegar até a Fase de disponibilidade:

1. Clique no cartão do projeto para abrir a página de aterrissagem do projeto.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. Navegue até o **Prontidão** conforme mostrado na figura abaixo.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Consulte Criação e gerenciamento de um projeto no Cloud Acceleration Manager para saber mais.

## Uso do cartão de análise de práticas recomendadas {#best-practices-analysis}

Siga as etapas abaixo para usar o cartão Análise de práticas recomendadas :

1. Clique no botão **Revisão** do botão **Análise de práticas recomendadas** cartão.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. Siga estas etapas para baixar o BPA (Best Practices Analyzer).

   >[!NOTE]
   >Para evitar um impacto em instâncias críticas para os negócios, é recomendável executar o BPA em um ambiente de Autor o mais próximo possível do ambiente de Produção nas áreas de personalizações, configurações, conteúdo e aplicativos de usuários. Como alternativa, ele pode ser executado em um clone do ambiente de Autor de produção.

   1. Navegar para [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal e baixe o Analisador de práticas recomendadas como arquivo zip.

      >[!NOTE]
      >Revisão [Uso do Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) para saber como executar o BPA.

   1. Exportar o relatório em um formato CSV

1. Clique em **Fazer upload do novo relatório** para fazer upload do relatório BPA no CAM.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >O relatório não pode ser carregado se você estiver no modo Incógnito do navegador.

1. Após carregar um novo relatório, você verá o relatório de Análise de práticas recomendadas .

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Revise e explore o painel de análise de práticas recomendadas do CAM. Consulte a seção abaixo [Relatório de análise de práticas recomendadas](#analysis-report) para obter mais detalhes.

   >[!NOTE]
   >Fazer upload de um novo relatório redefine todas as avaliações.

### Usando a Visualização de Impressão {#print-preview-cam}

Você pode selecionar a opção de pré-visualização de impressão no Cloud Acceleration Manager para obter uma pré-visualização imprimível dos relatórios ou imprimir o relatório em um formato PDF para facilitar a compartilhabilidade.

Siga as etapas abaixo:

1. Clique em **Visualização de impressão** , conforme mostrado abaixo.

   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Clicando em **Visualização de impressão** abre uma nova guia com o relatório exibido em uma visualização que pode ser impressa. Clique em **Imprimir** para imprimir o relatório em um formato PDF.

   >[!IMPORTANT]
   >* A opção **Salvar como PDF** é recomendado e compatível com a funcionalidade acima.
   >* Se o botão de impressão do navegador for usado, ele imprimirá apenas uma página.


   ![imagem](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview2.png)

### Usando a Linha de Tendência da Exibição {#trendline-view-cam}

Ao fazer upload de mais de um relatório do Analisador de práticas recomendadas (BPA) em um Projeto, você pode selecionar a variável **Exibir linha de tendência** para exibir e comparar os resultados dos relatórios BPA antigos.

Siga as etapas abaixo para exibir os relatórios a partir da opção de linha de tendência:

>[!NOTE]
>Ao fazer upload de mais de um relatório BPA em um Projeto, você verá a variável **...** ícone .

1. Navegue até o seu projeto e clique em **Revisão** do **Análise de práticas recomendadas** no **Prontidão** fase.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Clique no botão **...** ícone para exibir o menu suspenso.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >O relatório exibido na **Tela Relatório de linha de tendência** é sempre aquele com a data recente do relatório.

1. Clique em **Exibir linha de tendência**, conforme mostrado na figura abaixo.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view2.png)

1. Clicando em **Exibir linha de tendência** abre a visualização da linha de tendência do relatório, como mostrado na figura abaixo.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view3.png)

   >[!NOTE]
   >O Relatório de linha de tendência exibe os resultados dos relatórios históricos de BPA em uma representação gráfica.
   >
   >Você verá dois gráficos exibindo a tendência do:
   >1. **Tendência das conclusões de relatório**
   >1. **Tendência de componentes e modelos personalizados**

   >
   >Você pode adicionar ou alterar a exibição gráfica no menu suspenso, como mostrado na figura abaixo:
   >![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view4.png)

#### Excluir o relatório {#delete-trendline}

Siga as etapas abaixo para excluir um relatório da exibição de Linha de tendência:

>[!IMPORTANT]
>Um relatório pode ser excluído somente quando mais de um relatório tiver sido carregado em um projeto.

1. Navegue até o seu projeto e clique em **Revisão** do **Análise de práticas recomendadas** no **Prontidão** fase.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Clique no botão **...** ícone para exibir o menu suspenso.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view1.png)

1. Clique em **Exibir linha de tendência**, conforme mostrado na figura abaixo.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view2.png)

1. Clique no ícone de exclusão do **Relatório de linha de tendência** tela.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view5.png)

1. Clique em **Excluir** para confirmar a exclusão.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/trendline-view6.png)


### Relatório de análise de práticas recomendadas {#analysis-report}

Explore os seguintes cartões disponíveis na página Relatório de análise de práticas recomendadas :

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Com cada placa, você tem a capacidade de:
>* clique em cada cartão para abrir a guia associada
>* marcar todas as guias do relatório (incluindo filtragem) para compartilhamento ou futura recuperação
>* use o ícone de detalhes para exibir os detalhes de cada descoberta de relatório


#### Propriedades do relatório {#report-properties}

O **Propriedades do relatório** O cartão fornece informações sobre propriedades do relatório, como data do relatório, duração, filtros, data de upload e detalhes do Adobe Experience Manager (AEM).

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### Visão geral do relatório {#report-overview}

Essa **Visão geral do relatório** O cartão fornece os resultados do relatório e os níveis de gravidade que se aplicam ao avaliar a disponibilidade para mudar para AEM as a Cloud Service, como mostrado na figura abaixo.

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

Clicar nesse relatório abre o **Relatório** guia .

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

Você pode filtrar o relatório com base na importância, no subtipo ou na contagem.

![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Consulte [Interpretação do relatório do Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) para saber mais sobre as categorias de descobertas e os níveis de importância.

#### Avaliação de práticas recomendadas {#best-practices-assessment}

A opção Avaliação de práticas recomendadas fornece uma avaliação da instância de AEM atual e fornece orientação sobre as próximas etapas para adotar AEM práticas recomendadas. Você pode revisar as seguintes informações nesta guia:

* Visão geral da instância de AEM
* Componentes e modelos personalizados
* Conclusões adicionais
* Consultas lentas
* Tarefas de manutenção

#### Avaliação da complexidade da migração {#migration-complexity-assessment}

A opção Avaliação da complexidade da migração fornece uma avaliação da complexidade para migrar a implementação de AEM existente para AEM as a Cloud Service.

Você pode revisar as seguintes informações nesta guia:

* Visão geral da instância de AEM
* Avaliação
* Considerações sobre a migração de conteúdo

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Uso do Cartão de Planejamento e Configuração {#planning-setup}

Siga esta seção para explorar o cartão de atividade Planejamento e configuração.

1. Clique no botão **Exibir** do botão **Planejamento E Configuração** cartão. Este cartão fornece todo o conteúdo relevante que ajudará você a planejar e configurar sua migração de AEM.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. Um carrossel de conteúdo exibe todas as informações relevantes para essa fase da jornada de migração.

   ![imagem](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

## O que vem a seguir {#whats-next}

Depois de aprender a fazer logon no Cloud Acceleration Manager e a criar um projeto, agora você está pronto para passar para a revisão da próxima etapa no [Fase de implementação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
