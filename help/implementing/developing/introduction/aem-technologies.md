---
title: Fundamentos técnicos AEM
description: Uma visão geral dos fundamentos técnicos da AEM, incluindo como a AEM é estruturada e tecnologias fundamentais como JCR, Sling e OSGi.
translation-type: tm+mt
source-git-commit: 750fded1564de2b11f6c104cc70befc4453405b4
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# Fundamentos técnicos AEM {#aem-technical-foundations}

AEM é uma plataforma robusta baseada em tecnologias comprovadas, escaláveis e flexíveis. Este documento fornece uma visão geral detalhada das várias partes que compõem o AEM e é projetado como um apêndice técnico para um desenvolvedor AEM pilha completa. Não é destinado a um guia de introdução. Se você for novo em AEM desenvolvimento, consulte o Tutorial [](develop-wknd-tutorial.md) Introdução ao desenvolvimento do AEM Sites - WKND como uma primeira etapa.

>[!TIP]
>
>Antes de mergulhar nas tecnologias principais da AEM, a Adobe recomenda concluir o Tutorial [Introdução ao desenvolvimento do AEM Sites - WKND.](develop-wknd-tutorial.md)

## Fundamentos {#fundamentals}

Como um sistema de gestões de conteúdo moderno, AEM depende de tecnologias da Web padrão:

* O ciclo request-response (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

O repositório de conteúdo subjacente e as camadas de lógica comercial são criados em torno das tecnologias Java:

* JCR
* Sling
* OSGi

## Repositório de conteúdo Java {#java-content-repository}

O padrão Java Content Repository (JCR), [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html), especifica uma maneira independente do fornecedor e de implementação para acessar o conteúdo de forma bidirecional em um nível granular em um repositório de conteúdo. O chumbo da especificação é detido pela Adobe Research (Suíça) AG.

O pacote [JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html) `javax.jcr.*` é usado para acesso direto e manipulação do conteúdo do repositório.

AEM é construído sobre um JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/) é uma implementação de um repositório de conteúdo hierárquico escalável e de alto desempenho para uso como base de sites modernos de classe mundial e outras aplicações exigentes de conteúdo, em conformidade com o padrão JCR.

Jackrabbit Oak (também chamado simplesmente de Oak), é a implementação do padrão JCR sobre o qual AEM é construído.

## Processamento de solicitação Sling {#sling-request-processing}

