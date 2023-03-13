---
title: Componente de página SPA
description: Em um SPA, o componente página não fornece os elementos HTML de seus componentes filhos, mas delega isso à estrutura SPA. Este documento explica como isso torna o componente de página de um SPA exclusivo.
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 8%

---

# Componente de página SPA {#spa-page-component}

O componente de página de um SPA não fornece os elementos de HTML de seus componentes filhos por meio de um arquivo JSP ou HTL e objetos de recurso. Esta operação é delegada na estrutura de SPA. A representação de componentes secundários é buscada como uma estrutura de dados JSON (ou seja, o modelo). Os componentes do SPA são adicionados à página de acordo com o modelo JSON fornecido. Dessa forma, a composição do corpo inicial do componente de página difere de suas contrapartes de HTML pré-renderizadas.

## Gerenciamento do modelo de página {#page-model-management}

A resolução e o gerenciamento do modelo de página são delegados a um determinado [`PageModelManager`](blueprint.md#pagemodelmanager) módulo. O SPA deve interagir com a `PageModelManager` módulo ao ser inicializado para buscar o modelo da página inicial e registrar-se para atualizações de modelo - produzido principalmente quando o autor está editando a página por meio do Editor de páginas. A variável `PageModelManager` pode ser acessado pelo projeto SPA como um pacote npm. Por ser um intérprete entre o AEM e o SPA, o `PageModelManager` deve acompanhar o SPA.

Para permitir que a página seja criada, uma biblioteca do cliente chamada `cq.authoring.pagemodel.messaging` deve ser adicionado para fornecer um canal de comunicação entre o SPA e o editor de páginas. Se o componente da página SPA herdar do componente wcm/core da página, há as seguintes opções para fazer o `cq.authoring.pagemodel.messaging` categoria da biblioteca do cliente disponível:

* Se o modelo for editável, adicione a categoria da biblioteca do cliente à política da página.
* Adicione a categoria da biblioteca do cliente usando o `customfooterlibs.html` do componente de página.

Não se esqueça de limitar a inclusão do `cq.authoring.pagemodel.messaging` categoria ao contexto do editor de páginas.

## Tipo de dados da comunicação {#communication-data-type}

O tipo de dados de comunicação é definido como um elemento HTML dentro do componente Página AEM usando o `data-cq-datatype` atributo. Quando o tipo de dados de comunicação é definido como JSON, as solicitações do GET atingem os pontos de extremidade do Modelo Sling de um componente. Depois que uma atualização ocorre no editor de páginas, a representação JSON do componente atualizado é enviada para a biblioteca do Modelo de página. A biblioteca Modelo de página avisa o SPA sobre atualizações.

**Componente de página SPA -`body.html`**

```
<div id="page"></div>
```

Além de ser uma boa prática para não atrasar a geração de DOM, a estrutura SPA requer que os scripts sejam adicionados ao final do corpo.

**Componente de página SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

As propriedades do meta recursos que descrevem o conteúdo SPA:

**Componente de página SPA -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>O seletor de modelo padrão é definido estaticamente ao solicitar a representação do Modelo do Sling de um componente.

## Propriedades Meta {#meta-properties}

* `cq:wcmmode`: modo WCM dos editores (por exemplo, página, modelo)
* `cq:pagemodel_root_url`: URL do modelo raiz do aplicativo. Fundamental ao acessar diretamente uma página secundária, pois o modelo de página secundária é um fragmento do modelo raiz do aplicativo. A variável `PageModelManager` em seguida, recomenda sistematicamente o modelo inicial do aplicativo como entrada no aplicativo a partir de seu ponto de entrada raiz.
* `cq:pagemodel_router`: Ative ou desative o [`ModelRouter`](routing.md) do `PageModelManager` biblioteca
* `cq:pagemodel_route_filters`: lista separada por vírgulas ou expressões regulares para fornecer rotas para o [`ModelRouter`](routing.md) deve ignorar.

## Sincronização de sobreposição do editor de páginas {#page-editor-overlay-synchronization}

A sincronização das sobreposições é garantida pelo mesmo Mutation Observer fornecido pelo `cq.authoring.page` categoria.

## Configuração da estrutura exportada JSON do modelo Sling {#sling-model-json-exported-structure-configuration}

Quando os recursos de roteamento estão ativados, presume-se que a exportação em JSON do SPA contenha as diferentes rotas do aplicativo graças à exportação em JSON do componente de navegação AEM. A saída JSON do componente de navegação do AEM pode ser configurada na política de conteúdo da página raiz do SPA por meio das duas propriedades a seguir:

* `structureDepth`: Número correspondente à profundidade da árvore exportada
* `structurePatterns`: Regex da matriz de regex correspondente à página a ser exportada
