---
title: Marque com água seus ativos
description: Adicione uma marca d'água aos seus ativos digitais.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a9ebb97541b44140d0155bcfa5d0228c79dbffec
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Marque com água seus ativos {#watermark-assets}

[!DNL Adobe Experience Manager Assets] permite que você adicione uma marca d&#39;água digital a imagens. [!DNL Assets] suporta a aplicação de uma imagem como uma marca d&#39;água a outros arquivos de imagem. As marcas d&#39;água podem ajudar os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. Além disso, uma marca d&#39;água pode ser usada para indicar um documento como confidencial, rascunho, validade e assim por diante.

Para configurar ativos de Experience Manager para marca d&#39;água, siga estas etapas:

1. Um arquivo PNG é aplicado como uma marca d&#39;água. Carregue esse arquivo no repositório DAM.

1. Acesse o repositório Git do Cloud Manager associado ao seu ambiente. Confirme um arquivo nomeado `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.json` em seu repositório Git do Cloud Manager com o seguinte conteúdo. Para obter mais detalhes, consulte [como fazer a configuração de OSGi no Experience Manager como Cloud Service](/help/implementing/deploying/configuring-osgi.md).

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [Crie um perfil](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) de processamento para aproveitar os microserviços de ativos para aplicar a marca d&#39;água.

![Perfil de processamento de ativos para criar marca d&#39;água](assets/watermark-processing-profile.png)

1. [Aplique os perfis de processamento a uma pasta](/help/assets/asset-microservices-configure-and-use.md#use-profiles) para criar ativos com marca d&#39;água.

## Dicas e limitações {#tips-limitations-bestpractices}

* Você pode usar uma única configuração para marcar a água de todos os seus ativos. Apenas uma imagem é usada para marca d&#39;água e sua largura é fixa.
* Você pode colocar a marca d&#39;água no centro sem fazer o encaixe.
* Marcas d&#39;água baseadas em texto não são suportadas.

>[!MORELIKETHIS]
>
>* [Visão geral](/help/assets/asset-microservices-overview.md)dos microserviços de ativos.
>* [Use microserviços de ativos com perfis](/help/assets/asset-microservices-configure-and-use.md)de processamento.

