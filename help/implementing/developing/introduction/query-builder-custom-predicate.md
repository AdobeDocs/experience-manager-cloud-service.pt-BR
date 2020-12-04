---
title: Implementação de um Avaliador de Predicado Personalizado para o Construtor de Query
description: O Construtor de Query no AEM oferta é uma maneira fácil e personalizável de query do repositório de conteúdo
translation-type: tm+mt
source-git-commit: 21a0e6967a17ea30435d0343c4aa497f54134cda
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---


# Implementação de um Avaliador Predicado Personalizado para o Construtor de Query {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

Este documento descreve como estender o [Construtor de Query](query-builder-api.md) implementando um avaliador de predicado personalizado.

## Visão geral {#overview}

O [Construtor de Query](query-builder-api.md) oferta uma maneira fácil de query do repositório de conteúdo. AEM vem com [um conjunto de avaliadores predicados](#query-builder-predicates.md) que ajudam a query de seus dados.

No entanto, você pode querer simplificar seus query implementando um avaliador de predicado personalizado que oculta alguma complexidade e garante uma melhor semântica.

Um predicado personalizado também pode executar outras coisas que não são diretamente possíveis com o XPath, por exemplo:

* Consultar dados de outro serviço
* Filtragem personalizada com base em um cálculo

>[!NOTE]
>
>Problemas de desempenho devem ser considerados ao implementar um predicado personalizado.

>[!TIP]
>
>Você pode encontrar exemplos de query no documento [Construtor de Query](query-builder-api.md).

>[!TIP]
>
>Você pode encontrar o código desta página no GitHub
>
>* [Abra o projeto aem-search-custom-predicate-assessment no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)


>[!NOTE]
>
>Este código vinculado no GitHub e os trechos de código neste documento são fornecidos apenas para fins de demonstração.

### Prever avaliador em Detalhe {#predicate-evaluator-in-detail}

Um avaliador de predicado lida com a avaliação de determinados predicados, que são as restrições de definição de um query.

Ele mapeia uma restrição de pesquisa de nível superior (como `width>200`) para um query JCR específico que se encaixa no modelo de conteúdo real (por exemplo, `metadata/@width > 200`). Ou pode filtrar manualmente os nós e verificar suas restrições.

>[!TIP]
>
>Para obter mais informações sobre o pacote `PredicateEvaluator` e `com.day.cq.search`, consulte a [documentação do Java](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementação de um Avaliador Predicado Personalizado para Metadados de Replicação {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

Como exemplo, esta seção descreve como criar um avaliador de predicado personalizado que ajuda os dados com base nos metadados de replicação:

* `cq:lastReplicated` que armazena a data da última ação de replicação
* `cq:lastReplicatedBy` que armazena a ID do usuário que acionou a última ação de replicação
* `cq:lastReplicationAction` que armazena a última ação de replicação (por exemplo, Ativação, Desativação)

#### Consultando metadados de replicação com avaliadores preditivos padrão {#querying-replication-metadata-with-default-predicate-evaluators}

O query a seguir busca a lista de nós na ramificação `/content` que foram ativados por `admin` desde o início do ano.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

Esse query é válido, mas difícil de ler, e não destaca a relação entre as três propriedades de replicação. A implementação de um avaliador de predicado personalizado reduzirá a complexidade e melhorará a semântica desse query.

#### Objetivos {#objectives}

O objetivo do `ReplicationPredicateEvaluator` é suportar o query acima usando a seguinte sintaxe.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

O agrupamento de metadados de replicação prevê com um avaliador de predicado personalizado ajuda a criar um query significativo.

#### Atualizando dependências Maven {#updating-maven-dependencies}

>[!TIP]
>
>A configuração de novos projetos de AEM incluindo o uso de maven é explicada detalhadamente por [o tutorial WKND.](develop-wknd-tutorial.md)

Primeiro, você precisa atualizar as dependências Maven do seu projeto. O `PredicateEvaluator` faz parte do artefato `cq-search`, portanto, ele precisa ser adicionado ao arquivo pom Maven.

>[!NOTE]
>
>O escopo da dependência `cq-search` está definido como `provided` porque `cq-search` será fornecido pelo container `OSGi`.

O trecho a seguir mostra as diferenças no arquivo `pom.xml`, em [formato diff unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

```text
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

#### Gravando o ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

O projeto `cq-search` contém a classe abstrata `AbstractPredicateEvaluator`. Isso pode ser estendido com algumas etapas para implementar seu próprio avaliador de predicado personalizado `(PredicateEvaluator`).

>[!NOTE]
>
>O procedimento a seguir explica como criar uma expressão `Xpath` para filtrar dados. Outra opção seria implementar o método `includes` que seleciona os dados em uma base de linha. Consulte a [documentação do Java](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html#includes28comdaycqsearchpredicatejavaxjcrqueryrowcomdaycqsearchevalevaluationcontext29) para obter mais informações.

1. Crie uma nova classe Java que estende `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Faça anotações em sua classe com um trecho `@Component` como exibido em [formato diff unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

   ```text
   @@ -19,8 +19,11 @@
     */
    package com.adobe.aem.docs.search;
   
   +import org.apache.felix.scr.annotations.Component;
   +import com.day.cq.search.eval.AbstractPredicateEvaluator;
   
   +@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
    public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {
   
    }
   ```

   >[!NOTE]
   >
   >`factory`tem de ser uma cadeia de caracteres exclusiva que começa com `com.day.cq.search.eval.PredicateEvaluator/`e termina com o nome do seu `PredicateEvaluator` personalizado.

   >[!NOTE]
   >
   >O nome do `PredicateEvaluator` é o nome do predicado, que é usado ao criar query.

1. Substituir:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   No método override, você cria uma expressão `Xpath` com base no argumento `Predicate` fornecido.

### Exemplo de um Avaliador Predicado Personalizado para Metadados de Replicação {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

A implementação completa deste `PredicateEvaluator` pode ser semelhante à seguinte classe.

```java
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```
