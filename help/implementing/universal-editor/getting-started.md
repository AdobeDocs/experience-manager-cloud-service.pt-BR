---
title: Introdução ao Editor universal no AEM
description: Saiba como obter acesso ao Universal Editor e como começar a instrumentar seu primeiro aplicativo AEM para usá-lo.
source-git-commit: 7389e20ba73e84c2320ea8a834b381f415ad3983
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# Introdução ao Editor universal no AEM {#getting-started}

Saiba como obter acesso ao Universal Editor e como começar a instrumentar seu primeiro aplicativo AEM para usá-lo.

>[!TIP]
>
>Se preferir mergulhar diretamente em um exemplo, é possível revisar a variável [Aplicativo de exemplo do editor universal no GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

## Etapas de integração {#onboarding}

Embora o Editor Universal possa editar conteúdo de qualquer fonte, este documento usará um aplicativo AEM como exemplo.

Há várias etapas para integrar seu aplicativo AEM e instrumentá-lo a usar o Editor Universal.

1. [Solicite acesso ao Editor Universal.](#request-access)
1. [Inclua a biblioteca principal do Editor universal.](#core-library)
1. [Adicione a configuração OSGi necessária.](#osgi-configurations)
1. [Instrumente a página.](#instrument-page)

Este documento guiará você por essas etapas.

## Solicitar acesso ao editor universal {#request-access}

Primeiro, é necessário solicitar acesso ao Editor Universal. Por favor, vá para [https://experience.adobe.com/#/aem/editor,](https://experience.adobe.com/#/aem/editor) faça logon e valide se você tiver acesso ao Editor Universal.

Caso não tenha acesso, ele poderá ser solicitado por meio de um formulário vinculado na mesma página.

![Solicitar acesso ao Editor Universal](assets/request-access.png)

Clique em **Solicitar acesso** O e um representante do Adobe revisarão sua solicitação e entrarão em contato para discutir seu caso de uso.

## Incluir a biblioteca principal do editor universal {#core-library}

Antes que seu aplicativo possa ser instrumentado para uso com o Editor universal, ele precisa incluir a seguinte dependência.

```javascript
@adobe/universal-editor-cors
```

Para ativar a instrumentação, a seguinte importação precisa ser adicionada a `index.js`.

```javascript
import "@adobe/universal-editor-cors";
```

### Alternativa para aplicativos não reativos {#alternative}

Se você não estiver implementando um aplicativo React e/ou exigir renderização do lado do servidor, um método alternativo é incluir o seguinte ao corpo do documento.

```html
<script src="https://cdn.jsdelivr.net/gh/adobe/universal-editor-cors/dist/universal-editor-embedded.js" async></script>
```

## Adicionar as configurações OSGi necessárias {#osgi-configurations}

Para poder editar AEM conteúdo com seu aplicativo usando o Editor Universal, as configurações de CORS e cookie devem ser feitas no AEM.

O seguinte [As configurações de OSGi devem ser definidas na instância de criação do AEM.](/help/implementing/deploying/configuring-osgi.md)

* `SameSite Cookies = None` em `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler`
* Remover X-FRAME-OPTIONS: Cabeçalho SAMEORIGIN em `org.apache.sling.engine.impl.SlingMainServlet`

### com.day.crx.security.token.impl.impl.TokenAuthenticationHandler {#samesite-cookies}

O cookie do token de logon deve ser enviado para o AEM como um domínio de terceiros. Portanto, o cookie do mesmo site deve ser definido explicitamente como `None`.

Essa propriedade deve ser definida na variável `com.day.crx.security.token.impl.impl.TokenAuthenticationHandler` Configuração do OSGi.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig"
          token.samesite.cookie.attr="None" />
```

### org.apache.sling.engine.impl.SlingMainServlet {#sameorigin}

X-Frame-Options: SAMEORIGIN impede a renderização AEM páginas dentro de um iframe. Remover o cabeçalho permite que as páginas sejam carregadas.

Essa propriedade deve ser definida na variável `org.apache.sling.engine.impl.SlingMainServlet` Configuração do OSGi.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
          xmlns:jcr="http://www.jcp.org/jcr/1.0"
          jcr:primaryType="sling:OsgiConfig"
          sling.additional.response.headers="[X-Content-Type-Options=nosniff]"/>
```

## Instruir a página {#instrument-page}

O serviço do Editor Universal requer um [nome de recurso uniforme (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) para identificar e utilizar o sistema de back-end correto para o conteúdo no aplicativo que está sendo editado. Portanto, um esquema URN é necessário para mapear o conteúdo de volta para os recursos de conteúdo.

Os atributos de instrumentação adicionados à página consistem principalmente de [HTML Microdata,](https://developer.mozilla.org/en-US/docs/Web/HTML/Microdata) um padrão do setor que também pode ser usado para tornar o HTML mais semântico, tornar documentos do HTML indexáveis etc.

### Criação de conexões {#connections}

As conexões usadas no aplicativo são armazenadas como `<meta>` nas tags do `<head>`.

```html
<meta name="urn:auecon:<referenceName>" content="<protocol>:<url>">
```

* `<referenceName>` - Este é um nome curto que é reutilizado no documento para identificar a conexão. Por exemplo `aemconnection`
* `<protocol>` - Isso indica qual plug-in de persistência do Universal Editor Persistence Service usar. Por exemplo `aem`
* `<url>` - Este é o URL do sistema no qual as alterações devem ser persistentes. Por exemplo `http://localhost:4502`

O identificador curto `auecon` significa Adobe Universal Editor Connection.

`itemid`s usará o `urn` para encurtar o identificador.

```html
itemid="urn:<referenceName>:<resource>"
```

* `<referenceName>` - Esta é a referência mencionada no `<meta>` . Por exemplo `aemconnection`
* `<resource>` - Este é um ponteiro para o recurso no sistema de destino. Por exemplo, um caminho de conteúdo AEM como `/content/page/jcr:content`

>[!TIP]
>
>Consulte o documento [Atributos e tipos](attributes-types.md) para obter mais detalhes sobre os atributos e tipos de dados exigidos pelo Editor Universal.

### Exemplo de conexão {#example}

```html
<html>
<head>
    <meta name="urn:auecon:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:auecon:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul itemscope itemid="urn:aemconnection:/content/example/list" itemtype="container">
            <li itemscope itemid="urn:aemconnection/content/example/listitem" itemtype="component">
              <p itemprop="name" itemtype="text">Jane Doe</p>
              <p itemprop="title" itemtype="text">Journalist</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
 
...
 
            <li itemscope itemid="urn:fcsconnection:/documents/mytext" itemtype="component">
              <p itemprop="name" itemtype="text">John Smith</p>
              <p itemid="urn:aemconnection/content/example/another-source" itemprop="title" itemtype="text">Photographer</p>
              <img itemprop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" itemtype="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

## Você está pronto para usar o editor universal {#youre-ready}

Seu aplicativo agora é instrumentado a usar o Editor universal!

Consulte o documento [Criação de conteúdo com o editor universal](authoring.md) para saber como é fácil e intuitivo para os autores de conteúdo criar conteúdo usando o Editor Universal.

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Universal Editor, consulte estes documentos.

* [Introdução ao Editor Universal](introduction.md) - Saiba como o Editor Universal permite editar qualquer aspecto de qualquer conteúdo em qualquer implementação para fornecer experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvedor de última geração.
* [Criação de conteúdo com o editor universal](authoring.md) - Saiba como é fácil e intuitivo para os autores de conteúdo criar conteúdo usando o Editor Universal.
* [Publicação de conteúdo com o editor universal](publishing.md) - Saiba como o Editor visual universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.
* [Arquitetura do editor universal](architecture.md) - Saiba mais sobre a arquitetura do Editor Universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](attributes-types.md) - Saiba mais sobre os atributos e tipos de dados exigidos pelo Editor Universal.
* [Autenticação do editor universal](authentication.md) - Saiba como o Editor Universal se autentica.
