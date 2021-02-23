---
title: Uso de visualizações rápidas para criar pop-ups personalizados
description: A visualização Rápida padrão é usada em experiências de comércio eletrônico em que uma pop-up é exibida com informações do produto para acionar uma compra. Você pode acionar a exibição de conteúdo personalizado nos pop-ups.
translation-type: tm+mt
source-git-commit: ad626d9722f1942249197d96aa5fac3d8f7ed947
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 1%

---


# Usando visualizações rápidas para criar janelas pop-up personalizadas {#using-quickviews-to-create-custom-pop-ups}

A visualização Rápida padrão é usada em experiências de comércio eletrônico em que uma pop-up é exibida com informações do produto para acionar uma compra. No entanto, é possível acionar a exibição de conteúdo personalizado nos pop-ups. Dependendo do visualizador usado, os clientes podem tocar em um ponto de acesso, em uma imagem em miniatura ou em um mapa de imagem para ver informações ou conteúdo relacionado.

Visualizações rápidas são suportadas pelos seguintes visualizadores no Dynamic Media:

* Imagens interativas (pontos de acesso clicáveis)
* Vídeo interativo (imagens em miniatura clicáveis durante a reprodução do vídeo)
* Banners de carrossel (pontos de conexão clicáveis ou mapas de imagem)

Embora a funcionalidade de cada visualizador seja diferente, o processo de criação de uma visualização Rápida é o mesmo entre os três visualizadores suportados.

**Para usar visualizações rápidas para criar janelas pop-up personalizadas**

1. Crie uma visualização rápida para um ativo carregado.

   Geralmente, você cria uma visualização rápida ao mesmo tempo que edita um ativo para uso com o visualizador que está usando.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizador que você está usando</strong></td>
    <td><strong>Para criar a visualização Rápida, conclua estas etapas</strong></td>
    </tr>
    <tr>
    <td>Imagens interativas</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Adicionar pontos de acesso a um banner</a> de imagem.</td>
    </tr>
    <tr>
    <td>Vídeos interativos</td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Adicionando interatividade ao vídeo</a>.</td>
    </tr>
    <tr>
    <td>Banners em carrossel</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Adicionar pontos de conexão ou mapas de imagem a um banner</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Obtenha o código incorporado do visualizador para integrar o visualizador dentro do seu site.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizador que você está usando</strong><br /> </td>
    <td><strong>Para integrar o visualizador ao seu site, conclua estas etapas</strong></td>
    </tr>
    <tr>
    <td>Imagem interativa</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integração de uma imagem interativa com seu site</a>.<br /> </td>
    </tr>
    <tr>
    <td>Vídeo interativo<br /> </td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integração de um vídeo interativo com seu site</a>.<br /> </td>
    </tr>
    <tr>
    <td>Banner do carrossel</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Adicionar um banner de carrossel à página</a> do site.<br /> </td>
    </tr>
    </tbody>
   </table>

1. O visualizador usado precisa saber como usar a visualização Rápida.

   O visualizador usa um manipulador chamado `QuickViewActive`.

   ****
