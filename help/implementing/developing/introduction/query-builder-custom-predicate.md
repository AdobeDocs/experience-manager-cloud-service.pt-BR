---
title: Implementando um Avaliador de Predicados Personalizados para o Construtor de Consultas
description: O Query Builder no AEM oferece uma maneira fácil e personalizável de consultar o repositório de conteúdo
exl-id: 8c2f8c22-1851-4313-a1c9-10d6d9b65824
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---

# Implementando um Avaliador de Predicados Personalizados para o Construtor de Consultas {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

Este documento descreve como estender o [Query Builder](query-builder-api.md) implementando um avaliador de predicado personalizado.

## Visão geral {#overview}

O [Query Builder](query-builder-api.md) O oferece uma maneira fácil de consultar o repositório de conteúdo. AEM vem com [um conjunto de avaliadores de predicados](#query-builder-predicates.md) que ajudam a consultar seus dados.

No entanto, você pode querer simplificar suas consultas implementando um avaliador de predicado personalizado que oculta alguma complexidade e garante uma melhor semântica.

Um predicado personalizado também pode executar outras coisas que não são diretamente possíveis com o XPath, por exemplo:

* Consultando dados de outro serviço
* Filtragem personalizada com base em um cálculo

>[!NOTE]
>
>Problemas de desempenho devem ser considerados ao implementar um predicado personalizado.

>[!TIP]
>
>Você pode encontrar exemplos de queries no [Query Builder](query-builder-api.md) documento.

>[!TIP]
>
>Você pode encontrar o código desta página no GitHub
>
>* [Abra o projeto aem-search-custom-predicate-assessment no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)


>[!NOTE]
>
>Este código vinculado no GitHub e os trechos de código neste documento são fornecidos apenas para fins de demonstração.

### Avaliador de Predicados em Detalhes {#predicate-evaluator-in-detail}

Um avaliador de predicado lida com a avaliação de determinados predicados, que são as restrições de definição de um query.

Mapeia uma restrição de pesquisa de nível superior (como `width>200`) a uma consulta JCR específica que se ajuste ao modelo de conteúdo real (por exemplo, `metadata/@width > 200`). Ou pode filtrar nós manualmente e verificar suas restrições.

>[!TIP]
>
>Para obter mais informações sobre o `PredicateEvaluator` e `com.day.cq.search` consulte o [Documentação do Java](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementando um avaliador de predicado personalizado para metadados de replicação {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

Como exemplo, esta seção descreve como criar um avaliador de predicado personalizado que ajuda os dados com base nos metadados de replicação:

* `cq:lastReplicated` que armazena a data da última ação de replicação
* `cq:lastReplicatedBy` que armazena o id do usuário que acionou a última ação de replicação
* `cq:lastReplicationAction` que armazena a última ação de replicação (por exemplo, Ativação, Desativação)

#### Consulta de metadados de replicação com avaliadores de predicado padrão {#querying-replication-metadata-with-default-predicate-evaluators}

A consulta a seguir busca a lista de nós em `/content` ramificação que foi ativada por `admin` desde o início do ano.

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

Esta consulta é válida, mas difícil de ler, e não realça a relação entre as três propriedades de replicação. A implementação de um avaliador de predicado personalizado reduzirá a complexidade e melhorará a semântica deste query.

#### Objetivos {#objectives}

O objetivo da `ReplicationPredicateEvaluator` O é compatível com a consulta acima usando a seguinte sintaxe.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

O agrupamento de metadados de replicação prevê com um avaliador de predicado personalizado ajuda a criar um query significativa.

#### Atualização de dependências do Maven {#updating-maven-dependencies}

>[!TIP]
>
>A criação de novos projetos de AEM, incluindo a utilização de maven, é explicada em pormenor por [o tutorial WKND.](develop-wknd-tutorial.md)

Primeiro, você precisa atualizar as dependências Maven do seu projeto. O `PredicateEvaluator` faz parte do `cq-search` artefato, portanto, ele precisa ser adicionado ao arquivo pom Maven.

>[!NOTE]
>
>O âmbito da `cq-search` a dependência está definida como `provided` porque `cq-search` será fornecido pelo `OSGi` contêiner.

O trecho a seguir mostra as diferenças no `pom.xml` arquivo, em [formato diff unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

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

#### Escrever O ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

O `cq-search` o projeto contém a variável `AbstractPredicateEvaluator` classe abstrata. Isso pode ser estendido com algumas etapas para implementar seu próprio avaliador de predicado personalizado `(PredicateEvaluator`).

>[!NOTE]
>
>O procedimento a seguir explica como criar um `Xpath` para filtrar dados. Outra opção seria implementar o `includes` que seleciona dados com base em linhas. Consulte a [Documentação do Java](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html) para obter mais informações.

1. Crie uma nova classe Java que se estende `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Faça anotações em sua classe com um `@Component` curtir o trecho exibido em [formato diff unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

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
   >O `factory`deve ser uma string exclusiva que começa com `com.day.cq.search.eval.PredicateEvaluator/`e terminando com o nome do seu `PredicateEvaluator`.

   >[!NOTE]
   >
   >O nome do `PredicateEvaluator` é o nome do predicado, que é usado ao criar consultas.

1. Substituir:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   No método de substituição, você cria um `Xpath` com base na `Predicate` fornecida no argumento .

### Exemplo de um Avaliador de Predicado Personalizado para Metadados de Replicação {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

A implementação completa do `PredicateEvaluator` pode ser semelhante à seguinte classe.

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
