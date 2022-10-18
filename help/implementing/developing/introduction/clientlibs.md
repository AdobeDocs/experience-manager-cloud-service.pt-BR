---
title: Usar bibliotecas do lado do cliente no AEM as a Cloud Service
description: O AEM fornece Pastas de biblioteca do lado do cliente, que permitem armazenar o código do lado do cliente (clientlibs) no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser apresentada ao cliente
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: b93ec12616742910e35a3dac4224b690cd2c7116
workflow-type: tm+mt
source-wordcount: '2567'
ht-degree: 1%

---


# Usar bibliotecas do lado do cliente no AEM as a Cloud Service {#using-client-side-libraries}

As experiências digitais dependem muito do processamento no lado do cliente impulsionado por códigos complexos de JavaScript e CSS. AEM bibliotecas do lado do cliente (clientlibs) permitem organizar e armazenar centralmente essas bibliotecas do lado do cliente no repositório. Junto com o [processo de build front-end no arquétipo de projeto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) o gerenciamento do código front-end para o projeto de AEM se torna simples.

As vantagens de usar clientlibs no AEM incluem:

* O código do lado do cliente é armazenado no repositório como todos os outros códigos e conteúdos do aplicativo
* Clientlibs no AEM pode agregar todos os CSS e JS em um único arquivo
* Expor clientlibs por meio de um caminho acessível por meio do [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Permite a reescrita de caminhos para arquivos ou imagens referenciados

Clientlibs são a solução integrada para fornecer CSS e Javascript a partir da AEM.

>[!TIP]
>
>Os desenvolvedores de front-end que estão criando CSS e Javascript para projetos de AEM também devem se familiarizar com o [AEM Arquétipo de projeto e seu processo de build front-end automatizado.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## O que são bibliotecas do lado do cliente {#what-are-clientlibs}

Os sites exigem JavaScript e CSS, bem como recursos estáticos, como ícones e fontes da Web para serem processados no lado do cliente. Uma clientlib é AEM mecanismo para fazer referência (por categoria, se necessário) e servir esses recursos.

O AEM coleta o CSS e o Javascript do site em um único arquivo, em um local central, para garantir que apenas uma cópia de qualquer recurso esteja incluída na saída do HTML. Isso maximiza a eficiência do delivery e permite que esses recursos sejam mantidos centralmente no repositório por proxy, mantendo o acesso seguro.

## Desenvolvimento front-end para AEM as a Cloud Service {#fed-for-aemaacs}

Todos os JavaScript, CSS e outros ativos front-end devem ser mantidos no [Módulo ui.frontend do AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) A flexibilidade do arquétipo permite usar as ferramentas modernas da Web preferidas para criar e gerenciar esses recursos.

O arquétipo pode então compilar os recursos em um único arquivo CSS e JS, incorporando-os automaticamente em um `cq:clientLibraryFolder` no repositório.

## Estrutura de pastas da biblioteca do lado do cliente {#clientlib-folders}

Uma pasta de biblioteca do lado do cliente é um nó de repositório do tipo `cq:ClientLibraryFolder`. Sua definição em [Notação CND](https://jackrabbit.apache.org/node-type-notation.html) é

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` os nós podem ser colocados em qualquer lugar dentro do `/apps` subárvore do repositório.
* Use o `categories` propriedade do nó para identificar as categorias da biblioteca à qual pertence.

Cada `cq:ClientLibraryFolder` O é preenchido com um conjunto de arquivos JS e/ou CSS, juntamente com alguns arquivos de suporte (veja abaixo). Propriedades importantes da variável `cq:ClientLibraryFolder` são configuradas da seguinte maneira:

* `allowProxy`: Como todas as clientlibs devem ser armazenadas em `apps`, essa propriedade permite o acesso às bibliotecas do cliente por meio do servlet proxy. Consulte a seção [Localizando uma pasta da biblioteca do cliente e usando o servlet de bibliotecas do cliente proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) abaixo.
* `categories`: Identifica as categorias em que o conjunto de arquivos JS e/ou CSS dentro dessa `cq:ClientLibraryFolder` outono. O `categories` , com vários valores, permite que uma pasta de biblioteca faça parte de mais de uma categoria (veja abaixo como isso pode ser útil).

Se a pasta da biblioteca do cliente contiver um ou mais arquivos de origem que, no tempo de execução, serão mesclados em um único arquivo JS e/ou CSS. O nome do arquivo gerado é o nome do nó com a variável `.js` ou `.css` extensão do nome do arquivo. Por exemplo, o nó da biblioteca chamado `cq.jquery` resulta no arquivo gerado chamado `cq.jquery.js` ou `cq.jquery.css`.

As pastas da biblioteca de clientes contêm os seguintes itens:

* Os arquivos de origem JS e/ou CSS
* Recursos estáticos que oferecem suporte a estilos de CSS, como ícones, fontes da Web etc.
* One `js.txt` arquivo e/ou um `css.txt` arquivo que identifica os arquivos de origem a serem mesclados nos arquivos JS e/ou CSS gerados

![Arquitetura do clientlib](assets/clientlib-architecture.drawio.png)

## Criação de pastas de biblioteca do lado do cliente {#creating-clientlib-folders}

As bibliotecas de clientes devem estar localizadas em `/apps`. Isso é feito para isolar melhor o código do conteúdo e da configuração.

Para as bibliotecas de clientes em `/apps` para ser acessível, um servidor proxy é usado. As ACLs ainda são aplicadas na pasta da biblioteca do cliente, mas o servlet permite que o conteúdo seja lido via `/etc.clientlibs/` se a variável `allowProxy` está definida como `true`.

1. Abra o CRXDE Lite em um navegador da Web (`https://<host>:<port>/crx/de`).
1. Selecione o `/apps` e clique em **Criar > Criar nó**.
1. Insira um nome para a pasta da biblioteca e no **Tipo** selecionar lista `cq:ClientLibraryFolder`. Clique em **OK** e, em seguida, clique em **Salvar tudo**.
1. Para especificar a categoria ou categorias à qual a biblioteca pertence, selecione o `cq:ClientLibraryFolder` , adicione a seguinte propriedade e clique em **Salvar tudo**:
   * Nome: `categories`
   * Tipo: String
   * Valor: O nome da categoria
   * Várias: Selecionado
1. Para que as bibliotecas de clientes sejam acessíveis via proxy em `/etc.clientlibs`, selecione o `cq:ClientLibraryFolder` , adicione a seguinte propriedade e clique em **Salvar tudo**:
   * Nome: `allowProxy`
   * Tipo: booliano
   * Valor: `true`
1. Se precisar gerenciar recursos estáticos, crie uma subpasta chamada `resources` abaixo da pasta da biblioteca do cliente.
   * Se você armazenar recursos estáticos em qualquer lugar diferente da pasta `resources`, elas não podem ser referenciadas em uma instância de publicação.
1. Adicione arquivos de origem à pasta da biblioteca.
   * Normalmente, isso é feito pelo processo de build front-end do [AEM Arquétipo de projeto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Você pode organizar os arquivos de origem em subpastas, se desejar.
1. Selecione a pasta da biblioteca do cliente e clique em **Criar > Criar arquivo**.
1. Na caixa Nome do arquivo, digite um dos seguintes nomes de arquivo e clique em OK:
   * **`js.txt`:** Use esse nome de arquivo para gerar um arquivo JavaScript.
   * **`css.txt`:** Use esse nome de arquivo para gerar uma Folha de estilos em cascata.
1. Abra o arquivo e digite o seguinte texto para identificar a raiz do caminho dos arquivos de origem:
   * `#base=*[root]*`
   * Substituir `[root]` com o caminho para a pasta que contém os arquivos de origem, em relação ao arquivo TXT. Por exemplo, use o seguinte texto quando os arquivos de origem estiverem na mesma pasta do arquivo TXT:
      * `#base=.`
   * O código a seguir define a raiz como a pasta nomeada móvel abaixo da função `cq:ClientLibraryFolder` nó:
      * `#base=mobile`
1. Nas linhas abaixo `#base=[root]`, digite os caminhos dos arquivos de origem em relação à raiz. Coloque cada nome de arquivo em uma linha separada.
1. Clique em **Salvar tudo**.

## Servindo bibliotecas do lado do cliente {#serving-clientlibs}

Depois que a pasta da biblioteca do cliente estiver [configurado conforme necessário,](#creating-clientlib-folders) suas clientlibs podem ser solicitadas por proxy. Como exemplo:

* Você tem uma clientlib em `/apps/myproject/clientlibs/foo`
* Você tem uma imagem estática em `/apps/myprojects/clientlibs/foo/resources/icon.png`

O `allowProxy` permite solicitar:

* A clientlib via `/etc.clientlibs/myprojects/clientlibs/foo.js`
* A imagem estática via `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Carregamento de bibliotecas de clientes via HTL {#loading-via-htl}

Depois que as clientlibs forem armazenadas e gerenciadas com êxito na pasta da biblioteca do cliente, elas poderão ser acessadas via HTL.

As bibliotecas de clientes são carregadas por meio de um modelo auxiliar fornecido pelo AEM, que pode ser acessado por meio de `data-sly-use`. Os modelos de ajuda estão disponíveis neste arquivo, que pode ser chamado por meio de `data-sly-call`.

Cada modelo auxiliar espera uma opção `categories` para fazer referência às bibliotecas de clientes desejadas. Essa opção pode ser uma matriz de valores de cadeias de caracteres ou uma cadeia contendo uma lista de valores separados por vírgula.

[Consulte a documentação do HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) para obter mais detalhes sobre como carregar clientlibs via HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Bibliotecas de clientes no autor versus publicação {#clientlibs-author-publish}

A maioria das clientlibs será necessária na instância de publicação do AEM. Ou seja, a maioria dos objetivos das clientlibs é produzir a experiência do usuário final do conteúdo. Para clientlibs em instâncias de publicação, [ferramentas de criação front-end](#fed-for-aemaacs) pode ser usada e implantada via [as pastas da biblioteca do cliente, conforme descrito acima.](#creating-clientlib-folders)

No entanto, algumas vezes, as bibliotecas de clientes podem ser necessárias para personalizar a experiência de criação. Por exemplo, personalizar uma caixa de diálogo pode exigir a implantação de pequenos bits de CSS ou JS na instância de criação do AEM.

### Gerenciamento de bibliotecas de clientes no autor {#clientlibs-on-author}

Se precisar usar as bibliotecas de clientes no autor, poderá criar as bibliotecas de clientes em `/apps` usando os mesmos métodos de publicação, mas escreva-o diretamente em `/apps/.../clientlibs/foo` em vez de criar um projeto inteiro para gerenciá-lo.

Em seguida, você pode &quot;conectar&quot; ao JS de criação adicionando suas bibliotecas de clientes a uma categoria de biblioteca de clientes pronta para uso.

## Ferramentas de depuração {#debugging-tools}

O AEM fornece várias ferramentas para depurar e testar as pastas da biblioteca do cliente.

### Bibliotecas de clientes do Discover {#discover-client-libraries}

O `/libs/cq/granite/components/dumplibs/dumplibs` O componente gera uma página de informações sobre todas as pastas da biblioteca do cliente no sistema. O `/libs/granite/ui/content/dumplibs` tem o componente como um tipo de recurso. Para abrir a página, use o seguinte URL (alterando o host e a porta, conforme necessário):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

As informações incluem o caminho e o tipo da biblioteca (CSS ou JS) e os valores dos atributos da biblioteca, como categorias e dependências. As tabelas subsequentes na página mostram as bibliotecas em cada categoria e canal.

### Consulte Saída gerada {#see-generated-output}

O `dumplibs` componente inclui um seletor de teste que exibe o código-fonte gerado para `ui:includeClientLib` tags. A página inclui código para diferentes combinações de js, css e atributos temáticos.

1. Use um dos métodos a seguir para abrir a página Saída de teste:
   * No `dumplibs.html` clique no link na página **Clique aqui para testar a saída** texto.
   * Abra o seguinte URL no navegador da Web (use um host e uma porta diferentes, conforme necessário):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * A página padrão mostra a saída de tags sem valor para o atributo de categorias.
1. Para ver a saída de uma categoria, digite o valor da biblioteca do cliente `categories` propriedade e clique em **Enviar Consulta**.

## Recursos adicionais da pasta da biblioteca do cliente {#additional-features}

Há vários outros recursos compatíveis com as pastas da biblioteca do cliente no AEM. No entanto, estas não são exigidas AEM as a Cloud Service e, como tal, a sua utilização é desencorajada. Eles estão listados aqui para estarem completos.

>[!WARNING]
>
>Esses recursos adicionais das Pastas da biblioteca do cliente não são necessários AEM as a Cloud Service e, como tal, seu uso é desencorajado. Eles estão listados aqui para estarem completos.

### Adobe Granite HTML LIbrary Manager {#html-library-manager}

Configurações adicionais da biblioteca do cliente podem ser controladas por meio do **Gerenciador de biblioteca de HTML do Adobe Granite** painel do Console do sistema em `https://<host>:<port>/system/console/configMgr`).

### Propriedades Adicionais da Pasta {#additional-folder-properties}

As propriedades adicionais da pasta incluem permitir o controle de dependências e incorporações, mas geralmente não são mais necessárias e seu uso é desencorajado:

* `dependencies`: Esta é uma lista de outras categorias da biblioteca do cliente das quais essa pasta da biblioteca depende. Por exemplo, considerando dois `cq:ClientLibraryFolder` nodes `F` e `G`, se um arquivo em `F` requer outro arquivo em `G` para funcionar adequadamente, pelo menos um dos `categories` de `G` deve estar entre as `dependencies` de `F`.
* `embed`: Usado para incorporar o código de outras bibliotecas. nó If `F` nós incorporados `G` e `H`, o HTML resultante será uma concatenação de conteúdo de nós `G` e `H`.

### Vincular a dependências {#linking-to-dependencies}

Quando o código na pasta da biblioteca do cliente fizer referência a outras bibliotecas, identifique as outras bibliotecas como dependências. O `ui:includeClientLib` A tag que faz referência à pasta da biblioteca do cliente faz com que o código do HTML inclua um link para o arquivo da biblioteca gerado, bem como as dependências.

As dependências devem ser outras `cq:ClientLibraryFolder`. Para identificar dependências, adicione uma propriedade ao `cq:ClientLibraryFolder` nó com os seguintes atributos:

* **Nome:** dependências
* **Tipo:** String[]
* **Valores:** O valor da propriedade categories do nó cq:ClientLibraryFolder da qual a pasta de biblioteca atual depende.

Por exemplo, a variável `/etc/clientlibs/myclientlibs/publicmain` tem uma dependência do `cq.jquery` biblioteca. A página que faz referência à biblioteca principal do cliente gera HTML que inclui o seguinte código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Como Incorporar Código A Partir De Outras Bibliotecas {#embedding-code-from-other-libraries}

Você pode incorporar o código de uma biblioteca do cliente em outra biblioteca do cliente. No tempo de execução, os arquivos JS e CSS gerados da biblioteca de incorporação incluem o código da biblioteca incorporada.

A incorporação do código é útil para fornecer acesso a bibliotecas que são armazenadas em áreas seguras do repositório.

#### Pastas da biblioteca de clientes específicas do aplicativo {#app-specific-client-library-folders}

É uma prática recomendada manter todos os arquivos relacionados a aplicativos em sua pasta de aplicativos abaixo `/apps`. Também é uma prática recomendada negar o acesso dos visitantes do site à variável `/apps` pasta. Para atender às duas práticas recomendadas, crie uma pasta de biblioteca de clientes abaixo do `/etc` pasta que incorpora a biblioteca do cliente que está abaixo `/apps`.

Use a propriedade categories para identificar a pasta da biblioteca de clientes a ser incorporada. Para incorporar a biblioteca, adicione uma propriedade à incorporação `cq:ClientLibraryFolder` , usando os seguintes atributos de propriedade:

* **Nome:** embed
* **Tipo:** String[]
* **Valor:** O valor da propriedade categories da variável `cq:ClientLibraryFolder` nó a ser incorporado.

#### Usando a Incorporação para Minimizar Solicitações {#using-embedding-to-minimize-requests}

Em alguns casos, você pode descobrir que o HTML final gerado para uma página típica pela sua instância de publicação inclui um número relativamente grande de `<script>` elementos.

Nesses casos, pode ser útil combinar todo o código da biblioteca do cliente necessário em em um único arquivo para que o número de solicitações de frente e verso no carregamento da página seja reduzido. Para fazer isso, você pode `embed` as bibliotecas necessárias na biblioteca do cliente específica do aplicativo usando a propriedade embed do `cq:ClientLibraryFolder` nó .

#### Caminhos em arquivos CSS {#paths-in-css-files}

Quando você incorpora arquivos CSS, o código CSS gerado usa caminhos para recursos que são relativos à biblioteca de incorporação. Por exemplo, a biblioteca acessível publicamente `/etc/client/libraries/myclientlibs/publicmain` incorpora o `/apps/myapp/clientlib` biblioteca do cliente:

O `main.css` O arquivo contém o seguinte estilo:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

O arquivo CSS que `publicmain` O nó gerado contém o seguinte estilo, usando o URL da imagem original:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Consulte Arquivos incorporados na saída do HTML {#see-embedded-files}

Para rastrear a origem do código incorporado ou garantir que as bibliotecas de clientes incorporadas estejam produzindo os resultados esperados, você pode ver os nomes dos arquivos que estão sendo incorporados no tempo de execução. Para ver os nomes dos arquivos, anexe a variável `debugClientLibs=true` para o URL da página da Web. A biblioteca gerada contém `@import` instruções em vez do código incorporado.

No exemplo do anterior [Como Incorporar Código A Partir De Outras Bibliotecas](#embedding-code-from-other-libraries) seção , a variável `/etc/client/libraries/myclientlibs/publicmain` a pasta da biblioteca do cliente incorpora o `/apps/myapp/clientlib` pasta da biblioteca do cliente. Anexar o parâmetro à página da Web produz o seguinte link no código-fonte da página da Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Abrir o `publicmain.css` O arquivo revela o seguinte código:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Na caixa de endereço do navegador da Web, anexe o seguinte texto ao URL do seu HTML:
   * `?debugClientLibs=true`
1. Quando a página for carregada, visualize a fonte da página.
1. Clique no link fornecido como href para o elemento do link para abrir o arquivo e exibir o código-fonte.

### Uso de pré-processadores {#using-preprocessors}

AEM permite pré-processadores e entregas conectáveis com suporte para [Compressor YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS e JavaScript e [Compilador de Fechamento do Google (GCC)](https://developers.google.com/closure/compiler/) para JavaScript com YUI definido como AEM pré-processador padrão.

Os pré-processadores conectáveis permitem uma utilização flexível, incluindo:

* Definindo ScriptProcessors que podem processar fontes de script
* Os processadores são configuráveis com opções
* Os processadores podem ser usados para minificação, mas também para casos não minificados
* A clientlib pode definir qual processador usar

>[!NOTE]
>
>Por padrão, o AEM usa o Compactador YUI. Consulte a [Documentação do YUI Compressor GitHub](https://github.com/yui/yuicompressor/issues) para obter uma lista de problemas conhecidos. Alternar para o compressor GCC para clientlibs específicas pode resolver alguns problemas observados ao usar YUI.

>[!CAUTION]
>
>Não coloque uma biblioteca minificada em uma biblioteca do cliente. Em vez disso, forneça a biblioteca bruta e, se a minificação for necessária, use as opções dos pré-processadores.

#### Uso {#usage}

Você pode optar por configurar a configuração de pré-processadores por biblioteca do cliente ou todo o sistema.

* Adicionar as propriedades de vários valores `cssProcessor` e `jsProcessor` no nó clientlibrary
* Ou defina a configuração padrão do sistema por meio do **Gerenciador da biblioteca HTML** Configuração do OSGi

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

##### Tipo para pré-processar e, em seguida, GCC para minificar e ofuscar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

Para obter mais detalhes sobre as opções do GCC, consulte o [Documentação do GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Definir Minificador Padrão do Sistema {#set-system-default-minifier}

A IU é definida como minificador padrão no AEM. Para alterar para GCC, siga estas etapas.

1. Vá para o Apache Felix Config Manager em (`http://<host>:<portY/system/console/configMgr`)
1. Encontre e edite o **Gerenciador de biblioteca de HTML do Adobe Granite**.
1. Ative o **Minimizar** (se ainda não estiver habilitado).
1. Defina o valor **Configurações padrão do processador JS** para `min:gcc`.
   * As opções podem ser passadas se separadas por um ponto e vírgula, por exemplo, `min:gcc;obfuscate=true`.
1. Clique em **Salvar** para salvar as alterações.
