---
title: Assets Insights
description: Acompanhe as classificações de usuário e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas da Adobe.
contentOwner: AG
feature: Asset Insights, Asset Reports
role: User, Leader
exl-id: e268453b-e7c0-4aa4-bd29-2686edb5f99a
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 11%

---

# Assets Insights {#asset-insights}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/asset-insights.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

A funcionalidade do Assets Insights permite rastrear as classificações de usuários e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas da Adobe. Ele ajuda a fornecer insights sobre o desempenho e a popularidade das imagens.

O Assets Insights captura detalhes da atividade do usuário, como o número de vezes que uma imagem é classificada, clicada e impressões (número de vezes que uma imagem é carregada no site). Ele atribui pontuações a imagens com base nessas estatísticas. Você pode usar as pontuações e as estatísticas de desempenho para selecionar imagens populares para inclusão em catálogos, campanhas de marketing e assim por diante. Você pode até mesmo formular políticas de arquivamento e renovação de licença com base nessas estatísticas.

Para que o Assets Insights capture estatísticas de uso de imagens de um site, você deve incluir o código incorporado da imagem no código do site.

Para permitir que o Assets Insights exiba estatísticas de uso para ativos, primeiro configure o recurso para buscar dados de relatórios de [!DNL Adobe Analytics]. Para obter detalhes, consulte [Configurar o Assets Insights](#configure-asset-insights). Para usar este recurso, compre a licença do [!DNL Adobe Analytics] separadamente.

>[!NOTE]
>
>Os insights são compatíveis e fornecidos apenas para imagens.

## Exibir estatísticas de uma imagem {#viewing-statistics-for-an-image}

Você pode exibir as pontuações do Assets Insights na página de metadados.

1. Na interface de usuário do Assets, selecione a imagem e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página Propriedades, clique em **[!UICONTROL Insights]**.
1. Revise os detalhes de uso do ativo na guia **[!UICONTROL Insights]**. A seção **[!UICONTROL Pontuação]** descreve o uso total de ativos e as pontuações de desempenho de um ativo.

   A pontuação de uso descreve o número de vezes que o ativo é usado em várias soluções.

   A pontuação de **[!UICONTROL Impressões]** é o número de vezes que o ativo é carregado no site. O número exibido em **[!UICONTROL Cliques]** é o número de vezes que o ativo é clicado.

1. Revise a seção **[!UICONTROL Estatísticas de uso]** para saber de quais entidades o ativo fazia parte e quais soluções criativas o usaram recentemente. Quanto maior for o uso, maior será a probabilidade de o ativo ser popular entre os usuários. Os dados de uso são exibidos abaixo dos seguintes cabeçalhos:

   * **[!UICONTROL Ativo]**: o número de vezes que o ativo fez parte de uma coleção ou de um ativo composto.
   * **[!UICONTROL Web e Mobile]**: o número de vezes que o ativo fez parte de sites e aplicativos.
   * **[!UICONTROL Social]**: o número de vezes que o ativo foi usado em outras soluções, como um [!DNL Adobe Campaign].
   * **[!UICONTROL Email]**: o número de vezes que o ativo foi usado em campanhas de email.

   ![estatísticas_de_uso](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Como o recurso Assets Insights normalmente busca os dados de Soluções de [!DNL Adobe Analytics] de maneira periódica, a seção Soluções pode não exibir os dados mais recentes. O período para o qual os dados são exibidos depende do agendamento da operação de busca que o Assets Insights executa para recuperar os dados do Analytics.

1. Para exibir estatísticas de desempenho do ativo graficamente durante um período de tempo, selecione o período na seção **[!UICONTROL Estatísticas de desempenho]**. Detalhes, incluindo cliques e impressões, são exibidos como linhas de tendência de um gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Ao contrário dos dados na seção Soluções, a seção Estatísticas de desempenho exibe os dados mais recentes.

1. Para obter o código de inserção para o ativo incluído nos sites para obter dados de desempenho, clique em **[!UICONTROL Obter código de inserção]** abaixo da miniatura do ativo. <!-- For more information on how to include your Embed code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

   ![chlimage_1-98](assets/chlimage_1-98.png)

## Exibir estatísticas agregadas para imagens {#viewing-aggregate-statistics-for-images}

Exiba pontuações de todos os ativos em uma pasta simultaneamente usando a **[!UICONTROL Exibição do Insights]**.

1. Na interface do usuário do Assets, navegue até a pasta que contém os ativos para os quais deseja exibir insights.
1. Clique na opção **[!UICONTROL Layout]** da barra de ferramentas e escolha **[!UICONTROL Exibição do Insights]**.
1. A página exibe as pontuações de uso dos ativos. Compare as classificações dos vários ativos e obtenha insights.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Schedule background job {#scheduling-background-job}

Assets Insights fetches usage data for assets from Adobe Analytics report suites in a periodic manner. By default, Assets Insights runs a background job every 24 hours at 2 AM to the fetch data. However, you can modify both the frequency and the time by configuring the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service from the web console.

1. Click the [!DNL Experience Manager] logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Open the **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** service configuration.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Specify the desired scheduler frequency and the start time for the job in the property scheduler expression. Save the changes.
-->

## Configurar o Assets Insights {#configure-asset-insights}

[!DNL Experience Manager Assets] busca dados de uso sobre ativos digitais usados por sites de terceiros de [!DNL Adobe Analytics]. Para permitir que o Assets Insights recupere esses dados e gere insights, primeiro configure o recurso para integrar com o [!DNL Adobe Analytics].

>[!NOTE]
>
>Os insights só são aceitos e fornecidos para imagens.

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Clique no cartão **[!UICONTROL Configuração do Insights]**.

1. Para obter informações sobre acesso aos serviços Web do Analytics, vá para **[!UICONTROL Analytics]** > **[!UICONTROL Admin]** > **[!UICONTROL Ferramentas Administrativas]** > **[!UICONTROL Configurações da Empresa]** > **[!UICONTROL Serviços Web]** e copie a chave **[!UICONTROL Segredo Compartilhado]**.

   No assistente, selecione o **[!UICONTROL Data Center]** e forneça o nome de exibição da **[!UICONTROL Empresa]**, Serviços Web **[!UICONTROL Nome de Usuário]** e cole a chave **[!UICONTROL Segredo Compartilhado]**.

   Clique em **[!UICONTROL Autenticar]**.

   ![Configurar o Adobe Analytics para o Assets Insights em [!DNL Experience Manager]](assets/analytics-insight-config.png)

   *Figura: Configurar o Adobe Analytics para o Assets Insights no[!DNL Experience Manager]*

1. Após a autenticação bem-sucedida, os conjuntos de relatórios serão listados no menu suspenso. Selecione o **[!UICONTROL Conjunto de relatórios]** do Adobe Analytics de onde deseja que o Assets Insights busque dados. Clique em **[!UICONTROL Adicionar]**.

1. Depois que [!DNL Experience Manager] configurar seu conjunto de relatórios, clique em **[!UICONTROL Concluído]**.

Para obter mais informações, consulte [Adobe Analytics Web Services](https://experienceleague.adobe.com/docs/analytics/admin/company-settings/web-services-admin.html?lang=pt-BR#api-access-information).

### Rastreador de páginas {#page-tracker}

Após configurar sua conta do Adobe Analytics, o código do Rastreador de páginas é gerado para você. Para permitir que o Assets Insights rastreie os [!DNL Experience Manager] ativos usados em sites de terceiros, inclua o código do rastreador de página no código do site. Use o utilitário Rastreador de páginas no Assets para gerar o código do rastreador de páginas. <!--  For more information on how to include your Page Tracker code in third-party web pages, see [Using Page Tracker and Embed code in web pages](/help/assets/use-page-tracker.md). -->

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. Na página **[!UICONTROL Navegação]**, clique no cartão do **[!UICONTROL Rastreador de páginas do Insights]**.
1. Clique em **[!UICONTROL Baixar]** para baixar o código do rastreador de página.

<!--
Add page tracker code, CQDOC-18045, 30/07/2021
-->
O trecho de código de exemplo a seguir exibe o código do Rastreador de páginas incluído em uma página da Web de exemplo:

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```



<!--

## Using demo package for Assets Insights {#using-demo-package-for-asset-insights}

Using the demo package, you can enable Adobe Assets Insights to capture data from and generate insights for a sample web page.

1. Configure Assets Insights using the instructions in [Configure Assets Insights](#configure-asset-insights).
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

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
