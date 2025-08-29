---
title: Uso de bibliotecas do lado do cliente no AEM as a Cloud Service
description: O AEM fornece Pastas de bibliotecas do lado do cliente, que permitem armazenar seu código do lado do cliente (clientlibs) no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser entregue ao cliente
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: da44719521546e81af60e4f8dd5452d83ff5e1e7
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 1%

---


# Uso de bibliotecas do lado do cliente no AEM as a Cloud Service {#using-client-side-libraries}

As experiências digitais dependem muito do processamento do lado do cliente orientado por códigos JavaScript e CSS complexos. As Bibliotecas do lado do cliente do AEM (clientlibs) permitem organizar e armazenar centralmente essas bibliotecas do lado do cliente no repositório. Juntamente com o [processo de compilação de front-end no arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html), o gerenciamento do código de front-end para o seu projeto do AEM torna-se simples.

As vantagens de usar clientlibs no AEM incluem:

* O código do lado do cliente é armazenado no repositório como todo o código e conteúdo do aplicativo
* As bibliotecas de clientes no AEM podem agregar todos os CSS e JS em um único arquivo
* Exponha clientlibs por um caminho acessível por meio do [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Permite a regravação de caminhos para arquivos ou imagens referenciados

As bibliotecas de clientes são a solução integrada para fornecer CSS e JavaScript da AEM.

>[!TIP]
>
>Os desenvolvedores de front-end que estão criando CSS e JavaScript para projetos do AEM também devem se familiarizar com o [Arquétipo de Projetos AEM e seu processo de compilação automatizado de front-end](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html).

## O que são bibliotecas do lado do cliente {#what-are-clientlibs}

Os sites exigem que o JavaScript e o CSS, além de recursos estáticos, como ícones e fontes da Web, sejam processados no lado do cliente. Uma clientlib é o mecanismo do AEM para referenciar (por categoria, se necessário) e veicular esses recursos.

A AEM coleta o CSS e o JavaScript do site em um único arquivo, em um local central, para garantir que apenas uma cópia de qualquer recurso seja incluída na saída do HTML. Isso maximiza a eficiência da entrega e permite que esses recursos sejam mantidos centralmente no repositório via proxy, mantendo o acesso seguro.

## Desenvolvimento de front-end para o AEM as a Cloud Service {#fed-for-aemaacs}

Todos os ativos de JavaScript, CSS e outros ativos de front-end devem ser mantidos no módulo [ui.frontend do Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html). A flexibilidade do arquétipo permite usar suas ferramentas da Web modernas preferidas para criar e gerenciar esses recursos.

O arquétipo pode então compilar os recursos em arquivos CSS e JS únicos, incorporando-os automaticamente em um `cq:clientLibraryFolder` no repositório.

## Estrutura da pasta da biblioteca do lado do cliente {#clientlib-folders}

Uma pasta de biblioteca do lado do cliente é um nó de repositório do tipo `cq:ClientLibraryFolder`. Sua definição em [notação CND](https://jackrabbit.apache.org/node-type-notation.html) é

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* Os nós `cq:ClientLibraryFolder` podem ser colocados em qualquer lugar dentro da subárvore `/apps` do repositório.
* Use a propriedade `categories` do nó para identificar as categorias da biblioteca às quais ele pertence.

Cada `cq:ClientLibraryFolder` é preenchido com um conjunto de arquivos JS e/ou CSS, juntamente com alguns arquivos de suporte (veja abaixo). Propriedades importantes de `cq:ClientLibraryFolder` são configuradas da seguinte maneira:

* `allowProxy`: Como todas as clientlibs devem ser armazenadas em `apps`, esta propriedade permite acesso às bibliotecas de clientes via servlet proxy. Consulte a seção [Localizando uma Pasta de Biblioteca de Cliente e Usando o Servlet de Bibliotecas de Cliente Proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) abaixo.
* `categories`: Identifica as categorias nas quais o conjunto de arquivos JS e/ou CSS neste `cq:ClientLibraryFolder` se enquadra. Como a propriedade `categories` tem vários valores, uma pasta de biblioteca pode fazer parte de mais de uma categoria (veja abaixo como isso pode ser útil).

Se a pasta da biblioteca do cliente contiver um ou mais arquivos de código-fonte que, no tempo de execução, serão mesclados em um único arquivo JS e/ou CSS. O nome do arquivo gerado é o nome do nó com a extensão de nome de arquivo `.js` ou `.css`. Por exemplo, o nó de biblioteca chamado `cq.jquery` resulta no arquivo gerado chamado `cq.jquery.js` ou `cq.jquery.css`.

As pastas da biblioteca do cliente contêm os seguintes itens:

* Os arquivos de origem JS e/ou CSS
* Recursos estáticos que oferecem suporte a estilos CSS, como ícones, fontes da Web e assim por diante.
* Um arquivo `js.txt` e/ou um arquivo `css.txt` que identifica os arquivos de origem a serem mesclados nos arquivos JS e/ou CSS gerados

![Arquitetura do Clientlib](assets/clientlib-architecture.drawio.png)

## Criação de pastas de bibliotecas do lado do cliente {#creating-clientlib-folders}

As bibliotecas de clientes devem estar localizadas em `/apps`. Essa regra é necessária para isolar melhor o código do conteúdo e da configuração.

Para que as bibliotecas de clientes em `/apps` sejam acessíveis, um servidor proxy é usado. As ACLs ainda são impostas na pasta da biblioteca do cliente, mas o servlet permite que o conteúdo seja lido via `/etc.clientlibs/` se a propriedade `allowProxy` estiver definida como `true`.

1. Abra o CRXDE Lite em um navegador da Web (`https://<host>:<port>/crx/de`).
1. Selecione a pasta `/apps` e clique em **Criar > Criar nó**.
1. Insira um nome para a pasta da biblioteca e, na lista **Tipo**, selecione `cq:ClientLibraryFolder`. Clique em **OK** e em **Salvar tudo**.
1. Para especificar a categoria ou categorias às quais a biblioteca pertence, selecione o nó `cq:ClientLibraryFolder`, adicione a seguinte propriedade e clique em **Salvar tudo**:
   * Nome: `categories`
   * Tipo: String
   * Valor: o nome da categoria
   * Multi: selecionado
1. Para que as bibliotecas de clientes sejam acessíveis via proxy em `/etc.clientlibs`, selecione o nó `cq:ClientLibraryFolder`, adicione a seguinte propriedade e clique em **Salvar Tudo**:
   * Nome: `allowProxy`
   * Tipo: Booleano
   * Valor: `true`
1. Se você precisar gerenciar recursos estáticos, crie uma subpasta chamada `resources` abaixo da pasta da biblioteca do cliente.
   * Se você armazenar recursos estáticos em qualquer lugar que não seja na pasta `resources`, eles não poderão ser referenciados em uma instância de publicação.
1. Adicionar arquivos de origem à pasta da biblioteca.
   * Isso normalmente é feito pelo processo de build de front-end do [Arquétipo de Projetos AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html).
   * Você pode organizar os arquivos de origem em subpastas, se desejar.
1. Selecione a pasta da biblioteca do cliente e clique em **Criar > Criar arquivo**.
1. Na caixa Nome do arquivo, digite um dos seguintes nomes de arquivo e clique em OK:
   * **`js.txt`:** Use este nome de arquivo para gerar um arquivo JavaScript.
   * **`css.txt`:** Use este nome de arquivo para gerar uma Folha de Estilos em Cascata.
1. Abra o arquivo e digite o seguinte texto para identificar a raiz do caminho dos arquivos de origem:
   * `#base=*[root]*`
   * Substitua `[root]` pelo caminho para a pasta que contém os arquivos de origem, relativo ao arquivo TXT. Por exemplo, use o seguinte texto quando os arquivos de código-fonte estiverem na mesma pasta que o arquivo TXT:
      * `#base=.`
   * O código a seguir define a raiz como a pasta chamada mobile abaixo do nó `cq:ClientLibraryFolder`:
      * `#base=mobile`
1. Nas linhas abaixo de `#base=[root]`, digite os caminhos dos arquivos de origem relativos à raiz. Coloque cada nome de arquivo em uma linha separada.
1. Clique em **Salvar tudo**.

## Disponibilização de bibliotecas do lado do cliente {#serving-clientlibs}

Assim que a pasta da biblioteca do cliente for [configurada conforme necessário](#creating-clientlib-folders), suas clientlibs poderão ser solicitadas via proxy. Como exemplo:

* Você tem uma clientlib em `/apps/myproject/clientlibs/foo`
* Você tem uma imagem estática em `/apps/myprojects/clientlibs/foo/resources/icon.png`

A propriedade `allowProxy` permite solicitar:

* A clientlib via `/etc.clientlibs/myprojects/clientlibs/foo.js`
* A imagem estática via `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Carregamento de bibliotecas de clientes via HTL {#loading-via-htl}

Depois que as clientlibs forem armazenadas e gerenciadas com êxito na pasta da biblioteca do cliente, elas poderão ser acessadas por HTL.

As bibliotecas de clientes são carregadas por meio de um modelo auxiliar fornecido pela AEM, que pode ser acessado por meio de `data-sly-use`. Modelos auxiliares estão disponíveis neste arquivo, que pode ser chamado através de `data-sly-call`.

Cada modelo auxiliar espera uma opção `categories` para fazer referência às bibliotecas de clientes desejadas. Essa opção pode ser uma matriz de valores de cadeias de caracteres ou uma cadeia contendo uma lista de valores separados por vírgula.

[Consulte a documentação HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) para obter mais detalhes sobre como carregar clientlibs via HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Bibliotecas de clientes no Autor versus Publicar {#clientlibs-author-publish}

A maioria das clientlibs é necessária na instância de publicação do AEM. Ou seja, a finalidade da maioria das clientlibs é produzir a experiência do usuário final do conteúdo. Para clientlibs em instâncias de publicação, as [ferramentas de compilação de front-end](#fed-for-aemaacs) podem ser usadas e implantadas por meio de [pastas de biblioteca do cliente, conforme descrito acima](#creating-clientlib-folders).

No entanto, há momentos em que as bibliotecas de clientes podem ser necessárias para personalizar a experiência de criação. Por exemplo, personalizar uma caixa de diálogo pode exigir a implantação de pequenos bits de CSS ou JS na instância de criação do AEM.

### Gerenciamento de bibliotecas de clientes no Author {#clientlibs-on-author}

Se você precisar usar bibliotecas de clientes no autor, poderá criar suas bibliotecas de clientes em `/apps` usando os mesmos métodos de publicação, mas escreva-as diretamente em `/apps/.../clientlibs/foo` em vez de criar um projeto inteiro para gerenciá-lo.

Em seguida, você pode &quot;conectar&quot; ao JS de criação adicionando suas bibliotecas de clientes a uma categoria de biblioteca de clientes pronta para uso.

## Ferramentas de depuração {#debugging-tools}

O AEM fornece várias ferramentas para depurar e testar pastas da biblioteca do cliente.

### Descubra bibliotecas de clientes {#discover-client-libraries}

O componente `/libs/cq/granite/components/dumplibs/dumplibs` gera uma página de informações sobre todas as pastas da biblioteca do cliente no sistema. O nó `/libs/granite/ui/content/dumplibs` tem o componente como um tipo de recurso. Para abrir a página, use o seguinte URL (alterando o host e a porta conforme necessário):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

As informações incluem o caminho e o tipo da biblioteca (CSS ou JS), bem como os valores dos atributos da biblioteca, como categorias e dependências. As tabelas subsequentes na página mostram as bibliotecas em cada categoria e canal.

### Consulte Saída gerada {#see-generated-output}

O componente `dumplibs` inclui um seletor de teste que exibe o código-fonte gerado para `ui:includeClientLib` tags. A página inclui código para diferentes combinações de js, css e atributos temáticos.

1. Use um dos métodos a seguir para abrir a página Saída do teste:
   * Na página `dumplibs.html`, clique no link no texto **Clique aqui para testar a saída**.
   * Abra o seguinte URL no navegador da Web (use um host e porta diferentes, conforme necessário):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * A página padrão mostra saída para tags sem valor para o atributo categories.
1. Para ver a saída de uma categoria, digite o valor da propriedade `categories` da biblioteca do cliente e clique em **Enviar Consulta**.

## Recursos adicionais da pasta da biblioteca do cliente {#additional-features}

Há vários outros recursos compatíveis com as pastas da biblioteca do cliente no AEM. No entanto, elas não são necessárias no AEM as a Cloud Service e, portanto, seu uso não é incentivado. Eles estão listados aqui para fins de integridade.

>[!WARNING]
>
>Esses recursos adicionais das Pastas da biblioteca do cliente não são necessários no AEM as a Cloud Service e, portanto, seu uso não é incentivado. Eles estão listados aqui para fins de integridade.

### Gerenciador de biblioteca HTML do Adobe Granite {#html-library-manager}

As configurações adicionais da biblioteca do cliente podem ser controladas por meio do painel **Gerenciador de Bibliotecas de HTML do Adobe Granite** do Console do Sistema em `https://<host>:<port>/system/console/configMgr`).

### Propriedades adicionais da pasta {#additional-folder-properties}

As propriedades adicionais da pasta incluem permitir controle de dependências e incorporações, mas geralmente não são mais necessárias e seu uso não é incentivado:

* `dependencies`: esta é uma lista de outras categorias de bibliotecas de clientes das quais esta pasta de biblioteca depende. Por exemplo, dados dois nós `cq:ClientLibraryFolder` `F` e `G`, se um arquivo em `F` exigir que outro arquivo em `G` funcione corretamente, então pelo menos um dos `categories` de `G` deve estar entre os `dependencies` de `F`.
* `embed`: usado para incorporar o código de outras bibliotecas. Se o nó `F` incorporar os nós `G` e `H`, o HTML resultante será uma concatenação de conteúdo dos nós `G` e `H`.

### Vinculação a Dependências {#linking-to-dependencies}

Quando o código na pasta da biblioteca do cliente fizer referência a outras bibliotecas, identifique as outras bibliotecas como dependências. A marca `ui:includeClientLib` que faz referência à pasta da biblioteca do cliente faz com que o código HTML inclua um link para o arquivo de biblioteca gerado e as dependências.

As dependências devem ser outro `cq:ClientLibraryFolder`. Para identificar dependências, adicione uma propriedade ao nó `cq:ClientLibraryFolder` com os seguintes atributos:

* **Nome:** dependências
* **Tipo:** Cadeia de Caracteres[]
* **Valores:** o valor da propriedade categories do nó cq:ClientLibraryFolder do qual a pasta da biblioteca atual depende.

Por exemplo, o `/etc/clientlibs/myclientlibs/publicmain` tem uma dependência na biblioteca `cq.jquery`. A página que faz referência à biblioteca principal do cliente gera um HTML que inclui o seguinte código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Como incorporar código de outras bibliotecas {#embedding-code-from-other-libraries}

Você pode incorporar o código de uma biblioteca do cliente a outra biblioteca do cliente. No tempo de execução, os arquivos JS e CSS gerados da biblioteca de incorporação incluem o código da biblioteca incorporada.

A incorporação do código é útil para fornecer acesso às bibliotecas armazenadas em áreas seguras do repositório.

#### Pastas de bibliotecas de clientes específicas do aplicativo {#app-specific-client-library-folders}

É uma prática recomendada manter todos os arquivos relacionados a aplicativos em sua pasta de aplicativos abaixo de `/apps`. Também é uma prática recomendada negar acesso aos visitantes do site à pasta `/apps`. Para atender às duas práticas recomendadas, crie uma pasta de biblioteca do cliente abaixo da pasta `/etc` que incorpora a biblioteca do cliente que está abaixo de `/apps`.

Use a propriedade categories para identificar a pasta da biblioteca do cliente a ser incorporada. Para incorporar a biblioteca, adicione uma propriedade ao nó `cq:ClientLibraryFolder` incorporado, usando os seguintes atributos de propriedade:

* **Nome:** incorporado
* **Tipo:** Cadeia de Caracteres[]
* **Valor:** o valor da propriedade categories do nó `cq:ClientLibraryFolder` a ser incorporado.

#### Utilização de incorporação para minimizar solicitações {#using-embedding-to-minimize-requests}

Em alguns casos, você pode descobrir que o HTML final gerado para a página típica pela sua instância de publicação inclui um número relativamente grande de elementos `<script>`.

Nesses casos, pode ser útil combinar todo o código da biblioteca do cliente necessário no em um único arquivo para reduzir o número de solicitações de ida e volta no carregamento da página. Para fazer isso, você pode `embed` as bibliotecas necessárias na biblioteca do cliente específica do aplicativo usando a propriedade embed do nó `cq:ClientLibraryFolder`.

#### Caminhos em arquivos CSS {#paths-in-css-files}

Quando você incorpora arquivos CSS, o código CSS gerado usa caminhos para recursos relativos à biblioteca de incorporação. Por exemplo, a biblioteca `/etc/client/libraries/myclientlibs/publicmain` acessível publicamente incorpora a biblioteca cliente `/apps/myapp/clientlib`:

O arquivo `main.css` contém o seguinte estilo:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

O arquivo CSS gerado pelo nó `publicmain` contém o seguinte estilo, usando a URL da imagem original:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Consulte Arquivos incorporados na saída do HTML {#see-embedded-files}

Para rastrear a origem do código incorporado ou garantir que as bibliotecas de clientes incorporadas estejam produzindo os resultados esperados, você pode ver os nomes dos arquivos que estão sendo incorporados no tempo de execução. Para ver os nomes de arquivo, anexe o parâmetro `debugClientLibs=true` à URL da sua página da Web. A biblioteca gerada contém instruções `@import` em vez do código incorporado.

No exemplo da seção anterior [Incorporando Código de Outras Bibliotecas](#embedding-code-from-other-libraries), a pasta da biblioteca cliente `/etc/client/libraries/myclientlibs/publicmain` incorpora a pasta da biblioteca cliente `/apps/myapp/clientlib`. Anexar o parâmetro à página da Web produz o seguinte link no código-fonte da página da Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Abrir o arquivo `publicmain.css` revela o seguinte código:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Na caixa de endereço do navegador da Web, anexe o seguinte texto ao URL do HTML:
   * `?debugClientLibs=true`
1. Quando a página for carregada, exiba a origem da página.
1. Clique no link fornecido como href para o elemento do link para abrir o arquivo e exibir o código-fonte.

### Uso de pré-processadores {#using-preprocessors}

O AEM permite pré-processadores conectáveis e é fornecido com suporte ao [Compactador YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS e JavaScript e ao [Compilador de Fechamento do Google (GCC)](https://developers.google.com/closure/compiler/) para JavaScript com a interface do usuário definida como pré-processador padrão do AEM.

Os pré-processadores conectáveis permitem um uso flexível, incluindo:

* Definição de ScriptProcessors que podem processar origens de script
* Os processadores são configuráveis com opções
* Os processadores podem ser usados para minificação, mas também para casos não minificados
* A clientlib pode definir qual processador usar

>[!NOTE]
>
>Por padrão, o AEM usa o Compactador GCC para minificar o Javascript.

>[!CAUTION]
>
>Não coloque uma biblioteca minificada em uma biblioteca do cliente. Em vez disso, forneça a biblioteca bruta e, se a minificação for necessária, use as opções dos pré-processadores.

#### Uso {#usage}

Você pode optar por definir a configuração de pré-processadores por biblioteca do cliente ou em todo o sistema.

* Adicione as propriedades multivalor `cssProcessor` e `jsProcessor` no nó clientlibrary

Não há suporte para a definição da configuração padrão do sistema por meio do **HTML Library Manager**. Ela só será aplicada ao SDK local e não às execuções de pipeline de pilha completa.

#### Formato e exemplos {#format-and-examples}

##### Formato {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### Compactador YUI para Minificação CSS e GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Digitar script para pré-processar e, em seguida, GCC para minificar e ofuscar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### Opções adicionais de GCC {#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT_2018" as of release 21994, was previously "ECMASCRIPT5" )
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Para obter mais detalhes sobre as opções do GCC, consulte a [documentação do GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Definir Minificador Padrão do Sistema {#set-system-default-minifier}

Não há suporte para a configuração do minificador padrão do sistema no AEM as a Cloud Service.
