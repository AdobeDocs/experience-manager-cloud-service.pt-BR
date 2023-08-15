---
title: Uso de adaptadores Sling
description: O Sling oferece um padrão de adaptador para traduzir convenientemente objetos que implementam a interface adaptável
exl-id: 8ffe3bbd-01fe-44c2-bf60-7a4d25a6ba2b
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2213'
ht-degree: 1%

---

# Uso de adaptadores Sling {#using-sling-adapters}

[Sling](https://sling.apache.org) oferece um [Padrão do adaptador](https://sling.apache.org/documentation/the-sling-engine/adapters.html) para traduzir convenientemente objetos que implementam a [Adaptável](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) interface. Essa interface fornece uma interface [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) método que traduz o objeto para o tipo de classe que está sendo transmitido como argumento.

Por exemplo, para traduzir um objeto Resource para o objeto Node correspondente, você pode simplesmente fazer:

```java
Node node = resource.adaptTo(Node.class);
```

## Casos de uso {#use-cases}

Existem os seguintes casos de uso:

* Obter objetos específicos de implementação.

  Por exemplo, uma implementação baseada em JCR do genérico [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) fornece acesso ao JCR subjacente [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Criação de atalhos de objetos que exigem que objetos de contexto interno sejam passados.

  Por exemplo, a variável baseada em JCR [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) mantém uma referência à solicitação do [`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html), que por sua vez é necessário para muitos objetos que funcionam com base nessa sessão de solicitação, como o [`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) ou [`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/security/UserManager.html).

* Atalho para serviços.

  Um caso raro - `sling.getService()` também é simples.

### Valor de retorno nulo {#null-return-value}

`adaptTo()` Pode retornar nulo.

Há vários motivos para o retorno nulo, incluindo o seguinte:

* a implementação não dá suporte ao tipo de destino
* uma fábrica de adaptadores que lida com esse caso não está ativa (por exemplo, devido a referências de serviço ausentes)
* falha na condição interna
* serviço não disponível

É importante que você lide com o caso nulo normalmente. Para renderizações jsp, pode ser aceitável que o jsp falhe se resultar em um conteúdo vazio.

### Armazenamento em cache {#caching}

Para melhorar o desempenho, as implementações estão livres para armazenar em cache o objeto retornado de uma `obj.adaptTo()` chame. Se a variável `obj` for o mesmo, o objeto retornado será o mesmo.

Esse armazenamento em cache é executado para todos `AdapterFactory` casos baseados.

No entanto, não há uma regra geral: o objeto pode ser uma nova instância ou uma existente. Dessa forma, significa que você não pode confiar em nenhum dos comportamentos. Por isso, é importante, especialmente dentro `AdapterFactory`, de que os objetos são reutilizáveis nesse cenário.

### Como funciona {#how-it-works}

Há várias maneiras de `Adaptable.adaptTo()` pode ser implementado:

* Pelo próprio objeto; implementando o próprio método e mapeando para determinados objetos.
* Por um [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), que podem mapear objetos arbitrários.

  Os objetos ainda devem implementar o `Adaptable` e deve estender [`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (que passa o `adaptTo` chamada para um gerenciador de adaptador central).

  Esse método permite ganchos na `adaptTo` para classes existentes, como `Resource`.

* Uma combinação de ambos.

Para o primeiro caso, os documentos Java™ podem indicar o que `adaptTo-targets` são possíveis. No entanto, para subclasses específicas, como o Recurso baseado em JCR, essa instrução geralmente não é possível. Neste último caso, as `AdapterFactory` normalmente fazem parte das classes privadas de um pacote e, portanto, não estão expostas em uma API do cliente, nem listadas em documentos Java™. Teoricamente, é possível acessar todos os `AdapterFactory` implementações do [OSGi](/help/implementing/deploying/configuring-osgi.md) tempo de execução do serviço e observar as configurações (fontes e destinos) de &quot;adaptáveis&quot;, mas não mapeá-las entre si. No final, depende da lógica interna, que deve ser documentada. Daí esta referência.

## Referência {#reference}

### Sling {#sling}

[**Recurso**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Se for um recurso baseado em nó JCR ou uma propriedade JCR, fazer referência a um nó</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Propriedade</a></td>
   <td>Se for um recurso baseado em propriedades do JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Item</a></td>
   <td>Se for um recurso baseado em JCR (nó ou propriedade)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">Mapa</a></td>
   <td>Retorna um mapa das propriedades, se for um recurso baseado em nó JCR (ou outro recurso que suporte mapas de valores)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Retorna um mapa conveniente de propriedades se for um recurso baseado em nó JCR (ou outro recurso que suporte mapas de valor). Também pode ser obtida (de forma mais simples) utilizando<br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code> (trata maiúsculas e minúsculas e assim por diante)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>Extensão do <a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> que permite que a hierarquia de recursos seja contabilizada ao procurar propriedades</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModisibleValueMap</a></td>
   <td>Uma extensão do <a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>, que permite modificar propriedades nesse nó</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Retorna o conteúdo binário de um recurso de arquivo (se for um recurso baseado em nó JCR e o tipo de nó for <code>nt:file</code> ou <code>nt:resource</code>; se for um recurso agrupado; conteúdo do arquivo, se for um recurso do sistema de arquivos). Ou retorna os dados de um recurso de propriedade JCR binário.</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Retorna um URL para o recurso (URL do repositório deste nó se for um recurso baseado em nó JCR; URL do pacote jar se for um recurso do pacote; URL do arquivo se for um recurso do sistema de arquivos)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">Arquivo</a></td>
   <td>Se for um recurso do sistema de arquivos</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Se o recurso for um script (por exemplo, arquivo jsp) para o qual um mecanismo de script está registrado com o sling</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">Servlet</a></td>
   <td>Se o recurso for um script (por exemplo, arquivo jsp) para o qual um mecanismo de script está registrado com sling, ou se for um recurso servlet</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Booleano</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Longo</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Duplo</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendário</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Valor</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Booleano[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendário[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Valor[]</a></td>
   <td>Retorna os valores se for um recurso baseado em propriedades JCR (e o valor se ajustar)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">RecursoRotulado</a></td>
   <td>Se for um recurso baseado em nó JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Page.html">Página</a></td>
   <td>Se for um recurso baseado em nó JCR e o nó for um <code>cq:Page</code> (ou <code>cq:PseudoPage</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/Component.html">Componente</a></td>
   <td>Se for um <code>cq:Component</code> recurso de nó</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/designer/Design.html">Design</a></td>
   <td>Se for um nó de design (<code>cq:Page</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Template.html">Modelo</a></td>
   <td>Se for um <code>cq:Template</code> recurso de nó</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>Se for um <code>cq:Template</code> recurso de nó</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/Asset.html">Ativo</a></td>
   <td>Se for um recurso de nó dam:Asset</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/Rendition.html">Representação</a></td>
   <td>Se for uma representação dam:Asset (nt:file na pasta de representação de um dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html">Tag</a></td>
   <td>Se for um <code>cq:Tag</code> recurso de nó</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Com base na sessão JCR, se ele for um recurso baseado em JCR e o usuário tiver permissões para acessar o UserManager</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizável</a></td>
   <td>A Autorizável é a interface básica comum para usuários e grupos</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuário</a></td>
   <td>O usuário é um Authorizable especial que pode ser autenticado e representado</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/SimpleSearch.html">PesquisaSimples</a></td>
   <td>Pesquisa abaixo o recurso (ou use setSearchIn()) se ele for um recurso baseado em JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Status do fluxo de trabalho para determinada página/nó de carga do fluxo de trabalho</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/ReplicationStatus.html">StatusReplicação</a></td>
   <td>Status de replicação para o recurso fornecido ou seu subnó jcr:content (marcado primeiro)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Retorna um recurso de conector adaptado para determinados tipos, se for um recurso baseado em nó JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/contentsync/config/package-summary.html">Configuração</a></td>
   <td>Se for um <code>cq:ContentSyncConfig</code> recurso de nó</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Se estiver abaixo de um <code>cq:ContentSyncConfig</code> recurso de nó</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ResourceResolver.html) adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>A sessão JCR da solicitação, se for um resolvedor de recursos baseado em JCR (padrão)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>Com base na sessão JCR, se for um resolvedor de recursos baseado em JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>Com base na sessão JCR, se for um resolvedor de recursos baseado em JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>O UserManager fornece acesso e meios para manter objetos autorizáveis, ou seja, usuários e grupos. O UserManager está associado a uma sessão específica
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizável</a> </td>
   <td>O usuário atual</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuário</a><br /> </td>
   <td>O usuário atual</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html">Externalizador</a></td>
   <td>Para externalizar URLs absolutos, mesmo sem o objeto de solicitação<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) adapta-se a:

Ainda sem destinos, mas implementa Adaptable e pode ser usado como origem em um AdapterFactory personalizado.

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ManipuladordeConteúdo</a><br /> (XML)</td>
   <td>Se for uma resposta de reescrita do sling</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Página](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Page.html)** adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><br /> </td>
   <td>Recurso da página.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">RecursoRotulado</a></td>
   <td>Recurso rotulado (== este).</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Nó da página.</td>
  </tr>
  <tr>
   <td>..</td>
   <td>Tudo ao qual o recurso da página pode ser adaptado.</td>
  </tr>
 </tbody>
</table>

**[Componente](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/Component.html)** adapta-se a:

| [Recurso](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso do componente. |
|---|---|
| [RecursoRotulado](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html) | Recurso rotulado (== este). |
| [Nó](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó do componente. |
| ... | Tudo ao qual o recurso do componente pode ser adaptado. |

**[Modelo](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Template.html)** adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Recurso do modelo.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">RecursoRotulado</a></td>
   <td>Recurso rotulado (== este).</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Nó deste modelo.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tudo ao qual o recurso do modelo pode ser adaptado.</td>
  </tr>
 </tbody>
</table>

#### Segurança {#security}

**Autorizável**, **Usuário**, e **Grupo** adaptar a:

| [Nó](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Retorna o nó inicial do usuário/grupo. |
|---|---|
| [StatusReplicação](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/ReplicationStatus.html) | Retorna o status de replicação do nó inicial do usuário/grupo. |

#### DAM {#dam}

**Ativo** adapta-se a:

| [Recurso](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso do ativo. |
|---|---|
| [Nó](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó do ativo. |
| ... | Tudo ao qual o recurso do ativo pode ser adaptado. |

#### Marcação com tags {#tagging}

**Tag** adapta-se a:

| [Recurso](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso da tag. |
|---|---|
| [Nó](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó da tag. |
| ... | Tudo ao qual o recurso da tag pode ser adaptado. |

#### Outro {#other}

Além disso, o Sling/JCR/OCM também fornece uma [`AdapterFactory`](https://sling.apache.org/documentation/the-sling-engine/adapters.html) para OCM personalizado ([Mapeamento de conteúdo do objeto](https://jackrabbit.apache.org/jcr/object-content-mapping.html)) objetos.
