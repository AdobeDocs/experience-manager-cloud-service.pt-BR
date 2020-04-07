---
title: 'Informações de ativos '
description: Saiba como o recurso Asset Insights permite rastrear as classificações de usuários e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas da Adobe.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Informações de ativos {#asset-insights}

Os Asset Insights acompanham as classificações de usuários e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas da Adobe. Ele ajuda a fornecer insights sobre o desempenho e a popularidade das imagens.

O Assets Insights captura detalhes da atividade do usuário, como o número de vezes que uma imagem é classificada, clicada e impressões (número de vezes que uma imagem é carregada no site). Ele atribui pontuações a imagens com base nessas estatísticas. Você pode usar as estatísticas de pontuação e desempenho para selecionar imagens populares para inclusão em catálogos, campanhas de marketing e assim por diante. Você pode até mesmo formular políticas de arquivamento e renovação de licença com base nessas estatísticas.

Para que o Assets Insights capture as estatísticas de uso de imagens de um site, você deve incluir o código incorporado da imagem no código do site.

Para permitir que o Asset Insights exiba estatísticas de uso de ativos, configure primeiro o recurso para buscar dados de relatórios do Adobe Analytics. Para obter detalhes, consulte [Configurar insights](#configure-asset-insights)de ativos.

>[!NOTE]
>
>Os insights só são suportados e fornecidos para imagens.

## Estatísticas de Visualização para uma imagem {#viewing-statistics-for-an-image}

Você pode visualização as pontuações do Asset Insights na página de metadados.

1. Na interface do usuário do Assets (UI), selecione a imagem e toque em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página Propriedades, toque em **[!UICONTROL Insights]**.
1. Revise os detalhes de uso do ativo na guia **[!UICONTROL Insights]** . A seção **[!UICONTROL Pontuação]** descreve o uso total de ativos e as funções de desempenho de um ativo.

   A pontuação de uso descreve o número de vezes que o ativo é usado em várias soluções.

   A pontuação de **[!UICONTROL impressões]** é o número de vezes que o ativo é carregado no site. O número exibido em **[!UICONTROL Cliques]** é o número de vezes que o ativo é clicado.

1. Revise a seção Estatísticas **[!UICONTROL de]** uso para saber de quais entidades o ativo fazia parte e quais soluções criativas o utilizaram recentemente. Quanto maior o uso, maiores as chances de que o ativo seja popular entre os usuários. Os dados de uso são exibidos sob os seguintes cabeçalhos:

   * **[!UICONTROL Ativo]**: O número de vezes que o ativo fez parte de uma coleção ou de um ativo composto.
   * **[!UICONTROL Web e dispositivos móveis]**: O número de vezes que o ativo fez parte de sites e aplicativos.
   * **[!UICONTROL Social]**: O número de vezes que o ativo foi usado em soluções, como o Adobe Social e o Adobe Campaign.
   * **[!UICONTROL Email]**: O número de vezes que o ativo foi usado em campanhas de email.
   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Como o recurso Asset Insights normalmente obtém os dados de Soluções do Adobe Analytics de forma periódica, a seção Soluções pode não exibir os dados mais recentes. O período de tempo para o qual os dados são exibidos depende da programação da operação de busca executada pelo Asset Insights para recuperar os dados do Analytics.

1. Para exibir estatísticas de desempenho do ativo graficamente durante um período de tempo, selecione o período na seção **[!UICONTROL Estatísticas de desempenho]**. Detalhes, incluindo cliques e impressões, são exibidos como linhas de tendência de um gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Ao contrário dos dados na seção Soluções, a seção Estatísticas de desempenho exibe os dados mais recentes.

1. Para obter o código incorporado para o ativo que você inclui em sites para obter dados de desempenho, toque/clique em **[!UICONTROL Obter código]** incorporado abaixo da miniatura do ativo. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Estatísticas de agregação de Visualizações para imagens {#viewing-aggregate-statistics-for-images}

Exiba pontuações de todos os ativos em uma pasta simultaneamente usando a **[!UICONTROL Exibição do Insights]**.

1. Na interface do usuário Ativos, navegue até a pasta que contém os ativos para os quais você deseja visualização insights.
1. Toque/clique no ícone Layout na barra de ferramentas e escolha **[!UICONTROL Visualização]** Insights.
1. A página exibe as pontuações de uso dos ativos. Compare as classificações dos vários ativos e obtenha insights.

## Agendar tarefa em segundo plano {#scheduling-background-job}

O Asset Insights busca os dados de uso de ativos dos conjuntos de relatórios do Adobe Analytics de forma periódica. Por padrão, o Asset Insights executa uma tarefa em segundo plano a cada 24 horas às 2 horas da manhã para obter dados. No entanto, você pode modificar a frequência e a hora configurando o serviço Trabalho **[!UICONTROL de sincronização de relatório de desempenho de ativos do]** Adobe CQ DAM no console da Web.

1. Toque no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Abra a configuração do serviço **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** .

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Especifique a frequência de scheduler desejada e a hora de start para o trabalho na expressão de scheduler de propriedade. Salve as alterações.

## Configurar insights de ativos {#configure-asset-insights}

O Adobe Experience Manager (AEM) Assets obtém dados de uso em ativos AEM usados por sites de terceiros do Adobe Analytics. Para permitir que o Asset Insights recupere esses dados e gere insights, configure primeiro o recurso para integrar-se ao Adobe Analytics.

>[!NOTE]
>
>Os insights só são suportados e fornecidos para imagens.

1. No AEM, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Clique no cartão **[!UICONTROL Configuração do Insights]**.
1. No assistente, selecione um centro de dados e forneça suas credenciais, incluindo o nome de sua organização, o nome de usuário e o Segredo compartilhado.

   ![Configurar o Adobe Analytics para insights de ativos no AEM](assets/insights_config2.png)

   *Figura: Configurar o Adobe Analytics para insights de ativos no AEM*

1. Clique/toque em **[!UICONTROL Autenticar]**. Depois que o AEM autenticar suas credenciais, na lista **[!UICONTROL Report Suite]** , escolha um conjunto de relatórios do Adobe Analytics de onde deseja que o Asset Insights busque dados. Clique em **[!UICONTROL Adicionar]**.
1. Depois que o AEM configurar seu conjunto de relatórios, toque em **[!UICONTROL Concluído]**.

### Rastreador de página {#page-tracker}

Depois de configurar sua conta do Adobe Analytics, o código do rastreador de páginas é gerado para você. Para ativar o Assets Insights para rastrear ativos AEM usados em sites de terceiros, inclua o código do rastreador de página no código do site. Use o utilitário do rastreador de páginas nos ativos AEM para gerar o código do rastreador de páginas. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. No AEM, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Na página **[!UICONTROL Navegação]**, clique no cartão do **[!UICONTROL Rastreador de páginas do Insights]**.
1. Clique em **[!UICONTROL Download]** para baixar o código do rastreador de página.

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
1. Download the sample AEM Assets package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in AEM itself.

-->
