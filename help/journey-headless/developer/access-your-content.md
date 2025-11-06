---
title: Como acessar seu conteúdo por meio das APIs de entrega do AEM
description: Nesta parte da Jornada do desenvolvedor headless do AEM, saiba como usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo.
exl-id: 1adecc69-5f92-4007-8a2a-65bf1e960645
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 93%

---

# Como acessar seu conteúdo por meio das APIs de entrega do AEM {#access-your-content}

Nesta parte da [Jornada de desenvolvedores headless do AEM](overview.md), você pode aprender a usar consultas do GraphQL para acessar o conteúdo dos fragmentos de conteúdo e alimentá-lo no seu aplicativo (entrega headless).

## A história até agora {#story-so-far}

No documento anterior da jornada headless do AEM, [Como modelar seu conteúdo](model-your-content.md), você aprendeu as noções básicas da modelagem de conteúdo no AEM, então agora você deve entender como modelar a estrutura de conteúdo e, em seguida, colocar essa estrutura em prática usando Modelos de fragmento de conteúdo e Fragmentos de conteúdo do AEM:

* Reconhecer os conceitos e a terminologia relacionados à modelagem de conteúdo.
* Entender por que a modelagem de conteúdo é necessária para a entrega de conteúdo headless.
* Entender como colocar essa estrutura em prática usando Modelos de fragmento de conteúdo do AEM (e criar conteúdo com Fragmentos de conteúdo).
* Entender como modelar o conteúdo; princípios com amostras básicas.

Este artigo se baseia nesses fundamentos para que você entenda como acessar o conteúdo headless existente no AEM usando a API GraphQL do AEM.

* **Público-alvo**: iniciante
* **Objetivo**: aprender a acessar o conteúdo dos Fragmentos de conteúdo usando consultas GraphQL do AEM:
   * Introdução à GraphQL e a API GraphQL do AEM.
   * Aprenda os detalhes da API GraphQL do AEM.
   * Observe algumas consultas de amostra para ver como as coisas funcionam na prática.

## Então, gostaria de acessar seu conteúdo? {#so-youd-like-to-access-your-content}

Todo esse conteúdo perfeitamente estruturado (em Fragmentos de conteúdo) está disponível para alimentar seu novo aplicativo. A questão é: como fazer isso?

O que você precisa é de uma maneira de direcionar conteúdo específico, selecionar o que precisa e retorná-lo ao seu aplicativo para processamento adicional.

Com o Adobe Experience Manager (AEM) as a Cloud Service, você pode acessar seletivamente seus Fragmentos de conteúdo, usando a API GraphQL do AEM para retornar somente o conteúdo necessário. Isso significa que você pode realizar a entrega headless de conteúdo estruturado para uso em seus aplicativos.

>[!NOTE]
>
>A API GraphQL do AEM é uma implementação personalizada, com base na especificação padrão da API GraphQL.

## GraphQL: uma Introdução {#graphql-introduction}

GraphQL é uma especificação de código aberto que fornece:

* um idioma de consulta que permite selecionar conteúdo específico de objetos estruturados.
* um tempo de execução para realizar essas consultas com seu conteúdo estruturado.

O GraphQL é uma API altamente tipificada. Isso significa que *todo* o conteúdo deve ser claramente estruturado e organizado por tipo, para que a GraphQL *entenda* o que acessar e como. Os campos de dados são definidos nos esquemas GraphQL, que definem a estrutura dos objetos de conteúdo.

Os pontos de acesso da GraphQL fornecem os caminhos que respondem às consultas GraphQL.

Tudo isso significa que seu aplicativo pode selecionar com precisão, confiabilidade e eficiência o conteúdo de que precisa. Exatamente o que você precisa quando usado com o AEM.

>[!NOTE]
>
>Consulte *GraphQL*.org e *GraphQL*.com.

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## API GraphQL do AEM {#aem-graphql-api}

A API GraphQL do AEM é uma versão personalizada com base na especificação padrão da API GraphQL, especialmente configurada para permitir a execução de consultas (complexas) nos Fragmentos de conteúdo.

Fragmentos de conteúdo são usados, pois o conteúdo é estruturado de acordo com Modelos de fragmento de conteúdo. Isso atende a um requisito básico da GraphQL.

* Um Modelo de fragmento de conteúdo é composto de um ou mais campos.
   * Cada campo é definido de acordo com um Tipo de dados.
* Os Modelos de fragmento de conteúdo são usados para gerar os Esquemas GraphQL do AEM correspondentes.

Para acessar a GraphQL para o AEM (e o conteúdo), um ponto de acesso é usado para fornecer o caminho de acesso.

O conteúdo retornado, por meio da API GraphQL do AEM, pode ser usado pelos seus aplicativos.

Para ajudá-lo a inserir diretamente e testar consultas, uma implementação da interface GraphiQL padrão também está disponível para uso com a GraphQL do AEM (isso pode ser instalado com o AEM). Isso fornece recursos como realce de sintaxe, preenchimento automático e sugestão automática, juntamente com um histórico e uma documentação online.

>[!NOTE]
>
>A implementação da API GraphQL do AEM é baseada nas bibliotecas GraphQL do Java.

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEM as a Cloud Service environment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM as a Cloud Service is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## Fragmentos de conteúdo para uso com a API GraphQL do AEM {#content-fragments-use-with-aem-graphql-api}

Os fragmentos de conteúdo podem ser usados como base para esquemas e consultas GraphQL do AEM, como:

* Eles permitem que você desenvolva, crie, prepare e publique conteúdo independente de página que possa ser entregue de forma headless.
* Eles são baseados em um modelo de fragmento de conteúdo, que predefine a estrutura do fragmento resultante usando uma seleção de tipos de dados.
* É possível criar camadas adicionais de estrutura com o tipo de dados Referência de fragmento, disponível ao definir um modelo.

