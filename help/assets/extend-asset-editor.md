---
title: Extensão do editor de ativos
description: Saiba como estender os recursos do editor de ativos usando componentes personalizados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Extensão do Editor de ativos {#extending-asset-editor}

O Editor de ativos é a página que é aberta quando um ativo encontrado por meio do Compartilhamento de ativos é clicado, permitindo que o usuário edite esses aspectos do ativo como metadados, miniatura, título e tags.

A configuração do editor usando os componentes de edição predefinidos é abordada em [Criar e configurar uma página](https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-finder-editor.html)do editor de ativos.

Além de usar componentes de editor pré-existentes, os desenvolvedores do Adobe Experience Manager (AEM) também podem criar seus próprios componentes.

## Criando um modelo do editor de ativos {#creating-an-asset-editor-template}

As seguintes páginas de amostra estão incluídas no geometrixx:

* Página de amostra do Geometrixx: `/content/geometrixx/en/press/asseteditor.html`
* Modelo de amostra: `/apps/geometrixx/templates/asseteditor`
* Componente de página de amostra: `/apps/geometrixx/components/asseteditor`

### Configuração do Clientlib {#configuring-clientlib}

Os componentes do AEM Assets usam uma extensão da clientlib de edição do WCM. Os clientlibs normalmente são carregados em `init.jsp`.

Comparado ao carregamento padrão do clientlib (nos principais `init.jsp`), um modelo do AEM Assets deve ter o seguinte:

* O modelo deve incluir a `cq.dam.edit` clientlib (em vez de `cq.wcm.edit`).

* A clientlib também deve ser incluída no modo WCM desativado (por exemplo, carregado na **publicação**) para poder renderizar os predicados, as ações e as lentes.

Na maioria dos casos, copiar a amostra existente `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) deve atender a essas necessidades.

### Configuração de ações JS {#configuring-js-actions}

Alguns componentes do AEM Assets exigem funções JS definidas em `component.js`. Copie esse arquivo para o diretório do componente e vincule-o.

```xml
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

A amostra carrega essa fonte javascript em `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### Folhas de estilos adicionais {#additional-style-sheets}

Alguns componentes do AEM Assets usam a biblioteca de widgets do AEM. Para ser renderizada corretamente no contexto do conteúdo, uma folha de estilos adicional deve ser carregada. O componente de ação de tag requer mais um.

```xml
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Folha de estilo do Geometrixx {#geometrixx-style-sheet}

Os componentes da página de amostra exigem que todos os seletores comecem com `.asseteditor` ( `static.css``/etc/designs/geometrixx/static.css`). Melhores práticas: Copie todos os `.asseteditor` seletores para sua folha de estilos e ajuste as regras conforme desejado.

### FormChooser: Ajustes para recursos eventualmente carregados {#formchooser-adjustments-for-eventually-loaded-resources}

O Editor de ativos usa o Seletor de formulários, que permite editar recursos - neste caso, ativos - na mesma página de formulário simplesmente adicionando um seletor de formulário e o caminho do formulário ao URL do ativo.

Por exemplo:

* Página de formulário simples: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* Ativo carregado na página do formulário: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

As alças da amostra em `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) fazem o seguinte:

* Eles detectam se um ativo é carregado ou se o formulário simples precisa ser exibido.
* Se um ativo for carregado, ele desativará o modo WCM como parsys só poderá ser editado em uma página de formulário simples.
* Se um ativo for carregado, ele usará seu título em vez do título na página do formulário.

```java
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

Na parte HTML, use o conjunto de título anterior (ativo ou título de página):

```xml
<title><%= title %></title>
```

## Criação de um componente de campo de formulário simples {#creating-a-simple-form-field-component}

Este exemplo descreve como criar um componente que mostra e exibe os metadados de um ativo carregado.

1. Crie uma pasta de componentes no diretório de projetos, por exemplo, `/apps/geometrixx/components/samplemeta`.
1. Adicione `content.xml` o seguinte snippet:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. Adicione `samplemeta.jsp` o seguinte snippet:

   ```xml
   <%--
   
     Sample metadata field comopnent
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource will be the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. Para disponibilizar o componente, é necessário editá-lo. Para tornar um componente editável, no CRXDE Lite, adicione um nó `cq:editConfig` do tipo primário `cq:EditConfig`. Para que você possa remover parágrafos, adicione uma propriedade de vários valores `cq:actions` com um único valor de `DELETE`.

1. Navegue até o navegador e, na sua página de amostra (por exemplo, `asseteditor.html`) mude para o modo de design e ative o novo componente para o sistema de parágrafo.

1. No modo **Editar** , o novo componente (por exemplo, Metadados **de** amostra) agora está disponível no sidekick (encontrado no grupo Editor **de** ativos). Insira o componente. Para poder armazenar os metadados, eles devem ser adicionados ao formulário de metadados.

## Modificando opções de metadados {#modifying-metadata-options}

É possível modificar os namespaces disponíveis no formulário [de](https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-finder-editor.html)metadados.

Os metadados atualmente disponíveis são definidos em `/libs/dam/options/metadata`:

* O primeiro nível dentro deste diretório contém os namespaces.
* Os itens dentro de cada namespace representam metadados, como resultados em um item de peça local.
* O conteúdo de metadados contém as informações para o tipo e as opções de vários valores.

As opções podem ser substituídas em `/apps/dam/options/metadata`:

1. Copie o diretório de `/libs` para `/apps`.

1. Remover, modificar ou adicionar itens.

>[!NOTE]
>
>Se você adicionar novos namespaces, eles deverão estar registrados no repositório/CRX. Caso contrário, o envio do formulário de metadados resultará em um erro.
