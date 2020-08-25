---
title: Personalizar os Componentes principais da CIF
description: Personalizar os Componentes principais da CIF
translation-type: ht
source-git-commit: c3cf472f5e207e7ca0788dc3e42105868d9bdf00
workflow-type: ht
source-wordcount: '2520'
ht-degree: 100%

---


# Personalizar os Componentes principais da CIF do AEM{#customize-cif-components}

Os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) fornecem um conjunto padrão de componentes do Commerce que podem ser usados para acelerar um projeto que integra soluções do Adobe Experience Manager (AEM) e da Magento. Esses componentes estão prontos para produção e podem ser [facilmente estilizados com CSS](style-cif-component.md). Muitas implementações também estenderão esses componentes para atender às necessidades específicas da empresa.

Neste tutorial, vamos rever vários pontos de extensão diferentes fornecidos pelos Componentes principais da CIF do AEM e pelo AEM em geral. Faremos isso estendendo os recursos do componente [Teaser do produto](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) para incluir a capacidade de renderizar um banner com a inscrição &quot;Novo&quot;. Os autores de conteúdo terão a capacidade de ativar esse banner e determinar por quanto tempo será exibido. A &quot;idade&quot; do produto terá como base a data de criação no catálogo da Magento. Quando o produto tiver uma certa quantidade de dias, o banner “Novo” desaparecerá automaticamente.

![Aplicação do banner novo](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## Pré-requisitos {#prerequisites}

São necessárias as seguintes ferramentas e tecnologias:

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) (3.3.9 ou mais recente)
* [SDK da AEM Cloud com o complemento CIF](../develop.md)
* A Magento é compatível com os Componentes principais da CIF

É recomendável revisar o seguinte conteúdo antes de prosseguir com este tutorial:

* [Introdução à Commerce Integration Framework no AEM as a Cloud Service](/help/commerce-cloud/overview.md)
* [Alterar estilo dos Componentes principais da CIF do AEM — Tutorial](style-cif-component.md)

## Projeto inicial

