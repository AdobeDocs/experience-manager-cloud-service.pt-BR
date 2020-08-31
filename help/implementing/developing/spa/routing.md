---
title: Roteamento de modelo SPA
description: Para aplicativos de página única em AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo do roteamento, o contrato e as opções disponíveis.
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# Roteamento de modelo SPA{#spa-model-routing}

Para aplicativos de página única em AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo do roteamento, o contrato e as opções disponíveis.

## Roteamento do projeto {#project-routing}

O aplicativo é proprietário do roteamento e é implementado pelos desenvolvedores front-end do projeto. Este documento descreve o roteamento específico para o modelo retornado pelo servidor AEM. A estrutura de dados do modelo de página expõe o URL do recurso subjacente. O projeto front-end pode usar qualquer biblioteca personalizada ou de terceiros que ofereça funcionalidades de roteamento. Quando uma rota espera um fragmento de modelo, uma chamada para a `PageModelManager.getData()` função pode ser feita. Quando uma rota de modelo é alterada, um evento deve ser acionado para avisar bibliotecas de escuta, como o Editor de páginas.

## Arquitetura {#architecture}

Para obter uma descrição detalhada, consulte a seção [PageModelManager](blueprint.md#pagemodelmanager) do documento Blueprint SPA.

## ModelRouter {#modelrouter}

O `ModelRouter` - quando ativado - encapsula as funções da API do histórico HTML5 `pushState` `replaceState` e garante que um determinado fragmento do modelo seja obtido previamente e acessível. Em seguida, notifica o componente de front-end registrado de que o modelo foi modificado.

## Roteamento de modelo manual vs automático {#manual-vs-automatic-model-routing}

A `ModelRouter` automatiza a busca de fragmentos do modelo. Mas como qualquer ferramenta automática, ela traz limitações. Quando necessário, o `ModelRouter` pode ser desativado ou configurado para ignorar caminhos usando metapropriedades (consulte a seção Metpropriedades do documento do componente [da página](page-component.md) SPA). Os desenvolvedores front-end podem então implementar sua própria camada de roteamento de modelo, solicitando que `PageModelManager` o carregue qualquer fragmento específico do modelo usando a `getData()` função.

>[!CAUTION]
>
>A versão atual do suporte `ModelRouter` apenas ao uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo Sling. Ele não suporta o uso de URLs ou aliases personalizados.

## Contrato de roteamento {#routing-contract}

A implementação atual baseia-se na suposição de que o projeto SPA usa a API do histórico HTML5 para roteamento para as diferentes páginas do aplicativo.

### Configuração {#configuration}

O `ModelRouter` oferece suporte ao conceito de roteamento de modelo à medida que ele escuta `pushState` e `replaceState` chama para buscar previamente fragmentos de modelo. Internamente, ele aciona o `PageModelManager` para carregar o modelo que corresponde a um determinado URL e aciona um `cq-pagemodel-route-changed` evento que outros módulos podem ouvir.

Por padrão, esse comportamento é ativado automaticamente. Para desativá-la, o SPA deve renderizar a seguinte propriedade meta:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Observe que cada rota do SPA deve corresponder a um recurso acessível no AEM (por exemplo, &quot; `/content/mysite/mypage"`), pois o `PageModelManager` tentará carregar automaticamente o modelo de página correspondente depois que a rota for selecionada. Embora, se necessário, o SPA também possa definir uma &quot;lista de bloqueios&quot; de rotas que devem ser ignoradas pelo `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
