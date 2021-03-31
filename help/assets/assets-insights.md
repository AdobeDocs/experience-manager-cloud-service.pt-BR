---
title: 'Informações de ativos '
description: Saiba como o recurso Asset Insights permite que você acompanhe as classificações do usuário e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas do Adobe.
contentOwner: AG
feature: Insights de ativos,Relatórios de ativos
role: Profissional
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 9%

---


# Informações de ativos {#asset-insights}

O Asset Insights rastreia as estatísticas de uso e classificações de usuários de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas do Adobe. Ele ajuda a fornecer insights sobre o desempenho e a popularidade das imagens.

O Assets Insights captura detalhes da atividade do usuário, como o número de vezes que uma imagem é classificada, clicada e impressões (número de vezes que uma imagem é carregada no site). Ele atribui pontuações a imagens com base nessas estatísticas. Você pode usar as pontuações e as estatísticas de desempenho para selecionar imagens populares para inclusão em catálogos, campanhas de marketing e assim por diante. Você pode até mesmo formular políticas de arquivamento e renovação de licença com base nessas estatísticas.

Para que o Assets Insights capture as estatísticas de uso de imagens de um site, você deve incluir o código incorporado da imagem no código do site.

Para permitir que o Asset Insights exiba estatísticas de uso de ativos, primeiro configure o recurso para buscar dados de relatório do Adobe Analytics. Para obter detalhes, consulte [Configurar Asset Insights](#configure-asset-insights).

>[!NOTE]
>
>Os insights são suportados e fornecidos apenas para imagens.

## Exibir estatísticas de uma imagem {#viewing-statistics-for-an-image}

Você pode exibir as pontuações do Asset Insights da página de metadados.

1. Na interface do usuário do Assets (UI), selecione a imagem e toque em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página Propriedades, toque em **[!UICONTROL Insights]**.
1. Revise os detalhes de uso do ativo na guia **[!UICONTROL Insights]**. A seção **[!UICONTROL Pontuação]** descreve o uso total de ativos e as funções de desempenho de um ativo .

   A pontuação de uso descreve a quantidade de vezes que o ativo é usado em várias soluções.

   A pontuação **[!UICONTROL Impressões]** é o número de vezes que o ativo é carregado no site. O número exibido em **[!UICONTROL Clicks]** é o número de vezes que o ativo é clicado.

1. Revise a seção **[!UICONTROL Estatísticas de uso]** para saber quais entidades o ativo fazia parte e quais soluções criativas o usaram recentemente. Quanto maior for o uso, maior será a probabilidade de o ativo ser popular entre os usuários. Os dados de uso são exibidos abaixo dos seguintes cabeçalhos:

   * **[!UICONTROL Ativo]**: O número de vezes que o ativo fez parte de uma coleção ou de um ativo composto.
   * **[!UICONTROL Web e móvel]**: O número de vezes que o ativo fez parte de sites e aplicativos.
   * **[!UICONTROL Social]**: O número de vezes que o ativo foi usado em soluções, como Adobe Social e Adobe Campaign.
   * **[!UICONTROL Email]**: O número de vezes que o ativo foi usado em campanhas de email.

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Como o recurso Asset Insights normalmente busca os dados de Soluções da Adobe Analytics de maneira periódica, a seção Soluções pode não exibir os dados mais recentes. O período de tempo para o qual os dados são exibidos depende do agendamento da operação de busca executada pelo Asset Insights para recuperar dados do Analytics.

1. Para exibir estatísticas de desempenho do ativo graficamente durante um período de tempo, selecione o período na seção **[!UICONTROL Estatísticas de desempenho]**. Detalhes, incluindo cliques e impressões, são exibidos como linhas de tendência de um gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Ao contrário dos dados na seção Soluções , a seção Estatísticas de desempenho exibe os dados mais recentes.

1. Para obter o código incorporado do ativo que você inclui nos sites para obter dados de desempenho, toque/clique em **[!UICONTROL Obter código incorporado]** abaixo da miniatura do ativo. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Exibir estatísticas agregadas de imagens {#viewing-aggregate-statistics-for-images}

Exiba pontuações de todos os ativos em uma pasta simultaneamente usando a **[!UICONTROL Exibição do Insights]**.

1. Na interface do usuário do Assets, navegue até a pasta que contém os ativos para os quais deseja exibir insights.
1. Toque/clique no ícone Layout na barra de ferramentas e escolha **[!UICONTROL Exibição do Insights]**.
1. A página exibe as pontuações de uso dos ativos. Compare as classificações dos vários ativos e obtenha insights.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Asset Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Asset Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Configurar o Asset Insights {#configure-asset-insights}

[!DNL Experience Manager Assets] busca dados de uso em ativos digitais usados por sites de terceiros do  [!DNL Adobe Analytics]. Para permitir que o Asset Insights recupere esses dados e gere insights, primeiro configure o recurso para integrar com [!DNL Adobe Analytics].

>[!NOTE]
>
>Os insights são suportados e fornecidos apenas para imagens.

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Clique no cartão **[!UICONTROL Configuração do Insights]**.
1. No assistente, selecione um data center e forneça suas credenciais, incluindo o nome da organização, o nome de usuário e o Segredo compartilhado.

   ![Configurar o Adobe Analytics para o Assets Insights no  [!DNL Experience Manager]](assets/insights_config2.png)

   *Figura: Configurar o Adobe Analytics para o Assets Insights no[!DNL Experience Manager]*

1. Clique/toque em **[!UICONTROL Autenticar]**. Depois que [!DNL Experience Manager] autenticar suas credenciais, na lista **[!UICONTROL Report Suite]**, escolha um conjunto de relatórios do Adobe Analytics no qual deseja que o Asset Insights busque dados. Clique em **[!UICONTROL Adicionar]**.
1. Depois de [!DNL Experience Manager] configurar seu conjunto de relatórios, toque em **[!UICONTROL Concluído]**.

### Rastreador de página {#page-tracker}

Após configurar sua conta do Adobe Analytics, o código do Rastreador de página é gerado para você. Para permitir que o Assets Insights rastreie os ativos [!DNL Experience Manager] usados em sites de terceiros, inclua o código do rastreador de página no código do site. Use o utilitário do Rastreador de página no Assets para gerar o código do rastreador de página. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Na página **[!UICONTROL Navegação]**, clique no cartão do **[!UICONTROL Rastreador de páginas do Insights]**.
1. Clique em **[!UICONTROL Download]** para baixar o código do rastreador de página.

<!--

## Using demo package for Asset Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Asset Insights to capture data from and generate insights for a sample web page.

1. Configure Asset Insights using the instructions in [Configure Asset Insights](#configure-asset-insights).
1. Download the sample [!DNL Experience Manager Assets] package from below and install the package from CRXDE package manager.

   [Get File](assets/insightsdemo.zip)

1. Download the ZIP file containing the sample web page from below and extract on your local file system.

   [Get File](assets/demosite.zip)

1. Click the web page to open it in the web browser.

   >[!CAUTION]
   >
   >Web Page is configured to load asset from the localhost server . In case your server is running somewhere else change server address from localhost to server address in the HTML content of the web page.

   >[!NOTE]
   >
   >The external web page can be in [!DNL Experience Manager] itself.

-->
