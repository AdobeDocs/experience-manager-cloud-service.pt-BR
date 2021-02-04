---
title: O componente RemotePage
description: O Componente RemotePage é um componente de página personalizado para editar o React SPA remoto no AEM.
translation-type: tm+mt
source-git-commit: 6a88b93a4005b858eec222fd7ae15df9db269d31
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# O componente RemotePage {#remote-page-component}

Ao decidir [que nível de integração](/help/implementing/developing/headful-headless.md) você gostaria de ter entre seus SPA externos e AEM, geralmente fica claro que você precisa ser capaz de visualização e editar o SPA dentro do AEM. O Componente RemotePage é um componente de página personalizado apenas para essa finalidade.

## Visão geral {#overview}

O componente RemotePage obtém todos os ativos necessários do `asset-manifest.json` gerado pelo aplicativo e o usa para renderizar o SPA dentro do AEM.

## Requisitos {#requirements}

* Ativar CORS no desenvolvimento
* Configurar URL remoto nas Propriedades da página
* Renderizar o SPA em AEM

## Limitações           {#limitations}

* A implementação atual do componente RemotePage suporta apenas aplicações React remotas.
* O CSS interno definido no arquivo HTML raiz do aplicativo, bem como o CSS em linha no nó DOM raiz não estará disponível ao fazer renderização remota no AEM.

## Detalhes técnicos {#technical-details}

Como o resto do projeto de SPA AEM, o Componente RemotePage é de código aberto. Para obter todos os detalhes técnicos do Componente RemotePage, [consulte o repositório GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
