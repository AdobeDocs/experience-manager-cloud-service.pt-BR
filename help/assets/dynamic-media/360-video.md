---
title: Vídeo 360/VR
description: Saiba como trabalhar com o 360 e o Vídeo Virtual Reality (VR) na Dynamic Media.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Vídeo 360/VR {#vr-video}

Os vídeos de 360 graus gravam uma visualização em todas as direções ao mesmo tempo. Eles são filmados usando uma câmera onidirecional ou uma coleção de câmeras. Durante a reprodução num visor plano, o utilizador controla o ângulo de visualização; a reprodução em dispositivos móveis normalmente aproveita seus controles giroscópicos incorporados.

O Dynamic Media inclui suporte nativo para a entrega de 360 ativos de vídeo. Por padrão, nenhuma configuração adicional é necessária para exibir ou reproduzir. Você fornece 360 vídeos usando extensões de vídeo padrão, como .mp4, .mkv e .mov. O codec mais comum é H.264.

Esta seção descreve como trabalhar com o visualizador de vídeo 360/VR para renderizar vídeos necessários para uma experiência de visualização imersiva de uma sala, propriedade, local, paisagem, procedimento médico e assim por diante.

Não há suporte para áudio espacial no momento; se o áudio estiver misturado em estéreo, o equilíbrio (L/R) não é alterado à medida que o cliente altera o ângulo de visualização da câmera.

Consulte [Usar vídeos do Dynamic Media 360 e miniatura de vídeo personalizado com ativos](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html)AEM.

See also [Managing Viewer Presets](/help/assets/dynamic-media/managing-viewer-presets.md).

## 360 Vídeo em ação {#video-in-action}

Toque em [Space Station 360](http://mobiletest.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) para abrir uma janela do navegador e assistir a um vídeo de 360 graus. Durante a reprodução do vídeo, arraste o ponteiro do mouse para um novo local para alterar o ângulo de visualização.

![360 Exemplo](assets/6_5_360videoiss_simplified.png)de quadro de *vídeo da Estação Espacial 360*

## Vídeo 360/VR e Adobe Premiere Pro {#vr-video-and-adobe-premiere-pro}

Você pode usar o Adobe Premier Pro para exibir e editar imagens 360/VR. Por exemplo, você pode colocar logotipos e texto corretamente em uma cena e aplicar efeitos e transições projetados especificamente para mídia retangular.

Consulte [Editar vídeo](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html)360/VR.

## Fazer upload de ativos para uso com o visualizador de vídeo 360 {#uploading-assets-for-use-with-the-video-viewer}

Os ativos de vídeo 360 que são carregados no AEM são rotulados como **Multimídia** em uma página Ativo, similar ao ativo de vídeo normal.

![6_5_360video-select-preview](assets/6_5_360video-selecttopreview.png)*Um ativo de vídeo 360 carregado visto na exibição Cartão. O ativo é rotulado como Multimídia.*

**Para carregar ativos para uso com o visualizador de vídeo 360:**

1. Criada uma pasta dedicada ao seu ativo de vídeo 360.
1. [Aplique um perfil de vídeo adaptável à pasta](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   A renderização de conteúdo de vídeo 360 coloca requisitos mais altos para a resolução de vídeo de origem e para a resolução de execuções codificadas do que o conteúdo de vídeo padrão não-360.

   Você pode usar o Perfil de vídeo adaptativo pronto para uso que já vem com a Mídia dinâmica. No entanto, lembre-se de que isso resultará em uma qualidade de vídeo 360 nitidamente menor do que a obtida para vídeos não-360 codificados com as mesmas configurações renderizadas com um visualizador de vídeo não-360. Portanto, se for necessário um vídeo 360 de alta qualidade, faça o seguinte:

   * Idealmente, seu conteúdo original de vídeo 360 deve ter uma das seguintes resoluções:

      * 1080p - 1920 x 1080, conhecida como resolução Full HD ou FHD ou
      * 2160p - 3840 x 2160, conhecida como resolução 4K, UHD ou Ultra HD. Essa resolução de tela muito grande é encontrada na maioria das vezes em televisores premium e monitores de computador. A resolução 2160p é frequentemente chamada de &quot;4K&quot; porque a largura é próxima a 4000 pixels. Em outras palavras, oferece quatro vezes mais pixels do que 1080p.
   * [Crie um perfil](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) de vídeo adaptativo personalizado com execuções de qualidade superior. Por exemplo, você pode criar um Perfil de vídeo adaptativo que contenha as três configurações a seguir:

      * width=auto; height=720; bitrate=2500 kbps
      * width=auto; height=1080; bitrate=5000 kbps
      * width=auto; height=1440; bitrate=6600 kbps
   * Processa o conteúdo de vídeo 360 em uma pasta dedicada exclusivamente a 360 ativos de vídeo.
   Esteja ciente de que essa abordagem também exigirá mais demandas na rede e na CPU do usuário final.

1. [Carregue seu vídeo na pasta](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).

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

## Previewing 360 Video {#previewing-video}

Você pode usar a opção Visualizar para ver a aparência do seu vídeo 360 para os clientes e garantir que ele esteja se comportando como esperado.

Consulte também [Edição de predefinições](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets)do visualizador.

Quando estiver satisfeito com o vídeo 360, você poderá publicá-lo.

Consulte [Incorporação do visualizador de vídeo ou imagem em uma página](/help/assets/dynamic-media/embed-code.md)da Web.
See [Linking URLs to your web application](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). Observe que o método baseado em URL de vinculação não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.
See [Adding Dynamic Media Assets to pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**Para visualizar vídeos 360**

1. Em **[!UICONTROL Ativos]**, navegue até um vídeo 360 existente que você criou. Toque no ativo 360 Video para abri-lo no modo de visualização.

   ![6_5_360video-select, preview-1](assets/6_5_360video-selecttopreview-1.png)

   Toque no ativo de vídeo 360 para visualizar o vídeo.

1. Na página de visualização, próximo ao canto superior esquerdo da página, toque na lista suspensa e selecione **[!UICONTROL Visualizadores]**.

   ![6_5_360visualizadores-visualização de vídeo](assets/6_5_360video-preview-viewers.png)

   Na lista Visualizadores, toque em **[!UICONTROL Video360_social]** e execute um dos procedimentos a seguir:

   * Arraste o ponteiro do mouse pelo vídeo para alterar o ângulo de visualização da cena estática.
   * Toque no botão **[!UICONTROL Reproduzir]** do vídeo para iniciar a reprodução; à medida que o vídeo é reproduzido, arraste o ponteiro do mouse pelo vídeo para alterar seu ângulo de visualização.
   ![Captura de tela de vídeo 6_5_360video-preview-video360-](assets/6_5_360video-preview-video360-social.png)*socialA 360.*

   * Na lista Visualizadores, toque em **[!UICONTROL Video360VR]**.

      O vídeo Virtual Reality (VR) é um conteúdo de vídeo imersivo que é acessado através do uso de headsets de realidade virtual. Assim como acontece com os vídeos comuns, você cria vídeos VR no início quando um vídeo está sendo gravado ou capturado com câmeras de vídeo de 360 graus.
   ![6_5_360video-preview-video360vr](assets/6_5_360video-preview-video360vr.png)
   *Uma imagem de vídeo de 360 VR.*

1. Near the upper-right of the preview page, tap **[!UICONTROL Close]**.

## Publicação de vídeo 360 {#publishing-video}

Você precisa publicar o vídeo 360 para usá-lo. A publicação de um vídeo 360 ativa o URL e o código incorporado. Ele também publica o vídeo 360 na nuvem Dynamic Media, que é integrada a um CDN para fornecimento escalável e de desempenho.

Consulte [Publicação de ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) de mídia dinâmica para obter detalhes sobre como publicar vídeos 360.
Consulte também [Incorporação do visualizador de vídeo ou imagem em uma página](/help/assets/dynamic-media/embed-code.md)da Web.
Consulte também [Vincular URLs ao aplicativo](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)da Web. Observe que o método baseado em URL de vinculação não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.
See also [Adding Dynamic Media Assets to pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
