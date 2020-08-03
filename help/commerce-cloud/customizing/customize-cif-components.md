---
title: Personalizar componentes principais CIF
description: Personalizar componentes principais CIF
translation-type: tm+mt
source-git-commit: dd6973085ae34dd6ea7296c36d0a14f699440269
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 1%

---


# Personalizar AEM componentes principais CIF {#customize-cif-components}

[AEM CIF Componentes](https://github.com/adobe/aem-core-cif-components) principais fornece um conjunto padrão de componentes de Comércio que podem ser usados para acelerar um projeto que integra soluções de Adobe Experience Manager (AEM) e Magento. Esses componentes estão prontos para produção e podem ser [facilmente estilizados com CSS](style-cif-component.md). Muitas implementações também desejarão estender esses componentes para atender às necessidades específicas da empresa.

Neste tutorial, iremos rever vários pontos de extensão diferentes fornecidos por AEM componentes principais CIF e AEM em geral. Isso será feito estendendo os recursos do componente Teaser [do](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) produto para incluir a capacidade de renderizar um banner &quot;Novo&quot;. Os autores de conteúdo terão a capacidade de alternar esse banner e determinar quanto tempo serão exibidos. A &quot;idade&quot; do produto será baseada na data de criação no catálogo de Magento. Uma vez que um produto tenha uma certa quantidade de dias, o banner &quot;Novo&quot; deverá desaparecer automaticamente.

![Novo banner estendido](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## Pré-requisitos {#prerequisites}

As seguintes ferramentas e tecnologias são necessárias:

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 ou mais recente)
* [SKD da AEM Cloud com suplemento CIF](../develop.md)
* Magento compatível com os componentes principais CIF

É recomendável revisar o seguinte conteúdo antes de prosseguir com este tutorial:

* [Apresentando a estrutura de integração de comércio em AEM como Cloud Service](/help/commerce-cloud/overview.md)
* [Estilo AEM componentes principais CIF - Tutorial](style-cif-component.md)

## Projeto inicial

Fornecemos um projeto inicial para ser usado com este tutorial. O projeto foi gerado usando [v0.7.0](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) do arquivo CIF do projeto. É considerada uma prática recomendada sempre usar a versão [](https://github.com/adobe/aem-cif-project-archetype/releases/latest) mais recente do arquétipo ao iniciar um novo projeto.

1. Baixe o projeto inicial [**acme-store.zip **](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip)em seu desktop.

1. Descompacte **acme-store.zip** e você deve ver a seguinte estrutura de pastas:

   ```plain
   /acme-store
      /ui.content
      /ui.apps
      /samplecontent
      /core
      /all
      + pom.xml
      + README.md
   ```

1. Abra uma nova janela de terminal e crie e implante o projeto em uma instância local do AEM;

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Adicione as configurações OSGi necessárias para conectar sua instância de AEM a uma instância de Magento ou adicione as configurações ao projeto recém-criado.

1. Neste ponto, você deve ter uma versão em funcionamento de uma vitrine que esteja conectada a uma instância Magento. Navegue até a página `US` > `Home` em: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Vocês devem ver que a vitrine está usando o tema de Venia. Ao expandir o Menu principal da frente de loja, você deve ver várias categorias, indicando que o Magento de conexão está funcionando.

   ![Vitrine configurada com o tema Venia](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## Autor do Teaser de produto {#author-product-teaser}

Estenderemos o componente Teaser do produto neste tutorial. Como primeira etapa, adicionaremos uma nova instância do Teaser de produto ao Home page para entender a funcionalidade da linha de base.

1. Navegue até o **Home page** do site: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. Insira um novo Componente do **Teaser** do produto no container do layout principal na página.

   ![Inserir Teaser de Produto](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. Expanda o painel lateral (se ainda não estiver alternado) e alterne a lista suspensa do localizador de ativos para **Produtos**. Isso deve exibir uma lista de produtos disponíveis de uma instância de Magento conectada. Selecione um produto e **arraste e solte** -o no componente **Teaser** do produto na página.

   ![Arrastar + Soltar Teaser de Produto](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > Observação: você também pode configurar o produto exibido configurando o componente usando a caixa de diálogo (clicando no ícone de *chave* ).

1. Agora você deve ver um Produto sendo exibido pelo Teaser de produto. O Nome do produto e o Preço do produto são atributos padrão exibidos.

   ![Teaser do produto - estilo padrão](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## Personalização da marcação do Teaser de produto {#customize-markup-product-teaser}

Uma extensão comum de componentes AEM é modificar a marcação gerada pelo componente. Isso é feito substituindo o script [](https://docs.adobe.com/content/help/br/experience-manager-htl/using/overview.html) HTL que o componente usa para renderizar sua marcação. Linguagem de modelo HTML (HTL) é uma linguagem de modelo leve que AEM componentes usam para renderizar dinamicamente a marcação com base no conteúdo criado, permitindo que os componentes sejam reutilizados. O Teaser de produto, por exemplo, pode ser reutilizado várias vezes para exibir produtos diferentes.

Em nosso caso, queremos renderizar um banner sobre o teaser para indicar que o produto é &quot;Novo&quot; e foi adicionado recentemente ao catálogo. O padrão de design para [personalizar a marcação](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de um componente é, na verdade, padrão para todos os componentes AEM, não apenas para os componentes principais AEM.

Use o IDE de sua escolha para [abrir o projeto inicial baixado](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) no início do tutorial.

1. Navegue e expanda o módulo **ui.apps** e expanda a hierarquia de pastas para: `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` e inspecione o `.content.xml` arquivo.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   Acima está a definição de Componente para o Componente Teaser do Produto em nosso projeto. Observe a propriedade `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este é um exemplo de criação de um componente [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)Proxy. Em vez de copiar e colar todos os scripts HTL do Teaser de produto dos componentes principais CIF AEM, podemos usar o para herdar toda a funcionalidade. `sling:resourceSuperType`

1. Abra um novo navegador e navegue até [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) no AEM. Expanda a árvore para visualização do `productteaser` componente em: `/apps/core/cif/components/commerce/productteaser/v1/productteaser`:

   ![CRXDE Lite Product Teaser](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   Esta é a definição completa do componente do Teaser do produto.

1. Volte para seu IDE e para o projeto Acme Store. Crie um novo arquivo com o nome `productteaser.html` abaixo `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Copie o conteúdo do `productteaser.html` do [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) e cole-o no projeto Acme-Store no `productteaser.html` arquivo recém-criado.

   ![Substituição html do Teaser do produto](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. No projeto Acme-Store, modifique o `productteaser.html` arquivo e insira uma nova div que representa um selo acima da marcação de imagem do produto:

   ```html
   ...
   <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
       <!-- Add Badge -->
       <div class="item__badge">
           <span>New</span>
       </div>
       <!-- end add badge -->
       <a class="item__images" href=${product.url}>
           <img class="item__image" width="100%" height="100%"
                   src="${product.image}" alt="${product.image}"/>
       </a>
       <a class="item__name" href=${product.url}><span>${product.name}</span></a>
       <div class="item__price">
           <span> ${product.formattedPrice} </span>
       </div>
       <sly data-sly-call="${actionsTpl.actions @ product=product}"></sly>
   </div>
   ```

1. Implante o código atualizado para a instância local do AEM usando suas habilidades de maven ou usando [os recursos de seu IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment):

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. No navegador, retorne à [Página inicial da loja na frente](http://localhost:4502/editor.html/content/acme/us/en.html) da AEM. Atualize e você deverá ver que um banner &quot;novo&quot; aparece no canto superior direito do componente.

   ![Novo banner estendido](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   No momento, não há lógica atrás de quando o banner será exibido. Nos próximos exercícios, corrigiremos isso.

   > Observe que o CSS para renderizar o banner foi fornecido como parte do projeto inicial e pode ser encontrado em: `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. Para obter mais detalhes, consulte o tutorial [Styling CIF Core Components (Componentes principais de estilo CIF)](style-cif-component.md).

## Personalização da caixa de diálogo do Teaser de produto {#customize-dialog-product-teaser}

Em seguida, personalizaremos a caixa de diálogo do componente Teaser do produto para permitir que um autor determine o intervalo de datas para o qual um produto é considerado &quot;novo&quot; e se o banner deve ser exibido. Faremos isso [personalizando a caixa de diálogo](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) do Teaser de produto como parte do projeto da Acme Store.

1. Abra o projeto Acme Store no IDE de sua escolha e navegue até `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Abaixo da `productteaser` pasta, adicione uma nova pasta chamada `_cq_dialog`. Adicione um novo arquivo à `_cq_dialog` pasta chamada `.content.xml`. Agora você deve ter a seguinte estrutura de arquivos:

   ```plain
   ../acme
       /components
           /commerce
               /productteaser
                  /_cq_dialog
                     + .content.xml
                  /_cq_template
                  + .content.xml
                  + productteaser.html
   ```

1. Atualize `_cq_dialog/.content.xml` com o seguinte XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
       xmlns:cq="http://www.day.com/jcr/cq/1.0" 
       xmlns:jcr="http://www.jcp.org/jcr/1.0" 
       xmlns:nt="http://www.jcp.org/jcr/nt/1.0" 
       jcr:primaryType="nt:unstructured" 
       jcr:title="My Product Teaser" 
       sling:resourceType="cq/gui/components/authoring/dialog" 
       trackingFeature="cif-core-components:productteaser:v1">
       <content jcr:primaryType="nt:unstructured" 
           sling:resourceType="granite/ui/components/coral/foundation/container">
           <items jcr:primaryType="nt:unstructured">
               <tabs jcr:primaryType="nt:unstructured" 
                   sling:resourceType="granite/ui/components/coral/foundation/tabs" 
                   maximized="{Boolean}true">
                   <items jcr:primaryType="nt:unstructured">
                       <badge jcr:primaryType="nt:unstructured" 
                           jcr:title="Badge" 
                           sling:resourceType="granite/ui/components/coral/foundation/container" 
                           margin="{Boolean}true">
                           <items jcr:primaryType="nt:unstructured">
                               <columns jcr:primaryType="nt:unstructured" 
                                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns" 
                                   margin="{Boolean}true">
                                   <items jcr:primaryType="nt:unstructured">
                                       <column jcr:primaryType="nt:unstructured" 
                                           sling:resourceType="granite/ui/components/coral/foundation/container">
                                           <items jcr:primaryType="nt:unstructured">
                                               <badge jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/checkbox" 
                                                   text="Display 'New' badge" 
                                                   value="true" 
                                                   uncheckedValue="false" 
                                                   name="./badge" />
                                               <age jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield" 
                                                   fieldDescription="The maximum age in days the 'new' badge should be shown" 
                                                   fieldLabel="Max Product Age" 
                                                   name="./age"
                                                   min="{Long}0" 
                                                   value="10" />
                                               <ageTypeHint jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/foundation/form/hidden" 
                                                   ignoreData="{Boolean}true" 
                                                   name="./age@TypeHint" 
                                                   value="Long" />
                                           </items>
                                       </column>
                                   </items>
                               </columns>
                           </items>
                       </badge>
                   </items>
               </tabs>
           </items>
       </content>
   </jcr:root>
   ```

   Acima adicionamos 2 campos adicionais como parte de uma nova guia e um único campo oculto.

   1. Caixa de seleção para exibir o símbolo &quot;Novo&quot;
   2. Campo Número para definir a idade máxima do produto
   3. Campo oculto para garantir que a idade máxima do produto seja salva como uma longa (consulte [@TypeHint](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) para obter mais detalhes)

   As caixas de diálogo definidas como parte de um componente proxy herdam todos os campos de diálogo existentes com um recurso conhecido como Fusão [de Recursos de](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/sling-resource-merger.html)Sling. Portanto, não é necessário redefinir os campos existentes que fazem parte do Teaser de produto.

1. Atualize `productteaser.html` e adicione um `data-sly-test` ao `<div>` cartão do distintivo. Este será um teste simples para decidir renderizar o crachá se o usuário tiver marcado &quot;true&quot;.

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. Implante o código atualizado para a instância local do AEM usando os recursos de seu IDE ou usando suas habilidades em maven:

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. Retorne ao componente Teaser do produto e clique no *ícone da chave de fenda* para abrir a caixa de diálogo. Agora você deve ver uma guia para **Badge** com dois campos adicionais. Atualizar esses campos persistirá os valores para AEM. Você deve poder ativar/desativar o selo com a caixa de seleção:

   ![Alternar emblema](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   Isso dá ao autor algum controle sobre quando o crachá aparece. No entanto, seria ideal que o crachá desaparecesse automaticamente assim que o produto atingisse uma determinada idade do dia, com base na entrada **Máx. de idade** do produto. Para isso, teremos de implementar alguma lógica de back-end.

## Atualização do modelo Sling para o Teaser do produto {#updating-sling-model-product-teaser}

Em seguida, estenderemos a lógica comercial do Teaser de produto implementando um Modelo Sling. [Modelos](https://sling.apache.org/documentation/bundles/models.html)Sling são &quot;POJOs&quot; orientados por anotações (objetos Java simples) que implementam qualquer lógica comercial necessária ao componente. Modelos Sling são usados em conjunto com os scripts HTL como parte do componente. Seguiremos o padrão de [delegação para Modelos](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) Sling para que possamos estender partes do modelo existente do Teaser de Produto.

Os Modelos Sling são implementados como Java e podem ser encontrados no módulo **principal** do projeto gerado.

1. Abra o projeto Acme Store no IDE de sua escolha e navegue sob o módulo **principal** para: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java** é uma interface Java pré-criada que estende a interface CIF **ProductTeaser** .

1. Em seguida, abra o arquivo **MyProductTeaserImpl.java** localizado em: `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` é a classe de implementação da interface `MyProductTeaser`.

   Usando o padrão de [delegação para Modelos](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) Sling, podemos fazer referência à `ProductTeaser` classe por meio da `sling:resourceSuperType` propriedade:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Para todos os métodos que não queremos substituir ou alterar, podemos simplesmente retornar o valor que o `ProductTeaser` retorna:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

1. Um dos pontos de extensão adicionais fornecidos pela AEM CIF Core Components é o `AbstractProductRetriever` que nos permite obter acesso a atributos específicos do produto. Adicione o seguinte método para inicializar o `AbstractProductRetriever` no `init()` método:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
       }
   ...
   ```

1. Permite testar essas alterações modificando o preço formatado e substituindo a lógica em `getFormattedPrice()`. Faça as seguintes atualizações para que formate explicitamente o preço com base na localidade alemã. (ou escolha um país diferente!)

   ```java
           import java.util.Locale;
           import java.text.NumberFormat;
            ...
   
               @Override
                   public String getFormattedPrice() 
                   {
                   //return productTeaser.getFormattedPrice();
                   NumberFormat germanCurrencyFormat = NumberFormat.getCurrencyInstance(Locale.GERMANY);
                   Double price =  productRetriever.fetchProduct().getPrice().getRegularPrice().getAmount().getValue();
                       if(price != null) 
                       {
                           return germanCurrencyFormat.format(price);
                       }
                   return null;
                   }
   ```

   Observe como o `productRetriever` objeto nos dá acesso ao `ProductInterface` objeto por meio do `fetchProduct()` método. Você pode ver todos os métodos [disponíveis aqui](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java).

   > Observação* modificar a localidade para alemão é apenas um exemplo divertido para ver a substituição. Na realidade, o ProductTeaser usa a localidade da [página para determinar o formato](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173).

1. Em seguida, precisamos atualizar o **productteaser.html** no módulo **ui.apps** para consultar nosso novo Modelo Sling em: `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
       ...
   ```

   Salve as alterações em `productteaser.html`.

1. Implante a base de código para a instância local do AEM. Como foram feitas alterações nos módulos **ui.apps** e **core** , crie e implante o projeto da raiz:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Abra um navegador e navegue até: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels). Este console mostra todos os Modelos Sling registrados no sistema. Verifique o Duplo para garantir que MyTeaserModelImpl foi implantado e está mapeado corretamente. Você deve ser capaz de ver algo como:

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. Por fim, navegue até o local de criação do componente Teaser de produto e agora você deve ver o preço com o formato de moeda alemão:

   ![Formato de preço atualizado](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## Implementação da lógica isShowBadge {#implement-isshowbadge}

Agora que tivemos a oportunidade de experimentar com a substituição dos métodos do Modelo Sling, vamos implementar a lógica de quando exibir o &quot;novo&quot; selo.

1. Retorne ao seu IDE e abra o arquivo **MyProductTeaser.java** em: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`.

1. Adicione um novo método `isShowBadge()` à interface:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   }
   ```

   Este é um novo método que introduziremos para encapsular a lógica de mostrar ou não o crachá.

1. Em seguida, abra novamente **MyProductTeaserImpl.java** em `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`.

1. A lógica por quanto tempo o selo &quot;novo&quot; será exibido será baseada no `created_at` atributo do Produto. Para ter acesso a esse atributo, precisamos estender o query **GraphQL** executado pelo ProductTeaser. Podemos fazer isso atualizando o `init()` método em **MyProductTeaserImpl.java**:

   ```java
   //MyProductTeaserImpl.java
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           // Pass your custom partial query to the ProductRetriever. This class will
           // automatically take care of executing your query as soon
           // as you try to access any product property.
           productRetriever.extendProductQueryWith(p ->
               p.addCustomSimpleField("created_at")
           );
       }
   }
   ```

   Adicionar ao `extendProductQueryWith` método é uma maneira poderosa de garantir que atributos de produto adicionais estejam disponíveis para o restante do modelo. Também minimiza o número de query executados.

   >[!NOTE]
   >No código acima, estamos usando o para`addCustomSimpleField` recuperar a `created_at` propriedade. Isso ilustra como você pode query para qualquer atributo personalizado que faça parte do schema Magento.
   >
   > No entanto, a `created_at` propriedade foi efetivamente implementada como parte da Interface [do](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) Produto e uma prática melhor seria reutilizar o método como o: `productRetriever.extendProductQueryWith(p -> p.createdAt());`. A maioria dos atributos de schema comumente encontrados foram implementados, portanto, use somente os atributos `addCustomSimpleField` para atributos verdadeiramente personalizados.

1. Em seguida, implementaremos o `isShowBadge()` método:

   ```java
   import java.time.format.DateTimeFormatter;
   import java.util.Locale;
   import java.time.temporal.ChronoUnit;
   
   ...
   
   @Override
   public Boolean isShowBadge() {
        final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
   
        //Look at the checkbox from the dialog to see if we should even attempt to show the badge
        final boolean showBadge = properties.get("badge", false);
        if (showBadge) {
   
            //Look at the numberfield set from the dialog to determine the max "age" in days to compare too
            final int maxAgeProp = properties.get("age", 0);
   
           String createdAtString;
           try {
               //Grab the created_at property from the product
               //Here we show the example of retrieving the attribute as if it was a custom attribute
               // an alternative that would work is productRetriever.fetchProduct().getCreatedAt()
               createdAtString = productRetriever.fetchProduct().getAsString("created_at");
               log.info("***CREATED_AT**** " + createdAtString);
           } catch (SchemaViolationError e) {
               //it is possible that a schema error could be thrown if the attribute is not part of the schema
               log.error("Error determining to showBadge" , e);
               return false;
           }
   
            // Custom code to calc the date difference of the product creation
            // compared to today
           final LocalDate createdAt = LocalDate.parse(createdAtString, formatter);
            if (createdAt != null) {
   
                final long ageInDays = ChronoUnit.DAYS.between(createdAt, LocalDate.now());
                if (ageInDays < maxAgeProp) {
                    return true;
                }
            }
        }
        return false;
    }
   ```

   No método acima, primeiro verificamos se o autor habilitou a funcionalidade do crachá com a caixa de seleção. Em seguida, lemos o valor da propriedade `age` definida como parte da caixa de diálogo e representa o número máximo de dias que um produto deve ter até que o banner desapareça. Por fim, calculamos a idade do produto com base na `created_at` data. Se, depois de comparar os dois valores, voltarmos `true` a mostrar o crachá, `false` em todos os outros casos.

1. Finalmente, é necessário fazer mais uma adição ao `productteaser.html` script para chamar o `isShowBadge()` método. Abra o arquivo em `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`. Faça a seguinte atualização:

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. Implante a base de código para a instância local do AEM. Como foram feitas alterações nos módulos **ui.apps** e **core** , crie e implante o projeto da raiz:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Retorne ao AEM e ao componente ProductTeaser e experimente com números diferentes para exibir a idade máxima do produto. Dependendo da idade do produto, talvez seja necessário digitar números muito grandes para que o selo seja exibido.

   ![Idade Máx. do Produto 999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. Por fim, pesquise nos registros de AEM para ver a declaração de log inserida na etapa 5 acima. Isso deve imprimir o valor da `created_at` propriedade que vem do Magento. Você pode visualização os registros de AEM abrindo o `error.log` arquivo. Esse arquivo está localizado abaixo do local `crx-quickstart/logs/error.log` onde o jar AEM foi instalado. Você pode esperar ver um item de linha como o seguinte:

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   Agora você pode verificar se a lógica que implementamos está correta!

### Parabéns {#congratulations}

Você acabou de personalizar seu primeiro componente AEM CIF! Baixe o pacote da solução [concluída aqui](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip).

## Recursos adicionais {#additional-resources}

* [AEM Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)
* [Componentes principais CIF AEM](https://github.com/adobe/aem-core-cif-components)
* [Personalização AEM componentes principais CIF](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [Personalização dos componentes principais](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
