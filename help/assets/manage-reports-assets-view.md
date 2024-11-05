---
title: Gerenciar relatórios na visualização do Assets
description: Acesse os dados na seção de relatórios da visualização do Assets para avaliar o uso de produtos e recursos e obter insights sobre as principais métricas de sucesso.
exl-id: 26d0289e-445a-4b8e-a5a1-b02beedbc3f1
feature: Asset Insights, Asset Reports
role: User, Admin, Developer
source-git-commit: 5ff36490c4d9a6f61255ad06ffab984f18c1823b
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 29%

---

# Gerenciamento de relatórios {#manage-reports}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Os relatórios de ativos fornecem aos administradores visibilidade sobre as atividades do ambiente de exibição do Adobe Experience Manager Assets. Esses dados fornecem informações úteis sobre como os usuários interagem com o conteúdo e o produto. Todos os(as) usuários(as) podem acessar o painel Insights e aqueles que estiverem atribuídos(as) ao perfil de produto Administrador podem criar relatórios definidos pelo(a) usuário(a).

## Acessar relatórios {#access-reports}

Todos os usuários atribuídos ao perfil de produto de administradores da visualização do Assets podem acessar o painel Insights e criar relatórios definidos pelo usuário na visualização do Assets.

Para acessar os relatórios, navegue até **[!UICONTROL Relatórios]** em **[!UICONTROL Configurações]**.

![Relatórios](assets/reports.png)

<!--
In the **[!UICONTROL Reports]** screen, various components are shown in the tabular format which includes the following:

* **Title**: Title of the report
* **Type**: Determines whether the report is uploaded or downloaded to the repository
* **Description**: Provide details of the report that was given during uploading/downloading the report
* **Status**: Determines whether the report is completed, under progress, or deleted.
* **Author**: Provides email of the author who has uploaded/downloaded the report.
* **Created**: Gives information of the date when the report was generated.
-->

## Criar um relatório {#create-report}

O ambiente de exibição do AEM Assets oferece recursos abrangentes de relatórios por meio do painel Relatórios. Esse recurso permite que os usuários gerem e baixem relatórios CSV detalhando uploads e downloads de ativos em intervalos de tempo especificados, que variam de uma vez a diários, semanais, mensais ou anuais.

**Para criar um relatório:**

1. Navegue até **Relatórios** e clique em **Criar relatório** (na parte superior direita). A caixa de diálogo **criar relatório** exibe os seguintes campos:
   ![criar-relatório](/help/assets/assets/executed-reports1.svg)

   **Na guia Configuração:**

   1. **Tipo de relatório:** selecione entre o tipo de carregamento e download.
   1. **Título:** Adicione um título ao relatório.
   1. **Descrição:** Adicione uma descrição opcional ao relatório.
   1. **Selecionar caminho da pasta:** selecione um caminho de pasta para gerar o relatório de ativos carregados e baixados dentro dessa pasta específica. Por exemplo, se você precisar do relatório de ativos carregados em uma pasta, especifique o caminho para essa pasta.
   1. **Selecionar intervalo de datas:** Selecione o intervalo de datas para exibir a atividade de carregamento ou download na pasta.
   <br>

   >[!NOTE]
   >
   > A visualização do Assets converte todos os fusos horários locais para o Tempo Universal Coordenado (UTC).

   **Na Guia Colunas:** Selecione os nomes das colunas a serem exibidas no relatório. A tabela a seguir explica o uso de todas as colunas:

   <table>
    <tbody>
     <tr>
      <th><strong>Nome da coluna</strong></th>
      <th><strong>Descrição</strong></th>
      <th><strong>Tipo de relatório</strong></th>
     </tr>
     <tr>
      <td>Título</td>
      <td>O título do ativo.</td>
      <td>Fazer upload e baixar</td>
     </tr>
     <tr>
      <td>Caminho</td>
      <td>O caminho da pasta onde o ativo está disponível na visualização do Assets.</td>
      <td>Fazer upload e baixar</td>
     </tr>
     <tr>
      <td>Tipo MIME</td>
      <td>O tipo MIME do ativo.</td>
      <td>Fazer upload e baixar</td>
     </tr>
     <tr>
      <td>Tamanho</td>
      <td>O tamanho do ativo em bytes.</td>
      <td>Fazer upload e baixar</td>
     </tr>
     <tr>
      <td>Baixado por</td>
      <td>A ID do email do usuário que baixou o ativo.</td>
      <td>Download</td>
     </tr>
     <tr>
      <td>Data de download</td>
      <td>A data em que a ação de download do ativo foi executada.</td>
      <td>Download</td>
     </tr>
     <tr>
      <td>Autor</td>
      <td>O autor do ativo.</td>
      <td>Fazer upload e baixar</td>
     </tr>
     <tr>
      <td>Data de criação</td>
      <td>A data em que o ativo foi enviado para a visualização do Assets.</td>
      <td>Fazer upload e baixar</td>
     </tr>
     <tr>
      <td>Data da modificação</td>
      <td>A data em que o ativo foi modificado pela última vez.</td>
      <td>Fazer upload e baixar</td>
     </tr>
     <tr>
      <td>Expirado</td>
      <td>O status de expiração do ativo.</td>
      <td>Fazer upload e baixar</td>
     </tr>
     <tr>
      <td>Baixado por Nome de usuário</td>
      <td>O nome do usuário que baixou o ativo.</td>
      <td>Download</td>
     </tr>           
    </tbody>
   </table>

