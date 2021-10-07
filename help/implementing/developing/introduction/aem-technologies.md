---
title: Fundamentos Técnicos AEM
description: Uma visão geral dos fundamentos técnicos do AEM incluindo como o AEM é estruturado e tecnologias fundamentais como JCR, Sling e OSGi.
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '2186'
ht-degree: 0%

---

# Fundamentos Técnicos AEM {#aem-technical-foundations}

AEM é uma plataforma robusta baseada em tecnologias comprovadas, escaláveis e flexíveis. Este documento fornece uma visão geral detalhada das várias partes que compõem o AEM e se destina a ser um apêndice técnico para um desenvolvedor de AEM de pilha completa. Não se destina a ser um guia de introdução. Se você nunca usou o AEM desenvolvimento, consulte a [Introdução ao desenvolvimento do AEM Sites - Tutorial WKND](develop-wknd-tutorial.md) como uma primeira etapa.

>[!TIP]
>
>Antes de mergulhar nas tecnologias principais do AEM, o Adobe recomenda concluir o [Tutorial de desenvolvimento do AEM Sites - WKND.](develop-wknd-tutorial.md)

## Fundamentos {#fundamentals}

Como um sistema moderno de gerenciamento de conteúdo, o AEM depende de tecnologias padrão da Web:

