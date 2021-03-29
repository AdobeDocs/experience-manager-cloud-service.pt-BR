---
title: Guia de início rápido sem cabeçalho para acessar e entregar fragmentos de conteúdo
description: Saiba como usar AEM API REST do Assets para gerenciar Fragmentos de conteúdo e a API GraphQL para entrega sem interface do conteúdo do Fragmento de conteúdo.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Acessar e entregar fragmentos de conteúdo sem cabeçalho Guia de início rápido {#accessing-delivering-content-fragments}

Saiba como usar AEM API REST do Assets para gerenciar Fragmentos de conteúdo e a API GraphQL para entrega sem interface do conteúdo do Fragmento de conteúdo.

## O que são APIs REST de GraphQL e Assets? {#what-are-the-apis}

[Depois de criar alguns fragmentos de conteúdo, ](create-content-fragment.md) você pode usar AEM APIs para entregá-los sem periféricos.

* [A ](/help/assets/content-fragments/graphql-api-content-fragments.md) API GraphQL permite criar solicitações para acessar e fornecer Fragmentos de conteúdo.
* [A ](/help/assets/content-fragments/assets-api-content-fragments.md) API REST de ativos permite criar e modificar Fragmentos de conteúdo (e outros ativos).

O restante deste guia terá como foco o acesso GraphQL e a entrega do Fragmento de conteúdo.

## Como entregar um fragmento de conteúdo usando GraphQL {#how-to-deliver-a-content-fragment}

Os arquitetos de informações precisarão projetar consultas para seus pontos de extremidade de canal para fornecer conteúdo. Geralmente, esses queries só precisarão ser considerados uma vez por endpoint por modelo. Para os fins deste guia de introdução, só será necessário criar um.

<!-- Not in the UI yet - will need updating when it is -->
<!--
1. Log into AEM as a Cloud Service and from the main menu select **Tools -&gt; Assets -&gt; GraphQL** 
   * Alternatively open the page directly at `https://<host>:<port>/content/graphiql.html`.
-->

1. Faça logon no AEM como um Cloud Service e acesse a interface GraphiQL:
   * Por exemplo: `https://<host>:<port>/content/graphiql.html`.

1. O GraphiQL é um editor de consultas do navegador para GraphQL. Você pode usá-lo para criar consultas para recuperar Fragmentos de conteúdo para entregá-los com facilidade como JSON.
   * O painel esquerdo permite criar o query.
   * O painel direito exibe os resultados.
   * O Editor de consultas apresenta a conclusão de código e teclas de atalho para executar facilmente a consulta.
      ![Editor GraphiQL](../assets/graphiql.png)

1. Supondo que o modelo que criamos foi chamado `person` com campos `firstName`, `lastName` e `position`, podemos criar uma consulta simples para recuperar o conteúdo do Fragmento de conteúdo.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Insira o query no painel esquerdo.
   ![Consulta GraphiQL](../assets/graphiql-query.png)

1. Clique no botão **Executar Consulta** ou use a tecla de atalho `Ctrl-Enter` e os resultados são exibidos como JSON no painel direito.
   ![Resultados GraphiQL](../assets/graphiql-results.png)

1. Clique no link **Docs** no canto superior direito da página para mostrar a documentação de contexto para ajudá-lo a criar suas consultas que se adaptam aos seus próprios modelos.
   ![Documentação GraphiQL](../assets/graphiql-documentation.png)

O GraphQL permite consultas estruturadas que podem direcionar não apenas conjuntos de dados específicos ou objetos de dados individuais, mas também fornecer elementos específicos dos objetos, resultados aninhados, oferecer suporte para variáveis de consulta e muito mais.

O GraphQL pode evitar solicitações de API iterativas, bem como entrega excessiva e, em vez disso, permite a entrega em massa do que é necessário para renderização como resposta a uma única consulta de API. O JSON resultante pode ser usado para fornecer dados a outros sites ou aplicativos.

## Próximas etapas {#next-steps}

Pronto! Agora você tem uma compreensão básica do gerenciamento de conteúdo sem periféricos no AEM. É claro que há muito mais recursos onde você pode aprofundar um entendimento abrangente dos recursos disponíveis.

* **Navegador de configuração**  - Para obter detalhes sobre o Navegador de configuração de AEM
* **[Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)**  - Para obter detalhes sobre a criação e o gerenciamento dos Fragmentos de conteúdo
* **[Suporte a fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)**  - Para obter detalhes sobre como acessar AEM conteúdo diretamente sobre a API HTTP, por meio de operações CRUD (Criar, Ler, Atualizar, Excluir)
* **[API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md)**  - Para obter detalhes sobre como fornecer fragmentos de conteúdo sem interrupções
