---
title: Fragmentos de conteúdo - Navegador de configuração (Ativos - Fragmentos de conteúdo)
description: Saiba como ativar a funcionalidade de Fragmento de conteúdo no Navegador de configuração.
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 80%

---

# Fragmentos de conteúdo - Navegador de configuração{#content-fragments-configuration-browser}

Saiba como ativar determinadas funcionalidades do Fragmento de conteúdo no Navegador de configuração para usar recursos avançados de entrega headless AEM.

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
>Consulte [Navegador de configuração](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

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
      * Ele será gerado automaticamente com base no título e ajustado conforme as [convenções de nomenclatura do AEM](/help/implementing/developing/introduction/naming-conventions.md).
      * Você pode ajustá-lo se necessário.
   1. Para permitir seu uso, selecione
      * **Modelos de fragmentos do conteúdo**
      * **Consultas GraphQL persistidas**

      ![Definir configuração](assets/cfm-conf-01.png)

1. Selecione **Criar** para salvar a definição.

<!-- 1. Select the location appropriate to your website. -->

### Aplique a configuração à sua pasta de ativos {#apply-the-configuration-to-your-assets-folder}

Quando a configuração **global** está ativado para a funcionalidade de fragmento de conteúdo e se aplica a qualquer pasta de ativos.

Para usar outras configurações (com exceção da global) com uma pasta de ativos comparável, é necessário definir a conexão. Está conexão é feita ao selecionar a **configuração** apropriada na guia **Cloud Services** das **Propriedades da pasta** apropriada.

![Aplicar configuração](assets/cfm-conf-02.png)
