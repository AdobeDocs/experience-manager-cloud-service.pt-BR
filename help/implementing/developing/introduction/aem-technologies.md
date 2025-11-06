---
title: Fundamentos técnicos do AEM
description: Uma visão geral dos fundamentos técnicos do AEM, incluindo como o AEM é estruturado e as tecnologias fundamentais, como JCR, Sling e OSGi.
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2129'
ht-degree: 1%

---

# Fundamentos técnicos do AEM {#aem-technical-foundations}

O AEM é uma plataforma robusta criada com tecnologias comprovadas, escaláveis e flexíveis. Este documento fornece uma visão geral detalhada das várias partes que compõem o AEM e serve como um apêndice técnico para um desenvolvedor de AEM de pilha completa. Não se destina a ser um guia de introdução. Se você é novo no desenvolvimento do AEM, consulte [Introdução ao desenvolvimento do AEM Sites - Tutorial WKND](develop-wknd-tutorial.md) como primeira etapa.

>[!TIP]
>
>Antes de mergulhar nas tecnologias principais do AEM, a Adobe recomenda concluir a [Introdução ao desenvolvimento do AEM Sites - Tutorial WKND](develop-wknd-tutorial.md).

## Fundamentos {#fundamentals}

Como um sistema moderno de gerenciamento de conteúdo, o AEM depende de tecnologias padrão da Web:

