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

Os autores de formulários podem configurar uma página para cada formulário, para a qual os usuários do formulário são redirecionados após enviar um formulário.

1. No modo de edição, selecione um componente e clique em ![nível de campo](assets/select_parent_icon.svg) > **[!UICONTROL Contêiner de formulário adaptável]** e, em seguida, clique em ![cmppr](assets/configure-icon.svg).

1. Na barra lateral, clique em **[!UICONTROL Submissão]**.

1. Forneça o URL da página de redirecionamento em **[!UICONTROL Redirecionar URL/caminho]** no **[!UICONTROL Submissão]** seção.
1. Como opção, em Enviar ação, para a ação Enviar para o ponto de extremidade REST, você pode configurar o parâmetro a ser transmitido à página de redirecionamento.

   ![Redirecionar configuração da página](assets/redirect-url.png)

   Redirecionar configuração da página

Os autores de formulários podem usar os seguintes parâmetros passados para a página de agradecimento. Para todas as ações de envio disponíveis, `status` e `owner` parâmetros são passados. Além desses dois parâmetros, alguns parâmetros adicionais são passados para as seguintes Ações de envio:

* **[!UICONTROL Enviar para ponto de extremidade REST]**: Os parâmetros adicionados para mapeamento de parâmetro no campo são passados. `status` e `owner` parâmetros não são passados nesta Ação de envio. Para obter mais informações, consulte [Configuração da ação Enviar para o endpoint REST Enviar](configuring-submit-actions.md).
