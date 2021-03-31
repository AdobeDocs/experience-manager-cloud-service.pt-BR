---
title: Fragmentos de conteúdo - Navegador de configuração
description: Saiba como ativar determinadas funcionalidades de Fragmento de conteúdo no Navegador de configuração para aproveitar AEM poderosos recursos de entrega sem cabeçalho.
feature: Fragmentos de conteúdo
role: Profissional
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 20%

---


# Fragmentos de conteúdo - Navegador de configuração{#content-fragments-configuration-browser}

Saiba como ativar determinadas funcionalidades de Fragmento de conteúdo no Navegador de configuração para aproveitar AEM poderosos recursos de entrega sem cabeçalho.

## Ativar a funcionalidade de fragmento de conteúdo para sua instância {#enable-content-fragment-functionality-instance}

Antes de usar Fragmentos de conteúdo, você precisa usar o **Navegador de configuração** para ativar:

* **Modelos de fragmentos do conteúdo**  - obrigatório
* **Consultas**  persistentes GraphQL - opcional

>[!CAUTION]
>
>Se você não ativar **Modelos de fragmento de conteúdo** a opção **Criar** não estará disponível para criar novos modelos.

Para ativar a funcionalidade do fragmento de conteúdo, é necessário:

* Ativar o uso da funcionalidade de fragmento de conteúdo por meio do navegador de configuração
* Aplicar a configuração à sua pasta Ativos

### Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração {#enable-content-fragment-functionality-in-configuration-browser}

Para [usar determinada funcionalidade de Fragmento de conteúdo](#creating-a-content-fragment-model) você **deve** primeiro ativá-los por meio do **Navegador de configuração**:

>[!NOTE]
>
>Para obter mais detalhes, consulte também [Navegador de configuração:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!CAUTION]
>
>Subconfigurações (uma configuração aninhada em uma configuração) não são compatíveis com o Fragmentos de conteúdo.

1. Navegue até **Ferramentas**, **Gerale** abra o **Navegador de configuração**.

1. Use **Criar** para abrir a caixa de diálogo, onde você:

   1. Especifique um **Título**.
   1. Para permitir seu uso, selecione
      * **Modelos de fragmentos do conteúdo**
      * **Consultas Persistentes GraphQL**

      ![Definir configuração](assets/cfm-conf-01.png)


1. Selecione **Create** para salvar a definição.

<!-- 1. Select the location appropriate to your website. -->

### Aplique a configuração à sua pasta de ativos {#apply-the-configuration-to-your-assets-folder}

Quando a configuração **global** está ativada para a funcionalidade do fragmento de conteúdo, então se aplica a qualquer pasta de Ativos.

Para usar outras configurações (ou seja, excluindo globais) com uma pasta do Assets comparável, é necessário definir a conexão. Isso é feito ao selecionar a **Configuração** apropriada na guia **Serviços da nuvem** das **Propriedades da pasta** da pasta apropriada.

![Aplicar configuração](assets/cfm-conf-02.png)