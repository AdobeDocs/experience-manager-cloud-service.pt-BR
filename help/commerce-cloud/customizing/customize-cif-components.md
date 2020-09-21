---
title: Personalizar os Componentes principais da CIF
description: Saiba como personalizar AEM componentes principais CIF. O tutorial aborda como estender com segurança um Componente principal CIF para atender aos requisitos específicos da empresa. Saiba como estender um query GraphQL para retornar um atributo personalizado e exibir o novo atributo em um Componente principal CIF.
sub-product: comércio
topics: development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
kt: 4279
thumbnail: 4279-customize-cif.jpg
translation-type: tm+mt
source-git-commit: a88595f3fab37f4406e607cb104a27de51cdbef6
workflow-type: tm+mt
source-wordcount: '2550'
ht-degree: 30%

---


# Personalizar os Componentes principais da CIF do AEM{#customize-cif-components}

O [CIF Projeto](https://github.com/adobe/aem-cif-guides-venia) Venia é uma base de códigos de referência para a utilização dos componentes [principais](https://github.com/adobe/aem-core-cif-components)CIF. Neste tutorial, você estenderá ainda mais o componente Teaser [do](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) produto para exibir um atributo personalizado do Magento. Você também aprenderá mais sobre a integração do GraphQL entre o AEM e o Magento e os ganchos de extensão fornecidos pelos Componentes principais CIF.

>[!TIP]
>
> Use o arquétipo [AEM Projeto](https://github.com/adobe/aem-project-archetype) ao iniciar sua própria implementação de comércio.

## O que você vai criar

A marca Venia começou recentemente a fabricar alguns produtos usando materiais sustentáveis e a empresa gostaria de exibir um crachá **eco-amigável** como parte do Teaser do Produto. Um novo atributo personalizado será criado no Magento para indicar se um produto usa o material **ecológico** . Esse atributo personalizado será então adicionado como parte do query GraphQL e exibido no Teaser de produto para produtos especificados.

![Implementação final do selo ecológico](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Pré-requisitos {#prerequisites}

É necessário um ambiente de desenvolvimento local para concluir este tutorial. Isso inclui uma instância em execução de AEM configurada e conectada a uma instância Magento. Revise os requisitos e as etapas para [configurar um desenvolvimento local com AEM como SDK](../develop.md)Cloud Service. Para seguir o tutorial completamente, você precisará de permissões para adicionar [Atributos a um Produto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) no Magento.

Você também precisará do GraphQL IDE, como o [GraphiQL](https://github.com/graphql/graphiql) , ou de uma extensão do navegador para executar as amostras de código e os tutoriais. Se você instalar uma extensão do navegador, verifique se ele tem a capacidade de definir cabeçalhos de solicitação. No Google Chrome, o [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) é uma extensão que pode fazer o trabalho.

## Clonar o projeto Venia {#clone-venia-project}

Vamos clonar o Projeto [](https://github.com/adobe/aem-cif-guides-venia) Venia e depois substituir os estilos padrão.

>[!NOTE]
>
> **Sinta-se à vontade para usar um projeto** existente (com base no AEM Project Archetype com CIF incluído) e ignore esta seção.

1. Execute o seguinte comando git para clonar o projeto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crie e implante o projeto em uma instância local do AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Adicione as configurações OSGi necessárias para conectar a instância do AEM a uma instância da Magento ou adicione as configurações ao projeto recém-criado.

1. Nesta etapa, já deve estar funcionando uma versão de loja conectada a uma instância da Magento. Navigate to the `US` > `Home` page at: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Você verá que a loja está usando o tema Venia. Ao expandir o Menu principal da loja você verá várias categorias, que é um sinal de que a conexão com a Magento está funcionando.

   ![Storefront Configurado com o Tema de Venia](../assets/customize-cif-components/venia-store-configured.png)

## Criação do Teaser do produto {#author-product-teaser}

O componente Teaser do produto será estendido por todo este tutorial. Como primeira etapa, adicione uma nova instância do Teaser de produto ao Home page para entender a funcionalidade da linha de base.

1. Acesse a **página inicial** do site: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Insira um novo **Teaser do produto** no container do layout principal da página.

   ![Inserir Teaser do produto](../assets/customize-cif-components/product-teaser-add-component.png)

3. Expanda o painel lateral (se ainda não estiver sendo exibido) e na lista suspensa do localizador de ativos selecione **Produtos**. Essa ação deve exibir uma lista de produtos disponíveis em uma instância conectada da Magento. Selecione, **arraste e solte** um produto no **Teaser do produto** exibido na página.

   ![Arrastar e soltar Teaser do produto](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > Observação: você também pode configurar o produto exibido definindo o componente na caixa de diálogo (clicando na *chave inglesa*).

4. Agora você já deve estar vendo um produto no teaser. O nome e o preço do produto são atributos exibidos por padrão.

   ![Teaser do produto — estilo padrão](../assets/customize-cif-components/product-teaser-default-style.png)

## Adicionar um atributo personalizado no Magento {#add-custom-attribute}

Os produtos e os dados do produto exibidos no AEM são armazenados no Magento. Em seguida, adicione um novo atributo para **eco amigável** como parte do conjunto de atributos do produto usando a interface do Magento.

>[!TIP]
>
> Já tem um atributo personalizado **Sim/Não** como parte do conjunto de atributos do produto? Sinta-se à vontade para usá-lo e ignore esta seção.

1. Faça logon na sua instância do Magento.
1. Navegue até **Catálogo** > **Produtos**.
1. Atualize o filtro de pesquisa para localizar o Produto **** configurável usado quando adicionado ao componente Teaser no exercício anterior. Abra o produto no modo de edição.

   ![Busca pelo produto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. Na visualização do produto, clique em **Adicionar atributo** > **Criar novo atributo**.
1. Preencha o formulário **Novo atributo** com os seguintes valores (deixe as configurações padrão para outros valores)

   | Conjunto de campos | Rótulo do campo | Valor |
   |-----------|-------------|---------|
   | Propriedades do atributo | Rótulo do atributo | **Ecológico** |
   | Propriedades do atributo | Tipo de entrada do catálogo | **Sim/Não** |
   | Propriedades avançadas de atributos | Código do atributo | **eco_friendly** |

   ![Novo formulário de atributo](../assets/customize-cif-components/attribute-new-form.png)

   Clique em **Salvar atributo** ao terminar.

1. Role até a parte inferior do produto e expanda o cabeçalho **Atributos** . Vocês deveriam ver o novo campo **eco-amigável** . Alterne a alternância para **Sim**.

   ![Alternar alternância para yes](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **Salve** as alterações no produto.

   >[!TIP]
   >
   > Para obter mais detalhes sobre o gerenciamento de atributos [do produto, consulte o guia](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)do usuário do Magento.

1. Navegue até **Sistema** > **Ferramentas** > Gerenciamento **de** cache. Como foi feita uma atualização no schema de dados, precisamos invalidar alguns dos tipos de cache no Magento.
1. Marque a caixa ao lado de **Configuração** e envie o tipo de cache para **Atualizar**

   ![Atualizar Tipo de Cache de Configuração](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > Mais detalhes sobre o Gerenciamento de [cache podem ser encontrados no guia](https://docs.magento.com/user-guide/system/cache-management.html)do usuário do Magento.

## Usar um GraphQL IDE para verificar o atributo {#use-graphql-ide}

Antes de pular para AEM código, é útil explorar o [Magento GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) usando um GraphQL IDE. A integração do Magento com o AEM é feita principalmente por meio de uma série de query GraphQL. Compreender e modificar os query GraphQL é uma das principais maneiras pelas quais os Componentes Principais CIF podem ser estendidos.

Em seguida, use um GraphQL IDE para verificar se o `eco_friendly` atributo foi adicionado ao conjunto de atributos do produto. As capturas de tela neste tutorial estão usando o [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. Abra o GraphQL IDE e insira o URL `http://<magento-server>/graphql` na barra de URL do IDE ou da extensão.
2. Adicione o seguinte query [de](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) produtos, onde `YOUR_SKU` é o **SKU** do produto usado no exercício anterior:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. Execute o query e você deverá obter uma resposta como a seguinte:

   ```json
   {
   "data": {
       "products": {
           "items": [
               {
               "name": "Valeria Two-Layer Tank",
               "sku": "VT11",
               "eco_friendly": 1
               }
           ]
           }
       }
   }
   ```

   ![Exemplo de resposta GraphQL](../assets/customize-cif-components/sample-graphql-query.png)

   Observe que o valor de **Yes** é um número inteiro de **1**. Isso será útil quando gravarmos o query GraphQL no Java.

   >[!TIP]
   >
   > Documentação mais detalhada sobre o [Magento GraphQL pode ser encontrada aqui](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Update the Sling Model for the Product Teaser {#updating-sling-model-product-teaser}

A seguir, estenderemos a lógica de negócios do Teaser do produto implementando um Modelo do Sling. Os [Modelos do Sling](https://sling.apache.org/documentation/bundles/models.html) são objetos POJO (Plain Old Java Objects) orientados por anotações que implementam qualquer lógica de negócios exigida pelo componente. Modelos do Sling são usados junto com os scripts HTL como parte do componente. Seguiremos o [padrão de delegação para Modelos do Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) para que possamos estender partes do modelo existente do Teaser do produto.

Os Modelos do Sling são implementados como Java e podem ser encontrados no módulo **principal** do projeto gerado.

Use [o IDE de sua escolha](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) para importar o projeto Venia. Capturas de tela usadas são do código IDE [do](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)Visual Studio.

1. No IDE, navegue sob o módulo **principal** para: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE de localização principal](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` é uma interface Java que estende a interface CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) .

   Já foi adicionado um novo método chamado `isShowBadge()` para exibir um crachá se o produto for considerado &quot;Novo&quot;.

1. Adicione um novo método `isEcoFriendly()` à interface:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   Este é um novo método que introduziremos para encapsular a lógica para indicar se o produto tem o `eco_friendly` atributo definido como **Sim** ou **Não**.

1. Em seguida, inspecione o `MyProductTeaserImpl.java` em `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   O padrão de [delegação para Modelos](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) Sling permite `MyProductTeaserImpl` fazer referência ao `ProductTeaser` modelo por meio da `sling:resourceSuperType` propriedade:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Para todos os métodos que não queremos substituir ou alterar, podemos simplesmente retornar o valor que o `ProductTeaser` retorna. Por exemplo:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Isso minimiza a quantidade de código Java que uma implementação precisa gravar.

1. One of the extra extension points provided by AEM CIF Core Components is the `AbstractProductRetriever` which provides access to specific product attributes. Inspect o `initModel()` método:

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
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   A `@PostConstruct` anotação garante que esse método seja chamado assim que o Modelo Sling for inicializado.

   Observe que o query GraphQL do produto já foi estendido usando o `extendProductQueryWith` método para recuperar o `created_at` atributo adicional. Esse atributo é usado posteriormente como parte do `isShowBadge()` método.

1. Atualize o query GraphQL para incluir o `eco_friendly` atributo no query parcial:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p ->
                productRetriever.extendProductQueryWith(p -> p
                   .createdAt()
                   .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
               );
           );
       }
   }
   ```

   Atualizar o método `extendProductQueryWith` é uma maneira eficiente de garantir que atributos de produto adicionais estejam disponíveis para o restante do modelo. Essa ação também minimiza o número de consultas executadas.

   No código acima,`addCustomSimpleField` é usado para recuperar o `eco_friendly` atributo. Isso ilustra como você pode consultar qualquer atributo personalizado que faça parte do esquema da Magento.

   >[!NOTE]
   >
   > O `createdAt()` método foi implementado como parte da Interface [do](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)produto. A maioria dos atributos de esquema encontrados com frequência foram implementados, portanto, use `addCustomSimpleField` somente para atributos verdadeiramente personalizados.

1. Adicione um agente de log para ajudar a depurar o código Java:

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. Em seguida, implemente o `isEcoFriendly()` método:

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   No método acima, `productRetriever` é usado para buscar o produto e o `getAsInteger()` método é usado para obter o valor do `eco_friendly` atributo. Com base nos query GraphQL executados anteriormente, sabemos que o valor esperado quando o `eco_friendly` atributo é definido como &quot;**Sim**&quot; é na verdade um número inteiro de **1**.

   Agora que o Modelo Sling foi atualizado, a marcação Componente precisa ser atualizada para realmente exibir um indicador de **eco amigável** com base no Modelo Sling.

## Personalização da marcação do Teaser do produto {#customize-markup-product-teaser}

Uma extensão comum de componentes do AEM é modificar a marcação gerada pelo componente. Essa modificação é feita substituindo o [script HTL](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html) que o componente usa para renderizar sua marcação. A Linguagem de modelo HTML (HTL) é uma linguagem de modelo leve que os componentes do AEM usam para renderizar dinamicamente a marcação com base no conteúdo criado, permitindo que os componentes sejam reutilizados. O Teaser do produto, por exemplo, pode ser reutilizado várias vezes para exibir produtos diferentes.

Em nosso caso, queremos renderizar um banner sobre o teaser para indicar que o produto é &quot;Ecológico&quot; com base em um atributo personalizado. O padrão de design para [personalizar a marcação](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de um componente é, na verdade, padrão para todos os componentes do AEM, não apenas para os Componentes principais da CIF do AEM.

1. In the IDE, navigate and expand the `ui.apps` module and expand the folder hierarchy to: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` and inspect the `.content.xml` file.

   ![User.apps do Teaser do produto](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   Veja acima a definição de componente para o Teaser do produto em nosso projeto. Observe a propriedade `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Este é um exemplo de criação de um [componente Proxy](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/get-started/using.html#create-proxy-components). Em vez de copiar e colar todos os scripts HTL do Teaser do produto dos Componentes principais da CIF do AEM, podemos usar o `sling:resourceSuperType` para herdar toda a funcionalidade. 

1. Open the file `productteaser.html`. Esta é uma cópia do `productteaser.html` arquivo do [CIF Product Teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
       data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
       data-sly-use.actionsTpl="actions.html"
       data-sly-test.isConfigured="${properties.selection}"
       data-sly-test.hasProduct="${product.url}">
   ```

   Observe que o Modelo Sling para `MyProductTeaser` é usado e atribuído à `product` variável.

1. Modifique `productteaser.html` para fazer uma chamada para o `isEcoFriendly` método implementado no exercício anterior:

   ```html
   ...
   <div data-sly-test="${isConfigured && hasProduct}" class="item__root" data-cmp-is="productteaser" data-virtual="${product.virtualProduct}">
       <div data-sly-test="${product.showBadge}" class="item__badge">
           <span>${properties.text || 'New'}</span>
       </div>
       <!--/* Insert call to Eco Friendly here */-->
       <div data-sly-test="${product.ecoFriendly}" class="item__eco">
           <span>Eco Friendly</span>
       </div>
   ...
   ```

   Ao chamar um método Sling Model em HTL, a parte `get` e `is` do método é solta e a primeira letra é em minúsculas. Então `isShowBadge()` se torna `.showBadge` e `isEcoFriendly` se torna `.ecoFriendly`. Com base no valor booliano de `.isEcoFriendly()` que retornou determina se o `<span>Eco Friendly</span>` é exibido.

   Mais informações sobre `data-sly-test` e outras declarações de bloco [HTL podem ser encontradas aqui](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test).

1. Salve as alterações e implante as atualizações para AEM usando suas habilidades Maven, a partir de um terminal de linha de comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Abra uma nova janela do navegador e navegue até AEM e o console **do** OSGi > **Status** > Modelos **** Sling: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Procure `MyProductTeaserImpl` e você deverá ver uma linha como a seguinte:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Isso indica que o Modelo Sling foi implantado e mapeado corretamente para o componente correto.

1. Atualize para o Home page **Venia em** http://localhost:4502/editor.html/content/venia/us/en.html [](http://localhost:4502/editor.html/content/venia/us/en.html) , onde o Teaser do produto foi adicionado.

   ![Aparece a mensagem eco-amigável](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Se o produto tiver o `eco_friendly` atributo definido como **Sim**, você deverá ver o texto &quot;Ecológico&quot; na página. Tente alternar para produtos diferentes para ver a mudança de comportamento.

1. Em seguida, abra o AEM `error.log` para ver as declarações de log que adicionamos. O `error.log` está localizado em `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Pesquise nos registros de AEM para ver as declarações de log adicionadas no Sling Model:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > Você também pode ver alguns rastreamentos de pilha se o produto usado no teaser não tiver o `eco_friendly` atributo como parte do conjunto de atributos.

## Adicionar estilos ao selo eco-amigável {#add-styles}

Nesse ponto, a lógica para quando a exibição do crachá **eco-amigável** está funcionando, no entanto, o texto sem formatação pode usar alguns estilos. Em seguida, adicione um ícone e estilos ao `ui.frontend` módulo para concluir a implementação.

1. Baixe o arquivo [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) . Isso será usado como o crachá **eco-amigável** .
1. Retorne ao IDE e navegue até a `ui.frontend` pasta.
1. Adicione o `eco_friendly.svg` arquivo à `ui.frontend/src/main/resources/images` pasta:

   ![SVG eco-amigável adicionado](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Open the file `productteaser.scss` at `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Adicione as seguintes regras Sass dentro da `.productteaser` classe:

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg'); 
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > Consulte [Styling CIF Core Components](./style-cif-component.md) para obter mais detalhes sobre os workflows front-end.

1. Salve as alterações e implante as atualizações para AEM usando suas habilidades Maven, a partir de um terminal de linha de comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. Atualize para o Home page **Venia em** http://localhost:4502/editor.html/content/venia/us/en.html [](http://localhost:4502/editor.html/content/venia/us/en.html) , onde o Teaser do produto foi adicionado.

   ![Implementação final do selo ecológico](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Parabéns {#congratulations}

Você acabou de personalizar seu primeiro componente CIF do AEM. Download the [finished solution files here](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Desafio extra {#bonus-challenge}

Analise a funcionalidade do **novo** selo que já foi implementado no Teaser do produto. Tente adicionar uma caixa de seleção adicional para que os autores controlem quando o selo **eco-amigável** deve ser exibido. Será necessário atualizar a caixa de diálogo do componente em `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Novo desafio de implementação de emblema](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Recursos adicionais {#additional-resources}

* [Arquétipo do AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html)
* [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components)
* [Personalizar os Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [Personalizar os Componentes principais](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/customizing.html)
* [Introdução ao AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
