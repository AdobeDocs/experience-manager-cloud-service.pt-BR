---
title: Vídeo 360/VR
description: Saiba como trabalhar com 360 e Vídeo de realidade virtual (VR) no Dynamic Media.
contentOwner: Rick Brough
feature: 360 VR Video
role: User
exl-id: ffd092d3-2188-47b0-a475-8bfa660c03c1
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# Vídeo 360/VR {#vr-video}

Vídeos de 360° gravam uma vista em todas as direções ao mesmo tempo. Elas são filmadas usando uma câmera onidirecional ou uma coleção de câmeras. Durante a reprodução, em uma tela plana, o usuário tem controle do ângulo de visão; a reprodução em dispositivos móveis geralmente aplica seus controles giroscópicos incorporados.

O Dynamic Media inclui suporte nativo para a entrega de 360 ativos de vídeo. Por padrão, nenhuma configuração adicional é necessária para exibir ou reproduzir. Você fornece vídeo 360 usando extensões de vídeo padrão, como .mp4, .mkv e .mov. O codec mais comum é o H.264.

Você pode usar o visualizador de vídeo 360/VR para renderizar vídeo equiretangular. O resultado é uma experiência de visualização imersiva de uma sala, propriedade, localização, paisagem, procedimento médico e assim por diante.

O áudio espacial não é suportado atualmente; se o áudio estiver misturado em estéreo, o equilíbrio (L/R) não muda conforme o cliente muda o ângulo de visão da câmera.