* O ciclo request-response (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

O repositório de conteúdo subjacente e as camadas de lógica de negócios são construídos com base em tecnologias Java:

* JCR
* Sling
* OSGi

## Repositório de conteúdo Java {#java-content-repository}

O padrão Java Content Repository (JCR), [JSR 283](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html), especifica uma maneira independente do fornecedor e de implementação para acessar o conteúdo de forma bidirecional em um nível granular em um repositório de conteúdo. A Adobe Research (Suíça) AG detém o chumbo da especificação.

O pacote [JCR API 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html), `javax.jcr.*` é usado para o acesso direto e a manipulação do conteúdo do repositório.

AEM é criado com base em um JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit ](https://jackrabbit.apache.org/oak/) Oakis é uma implementação de um repositório de conteúdo hierárquico escalável e de alto desempenho para uso como a base de sites modernos de classe mundial e outros aplicativos de conteúdo exigentes, em conformidade com o padrão JCR.

Jackrabbit Oak (também chamado simplesmente de Oak) é a implementação do padrão JCR no qual o AEM é construído.

## Processamento de solicitação Sling {#sling-request-processing}

O AEM é criado usando o [Sling](https://sling.apache.org/site/index.html), uma estrutura de aplicação web baseada em princípios REST que fornece fácil desenvolvimento de aplicativos orientados a conteúdo. O Sling usa um repositório JCR, como o Apache Jackrabbit Oak, como seu armazenamento de dados. O Sling tem contribuído para a Apache Software Foundation - mais informações podem ser encontradas no Apache.

### Introdução ao Sling {#introduction-to-sling}

Usando o Sling, o tipo de conteúdo a ser renderizado não é a primeira consideração de processamento. Em vez disso, a principal consideração é se o URL resolve um objeto de conteúdo para o qual um script pode ser encontrado para executar a renderização. Isso oferece excelente suporte para autores de conteúdo da Web criarem páginas que são facilmente personalizadas para suas necessidades.

As vantagens dessa flexibilidade são visíveis em aplicativos com uma grande variedade de elementos de conteúdo diferentes, ou quando você precisa de páginas que possam ser facilmente personalizadas. Especificamente, ao implementar um sistema de Gestão de Conteúdo da Web, como o AEM.

Consulte [Discover Sling em 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para obter as primeiras etapas para desenvolver com o Sling.

O diagrama a seguir explica a resolução do script Sling: ele mostra como obter da solicitação HTTP para o nó de conteúdo, do nó de conteúdo para o tipo de recurso, do tipo de recurso para o script e quais variáveis de script estão disponíveis.

![Como entender a resolução do script Apache Sling](assets/sling-cheatsheet-01.png)

O diagrama a seguir explica todos os parâmetros de solicitação ocultos, mas poderosos, que você pode usar ao lidar com o `SlingPostServlet`, o manipulador padrão para todas as solicitações do POST que oferece opções infinitas para criar, modificar, excluir, copiar e mover nós no repositório.

![Uso do SlingPostServlet](assets/sling-cheatsheet-02.png)

### O Sling é centrado no conteúdo {#sling-is-content-centric}

O Sling é *centrado no conteúdo*. Isso significa que o processamento está focado no conteúdo, já que cada solicitação (HTTP) é mapeada no conteúdo na forma de um recurso JCR (um nó de repositório):

* O primeiro target é o recurso (nó JCR) que contém o conteúdo
* Em segundo lugar, a representação, ou script, está localizada nas propriedades do recurso em combinação com determinadas partes da solicitação (por exemplo, seletores e/ou extensão)

### Sling RESTful {#restful-sling}

Devido a sua filosofia centrada no conteúdo, o Sling implementa um servidor orientado por REST e, portanto, apresenta um novo conceito em estruturas de aplicativos Web. As vantagens são:

* Muito RESTful, não apenas à superfície; recursos e representações são modelados corretamente no servidor
* Remove um ou mais modelos de dados
   * Outras estruturas de gerenciamento de conteúdo podem exigir estrutura de URL, objetos de negócios, esquema de banco de dados para acessar um recurso.
   * Com o Sling, isso é reduzido a: URL = recurso = estrutura JCR

### Decomposição de URL {#url-decomposition}

No Sling, o processamento é orientado pelo URL da solicitação do usuário. Isso define o conteúdo a ser exibido pelos scripts apropriados. Para fazer isso, as informações são extraídas do URL.

Se analisarmos o seguinte URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos dividi-lo em suas partes compósitas:

| protocolo | host |  | caminho do conteúdo | seletor(s) | extensão |  | sufixo |  | param(s) |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocolo**  - HTTPS
* **host**  - Domínio do site
* **caminho do conteúdo**  - Caminho que especifica o conteúdo a ser renderizado e é usado em combinação com a extensão; neste exemplo, eles traduzem para  `tools/spy.html`
* **seletor(s)**  - usado para métodos alternativos de renderização do conteúdo; neste exemplo, uma versão compatível com a impressora no formato A4
* **extensão**  - Formato do conteúdo; especifica também o script a ser usado para renderização
* **sufixo**  - Pode ser usado para especificar informações adicionais
* **parâmetro(s)**  - Quaisquer parâmetros necessários para o conteúdo dinâmico

#### Do URL para conteúdo e scripts {#from-url-to-content-and-scripts}

Usando os princípios de decomposição de URL:

* O mapeamento usa o caminho de conteúdo extraído da solicitação para localizar o recurso.
* Quando o recurso apropriado está localizado, o tipo de recurso sling é extraído e usado para localizar o script a ser usado para renderizar o conteúdo.

A figura a seguir ilustra o mecanismo usado, que será discutido com mais detalhes nas seções a seguir.

![Mecanismo de mapeamento de URL](assets/url-mapping.png)

Com o Sling, você especifica qual script renderiza uma determinada entidade (definindo a propriedade `sling:resourceType` no nó JCR). Esse mecanismo oferece mais liberdade do que uma em que o script acessa as entidades de dados (como uma instrução SQL em um script PHP faria), pois um recurso pode ter várias representações.

#### Mapeamento de solicitações para recursos {#mapping-requests-to-resources}

O pedido é dividido e as informações necessárias são extraídas. O repositório é pesquisado pelo recurso solicitado (nó de conteúdo):

* O primeiro Sling verifica se há um nó no local especificado na solicitação; por exemplo `../content/corporate/jobs/developer.html`
* Se nenhum nó for encontrado, a extensão será removida e a pesquisa será repetida; por exemplo `../content/corporate/jobs/developer`
* Se nenhum nó for encontrado, o Sling retornará o código http 404 (Não encontrado).

O Sling também permite que outras coisas além dos nós JCR sejam recursos, mas esse é um recurso avançado.

### Localização do script {#locating-the-script}

Quando o recurso apropriado (nó de conteúdo) está localizado, o **tipo de recurso sling** é extraído. Este é um caminho, que localiza o script a ser usado para renderizar o conteúdo.

O caminho especificado pelo `sling:resourceType` pode ser:

* Absoluto
* Em relação a um parâmetro de configuração

>[!TIP]
>
>Os caminhos relativos são recomendados pelo Adobe, pois aumentam a portabilidade.

Todos os scripts Sling são armazenados em subpastas de `/apps` (mutável, scripts de usuário) ou `/libs` (imutável, scripts de sistema), que serão pesquisadas nessa ordem.

Alguns outros pontos são:

* Quando o método (GET, POST) é necessário, ele será especificado em maiúsculas de acordo com a especificação HTTP, por exemplo `jobs.POST.esp`
* Vários mecanismos de script são compatíveis, mas os scripts comuns e recomendados são HTL e JavaScript.

A lista de mecanismos de script compatíveis com a instância específica de AEM é listada no Felix Management Console ( `http://<host>:<port>/system/console/slingscripting`).

Usando o exemplo anterior, se `sling:resourceType` for `hr/jobs` então para:

* Solicitações de GET/HEAD e URLs que terminam em `.html` (tipos de solicitação padrão, formato padrão)
   * O script será `/apps/hr/jobs/jobs.esp`; a última seção do `sling:resourceType` forma o nome do arquivo.
* Solicitações de POST (todos os tipos de solicitação exceto GET/HEAD, o nome do método deve estar em maiúsculas)
   * POST será usado no nome do script.
   * O script será `/apps/hr/jobs/jobs.POST.esp`.
* URLs em outros formatos, sem terminar com `.html`
   * Por exemplo `../content/corporate/jobs/developer.pdf`
   * O script será `/apps/hr/jobs/jobs.pdf.esp`; o sufixo é adicionado ao nome do script.
* URLs com seletores
   * Os seletores podem ser usados para exibir o mesmo conteúdo em um formato alternativo. Por exemplo, uma versão amigável para a impressora, um feed rss ou um resumo.
   * Se observarmos uma versão amigável da impressora, onde o seletor pode ser `print`; como em `../content/corporate/jobs/developer.print.html`
   * O script será `/apps/hr/jobs/jobs.print.esp`; o seletor é adicionado ao nome do script.
* Se nenhum `sling:resourceType` tiver sido definido, então:
   * O caminho de conteúdo será usado para procurar um script apropriado (se o caminho baseado `ResourceTypeProvider` estiver ativo).
   * Por exemplo, o script para `../content/corporate/jobs/developer.html` geraria uma pesquisa em `/apps/content/corporate/jobs/`.
   * O tipo de nó principal será usado.
* Se nenhum script for encontrado, o script padrão será usado.
   * A representação padrão é suportada atualmente como texto sem formatação (`.txt`), HTML (`.html`) e JSON (`.json`), e todos listarão as propriedades do nó (formatadas adequadamente). A representação padrão da extensão `.res`, ou solicitações sem uma extensão de solicitação, é spool do recurso (quando possível).
* Para tratamento de erros http (códigos 403 ou 404), o Sling procurará um script em:
   * O local `/apps/sling/servlet/errorhandler` para scripts personalizados
   * Ou o local do script padrão `/libs/sling/servlet/errorhandler/404.jsp`

Se vários scripts se aplicarem a uma determinada solicitação, o script com a melhor correspondência será selecionado. Quanto mais específico for o jogo, melhor será; em outras palavras, quanto mais seletor corresponder melhor, independentemente de qualquer extensão de solicitação ou correspondência de nome de método.

Por exemplo, considere uma solicitação para acessar o recurso

* `/content/corporate/jobs/developer.print.a4.html`

de tipo

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

Além dos tipos de recursos (definidos principalmente pela propriedade `sling:resourceType`), também há o super tipo de recurso. Isso geralmente é indicado pela propriedade `sling:resourceSuperType` . Esses supertipos também são considerados ao tentar encontrar um script. A vantagem dos supertipos de recursos é que eles podem formar uma hierarquia de recursos na qual o tipo de recurso padrão `sling/servlet/default` (usado pelos servlets padrão) é efetivamente a raiz.

O supertipo de recurso de um recurso pode ser definido de duas formas:

* pela propriedade `sling:resourceSuperType` do recurso.
* pela propriedade `sling:resourceSuperType` do nó para o qual `sling:resourceType` aponta.

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

A hierarquia do tipo de:

* `/x`
   * É `[ c, b, a, <default>]`
* Enquanto para `/y`
   * A hierarquia é `[ c, a, <default>]`

Isso ocorre porque `/y` tem a propriedade `sling:resourceSuperType`, enquanto `/x` não tem e, portanto, seu supertipo é retirado de seu tipo de recurso.

#### Scripts Sling não podem ser chamados diretamente {#sling-scripts-cannot-be-called-directly}

No Sling, os scripts não podem ser chamados diretamente, pois isso quebraria o conceito estrito de um servidor REST; você misturaria recursos e representações.

Se você chamar a representação (o script) diretamente, oculta o recurso dentro do script, de modo que a estrutura (Sling) não saiba mais sobre ela. Assim, você perde determinados recursos:

* Tratamento automático de métodos http diferentes do GET, incluindo:
   * POST, PUT, DELETE, que são manipulados com uma implementação padrão do sling
   * O script `POST.jsp` no seu local `sling:resourceType`
* Sua arquitetura de código não está mais tão limpa ou tão claramente estruturada quanto deveria ser; de importância primordial para o desenvolvimento em larga escala

### API Sling {#sling-api}

Isso usa o pacote da API do Sling, `org.apache.sling.*`, e as bibliotecas de tags.

### Referência a elementos existentes usando sling:include {#referencing-existing-elements-using-sling-include}

Uma consideração final é a necessidade de fazer referência a elementos existentes nos scripts.

Scripts mais complexos (agregação de scripts) podem precisar acessar vários recursos (por exemplo, navegação, barra lateral, rodapé, elementos de uma lista) e fazer isso incluindo o *resource*.

Para fazer isso, você pode usar o comando `sling:include("/<path>/<resource>")`. Isso incluirá efetivamente a definição do recurso referenciado.

## OSGi {#osgi}

O OSGi (Open Services Gateway Initiative) define uma arquitetura para o desenvolvimento e implantação de aplicativos e bibliotecas modulares (também conhecida como Dynamic Module System for Java). Os contêineres OSGi permitem dividir o aplicativo em módulos individuais (são arquivos jar com informações meta adicionais e chamados de pacotes na terminologia OSGi) e gerenciar as dependências cruzadas entre eles com:

* Serviços implementados no contêiner
* Um contrato entre o contêiner e seu aplicativo

Esses serviços e contratos fornecem uma arquitetura que permite que elementos individuais se descubram dinamicamente para colaboração.

Em seguida, uma estrutura OSGi oferece carregamento/descarregamento dinâmico, configuração e controle desses pacotes, sem a necessidade de reinicializações.

>[!NOTE]
>
>Informações completas sobre a tecnologia OSGi podem ser encontradas no [site OSGi](https://www.osgi.org).
>
>Em particular, a página de Educação Básica contém uma coleção de apresentações e tutoriais.

Essa arquitetura permite estender o Sling com módulos específicos de aplicativo. O Sling, e portanto AEM, usa a implementação [Apache Felix](https://felix.apache.org/) do OSGi. Ambos são coleções de pacotes OSGi executados em uma estrutura OSGi.

Isso permite executar as seguintes ações em qualquer um dos pacotes da instalação:

* Instalar
* Início
* Parar
* Atualizar
* Desinstalar
* Ver o status atual
* Acesse informações mais detalhadas (por exemplo, nome simbólico, versão, localização, etc.) sobre os pacotes específicos

Consulte [Configuração do OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obter mais informações.

## Estrutura no Repositório {#structure-within-the-repository}

A lista a seguir fornece uma visão geral da estrutura que será exibida no repositório.

* `/apps` - Aplicações relacionadas; O inclui definições de componentes específicas para o seu site. Os componentes desenvolvidos podem ser baseados nos componentes prontos para uso disponíveis em `/libs/core/wcm/components`.
* `/content` - Conteúdo criado para o seu site.
* `/etc`
* `/home` - Informações sobre usuários e grupos.
* `/libs` - Bibliotecas e definições que pertencem ao núcleo da AEM. As subpastas em `/libs` representam os recursos prontos para uso do AEM. O conteúdo em `/libs` não pode ser modificado. Os recursos específicos do seu site devem ser feitos em `/apps`.
* `/tmp` - Área de trabalho temporária.
* `/var` - Arquivos que mudam e são atualizados pelo sistema; como logs de auditoria, estatísticas, tratamento de eventos.

>[!CAUTION]
>
>As alterações nessa estrutura, ou nos arquivos dentro dela, devem ser feitas com cuidado. Certifique-se de compreender totalmente as implicações de quaisquer alterações feitas.
>
>Você não deve alterar nada no caminho `/libs`. Para configuração e outras alterações, copie o item de `/libs` para `/apps` e faça quaisquer alterações em `/apps`.
