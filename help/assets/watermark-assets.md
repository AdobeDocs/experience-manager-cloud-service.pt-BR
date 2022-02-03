---
title: Marcar os ativos como uma marca d'água
description: Adicione uma marca d'água aos seus ativos digitais.
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 8f7dc67a8335822b51e4c7796ab55244199fb214
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Marque seus ativos com água {#watermark-assets}

[!DNL Adobe Experience Manager Assets] permite adicionar uma marca d&#39;água digital a imagens. [!DNL Assets] O suporta a aplicação de uma imagem como marca d&#39;água a outros arquivos de imagem. As marcas d&#39;água podem ajudar os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. Além disso, uma marca d&#39;água pode ser usada para indicar o estado de um documento como confidencial, rascunho, validade e assim por diante.

>[!NOTE]
>
>Esse recurso está disponível no canal de pré-lançamento. Consulte [Documentação do Canal de pré-lançamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#enable-prerelease) para obter informações sobre como habilitar o recurso para seu ambiente.

Para configurar [!DNL Experience Manager] para adicionar ativos de marca d&#39;água:

1. Um arquivo PNG é aplicado como uma marca d&#39;água. Faça upload desse arquivo para seu repositório DAM.

1. Navegar para **[!UICONTROL Ferramentas > Ativos > Configurações de ativos]**.

1. Clique em **[!UICONTROL Perfil de marca d&#39;água do sistema]**.

1. No [!UICONTROL Página Perfil de marca d&#39;água do sistema], especifique o caminho da imagem carregada no repositório DAM na etapa 1.

1. Especifique a escala da marca d&#39;água, que varia de 0,0 a 1,0, em relação à largura da representação, na variável **[!UICONTROL Escala]** campo.

1. Clique em **[!UICONTROL Salvar]**.

   ![Detector de duplicação de ativo](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >Se você configurou o Perfil de marca d&#39;água do sistema usando `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` arquivo de configuração (configuração OSGi), você pode continuar a usá-lo, no entanto, o Adobe recomenda usar o novo método.


1. [Criar um perfil de processamento](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) utilizar os microsserviços de ativos para aplicar a marca d&#39;água.

   ![Perfil de processamento de ativos para criar marca d&#39;água](assets/watermark-processing-profile.png)

   Certifique-se de ativar a variável **[!UICONTROL Marca d&#39;água]** alternar ao criar o perfil de processamento.

1. [Aplicar os perfis de processamento a uma pasta](/help/assets/asset-microservices-configure-and-use.md#use-profiles) para criar ativos com marca d&#39;água.

## Dicas e limitações {#tips-limitations-bestpractices}

* Você pode usar uma única configuração para marcar todos os ativos com marca d&#39;água. Apenas uma imagem é usada para marca d&#39;água e sua largura é fixa.
* Você pode colocar a marca d&#39;água no centro sem fazer o encaixe.
* Marcas d&#39;água baseadas em texto não são compatíveis.

>[!MORELIKETHIS]
>
>* [Visão geral dos microsserviços de ativos](/help/assets/asset-microservices-overview.md).
>* [Usar microsserviços de ativos com perfis de processamento](/help/assets/asset-microservices-configure-and-use.md).

