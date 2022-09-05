---
title: Fragmentos de conteúdo - Navegador de configuração (Ativos - Fragmentos de conteúdo)
description: Saiba como ativar determinadas funcionalidades de Fragmento de conteúdo no Navegador de configuração para aproveitar AEM poderosos recursos de entrega sem cabeçalho.
feature: Content Fragments
role: User
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: 21ee6ec3ffef602bfbac7d89bb6c3454869deda9
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Fragmentos de conteúdo — Navegador de configuração{#content-fragments-configuration-browser}

Saiba como ativar determinadas funcionalidades de Fragmento de conteúdo no Navegador de configuração para aproveitar AEM poderosos recursos de entrega sem cabeçalho.

## Ativar a funcionalidade de fragmento de conteúdo para sua instância {#enable-content-fragment-functionality-instance}

Antes de usar fragmentos de conteúdo, você precisa usar o **navegador de configuração** para ativar:

* **Modelos de fragmentos de conteúdo** (obrigatório)
* **Consultas Persistentes GraphQL** - opcional

>[!CAUTION]
>
>Se você não ativar os **modelos de fragmentos de conteúdo**:
>
>* a opção **Criar** não estará disponível para criar novos modelos.
>* você não poderá [selecionar a configuração de sites para criar o ponto de acesso relacionado](/help/headless/graphql-api/graphql-endpoint.md).


Para ativar a funcionalidade do fragmento de conteúdo, é necessário:

* Ativar o uso da funcionalidade de fragmento de conteúdo por meio do navegador de configuração
* Aplicar a configuração à sua pasta de ativos

### Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração {#enable-content-fragment-functionality-in-configuration-browser}

Para [usar determinadas funcionalidades do fragmento de conteúdo](#creating-a-content-fragment-model), primeiro é **necessário** habilitá-las por meio do **navegador de configuração**:

>[!NOTE]
>
>Para obter mais detalhes, consulte também [Navegador de configuração:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Subconfigurações](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (uma configuração aninhada em outra configuração) são totalmente compatíveis com o uso de fragmentos de conteúdo, modelos de fragmento de conteúdo e consultas GraphQL.
>
>Apenas observe que:
>
>
>* Depois de criar modelos em uma subconfiguração, NÃO é possível mover ou copiar o modelo para outra subconfiguração.
>
>* Um ponto de acesso de GraphQL (ainda) será baseado em uma configuração principal (raiz).
>
>* As consultas persistentes (ainda) serão salvas relativas à configuração principal (raiz).



1. Navegue até **Ferramentas**, **Geral**, e abra o **Navegador de configuração**.

1. Selecione **Criar** para abrir a caixa de diálogo, onde você:

   1. Especifica um **Título**.
   1. O **Nome** se tornará o nome do nó no repositório.
      * Ele será gerado automaticamente com base no título e ajustado de acordo com as [convenções de nomenclatura do AEM.](/help/implementing/developing/introduction/naming-conventions.md)
      * Pode ajustá-lo se necessário.
   1. Para permitir seu uso, selecione
      * **Modelos de fragmentos do conteúdo**
      * **Consultas GraphQL Persistidas**

      ![Definir configuração](assets/cfm-conf-01.png)


1. Selecione **Criar** para salvar a definição.

<!-- 1. Select the location appropriate to your website. -->

### Aplicar a configuração à sua pasta de ativos {#apply-the-configuration-to-your-assets-folder}

Quando a configuração **global** estiver ativado para a funcionalidade de fragmento de conteúdo, então se aplica a qualquer pasta de Ativos.

Para usar outras configurações (ou seja, excluindo globais) com uma pasta do Assets comparável, é necessário definir a conexão. Isso é feito ao selecionar a **Configuração** apropriada na guia **Serviços da nuvem** das **Propriedades da pasta** da pasta apropriada.

![Aplicar configuração](assets/cfm-conf-02.png)
