---
title: Introdução a SPAs no AEM usando o Angular
description: Este artigo apresenta uma amostra de aplicativo SPA, explica como ele é montado e permite que você comece a usar seu próprio SPA rapidamente usando a estrutura do Angular.
exl-id: 8013ac2c-d1a7-4940-bb65-15e3ed7652d6
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 12%

---

# Introdução a SPAs no AEM usando o Angular {#getting-started-with-spas-in-aem-using-angular}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas SPA, e os autores desejam editar o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação do SPA oferece uma solução abrangente para oferecer suporte ao SPA no AEM. Este artigo apresenta um aplicativo simplificado de SPA na estrutura do Angular e explica como ele é montado, permitindo que você comece a usar seu próprio SPA rapidamente.

>[!NOTE]
>
>Este artigo é baseado na estrutura do Angular. Para o documento correspondente para o quadro do React, ver [SPA Introdução ao AEM - React](getting-started-react.md).

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

A variável `package.json` define os requisitos do pacote SPA geral. As dependências mínimas necessárias do AEM estão listadas aqui.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

A variável `aem-clientlib-generator` O é usado para tornar a criação de bibliotecas de clientes automática como parte do processo de criação.

`"aem-clientlib-generator": "^1.4.1",`

Mais detalhes podem ser encontrados [no GitHub aqui](https://github.com/wcm-io-frontend/aem-clientlib-generator).

A variável `aem-clientlib-generator` está configurado no `clientlib.config.js` arquivo como segue.

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

### Criando {#building}

Criar realmente os usos do aplicativo [Webpack](https://webpack.js.org/) para tradução, além do aem-clientlib-generator para criação automática da biblioteca do cliente. Portanto, o comando build será semelhante a:

`"build": "ng build --build-optimizer=false && clientlib",`

Depois de criado, o pacote pode ser carregado para uma instância AEM.

### Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou o Angular e utiliza o SDK de SPA.

## Estrutura do aplicativo {#application-structure}

Incluir as dependências e criar seu aplicativo conforme descrito anteriormente deixará você com um pacote de SPA que funciona e que você pode carregar para sua instância do AEM.

A próxima seção deste documento abordará como um SPA no AEM está estruturado, os arquivos importantes que orientam o aplicativo e como eles funcionam juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo se baseiam no mesmo conceito.

### app.module.ts {#app-module-ts}

O ponto de entrada no SPA é o `app.module.ts` O arquivo mostrado aqui foi simplificado para se concentrar no conteúdo importante.

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

A variável `app.module.ts` arquivo é o ponto inicial do aplicativo e contém a configuração inicial do projeto e usa `AppComponent` para inicializar o aplicativo.

#### Instanciação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o template do componente, o valor deve ser passado do modelo para as propriedades do componente. Os valores do modelo são passados como atributos para ficarem disponíveis posteriormente como propriedades de componente.

### app.component.ts {#app-component-ts}

Uma vez `app.module.ts` bootstrap `AppComponent`, ele poderá inicializar o aplicativo, que é mostrado aqui em uma versão simplificada para se concentrar no conteúdo importante.

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

Ao processar a página, `app.component.ts` chamadas `main-content.component.ts` listado aqui em uma versão simplificada.

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

A variável `MainComponent` A assimila a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Mais detalhes sobre o `Page` pode ser encontrado no documento [Blueprint SPA](blueprint.md).

### image.component.ts {#image-component-ts}

A variável `Page` O é composto por componentes. Com o JSON assimilado, a variável `Page` podem processar esses componentes, como `image.component.ts` como mostrado aqui.

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

A ideia central do AEM é a ideia de mapear componentes do SPA AEM para componentes do SPA e atualizar o componente quando o conteúdo é modificado (e vice-versa). Consulte o documento [Visão geral do editor de SPA](editor-overview.md) para obter um resumo deste modelo de comunicação.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

A variável `MapTo` O método mapeia o componente SPA para o componente AEM. Ele suporta o uso de uma única string ou uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para habilitar os recursos de criação de um componente, fornecendo os metadados necessários para o editor gerar espaços reservados

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

* **Opção 1:** Centralize a lógica e a transmissão para os componentes necessários, por exemplo, usando uma classe util como uma solução puramente orientada a objetos.
* **Opção 2:** Compartilhe estados do componente usando uma biblioteca de estado como NgRx.
* **Opção 3:** Aproveite a hierarquia de objetos personalizando e estendendo o componente de contêiner.

## Próximas etapas {#next-steps}

* O artigo [Introdução aos SPAs no AEM usando o React](getting-started-react.md) mostra como um SPA básico é desenvolvido para funcionar com o editor de SPA no AEM usando o React.
* A [Visão geral do editor de SPA](editor-overview.md) aborda em detalhes o modelo de comunicação do AEM e do SPA.
* [Projeto SPA WKND](wknd-tutorial.md) O é um tutorial passo a passo para a implementação de um projeto simples de SPA no AEM.
* [Modelo dinâmico para mapeamento de componentes para SPA](model-to-component-mapping.md) SPA explica o modelo dinâmico para o mapeamento de componentes e como ele funciona dentro do AEM.
* [Blueprint SPA](blueprint.md) O oferece um aprofundamento em como o SDK do SPA para AEM funciona caso você queira implementar o SPA no AEM para uma estrutura diferente do React ou do Angular ou simplesmente deseja um entendimento mais profundo.