## Exibir e baixar relatório existente {#View-and-download-existing-report}

Os relatórios existentes são exibidos na guia **Relatórios executados**. Clique em **Relatórios** e selecione **Relatórios Executados** para exibir todos os relatórios criados com o status **concluído**, indicando que eles estão prontos para download. Para baixar o relatório no formato CSV ou excluí-lo, selecione a linha de relatório. Em seguida, selecione **Baixar CSV** ou **Excluir**.
![exibir e baixar relatórios existentes](/help/assets/assets/view-download-existing-report.png)

## Agendar um relatório {#schedule-report}

Na interface de exibição do AEM Assets, o **Agendar Relatório** configura uma geração automática de relatórios em intervalos futuros especificados, como diariamente, semanalmente, mensalmente ou anualmente. Esse recurso ajuda a simplificar as necessidades de relatórios recorrentes e garante atualizações de dados oportunas. Enquanto o **Criar Relatório** gera relatórios de datas passadas. Os relatórios concluídos estão listados em **Relatórios Executados** e os próximos relatórios serão encontrados em **Relatórios Agendados**.

Para agendar um relatório, siga as etapas abaixo:

1. Clique em Relatórios no painel esquerdo e, em seguida, clique em Criar relatório (no canto superior direito).
1. A caixa de diálogo do relatório exibe as informações abaixo:
   1. **Tipo de relatório:** selecione entre o tipo de carregamento e download.
   1. **Título:** Adicione um título ao relatório.
   1. **Descrição**: adicione uma descrição opcional ao relatório.
   1. **Selecionar caminho da pasta:** Selecione um caminho de pasta para gerar um relatório para os ativos que serão carregados ou baixados dessa pasta específica no futuro.
   1. Alternar **Relatório de agendamento:** para agendar o relatório para um momento posterior ou para sua ocorrência repetida.
      ![agendar relatório](/help/assets/assets/schedule-reports1.svg)

   1. **Escolha a frequência:** especifique o intervalo para gerar o relatório (por exemplo, diário, semanal, mensal, anual ou uma vez) e defina a data e a hora para executar o relatório junto com a data final para recorrência. Para um relatório único, selecione o intervalo de datas para o relatório sobre o tipo de atividade selecionado no ambiente AEM. Por exemplo, se você precisar de um relatório sobre ativos baixados do dia 10 ao dia 29 (datas futuras) de um mês específico, selecione essas datas no campo **Selecionar intervalo de datas**.

   >[!NOTE]
   >
   > A visualização do Assets converte todos os fusos horários locais para o Tempo Universal Coordenado (UTC).

## Visualizar Relatórios Agendados {#view-scheduled-reports}

