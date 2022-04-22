---
title: Criar uma solicitação de API - Configuração Headless
description: Saiba como usar a API GraphQL para a entrega headless do conteúdo do Fragmento de conteúdo e a API REST do AEM Assets para gerenciar Fragmentos de conteúdo.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: d3c926216486c2971e498c2ea8a47f9c96935554
workflow-type: ht
source-wordcount: '670'
ht-degree: 100%

---

# Criar uma solicitação de API - Configuração Headless {#accessing-delivering-content-fragments}

Saiba como usar a API GraphQL para a entrega headless do conteúdo do Fragmento de conteúdo e a API REST do AEM Assets para gerenciar Fragmentos de conteúdo.

## O que são as APIs REST do GraphQL e do Assets? {#what-are-the-apis}

[Agora que criou alguns fragmentos de conteúdo,](create-content-fragment.md) você pode usar as APIs do AEM para entregá-los de forma headless.

* [A API GraphQL](/help/headless/graphql-api/content-fragments.md) permite criar solicitações para acessar e fornecer Fragmentos de conteúdo. Essa API oferece o conjunto mais robusto de recursos para consultar e consumir conteúdo de Fragmento de conteúdo.
   * Para usar isso, [os endpoints precisam ser definidos e ativados no AEM](/help/headless/graphql-api/graphql-endpoint.md) e, se necessário, a [Interface GraphiQL precisa ser instalada](/help/headless/graphql-api/graphiql-ide.md).
* [A API REST do Assets](/help/assets/content-fragments/assets-api-content-fragments.md) permite criar e modificar Fragmentos de conteúdo (e outros ativos).

O restante deste guia terá como foco o acesso ao GraphQL e a entrega de Fragmento de conteúdo.

## Habilitar endpoint GraphQL

Para que as APIs GraphQL possam ser usadas, é necessário criar um endpoint GraphQL.

1. Navegue até **Ferramentas**, **Ativos** e, em seguida, selecione **GraphQL**.
1. Selecione **Criar**.
1. A caixa de diálogo **Criar novo endpoint de GraphQL** será aberta. Aqui, é possível especificar:
   * **Nome**: nome do endpoint; é possível inserir qualquer texto.
   * **Usar esquema GraphQL fornecido por**: use a lista suspensa para selecionar a configuração necessária.
1. Confirme com **Criar**.
1. No console, um **Caminho** será exibido com base na configuração criada anteriormente. Esse é o caminho usado para executar consultas GraphQL.

   ```
   /content/cq:graphql/<configuration-name>/endpoint
   ```

Mais detalhes sobre como ativar [endpoints GraphQL podem ser encontrados aqui](/help/headless/graphql-api/graphql-endpoint.md).

## Consultar conteúdo usando GraphQL com o GraphiQL

Os arquitetos da informação precisarão projetar consultas para seus endpoints de canal para fornecer conteúdo. Geralmente, essas consultas só precisarão ser consideradas uma vez por endpoint por modelo. Para os fins deste guia de introdução, só será necessário criar uma.

O GraphiQL é um IDE que pode ser instalado em um ambiente AEM. Siga as etapas em [Uso do GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) para instalar no seu ambiente AEM.

1. Faça logon no AEM as a Cloud Service e acesse a interface GraphiQL:
   * Por exemplo: `https://<host>:<port>/aem/graphiql.html`.

1. O GraphiQL IDE é um editor de consultas no navegador para GraphQL. Você pode usá-lo para criar consultas para recuperar fragmentos de conteúdo e entregá-los como JSON sem periféricos.
   * A lista suspensa no canto superior direito permite selecionar o endpoint.
   * Um painel à esquerda lista as consultas persistentes (quando disponíveis)
   * O painel central esquerdo permite criar a consulta.
   * O painel central direito exibe os resultados.
   * O Editor de consultas tem recursos de autocompletar código e teclas de atalho para executar a consulta com facilidade.

   ![Editor do GraphiQL](../assets/graphiql.png)

1. Supondo que o modelo que criamos era chamado `person`, com os campos `firstName`, `lastName` e `position`, podemos criar uma consulta simples para recuperar o conteúdo do Fragmento de conteúdo.

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

1. Insira a consulta no painel esquerdo.
   ![Consulta do GraphiQL](../assets/graphiql-query.png)

1. Clique no botão **Executar Consulta** ou use a tecla de atalho `Ctrl-Enter` e os resultados serão exibidos como JSON no painel direito.
   ![Resultados do GraphiQL](../assets/graphiql-results.png)

1. Clique no link **Documentação** na parte superior direita da página para mostrar a documentação contextual para ajudá-lo a criar suas consultas que se adaptam aos seus próprios modelos.
   ![Documentação do GraphiQL](../assets/graphiql-documentation.png)

O GraphQL permite consultas estruturadas que podem direcionar não apenas conjuntos de dados específicos ou objetos de dados individuais, mas também fornecer elementos específicos dos objetos, resultados aninhados, oferecer suporte para variáveis de consulta e muito mais.

O GraphQL pode evitar solicitações de API iterativas, bem como a entrega excessiva e, em vez disso, permite a entrega em massa do que é necessário para renderização como resposta a uma única consulta de API. O JSON resultante pode ser usado para fornecer dados a outros sites ou aplicativos.

## Próximas etapas {#next-steps}

Pronto! Agora você tem uma compreensão básica do gerenciamento de conteúdo headless no AEM. É claro que há muito mais recursos onde você pode se aprofundar para obter um entendimento abrangente dos recursos disponíveis.

* **[Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)** - Para obter detalhes sobre a criação e o gerenciamento dos Fragmentos de conteúdo
* **[Suporte a fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)** - Para obter detalhes sobre como acessar conteúdo do AEM diretamente pela API HTTP, por meio de operações CRUD (Criar, Ler, Atualizar, Excluir)
* **[API GraphQL](/help/headless/graphql-api/content-fragments.md)** - Para obter detalhes sobre como fornecer Fragmentos de conteúdo de forma headless
