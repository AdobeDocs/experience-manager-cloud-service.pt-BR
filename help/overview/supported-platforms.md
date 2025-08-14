---
title: Plataformas de cliente compatíveis
description: Saiba quais navegadores são compatíveis com a criação de conteúdo com o Adobe Experience Manager as a Cloud Service e com o acesso a sites publicados com o AEM.
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 7ddd0a75-621a-4499-91d1-7b3408a68269
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 2%

---

# Plataformas de cliente compatíveis {#supported-platforms}

Saiba quais navegadores são compatíveis com a criação de conteúdo com o Adobe Experience Manager as a Cloud Service e com o acesso a sites publicados com o AEM.

>[!TIP]
>
>Este documento aborda as plataformas clientes compatíveis com o AEM as a Cloud Service. Para obter detalhes sobre o ambiente de compilação para desenvolver seu projeto do AEM, consulte o documento [Ambiente de compilação.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)

## Níveis de suporte {#support-levels}

O Adobe define os seguintes níveis de suporte para as plataformas de cliente da AEM.

| Nível de compatibilidade | Descrição |
|---|---|
| A: Suportado | A Adobe oferece suporte e manutenção completos para essa configuração. Essa configuração é coberta pelo processo de controle de qualidade da Adobe. |
| R: Suporte restrito | O suporte exige uma solicitação formal à Adobe para usar a configuração em um projeto. Depois de confirmado pela Adobe, a Adobe fornece suporte total dentro do programa de suporte restrito. Para obter mais informações, entre em contato com o Atendimento ao cliente da Adobe. |
| Z: Não suportado | A configuração não é compatível. A Adobe não faz declarações sobre se a configuração funciona e não oferece suporte a ela. |

## Navegadores compatíveis com a criação de conteúdo {#authoring}

A interface do usuário do AEM é otimizada para telas maiores encontradas em notebooks, computadores desktop e dispositivos tablets (como o Apple iPad ou Microsoft Surface). O formato de telefone não é compatível com nenhum caso de uso de criação.

A interface de usuário do Adobe Experience Manager funciona com as seguintes plataformas de cliente, dependendo do [método de criação.](/help/edge/overview.md#authoring-method)

* [Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md)
* [Editor de página](/help/sites-cloud/authoring/page-editor/introduction.md)
* [Criação baseada em documentos](https://www.aem.live/docs/aem-authoring) usando o [Sidekick](https://www.aem.live/docs/sidekick)

Todos os navegadores são testados com o conjunto padrão de plug-ins e complementos.

| Navegador | Nível de Suporte do Editor Universal | Nível de suporte do editor de páginas | Nível de suporte da Sidekick |
|---|---|---|---|
| Google Chrome (evergreen) | A: Suportado | A: Suportado | A: Suportado |
| Microsoft Edge (evergreen) | A: Suportado | A: Suportado | Z: Não suportado |
| Mozilla Firefox (evergreen) | A: Suportado | A: Suportado | Z: Não suportado |
| ESR mais recente do Mozilla Firefox [1] | A: Suportado | A: Suportado | Z: Não suportado |
| Safari no macOS (evergreen) | A: Suportado | A: Suportado | Z: Não suportado |
| Safari no iPadOS (evergreen) | Z: Não suportado | A: Suportado | Z: Não suportado |

1. Versão de suporte estendido do Firefox ([saiba mais em mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/))

>[!NOTE]
>
>**Suporte para navegadores com ciclos de lançamento rápidos:**
>
>Atualizações regulares de versões do Firefox, Chrome e Edge. A Adobe tem o compromisso de manter o nível de suporte listado acima para as próximas versões desses navegadores.

## Navegadores compatíveis com sites {#websites}

O suporte do navegador para sites renderizados pelo AEM depende da implementação de modelos de página, blocos, design e saída de componente do AEM. Portanto, os desenvolvedores que implementam o projeto controlam a compatibilidade do site.

O [modelo do projeto do AEM,](https://www.aem.live/developer/ue-tutorial#create-github-project) [Componentes principais,](/help/implementing/developing/components/overview.md#aem-core-components) e [site de exemplo do WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) são compatíveis com todos os navegadores modernos.
