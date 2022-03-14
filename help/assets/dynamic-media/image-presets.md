---
title: Aplicar predefinições de imagem do Dynamic Media
description: Saiba como aplicar predefinições de imagens no Dynamic Media.
feature: Image Presets,Viewers,Renditions
role: User
exl-id: ad21b52e-594f-4421-9b5a-2382d032ec5a
source-git-commit: 1d42305b6a597dc95bff8b34eee8279eb0e511f3
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 7%

---

# Aplicar predefinições de imagem do Dynamic Media {#applying-image-presets}

As predefinições de imagens permitem que os ativos forneçam dinamicamente imagens de tamanhos diferentes, em formatos diferentes ou com outras propriedades de imagens que foram geradas dinamicamente. Você pode escolher uma predefinição ao exportar para reformatar imagens às especificações descritas pelo administrador.

Além disso, é possível escolher uma predefinição de imagem responsiva (designada pela variável **[!UICONTROL RESS]** depois de selecioná-lo).

[Os administradores podem criar e configurar predefinições de imagens](managing-image-presets.md).

>[!NOTE]
>
>A geração de imagens inteligentes funciona com as predefinições de imagens existentes. Ele usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade de conexão do navegador ou da rede. Consulte [Imagem inteligente](imaging-faq.md) para obter mais informações.

Você pode aplicar uma predefinição de imagem a uma imagem sempre que visualizá-la.

**Para aplicar as predefinições da imagem do Dynamic Media:**

1. Abra o ativo e, no painel à esquerda, selecione a lista suspensa e selecione **[!UICONTROL Representações]**.

   >[!NOTE]
   >
   >* As representações estáticas são exibidas na metade superior do painel. As representações dinâmicas aparecem na metade inferior. Com representações dinâmicas somente, você pode usar o URL para exibir a imagem. O **[!UICONTROL URL]** somente será exibido se você selecionar uma representação dinâmica. O **[!UICONTROL RESS]** só será exibido se você selecionar uma predefinição de imagem responsiva.
   >
   >* O sistema mostra várias representações ao selecionar **[!UICONTROL Representações]** na exibição Detalhes de um ativo. Você pode aumentar o número de predefinições vistas. Consulte [Aumento do número de predefinições de imagens exibidas](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Siga um destes procedimentos:

   * Para visualizar a predefinição de imagem, selecione uma representação dinâmica.
   * Para exibir a janela pop-up, selecione **[!UICONTROL URL]**, **[!UICONTROL Incorporar]** ou **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Se o ativo *e* a predefinição de imagem ainda não foi publicada, a variável **[!UICONTROL URL]** (ou botões URL e RESS, se aplicável) não estiverem disponíveis.
   >
   >Observe também que as predefinições de imagens são publicadas automaticamente em um servidor Dynamic Media S7.
