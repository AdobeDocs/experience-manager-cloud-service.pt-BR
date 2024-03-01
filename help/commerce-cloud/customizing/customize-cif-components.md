---
title: Personalizar os Componentes principais da CIF
description: Aprenda a personalizar AEM componentes principais de CIF. A tutorial aborda como estender com segurança um CIF Core Componente para atender a requisitos específicos da empresa. Aprenda a estender um query GraphQL para retornar um atributo personalizado e exibir o novo atributo em um Componente CIF Core.
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 4933fc37-5890-47f5-aa09-425c999f0c91
source-git-commit: 05e4adb0d7ada0f7cea98858229484bf8cca0d16
workflow-type: tm+mt
source-wordcount: '2298'
ht-degree: 9%

---

# Personalizar AEM componentes principais de CIF {#customize-cif-components}

A variável [Projeto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) é uma base de código de referência para o uso de [Componentes principais do CIF](https://github.com/adobe/aem-core-cif-components). Neste tutorial, você estenderá ainda mais a [Teaser do produto](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) para exibir um atributo personalizado do Adobe Commerce. Você também aprenderá mais sobre a integração do GraphQL entre AEM e o Adobe Commerce e os ganchos de extensão fornecidos pelos Componentes principais do CIF.

>[!TIP]
>
> Use o [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) ao iniciar sua própria implementação comercial.

## O que você vai criar

A marca Venia começou recentemente a fabricar alguns produtos usando materiais sustentáveis e a empresa gostaria de exibir uma **Eco Friendly** como parte do Teaser do produto. Um novo atributo personalizado é criado no Adobe Commerce para indicar se um produto usa o **Eco amigável** material. Esse atributo personalizado é adicionado como parte da consulta do GraphQL e exibido no Teaser do produto de produtos especificados.

![Medalha ecologicamente correta Implementação final](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Pré-requisitos {#prerequisites}

Um ambiente de desenvolvimento local é necessário para concluir este tutorial. Esse ambiente inclui uma instância do AEM em execução que está configurada e conectada a uma instância do Adobe Commerce. Revise os requisitos e as etapas para [configurar um desenvolvimento local com o SDK as a Cloud Service do AEM](../develop.md). Para seguir o tutorial completamente, você precisa de permissão para adicionar [Atributos a um produto](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) no Adobe Commerce.

Você também precisa de um IDE do GraphQL, como o [GraphiQL](https://github.com/graphql/graphiql) ou uma extensão navegador para executar as amostras de código e tutoriais. Se você instalar uma extensão de navegador, verifique se ela pode definir cabeçalhos de solicitação. No Google Chrome, _Cliente Altair GraphQL_ O é uma extensão que pode fazer o trabalho.

## Clonar o projeto venia {#clone-venia-project}

Clonar o [Projeto](https://github.com/adobe/aem-cif-guides-venia) Venia e, em seguida, substitua os estilos padrão.

>[!NOTE]
>
> **Sinta grátis usar um projeto** existente (com base no AEM Project Archetype com CIF incluído) e pule esta seção.

1. Execute o seguinte comando git para que você possa clonar o projeto:

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. Crie e implante o projeto em uma instância local do AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Adicione as configurações OSGi necessárias para conectar a instância do AEM a uma instância do Adobe Commerce ou adicione as configurações ao projeto criado.

1. Nesse ponto, você deve ter uma versão funcional de uma loja conectada a uma instância do Adobe Commerce. Navegue até a `US` > `Home` página em: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Você verá que a loja está usando o tema Venia. Ao expandir o Menu principal da loja, você verá várias categorias, indicando que a conexão com o Adobe Commerce está funcionando.

   ![Loja configurada com o tema Venia](../assets/customize-cif-components/venia-store-configured.png)

## Criação do Teaser do produto {#author-product-teaser}

O Teaser do produto é apresentado em todo este tutorial. Como primeira etapa, adicione uma instância do Teaser do produto à página inicial para entender a funcionalidade da linha de base.

1. Acesse a **página inicial** do site: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. Insira um novo **Teaser do produto** no container do layout principal da página.

   ![Inserir Teaser do produto](../assets/customize-cif-components/product-teaser-add-component.png)

3. Expanda o painel lateral (se ainda não estiver sendo exibido) e na lista suspensa do localizador de ativos selecione **Produtos**. Essa lista deve exibir uma lista de produtos disponíveis de um Adobe Systems Comércio instância conectado. Selecione, **arraste e solte** um produto no **Teaser do produto** exibido na página.

   ![Arrastar e soltar Teaser do produto](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > Observação: você também pode configurar o produto exibido definindo o componente na caixa de diálogo (clicando na _chave inglesa_).

4. Agora você já deve estar vendo um produto no teaser. O nome e o preço do produto são atributos exibidos por padrão.

   ![Teaser do produto — estilo padrão](../assets/customize-cif-components/product-teaser-default-style.png)

## Adicionar um atributo personalizado no Adobe Systems Comércio {#add-custom-attribute}

Os produtos e os dados do produto exibidos em AEM são armazenados em Adobe Systems Comércio. Próximo adicionar um atributo para **o Eco Friendly** como parte do atributo de produto definido usando o Adobe Systems Comércio interface.

>[!TIP]
>
> Já possui um atributo Sim/Não **personalizado** como parte do conjunto de atributos do produto? Sinta grátis usar e pule esta seção.

1. Faça logon na sua instância do Adobe Commerce.
1. Navegue até **Catálogo** > **Produtos**.
1. Atualize o filtro de pesquisa para encontrar o **Produto configurável** usado quando adicionado ao componente Teaser no exercício anterior. Abra o produto no modo de edição.

   ![Pesquisar por produto Valeria](../assets/customize-cif-components/search-valeria-product.png)

1. No visualização do produto, clique **em Adicionar atributo** > **Criar Novo atributo**.
1. Preencha o **formulário Novo Atributo** com os seguintes valores (deixe as configurações padrão para outros valores)

   | Conjunto de campos | Rótulo do campo | Valor |
   | ----------------------------- | ------------------ | ---------------- |
   | Propriedades do atributo | Rotular do atributo | **Eco Friendly** |
   | Propriedades de atributos | Tipo de entrada do catálogo | **Sim/Não** |
   | Propriedades do Atributo Avançado | Código do atributo | **eco_friendly** |

   ![Formulário de atributo do Novo](../assets/customize-cif-components/attribute-new-form.png)

   Clique **Salvar Atributo** quando terminar.

1. Role até a parte inferior do produto e expanda o **cabeçalho Atributos** . Você deverá ver o novo **campo Eco Friendly** . Alterne para **Sim**.

   ![Alternar para sim](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **Salvar** as alterações no produto.

   >[!TIP]
   >
   > Mais detalhes sobre gerenciamento [Os atributos do produto podem ser encontrados no guia do usuário do Adobe Commerce](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. Navegue até **Sistema** > **Ferramentas** > **Gerenciamento de cache**. Como foi feita uma atualização no esquema de dados, você deve invalidar alguns dos Tipos de cache no Adobe Commerce.
1. Marque a caixa ao lado de **Configuração** e enviar o tipo de cache para **Atualizar**

   ![Tipo de cache de configuração Atualizar](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > Mais detalhes sobre [o Gerenciamento de cache podem ser encontrados no guia](https://docs.magento.com/user-guide/system/cache-management.html) de Adobe Systems Comércio usuário.

## Usar um IDE do GraphQL para verificar o atributo {#use-graphql-ide}

Antes de entrar no AEM código, é útil explorar a Visão geral](https://devdocs.magento.com/guides/v2.4/graphql/) do [GraphQL usando um GraphQL IDE. A integração do Adobe Systems Comércio com o AEM é feita principalmente por meio de uma série de queries GraphQL. A compreensão e modificação das consultas GraphQL é uma das principais maneiras pelas quais os Componentes principais de CIF podem ser estendidos.

Em seguida, use um GraphQL IDE para verificar se o `eco_friendly` O atributo foi adicionado ao conjunto de atributos do produto. As capturas de tela deste tutorial estão usando o _Cliente Altair GraphQL_ Extensão do Google Chrome.

1. Abra o GraphQL IDE e digite a URL `http://<commerce-server>/graphql` na barra de URL do IDE ou da extensão.
2. Adicione os seguintes [produtos query](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) onde `YOUR_SKU` está a **SKU** do produto usado no exercício anterior:

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

3. Execute a query e receberá uma resposta curtir:

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

   ![Resposta de amostra graphQL](../assets/customize-cif-components/sample-graphql-query.png)

   O valor de **Sim** é um número inteiro de **1**. Esse valor é útil ao escrever a consulta do GraphQL em Java™.

   >[!TIP]
   >
   > Leia a documentação mais detalhada sobre [Adobe Commerce GraphQL aqui](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## Atualizar o Modelo do Sling para o Teaser do produto {#updating-sling-model-product-teaser}

Em seguida, estenda a lógica de negócios do Teaser do produto implementando um Modelo do Sling. [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html) são objetos POJO (Plain Old Java™ Objects) orientados por anotações que implementam a lógica de negócios exigida pelo componente. Os Modelos do Sling são usados com os scripts HTL como parte do componente. Siga as [padrão de delegação para Modelos do Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) para que você possa estender partes do modelo existente do Teaser do produto.

Os Modelos do Sling são implementados como Java™ e podem ser encontrados no **core** módulo do projeto gerado.

Uso [o IDE de sua escolha](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) para importar o projeto Venia. As capturas de tela usadas são do [IDE do Visual Studio Code](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code).

1. No IDE, navegue sob o **core** módulo para: `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![IDE do local principal](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` é uma interface do Java™ que estende a interface do CIF [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) .

   Já foi adicionado um novo método chamado `isShowBadge()` para exibir um selo se o produto for considerado &quot;Novo&quot;.

1. Adicionar `isEcoFriendly()` à interface:

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   Esse novo método é introduzido para encapsular a lógica para indicar se o produto tem a função `eco_friendly` atributo definido como **Sim** ou **Não**.

1. Em seguida, inspecione o `MyProductTeaserImpl.java` em `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   A variável [padrão de delegação para Modelos do Sling](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) permite `MyProductTeaserImpl` para referência `ProductTeaser` por meio da `sling:resourceSuperType` propriedade:

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   Para os métodos que não deseja substituir ou alterar, você pode retornar o valor que retorna `ProductTeaser` . Por exemplo:

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   Esse método minimiza a quantidade de código Java™ que um implementação deve gravar.

1. Um dos pontos de extensão extras fornecidos AEM Componentes principais de CIF é o `AbstractProductRetriever` que fornece acesso a atributos específicos do produto. Inspect o `initModel()` método:

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to initialize the productRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   O `@PostConstruct` anotação garante que esse método seja chamado quando o Modelo de Sling é inicializado.

   Observe que a consulta do GraphQL do produto já foi estendida usando o `extendProductQueryWith` método para recuperar o adicional `created_at` atributo. Esse atributo é usado posteriormente como parte da variável `isShowBadge()` método.

1. Atualize a consulta do GraphQL para incluir a `eco_friendly` atributo na consulta parcial:

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   Adicionar ao `extendProductQueryWith` Esse método é uma maneira avançada de garantir que atributos de produto adicionais estejam disponíveis para o restante do modelo. Essa ação também minimiza o número de consultas executadas.

   No código acima, a variável`addCustomSimpleField` é usado para recuperar o `eco_friendly` atributo. Este atributo ilustra como é possível query para quaisquer atributos personalizados que fazem parte da Adobe Systems Comércio schema.

   >[!NOTE]
   >
   > O `createdAt()` método foi implementado como parte da interface](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) do [produto. A maioria dos atributos de esquema encontrados com frequência foram implementados, portanto, use `addCustomSimpleField` somente para atributos verdadeiramente personalizados.

1. Adicione um logger para que você possa depurar o código Java™:

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

   No método acima, a variável `productRetriever` é usado para buscar o produto e a variável `getAsInteger()` é usado para obter o valor do `eco_friendly` atributo. Com base nas consultas do GraphQL executadas anteriormente, você sabe que o valor esperado quando a variável `eco_friendly` atributo está definido como &quot;**Sim**&quot; é na verdade um número inteiro de **1**.

   Agora que o Modelo Sling foi atualizado, a marcação do Componente deve ser atualizada para realmente exibir um indicador de **Eco Friendly** com base no Modelo Sling.

## Personalização da marcação do teaser do produto {#customize-markup-product-teaser}

Uma extensão comum de componentes do AEM é modificar a marcação gerada pelo componente. Essa edição é feita substituindo o [script](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR) HTL que o componente usa para renderizar sua marcação. O Idioma de modelo HTML (HTL) é uma linguagem de modelagem leve que AEM componentes usam para renderizar dinamicamente a marcação com base na conteúdo criada, permitindo que os componentes sejam reutilizados. O Teaser do produto, por exemplo, pode ser reutilizado várias vezes para exibir produtos diferentes.

Nesse caso, você deseja renderizar uma banner sobre a teaser para indicar que o produto é &quot;Eco Friendly&quot; com base em um atributo personalizado. O padrão de design para [personalizar a marcação](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) de um componente é padrão para todos os componentes AEM, não apenas para os componentes principais AEM CIF.

>[!NOTE]
>
> Se você personalizar um componente usando o produto CIF e categoria seletores, curtir este Teaser de produto ou o componente página CIF, certifique-se de incluir a clientlib necessária `cif.shell.picker` para as caixas de diálogo do componente. Consulte [Uso do produto CIF e categoria seletor](use-cif-pickers.md) para obter detalhes.

1. No IDE, navegue e expanda a janela `ui.apps` e expandir a hierarquia de pastas para: `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` e inspecionar o `.content.xml` arquivo.

   ![Teaser do produto ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   A definição de componente acima é para o Teaser do produto em seu projeto. Observe a propriedade `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. Esta propriedade é um exemplo de criação de um [Componente proxy](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components). AEM Em vez de copiar e colar os scripts HTL do Teaser do produto dos Componentes principais do CIF, você pode usar o `sling:resourceSuperType` para herdar toda a funcionalidade.

1. Abra o arquivo `productteaser.html`. Este arquivo é uma cópia do `productteaser.html` arquivo do [Teaser do produto CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html).

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   Observe que o Modelo Sling para `MyProductTeaser` é usada e atribuída à `product` variável.

1. Modificar `productteaser.html` para que você possa chamar o `isEcoFriendly` método aplicado no exercício anterior:

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   Ao chamar um método Modelo do Sling no HTL, a variável `get` e `is` parte do método é descartada e a primeira letra é em minúsculas. Então `isShowBadge()` torna-se `.showBadge` e `isEcoFriendly` torna-se `.ecoFriendly`. Com base no valor booleano retornado de `.isEcoFriendly()` determina se a variável `<span>Eco Friendly</span>` é exibido.

   Mais informações sobre `data-sly-test` e outras [declarações de blocos HTL podem ser encontradas aqui](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html).

1. Salvar as mudanças e implantar as atualizações para AEM usando suas habilidades maven, a partir de um terminal de linha de comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Abra uma nova janela do navegador e navegue até a AEM e no console **osGi**> **Status** > **Modelos** Sling: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. Search e `MyProductTeaserImpl` você verá uma linha curtir o seguinte:

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   Essa linha indica que o Modelo de Sling foi implantado e mapeado corretamente para o componente correto.

1. Atualize para o **Página inicial Venia** em [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) onde o Teaser do produto foi adicionado.

   ![Mensagem ecologicamente correta exibida](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   Se o produto tiver o `eco_friendly` atributo definido como **Sim**, você verá o texto &quot;Eco Friendly&quot; no página. Tente alternar para produtos diferentes para ver a mudança de comportamento.

1. Próximo abra o AEM `error.log` para ver as declarações de log adicionadas. O `error.log` está em `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   Search os logs do AEM para ver as declarações de log adicionadas no Modelo do Sling:

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > Você também pode ver alguns rastreamentos de pilha se o produto usado no teaser não tiver o `eco_friendly` atributo como parte de seu conjunto de atributos.

## Adicione estilos para o selo ecológico {#add-styles}

Nesse ponto, a lógica de quando exibir a variável **Eco Friendly** o símbolo está funcionando, no entanto, o texto sem formatação pode usar alguns estilos. Em seguida, adicione um ícone e estilos à `ui.frontend` módulo para concluir a implementação.

1. Baixe o [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) arquivo. Esse arquivo é usado como o **Eco Friendly** selo.
1. Retorne ao IDE e navegue até o `ui.frontend` pasta.
1. Adicione o `eco_friendly.svg` arquivo para o `ui.frontend/src/main/resources/images` pasta:

   ![SVG compatível com Eco adicionado](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. Abra o arquivo `productteaser.scss` em `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. Adicione as seguintes regras Sass dentro do `.productteaser` classe:

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
   > Confira [Estilização dos Componentes principais do CIF](./style-cif-component.md) para obter mais detalhes sobre fluxos de trabalho de front-end.

1. Salvar as mudanças e implantar as atualizações para AEM usando suas habilidades maven, a partir de um terminal de linha de comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. Atualize para o **Página inicial Venia** em [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) onde o Teaser do produto foi adicionado.

   ![Medalha ecologicamente correta Implementação final](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## Parabéns {#congratulations}

AEM Você personalizou seu primeiro componente CIF! Baixe o [arquivos de solução concluídos aqui](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## Desafio bônus {#bonus-challenge}

Revise a funcionalidade do **selo Novo** que já foi implementado na Teaser do produto. Tente adicionar uma caixa de seleção extra para que os autores controlem quando o **selo Eco Friendly** deve ser exibido. Atualize a caixa de diálogo do componente em `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![Desafio Novo implementação de selos](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## Recursos adicionais {#additional-resources}

- [Arquétipo do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR)
- [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components)
- [Personalizar os Componentes principais da CIF do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/customize-cif-components.html)
- [Personalizar os Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=pt-BR)
- [Introdução ao AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR)
- [Uso do seletor de categoria e produto para CIF](use-cif-pickers.md)
