---
title: Como acessar seu conteúdo por meio AEM APIs de entrega
description: Nesta parte da Jornada do desenvolvedor sem cabeçalho do AEM, saiba como usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo.
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 0c47dec1e96fc3137d17fc3033f05bf1ae278141
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 1%

---

# Como acessar seu conteúdo por meio AEM APIs de entrega {#access-your-content}

>[!CAUTION]
>
>TRABALHO EM ANDAMENTO - A criação deste documento está em curso e não deve ser entendida como completa ou definitiva, nem deve ser usada para fins de produção.

Nesta parte da [AEM Jornada do desenvolvedor sem cabeçalho,](overview.md) você pode aprender a usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo e alimentá-lo em seu aplicativo (entrega sem cabeçalho).

## A história até agora {#story-so-far}

No documento anterior da jornada sem cabeçalho de AEM, [Como modelar seu conteúdo](model-your-content.md) você aprendeu as noções básicas da modelagem de conteúdo no AEM, portanto, agora você deve entender como modelar sua estrutura de conteúdo e perceber essa estrutura usando AEM Modelos de fragmento de conteúdo e Fragmentos de conteúdo:

* Reconhecer os conceitos e a terminologia relacionados à modelagem de conteúdo.
* Entenda por que a modelagem de conteúdo é necessária para a entrega de conteúdo sem interface.
* Entenda como realizar essa estrutura usando AEM Modelos de fragmento de conteúdo (e criar conteúdo com Fragmentos de conteúdo).
* Entenda como modelar o conteúdo; princípios com amostras básicas.

Este artigo se baseia nesses fundamentos para que você entenda como acessar o conteúdo headless existente no AEM usando a API GraphQL AEM.

* **Público-alvo**: Iniciante
* **Objetivo**: Saiba como acessar o conteúdo dos Fragmentos de conteúdo usando AEM consultas GraphQL:
   * Apresente GraphQL e a API GraphQL AEM.
   * Saiba mais sobre os detalhes da API GraphQL da AEM.
   * Observe algumas consultas de amostra para ver como as coisas funcionam na prática.

## Então, gostaria de acessar seu conteúdo? {#so-youd-like-to-access-your-content}

Então...você tem todo esse conteúdo, perfeitamente estruturado (em Fragmentos de conteúdo) e apenas esperando para alimentar seu novo aplicativo. A questão é: como chegar lá?

O que você precisa é de uma maneira de direcionar conteúdo específico, selecionar o que precisa e retorná-lo ao seu aplicativo para processamento adicional.

Com o Adobe Experience Manager (AEM) as a Cloud Service, é possível acessar seletivamente os Fragmentos de conteúdo, usando a API GraphQL AEM, para retornar somente o conteúdo necessário. Isso significa que você pode realizar a entrega sem interface de conteúdo estruturado para uso em seus aplicativos.

>[!NOTE]
>
>AEM API GraphQL é uma implementação personalizada, com base na especificação da API GraphQL padrão.

## GraphQL - Uma Introdução {#graphql-introduction}

GraphQL é uma especificação de código aberto que fornece:

* um idioma de consulta que permite selecionar conteúdo específico de objetos estruturados.
* um tempo de execução para realizar essas consultas com seu conteúdo estruturado.

GraphQL é uma API do tipo *strong*. Isso significa que o conteúdo *all* deve ser claramente estruturado e organizado por tipo, para que GraphQL *entenda* o que acessar e como. Os campos de dados são definidos em esquemas GraphQL, que definem a estrutura dos objetos de conteúdo.

Os pontos de extremidade GraphQL fornecem os caminhos que respondem às consultas GraphQL.

Tudo isso significa que seu aplicativo pode selecionar com precisão, confiabilidade e eficiência o conteúdo de que precisa - exatamente o que você precisa quando usado com o AEM.

>[!NOTE]
>
>Consulte *GraphQL*.org e *GraphQL*.com.

## AEM e GraphQL {#aem-graphql}

GraphQL é usado em vários locais no AEM; por exemplo:

* Fragmentos de conteúdo
   * Uma API personalizada foi desenvolvida para este caso de uso (Entrega sem cabeçalho ao seu aplicativo).
      * Esta é a API GraphQL AEM.
* Commerce
   * O AEM Commerce consome dados de uma plataforma do Commerce via GraphQL.
   * Há integrações GraphQL entre o AEM e várias soluções comerciais de terceiros, usadas com os ganchos de extensão fornecidos pelos Componentes principais da CIF.
      * Isso não usa a API GraphQL AEM.

