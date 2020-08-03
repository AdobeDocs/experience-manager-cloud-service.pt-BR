---
title: Estilo AEM componentes principais CIF
description: Estilo AEM componentes principais CIF
translation-type: tm+mt
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 1%

---


# Estilo AEM componentes principais CIF {#style-aem-cif-core-components}

O arquétipo [de projeto](https://github.com/adobe/aem-cif-project-archetype) CIF cria um projeto CIF de Adobe Experience Manager (AEM) mínimo como ponto de partida para projetos de clientes que usam [AEM componentes](https://github.com/adobe/aem-core-cif-components)principais CIF. Um estilo padrão, conhecido como a marca Venia, é aplicado inicialmente ao site. Neste tutorial, você inspecionará um novo projeto AEM CIF, gerado pelo arquétipo e compreenderá como CSS e JavaScript usados pelos componentes AEM CIF Core são organizados. Você também criará um novo estilo usando o CSS para substituir o estilo padrão do componente Teaser do produto.

![O que você criará](/help/commerce-cloud/assets/style-cif-component/what-you-will-build.png)

>[!NOTE]
> Um novo estilo será implementado para o componente Teaser do produto que se assemelha a um cartão.

## Pré-requisitos {#prerequisites}

As seguintes ferramentas e tecnologias são necessárias:

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html) ou [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html) (somente AEM 6.5+)
* [Apache Maven](https://maven.apache.org/) (3.3.9 ou mais recente)
* Adobe Experience Manager (instância local)
   * [AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/introduction/technical-requirements.html)
   * [AEM 6.4.4+](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/sp-release-notes.html)
* Magento executando uma [versão compatível com o arquétipo](https://github.com/adobe/aem-cif-project-archetype#requirements)

## Gerar um projeto {#generate-project}

Geraremos um novo projeto AEM CIF usando o arquétipo [CIF do projeto](https://github.com/adobe/aem-cif-project-archetype) e substituiremos os estilos padrão.

**Sinta-se à vontade para usar um projeto** existente (com base no CIF Project Archetype) e ignore esta seção.

1. Determine a versão mais recente do CIF Project Archetype exibindo [a versão mais recente no GitHub](https://github.com/adobe/aem-cif-project-archetype/releases/latest). Na próxima etapa, substitua `x.y.z` pela versão mais recente.

1. Execute o seguinte comando Maven para gerar um novo projeto no modo [de](https://maven.apache.org/archetype/maven-archetype-plugin/examples/generate-batch.html)lote.

   ```terminal
   mvn archetype:generate -B \
       -DarchetypeGroupId="com.adobe.commerce.cif" \
       -DarchetypeArtifactId="cif-project-archetype" \
       -DarchetypeVersion=x.y.z \
       -DgroupId="com.acme.cif" \
       -DartifactId="acme-store" \
       -Dversion=0.0.1-SNAPSHOT \
       -Dpackage="com.acme.cif" \
       -DappsFolderName="acme" \
       -DartifactName="Acme Store" \
       -DcontentFolderName="acme" \
       -DpackageGroup="acme" \
       -DsiteName="Acme Store" \
       -DoptionAemVersion=6.5.0 \
       -DoptionIncludeExamples=y \
       -DoptionEmbedConnector=y
   ```

1. Crie e implante o projeto em uma instância local do AEM:

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. Adicione as configurações OSGi necessárias para conectar sua instância de AEM a uma instância de Magento ou adicione as configurações ao projeto recém-criado.

1. Neste ponto, você deve ter uma versão em funcionamento de uma vitrine que esteja conectada a uma instância Magento. Navegue até a página `US` > `Home` em: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Vocês devem ver que a vitrine está usando o tema de Venia. Ao expandir o Menu principal da frente de loja, você deve ver várias categorias, indicando que o Magento de conexão está funcionando.

   ![Vitrine configurada com o tema Venia](/help/commerce-cloud/assets/style-cif-component/acme-store-configured.png)

## Introdução às bibliotecas do cliente {#introduction-to-client-libraries}

O CSS e o JavaScript responsáveis pela renderização do tema/estilos da vitrine são gerenciados em AEM por uma biblioteca [do](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html) cliente ou clientlibs para abreviação. As bibliotecas de clientes fornecem um mecanismo para organizar o CSS e o Javascript no código de um projeto e, em seguida, são entregues na página.

A maneira de aplicar estilos específicos da marca AEM componentes principais CIF é adicionando e substituindo o CSS gerenciado por essas bibliotecas clientes. Entender como as bibliotecas do cliente são estruturadas e incluídas na página é essencial.

### Bibliotecas do cliente do projeto {#project-client-libraries}

Em seguida, inspecionaremos as bibliotecas do cliente geradas automaticamente pelo tipo de arquivo. Use o IDE de sua escolha para [importar o projeto gerado no exercício](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)anterior.

1. Navegue e expanda o módulo **ui.apps** e expanda a hierarquia de pastas para: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs`:

   ![ui.apps clientlibs](/help/commerce-cloud/assets/style-cif-component/ui-apps-clientli-folder.png)

   Há duas pastas abaixo, **clientlib-base** e **tema**.

1. **clientlib-base** - esta é uma biblioteca de cliente vazia que simplesmente incorpora as dependências necessárias de [AEM Componentes](https://docs.adobe.com/content/help/br/experience-manager-core-components/using/introduction.html)principais.

   ![Clientlib-base](/help/commerce-cloud/assets/style-cif-component/clientlib-base-folderhierarchy.png)

   Abaixo está a definição XML de **clientlib-base** (o `.content.xml` arquivo):

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.wcm.base]"
       embed="[core.wcm.components.accordion.v1,core.wcm.components.tabs.v1,core.wcm.components.carousel.v1,core.wcm.components.image.v2,core.wcm.components.breadcrumb.v2,core.wcm.components.search.v1,core.wcm.components.form.text.v2]"/>
   ```

   `acme.wcm.base` é a categoria desta biblioteca de cliente. Pense em uma categoria como uma etiqueta. Isso será usado para incluir ou incorporar a biblioteca na página.

   Observe a `embed` propriedade e a matriz de outras categorias clientlib. Cada uma dessas categorias representa uma biblioteca de clientes. Por exemplo, `core.wcm.components.accordion.v1` inclui o javascript necessário para que o componente [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/accordion.html) Acordeão funcione.

   Ao usar as `embed` propriedades e `categories` as bibliotecas do cliente podem ser gerenciadas e incluídas de diferentes projetos.

   `allowProxy=true` garante que a biblioteca do cliente CSS e JavaScript sejam fornecidos a partir de um caminho prefixado com: `/etc.clientlibs`. Isso garante que o código do aplicativo em `/apps` permanece protegido contra usuários finais, mas CSS e JavaScript necessários para o funcionamento do site podem ser fornecidos anonimamente. Mais detalhes sobre a propriedade [allowProxy podem ser encontrados aqui](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

1. **tema** - Esta é a biblioteca do cliente que contém o tema inicial e o CSS para o projeto CIF. Esta biblioteca de cliente foi projetada para ser personalizada por cada implementação, e é útil start com alguns estilos existentes para que os componentes sejam funcionais para o start.

   ![biblioteca de clientela do tema](/help/commerce-cloud/assets/style-cif-component/clientlib-theme-folder-hierarchy.png)

   Abaixo está a definição XML do **tema**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.theme]"/>
   ```

   `acme.theme` é a categoria desta biblioteca de cliente e é assim que a biblioteca de cliente será incluída na página.

1. Abaixo da biblioteca de **temas** , você deve ver um arquivo chamado **css.txt** localizado em: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/css.txt`:

   ```plain
   #base=.
   common/common.css
   
   components/button/button.css
   
   components/featuredcategorylist/categorylist.css
   
   ...
   ```

   O **css.txt** (e **js.txt**) atua como manifestos que ditam a ordem na qual os arquivos individuais são incluídos no arquivo CSS final. O pedido é importante para CSS e JavaScript e é bom poder criar vários arquivos para gerenciar melhor o código. Ao examinar o arquivo **css.txt** , você pode ver que os arquivos são organizados pelos componentes aos quais os estilos são aplicados.

1. Inspect os arquivos CSS abaixo do **tema/componentes** para ter uma ideia dos estilos de componentes da guia. Atualizaremos alguns desses arquivos posteriormente no tutorial.

### Inclusão da biblioteca do cliente com o componente da página base

Em seguida, verificaremos como as bibliotecas do cliente são incluídas em uma página usando o [HTL](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#using-htl) e o componente Página.

1. No módulo **ui.apps** , navegue até a definição do `page` componente em: `ui.apps/src/main/content/jcr_root/apps/acme/components/structure/page`. Esse componente de **página** , gerado pelo arquétipo, é o ponto de entrada usado para renderizar todas as páginas no projeto.

1. Se você inspecionar a definição do componente da **página** (`page/.content.xml`), verá uma propriedade `sling:resourceSuperType` que aponta para `core/cif/components/structure/page/v1/page`. Isso significa que o componente de **página** do projeto (Acme) herdará toda a funcionalidade do componente [CIF principal da página](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/structure/page/v1/page) e permitirá que gerenciemos menos códigos.

1. Abaixo do componente de **página** você encontrará dois arquivos: **customheaderlibs.html** e **customfooterlibs.html**.

   ```html
   <!--/* customheaderlibs.html */-->
   <sly data-sly-use.clientLib="/libs/granite/sightly/templates/clientlib.html"
    data-sly-call="${clientlib.css @ categories='acme.wcm.base'}"/>
   ```

   **customheaderlibs.html** é um script HTL que será renderizado no cabeçalho da página. É um script comum para substituir e adicionar uma lógica específica do projeto. Nesse caso, estamos usando-a para incluir a biblioteca do cliente com uma categoria de `acme.wcm.base`. Seguindo as práticas recomendadas de desenvolvimento da Web, incluímos somente o CSS no cabeçalho da página.

   ```html
   <!--/* customfooterlibs.html */-->
   <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
       <sly data-sly-call="${clientlib.js @ categories='acme.wcm.base'}"/>
   </sly>
   ```

   **customfooterlibs.html** é um script HTL que será renderizado na parte inferior da página, logo antes da `</body>` tag de fechamento. Novamente, a categoria de `acme.wcm.base` é usada, mas desta vez somente o JavaScript da biblioteca do cliente será carregado.

Modificar os scripts HTL do componente de **página** é como `acme.wcm.base` é incluído em todas as páginas. E quanto a `acme.theme`? No próximo exercício, iremos analisar outra opção para incluir bibliotecas de clientes.

### Inclusão da Biblioteca do cliente com modelos de página {#client-library-inclusion-pagetemplates}

Há várias opções para incluir uma biblioteca do lado do cliente. Em seguida, verificaremos como o projeto gerado inclui as bibliotecas do lado do cliente do tema por meio de Modelos [de](https://docs.adobe.com/content/help/en/experience-manager-65/developing/platform/templates/page-templates-editable.html)página.

Abra um novo navegador e faça logon na instância AEM na qual você implantou o projeto no início deste tutorial.

1. Na tela AEM Start, navegue até **Ferramentas** > **Geral** > **Modelos**.

   ![Navegação do modelo](/help/commerce-cloud/assets/style-cif-component/template-location.png)

1. Navegue até a pasta Configuração **da** Acme Store. Abra o Modelo **de página de** Categoria selecionando o ícone de *lápis* .

   ![Cartão de modelo de página de categoria](/help/commerce-cloud/assets/style-cif-component/category-page-template.png)

1. No canto superior esquerdo, selecione o ícone Informações **da** página e clique em Política **** da página.

   ![Item de menu da política de página](/help/commerce-cloud/assets/style-cif-component/page-policy-menu.png)

1. Isso abrirá a Política de página para o modelo de Página de catálogo:

   ![Política de página - página de catálogo](/help/commerce-cloud/assets/style-cif-component/page-policy-properties.png)

   No lado direito você pode ver uma lista de **categorias** de bibliotecas clientes que serão incluídas em todas as páginas que usam este modelo.

   * **wcm.foundation.components.page.responsive** - Fornece o CSS necessário para ativar os controles de layout [](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/siteandpage/responsive-layout.html) responsivos pelos autores.
   * **acme.theme** - Esse é o tema inicial gerado automaticamente pelo arquétipo. Por padrão, esse estilo é semelhante ao da loja de demonstração Venia. No entanto, como você pode ver pelo nome, ele deve ser personalizado pela implementação do projeto. *É isto que vamos modificar na próxima seção!*
   * **core.CIF.components.response** - Esta é uma Biblioteca de clientes compilada com vários componentes React usados para recursos dinâmicos como o Carrinho de compras. Mais [informações podem ser encontradas aqui](https://github.com/adobe/aem-core-cif-components/tree/master/react-components).

   Observe que outros modelos usam a mesma política, Página **de** conteúdo, **Landing page** etc.. Ao reutilizar a mesma política, podemos garantir que as mesmas bibliotecas de clientes sejam incluídas em todas as páginas.

   A vantagem de usar Modelos e políticas de página para gerenciar a inclusão das bibliotecas clientes é que você pode alterar a política por modelo. Por exemplo, talvez você esteja gerenciando duas marcas diferentes dentro da mesma instância AEM. Cada marca terá seu próprio estilo ou *tema* exclusivo, mas as bibliotecas básicas e o código serão os mesmos. Outro exemplo, se você tivesse uma biblioteca de cliente maior que você só queria que fosse exibida em determinadas páginas, poderia fazer uma política de página exclusiva apenas para esse modelo. A outra vantagem

### Verificar bibliotecas de clientes na página {#verify-client-libraries}

Neste ponto, analisamos como incluir bibliotecas de clientes usando HTL com os scripts **customheaderlibs.html** e **customfooterlibs.html** e como uma política de página do Modelo pode ser usada para incluir bibliotecas de clientes adicionais. Em seguida, verificaremos a inclusão das bibliotecas clientes no site.

1. Na tela AEM Start, navegue até **Sites** > **Acme Store** > Estados **Unidos >** Inglês **** e abra a página para edição: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Selecione o menu Informações **da** página e clique em **Visualização como Publicado**:

   ![Exibir como publicado](/help/commerce-cloud/assets/style-cif-component/view-as-published.png)

   Isso abrirá a página sem o carregamento do javascript do autor AEM, como seria exibido no site publicado. Observe que o url tem o parâmetro query `?wcmmode=disabled` anexado. Ao desenvolver o CSS e o Javascript, é uma boa prática usar esse parâmetro para simplificar a página sem AEM do autor.

1. Visualização na fonte da página e você deve ser capaz de identificar as seguintes bibliotecas de clientes que foram incluídas: **acme.wcm.base**, **wcm.foundation.components.page.responsive**, **acme.themate**, **core.CIF.components.response**

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/clientlib-base.css" type="text/css">
       <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/theme.css" type="text/css">
   </head>
   ...
   
       <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/react-components.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/acme/clientlibs/clientlib-base.js"></script>
   </body>
   </html>
   ```

## Estilo do Teaser de produto {#style-product-teaser}

Agora que entendemos a estrutura da biblioteca do cliente gerada pelo arquétipo, podemos começar a personalizar os componentes principais AEM. Modificaremos os estilos do componente Teaser de produto para que ele se pareça mais com um &quot;cartão&quot;.

### Autor do Teaser de produto {#author-product-teaser}

Como primeiro passo, adicionaremos uma nova instância do componente Teaser de produto ao home page do nosso site usando as ferramentas de criação de AEM.

1. Abra uma nova guia do navegador e navegue até o **Home page** do site: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Insira um novo Componente do **Teaser** do produto no container do layout principal na página.

   ![Inserir Teaser de Produto](/help/commerce-cloud/assets/style-cif-component/product-teaser-add-component.png)

1. Expanda o painel lateral (se ainda não estiver alternado) e alterne a lista suspensa do localizador de ativos para **Produtos**. Isso deve exibir uma lista de produtos disponíveis de uma instância de Magento conectada. Selecione um produto e **arraste e solte** -o no componente **Teaser** do produto na página.

   ![Arrastar + Soltar Teaser de Produto](/help/commerce-cloud/assets/style-cif-component/drag-drop-product-teaser.png)

   > Observação: você também pode configurar o produto exibido configurando o componente usando a caixa de diálogo (clicando no ícone de *chave* ).

1. Agora você deve ver um Produto sendo exibido pelo Teaser de produto. O Nome do produto e o Preço do produto são atributos padrão exibidos.

   ![Teaser do produto - estilo padrão](/help/commerce-cloud/assets/style-cif-component/product-teaser-default-style.png)

### Atualize o CSS para o Teaser do produto {#update-css-product-teaser}

Em seguida, modificaremos o CSS na biblioteca de **temas** do cliente para implementar um estilo de cartão para o Teaser de produto.

Retorne ao IDE e ao projeto gerado.

1. No módulo **ui.apps** , navegue até a pasta: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/components/productteaser`. É aqui que todos os estilos do Teaser de produto são definidos.

1. Abra o arquivo **teaser.css** e atualize as regras CSS correspondentes (ou baixe o arquivo [teaser.css da](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css) solução e substitua).

   Adicione uma sombra projetada e inclua cantos arredondados no Teaser do produto.

   ```css
    .productteaser .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .productteaser .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

   Altere a borda da imagem no Teaser de produto.

   ```css
   .productteaser .item__image {
       border-bottom: 1px solid #c0c0c0;
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
    }
   ```

   Atualize o nome do Produto para que apareça na parte inferior do teaser e modifique a cor do texto.

   ```css
   .productteaser .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

   Atualize o preço do Produto para que também apareça na parte inferior do teaser e modifique a cor do texto.

   ```css
   .productteaser .item__price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   }
   ```

   Atualize o query de mídia na parte inferior para empilhar o nome e o preço em telas menores que 992px.

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   Salve as alterações em **teaser.css**. Você pode baixar o arquivo teaser.css da [solução aqui](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css).

1. Implante as atualizações do módulo **ui.apps** para AEM usando suas habilidades Maven, de um terminal de linha de comando:

   ```shell
           $ cd acme-store/ui.apps/
           $ mvn -PautoInstallPackage clean install
           ...
           saving approx 0 nodes...
           Package imported.
           Package installed in 61ms.
           [INFO] ------------------------------------------------------------------------
           [INFO] BUILD SUCCESS
           [INFO] ------------------------------------------------------------------------
           [INFO] Total time:  6.903 s
           [INFO] Finished at: 2020-02-06T13:21:36-08:00
            [INFO] ------------------------------------------------------------------------
   ```

   >[!NOTE]
   >Há outras Ferramentas [e Configuração de](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) IDE que podem sincronizar arquivos de projeto diretamente em uma instância AEM local sem precisar executar uma compilação Maven completa.

### Teaser de produto atualizado da Visualização {#view-updated-product-teaser}

Depois que o código do projeto for implantado no AEM, nós poderemos ver as alterações no Teaser do produto.

1. Retorne ao seu navegador e reinicie o Home page: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html). Você deve ver os estilos atualizados de teaser do produto aplicados.

   ![Estilo atualizado do Teaser do produto](/help/commerce-cloud/assets/style-cif-component/product-teaser-new-style.png)

1. Experimente adicionando outros teasers de produtos. Use o Modo de layout para alterar a largura e o deslocamento dos componentes a fim de exibir vários bordos em uma linha.

   ![Vários teasers de produtos](/help/commerce-cloud/assets/style-cif-component/multiple-teasers-final.png)

   >[!NOTE]
   >Cada teaser de produto contém o mesmo estilo.

### Resolução de Problemas{#troubleshooting}

Você pode verificar no [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) se o arquivo CSS atualizado foi implantado: [http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css](http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css)

Ao implantar novos arquivos CSS e/ou JavaScript, também é importante garantir que o navegador não esteja fornecendo arquivos obsoletos. Você pode eliminar isso limpando o cache do navegador ou iniciando uma nova sessão do navegador.

AEM também tenta fazer cache das bibliotecas clientes para obter desempenho. Ocasionalmente, após a implantação de um código, os arquivos mais antigos são atendidos. Você pode invalidar manualmente AEM cache da biblioteca do cliente usando a ferramenta [](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)Reconstruir bibliotecas do cliente. *Invalidate Caches é o método preferido se você suspeitar que AEM armazenou em cache uma versão antiga de uma biblioteca do cliente. As bibliotecas de reconstrução são ineficientes e demoradas.*

### Parabéns {#congratulations}

Você acabou de colocar seu primeiro AEM CIF Componente principal!

### Desafio de bônus {#bonus-challenge}

Use o sistema [Estilo](https://docs.adobe.com/content/help/en/experience-manager-65/developing/components/style-system.html) AEM para criar dois estilos que podem ser ativados/desativados por um autor de conteúdo. [O desenvolvimento com o Sistema](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) de estilo inclui etapas detalhadas e informações sobre como fazer isso.

![Desafio de bônus - estilo Sistema](/help/commerce-cloud/assets/style-cif-component/bonus-challenge.png)

## Recursos adicionais {#additional-resources}

* [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype)

* [Componentes principais CIF AEM](https://github.com/adobe/aem-core-cif-components)

* [Configurar um Ambiente de desenvolvimento de AEM local](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)

* [Bibliotecas do lado do cliente](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html)
* [Introdução aos AEM Sites](https://docs.adobe.com/content/help/br/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* [Desenvolvimento com o sistema de estilo](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
