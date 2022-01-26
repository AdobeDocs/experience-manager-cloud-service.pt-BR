---
title: Remoção do índice de lucene genérico
description: Remoção do índice de lucene genérico
exl-id: fe0e00ac-f9c8-43cf-83c2-5a353f5eaeab
source-git-commit: bc7ef6567ad5baa4becd28a7e7d96bd6b579e1ad
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 0%

---

# Remoção do índice &quot;lucene genérico&quot;

O Adobe pretende remover o índice &quot;genérico lucene&quot; (`/oak:index/lucene-*`) da Adobe Experience Manager as a Cloud Service. Este índice está obsoleto desde o AEM 6.5. Nesta documentação, o impacto desta decisão é descrito, juntamente com descrições detalhadas sobre como examinar se uma instância AEM é afetada. Por fim, ele contém maneiras de alterar consultas para que elas funcionem sem que esse índice esteja presente.

## Segundo plano

Em AEM, consultas &quot;fulltext&quot; são aquelas que usam as seguintes funções:

* `jcr:contains()` no JCR XPATH
* `CONTAINS` em JCR-SQL2

Essas consultas não podem retornar resultados sem usar um índice. Ao contrário de uma consulta que contém apenas restrições de caminho ou propriedade, uma consulta que contém uma restrição de texto completo para a qual nenhum índice pode ser encontrado (e, portanto, uma travessia é executada) sempre retornará 0 resultados.

O índice &quot;genérico lucene&quot; (`/oak:index/lucene-*`) existe desde o AEM 6.0 / Oak 1.0 para fornecer uma pesquisa de texto completo na maioria da hierarquia do repositório (alguns caminhos, como `/jcr:system` e `/var` sempre foram excluídos disso), no entanto, esse índice foi substituído em grande parte por índices em tipos de nó mais específicos (por exemplo, `damAssetLucene-*` para o tipo de nó &quot;dam:Asset&quot;) que suporta pesquisas de texto completo e de propriedade.

