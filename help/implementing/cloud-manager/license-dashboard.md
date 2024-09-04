---
title: Painel de licenças
description: O Cloud Manager fornece um painel para facilitar a visualização dos direitos de produto do AEMaaCS disponíveis para sua organização ou locatário.
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 57fb7a011cb2da853cdca4f3233cd56775f4a459
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 37%

---


# Painel de licenças {#license-dashboard}

O Cloud Manager fornece um painel para facilitar a visualização dos direitos de produto do AEMaaCS disponíveis para sua organização ou locatário.

>[!IMPORTANT]
>
>O painel de licenças se aplica somente aos programas do AEM as a Cloud Service. [Programas AMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction) não estão incluídos no painel de licenças.
>
>Para determinar o tipo de serviço que seu programa tem (AMS ou AEMaaCS), consulte o documento [Navegação na interface do usuário do Cloud Manager.](/help/implementing/cloud-manager/navigation.md#program-cards)

## Visão geral {#overview}

O Painel de licenças do Cloud Manager fornece acesso fácil às seguintes informações:

1. Os direitos da solução estão disponíveis para você em todos os seus programas, incluindo o que é usado e o que está disponível
1. Métricas de consumo de Solicitação de conteúdo com tendência mensal para a solução Sites

## Uso do Painel de dispositivos {#using-dashboard}

Para acessar o painel de licenças, siga estas etapas.

>[!NOTE]
>
>Um usuário com a função **Proprietário da empresa** deve estar conectado para exibir o Painel de Licenças.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, toque ou clique no botão de menu de hambúrguer no Cabeçalho do Cloud Manager [.](/help/implementing/cloud-manager/navigation.md#cloud-manager-header) Isso revela as guias.
1. Toque ou clique na opção **Licença** na guia.

![Painel de licenças](assets/license-dashboard.png)

O painel é dividido em três seções que mostram:

* **Soluções** - Essa seção resume quais soluções você licenciou, como Sites ou Assets.
* **Complementos** - Essa seção resume quais complementos estão disponíveis para suas soluções licenciadas.
* **Outros direitos** - Esta seção resume qual ambiente de sandbox e desenvolvimento, bem como outros direitos que podem ser consumidos em seu locatário.

Cada seção resume o que está disponível e como é usado, se for o caso. Atualmente, somente as soluções do Sites e do Assets são exibidas, mesmo se outras soluções existirem no locatário.

* A coluna **Status** exibe o número de direitos não utilizados em relação ao total disponível para o locatário.
* A coluna **Configurado em** indica os programas nos quais o direito da solução foi aplicado.
   * Um direito será considerado usado somente quando um ambiente de produção for criado ou, se existir, quando um pipeline de atualização for executado nele.
   * Somente um número limitado de programas é listado individualmente na coluna com o restante representado por uma entrada `+x`.
   * Passe o mouse sobre a entrada `+x` para obter um pop-up com os detalhes de todos os programas.
* A coluna **Uso** exibe um botão **[Exibir detalhes de uso](#view-usage-details)** para mostrar estatísticas de uso da solução.

>[!TIP]
>
>Para saber como gerenciar os direitos de Adobe em toda a organização usando o Admin Console, consulte a [visão geral sobre Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html).

## Visualizar detalhes de uso {#view-usage-details}

<!--
The **View usage details** button gives access to the chosen solution's **Usage Details** window. This window gives a detailed breakdown including charts to show your solution's usage. How that usage is measured depends on the chosen solution. -->

O botão **Exibir detalhes de uso** na área de licença do Cloud Manager fornece um detalhamento do uso de recursos atual. Quando clicado, ele abre um relatório ou painel que mostra métricas importantes relacionadas à sua licença. <!-- ADD THIS SENTENCE IF ASSETS USAGE DETAILS GETS REINSTATED ", such as the number of users, storage consumption, or bandwidth usage, depending on the type of services you're using." --> Essa funcionalidade ajuda a monitorar e garantir que você permaneça nos limites do contrato, oferecendo insights para um melhor planejamento e otimização de recursos.

### Detalhes de uso de sites {#sites-usage-details}

A janela **Detalhes de uso do Sites** apresenta gráficos com uma visão geral do uso das licenças do Sites com base em [solicitações de conteúdo.](#what-is-a-content-request)

![Janela de detalhes de uso do Sites](assets/sites-usage-details.png)

O lado esquerdo da janela apresenta um gráfico de pizza que mostra o detalhamento do contrato para o ano do contrato selecionado na lista suspensa **Exibir ano do contrato**.

O lado direito da janela apresenta um gráfico de área que mostra o uso detalhado por programa ao longo do tempo para o ano do contrato selecionado. Um cursor do mouse revela um pop-up com detalhes por programa para o ponto no tempo selecionado.

<!-- REMOVED AS PER CQDOC-21983
### Assets usage details {#assets-usage-details}

The **Assets usage details** window, presents graphs giving an overview of the usage of your Assets licenses based on [storage](#storage) and [standard users.](#standard-users) Select the appropriate tab to toggle between the views.

For both storage and standard users views, you can use the **Environment Type** dropdown to toggle the view between production, stage, and development environments.

#### Storage {#storage}

![Assets usage details window for storage](assets/assets-usage-details-storage.png)

The left side of the window presents a pie chart showing the contract breakdown for the contract year selected in the **View contract year** dropdown.

The right side of the window presents an area chart showing the usage broken down by program over time for the selected contract year. A hover reveals a popup with details per program for the selected point in time.

#### Standard Users {#standard-users}

![Assets usage details window for standard-users](assets/assets-usage-details-standard-users.png)

The left side of the window presents a pie chart showing the contract breakdown for the contract year selected in the **View contract year** dropdown.

The right side of the window presents an area chart showing the usage broken down by program over time for the selected contract year. A hover reveals a popup with details per program for the selected point in time. -->

## Perguntas frequentes {#faq}

### O que é uma solicitação de conteúdo? {#what-is-a-content-request}

Uma solicitação de conteúdo é uma solicitação recebida no AEM Sites ou em qualquer sistema de cache fornecido pelo cliente, como uma rede de entrega de conteúdo, para fornecer conteúdo ou dados no formato HTML como uma exibição de página ou no formato JSON como uma chamada de API.

Uma solicitação de conteúdo é contabilizada para cada exibição de página ou para cada cinco chamadas de API, medidas na entrada do primeiro sistema de cache a receber uma solicitação de conteúdo. As solicitações de conteúdo são contabilizadas somente em ambientes de produção.

As solicitações de conteúdo excluem solicitações ou atividades iniciadas pelo Adobe ou em nome dele com o único objetivo de fornecer produtos e serviços. O tráfego de agente de usuário identificado pela Adobe como bots, crawlers e spiders relacionados a mecanismos de pesquisa comuns e serviços de redes sociais também são excluídos.

Consulte também [Entendendo as solicitações de conteúdo do Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### Como o Adobe Experience Manager mede as solicitações de conteúdo? {#how-are-content-requests-measured}

As solicitações de conteúdo são rastreadas nos servidores de borda do AEM as a Cloud Service. O tráfego de origem não é contabilizado nas solicitações de conteúdo. O CDN incorporado ao AEM as a Cloud Service rastreia solicitações HTML e JSON válidas.

O AEM também tem regras em vigor para excluir bots conhecidos, incluindo serviços conhecidos que acessam o site regularmente para atualizar seu índice de pesquisa ou serviço.

Consulte também [Entendendo as solicitações de conteúdo do Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### Por que meu relatório de Analytics mostra resultados diferentes das solicitações de conteúdo do AEM? {#why-are-reports-different}

As solicitações de conteúdo podem ter variações entre as ferramentas de relatório de Analytics de uma organização. Para obter mais informações, consulte [Entendendo as Solicitações de Conteúdo Cloud Service](/help/implementing/cloud-manager/content-requests.md).

### E se eu quiser saber mais sobre o volume de solicitação de conteúdo? {#current-request-volumes}

Se você quiser obter insights adicionais sobre o volume de solicitação de conteúdo mostrado no Painel de licenças, a equipe da Adobe pode fornecer um relatório que mostra os principais responsáveis pelo volume das solicitações de conteúdo. Entre em contato com a equipe de Adobe ou com o Suporte ao cliente do Adobe para solicitar um relatório de uso principal.

### E se eu estiver usando meu próprio CDN? {#using-own-cdn}

O Painel de licenças mostra apenas os dados rastreados pelo CDN do Cloud Service. Se você optar por trazer seu próprio CDN (BYOCDN), relate o volume de solicitações de conteúdo de volta ao Adobe anualmente, conforme declarado em seu contrato.
