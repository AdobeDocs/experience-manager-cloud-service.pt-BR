---
title: Introdução ao SPA no AEM usando React
description: Este artigo apresenta um aplicativo de amostra SPA, explica como ele é montado e permite que você entre em operação com seu próprio SPA rapidamente usando a estrutura React.
translation-type: tm+mt
source-git-commit: 8bdb7bbe80a4e22bb2b750c0719c6db745133392
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 1%

---


# Introdução ao SPA no AEM usando React {#getting-started-with-spas-in-aem-using-react}

Aplicativos de página única (SPA) podem oferta experiências interessantes para usuários de sites. Os desenvolvedores querem ser capazes de criar sites usando estruturas SPA e os autores querem editar o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação de SPA oferta uma solução abrangente para suportar SPA dentro do AEM. Este artigo apresenta um aplicativo de SPA simplificado na estrutura React, explica como ele é montado, permitindo que você se familiarize com seu próprio SPA rapidamente.

>[!NOTE]
>
>Este artigo baseia - se no quadro React. Para o documento correspondente da estrutura Angular, consulte [Introdução ao SPA em AEM - Angular](getting-started-angular.md).

## Introdução {#introduction}

Este artigo resume o funcionamento básico de uma SPA simples e o mínimo que você precisa saber para executar a sua.

Para obter mais detalhes sobre como SPA trabalhar em AEM, consulte os seguintes documentos:

* [Introdução SPA e Walkthrough](introduction.md)
* [Visão geral do editor de SPA](editor-overview.md)
* [SPA Blueprint](blueprint.md)

>[!NOTE]
>
>Para ser capaz de criar conteúdo dentro de um SPA, o conteúdo deve ser armazenado em AEM e exposto pelo modelo de conteúdo.
>
>Um SPA desenvolvido fora do AEM não será autorável se não respeitar o contrato do modelo de conteúdo.

Este documento passará pela estrutura de um SPA simplificado criado usando a estrutura React e ilustrará como funciona para que você possa aplicar essa compreensão ao seu próprio SPA.

## Dependências, configuração e criação {#dependencies-configuration-and-building}

Além da dependência esperada do React, o SPA de amostra pode aproveitar bibliotecas adicionais para tornar a criação do SPA mais eficiente.

### Dependências {#dependencies}

O `package.json` arquivo define os requisitos do pacote SPA geral. As dependências mínimas de AEM para um SPA ativo estão listadas aqui.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Como este exemplo é baseado na estrutura React, existem duas dependências React-specific que são obrigatórias no `package.json` arquivo:

```
 react
 react-dom
```

O recurso `aem-clientlib-generator` é utilizado para tornar a criação de bibliotecas de clientes automática como parte do processo de criação.

`"aem-clientlib-generator": "^1.4.1",`

