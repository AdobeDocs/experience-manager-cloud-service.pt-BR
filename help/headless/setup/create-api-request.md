---
title: Criar uma solicitação de API - Configuração sem cabeçalho
description: Saiba como usar a API GraphQL para a entrega sem interface do conteúdo do Fragmento de conteúdo e a API REST do Assets AEM para gerenciar Fragmentos de conteúdo.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: e81b852dc90e3cc5abc8b9f218f48d0fc1cc66eb
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---

# Criar uma solicitação de API - Configuração sem cabeçalho {#accessing-delivering-content-fragments}

Saiba como usar a API GraphQL para a entrega sem interface do conteúdo do Fragmento de conteúdo e a API REST do Assets AEM para gerenciar Fragmentos de conteúdo.

## O que são APIs REST de GraphQL e Assets? {#what-are-the-apis}

[Agora que você criou alguns fragmentos de conteúdo,](create-content-fragment.md) você pode usar AEM APIs para entregá-las sem periféricos.

* [A API GraphQL](/help/headless/graphql-api/content-fragments.md) O permite criar solicitações para acessar e fornecer Fragmentos de conteúdo. Essa API oferece o conjunto mais robusto de recursos para consultar e consumir o conteúdo do Fragmento de conteúdo.
   * Para usar isso, [os endpoints precisam ser definidos e ativados no AEM](/help/headless/graphql-api/graphql-endpoint.md)e, se necessário, a variável [Interface GraphiQL instalada](/help/headless/graphql-api/graphiql-ide.md).
* [A API REST do Assets](/help/assets/content-fragments/assets-api-content-fragments.md) O permite criar e modificar Fragmentos de conteúdo (e outros ativos).

O restante deste guia terá como foco o acesso GraphQL e a entrega do Fragmento de conteúdo.

## Habilitar Ponto de Extremidade GraphQL

Para que as APIs GraphQL possam ser usadas, é necessário criar um ponto de extremidade GraphQL.

1. Navegar para **Ferramentas**, **Ativos**, em seguida selecione **GraphQL**.
1. Selecione **Criar**.
1. O **Criar novo ponto de extremidade GraphQL** será aberta. Aqui você pode especificar:
   * **Nome**: nome do ponto final; você pode inserir qualquer texto.
   * **Use o esquema GraphQL fornecido por**: use a lista suspensa para selecionar a configuração necessária.
1. Confirme com **Criar**.
1. No console, uma **Caminho** será exibida com base na configuração criada anteriormente. Esse é o caminho usado para executar consultas GraphQL.

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

Mais detalhes sobre como ativar [Os pontos de extremidade GraphQL podem ser encontrados aqui](/help/headless/graphql-api/graphql-endpoint.md).

## Consultar conteúdo usando GraphQL com GraphiQL

Os arquitetos de informações precisarão projetar consultas para seus pontos de extremidade de canal para fornecer conteúdo. Geralmente, esses queries só precisarão ser considerados uma vez por endpoint por modelo. Para os fins deste guia de introdução, só será necessário criar um.

O GraphiQL é um IDE que pode ser instalado em um ambiente AEM. Siga as etapas em [Uso do GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) para instalar no ambiente de AEM.

1. Faça logon AEM as a Cloud Service e acesse a interface GraphiQL:
   * Por exemplo: `https://<host>:<port>/content/graphiql.html`.

1. O GraphiQL IDE é um editor de consultas do navegador para GraphQL. Você pode usá-lo para criar consultas para recuperar Fragmentos de conteúdo para entregá-los com facilidade como JSON.
   * O painel esquerdo permite criar o query.
   * O painel direito exibe os resultados.
   * O Editor de consultas apresenta a conclusão de código e teclas de atalho para executar facilmente a consulta.
      ![Editor GraphiQL](../assets/graphiql.png)

1. Supondo que o modelo que criamos era chamado `person` com campos `firstName`, `lastName`e `position`, podemos criar uma consulta simples para recuperar o conteúdo do Fragmento de conteúdo.

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

1. Clique no botão **Executar Consulta** ou use o `Ctrl-Enter` A tecla de atalho e os resultados são exibidos como JSON no painel direito.
   ![Resultados GraphiQL](../assets/graphiql-results.png)

1. Clique no botão **Documentação** link na parte superior direita da página para mostrar a documentação contextual para ajudá-lo a criar suas consultas que se adaptam aos seus próprios modelos.
   ![Documentação GraphiQL](../assets/graphiql-documentation.png)

O GraphQL permite consultas estruturadas que podem direcionar não apenas conjuntos de dados específicos ou objetos de dados individuais, mas também fornecer elementos específicos dos objetos, resultados aninhados, oferecer suporte para variáveis de consulta e muito mais.

O GraphQL pode evitar solicitações de API iterativas, bem como entrega excessiva e, em vez disso, permite a entrega em massa do que é necessário para renderização como resposta a uma única consulta de API. O JSON resultante pode ser usado para fornecer dados a outros sites ou aplicativos.

## Próximas etapas {#next-steps}

Pronto! Agora você tem uma compreensão básica do gerenciamento de conteúdo sem periféricos no AEM. É claro que há muito mais recursos onde você pode aprofundar um entendimento abrangente dos recursos disponíveis.

* **[Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)** - Para obter detalhes sobre a criação e o gerenciamento dos Fragmentos de conteúdo
* **[Suporte a fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)** - Para obter detalhes sobre como acessar AEM conteúdo diretamente pela API HTTP, por meio de operações CRUD (Criar, Ler, Atualizar, Excluir)
* **[API GraphQL](/help/headless/graphql-api/content-fragments.md)** - Para obter detalhes sobre como fornecer fragmentos de conteúdo sem interrupções