Consulte [Uso de vídeos do Dynamic Media 360 e miniatura de vídeo personalizada com o AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-360-video-custom-thumbnail-feature-video-use.html#dynamic-media).

Consulte também [Gerenciamento de predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

## Vídeo 360 em ação {#video-in-action}

Selecionar [Estação Espacial 360](https://s7d1.scene7.com/s7viewers/html5/Video360Viewer.html?asset=Viewers/space_station_360-AVS) para abrir uma janela do navegador e assistir a um vídeo de 360°. Durante a reprodução do vídeo, arraste o ponteiro para um novo local para alterar o ângulo de exibição.

![Quadro de vídeo do vídeo da estação espacial 360](assets/6_5_360videoiss_simplified.png)
*Quadro de vídeo da estação espacial 360*

## Vídeo e Adobe Premiere Pro 360/VR {#vr-video-and-adobe-premiere-pro}

Você pode usar o Adobe Premier Pro para visualizar e editar a gravação 360/VR. Por exemplo, você pode colocar logotipos e texto corretamente em uma cena e aplicar efeitos e transições projetados especificamente para mídia quadrretangular.

Consulte [Editar vídeo 360/VR](https://helpx.adobe.com/premiere-pro/how-to/edit-360-vr-video.html).

## Fazer upload de ativos para uso com o visualizador de vídeo 360 {#uploading-assets-for-use-with-the-video-viewer}

360 ativos de vídeo carregados no [!DNL Experience Manager] são rotulados como **Multimídia** em uma página de Ativo, semelhante ao ativo de vídeo normal.

![Um ativo de 360 vídeos carregado visualizado na exibição de cartão](assets/6_5_360video-selecttopreview.png)
*Um ativo de vídeo 360 carregado visto na exibição de Cartão. O ativo é rotulado como Multimídia.*

**Faça upload de ativos para uso com o visualizador de vídeo 360:**

1. Criação de uma pasta dedicada ao seu ativo de 360 vídeos.
1. [Aplicar um perfil de vídeo adaptável à pasta](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   A renderização de conteúdo de vídeo 360 impõe requisitos mais altos para a resolução do vídeo de origem e para a resolução de representações codificadas do que o conteúdo de vídeo padrão que não seja de 360.

   Você pode usar o Perfil de vídeo adaptável pronto para uso que já vem com o Dynamic Media. No entanto, isso resulta em uma qualidade de vídeo 360 consideravelmente menor do que a obtida para vídeos não-360 codificados com as mesmas configurações renderizadas com um visualizador de vídeo não-360. Portanto, se o vídeo 360 de alta qualidade for necessário, faça o seguinte:

   * Idealmente, seu conteúdo original de 360 vídeos deve ter uma das seguintes resoluções:

      * 1080p - 1920 x 1080, conhecido como resolução Full HD ou FHD ou
      * 2160p - 3840 x 2160, conhecido como 4k, UHD ou resolução de alta definição Ultra. Essa grande resolução de tela é mais frequentemente encontrada em televisores premium e monitores de computador. A resolução de 2160p é frequentemente chamada de &quot;4k&quot; porque a largura é próxima a 4000 pixels. Em outras palavras, oferece quatro vezes mais pixels do que 1080p.

   * [Criar um perfil de vídeo adaptável personalizado](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) com representações de maior qualidade. Por exemplo, você pode criar um Perfil de vídeo adaptável que contenha as três configurações a seguir:

      * Largura=automática; Altura=720; Taxa de bits=2500 kbps
      * Largura=automática; Altura=1080; Taxa de bits=5000 kbps
      * Largura=auto; Altura=1440; Taxa de bits=6600 kbps

   * Processe conteúdo de 360 vídeos em uma pasta dedicada exclusivamente a 360 ativos de vídeo.

   Essa abordagem exige mais da rede e da CPU do usuário.

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

## Visualizar vídeo 360 {#previewing-video}

Você pode usar a Visualização para ver como o vídeo 360 é exibido para os clientes e garantir que ele esteja se comportando conforme esperado.

Consulte também [Editar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md#editing-viewer-presets).

Quando estiver satisfeito com o vídeo 360, você poderá publicá-lo.

Consulte [Incorporação do visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md).
Consulte [Vincular URLs ao aplicativo da Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). O método de vinculação baseado em URL não é possível se o seu conteúdo interativo tiver links com URLs relativos, especialmente links para [!DNL Experience Manager Sites] páginas.
Consulte [Adição de ativos Dynamic Media a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

**Para visualizar 360 vídeos:**

1. Entrada **[!UICONTROL Assets]**, navegue até um vídeo 360 existente que você criou. Para abri-lo no modo de visualização, selecione o ativo Vídeo 360.

   ![Captura de tela de um ativo de vídeo 360 carregado, como visto na exibição de Cartão do Experience Manager.](assets/6_5_360video-selecttopreview-1.png)

   Para visualizar o vídeo, selecione o ativo de 360 vídeos.

1. Na página de visualização, próximo ao canto superior esquerdo da página, selecione a lista suspensa e, em seguida, **[!UICONTROL Visualizadores]**.

   ![Captura de tela de selecionar Visualizadores para ver a lista de visualizadores de vídeo disponíveis.](assets/6_5_360video-preview-viewers.png)

   Na lista Visualizadores, selecione **[!UICONTROL Video360_social]**, siga um destes procedimentos:

   * Para alterar o ângulo de exibição da cena estática, arraste o ponteiro pelo vídeo.
   * Para iniciar a reprodução, selecione o nome do vídeo **[!UICONTROL Reproduzir]** botão. Conforme o vídeo é reproduzido, arraste o ponteiro sobre o vídeo para alterar o ângulo de visão.

   ![Captura de tela de um usuário que seleciona o visualizador Video360_Social para visualizar um vídeo de 360 graus.](assets/6_5_360video-preview-video360-social.png)*Uma captura de tela de 360 vídeos.*

   * Na lista Visualizadores, selecione **[!UICONTROL Video360VR]**.

     O vídeo de realidade virtual (VR) é um conteúdo de vídeo imersivo que é acessado usando fones de ouvido de realidade virtual. Assim como em vídeos comuns, você cria vídeos de RV no início, quando um vídeo está sendo gravado ou capturado usando câmeras de vídeo de 360°.

   ![Captura de tela de um usuário que passa o ponteiro do mouse sobre a opção Visualizador de Video360VR.](assets/6_5_360video-preview-video360vr.png)
   *Captura de tela do vídeo 360 VR.*

1. Próximo ao canto superior direito da página de visualização, selecione **[!UICONTROL Fechar]**.

## Publicando vídeo 360 {#publishing-video}

Para usar o Vídeo 360, você deve publicá-lo. A publicação de um Vídeo 360 ativa o URL e o Código incorporado. Ele também publica o vídeo 360 na nuvem do Dynamic Media, que é integrada a um CDN para entrega escalável e eficiente.

Consulte [Publicação de ativos do Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar o Vídeo 360.
Consulte também [Incorporação do visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md).
Consulte também [Vincular URLs ao aplicativo da Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). O método de vinculação baseado em URL não é possível se o seu conteúdo interativo tiver links com URLs relativos, especialmente links para [!DNL Experience Manager Sites] páginas.
Consulte também [Adição de ativos Dynamic Media a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
