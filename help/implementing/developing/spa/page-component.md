---
title: Componente de página do SPA
description: Em um SPA, o componente de página não fornece os elementos HTML de seus componentes filhos, mas delega isso na estrutura do SPA. Este documento explica como isso torna o componente de página de um SPA único.
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Componente de página do SPA {#spa-page-component}

O componente de página de um SPA não fornece os elementos HTML de seus componentes filho por meio de um arquivo JSP ou HTL e objetos de recurso. Esta operação é delegada no quadro SPA. A representação dos componentes filhos é buscada como uma estrutura de dados JSON (ou seja, o modelo). Os componentes do SPA são adicionados à página de acordo com o modelo JSON fornecido. Dessa forma, a composição inicial do corpo do componente da página difere de seus equivalentes HTML pré-renderizados.

## Gerenciamento do modelo de página {#page-model-management}

A resolução e o gerenciamento do modelo de página são delegados em um [`PageModelManager`](blueprint.md#pagemodelmanager) módulo fornecido. O SPA deve interagir com o `PageModelManager` módulo ao inicializar para buscar o modelo de página inicial e registrar-se para atualizações de modelo - produzido principalmente quando o autor está editando a página pelo Editor de páginas. O `PageModelManager` é acessível pelo projeto SPA como um pacote npm. Sendo um intérprete entre AEM e a ZPE, o `PageModelManager` deve acompanhar a ZPE.

Para permitir a criação da página, é necessário adicionar uma biblioteca de cliente chamada `cq.authoring.pagemodel.messaging` para fornecer um canal de comunicação entre o SPA e o editor de página. Se o componente de página SPA herdar da página wcm/componente principal, então há as seguintes opções para disponibilizar a categoria da biblioteca do `cq.authoring.pagemodel.messaging` cliente:

* Se o modelo for editável, adicione a categoria da biblioteca do cliente à política de página.
* Adicione a categoria da biblioteca do cliente usando a parte `customfooterlibs.html` do componente da página.

Não se esqueça de limitar a inclusão da `cq.authoring.pagemodel.messaging` categoria ao contexto do editor de páginas.

## Tipo de dados de comunicação {#communication-data-type}

O tipo de dados de comunicação é definido como um elemento HTML dentro do componente Página AEM usando o `data-cq-datatype` atributo. Quando o tipo de dados de comunicação é definido como JSON, as solicitações de GET atingem os pontos finais do Modelo Sling de um componente. Depois que uma atualização ocorre no editor de página, a representação JSON do componente atualizado é enviada para a biblioteca do Modelo de página. A biblioteca do Modelo de página avisa o SPA sobre atualizações.

**Componente de página do SPA -`body.html`**

```
<div id="page"></div>
```

Além de ser uma boa prática não atrasar a geração de DOM, a estrutura do SPA exige que os scripts sejam adicionados ao final do corpo.

**Componente de página do SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

As propriedades dos recursos meta que descrevem o conteúdo do SPA:

**Componente de página do SPA -`customheaderlibs.html`**

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
>O seletor de modelo padrão é definido estaticamente ao solicitar a representação do Modelo Sling de um componente.

## Propriedades Meta {#meta-properties}

* `cq:wcmmode`: Modo WCM dos editores (por exemplo, página, modelo)
* `cq:pagemodel_root_url`: URL do modelo raiz do aplicativo. É fundamental ao acessar diretamente uma página secundária, pois o modelo de página filho é um fragmento do modelo raiz do aplicativo. Em seguida, o `PageModelManager` recompõe sistematicamente o modelo inicial do aplicativo ao inserir o aplicativo a partir do ponto de entrada raiz.
* `cq:pagemodel_router`: Ativar ou desativar a [`ModelRouter`](routing.md) biblioteca `PageModelManager`
* `cq:pagemodel_route_filters`: Lista separada por vírgulas ou expressões regulares para fornecer rotas que [`ModelRouter`](routing.md) devem ser ignoradas.

## Sincronização de sobreposição do editor de páginas {#page-editor-overlay-synchronization}

A sincronização das sobreposições é garantida pelo mesmo Observador de Mutações fornecido pela `cq.authoring.page` categoria.

## Configuração da Estrutura Exportada JSON do Modelo Sling {#sling-model-json-exported-structure-configuration}

Quando os recursos do roteamento estiverem ativados, a suposição é que a exportação JSON do SPA contenha as diferentes rotas do aplicativo graças à exportação JSON do componente de navegação AEM. A saída JSON do componente de navegação AEM pode ser configurada na política de conteúdo da página raiz do SPA por meio das duas propriedades a seguir:

* `structureDepth`: Número correspondente à profundidade da árvore exportada
* `structurePatterns`: Regex de matriz de regex correspondente à página a ser exportada
