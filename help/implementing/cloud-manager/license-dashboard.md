---
title: Painel de licenças
description: O Cloud Manager fornece um painel para facilitar a visualização dos direitos de produto do AEMaaCS disponíveis para sua organização ou locatário.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 58%

---

# Painel de licenças {#license-dashboard}

O Cloud Manager fornece um painel para facilitar a visualização dos direitos de produto do AEMaaCS disponíveis para sua organização ou locatário.

## Visão geral {#overview}

O Painel de licenças do Cloud Manager fornece acesso fácil às seguintes informações:

1. Os direitos da solução estão disponíveis para você em todos os seus programas, incluindo o que é usado e o que está disponível
1. Métricas de consumo de Solicitação de conteúdo com tendência mensal para a solução Sites

## Uso do Painel de dispositivos {#using-dashboard}

Para acessar o painel de licenças, siga estas etapas.

>[!NOTE]
>
>Um usuário no **Proprietário da empresa** A função deve estar conectada para exibir o Painel de licenças.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No **[Meus programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** , alterne para a **Licença** guia.

![Painel de licenças](assets/license-dashboard.png)

O painel é dividido em três seções que mostram:

* **Soluções** - Essa seção resume quais soluções você licenciou, como Sites ou Assets.
* **Complementos** - Essa seção resume quais complementos estão disponíveis para suas soluções licenciadas.
* **Ambientes de sandbox e desenvolvimento** - Essa seção resume quais ambientes estão disponíveis para você.

Cada seção resume o que está disponível e como é usado, se for o caso. Atualmente, somente as soluções do Sites são exibidas, mesmo se outras soluções existirem no locatário.

* A variável **Status** exibe o número de direitos não utilizados em relação ao total disponível para o locatário.
* A coluna **Configurado em** indica os programas nos quais o direito da solução foi aplicado.
   * Um direito será considerado usado somente quando um ambiente de produção for criado ou, se existir, quando um pipeline de atualização for executado nele.
* A coluna **Uso** exibe as solicitações de conteúdo consumidas nos últimos 12 meses na forma de um gráfico quando clicadas.

>[!TIP]
>
>Para saber como gerenciar os direitos de Adobe em toda a organização pelo Admin Console, consulte [visão geral do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html).

## Perguntas frequentes {#faq}

### O que é uma solicitação de conteúdo? {#what-is-a-content-request}

Uma solicitação de conteúdo é uma solicitação recebida no AEM Sites ou em qualquer sistema de cache fornecido pelo cliente, como uma rede de entrega de conteúdo, para fornecer conteúdo ou dados no formato HTML como uma exibição de página ou no formato JSON como uma chamada de API.

Uma solicitação de conteúdo é contabilizada para cada exibição de página ou para cada cinco chamadas de API, medidas na entrada do primeiro sistema de cache a receber uma solicitação de conteúdo. As solicitações de conteúdo são contabilizadas somente em ambientes de produção.

As solicitações de conteúdo excluem solicitações ou atividades iniciadas pelo Adobe ou em nome dele com o único objetivo de fornecer produtos e serviços. O tráfego de agente de usuário identificado pela Adobe como bots, crawlers e spiders relacionados a mecanismos de pesquisa comuns e serviços de redes sociais também são excluídos.

Consulte também [Noções básicas sobre solicitações de conteúdo Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### Como o Adobe Experience Manager mede as solicitações de conteúdo? {#how-are-content-requests-measured}

As solicitações de conteúdo são rastreadas nos servidores de borda do AEM as a Cloud Service. O tráfego de origem não é contabilizado nas solicitações de conteúdo. O CDN incorporado ao AEM as a Cloud Service rastreia solicitações HTML e JSON válidas.

O AEM também tem regras em vigor para excluir bots conhecidos, incluindo serviços conhecidos que acessam o site regularmente para atualizar seu índice de pesquisa ou serviço.

Consulte também [Noções básicas sobre solicitações de conteúdo Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### Por que meu relatório de Analytics mostra resultados diferentes das solicitações de conteúdo do AEM? {#why-are-reports-different}

As solicitações de conteúdo podem ter variações entre as ferramentas de relatório de Analytics de uma organização. Para obter mais informações, consulte [Noções básicas sobre solicitações de conteúdo Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### E se eu quiser saber mais sobre o volume de solicitação de conteúdo? {#current-request-volumes}

Se você quiser obter insights adicionais sobre o volume de solicitação de conteúdo mostrado no Painel de licenças, a equipe da Adobe pode fornecer um relatório que mostra os principais responsáveis pelo volume das solicitações de conteúdo. Entre em contato com a equipe de Adobe ou com o Suporte ao cliente do Adobe para solicitar um relatório de uso principal.

### E se eu estiver usando meu próprio CDN? {#using-own-cdn}

O Painel de licenças mostra apenas os dados rastreados pelo CDN do Cloud Service. Se você optar por trazer seu próprio CDN (BYOCDN), relate o volume de solicitações de conteúdo de volta ao Adobe anualmente, conforme declarado em seu contrato.
