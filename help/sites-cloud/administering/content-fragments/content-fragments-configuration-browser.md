---
title: Fragmentos de conteúdo - Navegador de configuração
description: Saiba como habilitar a funcionalidade de fragmentos de conteúdo e GraphQL no navegador de configuração para utilizar os recursos de entrega headless do AEM.
feature: Content Fragments
role: User
hide: true
index: false
hidefromtoc: true
exl-id: 55d442ae-ae06-4dfa-8e4e-b415385ccea5
source-git-commit: 5ce5746026c5683e79cdc1c9dc96804756321cdb
workflow-type: ht
source-wordcount: '358'
ht-degree: 100%

---

# Fragmentos de conteúdo — Navegador de configuração{#content-fragments-configuration-browser}

<!--
hide: yes
index: no
hidefromtoc: yes
-->

Saiba como ativar funcionalidades específicas do fragmento de conteúdo no navegador de configuração.

## Ativar a funcionalidade de fragmento de conteúdo para sua instância {#enable-content-fragment-functionality-instance}

Antes de usar fragmentos de conteúdo, você deve usar o **navegador de configuração** para habilitar:

* **Modelos de fragmentos de conteúdo** (obrigatório)
* **Consultas GraphQL persistidas** - opcional

>[!CAUTION]
>
>Se você não habilitar os **modelos de fragmentos de conteúdo**:
>
>* a opção **Criar** não estará disponível para criar modelos.
>* não será possível [selecionar a configuração de sites para criar o ponto de acesso relacionado](/help/headless/graphql-api/graphql-endpoint.md).

Para habilitar a funcionalidade dos fragmentos de conteúdo, você deve fazer o seguinte:

* Ativar o uso da funcionalidade de fragmento de conteúdo por meio do navegador de configuração
* Aplicar a configuração à sua pasta de ativos

### Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração {#enable-content-fragment-functionality-in-configuration-browser}

Para usar determinadas [funcionalidades dos fragmentos de conteúdo](#creating-a-content-fragment-model), primeiro é **necessário** habilitá-las por meio do **navegador de configuração**:

>[!NOTE]
>
>Para obter mais detalhes, consulte [Navegador de configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[Subconfigurações](/help/implementing/developing/introduction/configurations.md#configuration-resolution) (uma configuração aninhada em outra configuração) são totalmente compatíveis com o uso de fragmentos de conteúdo, modelos de fragmento de conteúdo e consultas GraphQL.
>
>Apenas observe que:
>
>
>* Após criar modelos em uma subconfiguração, NÃO é possível mover ou copiar o modelo para outra subconfiguração.
>
>* Um ponto de acesso de GraphQL (ainda) será baseado em uma configuração principal (raiz).
>
>* As consultas persistentes (ainda) serão salvas relativas à configuração principal (raiz).


1. Navegue até **Ferramentas**, **Geral**, e abra o **Navegador de configuração**.

1. Selecione **Criar** para abrir a caixa de diálogo, onde você:

   1. Especifica um **Título**.
   1. O **Nome** se tornará o nome do nó no repositório.
      * Ele será gerado automaticamente com base no título e ajustado de acordo com as [convenções de nomenclatura do AEM](/help/implementing/developing/introduction/naming-conventions.md).
      * Você pode ajustá-lo se necessário.
   1. Para permitir seu uso, selecione
      * **Modelos de fragmentos do conteúdo**
      * **Consultas GraphQL persistidas**

      ![Definir configuração](assets/cfm-conf-01.png)

1. Selecione **Criar** para salvar a definição.

<!-- 1. Select the location appropriate to your website. -->

### Aplicar a configuração à sua pasta {#apply-the-configuration-to-your-folder}

Quando a configuração **global** estiver habilitada para a funcionalidade de fragmento de conteúdo, ela se aplicará a qualquer pasta de ativos que possa ser acessada por meio do console de **Ativos**.

Para usar outras configurações (com exceção da global) com uma pasta de ativos comparável, é necessário definir a conexão. Está conexão é feita ao selecionar a **configuração** apropriada na guia **Cloud Services** das **Propriedades da pasta** apropriada.

![Aplicar configuração](assets/cfm-conf-02.png)
