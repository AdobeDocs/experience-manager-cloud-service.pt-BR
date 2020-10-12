---
title: Uso de bibliotecas do lado do cliente em AEM como Cloud Service
description: AEM fornece as Pastas de biblioteca do lado do cliente, que permitem armazenar o código do lado do cliente (clientlibs) no repositório, organizá-lo no categoria e definir quando e como cada categoria de código deve ser fornecida ao cliente
translation-type: tm+mt
source-git-commit: d4c031e17c0c83e44b687474502252c89ed37922
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 1%

---


# Uso de bibliotecas do lado do cliente em AEM como Cloud Service {#using-client-side-libraries}

As experiências digitais dependem muito do processamento no cliente, conduzido por códigos complexos de JavaScript e CSS. AEM bibliotecas do lado do cliente (clientlibs) permitem organizar e armazenar centralmente essas bibliotecas do lado do cliente no repositório. Em conjunto com o processo de compilação [front-end no arquétipo AEM Project,](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html) o gerenciamento do código front-end para o seu projeto AEM se torna simples.

As vantagens de usar clientlibs em AEM incluem:

* O código do cliente é armazenado no repositório como todo o outro código e conteúdo do aplicativo
* Clientlibs no AEM podem agregação todos os CSS e JS em um único arquivo
* Exponha clientlibs por um caminho que pode ser acessado pelo [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Permite a regravação de caminhos para arquivos ou imagens referenciados

Clientlibs são a solução integrada para fornecer CSS e Javascript da AEM.

>[!TIP]
>
>Os desenvolvedores de front-end que estão criando CSS e Javascript para projetos AEM também devem se familiarizar com o [AEM Project Archetype e seu processo automatizado de construção de front-end.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## O que são bibliotecas do lado do cliente {#what-are-clientlibs}

Os sites exigem JavaScript e CSS, bem como recursos estáticos, como ícones e fontes da Web, para serem processados no cliente. Uma clientlib é AEM mecanismo de referência (por categoria, se necessário) e que serve tais recursos.

AEM coleta o CSS e o Javascript do site em um único arquivo, em um local central, para garantir que apenas uma cópia de qualquer recurso seja incluída na saída HTML. Isso maximiza a eficiência do delivery e permite que esses recursos sejam mantidos centralmente no repositório por proxy, mantendo o acesso protegido.

## Desenvolvimento front-end para AEM como Cloud Service {#fed-for-aemaacs}

Todos os ativos JavaScript, CSS e outros ativos front-end devem ser mantidos no módulo [ui.front-end do AEM Project Archetype.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html) A flexibilidade do arquétipo permite usar as ferramentas da Web modernas de sua escolha para criar e gerenciar esses recursos.

O arquétipo pode, então, compilar os recursos em um único arquivo CSS e JS, incorporando-os automaticamente em um `cq:clientLibraryFolder` repositório.

## Estrutura da pasta da biblioteca do lado do cliente {#clientlib-folders}

Uma pasta de biblioteca do lado do cliente é um nó de repositório do tipo `cq:ClientLibraryFolder`. Sua definição na notação [da](https://jackrabbit.apache.org/node-type-notation.html) CND é

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` os nós podem ser colocados em qualquer lugar dentro da `/apps` subárvore do repositório.
* Use a `categories` propriedade do nó para identificar as categorias de biblioteca às quais ele pertence.

Cada um `cq:ClientLibraryFolder` é preenchido com um conjunto de arquivos JS e/ou CSS, juntamente com alguns arquivos de suporte (veja abaixo). As propriedades importantes do `cq:ClientLibraryFolder` são configuradas da seguinte maneira:

* `allowProxy`: Como todas as clientlibs devem ser armazenadas em `apps`, essa propriedade permite o acesso às bibliotecas de clientes por meio do servlet proxy. Consulte [Localizando uma pasta da biblioteca do cliente e Usando o Servlet](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) de bibliotecas do cliente proxy abaixo.
* `categories`: Identifica as categorias nas quais o conjunto de arquivos JS e/ou CSS nesse `cq:ClientLibraryFolder` intervalo. A `categories` propriedade, sendo de vários valores, permite que uma pasta da biblioteca faça parte de mais de uma categoria (veja abaixo como isso pode ser útil).

Se a pasta da biblioteca do cliente contiver um ou mais arquivos de origem que, em tempo de execução, serão mesclados em um único arquivo JS e/ou CSS. O nome do arquivo gerado é o nome do nó com a extensão do nome do arquivo `.js` ou `.css` . Por exemplo, o nó da biblioteca nomeado `cq.jquery` resulta no arquivo gerado chamado `cq.jquery.js` ou `cq.jquery.css`.

As pastas da biblioteca do cliente contêm os seguintes itens:

* Os arquivos de origem JS e/ou CSS
* Recursos estáticos compatíveis com estilos CSS, como ícones, fontes da Web etc.
* Um `js.txt` arquivo e/ou um `css.txt` arquivo que identifica os arquivos de origem a serem mesclados nos arquivos JS e/ou CSS gerados

![Arquitetura clientlib](assets/clientlib-architecture.drawio.png)

## Criando Pastas de Biblioteca do Lado do Cliente {#creating-clientlib-folders}

As bibliotecas do cliente devem estar localizadas em `/apps`. Isso é feito para isolar melhor o código do conteúdo e da configuração.

Para que as bibliotecas do cliente possam `/apps` ser acessadas, um servidor proxy é usado. As ACLs ainda são aplicadas na pasta da biblioteca do cliente, mas o servlet permite que o conteúdo seja lido via `/etc.clientlibs/` se a `allowProxy` propriedade estiver definida como `true`.

1. Open CRXDE Lite in a web browser (`https://<host>:<port>/crx/de`).
1. Selecione a `/apps` pasta e clique em **Criar > Criar nó**.
1. Digite um nome para a pasta da biblioteca e, na opção **lista Type** , selecione `cq:ClientLibraryFolder`. Clique em **OK** e em **Salvar tudo**.
1. Para especificar a categoria ou as categorias às quais a biblioteca pertence, selecione o `cq:ClientLibraryFolder` nó, adicione a seguinte propriedade e clique em **Salvar tudo**:
   * Nome: `categories`
   * Tipo: String
   * Valor: O nome da categoria
   * Vários: Selecionado
1. Para que as bibliotecas do cliente sejam acessíveis via proxy em `/etc.clientlibs`, selecione o `cq:ClientLibraryFolder` nó, adicione a seguinte propriedade e clique em **Salvar tudo**:
   * Nome: `allowProxy`
   * Tipo: booliano
   * Valor: `true`
1. Se precisar gerenciar recursos estáticos, crie uma subpasta com o nome `resources` abaixo da pasta da biblioteca do cliente.
   * Se você armazenar recursos estáticos na pasta `resources`, eles não poderão ser referenciados em uma instância de publicação.
1. Adicione arquivos de origem à pasta da biblioteca.
   * Normalmente, isso é feito pelo processo de compilação front-end do [AEM Project Archetype.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Se desejar, você pode organizar os arquivos de origem em subpastas.
1. Selecione a pasta da biblioteca do cliente e clique em **Criar > Criar arquivo**.
1. Na caixa Nome do arquivo, digite um dos seguintes nomes de arquivo e clique em OK:
   * **`js.txt`:** Use esse nome de arquivo para gerar um arquivo JavaScript.
   * **`css.txt`:** Use esse nome de arquivo para gerar uma folha de estilos em cascata.
1. Abra o arquivo e digite o seguinte texto para identificar a raiz do caminho dos arquivos de origem:
   * `#base=*[root]*`
   * Substitua `[root]` pelo caminho para a pasta que contém os arquivos de origem, em relação ao arquivo TXT. Por exemplo, use o seguinte texto quando os arquivos de origem estiverem na mesma pasta que o arquivo TXT:
      * `#base=.`
   * O código a seguir define a raiz como a pasta chamada mobile abaixo do `cq:ClientLibraryFolder` nó:
      * `#base=mobile`
1. Nas linhas abaixo `#base=[root]`, digite os caminhos dos arquivos de origem relativos à raiz. Coloque cada nome de arquivo em uma linha separada.
1. Clique em **Salvar tudo**.

## Servindo bibliotecas do lado do cliente {#serving-clientlibs}

Assim que a pasta da biblioteca do cliente for [configurada conforme necessário,](#creating-clientlib-folders) seus clientlibs poderão ser solicitados via proxy. Como exemplo:

* Você tem uma clientlib em `/apps/myproject/clientlibs/foo`
* Você tem uma imagem estática em `/apps/myprojects/clientlibs/foo/resources/icon.png`

A `allowProxy` propriedade permite solicitar:

* A clientlib via j`/etc.clientlibs/myprojects/clientlibs/foo.js`
* A imagem estática via `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Carregamento de bibliotecas de clientes via HTL {#loading-via-htl}

Depois que seus clientlibs forem armazenados e gerenciados com êxito na pasta da biblioteca do cliente, eles poderão ser acessados via HTL.

As bibliotecas do cliente são carregadas por meio de um modelo auxiliar fornecido pela AEM, que pode ser acessado por meio `data-sly-use`. Os modelos de ajuda estão disponíveis neste arquivo, que pode ser chamado até `data-sly-call`.

Cada modelo de ajuda espera uma `categories` opção para fazer referência às bibliotecas de clientes desejadas. Essa opção pode ser uma matriz de valores de string ou uma string contendo uma lista de valores separados por vírgula.

[Consulte a documentação](https://docs.adobe.com/content/help/en/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) HTL para obter mais detalhes sobre como carregar clientlibs via HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Bibliotecas do cliente no autor versus publicação {#clientlibs-author-publish}

A maioria dos clientlibs será necessária na instância de publicação AEM. Ou seja, a maioria dos propósitos dos clientlibs é produzir a experiência do usuário final do conteúdo. Para clientlibs em instâncias de publicação, as ferramentas [de criação](#fed-for-aemaacs) front-end podem ser usadas e implantadas pelas pastas da biblioteca [do cliente, conforme descrito acima.](#creating-clientlib-folders)

No entanto, algumas vezes, as bibliotecas do cliente podem ser necessárias para personalizar a experiência de criação. Por exemplo, personalizar uma caixa de diálogo pode exigir a implantação de pequenos bits de CSS ou JS para a instância de criação AEM.

### Gerenciando bibliotecas de clientes no autor {#clientlibs-on-author}

Se precisar usar bibliotecas de clientes no autor, você poderá criar suas bibliotecas de clientes usando `/apps` os mesmos métodos que para publicação, mas escreva-os diretamente em `/apps/.../clientlibs/foo` vez de criar um projeto inteiro para gerenciá-lo.

Em seguida, você pode &quot;conectar&quot; ao JS de criação adicionando suas bibliotecas de cliente a uma categoria predefinida da biblioteca de cliente.

## Ferramentas de depuração {#debugging-tools}

AEM fornece várias ferramentas para depurar e testar pastas da biblioteca do cliente.

### Bibliotecas do Discover Client {#discover-client-libraries}

O `/libs/cq/granite/components/dumplibs/dumplibs` componente gera uma página de informações sobre todas as pastas da biblioteca do cliente no sistema. O `/libs/granite/ui/content/dumplibs` nó tem o componente como um tipo de recurso. Para abrir a página, use o seguinte URL (alterando o host e a porta, conforme necessário):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

As informações incluem o caminho e o tipo da biblioteca (CSS ou JS) e os valores dos atributos da biblioteca, como categorias e dependências. As tabelas subsequentes na página mostram as bibliotecas em cada categoria e canal.

### Consulte Saída gerada {#see-generated-output}

O `dumplibs` componente inclui um seletor de teste que exibe o código-fonte gerado para `ui:includeClientLib` as tags. A página inclui código para diferentes combinações de atributos js, css e temáticos.

1. Use um dos seguintes métodos para abrir a página Saída de teste:
   * Na `dumplibs.html` página, clique no link no texto **Clique aqui para teste** de saída.
   * Abra o seguinte URL no navegador da Web (use um host e uma porta diferentes, conforme necessário):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * A página padrão mostra a saída de tags sem valor para o atributo categoria.
1. Para ver a saída de uma categoria, digite o valor da propriedade da biblioteca do cliente `categories` e clique em **Enviar Query**.

## Recursos adicionais da pasta da biblioteca do cliente {#additional-features}

Há vários outros recursos que são suportados pelas pastas da biblioteca do cliente no AEM. No entanto, estes não são necessários para AEM como Cloud Service e, como tal, a sua utilização é desencorajada. Eles estão listados aqui para estarem completos.

>[!WARNING]
>
>Esses recursos adicionais das Pastas de biblioteca do cliente não são necessários em AEM como Cloud Service e, como tal, seu uso é desencorajado. Eles estão listados aqui para estarem completos.

### Adobe Granite HTML LIbrary Manager {#html-library-manager}

As configurações adicionais da biblioteca do cliente podem ser controladas por meio do painel **Adobe Granite HTML Library Manager** do console do sistema em `https://<host>:<port>/system/console/configMgr`).

### Propriedades adicionais da pasta {#additional-folder-properties}

As propriedades adicionais da pasta incluem permitir o controle de dependências e incorporações, mas geralmente não são mais necessárias e seu uso é desencorajado:

* `dependencies`: Esta é uma lista de outras categorias da biblioteca do cliente das quais esta pasta da biblioteca depende. Por exemplo, dados dois `cq:ClientLibraryFolder` nós `F` e `G`, se um arquivo em `F` requer outro arquivo `G` para funcionar corretamente, então pelo menos um dos `categories` nós `G` deve estar entre os `dependencies` de `F`.
* `embed`: Usado para incorporar código de outras bibliotecas. Se o nó `F` incorporar nós `G` e `H`, o HTML resultante será uma concatenação de conteúdo de nós `G` e `H`.

### Vincular a dependências {#linking-to-dependencies}

Quando o código na pasta da biblioteca do cliente fizer referência a outras bibliotecas, identifique as outras bibliotecas como dependências. A `ui:includeClientLib` tag que faz referência à pasta da biblioteca do cliente faz com que o código HTML inclua um link para o arquivo da biblioteca gerado, bem como as dependências.

As dependências devem ser outras `cq:ClientLibraryFolder`. Para identificar dependências, adicione uma propriedade ao seu `cq:ClientLibraryFolder` nó com os seguintes atributos:

* **Nome:** dependências
* **Tipo:** String[]
* **Valores:** O valor da propriedade categoria do nó cq:ClientLibraryFolder do qual a pasta da biblioteca atual depende.

Por exemplo, o `/etc/clientlibs/myclientlibs/publicmain` tem uma dependência na `cq.jquery` biblioteca. A página que faz referência à biblioteca principal do cliente gera HTML que inclui o seguinte código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporação de código de outras bibliotecas {#embedding-code-from-other-libraries}

Você pode incorporar código de uma biblioteca de cliente em outra biblioteca de cliente. No tempo de execução, os arquivos JS e CSS gerados da biblioteca de incorporação incluem o código da biblioteca incorporada.

A incorporação do código é útil para fornecer acesso às bibliotecas que são armazenadas em áreas protegidas do repositório.

#### Pastas da biblioteca de clientes específicas do aplicativo {#app-specific-client-library-folders}

É uma prática recomendada manter todos os arquivos relacionados ao aplicativo em sua pasta de aplicativos abaixo `/app`. Também é uma prática recomendada negar o acesso de visitantes do site à `/app` pasta. Para satisfazer ambas as práticas recomendadas, crie uma pasta da biblioteca do cliente abaixo da `/etc` pasta que incorpora a biblioteca do cliente abaixo `/app`.

Use a propriedade categoria para identificar a pasta da biblioteca do cliente a ser incorporada. Para incorporar a biblioteca, adicione uma propriedade ao `cq:ClientLibraryFolder` nó de incorporação, usando os seguintes atributos de propriedade:

* **Nome:** embed
* **Tipo:** String[]
* **Valor:** O valor da propriedade categoria do `cq:ClientLibraryFolder` nó a ser incorporado.

#### Uso da incorporação para minimizar solicitações {#using-embedding-to-minimize-requests}

Em alguns casos, você pode descobrir que o HTML final gerado para a página típica pela sua instância de publicação inclui um número relativamente grande de `<script>` elementos.

Nesses casos, pode ser útil combinar todo o código da biblioteca do cliente necessário em um único arquivo para que o número de solicitações de ida e volta no carregamento da página seja reduzido. Para fazer isso, você pode inserir `embed` as bibliotecas necessárias na biblioteca de cliente específica do aplicativo usando a propriedade embed do `cq:ClientLibraryFolder` nó.

#### Caminhos em arquivos CSS {#paths-in-css-files}

Quando você incorpora arquivos CSS, o código CSS gerado usa caminhos para recursos relativos à biblioteca de incorporação. Por exemplo, a biblioteca acessível ao público `/etc/client/libraries/myclientlibs/publicmain` incorpora a biblioteca do `/apps/myapp/clientlib` cliente:

O `main.css` arquivo contém o seguinte estilo:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

O arquivo CSS gerado pelo `publicmain` nó contém o seguinte estilo, usando o URL da imagem original:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Consulte Arquivos incorporados na saída HTML {#see-embedded-files}

Para rastrear a origem do código incorporado ou garantir que as bibliotecas de clientes incorporadas produzam os resultados esperados, você pode ver os nomes dos arquivos que estão sendo incorporados no tempo de execução. Para ver os nomes dos arquivos, anexe o `debugClientLibs=true` parâmetro ao URL da sua página da Web. A biblioteca gerada contém `@import` instruções em vez do código incorporado.

No exemplo na seção anterior [Incorporar código de outras bibliotecas](#embedding-code-from-other-libraries) , a pasta da biblioteca do `/etc/client/libraries/myclientlibs/publicmain` cliente incorpora a pasta da biblioteca do `/apps/myapp/clientlib` cliente. Anexar o parâmetro à página da Web produz o seguinte link no código-fonte da página da Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

A abertura do `publicmain.css` arquivo revela o seguinte código:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Na caixa de endereço do navegador da Web, anexe o seguinte texto ao URL do seu HTML:
   * `?debugClientLibs=true`
1. Quando a página for carregada, visualização a fonte da página.
1. Clique no link fornecido como href para o elemento de link para abrir o arquivo e visualização o código fonte.

### Uso de pré-processadores {#using-preprocessors}

AEM permite pré-processadores e entregas conectáveis com suporte para o [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS e JavaScript e o [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript com YUI definido como AEM pré-processador padrão.

Os pré-processadores conectáveis permitem uma utilização flexível, incluindo:

* Definindo ScriptProcessors que podem processar fontes de script
* Os processadores podem ser configurados com opções
* Os processadores podem ser usados para a miniificação, mas também para casos não-reduzidos
* A clientlib pode definir qual processador usar

>[!NOTE]
>
>Por padrão, AEM usa o Compressor YUI. Consulte a documentação [do](https://github.com/yui/yuicompressor/issues) YUI Compressor GitHub para obter uma lista de problemas conhecidos. Mudar para o compressor GCC para clientlibs específicos pode resolver alguns problemas observados ao utilizar IU.

>[!CAUTION]
>
>Não coloque uma biblioteca minimizada em uma biblioteca cliente. Em vez disso, forneça a biblioteca bruta e, se for necessário a miniificação, use as opções dos pré-processadores.

#### Uso {#usage}

Você pode optar por configurar a configuração dos pré-processadores por biblioteca do cliente ou por todo o sistema.

* Adicionar as propriedades multivalue `cssProcessor` e `jsProcessor` no nó clientlibrary
* Ou defina a configuração padrão do sistema por meio da configuração OSGi do Gerenciador **de biblioteca** HTML

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

##### Compressor YUI para Minificação CSS e GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

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

Para obter mais detalhes sobre as opções de GCC, consulte a documentação [do](https://developers.google.com/closure/compiler/docs/compilation_levels)GCC.

#### Definir Miniador Padrão do Sistema {#set-system-default-minifier}

A IU é definida como a miniatura padrão no AEM. Para alterar para GCC, siga estas etapas.

1. Ir para o Apache Felix Config Manager em (`http://<host>:<portY/system/console/configMgr`)
1. Localize e edite o Gerenciador **de biblioteca HTML** Granite.
1. Ative a **opção Minifique** (se ainda não estiver ativada).
1. Defina o valor Configurações padrão do processador **JS** como `min:gcc`.
   * As opções podem ser passadas se separadas por um ponto-e-vírgula, por exemplo `min:gcc;obfuscate=true`.
1. Click **Save** to save the changes.