ExemploSuponha que você esteja usando a seguinte amostra de código incorporado em sua página da Web para uma imagem interativa:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   O manipulador é carregado no visualizador usando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Usando o exemplo de código incorporado de exemplo acima, você tem o seguinte código:**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   Saiba mais sobre o método `setHandlers()` no seguinte:

   * Visualizador de imagens interativas: [operadores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visualizador de vídeo interativo: [operadores](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. Agora, configure o manipulador `quickViewActivate`.

   O manipulador `quickViewActivate` controla as visualizações rápidas no visualizador. O manipulador contém a lista variável e as chamadas de função para uso com a visualização Rápida. O código incorporado fornece mapeamento para a variável SKU definida na visualização Rápida. Também faz uma chamada de função de exemplo `loadQuickView`.

   **Variável**
mapeamentoVariáveis do mapa para uso em sua página da Web com o valor SKU e variáveis genéricas contidas na visualização Rápida:

   `var *variable1*= inData.*quickviewVariable*`

   O código incorporado fornecido tem um mapeamento de amostra para a variável SKU:

   `var sku=inData.sku`

   Mapeie outras variáveis da visualização Rápida também, como a seguir:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Função**
callO manipulador também requer uma função chamada para que a visualização Rápida funcione. Pressupõe-se que a função seja acessível pela página de host. O código incorporado fornece uma chamada de função de exemplo:

   `loadQuickView(sku)`

   A chamada de função de exemplo considera que a função `loadQuickView()` existe e está acessível.

   Saiba mais sobre o método `quickViewActivate` no seguinte:

   * Visualizador de imagens interativas - [retornos de chamada do Evento](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visualizador de vídeo interativo - [retornos de chamada do Evento](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Suporte a dados interativos no Visualizador de vídeo interativo - [Suporte a dados interativos](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Faça o seguinte:

   * Exclua as barras de comentário da seção setHandlers do código incorporado.
   * Mapeie quaisquer variáveis adicionais contidas na visualização Rápida.

      * Atualize a chamada `loadQuickView(sku,*var1*,*var2*)` se você adicionar mais variáveis.
   * Crie uma função `loadQuickView` () simples na página, fora do visualizador.

      Por exemplo, o seguinte grava o valor de SKU no console do navegador:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Carregue uma página HTML de teste em um servidor Web e abra.

      As variáveis da visualização rápida são mapeadas. A chamada de função está ativada. E o console do navegador grava o valor da variável no console do navegador. Ele faz isso usando a função de amostra fornecida.



1. Agora você pode usar uma função para invocar um pop-up simples na visualização Rápida. O exemplo a seguir usa um `DIV` para um pop-up.
1. Estilo do pop-up `DIV` da seguinte maneira. Adicione estilos adicionais conforme desejado.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Coloque o pop-up `DIV` no corpo da sua página HTML.

   Um dos elementos é definido com uma ID que é atualizada com o valor SKU quando o usuário chama uma visualização rápida. O exemplo também inclui um botão simples para ocultar o pop-up novamente depois que ele se torna visível.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Para atualizar o valor de SKU na janela pop-up, adicione uma função. Torne a janela pop-up visível, substituindo a função simples criada na etapa 5 pelo seguinte:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Carregue uma página HTML de teste no seu servidor Web e abra. O visualizador exibe o pop-up `DIV` quando um usuário chama uma visualização rápida.
1. **Como exibir a janela pop-up personalizada no modo de tela cheia**

   Alguns visualizadores, como o Visualizador de vídeo interativo, suportam a exibição no modo de tela cheia. No entanto, usar o pop-up conforme descrito nas etapas anteriores faz com que ele seja exibido atrás do visualizador no modo de tela cheia.

   Para que a janela pop-up seja exibida nos modos padrão e de tela cheia, anexe a janela pop-up ao container do visualizador. Nesse caso, use um segundo método handler, `initComplete`.

   O manipulador `initComplete` é chamado depois que o visualizador é inicializado.

   ```xml
   "initComplete":function() { code block }
   ```

   Saiba mais sobre o método `init()` no seguinte:

   * Visualizador de imagens interativas - [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visualizador de vídeo interativo - [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. Para anexar o pop-up — descrito nas etapas anteriores — ao visualizador, use o seguinte código:

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   No código acima, você fez o seguinte:

   * Identificada a janela pop-up personalizada.
   * Removido do DOM.
   * Identificado o container do visualizador.
   * O pop-up foi anexado ao container do visualizador.

1. Todo o código setHandlers é semelhante ao seguinte (o visualizador de vídeo interativo foi usado):

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. Depois que os manipuladores forem carregados, você inicializará o visualizador:

   `*viewerInstance.*init()`

   ****
ExemploEste exemplo usa o visualizador de imagem interativo.

   `s7interactiveimageviewer.init()`

   Depois de incorporar o visualizador à página de host, verifique se a instância do visualizador foi criada. Além disso, verifique se os manipuladores foram carregados antes que o visualizador seja chamado usando `init()`.

