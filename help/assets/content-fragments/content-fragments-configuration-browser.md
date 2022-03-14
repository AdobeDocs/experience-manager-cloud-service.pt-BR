---
title: Fragmentos de conteúdo - Navegador de configuração
description: Saiba como ativar determinadas funcionalidades de Fragmento de conteúdo no Navegador de configuração para aproveitar AEM poderosos recursos de entrega sem cabeçalho.
feature: Content Fragments
role: User
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: e304b49b44cf871f3c47120fad7899407c573234
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 21%

---

# Fragmentos de conteúdo - Navegador de configuração{#content-fragments-configuration-browser}

Saiba como ativar determinadas funcionalidades de Fragmento de conteúdo no Navegador de configuração para aproveitar AEM poderosos recursos de entrega sem cabeçalho.

## Ativar a funcionalidade de fragmento de conteúdo para sua instância {#enable-content-fragment-functionality-instance}

Antes de usar Fragmentos de conteúdo, você precisa usar o **Navegador de configuração** para ativar:

* **Modelos de fragmentos do conteúdo** - obrigatório
* **Consultas Persistentes GraphQL** - opcional

>[!CAUTION]
>
>Se você não ativar **Modelos de fragmentos do conteúdo**:
>
>* o **Criar** não estará disponível para criar novos modelos.
>* você não poderá [selecione a configuração Sites para criar o ponto final relacionado](/help/headless/graphql-api/graphql-endpoint.md).


Para ativar a funcionalidade do fragmento de conteúdo, é necessário:

* Ativar o uso da funcionalidade de fragmento de conteúdo por meio do navegador de configuração
* Aplicar a configuração à sua pasta Ativos

### Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração {#enable-content-fragment-functionality-in-configuration-browser}

Para [usar determinada funcionalidade de Fragmento de conteúdo](#creating-a-content-fragment-model) you **must** primeiro habilite-os por meio da **Navegador de configuração**:

>[!NOTE]
>
>Para obter mais detalhes, consulte também [Navegador de configuração:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Subconfigurações (uma configuração aninhada em uma configuração) são suportadas para uso com Fragmentos de conteúdo, mas não podem ser usadas para consultas GraphQL.

1. Navegue até **Ferramentas**, **Gerale** abra o **Navegador de configuração**.

1. Use **Criar** para abrir a caixa de diálogo, onde você:

   1. Especifique um **Título**.
   1. Para permitir seu uso, selecione
      * **Modelos de fragmentos do conteúdo**
      * **Consultas persistentes de GraphQL**

      ![Definir configuração](assets/cfm-conf-01.png)


1. Selecionar **Criar** para salvar a definição.

<!-- 1. Select the location appropriate to your website. -->

### Aplicar a configuração à sua pasta de ativos {#apply-the-configuration-to-your-assets-folder}

Quando a configuração **global** estiver ativado para a funcionalidade de fragmento de conteúdo, então se aplica a qualquer pasta de Ativos.

Para usar outras configurações (ou seja, excluindo globais) com uma pasta do Assets comparável, é necessário definir a conexão. Isso é feito ao selecionar a **Configuração** apropriada na guia **Serviços da nuvem** das **Propriedades da pasta** da pasta apropriada.

![Aplicar configuração](assets/cfm-conf-02.png)
