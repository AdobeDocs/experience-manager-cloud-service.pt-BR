---
title: Componente de página SPA
description: Em um SPA, o componente de página não fornece os elementos HTML de seus componentes filho, mas delega isso à estrutura de SPA. Este documento explica como isso torna o componente de página de um SPA exclusivo.
exl-id: 41b56a60-ebb8-499d-a0ab-a2e920f26227
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 2%

---

# Componente de página SPA {#spa-page-component}

O componente de página de um SPA não fornece os elementos HTML de seus componentes filho por meio de um arquivo JSP ou HTL e objetos de recurso. Esta operação é delegada no quadro de SPA. A representação de componentes filho é buscada como uma estrutura de dados JSON (ou seja, o modelo). Os componentes de SPA são adicionados à página de acordo com o modelo JSON fornecido. Dessa forma, a composição do corpo inicial do componente de página difere de suas contrapartidas de HTML pré-renderizadas.

## Gerenciamento do modelo de página {#page-model-management}

A resolução e o gerenciamento do modelo de página são delegados a um [`PageModelManager`](blueprint.md#pagemodelmanager) módulo. O SPA deve interagir com o `PageModelManager` quando inicializa para buscar o modelo da página inicial e se registrar em atualizações de modelo - produzido principalmente quando o autor está editando a página por meio do Editor de páginas. O `PageModelManager` é acessível SPA projeto como um pacote npm. Sendo um intérprete entre o AEM e o SPA, o `PageModelManager` deve acompanhar o SPA.

Para permitir a criação da página, uma biblioteca do cliente chamada `cq.authoring.pagemodel.messaging` deve ser adicionado para fornecer um canal de comunicação entre o SPA e o editor de páginas. Se o componente de página de SPA herda do componente wcm/core da página, então há as seguintes opções para fazer a variável `cq.authoring.pagemodel.messaging` categoria de biblioteca de clientes disponível:

* Se o modelo for editável, adicione a categoria da biblioteca do cliente à política da página.
* Adicione a categoria da biblioteca do cliente usando o `customfooterlibs.html` do componente de página.

Não se esqueça de limitar a inclusão da variável `cq.authoring.pagemodel.messaging` para o contexto do editor de páginas.

## Tipo de dados da comunicação {#communication-data-type}

O tipo de dados de comunicação é definido como um elemento HTML dentro do componente Página de AEM usando o `data-cq-datatype` atributo. Quando o tipo de dados de comunicação é definido como JSON, as solicitações do GET atingem os endpoints do Modelo do Sling de um componente. Depois que uma atualização ocorre no editor de páginas, a representação JSON do componente atualizado é enviada para a biblioteca do Modelo de página. A biblioteca do Modelo de página avisa o SPA de atualizações.

**Componente de página SPA -`body.html`**

```
<div id="page"></div>
```

Além de ser uma boa prática não atrasar a geração do DOM, a estrutura do SPA exige que os scripts sejam adicionados ao final do corpo.

**Componente de página SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

As propriedades do meta resource que descrevem o conteúdo SPA:

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

* `cq:wcmmode`: Modo WCM dos editores (por exemplo, página, modelo)
* `cq:pagemodel_root_url`: URL do modelo raiz do aplicativo. Fundamental ao acessar diretamente uma página secundária, pois o modelo de página secundário é um fragmento do modelo raiz do aplicativo. O `PageModelManager` em seguida, recompõe sistematicamente o modelo inicial do aplicativo como inserindo o aplicativo a partir do ponto de entrada raiz.
* `cq:pagemodel_router`: Ative ou desative o [`ModelRouter`](routing.md) do `PageModelManager` biblioteca
* `cq:pagemodel_route_filters`: Lista separada por vírgulas ou expressões regulares para fornecer roteia a variável [`ModelRouter`](routing.md) deve ignorar.

## Sincronização de sobreposição do editor de páginas {#page-editor-overlay-synchronization}

A sincronização das sobreposições é garantida pelo mesmo Observador de Mutações fornecido pelo `cq.authoring.page` categoria .

## Configuração da Estrutura Exportada JSON do Modelo Sling {#sling-model-json-exported-structure-configuration}

Quando os recursos de roteamento estão ativados, a suposição é que a exportação JSON do SPA contém as diferentes rotas do aplicativo graças à exportação JSON do componente de navegação AEM. A saída JSON do componente de navegação de AEM pode ser configurada na política de conteúdo SPA página raiz por meio das duas propriedades a seguir:

* `structureDepth`: Número correspondente à profundidade da árvore exportada
* `structurePatterns`: Regex de matriz de regexes correspondente à página a ser exportada