### Modelos de fragmentos de conteúdo {#content-fragments-models}

Esses modelos de fragmentos de conteúdo:

* São usados para gerar os esquemas, quando **habilitados**.
* Fornecem os tipos de dados e campos necessários para o GraphQL. Garantem que seu aplicativo solicite apenas o que é possível e receba o que é esperado.
* O tipo de dados **Referências de fragmento** pode ser usado no modelo para fazer referência a outro fragmento de conteúdo e, assim, introduzir níveis adicionais de estrutura.

### Referências do fragmento {#fragment-references}

**Referência de fragmento** e **UUID de referência de fragmento**:

* Os tipos de dados específicos estão disponíveis ao definir um modelo de fragmento de conteúdo.
* Faz referência a outro fragmento, dependente de um modelo de fragmento de conteúdo específico.
* Permite criar e recuperar dados estruturados.

   * Quando definido como **multifeed**, vários fragmentos secundários podem ser referenciados (recuperados) pelo fragmento principal.

## Usar de fato a API GraphQL do AEM {#actually-using-aem-graphiql}

### Configuração inicial {#initial-setup}

Antes de começar com as consultas de conteúdo, você precisa:

* Habilitar o seu ponto de acesso
   * Use Ferramentas > Geral > GraphQL
   * [Habilitar seu ponto de acesso de GraphQL](/help/headless/graphql-api/graphql-endpoint.md)
      * Isso também habilitará o GraphiQL IDE.

### Estrutura de amostra {#sample-structure}

Para usar de fato a API GraphQL do AEM em uma consulta, podemos usar duas estruturas muito básicas de modelo de fragmentos de conteúdo:

* Empresa
   * Nome - Texto
   * CEO (Pessoa) - Referência do fragmento
   * Funcionários (Pessoas) - Referência(s) do fragmento
* Pessoa
   * Nome - Texto
   * Nome - Texto

Como você pode ver, os campos CEO e Funcionários fazem referência aos fragmentos de Pessoa.

Os modelos de fragmento são usados:

* ao criar o conteúdo no editor de fragmento de conteúdo
* para gerar os esquemas GraphQL que você consultará

### Onde testar suas consultas {#where-to-test-your-queries}

As consultas podem ser inseridas na interface do GraphiQL. É possível acessar o editor de consultas por meio de:

* **Ferramentas** > **Geral** > **Editor de Consultas do GraphQL**
* diretamente; por exemplo, `http://localhost:4502/aem/graphiql.html`

![Interface GraphiQL](assets/graphiql-interface.png "Interface GraphiQL")

### Introdução às consultas {#getting-Started-with-queries}

Uma consulta bastante simples é retornar o nome de todas as entradas no esquema Empresa. Aqui você solicita uma lista de todos os nomes de empresas:

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

Uma consulta um pouco mais complexa é selecionar todas as pessoas que não têm o nome “Jobs”. Isso filtrará todas as pessoas, mantendo apenas as que não tenham o nome Jobs. Isso é feito com o operador EQUALS_NOT (há muitos outros):

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

Você também pode criar consultas mais complexas. Por exemplo: consultar todas as empresas que tenham pelo menos um funcionário com o nome de “Smith”. Esta consulta ilustra a filtragem de pessoas com o nome “Smith”, retornando informações dos fragmentos aninhados:

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

Para obter os detalhes completos sobre o uso da API GraphQL do AEM, juntamente com a configuração dos elementos necessários, consulte:

* Saiba como usar o GraphQL com o AEM
* Amostra da estrutura do fragmento de conteúdo
* Saiba como usar o GraphQL com o AEM - Exemplos de conteúdo e consultas

## O que vem a seguir {#whats-next}

Agora que já sabe acessar e consultar seu conteúdo headless usando a API GraphQL do AEM, você pode [aprender como usar a API REST para acessar e atualizar o conteúdo dos fragmentos de conteúdo](update-your-content.md).

## Recursos adicionais {#additional-resources}

* [APIs do Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [GraphQL.org](https://graphql.org)
   * [Esquema](https://graphql.org/learn/schema/)
   * [Variáveis](https://graphql.org/learn/queries/#variables)
   * [Bibliotecas Java de GraphQL](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Saiba como usar o GraphQL com o AEM](/help/headless/graphql-api/content-fragments.md)
   * [Habilitar seu ponto de acesso de GraphQL](/help/headless/graphql-api/graphql-endpoint.md)
   * [Instalar a interface GraphiQL do AEM](/help/headless/graphql-api/graphiql-ide.md)
* [Amostra da estrutura do fragmento de conteúdo](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)
* [Saiba como usar o GraphQL com o AEM - Exemplos de conteúdo e consultas](/help/headless/graphql-api/sample-queries.md)
   * [Exemplo de consulta - Um único fragmento de cidade específico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment)
   * [Exemplo de consulta para metadados - Listar os metadados para prêmios denominados GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb)
   * [Exemplo de consulta - Todas as cidades com uma variação nomeada](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation)
* [Habilitar a funcionalidade de fragmento de conteúdo no navegador de configuração](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)
* [Trabalho com fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
   * [Modelos de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
   * [Saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Entender sobre o CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=pt-BR#understand-cross-origin-resource-sharing-(cors))
* [Consultas persistentes do GraphQL - ativação do armazenamento em cache no Dispatcher](/help/headless/deployment/dispatcher-caching.md)
* [Geração de tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Introdução ao AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=pt-BR) - Uma pequena série de tutoriais em vídeo que fornece uma visão geral da utilização de recursos headless do AEM, incluindo a modelagem de conteúdo e o GraphQL.