No AEM 6.5, o índice &quot;genérico lucene&quot; foi marcado como obsoleto (indicado que seria removido em versões futuras) e, desde então, um AVISO foi registrado quando o índice foi usado:

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'search term') and isdescendantnode(a, '/content/mysite') /* xpath: /jcr:root/content/mysite//*[jcr:contains(.,"search term")] */ fullText="search" "term", path=/content/mysite//*). Please change the query or the index definitions.
```

Em versões recentes de AEM, o índice &quot;lucene genérico&quot; foi usado para suportar um número muito pequeno de recursos. Eles estão sendo retrabalhados para usar outros índices ou modificados de outra forma para remover a dependência desse índice.
Por exemplo, as consultas &quot;pesquisa de referência&quot;, do formulário mostrado abaixo, agora devem estar usando o índice em &#39;/oak:index/pathreference&#39; (que indexa apenas os valores de propriedade String que correspondem a uma expressão regular que procura caminhos JCR). 

```
//*[jcr:contains(., '"/content/dam/mysite"')]
```

Para oferecer suporte a grandes volumes de dados do cliente, o Adobe não criará mais o índice &quot;lucene genérico&quot; em novos ambientes as a Cloud Service AEM e, a partir daí, começará a remover o índice dos repositórios existentes. Já ajustamos os custos do índice (por meio das propriedades &#39;costPerEntry&#39; e &#39;costPerExecution&#39;) para garantir que outros índices (como `/oak:index/pathreference`) são usados em detrimento de `/oak:index/lucene-*` sempre que possível. 

Os aplicativos do cliente que usam queries que ainda dependem desse índice devem ser atualizados imediatamente para aproveitar outros índices existentes (que podem ser personalizados, se necessário) ou novos índices personalizados devem ser adicionados ao aplicativo do cliente. Instruções completas para o gerenciamento de índice em AEM as a Cloud Service podem ser encontradas no [documentação de indexação](/help/operations/indexing.md).

## Como saber se seu aplicativo depende do índice &quot;genérico lucene&quot;?

O índice &quot;lucene genérico&quot; é usado no momento como &quot;fallback&quot; se nenhum outro índice de texto completo puder atender a uma consulta. Quando esse índice obsoleto é usado, uma mensagem como essa será registrada no nível WARN:

```
org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*). Please change the query or the index definitions.
```

Em algumas circunstâncias, o Oak pode tentar usar outro índice de texto completo (como `/oak:index/pathreference`) para oferecer suporte à consulta de texto completo, mas se a sequência de consulta não corresponder à expressão regular na definição do índice, uma mensagem será registrada no nível WARN e a consulta provavelmente não retornará resultados.

```
org.apache.jackrabbit.oak.query.QueryImpl Potentially improper use of index /oak:index/pathReference with queryFilterRegex (["']|^)/ to search for value "test"
```

Depois que o índice &quot;lucene genérico&quot; for removido, uma mensagem como mostrado abaixo será registrada no nível AVISO se uma consulta de texto completo não conseguir localizar nenhuma definição de índice adequada:

```
org.apache.jackrabbit.oak.query.QueryImpl Fulltext query without index for filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') /* xpath: //*[jcr:contains(.,"test")] */ fullText="test", path=*); no results will be returned
```

Se algum desses for registrado, talvez seja necessário retrabalhar a consulta para usar um índice de texto completo diferente ou fornecer um novo índice para suportar a consulta. Detalhes dos tipos de dependências que você poderá ver e como resolvê-las são fornecidos abaixo.

## Possíveis dependências no índice &quot;lucene genérico&quot;

### Publicação

#### Consultas personalizadas do aplicativo

A fonte mais comum de consultas que usam o índice &quot;lucene genérico&quot; em Publicar será consultas de aplicativo personalizadas.

Nos casos mais simples, essas podem ser consultas sem o tipo de nó especificado (implicando &#39;nt:base&#39;) ou nt:base especificado explicitamente, como:

```
/jcr:root/content/mysite//*[jcr:contains(., 'search term')]
/jcr:root/content/mysite//element(*, nt:base)[jcr:contains(., 'search term')]
```

Ação necessária : Essas consultas podem ser modificadas para usar um tipo de nó apropriado - por exemplo, para retornar resultados correspondentes a páginas (ou qualquer uma das &quot;agregações&quot; abaixo do nó cq:Page ), a consulta poderia se tornar:

```
/jcr:root/content/mysite//element(*, cq:Page)[jcr:contains(., 'search term')]
```

Em outros casos, uma consulta pode especificar um tipo de nó, mas conter uma restrição de texto completo que não pode ser manipulada por outro índice de texto completo, como:

```
/jcr:root/content/dam//element(*, dam:Asset)[jcr:contains(jcr:content/metadata/@cq:tags, 'NewsTopics:cateogries/domestic'))]
```

Nesse caso, a consulta tem o tipo de nó &quot;dam:Asset&quot;, mas contém uma restrição de texto completo no relativo `jcr:content/metadata/@cq:tags` propriedade.

Essa propriedade não está marcada como &quot;analisada&quot; no índice damAssetLucene (o índice de texto completo mais usado para consultas contra o tipo de nó &quot;dam:Asset&quot;), portanto, esse índice não pode ser usado para esta consulta.

Dessa forma, a consulta volta ao índice &#39;generic fulltext&#39;, onde todas as propriedades incluídas são marcadas como analisadas pela correspondência curinga em `/oak:index/lucene-2/indexRules/nt:base/properties/prop`.

Ação necessária do cliente : marcação da `jcr:content/metadata/@cq:tags` A propriedade como &quot;analisado&quot; em uma versão personalizada do índice damAssetLucene resultará na manipulação dessa consulta por esse índice, e nenhum AVISO será registrado.

### Autor 

Além de queries nos servlets de aplicativos do cliente, componentes OSGI e scripts de renderização, pode haver vários usos específicos do autor do índice &quot;lucene genérico&quot;. 

#### Pesquisa de referência

Historicamente, o índice &quot;lucene genérico&quot; foi usado para suportar &quot;pesquisa de referência&quot; (pesquisa por conteúdo que contém referências a outro caminho de conteúdo). Essas consultas já devem ter sido movidas para usar o novo índice &#39;/oak:index/pathreference&#39;.
Ação necessária do cliente : nenhuma ação necessária do cliente.


#### Pesquisa no seletor de campo de caminho

AEM inclui um componente de diálogo personalizado (tipo de recurso Sling &#39;granite/ui/components/coral/foundation/form/pathfield&#39;) que fornece um navegador (seletor) para selecionar outro caminho AEM.  O seletor de campo de caminho padrão (usado quando nenhuma propriedade &#39;pickerSrc&#39; personalizada definida na estrutura do conteúdo) renderiza uma barra de pesquisa na caixa de diálogo pop-up.
Os tipos de nó contra os quais pesquisar podem ser especificados usando a propriedade &#39;nodeTypes&#39; .

No momento, se nenhuma propriedade &#39;nodeTypes&#39; estiver presente, a consulta de pesquisa subjacente usará o tipo de nó &#39;nt:base&#39; e, portanto, provavelmente usará o índice &#39;generic lucene&#39; (normalmente, registrando as mensagens WARN mostradas abaixo).

```
20.01.2022 18:56:06.412 *WARN* [127.0.0.1 [1642704966377] POST /mnt/overlay/granite/ui/content/coral/foundation/form/pathfield/picker.result.single.html HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex This index is deprecated: /oak:index/lucene-2; it is used for query Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a where contains(*, 'test') and isdescendantnode(a, '/content') /* xpath: /jcr:root/content//element(*, nt:base)[(jcr:contains(., 'test'))] order by @jcr:score descending */ fullText="test", path=/content//*). Please change the query or the index definitions.
```

Antes da remoção de &quot;lucene genérico&quot;, o componente pathfield será atualizado para que a caixa de pesquisa fique oculta para componentes que usam o seletor padrão, que não fornecem uma propriedade &quot;nodeTypes&quot;.

| Seletor de campo de caminho com pesquisa | Seletor de campo de caminho sem pesquisa |
|---|---|
| ![Seletor de campo de caminho com pesquisa](assets/index-pathfield-picker-with-search.png) | ![Seletor de campo de caminho sem pesquisa](assets/index-pathfield-picker-without-search.png) |


Ação necessária do cliente : Se nenhuma pesquisa for necessária, nenhuma ação será necessária do cliente.

Se o cliente quiser manter a funcionalidade de Pesquisa no seletor de campos, uma propriedade &quot;nodeTypes&quot; deverá ser fornecida listando os tipos de nós com os quais deseja consultar. Eles podem ser especificados como uma lista separada por vírgulas de tipos de nó em uma propriedade String.


>[!NOTE]
>O Editor do modelo de fragmento de conteúdo usa campos especializados de caminho com o Tipo de recurso do Sling &#39;dam/cfm/models/editor/components/contentreference&#39;.
> * No momento, esses executam queries sem tipos de nó especificados - resultando em um AVISO sendo registrado devido ao uso do índice &quot;lucene genérico&quot;.
> * Em breve, as instâncias desses componentes serão automaticamente padronizadas para usar os tipos de nó &#39;cq:Page&#39; e &#39;dam:Asset&#39; sem nenhuma ação adicional do cliente.
> * A propriedade &#39;nodeTypes&#39; pode ser adicionada para substituir esses tipos de nó padrão. 





## Linha do tempo para remover o &quot;lucene genérico&quot;

O Adobe terá uma abordagem de duas fases para a remoção do índice &quot;genérico lucene&quot;.

**Fase 1** (previsto para 31 de janeiro de 2022): Não crie mais &#39;/oak:index/lucene-*&#39; em novos ambientes AEM as a Cloud Service.

**Fase 2** (previsto para 31 de março de 2022) : Remova o índice &#39;/oak:index/lucene-*&#39; de novos ambientes AEM as a Cloud Service.

O Adobe monitorará as mensagens de log anotadas acima e tentará entrar em contato com os clientes que permanecem dependentes do índice &quot;generic lucene&quot;.

Como mitigação a curto prazo, se necessário, o Adobe adicionará definições de índice personalizadas diretamente aos sistemas do cliente para evitar problemas funcionais ou de desempenho como resultado da remoção do índice &quot;lucene genérico&quot;.

Nesses casos, o cliente receberá a definição de índice atualizada e será aconselhado a incluí-la em versões futuras de seu aplicativo por meio do Cloud Manager.