* O ciclo solicitação-resposta (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

O repositório de conteúdo subjacente e as camadas de lógica de negócios são criados com base em tecnologias Java™:

* JCR
* Sling
* OSGi

## Repositório de conteúdo Java™ {#java-content-repository}

O padrão Java™ Content Repository (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html), especifica uma maneira independente de fornecedor e de implementação para acessar conteúdo bidirecionalmente em nível granular em um repositório de conteúdo. O lead da especificação é da Adobe Research (Switzerland) AG.

O pacote [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html), `javax.jcr.*` é usado para o acesso direto e manipulação de conteúdo do repositório.

O AEM é criado com base em um JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

O [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/) é uma implementação de um repositório de conteúdo hierárquico escalável e de alto desempenho para uso como a base de sites de classe mundial modernos e outros aplicativos de conteúdo exigentes, em conformidade com o padrão JCR.

Jackrabbit Oak (também conhecido simplesmente como Oak) é a implementação do padrão JCR no qual o AEM é construído.

## Processamento de solicitação do Sling {#sling-request-processing}

O AEM foi criado usando o [Sling](https://sling.apache.org/index.html), uma estrutura de aplicativo Web baseada em princípios REST que fornece desenvolvimento fácil de aplicativos orientados a conteúdo. O Sling usa um repositório JCR, como o Apache Jackrabbit Oak, como armazenamento de dados. O Sling contribuiu para a Apache Software Foundation - mais informações podem ser encontradas na Apache.

### Introdução ao Sling {#introduction-to-sling}

Usando o Sling, o tipo de conteúdo a ser renderizado não é a primeira consideração de processamento. Em vez disso, a principal consideração é se o URL resolve um objeto de conteúdo para o qual um script pode ser encontrado para executar a renderização. Esse processo oferece excelente suporte para que os autores de conteúdo da Web criem páginas que são facilmente personalizadas de acordo com suas necessidades.

As vantagens dessa flexibilidade são evidentes em aplicativos com uma grande variedade de elementos de conteúdo diferentes, ou quando você precisa de páginas que possam ser facilmente personalizadas. Especificamente, ao implementar um sistema de Gerenciamento de conteúdo da Web, como o AEM.

Consulte [Descubra o Sling em 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para conhecer as primeiras etapas de desenvolvimento com o Sling.

O diagrama a seguir explica a resolução do script Sling. Ele mostra como ir da solicitação HTTP ao nó de conteúdo, do nó de conteúdo ao tipo de recurso, do tipo de recurso ao script e quais variáveis de script estão disponíveis.

![Entendendo a resolução do script Apache Sling](assets/sling-cheatsheet-01.png)

O diagrama a seguir explica os parâmetros de solicitação ocultos, mas poderosos, que você pode usar com o `SlingPostServlet`, o manipulador padrão para todas as solicitações POST. O manipulador fornece opções infinitas para criar, modificar, excluir, copiar e mover nós no repositório.

![Usando o SlingPostServlet](assets/sling-cheatsheet-02.png)

### O Sling é centrado no conteúdo {#sling-is-content-centric}

O Sling é *centrado no conteúdo*. Isso significa que o processamento se concentra no conteúdo à medida que cada solicitação (HTTP) é mapeada no conteúdo na forma de um recurso JCR (um nó de repositório):

* O primeiro destino é o recurso (nó JCR) que contém o conteúdo
* Segundo, a representação ou script está localizada nas propriedades do recurso com determinadas partes da solicitação (por exemplo, seletores e/ou a extensão)

### Sling RESTful {#restful-sling}

Devido à sua filosofia centrada no conteúdo, o Sling implementa um servidor orientado para REST e, portanto, apresenta um novo conceito em estruturas de aplicações Web. As vantagens são:

* RESTful, não apenas na superfície; os recursos e as representações são modelados corretamente dentro do servidor
* Remove um ou mais modelos de dados
   * Outras estruturas de gerenciamento de conteúdo podem exigir estrutura de URL, objetos de negócios e esquema de banco de dados para acessar um recurso.
   * O uso do Sling o reduz a: URL = resource = JCR structure

### Decomposição de URL {#url-decomposition}

No Sling, o processamento é orientado pelo URL da solicitação do usuário. Ele define o conteúdo a ser exibido pelos scripts apropriados e as informações são extraídas do URL.

Análise do seguinte URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Você pode separá-la em suas partes compostas:

| protocolo | host |  | caminho do conteúdo | seletores | extensão |  | sufixo |  | params |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocolo** - HTTPS
* **host** - Domínio do site
* **caminho do conteúdo** - Caminho que especifica o conteúdo a ser renderizado e é usado com a extensão. Neste exemplo, ele significa `tools/spy.html`
* **seletores** - Usados para métodos alternativos de renderização do conteúdo; neste exemplo, uma versão compatível com a impressora no formato A4
* **extensão** - Formato de conteúdo; também especifica o script a ser usado para renderização
* **sufixo** - Pode ser usado para especificar informações adicionais
* **parâmetros** - Quaisquer parâmetros necessários para o conteúdo dinâmico

#### Do URL ao conteúdo e scripts {#from-url-to-content-and-scripts}

Usando os princípios de decomposição de URL:

* O mapeamento usa o caminho de conteúdo extraído da solicitação para localizar o recurso.
* Quando o recurso apropriado é localizado, o tipo de recurso do sling é extraído e usado para localizar o script a ser usado para renderizar o conteúdo.

A figura a seguir ilustra o mecanismo usado, que é discutido com mais detalhes nas seções a seguir.

![mecanismo de mapeamento de URL](assets/url-mapping.png)

Com o Sling, você especifica qual script renderiza uma determinada entidade (definindo a propriedade `sling:resourceType` no nó JCR). Este mecanismo oferece mais liberdade do que um em que o script acessa as entidades de dados (como uma instrução SQL em um script PHP faria) como um recurso pode ter várias representações.

#### Mapeamento de solicitações para recursos {#mapping-requests-to-resources}

O pedido é detalhado e as informações necessárias são extraídas. O repositório é pesquisado para o recurso solicitado (nó de conteúdo):

* O First Sling verifica se um nó existe no local especificado na solicitação; por exemplo, `../content/corporate/jobs/developer.html`
* Se nenhum nó for encontrado, a extensão será descartada e a pesquisa repetida; por exemplo, `../content/corporate/jobs/developer`
* Se nenhum nó for encontrado, o Sling retornará o código http 404 (Não encontrado).

O Sling também permite que outros itens além dos nós JCR sejam recursos, mas essa funcionalidade é um recurso avançado.

### Localização do script {#locating-the-script}

Quando o recurso apropriado (nó de conteúdo) é localizado, o **tipo de recurso de sling** é extraído. Esse caminho localiza o script a ser usado para renderizar o conteúdo.

O caminho especificado por `sling:resourceType` pode ser:

* Absoluto
* Relativo a um parâmetro de configuração

>[!TIP]
>
>Os caminhos relativos são recomendados pela Adobe, pois aumentam a portabilidade.

Todos os scripts Sling são armazenados em subpastas de `/apps` (mutável, scripts de usuário) ou `/libs` (imutável, scripts de sistema), que são pesquisadas nesta ordem.

Alguns outros pontos a observar são:

* Quando o método (GET, POST) é necessário, ele é especificado em maiúsculas, de acordo com a especificação HTTP, por exemplo, `jobs.POST.esp`
* Vários mecanismos de script são compatíveis, mas os scripts comuns recomendados são HTL e JavaScript.

A lista de mecanismos de script suportados pela instância fornecida do AEM está listada no Felix Management Console ( `http://<host>:<port>/system/console/slingscripting`).

Usando o exemplo anterior, se `sling:resourceType` for `hr/jobs`, para:

* Solicitações GET/HEAD e URLs terminando em `.html` (tipos de solicitação padrão, formato padrão)
   * O script é `/apps/hr/jobs/jobs.esp`; a última seção de `sling:resourceType` forma o nome do arquivo.
* Solicitações POST (todos os tipos de solicitações, exceto GET/HEAD; o nome do método deve estar em maiúsculas)
   * POST é usado no nome do script.
   * O script é `/apps/hr/jobs/jobs.POST.esp`.
* URLs em outros formatos, não terminando com `.html`
   * Por exemplo, `../content/corporate/jobs/developer.pdf`
   * O script é `/apps/hr/jobs/jobs.pdf.esp`; o sufixo é adicionado ao nome do script.
* URLs com seletores
   * Seletores podem ser usados para exibir o mesmo conteúdo em um formato alternativo. Por exemplo, uma versão para impressão, um feed RSS ou um resumo.
   * Se você observar uma versão para impressão em que o seletor poderia ser `print`; como em `../content/corporate/jobs/developer.print.html`
   * O script é `/apps/hr/jobs/jobs.print.esp`; o seletor é adicionado ao nome do script.
* Se não, `sling:resourceType` é definido então:
   * O caminho de conteúdo é usado para procurar um script apropriado (se o `ResourceTypeProvider` baseado em caminho estiver ativo).
   * Por exemplo, o script para `../content/corporate/jobs/developer.html` geraria uma pesquisa em `/apps/content/corporate/jobs/`.
   * O tipo de nó primário é usado.
* Se nenhum script for encontrado, o script padrão será usado.
   * A representação padrão tem suporte como texto sem formatação (`.txt`), HTML (`.html`) e JSON (`.json`), e todas listam as propriedades do nó (adequadamente formatadas). A representação padrão da extensão `.res`, ou solicitações sem uma extensão de solicitação, é fazer spool do recurso (quando possível).
* Para o tratamento de erros http (códigos 403 ou 404), o Sling procura um script em:
   * O local `/apps/sling/servlet/errorhandler` para scripts personalizados
   * Ou o local do script padrão `/libs/sling/servlet/errorhandler/404.jsp`

Se vários scripts se aplicarem a uma determinada solicitação, o script com a melhor correspondência será selecionado. Quanto mais específica for uma correspondência, melhor ela será; em outras palavras, quanto mais o seletor corresponder melhor, independentemente de qualquer correspondência de extensão de solicitação ou nome de método.

Por exemplo, considere uma solicitação para acessar o recurso

* `/content/corporate/jobs/developer.print.a4.html`

Do tipo

* `sling:resourceType="hr/jobs"`

Supondo que você tenha a seguinte lista de scripts no local correto:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Em seguida, a ordem de preferência seria (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Além dos tipos de recursos (definidos principalmente pela propriedade `sling:resourceType`), também há o supertipo de recurso. Este tipo é indicado pela propriedade `sling:resourceSuperType`. Esses supertipos também são considerados ao tentar encontrar um script. A vantagem dos supertipos de recursos é que eles podem formar uma hierarquia de recursos em que o tipo de recurso padrão `sling/servlet/default` (usado pelos servlets padrão) é efetivamente a raiz.

O supertipo de recurso de um recurso pode ser definido de duas maneiras:

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

A hierarquia de tipo de:

* `/x`
   * É `[ c, b, a, <default>]`
* Enquanto para `/y`
   * A hierarquia é `[ c, a, <default>]`

O motivo é porque `/y` tem a propriedade `sling:resourceSuperType`, enquanto `/x` não tem e, portanto, seu supertipo é retirado de seu tipo de recurso.

#### Os scripts do Sling não podem ser chamados diretamente {#sling-scripts-cannot-be-called-directly}

No Sling, os scripts não podem ser chamados diretamente porque quebrariam o conceito estrito de um servidor REST; você misturaria recursos e representações.

Se você chamar a representação (o script) diretamente, ocultará o recurso dentro do script para que a estrutura (Sling) não saiba mais sobre ela. Dessa forma, você perde determinados recursos:

* Manuseio automático de métodos http diferentes do GET, incluindo:
   * POST, PUT, DELETE que é manipulada com uma implementação padrão do sling
   * O script `POST.jsp` no seu local `sling:resourceType`
* Sua arquitetura de código não é mais tão limpa nem tão claramente estruturada como deveria ser; de importância primordial para o desenvolvimento em larga escala

### API Sling {#sling-api}

Usa o pacote da API do Sling, `org.apache.sling.*`, e bibliotecas de tags.

### Referenciando elementos existentes usando sling:include {#referencing-existing-elements-using-sling-include}

Uma consideração final é a necessidade de fazer referência aos elementos existentes nos scripts.

Scripts mais complexos (agregar scripts) acessam vários recursos (por exemplo, navegação, barra lateral, rodapé, elementos de uma lista) e fazem isso incluindo o *recurso*.

Nesse caso, você pode usar o comando `sling:include("/<path>/<resource>")`. Ele inclui efetivamente a definição do recurso referenciado.

## OSGi {#osgi}

O OSGi (Open Services Gateway Initiative) define uma arquitetura para desenvolver e implantar aplicativos e bibliotecas modulares (também é conhecido como Dynamic Module System for Java™). Os contêineres OSGi permitem dividir o aplicativo em módulos individuais (são arquivos jar com informações meta adicionais e chamados de pacotes na terminologia OSGi) e gerenciar as dependências cruzadas entre eles com:

* Serviços implementados no container
* Um contrato entre o contêiner e seu aplicativo

Esses serviços e contratos fornecem uma arquitetura que permite que elementos individuais descubram dinamicamente uns aos outros para colaboração.

Uma estrutura OSGi oferece carregamento/descarregamento dinâmico, configuração e controle desses pacotes, sem exigir reinicializações.

>[!NOTE]
>
>Informações completas sobre a tecnologia OSGi podem ser encontradas no [site OSGi](https://www.osgi.org).
>
>Em particular, a página Educação Básica contém uma coleção de apresentações e tutoriais.

Essa arquitetura permite estender o Sling com módulos específicos do aplicativo. O Sling e, portanto, o AEM, usam a implementação [Apache Felix](https://felix.apache.org/documentation/index.html) do OSGi. Ambas as coleções de pacotes OSGi são executadas em uma estrutura OSGi.

Essa funcionalidade permite executar as seguintes ações em qualquer um dos pacotes da sua instalação:

* Instalar
* Início
* Parar
* Atualizar o
* Desinstalar
* Ver status mais recente
* Acesse informações mais detalhadas sobre pacotes específicos, por exemplo, nome simbólico, versão e localização

Consulte [Configurando OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obter mais informações.

## Estrutura no repositório {#structure-within-the-repository}

A lista a seguir fornece uma visão geral da estrutura que você vê no repositório.

* `/apps` - Relacionado ao aplicativo; inclui definições de componentes específicas do site. Os componentes que você desenvolve podem ser baseados nos componentes prontos para uso disponíveis em `/libs/core/wcm/components`.
* `/content` - Conteúdo criado para o seu site.
* `/etc`
* `/home` - Informações de usuário e grupo.
* `/libs` - Bibliotecas e definições que pertencem ao núcleo do AEM. As subpastas em `/libs` representam os recursos predefinidos do AEM. O conteúdo em `/libs` não pode ser modificado. Os recursos específicos do seu site devem ser feitos em `/apps`.
* `/tmp` - Área de trabalho temporária.
* `/var` - Arquivos que são alterados e atualizados pelo sistema; como logs de auditoria, estatísticas, manipulação de eventos.

>[!CAUTION]
>
>As alterações nessa estrutura ou nos arquivos dentro dela devem ser feitas com cuidado. Certifique-se de entender totalmente as implicações de qualquer alteração feita.
>
>Não altere nada no caminho `/libs`. Para configuração e outras alterações, copie o item de `/libs` para `/apps` e faça as alterações em `/apps`.
