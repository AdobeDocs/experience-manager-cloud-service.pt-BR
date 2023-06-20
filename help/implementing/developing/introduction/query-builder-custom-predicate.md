---
title: Implementação de um avaliador de predicado personalizado no Construtor de consultas
description: O Query Builder do AEM oferece uma maneira fácil e personalizável de consultar o repositório de conteúdo
exl-id: 8c2f8c22-1851-4313-a1c9-10d6d9b65824
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Implementação de um avaliador de predicado personalizado no Construtor de consultas {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

Este documento descreve como estender o [Construtor de consulta](query-builder-api.md) implementando um avaliador de predicado personalizado.

## Visão geral {#overview}

A variável [Construtor de consulta](query-builder-api.md) O oferece uma maneira fácil de consultar o repositório de conteúdo. AEM vem com [um conjunto de avaliadores de predicados](#query-builder-predicates.md) que ajudam a consultar seus dados.

No entanto, talvez você queira simplificar suas consultas implementando um avaliador de predicado personalizado que oculta alguma complexidade e garante uma semântica melhor.

Um predicado personalizado também pode executar outras coisas que não são diretamente possíveis com XPath, por exemplo:

* Consulta de dados de outro serviço
* Filtros personalizados com base em um cálculo

>[!NOTE]
>
>Problemas de desempenho devem ser considerados ao implementar um predicado personalizado.

>[!TIP]
>
>Você pode encontrar exemplos de queries no [Construtor de consulta](query-builder-api.md) documento.

>[!TIP]
>
>Você pode encontrar o código desta página no GitHub
>
>* [Abra o projeto aem-search-custom-predicate-valuator no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

>[!NOTE]
>
>Este código vinculado no GitHub e os trechos de código neste documento são fornecidos apenas para fins de demonstração.

### Avaliador de predicado em detalhes {#predicate-evaluator-in-detail}

Um avaliador de predicado lida com a avaliação de determinados predicados, que são as restrições de definição de uma consulta.

Ele mapeia uma restrição de pesquisa de nível superior (como `width>200`) para uma consulta JCR específica que se ajuste ao modelo de conteúdo real (por exemplo, `metadata/@width > 200`). Ou ele pode filtrar nós manualmente e verificar suas restrições.

>[!TIP]
>
>Para obter mais informações sobre o `PredicateEvaluator` e a variável `com.day.cq.search` pacote consulte o [Documentação Java](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementação de um avaliador de predicado personalizado para metadados de replicação {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

Como exemplo, esta seção descreve como criar um avaliador de predicado personalizado que ajuda os dados com base nos metadados de replicação:

* `cq:lastReplicated` que armazena a data da última ação de replicação
* `cq:lastReplicatedBy` que armazena a id do usuário que acionou a última ação de replicação
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

Essa consulta é válida, mas difícil de ler e não realça a relação entre as três propriedades de replicação. A implementação de um avaliador de predicado personalizado reduzirá a complexidade e melhorará a semântica desse query.

#### Objetivos {#objectives}

A meta do `ReplicationPredicateEvaluator` é para oferecer suporte à consulta acima usando a seguinte sintaxe.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

O agrupamento de predicados de metadados de replicação com um avaliador de predicado personalizado ajuda a criar uma consulta significativa.

#### Atualização de dependências do Maven {#updating-maven-dependencies}

>[!TIP]
>
>A criação de novos projetos AEM, incluindo o uso do maven, é explicada em detalhes por [o tutorial do WKND.](develop-wknd-tutorial.md)

Primeiro, é necessário atualizar as dependências do Maven do seu projeto. A variável `PredicateEvaluator` faz parte da `cq-search` artefato, portanto, ele precisa ser adicionado ao seu arquivo pom Maven.

>[!NOTE]
>
>O âmbito de aplicação do `cq-search` a dependência está definida como `provided` porque `cq-search` é fornecido pela `OSGi` recipiente.

O trecho a seguir mostra as diferenças no `pom.xml` arquivo, em [formato de comparação unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

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

#### Gravando O ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

A variável `cq-search` o projeto contém o `AbstractPredicateEvaluator` classe abstrata. Isso pode ser estendido com algumas etapas para implementar seu próprio avaliador de predicado personalizado `(PredicateEvaluator`).

>[!NOTE]
>
>O procedimento a seguir explica como criar uma `Xpath` expressão para filtrar dados. Outra opção seria implementar a `includes` método que seleciona dados em base de linha. Consulte a [Documentação Java](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html) para obter mais informações.

1. Crie uma nova classe Java que estenda `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Anotar sua classe com um `@Component` curtir apresentações de trechos em [formato de comparação unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

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
   >A variável `factory`deve ser uma sequência de caracteres exclusiva, começando com `com.day.cq.search.eval.PredicateEvaluator/`e terminando com o nome do seu personalizado `PredicateEvaluator`.

   >[!NOTE]
   >
   >O nome do `PredicateEvaluator` é o nome do predicado, que é usado ao criar consultas.

1. Substituir:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   No método de substituição, você cria um `Xpath` expressão baseada no `Predicate` argumento.

### Exemplo de um avaliador de predicado personalizado para metadados de replicação {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

A execução completa deste `PredicateEvaluator` pode ser semelhante à seguinte classe.

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