>[!NOTE]
>
>Essa etapa da Jornada sem cabeçalho só se refere à API GraphQL AEM e aos Fragmentos de conteúdo.

## AEM API GraphQL {#aem-graphql-api}

A API GraphQL da AEM é uma versão personalizada baseada na especificação GraphQL da API padrão, especialmente configurada para permitir a execução de consultas (complexas) nos Fragmentos de conteúdo.

Fragmentos de conteúdo são usados, pois o conteúdo é estruturado de acordo com Modelos de fragmento de conteúdo. Isso atende a um requisito básico do GraphQL.

* Um Modelo de fragmento de conteúdo é composto de um ou mais campos.
   * Cada campo é definido de acordo com um Tipo de dados.
* Os Modelos de Fragmento de conteúdo são usados para gerar os Esquemas GraphQL AEM correspondentes.

Para realmente acessar GraphQL para AEM (e o conteúdo), um ponto de extremidade é usado para fornecer o caminho de acesso.

O conteúdo retornado, por meio da API GraphQL da AEM, pode ser usado pelos seus aplicativos.

>[!NOTE]
>
>A implementação AEM da API GraphQL é baseada nas bibliotecas GraphQL Java.

### Casos de uso para ambientes de autor e publicação {#use-cases-author-publish-environments}

Os casos de uso da API GraphQL da AEM podem depender do tipo de AEM como um ambiente de Cloud Service:

* Ambiente de publicação; usado para:
   * Conteúdo da consulta para o aplicativo JS (caso de uso padrão)

* Ambiente de criação; usado para:
   * Consultar conteúdo para &quot;fins de gerenciamento de conteúdo&quot;:
      * No momento, a GraphQL no AEM as a Cloud Service é uma API somente leitura.
      * A REST API pode ser usada para operações de CR(u)D.

## Fragmentos de conteúdo para uso com a API GraphQL AEM {#content-fragments-use-with-aem-graphql-api}

Os Fragmentos de conteúdo podem ser usados como base para GraphQL para AEM schemas e consultas como:

* Eles permitem projetar, criar, preparar e publicar conteúdo independente da página.
* Elas são baseadas em um Modelo de fragmento de conteúdo, que predefine a estrutura do fragmento resultante por meio de tipos de dados definidos.
* É possível obter camadas adicionais de estrutura com o tipo de dados Referência de fragmento , disponível ao definir um modelo.

### Modelos de fragmentos do conteúdo {#content-fragments-models}

Esses modelos de fragmentos de conteúdo:

* São usados para gerar os Esquemas, uma vez **Enabled**.

* Forneça os tipos de dados e campos necessários para GraphQL. Eles garantem que seu aplicativo solicite apenas o que é possível e receba o que é esperado.

* O tipo de dados **Referências de fragmento** pode ser usado em seu modelo para fazer referência a outro Fragmento de conteúdo e, portanto, introduzir níveis adicionais de estrutura.

### Referências do fragmento {#fragment-references}

A **Referência do fragmento**:

* É um tipo de dados específico disponível ao definir um Modelo de fragmento de conteúdo.

* Faz referência a outro fragmento, dependendo de um modelo de fragmento de conteúdo específico.

* Permite criar e recuperar dados estruturados.

   * Quando definido como **multifeed**, vários subfragmentos podem ser referenciados (recuperados) pelo fragmento principal.

### Visualização JSON {#json-preview}

Para ajudar na criação e desenvolvimento dos Modelos de fragmento de conteúdo, é possível visualizar a saída JSON no Editor de fragmento de conteúdo.

### Criação de modelos de fragmentos de conteúdo e fragmentos de conteúdo {#creating-content-fragment-models-and-content-fragments}

Os primeiros Modelos de fragmento de conteúdo são ativados para o seu site, isso é feito no Navegador de configuração:

![Definir configuração](assets/cfm-configuration.png)

Em seguida, os Modelos de fragmentos de conteúdo podem ser modelados:

![Modelo de fragmentos de conteúdo](assets/cfm-model.png)

Após selecionar o modelo apropriado, um Fragmento de conteúdo é aberto para edição no Editor de fragmento de conteúdo:

![Editor de conteúdo do fragmento](assets/cfm-editor.png)

>[!NOTE]
>
>Consulte Trabalhar com fragmentos de conteúdo .

