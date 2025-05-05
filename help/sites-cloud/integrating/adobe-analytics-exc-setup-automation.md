---
title: Integrar o Adobe Analytics com a automação de configuração do Experience Cloud
description: A Automação de configuração da Experience Cloud oferece uma maneira simples e automatizada de integrar e instrumentar o Experience Manager Sites com Tags da Experience Platform e Adobe Analytics com uma interface de assistente simples. Saiba como usar a configuração automatizada em seu próprio site.
feature: Integration
role: Admin
exl-id: 351ead2c-7b0d-4bd9-a020-47516948d467
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 87%

---

# Integrar o Adobe Analytics com a automação de configuração do Experience Cloud {#integrate-adobe-analytics-automation-setup}

A Automação de configuração da Experience Cloud oferece uma maneira simples e automatizada de integrar e instrumentar o Experience Manager Sites com Tags da Experience Platform e Adobe Analytics com uma interface de assistente simples.

Nunca foi tão simples integrar o Adobe Analytics com o AEM Sites. Com a Automação de configuração do Experience Cloud, a configuração, a integração e a instrumentação do site para capturar análises de desempenho e entender o quão bem seus clientes estão interagindo e se convertendo são todas resolvidas com apenas alguns cliques.

Este vídeo explica como um site do AEM pode ser integrado às Tags da Experience Platform e ao Analytics usando a Automação de configuração da Experience Cloud:

>[!VIDEO](https://video.tv.adobe.com/v/345372/?quality=12)

## Requisitos

A configuração da automação foi projetada para funcionar prontamente com um site do AEM criado com o uso dos [Componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR), com a [Camada de dados do cliente Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=pt-BR) habilitada. É possível gerar um novo site que tenha esses recursos habilitados automaticamente usando o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) ou criando um site usando um [Modelo de site](/help/journey-sites/quick-site/create-site.md).

## Pré-requisitos {#prerequisites}

Antes de usar esse recurso, é importante seguir estas instruções para garantir que os serviços de pré-requisitos tenham sido configurados corretamente em seu ambiente:

1. Faça logon no Adobe Admin Console (https://adminconsole.adobe.com/).
1. Verifique se a ID da organização IMS adequada está selecionada no canto superior direito.
1. Clique na opção de navegação de Produtos.
1. Verifique se o “Adobe Experience Manager as a Cloud Service” foi provisionado para a organização IMS.
1. Verifique se o “Adobe Analytics” foi provisionado para a organização IMS.
1. Acesse o Cloud Manager (https://experience.adobe.com/cloud-manager).
1. Selecione o programa apropriado.
1. Verifique se o ambiente está na versão mais recente do Cloud Service (caso contrário, selecione Atualizar nas opções do menu).
1. Execute um pipeline de pilha completa no Cloud Manager.

O ambiente agora deve estar pronto para a automação de configuração da Experience Cloud.

## Como configurar

1. Navegue até **Sites** e selecione a raiz do site a ser integrado ao Adobe Analytics.
1. Expanda o menu do painel lateral e selecione **Configurar Analytics**.

   Esta é uma nova opção no painel lateral que abre um painel e fornece controles e status para a Automação de configuração do Experience Cloud.
1. Selecione o botão **Integrar o Analytics**.
1. Na caixa de diálogo resultante, forneça um nome para a **ID do conjunto de relatórios**.

   Esta cadeia de caracteres é usada para criar um [ID do Conjunto de Relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=pt-BR) no Adobe Analytics como o armazenamento de dados para os dados analíticos do site AEM selecionado. A string fornecida tem anexada os identificadores de ambiente e de nível para garantir a exclusividade.

1. Atualize a página e o painel e selecione **Verificar Status da Integração** para verificar o status da automação.

   A configuração da automação ocorre de maneira assíncrona. O **Verificar status da integração** mostrará o status atual da integração.

   * **Em andamento** - indica que a tarefa está em execução.
   * **Integração concluída** - indica que o processo concluiu a integração do Analytics e das tags, configurando extensões de tags e regras de tags e criando o novo conjunto de relatórios no Adobe Analytics.
   * **Fracasso** - indica que a tarefa automatizada não pôde ser concluída com êxito. Verifique os arquivos de log dessa tarefa clicando no link Logs.

## Validar configuração do AEM 

Depois que a automação for concluída, valide se seu site está acionando os eventos do Analytics.

1. Abra uma página no seu site usando o **Editor de sites**.
1. Use a opção **Exibir conforme publicado** para carregar uma versão publicada da página
1. Use as ferramentas de desenvolvedor do navegador para inspecionar o tráfego da rede e se agora os arquivos de **Tags** e do `AppMeasurement.js` estão sendo carregados.
1. Inspecione o console do navegador para conferir se os eventos de nível de página e componente são acionados e coletados pela Camada de dados do cliente Adobe.

## Validar a configuração do Analytics

Em seguida, navegue até o Adobe Analytics para visualizar os dados que fluem dos eventos no site do AEM.

1. Navegue até o Adobe Analytics na mesma organização IMS do site do AEM.
1. Crie um novo relatório de visão geral do AEM Sites navegando até **Relatórios** > **Envolvimento** > **Adobe Experience Manager** > **Visão geral do desempenho do site**.
1. Selecione **Abrir Relatório**.
1. Selecione a **ID do conjunto de relatórios** que corresponde ao nome do Conjunto de relatórios usado no exercício anterior.
1. Visualize o fluxo de dados de análise no novo modelo ao longo do tempo.

   >[!NOTE]
   >
   > Com uma nova integração, pode levar algumas horas até que o relatório seja preenchido com dados.
