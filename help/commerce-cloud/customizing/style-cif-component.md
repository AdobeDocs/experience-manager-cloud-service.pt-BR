---
title: Alterar estilo dos Componentes principais da CIF do AEM
description: Saiba como criar o estilo AEM componentes principais CIF. O tutorial aborda como as bibliotecas do lado do cliente ou clientlibs são usadas para implantar e gerenciar CSS e Javascript para uma implementação de comércio da Adobe Experience Manager (AEM). Este tutorial também abordará como o módulo ui.front-end e um projeto de webpack são integrados ao processo de criação completo.
sub-product: Commerce
topics: Development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 3456
thumbnail: 3456-style-cif.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '2592'
ht-degree: 33%

---


# Alterar estilo dos Componentes principais da CIF do AEM {#style-aem-cif-core-components}

O [CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) é uma base de códigos de referência para o uso de [CIF Componentes Principais](https://github.com/adobe/aem-core-cif-components). Neste tutorial, você inspecionará o projeto de referência Venia e compreenderá como CSS e JavaScript usados pelos componentes CIF principais estão organizados. Você também criará um novo estilo usando o CSS para atualizar o estilo padrão do componente **Teaser do produto**.

>[!TIP]
>
> Use o [AEM Tipo de arquivo do projeto](https://github.com/adobe/aem-project-archetype) ao iniciar sua própria implementação de comércio.

## O que você vai criar

Neste tutorial, um novo estilo será implementado para o componente Teaser do produto que se assemelha a uma placa. As lições aprendidas no tutorial podem ser aplicadas a outros componentes principais CIF.

![O que você vai criar](../assets/style-cif-component/what-you-will-build.png)

## Pré-requisitos {#prerequisites}

É necessário um ambiente de desenvolvimento local para concluir este tutorial. Isso inclui uma instância em execução de AEM configurada e conectada a uma instância Magento. Revise os requisitos e as etapas para [configurar um desenvolvimento local com AEM como um SDK Cloud Service.](../develop.md)

## Clonar o projeto Venia {#clone-venia-project}

Vamos clonar o [Projeto Venia](https://github.com/adobe/aem-cif-guides-venia) e depois substituir os estilos padrão.

>[!NOTE]
>
> **Sinta-se à vontade para usar um projeto**  existente (com base no AEM Project Archetype com CIF incluído) e ignore esta seção.

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

1. Nesta etapa, já deve estar funcionando uma versão de loja conectada a uma instância da Magento. Navegue até a página `US` > `Home` em: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   Você verá que a loja está usando o tema Venia. Ao expandir o Menu principal da loja você verá várias categorias, que é um sinal de que a conexão com a Magento está funcionando.

   ![Storefront Configurado com o Tema de Venia](../assets/style-cif-component/venia-store-configured.png)

## Bibliotecas do cliente e módulo ui.front-end {#introduction-to-client-libraries}

O CSS e o JavaScript responsáveis pela renderização de temas/estilos da loja são gerenciados no AEM por uma [biblioteca do cliente](/help/implementing/developing/introduction/clientlibs.md) ou, abreviando, clientlibs. As bibliotecas de clientes fornecem um mecanismo para organizar o CSS e o Javascript no código de um projeto e, em seguida, na página.

Os estilos específicos da marca podem ser aplicados AEM componentes principais CIF adicionando e substituindo o CSS gerenciado por essas bibliotecas clientes. Entender como as bibliotecas de clientes são estruturadas e incluídas na página é essencial.

O [ui.front-end](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html) é um projeto dedicado [webpack](https://webpack.js.org/) para gerenciar todos os ativos front-end de um projeto. Isso permite que os desenvolvedores de front-end usem qualquer número de idiomas e tecnologias, como [TypeScript](https://www.typescriptlang.org/), [Sass](https://sass-lang.com/) e muito mais.

O módulo `ui.frontend` também é um módulo Maven e integrado ao projeto maior através do uso de um módulo NPM o [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator). Durante uma compilação, o `aem-clientlib-generator` copia os arquivos CSS e JavaScript compilados em uma Biblioteca do cliente no módulo `ui.apps`.

![ui.frontende à arquitetura ui.apps](../assets/style-cif-component/ui-frontend-architecture.png)

*CSS e Javascript compilados são copiados do  `ui.frontend` módulo para o  `ui.apps` módulo como uma biblioteca de cliente durante uma compilação Maven*

## Atualize o estilo do teaser {#ui-frontend-module}

Em seguida, faça uma pequena alteração no estilo do Teaser para ver como o módulo `ui.frontend` e as bibliotecas de clientes funcionam. Use [o IDE de sua escolha](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) para importar o projeto Venia. As capturas de tela usadas são do código do Visual Studio IDE[.](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)

1. Navegue e expanda o módulo **ui.front-end** e expanda a hierarquia de pastas para: `ui.frontend/src/main/styles/commerce`:

   ![pasta de comércio ui.front-end](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   Observe que existem vários arquivos Sass (`.scss`) abaixo da pasta. Esses são os estilos específicos de Comércio para cada um dos componentes de Comércio.

1. Abra o arquivo `_productteaser.scss`.

1. Atualize a regra `.item__image` e modifique a regra de borda:

   ```scss
   .item__image {
       border: #ea00ff 8px solid; /* <-- modify this rule */
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

   A regra acima deve adicionar uma borda rosa muito em negrito ao componente Teaser do produto.

1. Abra uma nova janela de terminal e navegue até a pasta `ui.frontend`:

   ```shell
   $ cd <project-location>/aem-cif-guides-venia/ui.frontend
   ```

1. Execute o seguinte comando Maven:

   ```shell
   $ mvn clean install
   ...
   [INFO] ------------------------------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ------------------------------------------------------------------------
   [INFO] Total time:  29.497 s
   [INFO] Finished at: 2020-08-25T14:30:44-07:00
   [INFO] ------------------------------------------------------------------------
   ```

   Inspect a saída do terminal. Você verá que o comando Maven executou vários scripts NPM, incluindo `npm run build`. O comando `npm run build` é definido no arquivo `package.json` e tem o efeito de compilar o projeto do webpack e acionar a geração da biblioteca do cliente.

1. Inspect o arquivo `ui.frontend/dist/clientlib-site/site.css`:

   ![CSS do site compilado](../assets/style-cif-component/comiled-site-css.png)

   O arquivo é a versão compilada e minified de todos os arquivos Sass no projeto.

   >[!NOTE]
   >
   > Arquivos como este são ignorados do controle de origem, pois devem ser gerados durante o tempo de criação.

1. Inspect o arquivo `ui.frontend/clientlib.config.js`.

   ```js
   /* clientlib.config.js*/
   ...
   // Config for `aem-clientlib-generator`
   module.exports = {
       context: BUILD_DIR,
       clientLibRoot: CLIENTLIB_DIR,
       libs: [
           {
               ...libsBaseConfig,
               name: 'clientlib-site',
               categories: ['venia.site'],
               dependencies: ['venia.dependencies', 'aem-core-cif-react-components'],
               assets: {
   ...
   ```

   Este é o arquivo de configuração para [aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator) e determina onde e como o CSS e o JavaScript compilados serão transformados em uma biblioteca de clientes AEM.

1. No módulo `ui.apps` inspecione o arquivo: `ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![CSS do site compilado em ui.apps](../assets/style-cif-component/comiled-css-ui-apps.png)

   Esse é o arquivo copiado `site.css` no projeto `ui.apps`. Agora, ela faz parte de uma biblioteca de clientes chamada `clientlib-site` com uma categoria de `venia.site`. Quando o arquivo fizer parte do módulo `ui.apps`, ele poderá ser implantado no AEM.

   >[!NOTE]
   >
   > Arquivos como este também são ignorados do controle de origem, pois devem ser gerados durante o tempo de criação.

1. Em seguida, inspecione as outras bibliotecas de clientes geradas pelo projeto:

   ![Outras bibliotecas do cliente](../assets/style-cif-component/other-clientlibs.png)

   Essas bibliotecas de cliente não são gerenciadas pelo módulo `ui.frontend`. Em vez disso, essas bibliotecas clientes incluem dependências CSS e JavaScript fornecidas pelo Adobe. A definição dessas bibliotecas de clientes está no arquivo `.content.xml` abaixo de cada pasta.

   **clientlib-base** — É uma biblioteca do cliente vazia que simplesmente incorpora as dependências necessárias dos [Componentes principais do AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) A categoria é `venia.base`.

   **clientlib-CIF**  - é também uma biblioteca de cliente vazia que simplesmente incorpora as dependências necessárias de  [AEM componentes](https://github.com/adobe/aem-core-cif-components) principais CIF. A categoria é `venia.cif`.

   **clientlib-grid**  - inclui o CSS necessário para ativar AEM recurso Grade responsiva. Usar a grade AEM ativa [Modo de layout](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/configuring-responsive-layout.html#include-the-responsive-css) no editor de AEM e dá aos autores de conteúdo a capacidade de redimensionar componentes. A categoria é `venia.grid` e está incorporada na biblioteca `venia.base`.

1. Inspect os arquivos `customheaderlibs.html` e `customfooterlibs.html` abaixo de `ui.apps/src/main/content/jcr_root/apps/venia/components/page`:

   ![Scripts personalizados de cabeçalho e rodapé](../assets/style-cif-component/custom-header-footer-script.png)

   Esses scripts incluem as bibliotecas **venia.base** e **venia.CIF** como parte de todas as páginas.

   >[!NOTE]
   >
   > Somente as bibliotecas base são &quot;codificadas permanentemente&quot; como parte dos scripts de página. `venia.site` não está incluído nesses arquivos e, em vez disso, é incluído como parte do modelo de página para maior flexibilidade. Esta questão será inspecionada mais tarde.

1. Do terminal, crie e implante o projeto inteiro em uma instância local do AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## Criar um Teaser de produto {#author-product-teaser}

Agora que as atualizações de código foram implantadas, adicione uma nova instância do componente Teaser do produto ao home page do site usando as ferramentas de criação AEM. Isso nos permitirá visualização dos estilos atualizados.

1. Abra uma nova guia do navegador e navegue até **Home page** do site: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Expanda o Localizador de ativos (o painel lateral) no modo **Editar**. Alterne o filtro Ativo para **Produtos**.

   ![Expanda o Localizador de ativos e filtre por Produtos](../assets/style-cif-component/drag-drop-product-page.png)

1. Arraste e solte um novo produto no home page no Container Layout principal:

   ![Teaser do produto com borda rosa](../assets/style-cif-component/pink-border-product-teaser.png)

   Você deve ver que o Teaser do produto agora tem uma borda rosa brilhante com base na alteração da regra CSS criada anteriormente.

## Verificar bibliotecas de clientes na página {#verify-client-libraries}

Em seguida, verifique a inclusão das bibliotecas clientes na página.

1. Navegue até o **Home page** do site: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Selecione o menu **Informações da página** e clique em **Exibir como publicado**:

   ![Exibir como publicado](../assets/style-cif-component/view-as-published.png)

   A página será exibida sem carregar o javascript criado pelo autor no AEM, como seria exibido no site publicado. Observe que o URL tem o parâmetro de consulta `?wcmmode=disabled` anexado. Ao desenvolver o CSS e o Javascript, é recomendado usar esse parâmetro para simplificar a página sem nenhuma ação de seu autor no AEM.

1. Visualização na fonte da página e você deve ser capaz de identificar várias bibliotecas de clientes que foram incluídas:

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-site.min.css" type="text/css">
   </head>
   ...
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-base.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/common.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-cif.min.js"></script>
   </body>
   </html>
   ```

   As bibliotecas de clientes quando entregues à página recebem o prefixo `/etc.clientlibs` e são fornecidas por meio de um [proxy](/help/implementing/developing/introduction/clientlibs.md) para evitar expor qualquer coisa sensível em `/apps` ou `/libs`.

   Observe `venia/clientlibs/clientlib-site.min.css` e `venia/clientlibs/clientlib-site.min.js`. Estes são os arquivos CSS e Javascript compilados derivados do módulo `ui.frontend`.

## Inclusão da biblioteca do cliente com modelos de página {#client-library-inclusion-pagetemplates}

Há várias opções para incluir uma biblioteca do lado do cliente. Em seguida, verifique como o projeto gerado inclui as bibliotecas `clientlib-site` por meio de [Modelos de página](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/developing/platform/templates/page-templates-editable.translate.html).

1. Navegue até o **Home page** do site no Editor de AEM: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

1. Selecione o menu **Informações da página** e clique em **Editar modelo**:

   ![Editar o modelo](../assets/style-cif-component/edit-template.png)

   Isso abrirá o modelo **Landing page** no qual a página **Início** se baseia.

   >[!NOTE]
   >
   > Para visualização de todos os modelos disponíveis na tela do Start AEM, navegue até **Ferramentas** > **Geral** > **Modelos**.

1. No canto superior esquerdo, selecione o ícone **Informações da página** e clique em **Política da página**.

   ![Item do menu da política da página](../assets/style-cif-component/page-policy-menu.png)

1. Isso abrirá a Política de página do modelo de Landing page:

   ![Política de página - landing page](../assets/style-cif-component/page-policy-properties.png)

   No lado direito, é possível ver uma lista das **categorias** de bibliotecas de clientes que serão incluídas em todas as páginas que utilizam esse modelo.

   * `venia.dependencies` - Fornece todas as bibliotecas de fornecedores  `venia.site` dependentes.
   * `venia.site` - Essa é a categoria gerada pelo  `clientlib-site`   `ui.frontend` módulo.

   Observe que outros modelos utilizam a mesma política, **Página de conteúdo**, **Página de aterrissagem**, etc. Ao reutilizar a mesma política, podemos garantir que as mesmas bibliotecas de clientes sejam incluídas em todas as páginas.

   A vantagem de utilizar modelos e políticas de página para gerenciar a inclusão das bibliotecas de clientes é que você pode alterar a política de acordo com o modelo. Por exemplo, talvez você esteja gerenciando duas marcas diferentes na mesma instância do AEM. Cada marca terá seu próprio estilo ou *tema*, mas as bibliotecas base e o código base serão os mesmos. Outro exemplo: se você quisesse que uma bibliotecas do cliente maior fosse exibida apenas em determinadas páginas, seria possível fazer uma política de página exclusiva para esse modelo.

## Desenvolvimento de webpack local {#local-webpack-development}

No exercício anterior, foi feita uma atualização em arquivos Sass no módulo `ui.frontend` e, depois de executar uma compilação Maven, as alterações são implantadas em AEM. Em seguida, vamos analisar como aproveitar um servidor webpack-dev para desenvolver rapidamente os estilos de front-end.

O webpack-dev-server proxies imagens e alguns dos CSS/JavaScript da instância local do AEM, mas permite que o desenvolvedor modifique os estilos e o JavaScript no módulo `ui.frontend`.

1. No navegador, navegue até a página **Início** e **Visualização como Publicado**: [http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled).

1. Visualização a fonte da página e o **copy** o HTML bruto da página.

1. Retorne ao IDE de sua escolha abaixo do módulo `ui.frontend` para abrir o arquivo: `ui.frontend/src/main/static/index.html`

   ![Arquivo HTML estático](../assets/style-cif-component/static-index-html.png)

1. Substitua o conteúdo de `index.html` e **colar** o HTML copiado na etapa anterior.

1. Encontre as inclusões para `clientlib-site.min.css`, `clientlib-site.min.js` e **remova** elas.

   ```html
   <head>
       <!-- remove this link -->
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       ...
   </head>
   <body>
       ...
        <!-- remove this link -->
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
   </body>
   ```

   Eles são removidos porque representam a versão compilada do CSS e do JavaScript gerada pelo módulo `ui.frontend`. Deixe as outras bibliotecas do cliente como serão enviadas por proxy da instância AEM em execução.

1. Abra uma nova janela de terminal e navegue até a pasta `ui.frontend`. Execute o comando `npm start`:

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   Isso start o webpack-dev-server em [http://localhost:8080/](http://localhost:8080/)

   >[!CAUTION]
   >
   > Se você receber um erro relacionado ao Sass, pare o servidor e execute o comando `npm rebuild node-sass` e repita as etapas acima. Isso pode ocorrer se tiver uma versão diferente de `npm` e `node`, em seguida, for especificada no projeto `aem-cif-guides-venia/pom.xml`.

1. Navegue até [http://localhost:8080/](http://localhost:8080/) em uma nova guia com o mesmo navegador que uma instância de AEM registrada. Você deve ver o home page Venia através do webpack-dev-server:

   ![Servidor de desenvolvimento de Webpack na porta 80](../assets/style-cif-component/webpack-dev-server-port80.png)

   Deixe o webpack-dev-server em execução. Ele será usado no próximo exercício.

## Implementar estilo de cartão para o Teaser do produto {#update-css-product-teaser}

Em seguida, modifique os arquivos Sass no módulo `ui.frontend` para implementar um estilo semelhante a cartão para o Teaser do produto. O webpack-dev-server será usado para visualizar rapidamente as alterações.

Retorne ao IDE e ao projeto gerado.

1. No módulo **ui.front-end**, abra novamente o arquivo `_productteaser.scss` em `ui.frontend/src/main/styles/commerce/_productteaser.scss`.

1. Faça as seguintes alterações na borda do Teaser de produto:

   ```diff
       .item__image {
   -       border: #ea00ff 8px solid;
   +       border-bottom: 1px solid #c0c0c0;
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

   Salve as alterações e o webpack-dev-server deve atualizar automaticamente com os novos estilos.

1. Adicione sombreado e pontas arredondadas ao Teaser do produto.

   ```scss
    .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

1. Atualize o nome do produto para que ele apareça na parte inferior do teaser e modifique a cor do texto.

   ```css
   .item__name {
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

1. Atualize o preço do produto para que ele também apareça na parte inferior do teaser e modifique a cor do texto.

   ```css
   .price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   
       ...
   ```

1. Atualize o query de mídia na parte inferior para empilhar o nome e o preço em telas menores que **992px**.

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

   Agora, você deve ver o estilo de cartão refletido no servidor webpack-dev:

   ![Alterações no teaser do Servidor de Desenvolvimento do Webpack](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   No entanto, as alterações ainda não foram implantadas em AEM. Você pode baixar o [arquivo de solução aqui](../assets/style-cif-component/_productteaser.scss).

1. Implante as atualizações para AEM usando suas habilidades Maven, a partir de um terminal de linha de comando:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >Há outras [Ferramentas e configurações do IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) que podem sincronizar arquivos de projeto diretamente em uma instância do AEM local sem precisar executar uma compilação completa de Maven.

## Exibir Teaser do produto atualizado {#view-updated-product-teaser}

Depois que o código do projeto for implantado no AEM, poderemos ver as alterações no Teaser do produto.

1. Retorne ao seu navegador e reinicie o Home page: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html). O estilo do teaser de produto já deve ter sido aplicado.

   ![Estilo atualizado do Teaser do produto](../assets/style-cif-component/product-teaser-new-style.png)

1. Tente adicionar outros teasers de produto. Use o Modo de layout para alterar a largura e a distância dos componentes a fim de exibir vários teasers em sequência.

   ![Vários teasers de produtos](../assets/style-cif-component/multiple-teasers-final.png)

## Resolução de problemas {#troubleshooting}

Você pode verificar em [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) se o arquivo CSS atualizado foi implantado: [http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

Ao implantar novos arquivos CSS e/ou JavaScript também é importante garantir que o navegador não esteja fornecendo arquivos obsoletos. Você pode corrigir isso limpando o cache do navegador ou iniciando uma nova sessão do navegador.

O AEM também tenta armazenar as bibliotecas de clientes em cache para melhorar o desempenho. Ocasionalmente, após a implantação de um código, os arquivos mais antigos são enviados. Você pode invalidar manualmente o cache das bibliotecas de clientes do AEM utilizando a [ferramenta Recompilar bibliotecas de clientes](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html). *Invalidar caches é o método mais aconselhável se você suspeitar que o AEM armazenou em cache uma versão antiga de uma biblioteca do cliente. A ferramenta Recompilar bibliotecas é ineficaz e demorada.*

## Parabéns {#congratulations}

Você acabou de criar o estilo do seu primeiro componente principal AEM CIF e usou um servidor de desenvolvimento de webpack!

## Desafio extra {#bonus-challenge}

Utilize o [Sistema de estilo do AEM](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/developing/components/style-system.translate.html) para criar dois estilos que podem ser ativados/desativados por um autor de conteúdo. Em [Desenvolvimento com o sistema de estilo](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) você encontra informações detalhadas com todas as etapas para fazê-lo.

![Desafio extra — Sistema de estilo](../assets/style-cif-component/bonus-challenge.png)

## Recursos adicionais {#additional-resources}

* [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
* [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components)
* [Configurar um Ambiente de desenvolvimento do AEM local](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [Bibliotecas do lado do cliente](/help/implementing/developing/introduction/clientlibs.md)
* [Introdução ao AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
* [Desenvolvimento com o sistema de estilo](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
