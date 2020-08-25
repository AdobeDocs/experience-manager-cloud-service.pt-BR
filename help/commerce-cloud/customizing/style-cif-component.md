---
title: Alterar estilo dos Componentes principais da CIF do AEM
description: Alterar estilo dos Componentes principais da CIF do AEM
translation-type: ht
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: ht
source-wordcount: '2568'
ht-degree: 100%

---


# Alterar estilo dos Componentes principais da CIF do AEM {#style-aem-cif-core-components}

O [arquétipo de projeto da CIF](https://github.com/adobe/aem-cif-project-archetype) cria um projeto mínimo da CIF do Adobe Experience Manager (AEM) como ponto de partida para projetos de clientes que usam [os Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components). Um estilo padrão, conhecido como marca Venia, é aplicado inicialmente ao site. Neste tutorial, você verá um novo projeto da CIF do AEM gerado pelo arquétipo e compreenderá como o CSS e o JavaScript usados pelos Componentes principais da CIF do AEM são organizados. Você também vai criar um novo estilo usando CSS para substituir o estilo padrão do componente Teaser do produto.

![O que você vai criar](/help/commerce-cloud/assets/style-cif-component/what-you-will-build.png)

>[!NOTE]
> Será implementado um novo estilo no componente Teaser do produto que se assemelha a um cartão.

## Pré-requisitos {#prerequisites}

São necessárias as seguintes ferramentas e tecnologias:

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html) ou [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html) (somente AEM 6.5+)
* [Apache Maven](Https://maven.apache.org/) (3.3.9 ou mais recente)
* Adobe Experience Manager (instância local)
   * [AEM 6.5](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/deploying/introduction/technical-requirements.translate.html)
   * [AEM 6.4.4+](https://docs.adobe.com/content/help/pt-BR/experience-manager-64/release-notes/sp-release-notes.translate.html)
* Magento executando uma [versão compatível com o arquétipo](https://github.com/adobe/aem-cif-project-archetype#requirements)

## Gerar um projeto {#generate-project}

Geraremos um novo projeto da CIF do AEM utilizando o [arquétipo de projeto da CIF](https://github.com/adobe/aem-cif-project-archetype) e substituiremos os estilos padrão.

**Você pode usar um projeto existente** (com base no arquétipo de projeto da CIF) e ignorar esta seção.

1. Verifique no GitHub a [versão mais recente](https://github.com/adobe/aem-cif-project-archetype/releases/latest) do arquétipo de projeto da CIF. Na próxima etapa, substitua `x.y.z` pela versão mais recente.

1. Execute o seguinte comando Maven para gerar um novo projeto no [modo de lote](https://maven.apache.org/archetype/maven-archetype-plugin/examples/generate-batch.html).

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

1. Adicione as configurações OSGi necessárias para conectar a instância do AEM a uma instância da Magento ou adicione as configurações ao projeto recém-criado.

1. Nesta etapa, já deve estar funcionando uma versão de loja conectada a uma instância da Magento. Acesse a página `US` > `Home` em: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   Você verá que a loja está usando o tema Venia. Ao expandir o Menu principal da loja você verá várias categorias, que é um sinal de que a conexão com a Magento está funcionando.

   ![Loja configurada com o tema Venia](/help/commerce-cloud/assets/style-cif-component/acme-store-configured.png)

## Introdução às bibliotecas de clientes {#introduction-to-client-libraries}

O CSS e o JavaScript responsáveis pela renderização de temas/estilos da loja são gerenciados no AEM por uma [biblioteca do cliente](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/developing/introduction/clientlibs.translate.html) ou, abreviando, clientlibs. As bibliotecas de clientes fornecem um mecanismo para organizar o CSS e o Javascript no código de um projeto e, em seguida, na página.

A maneira de aplicar estilos específicos da marca nos Componentes principais da CIF do AEM é adicionando e substituindo o CSS gerenciado pelas bibliotecas de clientes. Entender como as bibliotecas de clientes são estruturadas e incluídas na página é essencial.

### Bibliotecas de clientes do projeto{#project-client-libraries}

Em seguida, analisaremos as bibliotecas de clientes geradas automaticamente pelo arquétipo. Utilize o IDE de sua escolha para [importar o projeto gerado no exercício anterior](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment).

1. Acesse e expanda o módulo **ui.apps** e expanda a hierarquia de pastas para: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs`:

   ![ui.apps clientlibs](/help/commerce-cloud/assets/style-cif-component/ui-apps-clientli-folder.png)

   Há duas pastas abaixo, **clientlib-base** e **theme**.

1. **clientlib-base** — É uma biblioteca do cliente vazia que simplesmente incorpora as dependências necessárias dos [Componentes principais do AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html)

   ![Clientlib-base](/help/commerce-cloud/assets/style-cif-component/clientlib-base-folderhierarchy.png)

   Abaixo está a definição XML da **clientlib-base** (o arquivo `.content.xml`):

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.wcm.base]"
       embed="[core.wcm.components.accordion.v1,core.wcm.components.tabs.v1,core.wcm.components.carousel.v1,core.wcm.components.image.v2,core.wcm.components.breadcrumb.v2,core.wcm.components.search.v1,core.wcm.components.form.text.v2]"/>
   ```

   `acme.wcm.base` é a categoria desta biblioteca do cliente. Pense em uma categoria como uma tag. Ela será usada para incluir ou incorporar a biblioteca na página.

   Observe a propriedade `embed` e a variedade de outras categorias das bibliotecas de clientes. Cada uma dessas categorias representa uma biblioteca do cliente. Por exemplo, `core.wcm.components.accordion.v1` inclui o javascript necessário para que o [componente Acordeão](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/components/accordion.html) funcione.

   Com as propriedades `embed` e `categories` é possível gerenciar e incluir as bibliotecas de clientes de diferentes projetos.

   `allowProxy=true` garante que o CSS e o JavaScript das bibliotecas de clientes sejam operados a partir de um caminho prefixado com: `/etc.clientlibs`. Dessa forma, o código do aplicativo em `/apps` fica protegido de usuários finais, mas o CSS e o JavaScript necessários para o funcionamento do site podem ser fornecidos anonimamente. Mais detalhes sobre a [propriedade allowProxy podem ser encontrados aqui](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/developing/introduction/clientlibs.translate.html#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

1. **theme** — É a biblioteca do cliente que contém o tema inicial e o CSS para o projeto da CIF. Essa biblioteca do cliente foi projetada para ser personalizada por cada implementação, e é útil começar com alguns estilos existentes para que os componentes funcionem desde o início.

   ![theme clientlibrary](/help/commerce-cloud/assets/style-cif-component/clientlib-theme-folder-hierarchy.png)

   Abaixo está a definição XML do **tema**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.theme]"/>
   ```

   `acme.theme` é a categoria dessa biblioteca do cliente e é assim que ela será incluída na página.

1. Abaixo da biblioteca de **temas** de clientes, você deve ver um arquivo chamado **css.txt** localizado em: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/css.txt`:

   ```plain
   #base=.
   common/common.css
   
   components/button/button.css
   
   components/featuredcategorylist/categorylist.css
   
   ...
   ```

   O **css.txt** (e o **js.txt**) atua como manifestos que ditam a ordem em que os arquivos individuais são incluídos no arquivo CSS final. A ordem é importante para o CSS e para o JavaScript. É interessante criar vários arquivos em ordem para gerenciar melhor o código. Ao examinar o arquivo **css.txt**, é possível ver que os arquivos são organizados pelos componentes aos quais os estilos são aplicados.

1. Verifique os arquivos CSS abaixo de **tema/componentes** para ter uma ideia dos estilos de componentes prontos para uso. Atualizaremos alguns desses arquivos posteriormente no tutorial.

### Inclusão da biblioteca do cliente com a página base

Em seguida, verificaremos como as bibliotecas de clientes são incluídas em uma página usando [HTL](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/developing/introduction/clientlibs.translate.html#using-htl) e o componente Página.

1. No módulo **ui.apps**, acesse a definição do componente `page` em: `ui.apps/src/main/content/jcr_root/apps/acme/components/structure/page`. Esse componente **Página**, gerado pelo arquétipo, é o ponto de entrada utilizado para renderizar todas as páginas no projeto.

1. Se você inspecionar a definição do componente **Página** (`page/.content.xml`), verá uma propriedade `sling:resourceSuperType` que indica `core/cif/components/structure/page/v1/page`. Significa que o componente **página** do projeto (Acme) herdará toda a funcionalidade do componente [Página principal da CIF](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/structure/page/v1/page). Portanto, requer menos programação.

1. Abaixo do componente **página** você encontrará dois arquivos: **customheaderlibs.html** e **customfooterlibs.html**.

   ```html
   <!--/* customheaderlibs.html */-->
   <sly data-sly-use.clientLib="/libs/granite/sightly/templates/clientlib.html"
    data-sly-call="${clientlib.css @ categories='acme.wcm.base'}"/>
   ```

   **customheaderlibs.html** é um script HTL que será renderizado no cabeçalho da página. É um script comum para substituir e adicionar uma lógica específica do projeto. Nesse caso, usamos esse script para incluir uma categoria de `acme.wcm.base` na biblioteca do cliente. Seguindo as práticas recomendadas de desenvolvimento da Web, incluímos somente o CSS no cabeçalho da página.

   ```html
   <!--/* customfooterlibs.html */-->
   <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
       <sly data-sly-call="${clientlib.js @ categories='acme.wcm.base'}"/>
   </sly>
   ```

   **customfooterlibs.html** é um script HTL que será renderizado na parte inferior da página, antes da tag `</body>` de encerramento. Novamente, a categoria de `acme.wcm.base` é utilizada, mas dessa vez somente o JavaScript da biblioteca do cliente será carregado.

Com a modificação dos scripts HTL do componente **página**, `acme.wcm.base` é incluído em todas as páginas. E quanto ao `acme.theme`? No próximo exercício, analisaremos outra opção para incluir bibliotecas de clientes.

### Inclusão da biblioteca do cliente com modelos de página {#client-library-inclusion-pagetemplates}

Há várias opções para incluir uma biblioteca do lado do cliente. Em seguida, verificaremos como o projeto gerado inclui as bibliotecas de temas do lado do cliente por meio dos [Modelos de página](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/developing/platform/templates/page-templates-editable.translate.html).

Abra um novo navegador e faça logon na instância do AEM em que você implantou o projeto no início deste tutorial.

1. Na tela inicial do AEM, acesse **Ferramentas** > **Geral** > **Modelos**.

   ![Acesso aos modelos](/help/commerce-cloud/assets/style-cif-component/template-location.png)

1. Acesse a pasta **Configuração da Acme Store**. Abra a **categoria Modelo de página** selecionando o *lápis*.

   ![categoria cartão de modelo de página](/help/commerce-cloud/assets/style-cif-component/category-page-template.png)

1. No canto superior esquerdo, selecione o ícone **Informações da página** e clique em **Política da página**.

   ![Item do menu da política da página](/help/commerce-cloud/assets/style-cif-component/page-policy-menu.png)

1. A Política da página para o modelo Página do catálogo será exibida:

   ![Política da página — página do catálogo](/help/commerce-cloud/assets/style-cif-component/page-policy-properties.png)

   No lado direito, é possível ver uma lista das **categorias** de bibliotecas de clientes que serão incluídas em todas as páginas que utilizam esse modelo.

   * **wcm.foundation.components.page.responsive** — Fornece o CSS necessário para ativar os controles de [layout responsivos](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/authoring/siteandpage/responsive-layout.translate.html) pelos autores.
   * **acme.theme** — É o tema inicial gerado automaticamente pelo arquétipo. Por padrão, esse estilo é semelhante ao da loja de demonstração Venia. No entanto, como você pode ver pelo nome, ele deve ser personalizado pela implementação do projeto. *É o que vamos modificar na próxima seção.*
   * **core.CIF.components.response** — É uma biblioteca do cliente compilada com vários componentes React utilizados para recursos dinâmicos como o Carrinho de compras. Mais [informações podem ser encontradas aqui](https://github.com/adobe/aem-core-cif-components/tree/master/react-components).

   Observe que outros modelos utilizam a mesma política, **Página de conteúdo**, **Página de aterrissagem**, etc. Ao reutilizar a mesma política, podemos garantir que as mesmas bibliotecas de clientes sejam incluídas em todas as páginas.

   A vantagem de utilizar modelos e políticas de página para gerenciar a inclusão das bibliotecas de clientes é que você pode alterar a política de acordo com o modelo. Por exemplo, talvez você esteja gerenciando duas marcas diferentes na mesma instância do AEM. Cada marca terá seu próprio estilo ou *tema*, mas as bibliotecas base e o código base serão os mesmos. Outro exemplo: se você quisesse que uma bibliotecas do cliente maior fosse exibida apenas em determinadas páginas, seria possível fazer uma política de página exclusiva para esse modelo. A outra vantagem

### Verificar bibliotecas de clientes na página {#verify-client-libraries}

Até agora analisamos como incluir bibliotecas de clientes utilizando HTL com os scripts **customheaderlibs.html** e **customfooterlibs.html** e como uma política da página de um modelo pode ser utilizada para incluir bibliotecas de clientes adicionais. Em seguida, verificaremos a inclusão de bibliotecas de clientes no site.

1. Na tela inicial do AEM, acesse **Sites** > **Acme Store** > **Estados Unidos** > **Inglês** e abra a página para edição: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Selecione o menu **Informações da página** e clique em **Exibir como publicado**:

   ![Exibir como publicado](/help/commerce-cloud/assets/style-cif-component/view-as-published.png)

   A página será exibida sem carregar o javascript criado pelo autor no AEM, como seria exibido no site publicado. Observe que o URL tem o parâmetro de consulta `?wcmmode=disabled` anexado. Ao desenvolver o CSS e o Javascript, é recomendado usar esse parâmetro para simplificar a página sem nenhuma ação de seu autor no AEM.

1. Ao visualizar a fonte da página, você identificará as seguintes bibliotecas de clientes que foram incluídas: **acme.wcm.base**, **wcm.foundation.components.page.responsive**, **acme.themate**, **core.CIF.components.response**

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

## Estilo do Teaser do produto {#style-product-teaser}

Agora que entendemos a estrutura da biblioteca do cliente gerada pelo arquétipo, podemos começar a personalizar os Componentes principais da CIF do AEM. Modificaremos os estilos do componente teaser de produto para que ele se pareça mais com um &quot;cartão&quot;.

### Criação do Teaser do produto {#author-product-teaser}

Como primeiro passo, adicionamos uma nova instância do Teaser do produto à página inicial do site usando as ferramentas de criação do AEM.

1. Abra uma nova guia do navegador e acesse a **Página inicial** do site: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html).

1. Insira um novo **Teaser do produto** no container do layout principal da página.

   ![Inserir Teaser do produto](/help/commerce-cloud/assets/style-cif-component/product-teaser-add-component.png)

1. Expanda o painel lateral (se ainda não estiver sendo exibido) e na lista suspensa do localizador de ativos selecione **Produtos**. Essa ação deve exibir uma lista de produtos disponíveis em uma instância conectada da Magento. Selecione, **arraste e solte** um produto no **Teaser do produto** exibido na página.

   ![Arrastar e soltar Teaser do produto](/help/commerce-cloud/assets/style-cif-component/drag-drop-product-teaser.png)

   > Observação: você também pode configurar o produto exibido definindo o componente na caixa de diálogo (clicando na *chave inglesa*).

1. Agora você já deve estar vendo um produto no teaser. O nome e o preço do produto são atributos exibidos por padrão.

   ![Teaser do produto — estilo padrão](/help/commerce-cloud/assets/style-cif-component/product-teaser-default-style.png)

### Atualizar o CSS do Teaser do produto {#update-css-product-teaser}

Em seguida, modificaremos o CSS na biblioteca de **temas** do cliente para implementar um Teaser do produto com layout de cartão.

Retorne ao IDE e ao projeto gerado.

1. No módulo **ui.apps**, acesse a pasta: `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/components/productteaser`. É nela que todos os estilos de Teaser do produto são definidos.

1. Abra o arquivo **teaser.css** e atualize as regras CSS correspondentes (ou baixe [o arquivo de solução teaser.css](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css) e substitua-o).

   Adicione sombreado e pontas arredondadas ao Teaser do produto.

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

   Altere a borda da imagem no Teaser do produto.

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

   Atualize o nome do produto para que ele apareça na parte inferior do teaser e modifique a cor do texto.

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

   Atualize o preço do produto para que ele também apareça na parte inferior do teaser e modifique a cor do texto.

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

   Atualize a consulta de mídia na parte inferior para empilhar o nome e o preço em telas menores que 992 px.

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

   Salve as alterações em **teaser.css**. Você pode baixar o [arquivo de solução teaser.css aqui](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css).

1. Implante as atualizações do módulo **ui.apps** no AEM aplicando seus conhecimentos de Maven em um terminal de linha de comando:

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
   >Há outras [Ferramentas e configurações do IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) que podem sincronizar arquivos de projeto diretamente em uma instância do AEM local sem precisar executar uma compilação completa de Maven.

### Exibir Teaser do produto atualizado {#view-updated-product-teaser}

Depois que o código do projeto for implantado no AEM, poderemos ver as alterações no Teaser do produto.

1. Retorne ao navegador e atualize a página inicial: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html). O estilo do teaser de produto já deve ter sido aplicado.

   ![Estilo atualizado do Teaser do produto](/help/commerce-cloud/assets/style-cif-component/product-teaser-new-style.png)

1. Tente adicionar outros teasers de produto. Use o Modo de layout para alterar a largura e a distância dos componentes a fim de exibir vários teasers em sequência.

   ![Vários teasers de produtos](/help/commerce-cloud/assets/style-cif-component/multiple-teasers-final.png)

   >[!NOTE]
   >Cada teaser de produto contém o mesmo estilo.

### Resolução de problemas {#troubleshooting}

Você pode verificar no [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) se o arquivo CSS atualizado foi implantado: [http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css](http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css)

Ao implantar novos arquivos CSS e/ou JavaScript também é importante garantir que o navegador não esteja fornecendo arquivos obsoletos. Você pode corrigir isso limpando o cache do navegador ou iniciando uma nova sessão do navegador.

O AEM também tenta armazenar as bibliotecas de clientes em cache para melhorar o desempenho. Ocasionalmente, após a implantação de um código, os arquivos mais antigos são enviados. Você pode invalidar manualmente o cache das bibliotecas de clientes do AEM utilizando a [ferramenta Recompilar bibliotecas de clientes](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *Invalidar caches é o método mais aconselhável se você suspeitar que o AEM armazenou em cache uma versão antiga de uma biblioteca do cliente. A ferramenta Recompilar bibliotecas é ineficaz e demorada.*

### Parabéns {#congratulations}

Você acabou de personalizar o seu primeiro Componente principal da CIF do AEM.

### Desafio extra {#bonus-challenge}

Utilize o [Sistema de estilo do AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/developing/components/style-system.translate.html) para criar dois estilos que podem ser ativados/desativados por um autor de conteúdo. Em [Desenvolvimento com o sistema de estilo](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) você encontra informações detalhadas com todas as etapas para fazê-lo.

![Desafio extra — Sistema de estilo](/help/commerce-cloud/assets/style-cif-component/bonus-challenge.png)

## Recursos adicionais {#additional-resources}

* [Arquétipo da CIF do AEM](https://github.com/adobe/aem-cif-project-archetype)

* [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components)

* [Configurar um Ambiente de desenvolvimento do AEM local](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)

* [Bibliotecas do lado do cliente](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/developing/introduction/clientlibs.translate.html)
* [Introdução ao AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* [Desenvolvimento com o sistema de estilo](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