Os relatórios agendados são exibidos na guia **Relatórios agendados** de forma organizada sistematicamente. Todos os relatórios concluídos para cada relatório agendado são armazenados em uma única pasta de relatório. Clique em![expandir recolher](/help/assets/assets/expand-icon1.svg)para exibir os relatórios concluídos. Por exemplo, se você tiver agendado um relatório diário, todos os relatórios concluídos serão agrupados em uma pasta. Essa organização simplifica a navegação e a capacidade de descoberta dos relatórios. Para exibir os relatórios agendados, clique em **Relatórios** e em **Relatórios Agendados**. Todos os relatórios agendados são exibidos com o status em andamento ou concluído. Os relatórios concluídos estão prontos para download.\
![relatório agendado](/help/assets/assets/scheduled-reports-tab.png)

## Editar e cancelar relatórios agendados {#edit-cancel-scheduled-reports}

1. Navegue até a guia **Relatórios agendados**.
1. Selecione a linha do relatório.
1. Clique em **Editar**.
1. Clique em **Cancelar Agendamento** e em **Confirmar** para cancelar o relatório agendado. Para relatórios cancelados, o próximo tempo de execução fica vazio e o status mostra cancelado.
   ![editar e cancelar o relatório agendado](/help/assets/assets/cancel-edit-scheduled-reports.png)

### Retomar cronograma {#resume-schedule}

Para retomar o agendamento cancelado, selecione a linha de relatório e clique em **Retomar Agendamento**. Quando retomadas, as próximas entradas de tempo de execução são exibidas novamente e o status mostra em andamento.
![retomar agendamento](/help/assets/assets/resume-schedule.png)

>[!NOTE]
>
> Se você retomar um relatório cancelado antes da data final programada, os relatórios da data de cancelamento até a data de retomada serão gerados automaticamente.

## Exibir o Insights {#view-live-statistics}

A visualização do Assets permite visualizar dados do seu ambiente da visualização do Assets em tempo real, por meio do painel Insights. Você pode visualizar métricas de evento em tempo real dos últimos 30 dias ou dos últimos 12 meses.

<!--![Toolbar options when you select an asset](assets/assets-view-live-statistics.png)-->

Clique na opção **[!UICONTROL Insights]**, disponível no painel de navegação esquerdo, para exibir os seguintes gráficos gerados automaticamente:

* **Downloads**: o número de ativos baixados do ambiente de exibição do Assets nos últimos 30 dias ou 12 meses representados usando um gráfico de linhas.
  ![downloads-insights](/help/assets/assets/insights-downloads2341.svg)

* **Carregamentos**: o número de ativos carregados para o ambiente de exibição do Assets nos últimos 30 dias ou 12 meses representados usando um gráfico de linhas.
  ![uploads-insights](/help/assets/assets/insights-uplods2.svg)
  <!--* **Asset Count by Size**: The division of count of assets based on their range of various sizes from 0 MB to 100 GB.-->

* **Uso de armazenamento**: o uso de armazenamento, em bytes, para o ambiente de exibição do Assets representado por um gráfico de barras.
  ![uploads-insights](/help/assets/assets/insights-storage-usage1.svg)
  <!--* **Delivery**: The graph depicts the count of assets as the delivery dates.-->

<!--* **Asset Count by Asset Type**: Represents count of various MIME types of the available assets. For example, application/zip, image/png, video/mp4, application/postscripte.-->

* **Principais Pesquisas**: visualize os principais termos pesquisados junto com o número de vezes que esses termos foram pesquisados no ambiente de visualização do Assets nos últimos 30 dias ou 12 meses representados em formato de tabela.
  ![uploads-insights](/help/assets/assets/insights-top-search.svg)
  <!--
   ![Insights](assets/insights1.png)
   ![Insights](assets/insights2.png)
   -->
* **Contagem de ativos por tamanho:** segmenta a contagem total de ativos no seu ambiente de visualização de ativos em intervalos de tamanhos diferentes, realçando a contagem e a porcentagem de ativos em cada intervalo de tamanhos, representadas por um gráfico de rosquinha.
  ![insights-assets-count-by-size](/help/assets/assets/insights-assets-count-by-size.svg)
* **Contagem de ativos por tipo de ativo:** segmenta a contagem total de ativos no seu ambiente do Assets View, destacando a contagem e a porcentagem de ativos com base em seus tipos de arquivos, representados por um gráfico de rosca.
  ![insights-assets-count-by-size](/help/assets/assets/insights-assest-count-by-asset-type1.svg)