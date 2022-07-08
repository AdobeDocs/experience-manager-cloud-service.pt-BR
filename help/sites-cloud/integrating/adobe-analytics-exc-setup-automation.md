---
title: Integrar o Adobe Analytics com a automação de configuração do Experience Cloud
description: A Automação de configuração do Experience Cloud oferece uma maneira simples e automatizada de integrar e instrumentar o Experience Manager Sites com o Experience Platform Launch e o Adobe Analytics usando uma interface simples de assistente. Saiba como usar a configuração automatizada em seu próprio site.
feature: Administering
role: Admin
hide: true
hidefromtoc: true
index: false
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '639'
ht-degree: 100%

---

# Integrar o Adobe Analytics com a automação de configuração do Experience Cloud {#integrate-adobe-analytics-automation-setup}

>[!CAUTION]
>
> No momento, essa funcionalidade está na versão beta interna. A versão do Target será lançada no primeiro trimestre de 2022.

A Automação de configuração do Experience Cloud oferece uma maneira simples e automatizada de integrar e instrumentar o Experience Manager Sites com o Experience Platform Launch e o Adobe Analytics usando uma interface simples de assistente.

Nunca foi tão simples integrar o Adobe Analytics com o AEM Sites. Com a Automação de configuração do Experience Cloud, a configuração, a integração e a instrumentação do site para capturar análises de desempenho e entender o quão bem seus clientes estão interagindo e se convertendo são todas resolvidas com apenas alguns cliques.

Este vídeo explica como um site do AEM pode ser integrado ao Experience Platform Launch e ao Analytics usando a Automação de configuração do Experience Cloud:

>[!VIDEO](https://video.tv.adobe.com/v/339605/?quality=12)

## Requisitos

A configuração da automação foi projetada para funcionar prontamente com um site do AEM criado com o uso dos [Componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR), com a [Camada de dados do cliente Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=pt_BR) habilitada. É possível gerar um novo site que tenha esses recursos habilitados automaticamente usando o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt_BR) ou criando um site usando um [Modelo de site](/help/journey-sites/quick-site/create-site.md).

## Como configurar

1. Navegue até **Sites** e selecione a raiz do site a ser integrado ao Adobe Analytics.
1. Expanda o menu do painel lateral e toque em **Configurar o Analytics**.

   Esta é uma nova opção no painel lateral que abrirá um painel e fornecerá controles e status para a Automação de configuração do Experience Cloud.
1. Toque no botão **Integrar o Analytics**.
1. Na caixa de diálogo resultante, forneça um nome para a **ID do conjunto de relatórios**.

   Esta sequência de caracteres será usada para criar um novo [ID do conjunto de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=pt_BR) no Adobe Analytics como o armazenamento de dados para os dados analíticos do site do AEM selecionado. A sequência de caracteres fornecida será anexada com identificadores de ambiente e nível para garantir a exclusividade.

1. Atualize a página e o painel e toque em **Verificar status da integração** para verificar o status da automação.

   A configuração da automação ocorre de maneira assíncrona. O **Verificar status da integração** mostrará o status atual da integração.

   * **Em andamento** - indica que a tarefa está em execução.
   * **Integração concluída** - indica que a tarefa concluiu a integração do Analytics e do Launch, a configuração das extensões e das regras do Launch e a criação do novo Conjunto de relatórios no Adobe Analytics.
   * **Fracasso** - indica que a tarefa automatizada não pôde ser concluída com êxito. Verifique os arquivos de log dessa tarefa clicando no link Logs.

## Validar configuração do AEM 

Depois que a automação for concluída, valide se seu site está acionando os eventos do Analytics.

1. Abra uma página no seu site usando o **Editor de sites**.
1. Use a opção **Exibir conforme publicado** para carregar uma versão publicada da página
1. Use as ferramentas de desenvolvedor do navegador para inspecionar o tráfego da rede e que agora os arquivos do **Launch** e do `AppMeasurement.js` estão sendo carregados.
1. Inspecione o console do navegador para conferir se os eventos de nível de página e componente são acionados e coletados pela Camada de dados do cliente Adobe.

## Validar a configuração do Analytics

Em seguida, navegue até o Adobe Analytics para visualizar os dados que fluem dos eventos no site do AEM.

1. Navegue até o Adobe Analytics na mesma organização IMS do site do AEM.
1. Crie um novo relatório de visão geral do AEM Sites navegando até **Relatórios** > **Envolvimento** > **Adobe Experience Manager** > **Visão geral do desempenho do site**.
1. Toque em **Abrir relatório**.
1. Selecione a **ID do conjunto de relatórios** que corresponde ao nome do Conjunto de relatórios usado no exercício anterior.
1. Visualize o fluxo de dados de análise no novo modelo ao longo do tempo.

   >[!NOTE]
   >
   > Com uma nova integração, pode levar algumas horas até que o relatório seja preenchido com dados.
