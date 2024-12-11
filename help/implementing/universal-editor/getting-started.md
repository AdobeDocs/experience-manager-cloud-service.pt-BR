---
title: Introdução ao Editor universal no AEM
description: Saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
exl-id: 9091a29e-2deb-4de7-97ea-53ad29c7c44d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 8357caf2b0d396f6a1bd7b6160d6b48d8d6c026c
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 62%

---


# Introdução ao Editor universal no AEM {#getting-started}

Saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.

>[!TIP]
>
>Se preferir ir direto para o exemplo, você pode consultar o [aplicativo de demonstração do Editor universal no GitHub.](https://github.com/adobe/universal-editor-sample-editable-app)

Embora o Editor universal possa editar o conteúdo de qualquer fonte, este documento usará um aplicativo AEM como exemplo. Este documento o orientará por essas etapas.

## Instrumentar a página {#instrument-page}

O Editor universal exige uma biblioteca JavaScript para renderizar e editar a página no editor.

Além disso, o serviço do Editor Universal requer um [nome de recurso uniforme (URN)](https://en.wikipedia.org/wiki/Uniform_Resource_Name) para identificar e utilizar o sistema de back-end correto para o conteúdo no aplicativo que está sendo editado. Portanto, um esquema URN é necessário para mapear o conteúdo de volta para os recursos de conteúdo.

### Incluir a biblioteca CORS do editor universal {#cors-library}

Para que o Editor universal se conecte ao seu aplicativo, ele deve incluir a biblioteca CORS do Editor universal. Adicione o script a seguir ao aplicativo.

```html
 <script src="https://universal-editor-service.adobe.io/cors.js" async></script>
```

### Criação de conexões {#connections}

As conexões usadas no aplicativo são armazenadas como tags de `<meta>` no `<head>` da página.

```html
<meta name="urn:adobe:aue:<category>:<referenceName>" content="<protocol>:<url>">
```

* `<category>` - Esta é uma classificação da conexão com duas opções.
   * `system` - Para pontos de extremidade de conexão
   * `config` - Para [definindo configurações opcionais](#configuration-settings)
* `<referenceName>`: este é um nome curto que é reutilizado no documento para identificar a conexão. Por exemplo: `aemconnection`
* `<protocol>`: isso indica qual plug-in do serviço de persistência do Editor universal deve ser utilizado. Por exemplo: `aem`
* `<url>`: esta é a URL do sistema no qual as alterações devem ser mantidas. Por exemplo: `http://localhost:4502`

O identificador `urn:adobe:aue:system` representa a conexão do Editor universal da Adobe.

`data-aue-resource`s usarão o prefixo `urn` para encurtar o identificador.

```html
data-aue-resource="urn:<referenceName>:<resource>"
```

* `<referenceName>`: esta é a referência de nome mencionada na tag `<meta>`. Por exemplo: `aemconnection`
* `<resource>`: este é um indicador do recurso no sistema de destino. Por exemplo: um caminho de conteúdo do AEM, como `/content/page/jcr:content`

>[!TIP]
>
>Consulte o documento [Atributos e tipos](attributes-types.md) para obter mais detalhes sobre os atributos e tipos de dados exigidos pelo Editor universal.

### Exemplo de conexão {#example}

```html
<meta name="urn:adobe:aue:system:<referenceName>" content="<protocol>:<url>">

<html>
<head>
    <meta name="urn:adobe:aue:system:aemconnection" content="aem:https://localhost:4502">
    <meta name="urn:adobe:aue:system:fcsconnection" content="fcs:https://example.franklin.adobe.com/345fcdd">
</head>
<body>
        <aside>
          <ul data-aue-resource="urn:aemconnection:/content/example/list" data-aue-type="container">
            <li data-aue-resource="urn:aemconnection:/content/example/listitem" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">Jane Doe</p>
              <p data-aue-prop="title" data-aue-type="text">Journalist</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>

...

            <li data-aue-resource="urn:fcsconnection:/documents/mytext" data-aue-type="component">
              <p data-aue-prop="name" data-aue-type="text">John Smith</p>
              <p data-aue-resource="urn:aemconnection:/content/example/another-source" data-aue-prop="title" data-aue-type="text">Photographer</p>
              <img data-aue-prop="avatar" src="https://www.adobe.com/content/dam/cc/icons/Adobe_Corporate_Horizontal_Red_HEX.svg" data-aue-type="image" alt="avatar"/>
            </li>
          </ul>
        </aside>
</body>
</html>
```

### Definições de configuração {#configuration-settings}

Você pode usar o prefixo `config` no URN da conexão para definir pontos de extremidade de serviço e extensão, se necessário.

Se você não quiser usar o Universal Editor Service, que é hospedado pelo Adobe, mas sua própria versão hospedada, poderá defini-lo em uma meta tag. Para substituir o ponto de extremidade de serviço padrão fornecido pelo Editor Universal, defina seu próprio ponto de extremidade de serviço:

* Meta name - `urn:adobe:aue:config:service`
* Conteúdo meta - `content="https://adobe.com"` (exemplo)

```html
<meta name="urn:adobe:aue:config:service" content="<url>">
```

Se você quiser que apenas determinadas extensões sejam ativadas para uma página, poderá definir isso em uma meta tag. Para buscar extensões, defina os pontos de extremidade da extensão:

* Nome meta: `urn:adobe:aue:config:extensions`
* Conteúdo meta: `content="https://adobe.com,https://anotherone.com,https://onemore.com"` (exemplo)

```html
<meta name="urn:adobe:aue:config:extensions" content="<url>,<url>,<url>">
```

## Você está pronto para usar o Editor universal {#youre-ready}

Seu aplicativo agora está pronto para utilizar o Editor universal.

Consulte [Criação de conteúdo com o Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) para ver como é fácil e intuitivo criar conteúdo utilizando o Editor universal.

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Editor universal, consulte estes documentos.

* [Introdução ao Editor universal](introduction.md): saiba como o Editor universal permite editar qualquer aspecto do conteúdo das implementações, a fim de entregar experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvimento de última geração.
* [Criação de conteúdo com o Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md): saiba como é fácil e intuitivo para os autores criarem conteúdo usando o Editor universal.
* [Publicando Conteúdo com o Editor Universal](/help/sites-cloud/authoring/universal-editor/publishing.md) - Saiba como o Editor Universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.
* [Arquitetura do Editor universal](architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](attributes-types.md): saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
* [Autenticação do Editor universal](authentication.md): saiba como funciona a autenticação do Editor universal.

