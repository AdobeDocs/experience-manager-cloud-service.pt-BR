---
title: Visão geral do console da Live Copy
description: Saiba mais sobre as noções básicas do Console de visão geral da Live Copy para entender rapidamente o status das suas Live Copies a fim de sincronizar o conteúdo.
feature: Multi Site Manager
role: Admin
exl-id: 3ef7fbce-10a1-4b21-8486-d3c3706e537c
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 2%

---

# Visão geral do console da Live Copy {#live-copy-overview-console}

O **Visão geral da Live Copy** O console permite:

* Exibir/gerenciar a herança em um site.
   * Exibir a árvore do blueprint e a estrutura correspondente da Live Copy, junto com o status da herança
   * Alterar o status da herança, como suspender e retomar
   * Exibir propriedades do blueprint e da Live Copy
* Execute ações de implantação.

## Abrir a visão geral da Live Copy {#opening-the-live-copy-overview}

Você pode abrir a Visão geral da Live Copy em:

* [Painel lateral Referências de uma página do blueprint (console Sites)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Propriedades de uma página do blueprint](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Referências a uma página do Blueprint {#references-to-a-blueprint-page}

O **Visão geral da Live Copy** pode ser aberto a partir do **Referências** painel lateral do **Sites** console:

1. No **Sites** console, [navegue até a página do blueprint e selecione-a.](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. Abra o **[Referências](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** e selecione **Live Copies**.

   ![Live Copy do painel de referências](../assets/live-copy-references.png)

   >[!TIP]
   >
   >Você também pode abrir referências primeiro e depois selecionar o blueprint.

1. Selecionar **Visão geral da Live Copy** para mostrar e usar a visão geral de todas as Live Copies relacionadas ao blueprint selecionado.
1. Use **Fechar** para sair e retornar ao **Sites** console.

### Propriedades de uma página do Blueprint {#properties-of-a-blueprint-page}

O **Visão geral da Live Copy** pode ser aberto ao visualizar propriedades de uma página do blueprint:

1. Abrir **Propriedades** para a página do blueprint apropriada.
1. Abra o **Blueprint** guia - o **Visão geral da Live Copy** será exibida na barra de ferramentas superior:

   ![Guia Propriedades do Blueprint](../assets/live-copy-blueprint-tab.png)

1. Selecionar **Visão geral da Live Copy** para mostrar e usar a visão geral de todas as Live Copies relacionadas ao blueprint atual.

1. Use **Fechar** para sair e retornar ao **Sites** console.

## Uso da visão geral da Live Copy {#using-the-live-copy-overview}

O **Visão geral da Live Copy** fornece uma visão geral do status das Live Copies relacionadas à página selecionada.

![Janela Visão geral da Live Copy](../assets/live-copy-overview.png)

Uma implantação depende das ações de sincronização definidas na configuração de implantação específica. Algumas ações dependem de modificações no conteúdo. No entanto, também há muitas ações que não dependem de modificações no conteúdo, mas que dependem de eventos como a ativação da página. Esses eventos não modificam o conteúdo, mas modificam as propriedades internas relacionadas ao conteúdo.

Os campos de status também dependem das ações de sincronização definidas na configuração de implementação específica e indicam se houve alguma dessas ações no blueprint ou na Live Copy desde a última implantação bem-sucedida. Um campo de status refletirá apenas as ações na configuração de implementação específica. Se nenhum lançamento bem-sucedido tiver sido executado em uma Live Copy, o status sempre será atualizado.

Por exemplo, uma configuração de implementação é definida como `targetActivate`. Portanto, uma implantação dependerá apenas dos eventos de ativação. O campo de status indicará apenas se algum evento de ativação ocorreu desde a última implantação bem-sucedida.

O **Visão geral da Live Copy** também pode ser usado para executar ações na Live Copy:

1. Abra o **Visão geral da Live Copy**.
1. Selecione o blueprint necessário ou a página Live Copy e a barra de ferramentas será atualizada para mostrar as ações disponíveis. O [ações](overview.md#terms-used) disponível depende da seleção de um [blueprint](#actions-for-a-blueprint-page) ou [Live Copy](#actions-for-a-live-copy-page) página.

### Ações para uma página do Blueprint {#actions-for-a-blueprint-page}

Quando você seleciona uma página do blueprint, as seguintes ações estão disponíveis:

![Ações de visão geral da Live Copy para um blueprint](../assets/live-copy-overview-actions-blueprint.png)

* **Editar** - Abra a página do blueprint para edição.
* **[Implantação](overview.md#rollout-and-synchronize)** - Execute uma implantação para enviar as alterações da origem para a Live Copy.

### Ações para uma página de Live Copy {#actions-for-a-live-copy-page}

Quando você seleciona uma página de Live Copy, as seguintes ações estão disponíveis:

![Ações de visão geral da Live Copy para uma Live Copy](../assets/live-copy-overview-actions.png)

* **Editar** - Abra a página Live Copy para edição.
* **[Status do relacionamento](#relationship-status)** - Exibir informações sobre o status e a herança.
* **[Sincronizar](overview.md#rollout-and-synchronize)** - Sincronizar uma Live Copy para extrair as alterações da origem para a Live Copy.
* **[Redefinir](creating-live-copies.md#resetting-a-live-copy-page)** - Redefina uma página de Live Copy para remover todos os cancelamentos de herança e retornar a página ao mesmo estado que a página de origem.
* **[Suspender](overview.md#suspending-and-cancelling-inheritance-and-synchronization)** - Desativa temporariamente a relação ativa entre uma Live Copy e sua página do blueprint.
* **[Retomar](creating-live-copies.md#resuming-inheritance-for-a-page)** - Resume permite que você reinstale uma relação suspensa.
* **[Desanexar](overview.md#detaching-a-live-copy)** - Remove permanentemente a relação ativa entre uma Live Copy e sua página de blueprint.

## Status do relacionamento {#relationship-status}

O **Status do relacionamento** O console tem duas guias, fornecendo uma variedade de funcionalidades.

* [Status do relacionamento](#relationship-status-tab)
* [Live Copy ](#live-copy-tab)

### Status do relacionamento {#relationship-status-tab}

Esta guia fornece informações detalhadas sobre o status da relação entre o blueprint e a Live Copy.

![Guia Status da Relação](../assets/live-copy-relationship-status.png)

### Live Copy  {#live-copy-tab}

Esta guia permite visualizar e editar a configuração da Live Copy.

![Guia Live Copy](../assets/live-copy-relationship-status-live-copy.png)
