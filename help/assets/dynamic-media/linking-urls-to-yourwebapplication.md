---
title: Vincular URLs ao seu aplicativo web.
description: Saiba como vincular URLs ao aplicativo da Web no Dynamic Media.
role: User
exl-id: 3cd3f4d5-ebf0-4318-9a0d-1ea69453d57b
source-git-commit: 1d42305b6a597dc95bff8b34eee8279eb0e511f3
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 6%

---

# Vincular URLs ao seu aplicativo web. {#linking-urls-to-your-web-application}

Seus sites e aplicativos acessam os serviços da Dynamic Media por meio de chamadas de URL. Após publicar um ativo, o Dynamic Media ativa uma string de URL que faz referência a ele. Você pode colar esses URLs em um navegador da Web para testes.

Você vincula a URLs somente se *not* usando o Adobe Experience Manager como WCM. A vinculação - versus a incorporação - é usada quando você deseja fornecer um reprodutor de vídeo como uma janela pop-up ou modal. Se estiver usando o Experience Manager como o WCM, [você adiciona os ativos diretamente na página.](adding-dynamic-media-assets-to-pages.md)

Para colocar essas cadeias de caracteres de URL em suas páginas da Web e aplicativos, copie-as do Dynamic Media.

>[!NOTE]
>
>As cadeias de caracteres de URL só estão disponíveis para representações dinâmicas de ativos. No momento, eles não estão disponíveis para ativos estáticos que residem no DAM e não no servidor do Dynamic Media. O botão URL não é exibido para representações estáticas.

Consulte também [Incorporar o visualizador de vídeo ou imagem em uma página da Web](embed-code.md).

Consulte também [Vincular URLs do YouTube ao aplicativo da Web](video.md).

Consulte também [Fornecer imagens otimizadas para um site responsivo](responsive-site.md).

Consulte também [Fazer upload de ativos](/help/assets/manage-digital-assets.md#uploading-assets).

## Obter um URL para um ativo {#obtaining-a-url-for-an-asset}

Você pode obter uma string de URL gerada por uma Predefinição de imagem ou por uma Predefinição do visualizador. Depois de copiar o URL, ele chega à Área de transferência para que você possa colá-lo conforme necessário nas páginas do seu site ou aplicativo.

>[!NOTE]
>
>O URL não está disponível para cópia até que você tenha publicado o ativo selecionado. Além disso, você também deve publicar a predefinição do visualizador ou a predefinição de imagem.
>
>Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).
>
>Consulte [Publicar predefinições do visualizador](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Publicar predefinições da imagem](managing-image-presets.md#publishing-image-presets).

Há várias maneiras diferentes de obter uma string de URL. No entanto, as etapas abaixo mostram apenas um método que você pode usar.

**Para obter um URL para um ativo:**

1. Navegue até o *publicado* ativo cujo URL predefinido de imagem ou URL predefinido do visualizador você deseja copiar e selecione o ativo para abri-lo.

   Lembre-se de que os URLs só estão disponíveis para cópia *depois* que você *publicou* os ativos pela primeira vez. Além disso, a predefinição do visualizador ou da imagem também deve ser publicada.

   Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).

   Consulte [Publicar predefinições do visualizador](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Publicar predefinições da imagem](managing-image-presets.md#publishing-image-presets).

1. Com base no ativo selecionado, execute um dos seguintes procedimentos:

   * Se você selecionou uma imagem, no menu suspenso, selecione **[!UICONTROL Representações]**.

      Em **[!UICONTROL Dinâmico]** selecione um nome predefinido para exibir sua representação no quadro direito. Se necessário, role a lista Representações para ver o cabeçalho Dinâmico .

      Na parte inferior do painel esquerdo, selecione **[!UICONTROL URL]**.

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * Se você selecionou um conjunto de rotação, um conjunto de imagens, um conjunto de carrossel ou um vídeo, no menu suspenso, selecione **[!UICONTROL Visualizadores]**.

      No painel à esquerda, selecione um nome de predefinição do visualizador. Uma visualização do conjunto ou do vídeo é aberta em uma página separada.

      No painel à esquerda, na parte inferior, selecione **[!UICONTROL URL]**.

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. Para visualizar o ativo ou adicionar à página de conteúdo da Web, selecione e copie o texto no navegador da Web.

   Para sair da janela do URL, selecione o **[!UICONTROL X]** ou selecione **[!UICONTROL Fechar]**.

## Obter um URL para um ativo estático {#obtaining-a-url-for-a-static-asset}

O Dynamic Media oferece suporte à entrega de ativos estáticos, que são outros ativos além de apenas imagens e vídeo. Os formatos de ativos estáticos suportados para entrega incluem:

* arquivos 3D
* GIF animado
* Arquivos de áudio
* CSS
* JavaScript (quando sua empresa é configurada com seu próprio domínio)
* PDF
* SVG
* XML
* ZIP

**Para obter um URL para um ativo estático:**

1. Navegue até o *publicado* ativo estático cujo URL você deseja copiar e selecione o ativo para abri-lo.

   Lembre-se de que os URLs só estão disponíveis para cópia *after* você tem primeiro *publicado* o ativo estático.

   Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).

1. Use qualquer um dos métodos a seguir para obter o URL do ativo estático publicado:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         Por exemplo, `https://aem.com/is/content/adobe/image.gif`.
   * Selecionar **[!UICONTROL Ativo]** > **[!UICONTROL Representações dinâmicas]**, em seguida, selecione uma representação dinâmica do ativo estático e copie o URL.

      Altere o URL copiado para usar `is/content` no caminho em vez de `is/image/`.