A AEM é criada com o [Sling](https://sling.apache.org/site/index.html), uma estrutura de Aplicação web baseada em princípios REST que oferece fácil desenvolvimento de aplicativos orientados a conteúdo. A Sling usa um repositório JCR, como o Apache Jackrabbit Oak, como armazenamento de dados. A Sling contribuiu para a Apache Software Foundation - mais informações estão disponíveis no Apache.

### Introdução ao Sling {#introduction-to-sling}

Usando o Sling, o tipo de conteúdo a ser renderizado não é a primeira consideração de processamento. Em vez disso, a principal consideração é se o URL é resolvido para um objeto de conteúdo para o qual um script pode ser encontrado para executar a renderização. Isso oferece excelente suporte para autores de conteúdo da Web para criar páginas que são facilmente personalizadas para suas necessidades.

As vantagens dessa flexibilidade são evidentes em aplicativos com uma grande variedade de elementos de conteúdo diferentes, ou quando você precisa de páginas que possam ser facilmente personalizadas. Em particular, ao implementar um sistema de Gestão de conteúdo da Web como o AEM.

Consulte [Discover Sling em 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para obter os primeiros passos para o desenvolvimento com o Sling.

O diagrama a seguir explica a resolução do script Sling: ele mostra como obter da solicitação HTTP para o nó de conteúdo, do nó de conteúdo para o tipo de recurso, do tipo de recurso para o script e quais variáveis de script estão disponíveis.

![Noções básicas sobre a resolução de scripts do Apache Sling](assets/sling-cheatsheet-01.png)

O diagrama a seguir explica todos os parâmetros de solicitação ocultos, mas poderosos, que você pode usar ao lidar com o manipulador `SlingPostServlet`, o manipulador padrão para todas as solicitações de POST, que oferece opções intermináveis para criar, modificar, excluir, copiar e mover nós no repositório.

![Uso do SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling é centrado no conteúdo {#sling-is-content-centric}

O Sling é centrado no *conteúdo*. Isso significa que o processamento está focado no conteúdo, já que cada solicitação (HTTP) está mapeada para o conteúdo na forma de um recurso JCR (um nó de repositório):

* O primeiro público alvo é o recurso (nó JCR) que contém o conteúdo
* Em segundo lugar, a representação, ou script, está localizada nas propriedades do recurso em combinação com determinadas partes da solicitação (por exemplo, seletores e/ou extensão)

### Sling RESTful {#restful-sling}

Devido à sua filosofia centrada no conteúdo, o Sling implementa um servidor orientado por REST e, portanto, apresenta um novo conceito em estruturas de aplicativos da Web. As vantagens são:

* Muito RESTful, não apenas na superfície. recursos e representações são modelados corretamente dentro do servidor
* Remove um ou mais modelos de dados
   * Outras estruturas de gestão de conteúdo podem exigir estrutura de URL, objetos de negócios, schema de banco de dados para acessar um recurso.
   * Usando o Sling, isso é reduzido a: URL = recurso = estrutura JCR

### Decomposição de URL {#url-decomposition}

No Sling, o processamento é conduzido pelo URL da solicitação do usuário. Isso define o conteúdo a ser exibido pelos scripts apropriados. Para fazer isso, as informações são extraídas do URL.

Se analisarmos o seguinte URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos dividi-lo em suas partes compostas:

| protocolo | host |  | caminho do conteúdo | seletor(s) | extensão |  | sufixo |  | param(s) |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocolo** - HTTPS
* **host** - Domínio do site
* **caminho** do conteúdo - Caminho que especifica o conteúdo a ser renderizado e é usado em combinação com a extensão; neste exemplo, eles traduzem para `tools/spy.html`
* **seletor(s)** - usado para métodos alternativos de renderização do conteúdo; neste exemplo, uma versão compatível com a impressora em formato A4
* **extensão** - Formato do conteúdo; especifica também o script a ser usado para renderização
* **sufixo** - Pode ser usado para especificar informações adicionais
* **param(s)** - Quaisquer parâmetros necessários para o conteúdo dinâmico

#### Do URL ao conteúdo e scripts {#from-url-to-content-and-scripts}

Usando os princípios de decomposição de URL:

* O mapeamento usa o caminho de conteúdo extraído da solicitação para localizar o recurso.
* Quando o recurso apropriado está localizado, o tipo de recurso sling é extraído e usado para localizar o script a ser usado para renderizar o conteúdo.

A figura a seguir ilustra o mecanismo utilizado, que será discutido mais pormenorizadamente nas seções a seguir.

![Mecanismo de mapeamento de URL](assets/url-mapping.png)

Com Sling, você especifica qual script renderiza uma determinada entidade (definindo a `sling:resourceType` propriedade no nó JCR). Esse mecanismo oferta mais liberdade do que uma em que o script acessa as entidades de dados (como uma instrução SQL em um script PHP faria), pois um recurso pode ter várias execuções.

#### Mapeamento de solicitações para recursos {#mapping-requests-to-resources}

O pedido é discriminado e as informações necessárias são extraídas. O repositório é pesquisado pelo recurso solicitado (nó de conteúdo):

* O First Sling verifica se existe um nó no local especificado na solicitação; por exemplo, `../content/corporate/jobs/developer.html`
* Se nenhum nó for encontrado, a extensão será ignorada e a pesquisa será repetida; por exemplo, `../content/corporate/jobs/developer`
* Se nenhum nó for encontrado, o Sling retornará o código http 404 (Não encontrado).

O Sling também permite que outros nós que não o JCR sejam recursos, mas esse é um recurso avançado.

### Localização do script {#locating-the-script}

Quando o recurso apropriado (nó de conteúdo) está localizado, o tipo **de recurso** sling é extraído. Esse é um caminho, que localiza o script a ser usado para renderizar o conteúdo.

O caminho especificado pelo `sling:resourceType` pode ser:

* Absoluto
* Relativo a um parâmetro de configuração

>[!TIP]
>
>Os caminhos relativos são recomendados pelo Adobe, pois aumentam a portabilidade.

Todos os scripts Sling são armazenados em subpastas de `/apps` (mutable, user scripts) ou `/libs` (imutável, system scripts), que serão pesquisadas nessa ordem.

Alguns outros pontos são:

* Quando o método (GET, POST) for necessário, ele será especificado em maiúsculas de acordo com a especificação HTTP, por exemplo `jobs.POST.esp`
* Há suporte para vários mecanismos de script, mas os scripts comuns e recomendados são HTL e JavaScript.

A lista de mecanismos de script suportados pela instância específica do AEM está listada no Console de Gerenciamento do Felix ( `http://<host>:<port>/system/console/slingscripting`).

Usando o exemplo anterior, se o `sling:resourceType` for `hr/jobs` :

* Solicitações de GET e URLs que terminam em `.html` (tipos de solicitação padrão, formato padrão)
   * O script será `/apps/hr/jobs/jobs.esp`; a última seção dos `sling:resourceType` formulários com o nome do arquivo.
* solicitações de POST (todos os tipos de solicitação exceto GET/HEAD, o nome do método deve estar em maiúsculas)
   * POST será usado no nome do script.
   * O script será `/apps/hr/jobs/jobs.POST.esp`.
* URLs em outros formatos, sem terminar com `.html`
   * Por exemplo `../content/corporate/jobs/developer.pdf`
   * O script será `/apps/hr/jobs/jobs.pdf.esp`; o sufixo é adicionado ao nome do script.
* URLs com seletores
   * Os seletores podem ser usados para exibir o mesmo conteúdo em um formato alternativo. Por exemplo, uma versão compatível com a impressora, um feed rss ou um resumo.
   * Se olharmos para uma versão fácil para a impressora onde o seletor poderia estar `print`; como em `../content/corporate/jobs/developer.print.html`
   * O script será `/apps/hr/jobs/jobs.print.esp`; o seletor é adicionado ao nome do script.
* Se nenhum `sling:resourceType` foi definido, então:
   * O caminho do conteúdo será usado para procurar um script apropriado (se o caminho baseado `ResourceTypeProvider` estiver ativo).
   * Por exemplo, o script para `../content/corporate/jobs/developer.html` geraria uma pesquisa em `/apps/content/corporate/jobs/`.
   * O tipo de nó primário será usado.
* Se nenhum script for encontrado, o script padrão será usado.
   * A renderização padrão é atualmente compatível com texto sem formatação (`.txt`), HTML (`.html`) e JSON (`.json`), todos os quais serão listas nas propriedades do nó (devidamente formatados). A renderização padrão para a extensão `.res`ou solicitações sem uma extensão de solicitação é para spool do recurso (quando possível).
* Para a manipulação de erros http (códigos 403 ou 404), o Sling procurará um script em:
   * O local `/apps/sling/servlet/errorhandler` para scripts personalizados
   * Ou a localização do script padrão `/libs/sling/servlet/errorhandler/404.jsp`

Se vários scripts se aplicarem a uma determinada solicitação, o script com a melhor correspondência será selecionado. Quanto mais específico for o jogo, melhor será; em outras palavras, quanto mais o seletor corresponder melhor, independentemente de qualquer extensão de solicitação ou nome de método correspondente.

Por exemplo, considere uma solicitação para acessar o recurso

* `/content/corporate/jobs/developer.print.a4.html`

do tipo

* `sling:resourceType="hr/jobs"`

Supondo que tenhamos a seguinte lista de scripts no local correto:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Em seguida, a ordem de preferência seria (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Além dos tipos de recursos (definidos primariamente pela `sling:resourceType` propriedade), há também o supertipo de recurso. Isso é geralmente indicado pela `sling:resourceSuperType` propriedade. Esses supertipos também são considerados ao tentar encontrar um script. A vantagem dos supertipos de recursos é que eles podem formar uma hierarquia de recursos na qual o tipo de recurso padrão `sling/servlet/default` (usado pelos servlets padrão) é efetivamente a raiz.

O supertipo de recurso de um recurso pode ser definido de duas formas:

* pela `sling:resourceSuperType` propriedade do recurso.
* pela `sling:resourceSuperType` propriedade do nó para o qual os `sling:resourceType` pontos são posicionados.

Por exemplo:

* `/`
   * `a`
   * `b`
      * `sling:resourceSuperType = a`
   * `c`
      * `sling:resourceSuperType = b`
   * `x`
      * `sling:resourceType = c`
   * `y`
      * `sling:resourceType = c`
      * `sling:resourceSuperType = a`

A hierarquia de tipos de:

* `/x`
   * Is `[ c, b, a, <default>]`
* While for `/y`
   * A hierarquia é `[ c, a, <default>]`

Isso ocorre porque `/y` tem a `sling:resourceSuperType` propriedade, enquanto `/x` não, e portanto seu supertipo é retirado de seu tipo de recurso.

#### Scripts Sling não podem ser chamados diretamente {#sling-scripts-cannot-be-called-directly}

No Sling, os scripts não podem ser chamados diretamente, pois isso quebraria o conceito restrito de servidor REST. você misturaria recursos e representações.

Se você chamar a representação (o script) diretamente, oculta o recurso dentro do script, de modo que a estrutura (Sling) não saiba mais sobre ele. Assim, você perde determinados recursos:

* Manuseio automático de métodos http diferentes de GET, incluindo:
   * POST, PUT, DELETE que são manipulados com uma implementação padrão de sling
   * O `POST.jsp` script no seu `sling:resourceType` local
* Sua arquitetura de código não é mais tão limpa e tão claramente estruturada quanto deveria ser; de importância primordial para o desenvolvimento em larga escala

### API Sling {#sling-api}

Isso usa o pacote Sling API `org.apache.sling.*`e as bibliotecas de tags.

### Referência a elementos existentes usando sling:include {#referencing-existing-elements-using-sling-include}

Uma consideração final é a necessidade de fazer referência aos elementos existentes nos scripts.

Scripts mais complexos (como a agregação de scripts) podem precisar acessar vários recursos (por exemplo, navegação, barra lateral, rodapé, elementos de uma lista) e fazer isso incluindo o *recurso*.

Para fazer isso, use o `sling:include("/<path>/<resource>")` comando. Isso incluirá efetivamente a definição do recurso referenciado.

## OSGi {#osgi}

O OSGi (Open Services Gateway Initiative) define uma arquitetura para desenvolver e implantar aplicativos e bibliotecas modulares (também conhecida como Dynamic Module System for Java). Os container OSGi permitem que você divida seu aplicativo em módulos individuais (são arquivos jar com informações meta adicionais e chamados de pacotes na terminologia OSGi) e gerencie as dependências cruzadas entre eles com:

* Serviços implementados no container
* Um contrato entre o container e o aplicativo

Esses serviços e contratos fornecem uma arquitetura que permite que elementos individuais se descubram dinamicamente para colaboração.

Em seguida, uma estrutura OSGi oferta o carregamento/descarregamento dinâmico, a configuração e o controle desses pacotes - sem a necessidade de reinicializações.

>[!NOTE]
>
>Para informações completas sobre a tecnologia OSGi, consultar o sítio web [do](https://www.osgi.org)OSGi.
>
>Em particular, a página de Educação Básica contém uma coleção de apresentações e tutoriais.

Essa arquitetura permite estender o Sling com módulos específicos do aplicativo. A Sling, e portanto AEM, utiliza a implementação do [Apache Felix](https://felix.apache.org/) do OSGi. Ambos são coleções de pacotes OSGi executados em uma estrutura OSGi.

Isso permite executar as seguintes ações em qualquer um dos pacotes da sua instalação:

* Instalar
* Início
* Parar
* Atualizar
* Desinstalar
* Ver o estado atual
* Acesse informações mais detalhadas (por exemplo, nome simbólico, versão, localização etc.) sobre os pacotes específicos

Consulte [Configuração do OSGi para AEM como Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obter mais informações.

## Estrutura no repositório {#structure-within-the-repository}

A lista a seguir fornece uma visão geral da estrutura que você verá no repositório.

* `/apps` - Aplicações relacionadas; inclui definições de componentes específicas ao seu site. Os componentes que você desenvolve podem ser baseados nos componentes prontos disponíveis em `/libs/core/wcm/components`.
* `/content` - Conteúdo criado para seu site.
* `/etc`
* `/home` - Informações do usuário e do grupo.
* `/libs` - Bibliotecas e definições que pertencem ao núcleo da AEM. As subpastas em `/libs` representam os recursos predefinidos AEM. O conteúdo em não `/libs` pode ser modificado. Os recursos específicos do seu site devem ser criados em `/apps`.
* `/tmp` - Área de trabalho temporária.
* `/var` - Arquivos que mudam e são atualizados pelo sistema; como registros de auditoria, estatísticas, tratamento de eventos.

>[!CAUTION]
>
>As alterações nesta estrutura, ou nos arquivos nela contidos, devem ser feitas com cuidado. Certifique-se de compreender totalmente as implicações de quaisquer alterações feitas.
>
>Você não deve alterar nada no `/libs` caminho. Para a configuração e outras alterações, copie o item de `/libs` para `/apps` e faça quaisquer alterações dentro `/apps`.