Criamos um projeto inicial para ser usado com este tutorial. O projeto foi gerado usando a [v0.7.0](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) do Arquétipo de projeto da CIF. É considerada uma prática recomendada usar sempre a [versão mais recente](https://github.com/adobe/aem-cif-project-archetype/releases/latest) do arquétipo ao iniciar um novo projeto.

1. Baixe o projeto inicial [**acme-store.zip**](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip) no seu desktop.

1. Depois de descompactar o arquivo **acme-store.zip**, você verá a seguinte estrutura de pastas:

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

1. Abra uma nova janela de terminal para criar e implantar o projeto em uma instância local do AEM.

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Adicione as configurações OSGi necessárias para conectar a instância do AEM a uma instância da Magento ou adicione as configurações ao projeto recém-criado.

1. Nesta etapa, já deve estar funcionando uma versão de loja conectada a uma instância da Magento. Acesse a página `US` > `Home` em: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Você verá que a loja está usando o tema Venia. Ao expandir o Menu principal da loja você verá várias categorias, que é um sinal de que a conexão com a Magento está funcionando.

   ![Loja configurada com o tema Venia](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## Criação do Teaser do produto {#author-product-teaser}

Falaremos mais detalhadamente sobre o Teaser do produto neste tutorial. Como primeira etapa, adicionaremos uma nova instância do Teaser do produto à página inicial para entender a funcionalidade da linha de base.

1. Acesse a **página inicial** do site: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. Insira um novo **Teaser do produto** no container do layout principal da página.

   ![Inserir Teaser do produto](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. Expanda o painel lateral (se ainda não estiver sendo exibido) e na lista suspensa do localizador de ativos selecione **Produtos**. Essa ação deve exibir uma lista de produtos disponíveis em uma instância conectada da Magento. Selecione, **arraste e solte** um produto no **Teaser do produto** exibido na página.

   ![Arrastar e soltar Teaser do produto](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > Observação: você também pode configurar o produto exibido definindo o componente na caixa de diálogo (clicando na *chave inglesa*).

1. Agora você já deve estar vendo um produto no teaser. O nome e o preço do produto são atributos exibidos por padrão.

   ![Teaser do produto — estilo padrão](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## Personalização da marcação do Teaser do produto {#customize-markup-product-teaser}

Uma extensão comum de componentes do AEM é modificar a marcação gerada pelo componente. Essa modificação é feita substituindo o [script HTL](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html) que o componente usa para renderizar sua marcação. A Linguagem de modelo HTML (HTL) é uma linguagem de modelo leve que os componentes do AEM usam para renderizar dinamicamente a marcação com base no conteúdo criado, permitindo que os componentes sejam reutilizados. O Teaser do produto, por exemplo, pode ser reutilizado várias vezes para exibir produtos diferentes.

Em nosso caso, queremos renderizar um banner sobre o teaser para indicar que o produto é &quot;Novo&quot; e foi adicionado recentemente ao catálogo. O padrão de design para [personalizar a marcação](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de um componente é, na verdade, padrão para todos os componentes do AEM, não apenas para os Componentes principais da CIF do AEM.

Use o IDE de sua escolha para [abrir o projeto inicial baixado](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) no início do tutorial.

1. Acesse e expanda o módulo **ui.apps** e expanda a hierarquia de pastas para: `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` e verifique o arquivo `.content.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   Veja acima a definição de componente para o Teaser do produto em nosso projeto. Observe a propriedade `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este é um exemplo de criação de um [componente Proxy](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/get-started/using.html#create-proxy-components). Em vez de copiar e colar todos os scripts HTL do Teaser do produto dos Componentes principais da CIF do AEM, podemos usar o `sling:resourceSuperType` para herdar toda a funcionalidade. 

1. Abra um novo navegador e acesse o [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) no AEM. Expanda a árvore para visualizar o componente `productteaser` em: `/apps/core/cif/components/commerce/productteaser/v1/productteaser`:

   ![Teaser do produto CRXDE Lite](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   Esta é a definição completa do componente Teaser do produto.

1. Volte para o IDE e para o projeto Acme Store. Crie um novo arquivo com o nome `productteaser.html` debaixo de `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Copie o conteúdo de `productteaser.html` do [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) e cole-o no projeto Acme-Store no arquivo `productteaser.html` recém-criado.

   ![Substituir HTML do Teaser do produto](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. No projeto Acme-Store, modifique o arquivo `productteaser.html` e insira uma nova div que represente um símbolo acima da marcação de imagem do produto:

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

1. Implante o código atualizado na instância local do AEM usando suas habilidades maven ou usando [os recursos do IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment):

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. No navegador, retorne à [Página inicial da loja](http://localhost:4502/editor.html/content/acme/us/en.html) no AEM. Atualize a página e o banner &quot;novo&quot; aparecerá no canto superior direito do componente.

   ![Aplicação do banner novo](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   No momento, não há lógica de quando o banner será exibido. Nos próximos exercícios, corrigiremos esse problema.

   > Observe que o CSS para renderizar o banner foi fornecido como parte do projeto inicial e pode ser encontrado em: `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. Para obter mais detalhes, consulte o tutorial [Alterar estilo dos Componentes principais da CIF](style-cif-component.md).

## Personalizar a caixa de diálogo do Teaser do produto {#customize-dialog-product-teaser}

A seguir, personalizaremos a caixa de diálogo do Teaser do produto para permitir que um autor determine o intervalo de datas em que um produto é considerado &quot;novo&quot; e se o banner deve ser exibido. Faremos isso [personalizando a caixa de diálogo](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) do Teaser do produto como parte do projeto Acme Store.

1. Abra o projeto Acme Store no IDE de sua escolha e acesse `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`.

1. Abaixo da pasta `productteaser` adicione uma nova pasta chamada `_cq_dialog`. Adicione um novo arquivo à pasta `_cq_dialog` chamado `.content.xml`. Você deve ter a seguinte estrutura de arquivos:

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

   Acima, adicionamos dois campos como parte de uma nova guia e um só campo oculto.

   1. Caixa de seleção para exibir o símbolo “Novo”
   2. Campo de número para definir a idade máxima do produto
   3. Campo oculto para garantir que a idade máxima do produto seja salva como uma data longa (consulte [@TypeHint](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) para obter mais detalhes)

   As caixas de diálogo definidas como parte de um componente proxy herdam todos os campos de diálogo existentes com um recurso conhecido como [Sling Resource Merger](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/sling-resource-merger.html). Portanto, não é necessário redefinir os campos existentes que fazem parte do Teaser do produto.

1. Atualize `productteaser.html` e adicione um `data-sly-test` ao `<div>` para o símbolo. É um teste simples para decidir renderizar o símbolo se o usuário tiver marcado &quot;true&quot;.

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. Implante o código atualizado na instância local do AEM usando os recursos do IDE ou usando suas habilidades maven:

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. Retorne ao Teaser do produto e clique na *chave inglesa* para abrir a caixa de diálogo. A guia **Símbolo** será exibida com dois campos adicionais. A atualização desses campos manterá os valores no AEM. Você deve poder ativar/desativar o símbolo com a caixa de seleção:

   ![Ativar símbolo](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   Essa opção permite que o autor controle o tempo de exibição do símbolo. No entanto, seria ideal que o símbolo desaparecesse automaticamente assim que o produto atingisse um determinado período do dia, com base na entrada **Idade máxima do produto**. Para que isso aconteça, teremos de implementar alguma lógica de back-end.

## Atualizar o Modelo do Sling para o Teaser do produto {#updating-sling-model-product-teaser}

A seguir, estenderemos a lógica de negócios do Teaser do produto implementando um Modelo do Sling. Os [Modelos do Sling](https://sling.apache.org/documentation/bundles/models.html) são objetos POJO (Plain Old Java Objects) orientados por anotações que implementam qualquer lógica de negócios exigida pelo componente. Modelos do Sling são usados junto com os scripts HTL como parte do componente. Seguiremos o [padrão de delegação para Modelos do Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) para que possamos estender partes do modelo existente do Teaser do produto.

Os Modelos do Sling são implementados como Java e podem ser encontrados no módulo **principal** do projeto gerado.

1. Abra o projeto Acme Store no IDE de sua escolha e acesse o módulo **principal** em: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java** é uma interface Java pré-criada que estende a interface **ProductTeaser** da CIF.

1. Em seguida, abra o arquivo **MyProductTeaserImpl.java** localizado em: `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` é a classe de implementação da interface `MyProductTeaser`.

   Usando o [padrão de delegação para Modelos do Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models), podemos fazer referência à classe `ProductTeaser` por meio da propriedade `sling:resourceSuperType`:

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

1. Um dos pontos de extensão adicionais fornecidos pelos Componentes principais da CIF do AEM é o `AbstractProductRetriever`, que nos permite obter acesso a atributos específicos do produto. Adicione o seguinte método para inicializar o `AbstractProductRetriever` no método `init()`:

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

1. Vamos testar essas alterações modificando o preço formatado e substituindo a lógica em `getFormattedPrice()`. Faça as atualizações a seguir para formatar o preço com base no locale Alemanha (ou escolha um país diferente).

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

   Observe como o objeto `productRetriever` oferece acesso ao objeto `ProductInterface` por meio do método `fetchProduct()`. Você pode ver todos os métodos [disponíveis aqui](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java).

   > Observação: modificar o locale para Alemanha é apenas um exemplo divertido para ver a substituição. Na realidade, o ProductTeaser usa o [locale da página para determinar o formato](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173).

1. Em seguida, precisamos atualizar o **productteaser.html** no módulo **ui.apps** para consultar nosso novo Modelo do Sling em: `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
      ...
   ```

   Salve as alterações em `productteaser.html`.

1. Implante a base de código na instância local do AEM. Como foram feitas alterações nos módulos **ui.apps** e **core**, crie e implante o projeto da raiz:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Abra um navegador e acesse: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels). Este console mostra todos os Modelos do Sling registrados no sistema. Verifique se MyTeaserModelImpl foi implantado e está mapeado corretamente. Você deve ver algo como:

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. Por fim, acesse o local de criação do Teaser do produto para ver o preço com o formato de moeda alemão:

   ![Formato de preço atualizado](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## Implementar a lógica isShowBadge {#implement-isshowbadge}

Agora que tivemos a oportunidade de testar a substituição dos métodos do Modelo do Sling, vamos implementar a lógica de quando exibir o símbolo “novo”.

1. Retorne ao IDE e abra o arquivo **MyProductTeaser.java** em: `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`.

1. Adicione um novo método `isShowBadge()` à interface:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   }
   ```

   É um novo método que introduziremos para encapsular a lógica de mostrar ou não o símbolo.

1. Em seguida, abra novamente **MyProductTeaserImpl.java** em `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`.

1. A lógica de por quanto tempo o símbolo &quot;novo&quot; será exibido se baseia no atributo `created_at` do produto. Para ter acesso a esse atributo, precisamos estender a consulta **GraphQL** executada pelo ProductTeaser. Podemos fazer isso atualizando o método `init()` em **MyProductTeaserImpl.java**:

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

   Atualizar o método `extendProductQueryWith` é uma maneira eficiente de garantir que atributos de produto adicionais estejam disponíveis para o restante do modelo. Essa ação também minimiza o número de consultas executadas.

   >[!NOTE]
   >No código acima, estamos usando o `addCustomSimpleField` para recuperar a propriedade `created_at`. Isso ilustra como você pode consultar qualquer atributo personalizado que faça parte do esquema da Magento.
   >
   > No entanto, a propriedade `created_at` foi implementada como parte da [Interface do produto](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) e seria recomendável reutilizar o método como: `productRetriever.extendProductQueryWith(p -> p.createdAt());`. A maioria dos atributos de esquema encontrados com frequência foram implementados, portanto, use `addCustomSimpleField` somente para atributos verdadeiramente personalizados.

1. Em seguida, implementaremos o método `isShowBadge()`:

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

   No método acima, primeiro verificamos se o autor habilitou a funcionalidade do símbolo com a caixa de seleção. Em seguida, lemos o valor da propriedade `age` que é definida como parte da caixa de diálogo e que representa o número máximo de dias que um produto deve permanecer publicado até que o banner desapareça. Por fim, calculamos a idade do produto de acordo com a data `created_at`. Depois de comparar os dois valores, obtemos `true` para exibir o símbolo e `false` em todos os outros casos.

1. É necessário fazer mais uma adição ao script `productteaser.html` para chamar o método `isShowBadge()`. Abra o arquivo em `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`. Faça a seguinte atualização:

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. Implante a base de código na instância local do AEM. Como foram feitas alterações nos módulos **ui.apps** e **core**, crie e implante o projeto da raiz:

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. Retorne ao AEM e ao componente ProductTeaser e teste números diferentes para exibir a idade máxima do produto. Dependendo da idade do produto, talvez seja necessário digitar números muito grandes para que o símbolo seja exibido.

   ![Idade máxima do produto 999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. Por fim, pesquise nos logs do AEM para ver a declaração de log inserida na etapa 5 acima. Essa etapa deve imprimir o valor da propriedade `created_at` que vem da Magento. Você pode visualizar os logs do AEM abrindo o arquivo `error.log`. Esse arquivo está localizado debaixo de `crx-quickstart/logs/error.log` onde o jar do AEM foi instalado. Você pode ver um item de linha como o seguinte:

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   Agora você pode verificar se a lógica que implementamos está correta.

### Parabéns {#congratulations}

Você acabou de personalizar seu primeiro componente CIF do AEM. Baixe o [pacote da solução concluída aqui](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip).

## Recursos adicionais {#additional-resources}

* [Arquétipo do AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html)
* [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components)
* [Personalizar os Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [Personalizar os Componentes principais](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/customizing.html)
