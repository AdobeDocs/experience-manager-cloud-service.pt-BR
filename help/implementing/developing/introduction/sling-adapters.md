---
title: Uso de adaptadores Sling
description: Como deslizar o oferta e o padrão do adaptador para converter convenientemente objetos que implementam a interface adaptável
translation-type: tm+mt
source-git-commit: 639bf1add463c0e62982a44ecdca834e2c7c53fe
workflow-type: tm+mt
source-wordcount: '2234'
ht-degree: 1%

---


# Uso de adaptadores Sling {#using-sling-adapters}

[O ](https://sling.apache.org) Slingues oferece um padrão  [de adaptador ](https://sling.apache.org/site/adapters.html) para converter convenientemente objetos que implementam a interface  [](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) adaptável. Esta interface fornece um método genérico [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) que irá traduzir o objeto para o tipo de classe que está sendo transmitido como argumento.

Por exemplo, para traduzir um objeto de Recurso para o objeto Nó correspondente, basta fazer o seguinte:

```java
Node node = resource.adaptTo(Node.class);
```

## Casos de uso {#use-cases}

Há os seguintes casos de uso:

* Obtenha objetos específicos da implementação.

   Por exemplo, uma implementação baseada em JCR da interface genérica [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) fornece acesso ao JCR subjacente [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Criação de atalhos de objetos que exigem a transmissão de objetos de contexto internos.

   Por exemplo, o JCR baseado em [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) contém uma referência para o [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html) da solicitação, que por sua vez é necessário para muitos objetos que funcionarão com base nessa sessão de solicitação, como [`PageManager`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html) ou [`UserManager`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/security/UserManager.html).

* Atalho para serviços.

   Um caso raro - `sling.getService()` também é simples.

### Valor de Retorno Nulo {#null-return-value}

`adaptTo()` pode retornar nulo.

Há várias razões para isso, incluindo:

* a implementação não suporta o tipo de público alvo
* um adaptador de fábrica que manuseia este caso não está ativo (por exemplo, devido a referências de serviço ausentes)
* falha na condição interna
* serviço não está disponível

É importante que você manipule a caixa nula com cuidado. Para renderizações jsp, pode ser aceitável que o jsp falhe se isso resultar em um conteúdo vazio.

### Cache {#caching}

Para melhorar o desempenho, as implementações podem armazenar em cache o objeto retornado de uma chamada `obj.adaptTo()`. Se `obj` for o mesmo, o objeto retornado será o mesmo.

Esse cache é executado para todos os casos baseados em `AdapterFactory`.

No entanto, não há regra geral - o objeto pode ser uma nova instância ou uma existente. Isso significa que você não pode confiar em nenhum dos comportamentos. Portanto, é importante, especialmente dentro de `AdapterFactory`, que os objetos sejam reutilizáveis neste cenário.

### Como funciona {#how-it-works}

Há várias maneiras de `Adaptable.adaptTo()` ser implementado:

* Pelo próprio objeto; implementação do próprio método e mapeamento para certos objetos.
* Por um [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), que pode mapear objetos arbitrários.

   Os objetos ainda devem implementar a interface `Adaptable` e devem estender [`SlingAdaptable`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/adapter/SlingAdaptable.html) (que passa a chamada `adaptTo` para um gerenciador central de adaptadores).

   Isso permite que os ganchos sejam inseridos no mecanismo `adaptTo` para classes existentes, como `Resource`.

* Uma combinação de ambos.

No primeiro caso, os javadocs podem indicar o que `adaptTo-targets` são possíveis. No entanto, para subclasses específicas, como o recurso baseado no JCR, isso geralmente não é possível. No último caso, as implementações de `AdapterFactory` são normalmente parte das classes privadas de um pacote e, portanto, não são expostas em uma API de cliente, nem listadas em javadocs. Teoricamente, seria possível acessar todas as implementações `AdapterFactory` do [OSGi](/help/implementing/deploying/configuring-osgi.md) tempo de execução do serviço e verificar suas configurações &quot;adaptáveis&quot; (fontes e públicos alvos), mas não mapeá-las umas às outras. Afinal, isso depende da lógica interna, que deve ser documentada. Daí essa referência.

## Referência {#reference}

### Sling {#sling}

[**O**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) recurso adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Se for um recurso baseado em nó JCR ou uma propriedade JCR que faça referência a um nó.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Propriedade</a></td>
   <td>Se este for um recurso baseado em propriedade do JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Item</a></td>
   <td>Se for um recurso baseado em JCR (nó ou propriedade).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Mapa</a></td>
   <td>Retorna um mapa das propriedades, se este for um recurso baseado em nós JCR (ou outros mapas de valor de suporte de recursos).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Retorna um mapa conveniente das propriedades, se for um recurso baseado em nós JCR (ou outros mapas de valor de suporte de recursos). Também pode ser obtido (mais simplesmente) usando<br /> <code><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> (lida com letras maiúsculas e minúsculas, etc.).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>Extensão de <a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> que permite que a hierarquia de recursos seja considerada ao procurar propriedades.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModificávelValueMap</a></td>
   <td>Uma extensão do <a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>, que permite modificar as propriedades nesse nó.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Retorna o conteúdo binário de um recurso de arquivo (se for um recurso baseado em nó JCR e o tipo de nó for <code>nt:file</code> ou <code>nt:resource</code>; se este for um recurso de conjunto; conteúdo de arquivo, se for um recurso do sistema de arquivos) ou os dados de um recurso de propriedade JCR binária.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Retorna um URL para o recurso (URL do repositório desse nó se for um recurso baseado em nó JCR; URL do pacote jar se este for um recurso de conjunto; URL do arquivo, se for um recurso do sistema de arquivos).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/File.html">Arquivo</a></td>
   <td>Se este for um recurso do sistema de arquivos.</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Se esse recurso for um script (por exemplo, arquivo jsp) para o qual um mecanismo de script está registrado com sling.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/products/servlet/2.2/javadoc/javax/servlet/Servlet.html">Servlet</a></td>
   <td>Se esse recurso for um script (por exemplo, arquivo jsp) para o qual um mecanismo de script está registrado com sling ou se for um recurso de servlet.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Double.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html"></a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html"></a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/String.html">StringBooleanLongDoubleCalendarValueString[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://java.sun.com/j2se/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>Retorna os valores se este for um recurso baseado em propriedade JCR (e o valor se ajustar).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Se este for um recurso baseado em nó JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Page.html">Página</a></td>
   <td>Se este for um recurso baseado em nó JCR e o nó for <code>cq:Page</code> (ou <code>cq:PseudoPage</code>).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/components/Component.html">Componente</a></td>
   <td>Se este for um recurso de nó <code>cq:Component</code>.</td>
  </tr>  
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/designer/Design.html">Design</a></td>
   <td>Se este for um nó de design (<code>cq:Page</code>).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Template.html">Modelo</a></td>
   <td>Se este for um recurso de nó <code>cq:Template</code>.</td>
  </tr>  
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>Se este for um recurso de nó <code>cq:Template</code>.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/dam/api/Asset.html">Ativo</a></td>
   <td>Se este for um recurso de nó dam:Asset.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/dam/api/Rendition.html">Representação</a></td>
   <td>Se for um dam:representação de ativo (nt:file na pasta de renderização de um dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/Tag.html">Tag</a></td>
   <td>Se este for um recurso de nó <code>cq:Tag</code>.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Com base na sessão do JCR se este for um recurso baseado em JCR e o usuário tiver permissões para acessar o UserManager.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizável</a></td>
   <td>A opção Autorizável é a interface base comum para Usuário e Grupo.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuário</a></td>
   <td>O usuário é um Autorizável especial que pode ser autenticado e representado.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>Pesquisa abaixo do recurso (ou use setSearchIn()) se este for um recurso baseado em JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Status do fluxo de trabalho para o nó de carga de página/fluxo de trabalho especificado.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>Status de replicação para o recurso fornecido ou seu subnó jcr:content (marcado primeiro).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Retorna um recurso de conector adaptado para certos tipos, se for um recurso baseado em nó JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/contentsync/config/package-summary.html">Configuração</a></td>
   <td>Se este for um recurso de nó <code>cq:ContentSyncConfig</code>.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Se estiver abaixo de um recurso de nó <code>cq:ContentSyncConfig</code>.</td>
  </tr>
 </tbody>
</table>

[**O**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/ResourceResolver.html) ResourceResolveradapts para:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Sessão</a></td>
   <td>A sessão JCR da solicitação, se for um resolvedor de recursos baseado em JCR (padrão).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>Com base na sessão do JCR, se for um resolvedor de recursos baseado em JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>Com base na sessão do JCR, se for um resolvedor de recursos baseado em JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>O UserManager fornece acesso e meios para manter objetos autorizados, ou seja, usuários e grupos. O UserManager está vinculado a uma sessão específica.
   </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizável</a> </td>
   <td>O usuário atual.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuário</a><br /> </td>
   <td>O usuário atual.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html">Externalizador</a></td>
   <td>Para externalizar URLs absolutos, mesmo sem o objeto de solicitação.<br /> </td>
  </tr>
 </tbody>
</table>

[**O**](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/SlingHttpServletRequest.html) SlingHttpServletRequestadapta-se a:

Nenhum público alvo ainda, mas implementa Adaptável e pode ser usado como fonte em um AdapterFactory personalizado.

[****](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/SlingHttpServletResponse.html) SlingHttpServletResponseadapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>Se isso for uma resposta de um sling rewriter.</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[A ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Page.html)** página adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><br /> </td>
   <td>Recurso da página.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Recurso rotulado (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Nó da página.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tudo ao qual o recurso da página pode ser adaptado.</td>
  </tr>
 </tbody>
</table>

**[Os ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/components/Component.html)** componentes se adaptam a:

| [Recurso](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) | Recurso do componente. |
|---|---|
| [LabeledResource](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html) | Recurso rotulado (== this). |
| [Nó](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó do componente. |
| ... | Tudo ao qual o recurso do componente pode ser adaptado. |

**[O ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/Template.html)** modelo adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Recurso do modelo.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>Recurso rotulado (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Nó deste modelo.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tudo ao qual o recurso do modelo pode ser adaptado.</td>
  </tr>
 </tbody>
</table>

#### Segurança {#security}

**Autorizável**,  **** Utilizador e  **** Grupo

| [Nó](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Retorna o nó inicial do usuário/grupo. |
|---|---|
| [ReplicationStatus](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/replication/ReplicationStatus.html) | Retorna o status de replicação do nó inicial do usuário/grupo. |

#### DAM {#dam}

**Os** ativos se adaptam a:

| [Recurso](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) | Recurso do ativo. |
|---|---|
| [Nó](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó do ativo. |
| ... | Tudo ao qual o recurso do ativo pode ser adaptado. |

#### Marcação com tags {#tagging}

**As** tags adaptam-se a:

| [Recurso](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/org/apache/sling/api/resource/Resource.html) | Recurso da tag . |
|---|---|
| [Nó](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó da tag . |
| ... | Tudo ao qual o recurso da tag pode ser adaptado. |

#### Outro {#other}

Além disso, Sling / JCR / COM também fornece [`AdapterFactory`](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory) para objetos MAC personalizados ([Mapeamento de conteúdo de objeto](https://jackrabbit.apache.org/object-content-mapping.html)).
