---
title: Fornecer imagens otimizadas para um site responsivo
description: Saiba como usar o recurso de código responsivo para fornecer imagens otimizadas do Dynamic Media.
feature: Gerenciamento de ativos
role: User
exl-id: 62af6f3f-9c86-44ad-870d-140f572f99c5
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 10%

---

# Fornecer imagens otimizadas para um site responsivo {#delivering-optimized-images-for-a-responsive-site}

Use o recurso de código responsivo quando quiser compartilhar o código para serviço responsivo com seu desenvolvedor da Web. Você copia o código responsivo (**[!UICONTROL RESS]**) para a área de transferência para compartilhá-lo com o desenvolvedor da Web.

Esse recurso faz sentido usar se o site estiver em um WCM de terceiros. No entanto, se seu site estiver no Adobe Experience Manager, um servidor de imagem externo renderiza a imagem e a fornece à página da Web.

Consulte também [Incorporar o visualizador de vídeo em uma página da Web](embed-code.md).

Consulte também [Vincular URLs ao seu aplicativo Web](linking-urls-to-yourwebapplication.md).

**Para fornecer imagens otimizadas para um site responsivo:**

1. Navegue até a imagem para a qual deseja fornecer o código responsivo e, no menu suspenso, selecione **[!UICONTROL Representações]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Selecione uma predefinição de imagem responsiva. Os botões **[!UICONTROL URL]** e **[!UICONTROL RESS]** são exibidos.

   ![chlimage_1-409](assets/chlimage_1-409.png)

   >[!NOTE]
   >
   >O ativo selecionado *e* a predefinição de imagem ou a predefinição do visualizador selecionado devem ser publicados para disponibilizar os botões **[!UICONTROL URL]** ou **[!UICONTROL RESS]**.
   >
   >As predefinições de imagens são publicadas automaticamente.

1. Selecione **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. Na caixa de diálogo **[!UICONTROL Incorporar imagem responsiva]**, selecione e copie o texto do código responsivo e o cole no site para acessar o ativo responsivo.
1. Edite os pontos de interrupção padrão no código incorporado para corresponder ao que é encontrado no site responsivo, diretamente no código. Além disso, teste as diferentes resoluções de imagem que estão sendo veiculadas em diferentes pontos de interrupção da página.

## Usar HTTP/2 para fornecer ativos da Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como os navegadores e servidores se comunicam. Ele oferece transferência mais rápida de informações e reduz a quantidade de poder de processamento necessário. A entrega de ativos do Dynamic Media é compatível com o uso do HTTP/2, o que oferece melhor resposta e tempos de carregamento.

Consulte [HTTP2 Delivery of Content](http2faq.md) para obter detalhes completos sobre como começar a usar HTTP/2 com sua conta Dynamic Media.
