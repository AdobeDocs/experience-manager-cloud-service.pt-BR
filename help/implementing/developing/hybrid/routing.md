---
title: Roteamento do Modelo de SPA
description: Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de roteamento, o contrato e as opções disponíveis.
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Roteamento do Modelo de SPA{#spa-model-routing}

Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de roteamento, o contrato e as opções disponíveis.

## Roteamento do projeto {#project-routing}

O aplicativo é proprietário do roteamento e é implementado pelos desenvolvedores de front-end do projeto. Este documento descreve o roteamento específico para o modelo retornado pelo servidor AEM. A estrutura de dados do modelo de página expõe o URL do recurso subjacente. O projeto front-end pode usar qualquer biblioteca personalizada ou de terceiros que forneça funcionalidades de roteamento. Quando uma rota espera um fragmento de modelo, uma chamada para a variável `PageModelManager.getData()` pode ser feita. Quando uma rota de modelo é alterada, um evento deve ser acionado para avisar as bibliotecas de escuta, como o Editor de páginas.

## Arquitetura {#architecture}

Para obter uma descrição detalhada, consulte o [PageModelManager](blueprint.md#pagemodelmanager) seção do documento Blueprint SPA.

## ModelRouter {#modelrouter}

O `ModelRouter` - quando ativado - encapsula as funções da API do Histórico do HTML5 `pushState` e `replaceState` para garantir que um determinado fragmento do modelo seja buscado e acessível previamente. Em seguida, notifica o componente front-end registrado de que o modelo foi modificado.

## Roteamento Manual vs Automático de Modelo {#manual-vs-automatic-model-routing}

O `ModelRouter` automatiza a busca de fragmentos do modelo. Mas como qualquer ferramenta automatizada, ela tem limitações. Quando necessário `ModelRouter` pode ser desativado ou configurado para ignorar caminhos usando propriedades meta (consulte a seção Propriedades Meta do [Componente Página SPA](page-component.md) documento). Os desenvolvedores de front-end podem implementar sua própria camada de roteamento de modelo, solicitando a `PageModelManager` para carregar qualquer fragmento específico do modelo usando o `getData()` .

>[!CAUTION]
>
>A versão atual do `ModelRouter` suporta apenas o uso de URLs que apontem para o caminho de recurso real dos pontos de entrada do Modelo do Sling. Não é compatível com o uso de URLs ou aliases personalizados.

## Contrato de Roteamento {#routing-contract}

A implementação atual baseia-se na hipótese de que o projeto de SPA usa a API do Histórico do HTML5 para rotear para as diferentes páginas do aplicativo.

### Configuração {#configuration}

O `ModelRouter` suporta o conceito de roteamento de modelo como ele escuta `pushState` e `replaceState` chamadas para buscar fragmentos de modelo previamente. Internamente, ele dispara a função `PageModelManager` para carregar o modelo que corresponde a um determinado URL e dispara um `cq-pagemodel-route-changed` evento que outros módulos podem ouvir.

Por padrão, esse comportamento é ativado automaticamente. Para desativá-lo, o SPA deve renderizar a seguinte meta propriedade:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Observe que cada rota do SPA deve corresponder a um recurso acessível em AEM (por exemplo, &quot; `/content/mysite/mypage"`) desde a `PageModelManager` O tentará carregar automaticamente o modelo de página correspondente depois que a rota for selecionada. Embora, se necessário, o SPA também possa definir uma &quot;lista de bloqueios&quot; de rotas que devem ser ignoradas pelo `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