## Obter um URL de vídeo para uma representação de vídeo publicada {#obtaining-a-video-url-for-a-published-video-rendition}

1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Cloud]** > **[!UICONTROL Cloud Services]**.
1. No **[!UICONTROL Cloud Services]** página, role para baixo até a página **[!UICONTROL Dynamic Media Cloud Services]** e selecione **[!UICONTROL Mostrar configurações]**.
1. Em **[!UICONTROL Configurações disponíveis]**, selecione o nome da configuração desejada.

1. No **[!UICONTROL Configurações da Dynamic Media Cloud]** página, em **[!UICONTROL URL do serviço de vídeo]**, copie todo o caminho do URL. Posteriormente, é necessário o caminho do URL copiado nas etapas.

   Por exemplo, o caminho do URL pode ser exibido de forma semelhante ao seguinte:

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (O caminho acima é apenas para fins de explicação; não é o caminho real que você copia.)

1. Em **[!UICONTROL ID de registro]**, copie o nome do cliente encontrado na última parte da ID.

   Por exemplo, se a ID de registro foi `87654321|MyCompany`, o nome do cliente seria `MyCompany`.

1. Ao lado do canto superior esquerdo da página, selecione **[!UICONTROL Cloud Services]**, selecione o ícone Experience Manager e navegue até **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. Copie todo o caminho de representação de vídeo do JCR (Java™ Content Repository).

   Por exemplo, o caminho de representação do vídeo pode ser exibido de forma semelhante ao seguinte:

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (O caminho acima é apenas para fins de explicação; não é o caminho real que você copia.)

1. Para formar um caminho de URL completo, organize as informações copiadas na seguinte ordem:

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Por exemplo, usando os caminhos de exemplo e o nome de cliente de exemplo das etapas acima, o caminho completo é exibido da seguinte maneira:

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Esse caminho é o URL completo do vídeo para uma representação de vídeo publicada.

## Obter um URL de vídeo para transmissão adaptável (HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Cloud]** > **[!UICONTROL Cloud Services]**.
1. No **[!UICONTROL Cloud Services]** página, role para baixo até a página **[!UICONTROL Dynamic Media Cloud Services]** e selecione **[!UICONTROL Mostrar configurações]**.
1. Em **[!UICONTROL Configurações disponíveis]**, selecione o nome da configuração desejada.
1. No **[!UICONTROL Configurações do Dynamic Media Cloud Services]** faça o seguinte:

   * Em **[!UICONTROL URL do serviço de vídeo]**, copie o caminho do URL inteiro. Posteriormente, você precisará do caminho do URL copiado nessas etapas. Por exemplo, o caminho do URL pode ser exibido de forma semelhante ao seguinte:

   `https://gateway-na.assetsadobe.com/DMGateway/`

   (O caminho acima é apenas para fins de explicação; não é o caminho real que você copia.)

   * Em **[!UICONTROL ID de registro]**, copie o nome do cliente encontrado na última parte da ID. Posteriormente, você precisará do nome do cliente copiado nessas etapas.

      Por exemplo, se a ID de registro foi `87654321|demoCo`, o nome do cliente que você copiar seria `demoCo`.


1. Com base no protocolo de entrega de vídeo que você está usando, copie o respectivo seletor de protocolo. Posteriormente, você precisará do seletor de protocolo copiado nessas etapas.

   <table>
    <tbody>
      <tr>
      <td><strong>Protocolo de entrega de vídeo usado</strong></td>
      <td><strong>Seletor de protocolo a ser usado</strong></td>
      </tr>
      <tr>
      <td><p>HTTP</p> <p>Se estiver usando HTTP (entrega de vídeo não segura), altere <code>https</code> para <code>http</code> no valor do URL do serviço de vídeo copiado anteriormente.</p> </td>
      <td><code>public/</code></td>
      </tr>
      <tr>
      <td>HTTPS</td>
      <td><code>public-ssl/</code></td>
      </tr>
    </tbody>
   </table>

1. Copie o caminho completo do ativo de vídeo no Experience Manager, conforme processado pelo Dynamic Media. Posteriormente, é necessário usar esse caminho de ativo de vídeo copiado nessas etapas.

   Por exemplo:

   `/content/dam/marketing/MyVideo.mp4`

1. Combine todas as partes copiadas anteriormente para criar uma cadeia de caracteres na seguinte ordem:

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   Por exemplo, usando as informações copiadas dos exemplos nessas etapas, a sequência de caracteres seria exibida da seguinte maneira:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Preencha o URL ao anexar `.m3u8` ao final da string. Por exemplo, anexar `.m3u8` para a string da etapa anterior, o caminho completo do URL seria exibido da seguinte maneira:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Usar HTTP/2 para fornecer ativos da Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como os navegadores e servidores se comunicam. Ele oferece transferência mais rápida de informações e reduz a quantidade de poder de processamento necessário. A entrega de ativos do Dynamic Media agora pode ser feita via HTTP/2, o que oferece melhor resposta e tempo de carregamento.

Consulte [Entrega de conteúdo HTTP2](http2faq.md) para obter detalhes completos sobre a introdução ao HTTP/2 com sua conta do Dynamic Media.
