---
title: Estender opções de pesquisa e recursos nos ativos Adobe Experience Manager
description: Estenda os recursos de pesquisa dos Ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Estender pesquisa de ativos {#extend-assets-search}

Você pode estender os recursos de pesquisa dos ativos Adobe Experience Manager (AEM). Os ativos AEM pesquisam ativos por sequências de caracteres.

A pesquisa é feita pela interface do QueryBuilder para que a pesquisa possa ser personalizada com vários predicados. Você pode sobrepor o conjunto padrão de predicados no seguinte diretório: `/apps/dam/content/search/searchpanel/facets`.

Você também pode adicionar outras guias ao painel de administração do AEM Assets.

## Sobreposição {#overlay}

Para sobrepor os predicados pré-configurados, copie o `facets` nó `/libs/dam/content/search/searchpanel` para `/apps/dam/content/search/searchpanel/` ou especifique outra `facetURL` propriedade na configuração do painel de pesquisa (o padrão é para `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

>[!NOTE]
>
>Por padrão, a estrutura de diretório em `/apps` não existe e precisa ser criada. Certifique-se de que os tipos de nó correspondam aos em `/libs`.

### Adicionar guias {#add-tabs}

É possível adicionar guias de pesquisa adicionais configurando-as no Admin do AEM Assets. Para criar guias adicionais:

1. Crie a estrutura de pastas `/apps/wcm/core/content/damadmin/tabs,`se ela ainda não existir e copie o `tabs` nó de `/libs/wcm/core/content/damadmin` e cole-o.
1. Crie e configure a segunda guia, conforme desejado.

   >[!NOTE]
   >
   >Ao criar um segundo `siteadminsearchpanel`, certifique-se de definir uma `id` propriedade para evitar conflitos de formulário.

### Criar predicados personalizados {#create-custom-predicates}

Os ativos AEM vêm com um conjunto de predicados predefinidos que podem ser usados para personalizar uma página de compartilhamento de ativos.
<!-- In addition to using pre-existing predicates, AEM developers can also create their own predicates using the [Query Builder API](/help/sites-developing/querybuilder-api.md). -->

A criação de predicados personalizados requer conhecimento básico sobre a estrutura [de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)Widgets.

A prática recomendada é copiar um predicado existente e ajustá-lo. Os predicados de amostra estão localizados em **/libs/cq/search/components/predicados**.

#### Exemplo: Criar um predicado de propriedade simples {#example-build-a-simple-property-predicate}

Para criar um predicado de propriedade:

1. Crie uma pasta de componentes no diretório de projetos, por exemplo **/apps/geometrixx/components/titlepredicate**.
1. Adicionar **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Adicionar `titlepredicate.jsp`.

   ```xml
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. Para disponibilizar o componente, é necessário editá-lo. Para tornar um componente editável, no CRXDE, adicione um nó **cq:editConfig** do tipo primário **cq:EditConfig**. Para que você possa remover parágrafos, adicione uma propriedade de vários valores **cq:actions** com um único valor de **DELETE**.
1. Navegue até o navegador e, na página de amostra (por exemplo, **press.html**), alterne para o modo de design e ative o novo componente para o sistema de parágrafo de previsão (por exemplo, **esquerda**).

1. No modo **Editar** , o novo componente agora está disponível no sidekick (encontrado no grupo **Pesquisar** ). Insira o componente na coluna **Predicados** e digite uma palavra de pesquisa, por exemplo, **Diamante** , e clique na lupa para iniciar a pesquisa.

   >[!NOTE]
   >
   >Ao pesquisar, digite exatamente o termo, incluindo as letras maiúsculas e minúsculas corretas.

#### Exemplo: Criar um predicado de grupo simples {#example-build-a-simple-group-predicate}

Para criar um predicado de grupo:

1. Crie uma pasta de componentes no diretório de projetos, por exemplo **/apps/geometrixx/components/picspredicate.**
1. Adicionar **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Adicione **titlepredicate.jsp**:

   ```xml
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. Para disponibilizar o componente, é necessário editá-lo. Para tornar um componente editável, no CRXDE, adicione um nó **cq:editConfig** do tipo primário **cq:EditConfig**. Para que você possa remover parágrafos, adicione uma propriedade de vários valores **cq:actions** com um único valor de **DELETE**.
1. Navegue até o navegador e, na página de amostra (por exemplo, **press.html**), alterne para o modo de design e ative o novo componente para o sistema de parágrafo de previsão (por exemplo, **esquerda**).
1. No modo **Editar** , o novo componente agora está disponível no sidekick (encontrado no grupo **Pesquisar** ). Insira o componente na coluna **Predicados** .

### Widgets preditivos instalados {#installed-predicate-widgets}

Os seguintes predicados estão disponíveis como widgets ExtJS pré-configurados.

#### PredicadoTexto completo {#fulltextpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Sequência de caracteres</td>
   <td>Nome do predicado. O padrão é 'fulltext'</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Função</td>
   <td>Retorno de chamada para acionar a pesquisa no evento "keyup". Padrão para 'CQ.wcm.SiteAdmin.doSearch'</td>
  </tr>
 </tbody>
</table>

#### PropertyPredicate {#propertypredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Sequência de caracteres</td>
   <td>Nome do predicado. O padrão é 'property'</td>
  </tr>
  <tr>
   <td>propertyName</td>
   <td>Sequência de caracteres </td>
   <td>Nome da propriedade JCR. Padrão para 'jcr:title'</td>
  </tr>
  <tr>
   <td>defaultValue<br /> </td>
   <td>Sequência de caracteres<br /> </td>
   <td>Valor padrão pré-preenchido.<br /> </td>
  </tr>
 </tbody>
</table>

#### PathPredicate {#pathpredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Sequência de caracteres</td>
   <td>Nome do predicado. O padrão é 'path'</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Sequência de caracteres </td>
   <td>Caminho raiz do predicado. Padrão para '/content/dam'</td>
  </tr>
  <tr>
   <td>pathFieldPredicateName</td>
   <td>Sequência de caracteres</td>
   <td>Padrão para "pasta"</td>
  </tr>
  <tr>
   <td>showFlatOption</td>
   <td>Booleano</td>
   <td>Sinalizador para mostrar a caixa de seleção 'pesquisar em subpastas'. O padrão é true.</td>
  </tr>
 </tbody>
</table>

#### DatePredicate {#datepredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Sequência de caracteres</td>
   <td>Nome do predicado. O padrão é 'daterange'</td>
  </tr>
  <tr>
   <td>propertyname</td>
   <td>Sequência de caracteres</td>
   <td>Nome da propriedade JCR. Padrão para 'jcr:content/jcr:lastModified'</td>
  </tr>
  <tr>
   <td>defaultValue </td>
   <td>Sequência de caracteres </td>
   <td>Valor padrão pré-preenchido </td>
  </tr>
 </tbody>
</table>

#### OpçõesPredicado {#optionspredicate}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade<br /> </strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>título </td>
   <td>Sequência de caracteres </td>
   <td>Adiciona um título superior adicional </td>
  </tr>
  <tr>
   <td>predicateName</td>
   <td>Sequência de caracteres</td>
   <td>Nome do predicado. O padrão é 'daterange'</td>
  </tr>
  <tr>
   <td>propertyname</td>
   <td>Sequência de caracteres</td>
   <td>Nome da propriedade JCR. Padrão para 'jcr:content/metadata/cq:tags'</td>
  </tr>
  <tr>
   <td>colapso</td>
   <td>Sequência de caracteres</td>
   <td>Reduzir nível. O padrão é 'level1'</td>
  </tr>
  <tr>
   <td>triggerSearch</td>
   <td>Booleano </td>
   <td>Sinalizador para acionar a pesquisa na verificação. O padrão é false</td>
  </tr>
  <tr>
   <td>searchCallback</td>
   <td>Função</td>
   <td>Retorno de chamada para acionar a pesquisa. O padrão é 'CQ.wcm.SiteAdmin.doSearch'</td>
  </tr>
  <tr>
   <td>searchTimeoutTime</td>
   <td>Número</td>
   <td>Tempo limite antes de o searchCallback ser disparado. O padrão é 800 ms</td>
  </tr>
 </tbody>
</table>