## Geração de esquema GraphQL a partir dos fragmentos de conteúdo {#graphql-schema-generation-content-fragments}

GraphQL é uma API altamente digitada, o que significa que o conteúdo deve ser claramente estruturado e organizado por tipo. A especificação GraphQL fornece uma série de diretrizes sobre como criar uma API robusta para interrogar conteúdo em uma determinada instância. Para fazer isso, um cliente precisa buscar o Esquema, que contém todos os tipos necessários para uma consulta.

Para Fragmentos de conteúdo, os esquemas GraphQL (estrutura e tipos) são baseados em **Modelos de fragmento de conteúdo ativados** e seus tipos de dados.

>[!CAUTION]
>
>Todos os esquemas GraphQL (derivados dos Modelos de fragmento de conteúdo que foram **Enabled**) podem ser lidos pelo ponto de extremidade GraphQL.
>
>Isso significa que é necessário garantir que nenhum conteúdo confidencial esteja disponível para garantir que nenhum dado sensível seja exposto por meio de pontos de extremidade GraphQL; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

Por exemplo, se um usuário criou um Modelo de fragmento de conteúdo chamado `Article`, AEM gera o objeto `article` que é do tipo `ArticleModel`. Os campos desse tipo correspondem aos campos e tipos de dados definidos no modelo.

1. Um modelo de fragmento de conteúdo:

   ![Modelo de fragmento de conteúdo para uso com o ](assets/graphqlapi-cfmodel.png "GraphQLContent Fragment Model para uso com GraphQL")

