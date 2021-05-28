---
title: Usar bibliotecas do lado do cliente no AEM as a Cloud Service
description: O AEM fornece Pastas de biblioteca do lado do cliente, que permitem armazenar o código do lado do cliente (clientlibs) no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser apresentada ao cliente
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2561'
ht-degree: 0%

---

# Usar bibliotecas do lado do cliente no AEM como um Cloud Service {#using-client-side-libraries}

As experiências digitais dependem muito do processamento no lado do cliente impulsionado por códigos complexos de JavaScript e CSS. AEM bibliotecas do lado do cliente (clientlibs) permitem organizar e armazenar centralmente essas bibliotecas do lado do cliente no repositório. Junto com o [processo de build front-end no arquétipo de Projeto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) o gerenciamento do código front-end para o seu projeto AEM se torna simples.

As vantagens de usar clientlibs no AEM incluem:

* O código do lado do cliente é armazenado no repositório como todos os outros códigos e conteúdos do aplicativo
* Clientlibs no AEM pode agregar todos os CSS e JS em um único arquivo
* Exponha clientlibs por um caminho que seja acessível por meio do [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Permite a reescrita de caminhos para arquivos ou imagens referenciados

Clientlibs são a solução integrada para fornecer CSS e Javascript a partir da AEM.

>[!TIP]
>
>Os desenvolvedores de front-end que estão criando CSS e Javascript para projetos de AEM também devem se familiarizar com o [AEM Arquétipo de projeto e seu processo de build de front-end automatizado.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## O que são bibliotecas do lado do cliente {#what-are-clientlibs}

Os sites exigem JavaScript e CSS, bem como recursos estáticos, como ícones e fontes da Web para serem processados no lado do cliente. Uma clientlib é AEM mecanismo para fazer referência (por categoria, se necessário) e servir esses recursos.

O AEM coleta o CSS e o Javascript do site em um único arquivo, em um local central, para garantir que apenas uma cópia de qualquer recurso esteja incluída na saída HTML. Isso maximiza a eficiência do delivery e permite que esses recursos sejam mantidos centralmente no repositório por proxy, mantendo o acesso seguro.

## Desenvolvimento front-end para AEM como Cloud Service {#fed-for-aemaacs}

Todos os ativos JavaScript, CSS e outros ativos front-end devem ser mantidos no módulo [ui.front-end do Arquétipo de projeto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) A flexibilidade do arquétipo permite usar as ferramentas modernas da Web preferidas para criar e gerenciar esses recursos.

O arquétipo pode então compilar os recursos em um único arquivo CSS e JS, incorporando-os automaticamente em um `cq:clientLibraryFolder` no repositório.

## Estrutura da pasta da biblioteca do lado do cliente {#clientlib-folders}

Uma pasta de biblioteca do lado do cliente é um nó de repositório do tipo `cq:ClientLibraryFolder`. Sua definição em [Notação CND](https://jackrabbit.apache.org/node-type-notation.html) é

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` os nós podem ser colocados em qualquer lugar dentro da  `/apps` subárvore do repositório.
* Use a propriedade `categories` do nó para identificar as categorias da biblioteca à qual pertence.

Cada `cq:ClientLibraryFolder` é preenchido com um conjunto de arquivos JS e/ou CSS, juntamente com alguns arquivos de suporte (veja abaixo). As propriedades importantes do `cq:ClientLibraryFolder` são configuradas da seguinte maneira:

* `allowProxy`: Como todas as clientlibs devem ser armazenadas em  `apps`, essa propriedade permite acessar as bibliotecas de clientes por meio do servlet proxy. Consulte [Localizando uma pasta da biblioteca do cliente e Usando o Servlet de bibliotecas do cliente proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) abaixo.
* `categories`: Identifica as categorias em que o conjunto de arquivos JS e/ou CSS  `cq:ClientLibraryFolder` é incluído. A propriedade `categories`, com vários valores, permite que uma pasta de biblioteca faça parte de mais de uma categoria (veja abaixo como isso pode ser útil).

Se a pasta da biblioteca do cliente contiver um ou mais arquivos de origem que, no tempo de execução, serão mesclados em um único arquivo JS e/ou CSS. O nome do arquivo gerado é o nome do nó com a extensão de nome de arquivo `.js` ou `.css`. Por exemplo, o nó da biblioteca chamado `cq.jquery` resulta no arquivo gerado chamado `cq.jquery.js` ou `cq.jquery.css`.

As pastas da biblioteca de clientes contêm os seguintes itens:

* Os arquivos de origem JS e/ou CSS
* Recursos estáticos que oferecem suporte a estilos de CSS, como ícones, fontes da Web etc.
* Um arquivo `js.txt` e/ou um arquivo `css.txt` que identifica os arquivos de origem a serem mesclados nos arquivos JS e/ou CSS gerados

![Arquitetura do clientlib](assets/clientlib-architecture.drawio.png)

## Criação de pastas de biblioteca do lado do cliente {#creating-clientlib-folders}

As bibliotecas de clientes devem estar localizadas em `/apps`. Isso é feito para isolar melhor o código do conteúdo e da configuração.

Para que as bibliotecas de clientes em `/apps` sejam acessíveis, um serviço proxy é usado. As ACLs ainda são aplicadas na pasta da biblioteca do cliente, mas o servlet permite que o conteúdo seja lido por `/etc.clientlibs/` se a propriedade `allowProxy` estiver definida como `true`.

1. Abra o CRXDE Lite em um navegador da Web (`https://<host>:<port>/crx/de`).
1. Selecione a pasta `/apps` e clique em **Criar > Criar nó**.
1. Insira um nome para a pasta da biblioteca e, na lista **Type**, selecione `cq:ClientLibraryFolder`. Clique em **OK** e em **Salvar tudo**.
1. Para especificar a categoria ou categorias à qual a biblioteca pertence, selecione o nó `cq:ClientLibraryFolder`, adicione a seguinte propriedade e clique em **Salvar tudo**:
   * Nome: `categories`
   * Tipo: String
   * Valor: O nome da categoria
   * Várias: Selecionado
1. Para que as bibliotecas de clientes sejam acessíveis via proxy em `/etc.clientlibs`, selecione o nó `cq:ClientLibraryFolder`, adicione a seguinte propriedade e clique em **Salvar tudo**:
   * Nome: `allowProxy`
   * Tipo: booliano
   * Valor: `true`
1. Se precisar gerenciar recursos estáticos, crie uma subpasta chamada `resources` abaixo da pasta da biblioteca do cliente.
   * Se você armazenar recursos estáticos na pasta `resources`, eles não poderão ser referenciados em uma instância de publicação.
1. Adicione arquivos de origem à pasta da biblioteca.
   * Normalmente, isso é feito pelo processo de build de front-end do [Arquétipo de projeto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Você pode organizar os arquivos de origem em subpastas, se desejar.
1. Selecione a pasta da biblioteca do cliente e clique em **Criar > Criar arquivo**.
1. Na caixa Nome do arquivo, digite um dos seguintes nomes de arquivo e clique em OK:
   * **`js.txt`:** use esse nome de arquivo para gerar um arquivo JavaScript.
   * **`css.txt`:** use esse nome de arquivo para gerar uma Folha de estilos em cascata.
1. Abra o arquivo e digite o seguinte texto para identificar a raiz do caminho dos arquivos de origem:
   * `#base=*[root]*`
   * Substitua `[root]` pelo caminho para a pasta que contém os arquivos de origem, em relação ao arquivo TXT. Por exemplo, use o seguinte texto quando os arquivos de origem estiverem na mesma pasta do arquivo TXT:
      * `#base=.`
   * O código a seguir define a raiz como a pasta nomeada móvel abaixo do nó `cq:ClientLibraryFolder`:
      * `#base=mobile`
1. Nas linhas abaixo de `#base=[root]`, digite os caminhos dos arquivos de origem relativos à raiz. Coloque cada nome de arquivo em uma linha separada.
1. Clique em **Salvar tudo**.

## Servindo bibliotecas do lado do cliente {#serving-clientlibs}

Assim que sua pasta da biblioteca do cliente estiver [configurada conforme necessário,](#creating-clientlib-folders) suas clientlibs poderão ser solicitadas por proxy. Como exemplo:

* Você tem uma clientlib em `/apps/myproject/clientlibs/foo`
* Você tem uma imagem estática em `/apps/myprojects/clientlibs/foo/resources/icon.png`

A propriedade `allowProxy` permite solicitar:

* A clientlib via j`/etc.clientlibs/myprojects/clientlibs/foo.js`
* A imagem estática via `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Carregamento de bibliotecas de clientes via HTL {#loading-via-htl}

Depois que as clientlibs forem armazenadas e gerenciadas com êxito na pasta da biblioteca do cliente, elas poderão ser acessadas via HTL.

As bibliotecas de clientes são carregadas por meio de um modelo auxiliar fornecido pelo AEM, que pode ser acessado por meio de `data-sly-use`. Os modelos de ajuda estão disponíveis neste arquivo, que pode ser chamado por meio de `data-sly-call`.

Cada modelo de auxiliar espera uma opção `categories` para fazer referência às bibliotecas de clientes desejadas. Essa opção pode ser uma matriz de valores de string ou uma string contendo uma lista de valores separados por vírgula.

[Consulte a ](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) documentação do HTL para obter mais detalhes sobre como carregar clientlibs via HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Bibliotecas de clientes no autor versus publicar {#clientlibs-author-publish}

A maioria das clientlibs será necessária na instância de publicação do AEM. Ou seja, a maioria dos objetivos das clientlibs é produzir a experiência do usuário final do conteúdo. Para clientlibs em instâncias de publicação, [ferramentas de compilação front-end](#fed-for-aemaacs) podem ser usadas e implantadas por meio de [pastas de biblioteca do cliente, conforme descrito acima.](#creating-clientlib-folders)

No entanto, algumas vezes, as bibliotecas de clientes podem ser necessárias para personalizar a experiência de criação. Por exemplo, personalizar uma caixa de diálogo pode exigir a implantação de pequenos bits de CSS ou JS na instância de criação do AEM.

### Gerenciando bibliotecas de clientes no autor {#clientlibs-on-author}

Se precisar usar bibliotecas de clientes no autor, poderá criar suas bibliotecas de clientes em `/apps` usando os mesmos métodos de publicação, mas gravá-las diretamente em `/apps/.../clientlibs/foo` em vez de criar um projeto inteiro para gerenciá-las.

Em seguida, você pode &quot;conectar&quot; ao JS de criação adicionando suas bibliotecas de clientes a uma categoria de biblioteca de clientes pronta para uso.

## Ferramentas de depuração {#debugging-tools}

O AEM fornece várias ferramentas para depurar e testar as pastas da biblioteca do cliente.

### Discover Client Library {#discover-client-libraries}

O componente `/libs/cq/granite/components/dumplibs/dumplibs` gera uma página de informações sobre todas as pastas da biblioteca do cliente no sistema. O nó `/libs/granite/ui/content/dumplibs` tem o componente como um tipo de recurso. Para abrir a página, use o seguinte URL (alterando o host e a porta, conforme necessário):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

As informações incluem o caminho e o tipo da biblioteca (CSS ou JS) e os valores dos atributos da biblioteca, como categorias e dependências. As tabelas subsequentes na página mostram as bibliotecas em cada categoria e canal.

### Consulte Saída gerada {#see-generated-output}

O componente `dumplibs` inclui um seletor de teste que exibe o código-fonte gerado para as tags `ui:includeClientLib`. A página inclui código para diferentes combinações de js, css e atributos temáticos.

1. Use um dos métodos a seguir para abrir a página Saída de teste:
   * Na página `dumplibs.html`, clique no link no texto **Clique aqui para obter o teste de saída**.
   * Abra o seguinte URL no navegador da Web (use um host e uma porta diferentes, conforme necessário):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * A página padrão mostra a saída de tags sem valor para o atributo de categorias.
1. Para ver a saída de uma categoria, digite o valor da propriedade `categories` da biblioteca do cliente e clique em **Enviar consulta**.

## Recursos adicionais da pasta da biblioteca do cliente {#additional-features}

Há vários outros recursos compatíveis com as pastas da biblioteca do cliente no AEM. No entanto, estas não são exigidas no AEM como Cloud Service e, como tal, a sua utilização é desencorajada. Eles estão listados aqui para estarem completos.

>[!WARNING]
>
>Esses recursos adicionais das Pastas da biblioteca do cliente não são necessários no AEM como um Cloud Service e, como tal, seu uso é desencorajado. Eles estão listados aqui para estarem completos.

### Gerenciador da biblioteca HTML do Adobe Granite {#html-library-manager}

Configurações adicionais da biblioteca do cliente podem ser controladas por meio do painel **Gerenciador da biblioteca HTML do Adobe Granite** do Console do Sistema em `https://<host>:<port>/system/console/configMgr`).

### Propriedades Adicionais da Pasta {#additional-folder-properties}

As propriedades adicionais da pasta incluem permitir o controle de dependências e incorporações, mas geralmente não são mais necessárias e seu uso é desencorajado:

* `dependencies`: Esta é uma lista de outras categorias da biblioteca do cliente das quais essa pasta da biblioteca depende. Por exemplo, dados os dois nós `cq:ClientLibraryFolder` `F` e `G`, se um arquivo em `F` exigir outro arquivo em `G` para funcionar corretamente, pelo menos um dos `categories` de `G` deverá estar entre os `dependencies` de `F`.
* `embed`: Usado para incorporar o código de outras bibliotecas. Se o nó `F` incorporar nós `G` e `H`, o HTML resultante será uma concatenação de conteúdo de nós `G` e `H`.

### Vincular a dependências {#linking-to-dependencies}

Quando o código na pasta da biblioteca do cliente fizer referência a outras bibliotecas, identifique as outras bibliotecas como dependências. A tag `ui:includeClientLib` que faz referência à pasta da biblioteca do cliente faz com que o código HTML inclua um link para o arquivo da biblioteca gerado, bem como as dependências.

As dependências devem ser outro `cq:ClientLibraryFolder`. Para identificar dependências, adicione uma propriedade ao nó `cq:ClientLibraryFolder` com os seguintes atributos:

* **Nome:** dependências
* **Tipo:** sequência de caracteres[]
* **Valores:** O valor da propriedade categories do nó cq:ClientLibraryFolder da qual a pasta de biblioteca atual depende.

Por exemplo, `/etc/clientlibs/myclientlibs/publicmain` tem uma dependência na biblioteca `cq.jquery`. A página que faz referência à biblioteca principal do cliente gera um HTML que inclui o seguinte código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporando código de outras bibliotecas {#embedding-code-from-other-libraries}

Você pode incorporar o código de uma biblioteca do cliente em outra biblioteca do cliente. No tempo de execução, os arquivos JS e CSS gerados da biblioteca de incorporação incluem o código da biblioteca incorporada.

A incorporação do código é útil para fornecer acesso a bibliotecas que são armazenadas em áreas seguras do repositório.

#### Pastas da biblioteca do cliente específicas do aplicativo {#app-specific-client-library-folders}

É uma prática recomendada manter todos os arquivos relacionados ao aplicativo em sua pasta de aplicativo abaixo `/app`. Também é uma prática recomendada negar o acesso dos visitantes do site à pasta `/app`. Para atender às duas práticas recomendadas, crie uma pasta de biblioteca do cliente abaixo da pasta `/etc` que incorpora a biblioteca do cliente que está abaixo de `/app`.

Use a propriedade categories para identificar a pasta da biblioteca de clientes a ser incorporada. Para incorporar a biblioteca, adicione uma propriedade ao nó de incorporação `cq:ClientLibraryFolder`, usando os seguintes atributos de propriedade:

* **Nome:** embed
* **Tipo:** sequência de caracteres[]
* **Valor:** o valor da propriedade categories do  `cq:ClientLibraryFolder` nó a ser incorporado.

#### Usando a Incorporação para Minimizar Solicitações {#using-embedding-to-minimize-requests}

Em alguns casos, você pode descobrir que o HTML final gerado para a página típica pela sua instância de publicação inclui um número relativamente grande de elementos `<script>`.

Nesses casos, pode ser útil combinar todo o código da biblioteca do cliente necessário em em um único arquivo para que o número de solicitações de frente e verso no carregamento da página seja reduzido. Para fazer isso, você pode `embed` as bibliotecas necessárias na biblioteca do cliente específica do aplicativo usando a propriedade embed do nó `cq:ClientLibraryFolder`.

#### Caminhos em arquivos CSS {#paths-in-css-files}

Quando você incorpora arquivos CSS, o código CSS gerado usa caminhos para recursos que são relativos à biblioteca de incorporação. Por exemplo, a biblioteca acessível publicamente `/etc/client/libraries/myclientlibs/publicmain` incorpora a biblioteca do cliente `/apps/myapp/clientlib`:

O arquivo `main.css` contém o seguinte estilo:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

O arquivo CSS gerado pelo nó `publicmain` contém o seguinte estilo, usando o URL da imagem original:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Consulte Arquivos incorporados na saída HTML {#see-embedded-files}

Para rastrear a origem do código incorporado ou garantir que as bibliotecas de clientes incorporadas estejam produzindo os resultados esperados, você pode ver os nomes dos arquivos que estão sendo incorporados no tempo de execução. Para ver os nomes dos arquivos, anexe o parâmetro `debugClientLibs=true` ao URL da página da Web. A biblioteca gerada contém instruções `@import` em vez do código incorporado.

No exemplo na seção anterior [Incorporando código de outras bibliotecas](#embedding-code-from-other-libraries), a pasta `/etc/client/libraries/myclientlibs/publicmain` da biblioteca do cliente incorpora a pasta `/apps/myapp/clientlib` da biblioteca do cliente. Anexar o parâmetro à página da Web produz o seguinte link no código-fonte da página da Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Abrir o arquivo `publicmain.css` revela o seguinte código:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Na caixa de endereço do navegador da Web, anexe o seguinte texto ao URL do seu HTML:
   * `?debugClientLibs=true`
1. Quando a página for carregada, visualize a fonte da página.
1. Clique no link fornecido como href para o elemento do link para abrir o arquivo e exibir o código-fonte.

### Uso de pré-processadores {#using-preprocessors}

O AEM permite pré-processadores e entregas conectáveis com suporte para [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS e JavaScript e [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript com YUI definido como AEM pré-processador padrão.

Os pré-processadores conectáveis permitem uma utilização flexível, incluindo:

* Definindo ScriptProcessors que podem processar fontes de script
* Os processadores são configuráveis com opções
* Os processadores podem ser usados para minificação, mas também para casos não minificados
* A clientlib pode definir qual processador usar

>[!NOTE]
>
>Por padrão, o AEM usa o Compactador YUI. Consulte a [documentação do YUI Compressor GitHub](https://github.com/yui/yuicompressor/issues) para obter uma lista de problemas conhecidos. Alternar para o compressor GCC para clientlibs específicas pode resolver alguns problemas observados ao usar YUI.

>[!CAUTION]
>
>Não coloque uma biblioteca minificada em uma biblioteca do cliente. Em vez disso, forneça a biblioteca bruta e, se a minificação for necessária, use as opções dos pré-processadores.

#### Uso {#usage}

Você pode optar por configurar a configuração de pré-processadores por biblioteca do cliente ou todo o sistema.

* Adicione as propriedades de vários valores `cssProcessor` e `jsProcessor` no nó clientlibrary
* Ou defina a configuração padrão do sistema por meio da configuração **Gerenciador de biblioteca HTML** OSGi

Uma configuração de pré-processador no nó clientlib tem prioridade sobre a configuração OSGI.

#### Formato e exemplos {#format-and-examples}

##### Formato {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### Compactador YUI para Minificação de CSS e GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Digitar para pré-processar e, em seguida, GCC para minificar e ofuscar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### Opções adicionais do GCC {#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Para obter mais detalhes sobre as opções do GCC, consulte a [documentação do GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Definir Minificador Padrão do Sistema {#set-system-default-minifier}

A IU é definida como minificador padrão no AEM. Para alterar para GCC, siga estas etapas.

1. Vá para o Apache Felix Config Manager em (`http://<host>:<portY/system/console/configMgr`)
1. Localize e edite o **Gerenciador da biblioteca HTML do Adobe Granite**.
1. Ative a opção **Minimizar** (se ainda não estiver ativada).
1. Defina o valor **Configurações padrão do processador JS** para `min:gcc`.
   * As opções podem ser passadas se separadas por um ponto e vírgula, por exemplo `min:gcc;obfuscate=true`.
1. Clique em **Save** para salvar as alterações.