Mais detalhes sobre o assunto podem ser encontrados [no GitHub aqui](https://github.com/wcm-io-frontend/aem-clientlib-generator).

O `aem-clientlib-generator` é configurado no `clientlib.config.js` arquivo da seguinte maneira.

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

### Criando {#building}

Na verdade, a criação do aplicativo aproveita o [Webpack](https://webpack.js.org/) para transpilação, além do gerador aem-clientlib para a criação automática da biblioteca do cliente. Portanto, o comando build será semelhante a:

`"build": "webpack && clientlib --verbose"`

Depois de criado, o pacote pode ser carregado para uma instância AEM.

### Arquétipo de projeto do AEM{#aem-project-archetype}

Qualquer projeto AEM deve aproveitar o [AEM Project Archetype](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html), que suporta projetos SPA usando React ou Angular e aproveita o SPA SDK.

## Estrutura do aplicativo {#application-structure}

A inclusão das dependências e a criação do aplicativo conforme descrito anteriormente o deixarão com um pacote SPA que pode ser carregado para a instância AEM.

A próxima seção deste documento o orientará sobre como um SPA em AEM é estruturado, os arquivos importantes que acionam o aplicativo e como eles trabalham juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo são baseados no mesmo conceito.

### index.js {#index-js}

O ponto de entrada no SPA é, claro, o `index.js` arquivo mostrado aqui simplificado para focar no conteúdo importante.

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

A função principal do é `index.js` alavancar a `ReactDOM.render` função para determinar onde o DOM deve injetar o aplicativo.

Este é um uso padrão desta função, não exclusivo para este aplicativo de exemplo.

#### Instanciação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o modelo de componente (por exemplo, JSX), o valor deve ser passado do modelo para as propriedades do componente.

### App.js {#app-js}

Ao renderizar o aplicativo, `index.js` as chamadas `App.js`, que são mostradas aqui em uma versão simplificada para focar no conteúdo importante.

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

Ao renderizar a página, `App.js` as chamadas `Page.js` listadas aqui em uma versão simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

Neste exemplo, a `AppPage` classe se estende `Page`, que contém os métodos de conteúdo interno que podem ser usados.

O `Page` assimila a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Para obter mais detalhes sobre o documento, consulte `Page` [SPA Blueprint.](blueprint.md)

### Image.js {#image-js}

Com a página renderizada, os componentes, como `Image.js` mostrado aqui, podem ser renderizados.

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

A ideia central do SPA em AEM é mapear componentes SPA para AEM componentes e atualizar o componente quando o conteúdo é modificado (e vice-versa). Consulte Visão geral [do editor de documentos](editor-overview.md) SPA para obter um resumo desse modelo de comunicação.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

O `MapTo` método mapeia o componente SPA para o componente AEM. Ele suporta o uso de uma única string ou de uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para ativar os recursos de criação de um componente, fornecendo os metadados necessários para o editor gerar espaços reservados

Se não houver conteúdo, os rótulos serão fornecidos como espaços reservados para representar o conteúdo vazio.

#### Propriedades aprovadas dinamicamente {#dynamically-passed-properties}

Os dados provenientes do modelo são transmitidos dinamicamente como propriedades do componente.

## Exportar conteúdo editável {#exporting-editable-content}

Você pode exportar um componente e mantê-lo editável.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

A `MapTo` função retorna um resultado `Component` que é o resultado de uma composição que estende o conteúdo fornecido `PageClass` com os nomes e atributos da classe que habilitam a criação. Esse componente pode ser exportado para ser instanciado posteriormente na marcação do aplicativo.

Quando exportado usando as funções `MapTo` ou `withModel` , o `Page` componente é encapsulado com um `ModelProvider` componente que fornece aos componentes padrão acesso à versão mais recente do modelo de página ou a um local preciso nesse modelo de página.

Para obter mais informações, consulte o documento [Blueprint](blueprint.md)SPA.

>[!NOTE]
>
>Por padrão, você recebe o modelo inteiro do componente ao usar a `withModel` função.

## Compartilhamento De Informações Entre SPA Componentes {#sharing-information-between-spa-components}

É necessário que os componentes de um aplicativo de página única compartilhem informações regularmente. Há várias maneiras recomendadas de fazer isso, listadas a seguir, para aumentar a ordem de complexidade.

* **Opção 1:** Centralize a lógica e transmita para os componentes necessários, por exemplo, usando Reagir contexto.
* **Opção 2:** Compartilhe estados de componentes usando uma biblioteca de estados como Redux.
* **Opção 3:** Aproveite a hierarquia de objetos personalizando e estendendo o componente de container.

## Próximas etapas {#next-steps}

* [A Introdução ao SPA no AEM usando o Angular](getting-started-angular.md) mostra como um SPA básico foi criado para funcionar com o Editor SPA no AEM usando o Angular.
* [SPA Visão geral](editor-overview.md) do editor aprofunda o modelo de comunicação entre AEM e o SPA.
* [SPA Projeto](wknd-tutorial.md) WKND é um tutorial passo a passo que implementa um projeto SPA simples em AEM.
* [O Modelo dinâmico para mapeamento de componentes para SPA](model-to-component-mapping.md) explica o modelo dinâmico para mapeamento de componentes e como ele funciona dentro do SPA em AEM.
* [SPA Blueprint](blueprint.md) oferta um aprofundamento sobre como o SDK SPA para AEM funciona caso você deseje implementar SPA em AEM para uma estrutura diferente de React ou Angular ou simplesmente deseje um entendimento mais profundo.
