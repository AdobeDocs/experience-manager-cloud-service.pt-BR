---
title: Introdução ao SPA no AEM usando o React
description: Este artigo apresenta uma amostra de aplicativo SPA, explica como ele é montado e permite que você comece a usar seu próprio SPA rapidamente usando a estrutura do React.
exl-id: 13998526-65e7-4d1b-bd47-452bad3780a2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 6%

---

# Introdução ao SPA no AEM usando o React {#getting-started-with-spas-in-aem-using-react}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas SPA, e os autores desejam editar o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação do SPA oferece uma solução abrangente para oferecer suporte ao SPA no AEM. Este artigo apresenta um aplicativo simplificado para SPA na estrutura do React, explica como ele é montado, permitindo que você comece a usar seu próprio SPA rapidamente.

>[!NOTE]
>
>Este artigo baseia-se no quadro do React. Para o documento correspondente para a estrutura do Angular, consulte [Introdução ao SPA no AEM - Angular](getting-started-angular.md).

## Introdução {#introduction}

Este artigo resume o funcionamento básico de um SPA simples e o mínimo que você precisa saber para que o seu funcione.

Para obter mais detalhes sobre como o SPA funciona no AEM, consulte os seguintes documentos:

* [Introdução e passo a passo do SPA](introduction.md)
* [Visão geral do editor de SPA](editor-overview.md)
* [Blueprint do SPA](blueprint.md)

>[!NOTE]
>
>Para ser capaz de criar conteúdo dentro de um SPA, o conteúdo deve ser armazenado no AEM e ser exposto pelo modelo de conteúdo.
>
>Um SPA desenvolvido fora do AEM não será autorável se não respeitar o contrato do modelo de conteúdo.

Este documento abordará a estrutura de um SPA simplificado criado usando a estrutura do React e ilustrará como ele funciona para que você possa aplicar essa compreensão ao seu próprio SPA.

## Dependências, configuração e criação {#dependencies-configuration-and-building}

Além da dependência esperada do React, o SPA de amostra pode usar bibliotecas adicionais para tornar a criação do SPA mais eficiente.

### Dependências {#dependencies}

O arquivo `package.json` define os requisitos do pacote SPA geral. As dependências mínimas do AEM para um SPA em funcionamento estão listadas aqui.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Como este exemplo é baseado na estrutura do React, há duas dependências específicas do React que são obrigatórias no arquivo `package.json`:

```
 react
 react-dom
```

O `aem-clientlib-generator` é usado para tornar a criação de bibliotecas de clientes automática como parte do processo de compilação.

`"aem-clientlib-generator": "^1.4.1",`

