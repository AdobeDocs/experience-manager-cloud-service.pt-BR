---
title: Como acessar seu conteúdo por meio AEM APIs de entrega
description: Nesta parte da Jornada do desenvolvedor sem cabeçalho do AEM, saiba como usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo.
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 6097cb8961f604ec2d3f5f6d602c927efc7344d5
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---


# Como acessar seu conteúdo por meio AEM APIs de entrega {#access-your-content}

>[!CAUTION]
>
>TRABALHO EM ANDAMENTO - A criação deste documento está em curso e não deve ser entendida como completa ou definitiva, nem deve ser usada para fins de produção.

Nesta parte da [AEM Jornada de desenvolvedores headless,](#overview.md) saiba como usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo.

## A história até agora {#story-so-far}

No documento anterior da jornada sem cabeçalho AEM, [Como modelar seu conteúdo](model-your-content.md) você aprendeu as noções básicas da modelagem de dados no AEM e agora deve:

* Entenda considerações importantes sobre o planejamento para criar seu conteúdo.
* Entenda as etapas para implementar sem periféricos dependendo dos requisitos de nível de integração.
* Configure as ferramentas e as configurações de AEM necessárias.
* Conheça as práticas recomendadas para tornar sua jornada sem interface suave, manter a geração de conteúdo eficiente e garantir que o conteúdo seja entregue rapidamente.

Este artigo se baseia nesses fundamentos para que você entenda como acessar o conteúdo headless existente no AEM via API.

* **Público-alvo**: Iniciante
* **Objetivo**: Saiba como acessar o conteúdo dos Fragmentos de conteúdo usando AEM consultas GraphQL:
   * Introduza GraphQL.
   * Introduza AEM API GraphQL.
   * Saiba mais sobre os detalhes da API GraphQL da AEM.
   * Observe algumas consultas de amostra para ver como as coisas funcionam na prática.

Com o Adobe Experience Manager (AEM) as a Cloud Service, é possível usar os Fragmentos de conteúdo, juntamente com a API GraphQL AEM, para fornecer conteúdo estruturado de maneira headless para uso em seus aplicativos. A capacidade de personalizar uma única consulta de API permite recuperar e entregar o conteúdo específico que você deseja/precisa renderizar (como resposta à única consulta de API).

>[!NOTE]
>AEM API GraphQL é uma implementação personalizada, com base no GraphQL padrão.

## GraphQL - Uma Introdução {#graphql-introduction}

GraphQL é:

* &quot;*...um idioma de consulta para APIs e um tempo de execução para realizar essas consultas com seus dados existentes.*&quot;.

   Consulte *GraphQL*.

### GraphQL - Tipos {#graphql-types}

### GraphQL - Esquemas {#graphql-schemas}

### GraphQL - Consultas {#graphql-queries}

## AEM e GraphQL {#aem-graphql}

GraphQL é usado em vários locais no AEM:

* Commerce
   * Espaço reservado
* Fragmentos de conteúdo
   * Uma API personalizada foi desenvolvida para este caso de uso.
   * Esta é a API GraphQL AEM.

## AEM API GraphQL {#aem-graphql-api}

Para o Adobe Experience as a Cloud Experience, uma implementação personalizada da API GraphQL padrão foi desenvolvida.

A API GraphQL da AEM permite executar consultas (complexas) nos Fragmentos de conteúdo; com cada query de acordo com um tipo de modelo específico. O conteúdo retornado pode ser usado pelos seus aplicativos.

>[!NOTE]
>
>A implementação AEM da API GraphQL é baseada nas bibliotecas GraphQL Java.

### AEM API GraphQL e Fragmentos de conteúdo {#aem-graphql-content-fragments}

## Fragmentos de conteúdo para uso com a API GraphQL AEM {#content-fragments-use-with-aem-graphql-api}

Os Fragmentos de conteúdo podem ser usados como base para GraphQL para consultas de AEM como:

* Eles permitem projetar, criar, preparar e publicar conteúdo independente da página.
* Os Modelos de fragmento de conteúdo fornecem a estrutura necessária por meio de tipos de dados definidos.
* A Referência do fragmento, disponível ao definir um modelo, pode ser usada para definir camadas adicionais de estrutura.

### Fragmentos de conteúdo {#content-fragments}

Fragmentos de conteúdo:

* Contém conteúdo estruturado.

* Elas são baseadas em um Modelo de fragmento de conteúdo, que predefine a estrutura do fragmento resultante.

### Modelos de fragmentos do conteúdo {#content-fragments-models}

Esses modelos de fragmentos de conteúdo:

* São usados para gerar os Esquemas, uma vez **Enabled**.

* Forneça os tipos de dados e campos necessários para GraphQL. Eles garantem que seu aplicativo solicite apenas o que é possível e receba o que é esperado.

* O tipo de dados **Referências de fragmento** pode ser usado em seu modelo para fazer referência a outro Fragmento de conteúdo e, portanto, introduzir níveis adicionais de estrutura.

### Referências do fragmento {#fragment-references}

A **Referência do fragmento**:

* É de especial interesse em conjunto com GraphQL.

* É um tipo de dados específico que pode ser usado ao definir um Modelo de fragmento de conteúdo.

* Faz referência a outro fragmento, dependendo de um modelo de fragmento de conteúdo específico.

* Permite recuperar dados estruturados.

   * Quando definido como **multifeed**, vários subfragmentos podem ser referenciados (recuperados) pelo fragmento principal.

### Visualização JSON {#json-preview}

Para ajudar na criação e desenvolvimento dos Modelos de fragmento de conteúdo, você pode visualizar [saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## O que vem a seguir {#whats-next}

[Saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos](/help/implementing/developing/headless-journey/update-your-content.md) de conteúdo.

## Recursos adicionais {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Esquema](https://graphql.org/learn/schema/)
   * [Bibliotecas GraphQL Java](https://graphql.org/code/#java)
* [AEM API GraphQL para uso com Fragmentos de conteúdo](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * [Saiba como usar GraphQL com AEM - Conteúdo de amostra e consultas](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Autenticação para consultas GraphQL de AEM Remotas em Fragmentos de Conteúdo](/help/assets/content-fragments/graphql-authentication-content-fragments.md)
* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
   * [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
   * [Saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
