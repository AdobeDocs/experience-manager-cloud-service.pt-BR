---
title: Introdução ao SPA no AEM usando o Angular
description: Este artigo apresenta uma amostra de aplicativo SPA, explica como ele é montado e permite que você comece a usar seu próprio SPA rapidamente usando a estrutura do Angular.
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 6%

---

# Introdução ao SPA no AEM usando o Angular {#getting-started-with-spas-in-aem-using-angular}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas SPA, e os autores desejam editar o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação do SPA oferece uma solução abrangente para oferecer suporte ao SPA no AEM. Este artigo apresenta um aplicativo simplificado de SPA na estrutura do Angular e explica como ele é montado, permitindo que você comece a usar seu próprio SPA rapidamente.

>[!NOTE]
>
>Este artigo é baseado na estrutura do Angular. SPA Para o documento correspondente para a estrutura do React, consulte [Introdução ao AEM - React](getting-started-react.md).

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

Este documento abordará a estrutura de um SPA simplificado e ilustrará como ele funciona para que você possa aplicar essa compreensão ao seu próprio SPA.

## Dependências, configuração e criação {#dependencies-configuration-and-building}

Além da dependência de Angular esperada, a amostra SPA pode usar bibliotecas adicionais para tornar a criação do SPA mais eficiente.

### Dependências {#dependencies}

O arquivo `package.json` define os requisitos do pacote SPA geral. As dependências mínimas necessárias do AEM estão listadas aqui.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

`"build": "ng build --build-optimizer=false && clientlib",`

Depois de criado, o pacote pode ser carregado para uma instância AEM.

### Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou o Angular e utiliza o SDK de SPA.

## Estrutura do aplicativo {#application-structure}

Incluir as dependências e criar seu aplicativo conforme descrito anteriormente deixará você com um pacote de SPA que funciona e que você pode carregar para sua instância do AEM.

A próxima seção deste documento abordará como um SPA no AEM está estruturado, os arquivos importantes que orientam o aplicativo e como eles funcionam juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo se baseiam no mesmo conceito.

### app.module.ts {#app-module-ts}

O ponto de entrada no SPA é o arquivo `app.module.ts` mostrado aqui simplificado para se concentrar no conteúdo importante.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

O arquivo `app.module.ts` é o ponto inicial do aplicativo e contém a configuração inicial do projeto e usa `AppComponent` para inicializar o aplicativo.

#### Instanciação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o template do componente, o valor deve ser passado do modelo para as propriedades do componente. Os valores do modelo são passados como atributos para ficarem disponíveis posteriormente como propriedades de componente.

### app.component.ts {#app-component-ts}

Uma vez que o `app.module.ts` inicializa o `AppComponent`, ele pode inicializar o aplicativo, que é mostrado aqui em uma versão simplificada para se concentrar no conteúdo importante.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

Ao processar a página, o `app.component.ts` chama o `main-content.component.ts` listado aqui em uma versão simplificada.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

O `MainComponent` assimila a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Mais detalhes sobre o `Page` podem ser encontrados no documento [Blueprint do SPA](blueprint.md).

### image.component.ts {#image-component-ts}

O `Page` é composto de componentes. Com o JSON assimilado, o `Page` pode processar esses componentes, como o `image.component.ts`, como mostrado aqui.

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

A ideia central do AEM é a ideia de mapear componentes do SPA AEM para componentes do SPA e atualizar o componente quando o conteúdo é modificado (e vice-versa). Consulte o documento [Visão geral do editor de SPA](editor-overview.md) para obter um resumo desse modelo de comunicação.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

O método `MapTo` mapeia o componente SPA para o componente AEM. Ele suporta o uso de uma única string ou uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para habilitar os recursos de criação de um componente, fornecendo os metadados necessários para que o editor gere espaços reservados

Se não houver conteúdo, os rótulos serão fornecidos como espaços reservados para representar o conteúdo vazio.

#### Propriedades passadas dinamicamente {#dynamically-passed-properties}

Os dados provenientes do modelo são transmitidos dinamicamente como propriedades do componente.

### image.component.html {#image-component-html}

Finalmente, a imagem pode ser renderizada em `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Compartilhamento de informações entre componentes do SPA {#sharing-information-between-spa-components}

É regularmente necessário que os componentes de um aplicativo de página única compartilhem informações. Há várias maneiras recomendadas de fazer isso, listadas a seguir em uma ordem crescente de complexidade.

* **Opção 1:** Centralize a lógica e a difusão nos componentes necessários, por exemplo, usando uma classe util como uma solução puramente orientada a objetos.
* **Opção 2:** Compartilhe estados do componente usando uma biblioteca de estado como NgRx.
* **Opção 3:** Aproveite a hierarquia de objetos personalizando e estendendo o componente de contêiner.

## Próximas etapas {#next-steps}

* [Introdução ao SPA no AEM usando o React](getting-started-react.md) mostra como um SPA básico é criado para funcionar com o editor do SPA AEM usando o React.
* A [Visão geral do editor de SPA](editor-overview.md) aborda em detalhes o modelo de comunicação do AEM e do SPA.
* O [Projeto WKND SPA](wknd-tutorial.md) é um tutorial passo a passo para a implementação de um projeto SPA simples no AEM.
* [Modelo dinâmico para mapeamento de componentes para SPA](model-to-component-mapping.md) explica o modelo dinâmico para mapeamento de componentes e como ele funciona dentro do SPA no AEM.
* O [Blueprint do SPA](blueprint.md) oferece um aprofundamento sobre como o SDK do SPA para AEM funciona caso você queira implementar o SPA AEM no para uma estrutura diferente do React ou do Angular ou simplesmente deseja obter um entendimento mais profundo.
