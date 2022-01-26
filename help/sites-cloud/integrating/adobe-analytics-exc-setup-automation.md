---
title: Integrar o Adobe Analytics com a automação de configuração do Experience Cloud
description: A Automação de configuração do Experience Cloud oferece uma maneira simples e automatizada de integrar e instrumentar o Experience Manager Sites com o Experience Platform Launch e o Adobe Analytics com uma interface simples de assistente de interface do usuário. Saiba como usar a configuração automatizada com seu próprio site.
feature: Administering
role: Admin
hide: true
hidefromtoc: true
index: false
source-git-commit: 6c84c0eff6392f1f86c18c9daf15c402c4d9e778
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# Integrar o Adobe Analytics com a automação de configuração do Experience Cloud {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> No momento, essa funcionalidade está na versão beta interna. A versão do Target está no primeiro trimestre de 2022.

A Automação de configuração do Experience Cloud oferece uma maneira simples e automatizada de integrar e instrumentar o Experience Manager Sites com o Experience Platform Launch e o Adobe Analytics com uma interface simples de assistente de interface do usuário.

Nunca foi mais simples integrar o Adobe Analytics com o AEM Sites. Com a Automação de configuração do Experience Cloud, a configuração, a integração e a instrumentação do site para capturar análises de desempenho para entender o desempenho de seus clientes se envolvendo e convertendo são todas tomadas conta com apenas alguns cliques.

Este vídeo explica como um site de AEM é integrado ao Experience Platform Launch e ao Analytics usando a Automação de configuração do Experience Cloud:

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## Requisitos

A configuração da automação foi projetada para funcionar imediatamente com um Site de AEM criado com o uso do [Componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) com o [Camada de dados do cliente Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html) habilitado. Você pode gerar um novo site que tenha esses recursos ativados automaticamente usando o [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) ou criando um site usando um [Modelo do site](/help/journey-sites/quick-site/create-site.md).

## Como configurar

1. Navegar para **Sites** e selecione a raiz do site a ser integrado ao Adobe Analytics.
1. Expanda o menu do painel lateral e toque em **Configurar Analytics**.

   Esta é uma nova opção no painel lateral que abrirá um painel que fornecerá controles e status para a Automação de configuração do Experience Cloud.
1. Toque no **Integrar o Analytics** botão.
1. Na caixa de diálogo resultante, forneça um nome para a variável **ID do conjunto de relatórios**.

   Essa string será usada para criar um novo [ID do conjunto de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=en) no Adobe Analytics como o armazenamento de dados para os dados analíticos do site de AEM selecionado. A cadeia de caracteres fornecida será anexada com identificadores de ambiente e camada para garantir exclusividade.

1. Atualize a página e o painel e toque em **Verificar status de integração** para verificar o status da automação.

   A configuração da automação ocorre de forma assíncrona. O **Verificar status de integração** mostrará o status atual da integração.

   * **Em andamento** - indica que a tarefa está em execução.
   * **Integração concluída** - indica que a tarefa concluiu a integração do Analytics e do Launch, a configuração das extensões do Launch e das regras do Launch e a criação do novo Conjunto de relatórios no Adobe Analytics.
   * **Falha** - indica que o trabalho automatizado não pôde ser concluído com êxito. Verifique os arquivos de log desse trabalho clicando no link Logs .

## Validar AEM configuração

Depois que a automação for concluída, valide se seu site está acionando os eventos do Analytics.

1. Abra uma página no seu site usando o **Editor de sites**.
1. Use o **Exibir como publicado** para carregar uma versão publicada da página.
1. Use as ferramentas de desenvolvedor do navegador para inspecionar o tráfego da rede e que **Launch** e `AppMeasurement.js` agora os arquivos estão sendo carregados.
1. Inspect o console do navegador para ver se os eventos de nível de página e componente são acionados e coletados pela Camada de dados do cliente do Adobe.

## Validar a configuração do Analytics

Em seguida, navegue até o Adobe Analytics para exibir os dados que fluem dos eventos no site de AEM.

1. Navegue até o Adobe Analytics na mesma Organização IMS que o site de AEM.
1. Crie um novo relatório de visão geral para o AEM Sites navegar até **Relatórios** > **Envolvimento** > **Adobe Experience Manager** > **Visão geral do desempenho do site**.
1. Toque **Abrir relatório**.
1. Selecione o **ID do conjunto de relatórios** que corresponde ao nome do Conjunto de relatórios usado no exercício anterior.
1. Visualize o fluxo de dados de análise no novo modelo ao longo do tempo.

   >[!NOTE]
   >
   > Com uma nova integração, pode levar algumas horas até que o relatório seja preenchido com dados.
