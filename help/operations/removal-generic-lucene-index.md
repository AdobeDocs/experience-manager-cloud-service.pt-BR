---
title: Remoção Genérica do Índice Lucene
description: Saiba mais sobre a remoção planejada de índices genéricos de Lucene e como você pode ser afetado.
exl-id: 3b966d4f-6897-406d-ad6e-cd5cda020076
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---

# Remoção Genérica do Índice Lucene {#generic-lucene-index-removal}

O Adobe pretende remover o índice &quot;genérico Lucene&quot; (`/oak:index/lucene-*`) da Adobe Experience Manager as a Cloud Service. Este índice está obsoleto desde o AEM 6.5. Neste documento é descrito o impacto desta decisão, juntamente com descrições detalhadas sobre como examinar se uma instância AEM é afetada. Também contém maneiras de alterar queries para que eles continuem a funcionar sem o índice Lucene genérico.

## Segundo plano {#background}

Em AEM, as consultas de texto completo são aquelas que usam as seguintes funções:

* `jcr:contains()` no JCR XPATH
* `CONTAINS` em JCR-SQL2

Essas consultas não podem retornar resultados sem usar um índice. Ao contrário de uma consulta que contém apenas restrições de caminho ou propriedade, uma consulta que contém uma restrição de texto completa para a qual nenhum índice pode ser encontrado (e, portanto, uma travessia é executada) sempre retornará resultados zero.

O índice Lucene genérico (`/oak:index/lucene-*`) existe desde o AEM 6.0 / Oak 1.0 para fornecer uma pesquisa de texto completo na maioria da hierarquia do repositório, embora alguns caminhos, como `/jcr:system` e `/var` sempre foram excluídas disso. No entanto, esse índice foi substituído em grande parte por índices em tipos de nó mais específicos (por exemplo, `damAssetLucene-*` para `dam:Asset` tipo de nó ), que suporta texto completo e pesquisas de propriedade.

No AEM 6.5, o índice Lucene genérico foi marcado como obsoleto, indicando que seria removido em versões futuras. Desde então, um AVISO foi registrado quando o índice foi usado, conforme ilustrado pelo seguinte trecho de log:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

Em versões recentes de AEM, o índice genérico Lucene foi usado para suportar um número muito pequeno de recursos. Eles estão sendo retrabalhados para usar outros índices ou modificados de outra forma para remover a dependência desse índice.

Por exemplo, consultas de pesquisa de referência, como no exemplo a seguir, agora devem usar o índice em `/oak:index/pathreference`, que indexam somente `String` valores de propriedade que correspondem a uma expressão regular que procura caminhos JCR.

```text
//*[jcr:contains(., '"/content/dam/mysite"')]
```

