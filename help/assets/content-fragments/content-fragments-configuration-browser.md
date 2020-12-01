---
title: Fragmentos de conteúdo - Navegador de configuração
description: Saiba como ativar determinadas funcionalidades do Fragmento de conteúdo no Navegador de configuração.
translation-type: tm+mt
source-git-commit: ae918d074d4bacfc207d4dca2c67f41a3118aff4
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 20%

---


# Fragmentos de conteúdo - Navegador de configuração{#content-fragments-configuration-browser}

>[!CAUTION]
>
>A API AEM GraphQL, para o Delivery de fragmento de conteúdo, será lançada no início de 2021.
>
>A documentação relacionada já está disponível para fins de pré-visualização.

## Ativar a funcionalidade de fragmento de conteúdo para sua instância {#enable-content-fragment-functionality-instance}

Antes de usar Fragmentos de conteúdo, você precisa usar o **Navegador de configuração** para ativar:

* **Modelos**  de fragmento de conteúdo - obrigatório
* **Query**  persistentes GraphQL - opcional

>[!CAUTION]
>
>Se você não ativar **Modelos de fragmento de conteúdo** a opção **Criar** não estará disponível para criar novos modelos.

Para ativar a funcionalidade do fragmento de conteúdo, é necessário:

* Habilitar o uso da funcionalidade de fragmento de conteúdo por meio do navegador de configuração
* Aplicar a configuração à pasta Ativos

### Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração {#enable-content-fragment-functionality-in-configuration-browser}

Para [utilizar determinadas funcionalidades do Fragmento de conteúdo](#creating-a-content-fragment-model) você **deve** primeiro ativá-las por meio do **Navegador de configuração**:

>[!NOTE]
>
>Para obter mais detalhes, consulte também [Navegador de configuração:](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

1. Navegue até **Ferramentas**, **Gerale** abra o **Navegador de configuração**.
2. Selecione o local apropriado para seu site.
3. Use **Criar** para abrir a caixa de diálogo, onde você:

   1. Especifique um **Título**.
   2. Para habilitar o uso, selecione
      * **Modelos de fragmentos do conteúdo**
      * **Query Persistentes GraphQL**

      ![Definir configuração](assets/cfm-conf-01.png)


4. Selecione **Criar** para guardar a definição.

### Aplicar a configuração à sua pasta Assets {#apply-the-configuration-to-your-assets-folder}

Quando a configuração **global** estiver ativada para a funcionalidade do fragmento do conteúdo, então se aplica a qualquer pasta Ativos.

Para usar outras configurações (ou seja, excluindo globais) com uma pasta do Assets comparável, é necessário definir a conexão. Isso é feito ao selecionar a **Configuração** apropriada na guia **Serviços da nuvem** das **Propriedades da pasta** da pasta apropriada.

![Aplicar configuração](assets/cfm-conf-02.png)