---
title: Adicionar marca d'água aos seus ativos digitais
description: Saiba como usar o recurso Marca d'água para adicionar uma marca d'água digital aos ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Aplicação de marca d&#39;água {#watermarking}

O recurso de Marca d&#39;água nos ativos Adobe Experience Manager (AEM) permite que você adicione uma marca d&#39;água digital aos ativos, o que ajuda os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. O AEM Assets oferece suporte para texto a ser usado como marca d&#39;água em arquivos PNG e JPEG.

Para poder aplicar marca d&#39;água em ativos, adicione a etapa Marca d&#39;água no fluxo de trabalho Atualizar ativo do DAM.

1. Toque/clique no logotipo do AEM e vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos de fluxo de trabalho, selecione o fluxo de trabalho **[!UICONTROL Atualizar ativo]** DAM e clique em **[!UICONTROL Editar]**.

1. No painel lateral, arraste a etapa **[!UICONTROL Adicionar marca d&#39;água]** para o fluxo de trabalho Atualizar ativo do DAM.

<!--  ![Darg add watermark step in the DAM update asset workflow](assets/add_watermark_step_aem_assets.png) -->

>[!NOTE]
>
>Coloque a etapa Adicionar marca d&#39;água em qualquer lugar antes da etapa Processar miniatura.

1. Abra a etapa **[!UICONTROL Adicionar marca d&#39;água]** para exibir suas propriedades.
1. Na guia **[!UICONTROL Argumentos]** , especifique valores válidos nos vários campos, incluindo texto, tipo de fonte, tamanho, cor, posição, orientação e assim por diante. Para confirmar as alterações, toque/clique no ícone Concluído.

<!--   ![Provide the arguments in the add watermark step in Assets](assets/arguments_add_watermark_aem_assets.png) -->

1. Salve o fluxo de trabalho do Ativo **[!UICONTROL de atualização do]** DAM com a etapa Marca d&#39;água.
1. Na interface do usuário Ativos, faça upload de um ativo de amostra. A marca d&#39;água é exibida com o tamanho da fonte, a cor e assim por diante, na posição configurada nas etapas acima.
