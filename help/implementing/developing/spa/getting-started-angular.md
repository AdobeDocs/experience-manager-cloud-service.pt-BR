---
title: Introdução aos SPAs no AEM usando o Angular
description: Este artigo apresenta um aplicativo SPA de amostra, explica como ele é montado e permite que você comece a trabalhar com seu próprio SPA rapidamente usando a estrutura Angular.
translation-type: tm+mt
source-git-commit: 8bdb7bbe80a4e22bb2b750c0719c6db745133392
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---


# Introdução aos SPAs no AEM usando o Angular {#getting-started-with-spas-in-aem-using-angular}

Os aplicativos de página única (SPAs) podem oferta experiências interessantes para os usuários do site. Os desenvolvedores desejam criar sites usando estruturas SPA e os autores desejam editar o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação do SPA oferta uma solução abrangente para suportar SPAs dentro do AEM. Este artigo apresenta um aplicativo de SPA simplificado na estrutura Angular, explica como ele é montado, permitindo que você entre em operação com seu próprio SPA rapidamente.

>[!NOTE]
>
>Este artigo baseia-se na estrutura Angular. Para o documento correspondente para a estrutura React, consulte [Introdução às SPAs em AEM - Reagir](getting-started-react.md).

## Introdução {#introduction}

Este artigo resume o funcionamento básico de um SPA simples e o mínimo que você precisa saber para executar o seu.

Para obter mais detalhes sobre como os SPAs funcionam em AEM, consulte os seguintes documentos:

* [Introdução ao SPA e Walkthrough](introduction.md)
* [Visão geral do editor SPA](editor-overview.md)
* [Blueprint do SPA](blueprint.md)

>[!NOTE]
>
>Para ser capaz de criar conteúdo em um SPA, o conteúdo deve ser armazenado em AEM e exposto pelo modelo de conteúdo.
>
>Um SPA desenvolvido fora do AEM não será autorável se não respeitar o contrato do modelo de conteúdo.

Este documento percorrerá a estrutura de um SPA simplificado e ilustrará como ele funciona para que você possa aplicar essa compreensão ao seu próprio SPA.

## Dependências, configuração e criação {#dependencies-configuration-and-building}

Além da dependência Angular esperada, o SPA de amostra pode aproveitar bibliotecas adicionais para tornar a criação do SPA mais eficiente.

### Dependências {#dependencies}

O `package.json` arquivo define os requisitos do pacote SPA geral. As dependências de AEM mínimas obrigatórias estão listadas aqui.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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

Na verdade, a criação do aplicativo aproveita o [Webpack](https://webpack.js.org/) para transpilação, além do gerador aem-clientlib para a criação automática da biblioteca do cliente. Portanto, o comando build será semelhante a:

`"build": "ng build --build-optimizer=false && clientlib",`

Depois de criado, o pacote pode ser carregado para uma instância AEM.

### Arquétipo de projeto do AEM{#aem-project-archetype}

Qualquer projeto AEM deve aproveitar o [AEM Project Archetype](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html), que suporta projetos SPA usando React ou Angular e aproveita o SDK do SPA.

## Estrutura do aplicativo {#application-structure}

A inclusão das dependências e a criação do aplicativo conforme descrito anteriormente o deixarão com um pacote SPA em funcionamento que você pode carregar para a instância AEM.

A próxima seção deste documento o orientará sobre como um SPA em AEM é estruturado, os arquivos importantes que acionam o aplicativo e como eles trabalham juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo são baseados no mesmo conceito.

### app.module.ts {#app-module-ts}

O ponto de entrada no SPA é o `app.module.ts` arquivo mostrado aqui simplificado para focar no conteúdo importante.

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

O `app.module.ts` arquivo é o ponto de partida do aplicativo e contém a configuração inicial do projeto e usa `AppComponent` para inicializar o aplicativo.

#### Instanciação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o modelo de componente, o valor deve ser passado do modelo para as propriedades do componente. Os valores do modelo são passados como atributos para ficarem disponíveis posteriormente como propriedades do componente.

### app.component.ts {#app-component-ts}

Depois de `app.module.ts` inicializar `AppComponent`, é possível inicializar o aplicativo, que é mostrado aqui em uma versão simplificada para focar no conteúdo importante.

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

Ao processar a página, `app.component.ts` as chamadas `main-content.component.ts` listadas aqui em uma versão simplificada.

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

O `MainComponent` assimila a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Para obter mais detalhes sobre o `Page` documento, consulte [SPA Blueprint (Blueprint](blueprint.md)do SPA do adaptador SPA).

### image.component.ts {#image-component-ts}

O `Page` é composto de componentes. Com o JSON ingerido, o `Page` pode processar esses componentes, como `image.component.ts` mostrado aqui.

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

A ideia central dos SPAs no AEM é mapear componentes do SPA para AEM componentes e atualizar o componente quando o conteúdo é modificado (e vice-versa). Consulte Visão geral [do editor](editor-overview.md) SPA do documento para obter um resumo desse modelo de comunicação.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

O `MapTo` método mapeia o componente SPA para o componente AEM. Ele suporta o uso de uma única string ou de uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para ativar os recursos de criação de um componente, fornecendo os metadados necessários para o editor gerar espaços reservados

Se não houver conteúdo, os rótulos serão fornecidos como espaços reservados para representar o conteúdo vazio.

#### Propriedades aprovadas dinamicamente {#dynamically-passed-properties}

Os dados provenientes do modelo são transmitidos dinamicamente como propriedades do componente.

### image.component.html {#image-component-html}

Finalmente, a imagem pode ser renderizada em `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Compartilhamento de informações entre componentes do SPA {#sharing-information-between-spa-components}

É necessário que os componentes de um aplicativo de página única compartilhem informações regularmente. Há várias maneiras recomendadas de fazer isso, listadas a seguir, para aumentar a ordem de complexidade.

* **Opção 1:** Centralize a lógica e a transmissão para os componentes necessários, por exemplo, usando uma classe util como uma solução pura orientada a objetos.
* **Opção 2:** Compartilhe estados de componentes usando uma biblioteca de estado como NgRx.
* **Opção 3:** Aproveite a hierarquia de objetos personalizando e estendendo o componente de container.

## Próximas etapas {#next-steps}

* [A Introdução aos SPAs no AEM usando o React](getting-started-react.md) mostra como um SPA básico foi criado para funcionar com o Editor SPA no AEM usando o React.
* [Visão geral](editor-overview.md) do editor SPA aprofunda o modelo de comunicação entre o AEM e o SPA.
* [O WKND SPA Project](wknd-tutorial.md) é um tutorial passo a passo que implementa um projeto SPA simples no AEM.
* [O Modelo dinâmico para mapeamento de componentes para SPAs](model-to-component-mapping.md) explica o modelo dinâmico para mapeamento de componentes e como ele funciona em SPAs no AEM.
* [O SPA Blueprint](blueprint.md) oferta um aprofundamento sobre como o SDK do AEM funciona caso você deseje implementar SPAs em AEM para uma estrutura diferente de React ou Angular ou simplesmente deseje um entendimento mais profundo.
