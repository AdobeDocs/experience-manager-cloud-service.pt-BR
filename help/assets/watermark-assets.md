---
title: Marcar os ativos como uma marca d'água
description: Adicione uma marca d'água aos seus ativos digitais.
contentOwner: AG
feature: Gerenciamento de ativos,Publicação
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Marque seus ativos com água {#watermark-assets}

[!DNL Adobe Experience Manager Assets] permite adicionar uma marca d&#39;água digital a imagens. [!DNL Assets] O suporta a aplicação de uma imagem como marca d&#39;água a outros arquivos de imagem. As marcas d&#39;água podem ajudar os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. Além disso, uma marca d&#39;água pode ser usada para indicar o estado de um documento como confidencial, rascunho, validade e assim por diante.

Para configurar [!DNL Experience Manager] para criar ativos de marca d&#39;água, siga estas etapas:

1. Um arquivo PNG é aplicado como uma marca d&#39;água. Faça upload desse arquivo no repositório DAM.

1. Acesse o repositório Git [!DNL Cloud Manager] associado ao seu ambiente. Confirme um arquivo chamado `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` no repositório com o seguinte conteúdo. Para obter instruções, consulte [como fazer a configuração OSGi em [!DNL Experience Manager] como um [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [Crie um ](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) perfil de processamento para aproveitar os microsserviços de ativos para aplicar a marca d&#39;água.

   ![Perfil de processamento de ativos para criar marca d&#39;água](assets/watermark-processing-profile.png)

1. [Aplique os perfis de processamento a uma ](/help/assets/asset-microservices-configure-and-use.md#use-profiles) pasta para criar ativos com marca d&#39;água.

## Dicas e limitações {#tips-limitations-bestpractices}

* Você pode usar uma única configuração para marcar todos os ativos com marca d&#39;água. Apenas uma imagem é usada para marca d&#39;água e sua largura é fixa.
* Você pode colocar a marca d&#39;água no centro sem fazer o encaixe.
* Marcas d&#39;água baseadas em texto não são compatíveis.

>[!MORELIKETHIS]
>
>* [Visão geral dos microsserviços de ativos](/help/assets/asset-microservices-overview.md).
>* [Use microsserviços de ativos com perfis](/help/assets/asset-microservices-configure-and-use.md) de processamento.

