---
title: Como configurar uma página de redirecionamento ou uma mensagem de agradecimento?
description: Saiba como os usuários podem exibir uma mensagem de agradecimento ou ser redirecionados para uma página da Web que os autores de formulários podem configurar ao criar o formulário.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
source-git-commit: 87650caea6eb907093f0f327f1dbc19641098e4a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Configurar Redirecionamento ou Mensagem de Agradecimento

Em formulários criados usando o Editor universal, os autores de formulários podem configurar o que acontece depois que um usuário envia um formulário. Você pode exibir uma mensagem de agradecimento ou redirecionar o usuário para uma página da Web específica usando a guia Envio na extensão Editar propriedades do formulário.

É possível configurar a mensagem de agradecimento ou as URLs de redirecionamento para formulários criados no Editor Universal usando a guia **Envio** da extensão **Propriedades do Formulário AEM**.

## Pré-requisitos

É possível configurar a ação de envio para formulários criados no Universal Editor usando a guia **Envio** da extensão **Editar Propriedades do Formulário**.

![Ícone de propriedades do formulário](/help/forms/assets/ue-form-properties-icon.png)

![Propriedades de Formulário do Editor Universal](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> * Se você não vir o ícone **Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** no Extension Manager.
> * Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.

## Como configurar o redirecionamento ou a mensagem de agradecimento?

No envio de um formulário, você pode redirecionar o usuário para outra página da Web ou mostrar uma mensagem.

Para configurar a página de redirecionamento ou a mensagem de agradecimento:

1. Abra o Formulário adaptável para edição.
2. Abra a Árvore de conteúdo e selecione o **[!UICONTROL Contêiner do guia]**.
3. Clique no ícone de propriedades do Contêiner de formulário adaptável ![propriedades do Contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável para configurar os Modelos de dados é aberta.
4. Abra a guia **[!UICONTROL Envio]**. As opções para configurar uma página de redirecionamento ou uma mensagem são exibidas:

   ![Caixa de diálogo de envio do Contêiner do Guia para configurar uma página de redirecionamento ou uma mensagem](/help/forms/assets/adaptive-forms-core-components-redirect-page-or-thank-you-message.png)

**Configurar URLs de Redirecionamento**

* Para configurar uma URL de Redirecionamento, para a opção Enviar, selecione a **[!UICONTROL opção Redirecionar para URL]** e forneça um endereço absoluto, uma URL de Redirecionamento ou um caminho relativo de uma página do AEM Sites.

![redirecionar](/help/edge/docs/forms/universal-editor/assets/redirect-ue.png)

**Configurar mensagem de agradecimento**

* Para configurar uma mensagem personalizada ou de agradecimento, selecione a opção **[!UICONTROL Mostrar Mensagem]** e forneça uma mensagem na caixa Conteúdo da mensagem. É uma caixa de rich text, você pode usar a opção de tela cheia para exibir todos os itens de rich text disponíveis.

![obrigado](/help/edge/docs/forms/universal-editor/assets/thankyou-ue.png)

Os autores de formulários podem configurar uma página para cada formulário, para a qual os usuários são redirecionados após enviarem um formulário.
