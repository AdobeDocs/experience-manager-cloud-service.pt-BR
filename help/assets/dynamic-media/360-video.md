---
title: Vídeo 360/VR
description: Saiba como trabalhar com 360 e Vídeo de realidade virtual (VR) no Dynamic Media.
feature: Vídeo 360 VR
role: Business Practitioner
exl-id: ffd092d3-2188-47b0-a475-8bfa660c03c1
source-git-commit: 5e9cf9494ce9d54dd1d3b7818b3b975b2acb4e3c
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Vídeo 360/VR {#vr-video}

Vídeos de 360 graus gravam uma visualização em todas as direções ao mesmo tempo. Eles são filmados com uma câmera onidirecional ou com uma coleção de câmeras. Durante a reprodução, em uma tela plana, o usuário tem o controle do ângulo de visualização; a reprodução em dispositivos móveis geralmente aplica seus controles giroscópicos incorporados.

O Dynamic Media inclui suporte nativo para a entrega de 360 ativos de vídeo. Por padrão, nenhuma configuração adicional é necessária para visualizar ou reproduzir. Você fornece 360 vídeos usando extensões de vídeo padrão, como .mp4, .mkv e .mov. O codec mais comum é o H.264.

Você pode usar o visualizador de vídeo 360/VR para renderizar vídeos necessários. O resultado é uma experiência de visualização imersiva de uma sala, propriedade, localização, paisagem, procedimento médico e assim por diante.

Atualmente, não há suporte para áudio espacial; se o áudio estiver misturado em estéreo, o saldo (L/R) não muda conforme o cliente altera o ângulo de visualização da câmera.

Consulte [Usar vídeos do Dynamic Media 360 e miniatura de vídeo personalizado com AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html#dynamic-media).

Consulte também [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

## 360 Vídeo em ação {#video-in-action}

Selecione [Space Station 360](https://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) para abrir uma janela do navegador e assistir a um vídeo de 360 graus. Durante a reprodução do vídeo, arraste o ponteiro para um novo local para alterar o ângulo de exibição.

![360 ](assets/6_5_360videoiss_simplified.png)
*Exemplo de vídeoQuadro de vídeo da Estação Espacial 360*

## Vídeo 360/VR e Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Você pode usar o Adobe Premier Pro para exibir e editar imagens 360/VR. Por exemplo, você pode colocar logotipos e texto corretamente em uma cena e aplicar efeitos e transições projetadas especificamente para mídia Retangular.

Consulte [Editar vídeo 360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Fazer upload de ativos para usar com o visualizador de vídeo 360 {#uploading-assets-for-use-with-the-video-viewer}

360 ativos de vídeo que são enviados por upload para [!DNL Experience Manager] são rotulados como **Multimídia** em uma página de Ativo, semelhante ao ativo de vídeo normal.

![6_5_360video-](assets/6_5_360video-selecttopreview.png)
*selectUm ativo de vídeo 360 carregado e visualizado na exibição Cartão. O ativo é rotulado como Multimídia.*

**Faça upload de ativos para usar com o visualizador de vídeo 360:**

1. Criada uma pasta dedicada ao seu ativo de vídeo 360.
1. [Aplique um perfil de vídeo adaptável à pasta](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   A renderização do conteúdo de vídeo 360 coloca requisitos mais altos para a resolução de vídeo de origem e para as representações codificadas do que o conteúdo de vídeo não-360 padrão.

   Você pode usar o Perfil de vídeo adaptável pronto para uso que já vem com o Dynamic Media. No entanto, isso resulta em uma qualidade de vídeo 360 consideravelmente menor do que a obtida para vídeos não-360 codificados com as mesmas configurações renderizadas com um visualizador de vídeo não-360. Portanto, se for necessário vídeo de alta qualidade 360, faça o seguinte:

   * Idealmente, seu conteúdo original de vídeo 360 tem uma das seguintes resoluções:

      * 1080p - 1920 x 1080, conhecida como resolução Full HD ou FHD ou
      * 2160p - 3840 x 2160, conhecida como resolução 4k, UHD ou Ultra HD. Essa grande resolução de exibição é encontrada com mais frequência em televisores premium e monitores de computador. A resolução 2160p geralmente é chamada de &quot;4k&quot; porque a largura é próxima a 4000 pixels. Em outras palavras, ele oferece quatro vezes mais pixels do que 1080p.
   * [Crie um ](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) Perfil de vídeo adaptativo personalizado com representações de maior qualidade. Por exemplo, você pode criar um Perfil de vídeo adaptativo que contenha as três configurações a seguir:

      * Width=auto; Altura=720; Taxa de bits=2500 kbps
      * Width=auto; Altura=1080; Taxa de bits=5000 kbps
      * Width=auto; Altura=1440; Taxa de bits=6600 kbps
   * Processar o conteúdo de vídeo 360 em uma pasta dedicada exclusivamente a 360 ativos de vídeo.

   Essa abordagem coloca maiores demandas na rede e na CPU do usuário final.

1. [Faça upload do vídeo para a pasta](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) .

<!--

## Overriding the default aspect ratio of 360 videos  {#overriding-the-default-aspect-ratio-of-videos}

For an uploaded asset to qualify as a 360 video that you intend to use with the 360 Video viewer, the asset must have an aspect ratio of 2.

By default, AEM detects video as "360" if its aspect ratio (width/height) is 2.0. If you are an Administrator, you can override the default aspect ratio setting of 2 by setting the optional `s7video360AR` property in CRXDE Lite at the following:

* `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

  * **Property type**: Double
  * **Value**: floating-point aspect ratio, default 2.0.

After you set this property, it takes effect immediately on both existing videos and newly uploaded videos.

The aspect ratio applies to 360 video assets for the asset details page and the [Video 360 Media WCM component](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components).

Start by uploading 360 Videos.

-->

## Visualizar vídeo 360 {#previewing-video}

Você pode usar a opção Visualizar para ver como o vídeo 360 aparece para os clientes e garantir que ele esteja funcionando como esperado.

Consulte também [Editar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets).

Quando estiver satisfeito com o vídeo 360, você poderá publicá-lo.

Consulte [Incorporando o visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md).
Consulte [Vincular URLs ao aplicativo Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas [!DNL Experience Manager Sites].
Consulte [Adicionar ativos Dynamic Media às páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

**Para visualizar 360 vídeos:**

1. Em **[!UICONTROL Assets]**, navegue até um vídeo 360 existente que você criou. Para abri-lo no modo de visualização, selecione o ativo de Vídeo 360.

   ![6_5_360seleção de vídeo-visualização-1](assets/6_5_360video-selecttopreview-1.png)

   Para visualizar o vídeo, selecione o ativo de vídeo 360.

1. Na página de visualização, próximo ao canto superior esquerdo da página, selecione a lista suspensa e selecione **[!UICONTROL Visualizadores]**.

   ![6_5_360visualizadores de visualização de vídeo](assets/6_5_360video-preview-viewers.png)

   Na lista Visualizadores, selecione **[!UICONTROL Video360_social]** e siga um destes procedimentos:

   * Para alterar o ângulo de visualização da cena estática, arraste o ponteiro sobre o vídeo.
   * Para iniciar a reprodução, selecione o botão **[!UICONTROL Play]** do vídeo. Conforme o vídeo é reproduzido, arraste o ponteiro sobre o vídeo para alterar seu ângulo de exibição.

   ![Captura de tela de vídeo 6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360.*

   * Na lista Visualizadores, selecione **[!UICONTROL Video360VR]**.

      Vídeo VR (Virtual Reality) é um conteúdo de vídeo imersivo que é acessado usando fones de realidade virtual. Assim como em vídeos comuns, você cria vídeos VR no início quando um vídeo está sendo gravado ou capturado por meio de câmeras de vídeo de 360 graus.
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *Uma captura de tela de vídeo 360 VR.*

1. Próximo ao canto superior direito da página de visualização, selecione **[!UICONTROL Fechar]**.

## Publicação de vídeo 360 {#publishing-video}

Para usar o vídeo 360, você deve publicá-lo. A publicação de um vídeo 360 ativa o URL e o código incorporado. Ele também publica o vídeo 360 na nuvem do Dynamic Media, que é integrada a uma CDN para entrega escalável e com desempenho.

Consulte [Publicação de ativos Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar vídeo 360.
Consulte também [Incorporação do visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md).
Consulte também [Vincular URLs ao seu aplicativo Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas [!DNL Experience Manager Sites].
Consulte também [Adicionar ativos Dynamic Media às páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
