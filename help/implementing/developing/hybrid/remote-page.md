---
title: O componente RemotePage
description: O Componente de página remota é um componente de página personalizado para editar o React SPA remoto no AEM.
translation-type: tm+mt
source-git-commit: 9a1048f6d185d2d3229bab05b8e827845444d11c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# O componente RemotePage {#remote-page-component}

Ao decidir [que nível de integração](/help/implementing/developing/headful-headless.md) você gostaria de ter entre seu SPA externo e o AEM, geralmente fica claro que você precisa visualizar e editar o SPA no AEM. O Componente RemotePage é um componente de página personalizado apenas para essa finalidade.

## Visão geral {#overview}

O componente RemotePage obtém todos os ativos necessários do `asset-manifest.json` gerado pelo aplicativo e o usa para renderizar o SPA no AEM.

* A página remota permite inserir os scripts e as folhas de estilos de um SPA no corpo de um componente de página do AEM.
* Os Componentes do Virtual Frontend permitem marcar seções como editáveis no Editor do SPA do AEM.
* Juntos, um SPA hospedado em um domínio diferente pode ser editável no AEM.

Consulte o artigo [Editing an External SPA in AEM](editing-external-spa.md) para obter mais detalhes sobre SPAs editáveis e externos no AEM.

## Requisitos {#requirements}

* Habilitar CORS no desenvolvimento
* Configurar o URL remoto nas Propriedades da página
* Renderizar o SPA no AEM

## Limitações           {#limitations}

* A implementação atual do componente RemotePage suporta apenas aplicações de Reação Remota.
* O CSS interno definido no arquivo HTML raiz do aplicativo, bem como o CSS em linha no nó DOM raiz, não estarão disponíveis ao fazer a renderização remota no AEM.

## Detalhes técnicos {#technical-details}

Como o resto do projeto SPA do AEM, o Componente de página remota é de código aberto. Para obter os detalhes técnicos completos do Componente RemotePage, [consulte o repositório GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
