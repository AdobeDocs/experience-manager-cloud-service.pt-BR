---
title: Roteamento de modelo SPA
description: Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de encaminhamento, o contrato e as opções disponíveis.
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Roteamento de modelo SPA{#spa-model-routing}

Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de encaminhamento, o contrato e as opções disponíveis.

## Roteamento do projeto {#project-routing}

O aplicativo é o proprietário do roteamento e é implementado pelos desenvolvedores de front-end do projeto. Este documento descreve o roteamento específico para o modelo retornado pelo servidor AEM. A estrutura de dados do modelo de página expõe o URL do recurso subjacente. O projeto de front-end pode usar qualquer biblioteca personalizada ou de terceiros fornecendo funcionalidades de roteamento. Quando uma rota espera um fragmento de modelo, uma chamada para o `PageModelManager.getData()` função pode ser feita. Quando uma rota de modelo é alterada, um evento deve ser acionado para avisar as bibliotecas de escuta, como o Editor de páginas.

## Arquitetura {#architecture}

Para obter uma descrição detalhada, consulte o [PageModelManager](blueprint.md#pagemodelmanager) seção do documento Blueprint SPA.

## RoteadorModelo {#modelrouter}

A variável `ModelRouter` - quando ativado - encapsula as funções da API do histórico do HTML5 `pushState` e `replaceState` para garantir que determinado fragmento de modelo seja buscado previamente e acessível. Em seguida, notifica o componente de front-end registrado de que o modelo foi modificado.

## Roteiro de Modelo Manual vs. Automático {#manual-vs-automatic-model-routing}

A variável `ModelRouter` O automatiza a busca de fragmentos do modelo. Mas, como qualquer ferramenta automatizada, há limitações. Quando necessário, a variável `ModelRouter` podem ser desativadas ou configuradas para ignorar caminhos usando metapropriedades (Consulte a seção Metapropriedades do [Componente de página do SPA](page-component.md) documento). Os desenvolvedores de front-end podem então implementar sua própria camada de roteamento de modelo, solicitando a `PageModelManager` para carregar um determinado fragmento de modelo usando o `getData()` função.

>[!CAUTION]
>
>A versão atual do `ModelRouter` suportam apenas o uso de URLs que apontam para o caminho real do recurso dos pontos de entrada do Modelo Sling. Ele não é compatível com o uso de URLs ou aliases personalizados.

## Contrato de Encaminhamento {#routing-contract}

A implementação atual baseia-se no pressuposto de que o projeto SPA usa a API de Histórico HTML5 para roteamento para as diferentes páginas de aplicativos.

### Configuração {#configuration}

A variável `ModelRouter` O suporta o conceito de roteamento de modelo conforme ele escuta `pushState` e `replaceState` chamadas para buscar previamente fragmentos do modelo. Internamente, ele aciona o `PageModelManager` para carregar o modelo que corresponde a um determinado URL e acionar um `cq-pagemodel-route-changed` evento que outros módulos podem ouvir.

Por padrão, esse comportamento é ativado automaticamente. Para desativá-lo, o SPA deve renderizar a seguinte metapropriedade:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Observe que cada rota do SPA deve corresponder a um recurso acessível no AEM (por exemplo, &quot; `/content/mysite/mypage"`), uma vez que `PageModelManager` O tentará carregar automaticamente o modelo de página correspondente quando a rota for selecionada. Embora, se necessário, o SPA também possa definir uma &quot;lista de bloqueios&quot; de rotas que devem ser ignoradas pelo `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
