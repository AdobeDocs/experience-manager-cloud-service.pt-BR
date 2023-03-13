---
title: Aplicar predefinições de imagem do Dynamic Media
description: Saiba como aplicar predefinições de imagem no Dynamic Media.
contentOwner: Rick Brough
feature: Image Presets,Viewers,Renditions
role: User
exl-id: ad21b52e-594f-4421-9b5a-2382d032ec5a
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 7%

---

# Aplicar predefinições de imagem do Dynamic Media {#applying-image-presets}

As Predefinições de imagem permitem que os ativos forneçam imagens dinamicamente em diferentes tamanhos, em diferentes formatos ou com outras propriedades de imagem que são geradas dinamicamente. Ao exportar, é possível escolher uma predefinição para reformatar imagens para as especificações descritas pelo administrador.

Além disso, é possível escolher uma predefinição de imagem que seja responsiva (designada pelo **[!UICONTROL RESS]** após selecioná-lo).

[Os administradores podem criar e configurar predefinições de imagens](managing-image-presets.md).

>[!NOTE]
>
>As imagens inteligentes funcionam com as predefinições de imagens existentes. Ele usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Imagem inteligente](imaging-faq.md) para obter mais informações.

É possível aplicar uma predefinição de imagem a uma imagem sempre que ela for visualizada.

**Para aplicar Predefinições de imagem do Dynamic Media:**

1. Abra o ativo e, no painel à esquerda, selecione a lista suspensa e **[!UICONTROL Representações]**.

   >[!NOTE]
   >
   >* As representações estáticas aparecem na metade superior do painel. As representações dinâmicas aparecem na metade inferior. Somente com representações dinâmicas, é possível usar o URL para exibir a imagem. A variável **[!UICONTROL URL]** será exibido somente se você selecionar uma representação dinâmica. A variável **[!UICONTROL RESS]** O botão só será exibido se você selecionar uma predefinição de imagem responsiva.
   >
   >* O sistema mostra várias execuções ao selecionar **[!UICONTROL Representações]** na exibição de Detalhes de um ativo. Você pode aumentar o número de predefinições vistas. Consulte [Aumentar o número de predefinições de imagens exibidas](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).


   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Siga um destes procedimentos:

   * Para visualizar a predefinição da imagem, selecione uma representação dinâmica.
   * Para exibir a janela pop-up, selecione **[!UICONTROL URL]**, **[!UICONTROL Incorporar]** ou **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Se o ativo *e* a predefinição de imagem ainda não foi publicada, a variável **[!UICONTROL URL]** botão (ou botões URL e RESS, se aplicável) não está disponível.
   >
   >Observe também que as predefinições de imagem são publicadas automaticamente em um servidor Dynamic Media S7.