1. O esquema GraphQL correspondente (saída da documentação automática GraphiQL):
   ![Esquema GraphQL com base no ](assets/graphqlapi-cfm-schema.png "modelo de fragmento de conteúdoGraphQL com base no modelo de fragmento de conteúdo")

   Isso mostra que o tipo gerado `ArticleModel` contém vários [campos](#fields).

   * Três delas foram controladas pelo usuário: `author`, `main` e `referencearticle`.

   * Os outros campos foram adicionados automaticamente por AEM e representam métodos úteis para fornecer informações sobre um determinado Fragmento de conteúdo; neste exemplo, `_path`, `_metadata`, `_variations`. Esses [campos auxiliares](#helper-fields) são marcados com um `_` anterior para distinguir entre o que foi definido pelo usuário e o que foi gerado automaticamente.

1. Depois que um usuário cria um Fragmento de conteúdo com base no modelo de Artigo, ele pode ser interrogado por meio de GraphQL. Para obter exemplos, consulte a Amostra de consultas.md#grafql-sample-queries) (com base em uma amostra da estrutura do Fragmento de conteúdo para ser usada com GraphQL.

No GraphQL para AEM, o esquema é flexível. Isso significa que ele é gerado automaticamente cada vez que um Modelo de fragmento de conteúdo é criado, atualizado ou excluído. Os caches de esquema de dados também são atualizados quando você atualiza um Modelo de fragmento de conteúdo.

O serviço GraphQL do Sites escuta (em segundo plano) quaisquer modificações feitas em um Modelo de fragmento de conteúdo. Quando as atualizações são detectadas, somente essa parte do esquema é regenerada. Essa otimização economiza tempo e oferece estabilidade.

Por exemplo, se você:

1. Instale um pacote contendo `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Os tipos GraphQL para `Model-1` e `Model-2` serão gerados.

1. Em seguida, modifique `Content-Fragment-Model-2`:

   1. Somente o tipo GraphQL `Model-2` será atualizado.

   1. Enquanto `Model-1` permanecerá o mesmo.

>[!NOTE]
>
>Isso é importante observar caso queira fazer atualizações em massa nos Modelos de fragmento de conteúdo por meio da api REST ou de outra forma.

O esquema é distribuído por meio do mesmo terminal que as consultas GraphQL, com o cliente lidando com o fato de que o esquema é chamado com a extensão `GQLschema`. Por exemplo, executar uma solicitação `GET` simples em `/content/cq:graphql/global/endpoint.GQLschema` resultará na saída do schema com o Tipo de conteúdo: `text/x-graphql-schema;charset=iso-8859-1`.

### Geração de esquema - Modelos não publicados {#schema-generation-unpublished-models}

Quando os Fragmentos de conteúdo são aninhados, pode acontecer que um Modelo de fragmento de conteúdo principal seja publicado, mas um modelo referenciado não é.

>[!NOTE]
>
>A interface do usuário do AEM impede que isso aconteça, mas se a publicação for feita de forma programática ou com pacotes de conteúdo, ela poderá ocorrer.

Quando isso acontece, o AEM gera um esquema *incompleto* para o modelo de fragmento de conteúdo pai. Isso significa que a Referência do fragmento, que depende do modelo não publicado, é removida do esquema.

## Pontos finais GraphQL AEM {#aem-graphql-endpoints}

<!--
need details/examples
-->

Um endpoint é o caminho usado para acessar GraphQL para AEM. Usando esse caminho você (ou seu aplicativo) pode:

* acessar os esquemas GraphQL,
* enviar suas consultas GraphQL,
* receba as respostas (para suas consultas GraphQL).

AEM permite:

* Um endpoint global - disponível para uso por todos os sites.
* Endpoints do locatário - que você pode configurar, específicos de um site/projeto especificado.

## Permissões  {#permissions}

As permissões são as necessárias para acessar o Assets.

## A interface GraphiQL AEM {#aem-graphiql-interface}

Para ajudá-lo a inserir diretamente e testar consultas, uma implementação da interface GraphiQL padrão está disponível para uso com AEM GraphQL. Isso pode ser instalado com AEM.

Ele fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática, juntamente com um histórico e documentação online.

![Interface GraphiQL ](assets/graphiql-interface.png "InterfaceInterface GraphiQL")

## Na verdade, usando a API GraphQL AEM {#actually-using-aem-graphiql}

Para realmente usar a API GraphQL AEM em uma consulta, podemos usar as duas estruturas muito básicas do Modelo de fragmento de conteúdo:

* Empresa
   * Nome
   * CEO (Pessoa)
   * Empregados (Pessoas)
* Person
   * Nome
   * Nome

Como é possível ver, os campos CEO e Employees fazem referência aos fragmentos Pessoa.

Os modelos de fragmento serão usados:

* ao criar o conteúdo no Editor de fragmento de conteúdo
* para gerar os esquemas GraphQL que você consultará

As consultas podem ser inseridas na interface GraphiQL, por exemplo, em:

* `http://localhost:4502/content/graphiql.html `

Uma consulta simples é retornar o nome de todas as entradas no schema Empresa. Aqui você solicita uma lista de todos os nomes de empresas:

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

Uma consulta um pouco mais complexa é selecionar todas as pessoas que não têm o nome de &quot;Trabalhos&quot;. Isso filtrará todas as pessoas para qualquer pessoa que não tenha o nome Trabalhos. Isso é feito com o operador EQUALS_NOT (há muito mais):

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

Você também pode criar consultas mais complexas. Por exemplo, consulte todas as empresas que tenham pelo menos um funcionário com o nome de &quot;Smith&quot;. Esta consulta ilustra a filtragem de qualquer pessoa com o nome &quot;Smith&quot;, retornando informações de todos os fragmentos aninhados:

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

<!-- need code / curl / cli examples-->

Para obter todos os detalhes sobre o uso da API GraphQL da AEM, juntamente com a configuração dos elementos necessários, é possível fazer referência a:

* Aprendendo a usar GraphQL com AEM
* A estrutura do fragmento de conteúdo de amostra
* Saiba como usar GraphQL com AEM - Conteúdo de amostra e consultas

## O que vem a seguir {#whats-next}

Agora que você aprendeu a acessar e consultar o conteúdo sem periféricos usando a API GraphQL AEM, agora é possível [aprender a usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo](/help/implementing/developing/headless-journey/update-your-content.md).

## Recursos adicionais {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Esquema](https://graphql.org/learn/schema/)
   * [Variáveis](https://graphql.org/learn/queries/#variables)
   * [Bibliotecas GraphQL Java](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Aprendendo a usar GraphQL com AEM](/help/assets/content-fragments/graphql-api-content-fragments.md)
* [A estrutura do fragmento de conteúdo de amostra](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Saiba como usar GraphQL com AEM - Conteúdo de amostra e consultas](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Exemplo de consulta - Um único fragmento de cidade específico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [Exemplo de consulta para metadados - Lista os metadados para prêmios denominados GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [Consulta de exemplo - Todas as cidades com uma variável nomeada](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
   * [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
   * [Saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Entenda o CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [Gerar tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Introdução ao AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  - Uma pequena série de tutoriais em vídeo que fornece uma visão geral do uso de AEM recursos headless, incluindo modelagem de conteúdo e GraphQL.
