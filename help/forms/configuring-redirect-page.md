---
title: Como configurar uma página de redirecionamento?
description: Saiba como os usuários podem ser redirecionados para uma página da Web que os autores de formulários podem configurar ao criar o formulário.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: e4dc01d2-7c89-4bd8-af0a-1d2df4676a9a
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Configuração da página de redirecionamento {#configuring-redirect-page}

Os autores de formulários podem configurar uma página para cada formulário, para a qual os usuários são redirecionados após enviarem um formulário.

1. No modo de edição, selecione um componente e clique em ![nível de campo](assets/select_parent_icon.svg) > **[!UICONTROL Contêiner de formulário adaptável]** e clique em ![cmppr](assets/configure-icon.svg).

1. Na barra lateral, clique em **[!UICONTROL Envio]**.

1. Forneça o URL da página de redirecionamento em **[!UICONTROL URL/caminho de redirecionamento]** no **[!UICONTROL Envio]** seção.
1. Como opção, em Enviar ação, para a ação de endpoint Enviar para REST, é possível configurar o parâmetro a ser transmitido para a página de redirecionamento.

   ![Redirecionar configuração de página](assets/redirect-url.png)

   Redirecionar configuração de página

Os autores de formulário podem usar os seguintes parâmetros que são passados para a página Thank you. Para todas as ações enviar disponíveis, `status` e `owner` parâmetros são transmitidos. Além desses dois parâmetros, alguns parâmetros adicionais são transmitidos para as seguintes Ações de envio:

* **[!UICONTROL Enviar para endpoint REST]**: os parâmetros adicionados para o mapeamento no campo para o parâmetro são transmitidos. `status` e `owner` Os parâmetros do não são transmitidos nesta Ação de envio. Para obter mais informações, consulte [Configuração da ação enviar Enviar para endpoint REST](configuring-submit-actions.md).