Para obter mais detalhes, consulte [aem-clientlib-generator no GitHub](https://github.com/wcm-io-frontend/aem-clientlib-generator).

O `aem-clientlib-generator` está configurado no arquivo `clientlib.config.js` da seguinte maneira.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Compilação {#building}

Na verdade, a compilação do aplicativo usa o [Webpack](https://webpack.js.org/) para transpilação, além do aem-clientlib-generator para a criação automática da biblioteca do cliente. Portanto, o comando build será semelhante a:

`"build": "webpack && clientlib --verbose"`

Depois de criado, o pacote pode ser carregado para uma instância AEM.

### Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou o Angular e utiliza o SDK de SPA.

## Estrutura do aplicativo {#application-structure}

Incluir as dependências e criar seu aplicativo conforme descrito anteriormente deixará você com um pacote de SPA que funciona e que você pode carregar para sua instância do AEM.

A próxima seção deste documento abordará como um SPA no AEM é estruturado, os arquivos importantes que orientam o aplicativo e como eles funcionam juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo se baseiam no mesmo conceito.

### index.js {#index-js}

O ponto de entrada no SPA é o arquivo `index.js` mostrado aqui simplificado para se concentrar no conteúdo importante.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

A função principal de `index.js` é usar a função `ReactDOM.render` para determinar onde no DOM inserir o aplicativo.

Este é um uso padrão dessa função, não exclusivo deste aplicativo de exemplo.

#### Instanciação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o template do componente (por exemplo, JSX), o valor deve ser passado do modelo para as propriedades do componente.

### App.js {#app-js}

Renderizando o aplicativo, `index.js` chama `App.js`, que é mostrado aqui em uma versão simplificada para se concentrar no conteúdo importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` serve principalmente para envolver os componentes raiz que compõem o aplicativo. O ponto de entrada de qualquer aplicativo é a página.

### Page.js {#page-js}

Ao renderizar a página, o `App.js` chama o `Page.js` listado aqui em uma versão simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

Neste exemplo, a classe `AppPage` estende `Page`, que contém os métodos de conteúdo interno que podem ser usados.

O `Page` assimila a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Mais detalhes sobre o `Page` podem ser encontrados no documento [Blueprint do SPA.](blueprint.md)

### Image.js {#image-js}

Com a página renderizada, os componentes como o `Image.js`, como mostrado aqui, podem ser renderizados.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

A ideia central do AEM é a ideia de mapear componentes do SPA AEM para componentes do SPA e atualizar o componente quando o conteúdo é modificado (e vice-versa). Consulte o documento [Visão geral do editor de SPA](editor-overview.md) para obter um resumo desse modelo de comunicação.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

O método `MapTo` mapeia o componente SPA para o componente AEM. Ele suporta o uso de uma única string ou uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para habilitar os recursos de criação de um componente, fornecendo os metadados necessários para que o editor gere espaços reservados

Se não houver conteúdo, os rótulos serão fornecidos como espaços reservados para representar o conteúdo vazio.

#### Propriedades passadas dinamicamente {#dynamically-passed-properties}

Os dados provenientes do modelo são transmitidos dinamicamente como propriedades do componente.

## Exportar conteúdo editável {#exporting-editable-content}

É possível exportar um componente e mantê-lo editável.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

A função `MapTo` retorna um `Component` que é o resultado de uma composição que estende o `PageClass` fornecido com os nomes e atributos de classe que habilitam a criação. Esse componente pode ser exportado para ser instanciado posteriormente na marcação do aplicativo.

Quando exportado usando as funções `MapTo` ou `withModel`, o componente `Page` é encapsulado com um componente `ModelProvider` que fornece aos componentes padrão acesso à versão mais recente do modelo de página ou a um local preciso nesse modelo de página.

Para obter mais informações, consulte o [documento do blueprint do SPA](blueprint.md).

>[!NOTE]
>
>Por padrão, você recebe o modelo inteiro do componente ao usar a função `withModel`.

## Compartilhamento de informações entre componentes do SPA {#sharing-information-between-spa-components}

É regularmente necessário que os componentes de um aplicativo de página única compartilhem informações. Há várias maneiras recomendadas de fazer isso, listadas a seguir em uma ordem crescente de complexidade.

* **Opção 1:** Centralize a lógica e a difusão nos componentes necessários, por exemplo, usando o Contexto React.
* **Opção 2:** Compartilhe estados do componente usando uma biblioteca de estado como Redux.
* **Opção 3:** Aproveite a hierarquia de objetos personalizando e estendendo o componente de contêiner.

## Próximas etapas {#next-steps}

* [Introdução ao SPA no AEM usando o Angular](getting-started-angular.md) mostra como um SPA básico é criado para funcionar com o editor de no SPA AEM usando o Angular.
* A [Visão geral do editor de SPA](editor-overview.md) aborda em detalhes o modelo de comunicação do AEM e do SPA.
* O [Projeto WKND SPA](wknd-tutorial.md) é um tutorial passo a passo para a implementação de um projeto SPA simples no AEM.
* [Modelo dinâmico para mapeamento de componentes para SPA](model-to-component-mapping.md) explica o modelo dinâmico para mapeamento de componentes e como ele funciona dentro do SPA no AEM.
* O [Blueprint do SPA](blueprint.md) oferece um aprofundamento sobre como o SDK do SPA para AEM funciona caso você queira implementar o SPA AEM no para uma estrutura diferente do React ou do Angular ou simplesmente deseja obter um entendimento mais profundo.