Para oferecer suporte a grandes volumes de dados do cliente, o Adobe não criará mais o índice Lucene genérico em novos ambientes AEM as a Cloud Service. Além disso, o Adobe começará a remover o índice dos repositórios existentes. [Ver a linha do tempo](#timeline) no final deste documento para obter mais detalhes.

O Adobe já ajustou os custos do índice por meio do `costPerEntry` e `costPerExecution` para garantir que outros índices, como `/oak:index/pathreference` sempre que possível, são utilizadas de preferência.

Os aplicativos do cliente que usam queries que ainda dependem desse índice devem ser atualizados imediatamente para aproveitar outros índices existentes, que podem ser personalizados, se necessário. Como alternativa, novos índices personalizados podem ser adicionados ao aplicativo do cliente. Instruções completas para o gerenciamento de índice AEM as a Cloud Service podem ser encontradas no [documentação de indexação.](/help/operations/indexing.md)

## Você É Afetado? {#are-you-affected}

O índice Lucene genérico é usado no momento como um fallback se nenhum outro índice de texto completo puder atender a um query. Quando esse índice obsoleto é usado, uma mensagem como essa será registrada no nível WARN:

```text
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

Em algumas circunstâncias, o Oak pode tentar usar outro índice de texto completo (como `/oak:index/pathreference`) para oferecer suporte à consulta de texto completo, mas se a sequência de consulta não corresponder à expressão regular na definição do índice, uma mensagem será registrada no nível WARN e a consulta provavelmente não retornará resultados.

```text
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

Depois que o índice Lucene genérico for removido, uma mensagem como mostrado abaixo será registrada no nível AVISO se uma consulta de texto completo não conseguir localizar nenhuma definição de índice adequada:

```text
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

>[!IMPORTANT]
>
>**Ação necessária do cliente**
>
> Se qualquer uma das mensagens de aviso acima for registrada, talvez seja necessário retrabalhar a consulta para usar um índice de texto completo diferente ou fornecer um novo índice para suportar a consulta.
>
>Detalhes dos tipos de dependências que você poderá ver e como resolvê-las são fornecidos nas seções a seguir.

## Dependências Potenciais em Índices Lucene Genéricos {#potential-dependencies}

Há várias áreas em que seus aplicativos e instalações de AEM podem ser dependentes de índices genéricos de Lucene em instâncias de autor e publicação.

### Instância de publicação {#publish-instance}

#### Consultas de Aplicativo Personalizado {#custom-application-queries}

A fonte mais comum de queries usando o índice Lucene genérico em uma instância de publicação serão queries de aplicativo personalizados.

Nos casos mais simples, essas podem ser consultas sem o tipo de nó especificado, implicando `nt:base` ou `nt:base` especificado explicitamente, como:

```text
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

>[!IMPORTANT]
>
>**Ação necessária do cliente**
>
>As consultas mencionadas acima devem ser modificadas para usar um tipo de nó apropriado, conforme detalhado na seção a seguir.

Por exemplo, as consultas podem ser modificadas para retornar resultados correspondentes a páginas ou qualquer uma das agregações abaixo da variável `cq:Page node`. O query poderia então se tornar:

```text
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

Em outros casos, um query pode especificar um tipo de nó, mas conter uma restrição de texto completo que não pode ser manipulada por outro índice de texto completo, como:

```text
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

Nesse caso, a query tem a variável `dam:Asset` tipo de nó, mas contém uma restrição de texto completo no relativo `jcr:content/metadata/@cq:tags` propriedade.

Essa propriedade não está marcada como analisada no `damAssetLucene` índice, que é o índice de texto completo mais usado para queries no `dam:Asset` tipo de nó. Portanto, esse índice não pode ser usado para esta consulta.

Dessa forma, a consulta volta ao índice de texto completo genérico, onde todas as propriedades incluídas são marcadas como analisadas pela correspondência curinga em `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

>[!IMPORTANT]
>
>**Ação necessária do cliente**
>
>Marcar o `jcr:content/metadata/@cq:tags` como analisado em uma versão personalizada do `damAssetLucene` O índice resultará na manipulação dessa consulta por esse índice, e nenhum AVISO será registrado.

### Instância do autor {#author-instance}

Além de consultas em servlets de aplicativos do cliente, componentes OSGi e scripts de renderização, pode haver vários usos específicos do autor do índice Lucene genérico.

#### Pesquisa de referência {#reference-search}

Historicamente, o índice Lucene genérico foi usado para suportar pesquisa de referência ou pesquisa de conteúdo que contém referências a outro caminho de conteúdo. Essas consultas já devem ter sido atualizadas para usar o novo `/oak:index/pathreference` índice.

#### Pesquisa do seletor de campo de caminho {#picker-search}

AEM inclui um componente de diálogo personalizado com o tipo de recurso Sling `granite/ui/components/coral/foundation/form/pathfield`, que fornece um navegador/seletor para selecionar outro caminho de AEM. O seletor de campo de caminho padrão, que é usado quando não é personalizado `pickerSrc` é definida na estrutura do conteúdo, renderiza uma barra de pesquisa na caixa de diálogo pop-up.

Os tipos de nó em relação aos quais a pesquisa pode ser especificada usando o `nodeTypes` propriedade.

Atualmente, se não `nodeTypes` estiver presente, a consulta de pesquisa subjacente usará a variável `nt:base` tipo de nó e, portanto, provavelmente usará o índice Lucene genérico, normalmente registrando mensagens WARN semelhantes ao seguinte.

```text
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

Antes da remoção do índice Lucene genérico, a variável `pathfield` será atualizado para que a caixa de pesquisa fique oculta para componentes que usam o seletor padrão, que não fornecem um `nodeTypes` propriedade.

| Seletor de campo de caminho com pesquisa | Seletor de campo de caminho sem pesquisa |
|---|---|
| ![Seletor de campo de caminho com pesquisa](assets/index-pathfield-picker-with-search.png) | ![Seletor de campo de caminho sem pesquisa](assets/index-pathfield-picker-without-search.png) |

>[!IMPORTANT]
>
>**Ação necessária do cliente**
>
>Se o cliente quiser manter a funcionalidade de pesquisa dentro do seletor de campo de caminho, uma `nodeTypes` deve ser fornecida listando os tipos de nó com os quais deseja consultar. Eles podem ser especificados como uma lista separada por vírgulas de tipos de nó em uma `String` propriedade. Se nenhuma pesquisa for necessária, nenhuma ação será necessária do cliente.

>[!NOTE]
>
>O Editor do modelo de fragmento de conteúdo usa campos de caminho especializados com o tipo de recurso Sling `dam/cfm/models/editor/components/contentreference`.
> * No momento, esses executam queries sem tipos de nó especificados, resultando em um AVISO sendo registrado devido ao uso do índice Lucene genérico.
> * Em breve, as instâncias desses componentes serão automaticamente padronizadas para usar `cq:Page` e `dam:Asset` tipos de nó sem nenhuma ação adicional do cliente.
> * O `nodeTypes` pode ser adicionada para substituir esses tipos de nó padrão.


## Linha do tempo para remoção de Lucene genérica {#timeline}

O Adobe usará uma abordagem de duas fases para remover o índice Lucene genérico.

* **Fase 1** (início previsto em 31 de Janeiro de 2022): Não criar mais `/oak:index/lucene-*` em novos ambientes AEM as a Cloud Service.
* **Fase 2** (início previsto em 31 de março de 2022): Remover `/oak:index/lucene-*` indexe de ambientes as a Cloud Service existentes AEM.

O Adobe monitorará as mensagens de log anotadas acima e tentará entrar em contato com os clientes que permanecem dependentes do índice Lucene genérico.

Como mitigação a curto prazo, o Adobe adicionará definições de índice personalizadas diretamente aos sistemas do cliente para evitar problemas funcionais ou de desempenho como resultado da remoção do índice Lucene genérico, conforme necessário.

Nesses casos, o cliente receberá a definição de índice atualizada e será aconselhado a incluí-la em versões futuras de seu aplicativo por meio do Cloud Manager.
