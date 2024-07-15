---
title: Como configurar uma página de redirecionamento?
description: Saiba como os usuários podem ser redirecionados para uma página da Web que os autores de formulários podem configurar ao criar o formulário.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 6%

---

# Configuração da página de redirecionamento {#configuring-redirect-page}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-redirect-page.html) |
| AEM as a Cloud Service | Este artigo |

Os autores de formulários podem configurar uma página para cada formulário, para a qual os usuários são redirecionados após enviarem um formulário.

1. No modo de edição, selecione um componente e clique em ![nível do campo](assets/select_parent_icon.svg) > **[!UICONTROL Contêiner de formulário adaptável]** e clique em ![cmppr](assets/configure-icon.svg).

1. Na barra lateral, clique em **[!UICONTROL Envio]**.

1. Forneça a URL da página de redirecionamento em **[!UICONTROL Redirecionar URL/Caminho]** na seção **[!UICONTROL Envio]**.
1. Como opção, em Enviar ação, para a ação de endpoint Enviar para REST, é possível configurar o parâmetro a ser transmitido para a página de redirecionamento.

   ![Redirecionar configuração de página](assets/redirect-url.png)

   Redirecionar configuração de página

Os autores de formulário podem usar os seguintes parâmetros que são passados para a página Thank you. Para todas as Ações de Envio disponíveis, `status` e `owner` parâmetros são passados. Além desses dois parâmetros, alguns parâmetros adicionais são transmitidos para as seguintes Ações de envio:

* **[!UICONTROL Enviar para ponto de extremidade REST]**: os parâmetros adicionados para o campo ao mapeamento de parâmetros são passados. Os parâmetros `status` e `owner` não são passados nesta Ação de Envio. Para obter mais informações, consulte [Configurando a Ação de Envio de Enviar para ponto de extremidade REST](configuring-submit-actions.md).

>[!MORELIKETHIS]
>
>* [Configurar uma página de redirecionamento ou uma mensagem de agradecimento](/help/forms/configure-redirect-page-or-thank-you-message.md)
