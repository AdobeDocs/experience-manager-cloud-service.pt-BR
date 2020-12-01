---
title: Guia de Start rápido para acessar e fornecer fragmentos de conteúdo sem cabeçalho
description: A API REST de ativos permite gerenciar fragmentos de conteúdo e a API GraphQL permite um delivery simples do conteúdo do fragmento de conteúdo.
translation-type: tm+mt
source-git-commit: 7ed96dc0da879800d731983a0399b4f4fb3d7d41
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Acesso e entrega de fragmentos de conteúdo Guia de Start rápido sem cabeçalho {#accessing-delivering-content-fragments}

A API REST de ativos permite gerenciar fragmentos de conteúdo e a API GraphQL permite um delivery simples do conteúdo do fragmento de conteúdo.

## O que são APIs REST do GraphQL e do Assets? {#what-are-the-apis}

[Agora que você criou alguns fragmentos de conteúdo, ](create-content-fragment.md) é possível usar AEM APIs para fornecê-los sem interrupções.

* [A ](/help/assets/content-fragments/graphql-api-content-fragments.md) API GraphQL permite que você crie solicitações para acessar e fornecer Fragmentos de conteúdo.
* [A ](/help/assets/content-fragments/assets-api-content-fragments.md) API REST de ativos permite criar e modificar Fragmentos de conteúdo (e outros ativos).

O restante deste guia se concentrará no acesso ao GraphQL e no delivery do fragmento do conteúdo.

## Como fornecer um fragmento de conteúdo usando o GraphQL {#how-to-deliver-a-content-fragment}

Os arquitetos de informações precisarão projetar query para seus pontos de extremidade de canal a fim de fornecer conteúdo. Esses query geralmente só precisam ser considerados uma vez por endpoint por modelo. Para os fins deste guia de introdução, só precisaremos criar um.

1. Efetue login no AEM como um Cloud Service e, no menu principal, selecione **Ferramentas -> Ativos -> GraphQL**
   * Como alternativa, abra a página diretamente em `https://<host>:<port>/content/graphiql.html`.

1. O GraphiQL é um editor de query no navegador para o GraphQL. Você pode usá-lo para criar query para recuperar os Fragmentos de conteúdo para entregá-los de forma direta como JSON.
   * O painel esquerdo permite que você crie seu query.
   * O painel direito exibe os resultados.
   * O editor de query apresenta a conclusão de código e teclas de atalho para executar facilmente o query.
      ![Editor de GraphiQL](../assets/graphiql.png)

1. Supondo que o modelo que criamos tenha sido chamado `person` com os campos `firstName`, `lastName` e `position`, podemos criar um query simples para recuperar o conteúdo de nosso Fragmento de conteúdo.

   ```
   query {
     persons {
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
   ![Query GraphiQL](../assets/graphiql-query.png)

1. Clique no botão **Executar Query** ou use a tecla de atalho `Ctrl-Enter` e os resultados serão exibidos como JSON no painel direito.
   ![Resultados do GraphiQL](../assets/graphiql-results.png)

1. Clique no link **Documentos** no canto superior direito da página para mostrar a documentação em contexto para ajudá-lo a criar seus query que se adaptam aos seus próprios modelos.
   ![Documentação do GraphiQL](../assets/graphiql-documentation.png)

O GraphQL permite query estruturados que podem público alvo não apenas conjuntos de dados específicos ou objetos de dados individuais, mas também fornecer elementos específicos dos objetos, resultados aninhados, suporte do oferta para variáveis de query e muito mais.

O GraphQL pode evitar solicitações iterativas de API, bem como delivery excessivo, e em vez disso permite o delivery em massa do que é necessário para renderizar como resposta a um único query de API. O JSON resultante pode ser usado para fornecer dados para outros sites ou aplicativos.

## Próximas etapas {#next-steps}

É isso! Agora você tem uma compreensão básica da gestão de conteúdo sem cabeça em AEM. É claro que há muito mais recursos onde você pode mergulhar mais fundo para obter uma compreensão abrangente dos recursos disponíveis.

* **Navegador**  de configuração - Para obter detalhes sobre o Navegador de configuração AEM
* **[Fragmentos](/help/assets/content-fragments/content-fragments.md)**  de conteúdo - Para obter detalhes sobre como criar e gerenciar fragmentos de conteúdo
* **[Suporte a fragmentos de conteúdo na API](/help/assets/content-fragments/assets-api-content-fragments.md)**  HTTP AEM Assets - para obter detalhes sobre como acessar AEM conteúdo diretamente pela API HTTP, por meio de operações CRUD (Criar, Ler, Atualizar, Excluir)
* **[API](/help/assets/content-fragments/graphql-api-content-fragments.md)**  GraphQL - Para obter detalhes sobre como fornecer fragmentos de conteúdo sem interrupções
