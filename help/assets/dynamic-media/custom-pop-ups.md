---
title: Criar pop-ups personalizados usando o Quickview
description: '"Saiba mais sobre como o Quickview padrão é usado em experiências de comércio eletrônico, em que uma janela pop-up é exibida com informações do produto para impulsionar uma compra. Você pode acionar a exibição de conteúdo personalizado na janela pop-up."'
feature: Interactive Images,Interactive Videos,Carousel Banners
role: Admin,User
exl-id: c2bc6ec8-d46e-4681-ac3e-3337b9e6ae5c
source-git-commit: 462ce45d24cf8bcad6963011d2d57d9d7da45550
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# Criar pop-ups personalizados usando o Quickview {#using-quickviews-to-create-custom-pop-ups}

O Quickview padrão é usado em experiências de comércio eletrônico, onde uma pop-up é exibida com informações do produto para impulsionar uma compra. No entanto, você pode acionar a exibição de conteúdo personalizado nas janelas pop-ups. Dependendo do visualizador usado, os clientes podem selecionar um ponto de acesso, uma imagem em miniatura ou um mapa de imagem para ver informações ou conteúdo relacionado.

O Quickview é compatível com os seguintes visualizadores no Dynamic Media:

* Imagens interativas (pontos de acesso selecionáveis)
* Vídeo interativo (imagens em miniatura selecionáveis durante a reprodução do vídeo)
* Banners de carrossel (pontos de conexão ou mapas de imagem selecionáveis)

Embora a funcionalidade de cada visualizador seja diferente, o processo de criação de uma exibição rápida é o mesmo em todos os três visualizadores compatíveis.

**Para criar pop-ups personalizados usando o Quickview:**

1. Crie uma Exibição rápida para um ativo carregado.

   Geralmente, você cria um Quickview ao mesmo tempo em que edita um ativo para uso com o visualizador que está usando.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizador que você está usando</strong></td>
    <td><strong>Para criar o Quickview, conclua essas etapas</strong></td>
    </tr>
    <tr>
    <td>Imagens interativas</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Adicionar pontos de acesso a um banner de imagem</a>.</td>
    </tr>
    <tr>
    <td>Vídeos interativos</td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Adicionar interatividade ao vídeo</a>.</td>
    </tr>
    <tr>
    <td>Banners em carrossel</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Adição de pontos de acesso ou mapas de imagem a um banner</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Obtenha o código incorporado do visualizador para Integrar o visualizador em seu site.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizador que você está usando</strong><br /> </td>
    <td><strong>Para integrar o visualizador ao seu site, conclua estas etapas</strong></td>
    </tr>
    <tr>
    <td>Imagem interativa</td>
    <td><a href="/help/assets/dynamic-media/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integração de uma imagem interativa ao seu site</a>.<br /> </td>
    </tr>
    <tr>
    <td>Vídeo interativo<br /> </td>
    <td><a href="/help/assets/dynamic-media/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integração de um vídeo interativo com seu site</a>.<br /> </td>
    </tr>
    <tr>
    <td>Banner do carrossel</td>
    <td><a href="/help/assets/dynamic-media/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Adicionar um banner de carrossel à página do site</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. O visualizador usado precisa saber como usar o Quickview.

   O visualizador usa um manipulador chamado `QuickViewActive`.

   **Exemplo**
Suponha que você estava usando o seguinte código incorporado de exemplo na sua página da Web para uma imagem interativa:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   O manipulador é carregado no visualizador usando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Usando o exemplo de código incorporado de exemplo acima, você tem o seguinte código:**

   ```xml {.line-numbers}
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   Saiba mais sobre `setHandlers()` método no seguinte:

   * Visualizador de Imagem Interativa - [ladrões](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visualizador de vídeo interativo - [ladrões](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. Agora configure o `quickViewActivate` manipulador.

   O `quickViewActivate` O manipulador controla o Quickview no visualizador. O manipulador contém a lista de variáveis e as chamadas de função para uso com o Quickview. O código incorporado fornece mapeamento para a variável SKU definida no Quickview. Também faz uma amostra `loadQuickView` chamada de função.

   **Mapeamento de variável**
Mapeie variáveis para uso em sua página da Web para o valor SKU e variáveis genéricas contidas no Quickview:

   `var *variable1*= inData.*quickviewVariable*`

   O código incorporado fornecido tem um mapeamento de amostra para a variável SKU:

   `var sku=inData.sku`

   Mapeie outras variáveis do Quickview também, como no seguinte:

   ```xml {.line-numbers}
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Chamada de função**
O manipulador também requer uma chamada de função para que o Quickview funcione. A função é considerada acessível pela página de host. O código incorporado fornece uma chamada de função de exemplo:

   `loadQuickView(sku)`

   A chamada de função de exemplo assume a função `loadQuickView()` existe e está acessível.

   Saiba mais sobre `quickViewActivate` método no seguinte:

   * Visualizador de Imagem Interativa - [Retornos de chamada do evento](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visualizador de vídeo interativo - [Retornos de chamada do evento](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Suporte a dados interativos no visualizador de Vídeo interativo - [Suporte a dados interativos](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Faça o seguinte:

   * Exclua a seção setHandlers do código incorporado.
   * Mapeie quaisquer variáveis adicionais contidas no Quickview.

      * Atualize o `loadQuickView(sku,*var1*,*var2*)` chame se você adicionar mais variáveis.
   * Crie um `loadQuickView` () na página, fora do visualizador.

      Por exemplo, o item a seguir grava o valor de SKU no console do navegador:

   ```xml {.line-numbers}
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Faça o upload de uma HTML de teste para um servidor da Web e abra.

      As variáveis do Quickview são mapeadas. A chamada de função está em vigor. E o console do navegador grava o valor da variável no console do navegador. Ele faz isso usando a função de amostra fornecida.



1. Agora você pode usar uma função para invocar um pop-up simples no Quickview. O exemplo a seguir usa um `DIV` para um pop-up.
1. Estilo da pop-up `DIV` da seguinte maneira. Adicione estilos adicionais, conforme desejado.

   ```xml {.line-numbers}
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Inserir o pop-up `DIV` no corpo da página do HTML.

   Um dos elementos é definido com uma ID que é atualizada com o valor SKU quando o usuário chama uma Quickview. O exemplo também inclui um botão simples para ocultar a pop-up novamente depois que ela se tornar visível.

   ```xml {.line-numbers}
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Para atualizar o valor SKU na janela pop-up, adicione uma função. Torne a janela pop-up visível ao substituir a função simples criada na etapa 5 pelo seguinte:

   ```xml {.line-numbers}
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Carregue uma página de HTML de teste no seu servidor da Web e abra. O visualizador exibe o pop-up `DIV` quando um usuário chamar uma exibição rápida.
1. **Como exibir a janela pop-up personalizada no modo de tela cheia**

   Alguns visualizadores, como o visualizador de Vídeo interativo, suportam a exibição no modo de tela cheia. No entanto, usar a pop-up conforme descrito nas etapas anteriores faz com que seja exibido atrás do visualizador no modo de tela cheia.

   Para exibir a janela pop-up nos modos de tela cheia e padrão, anexe a janela pop-up ao contêiner do visualizador. Nesse caso, use um segundo método handler, `initComplete`.

   O `initComplete` O manipulador é chamado após a inicialização do visualizador.

   ```xml {.line-numbers}
   "initComplete":function() { code block }
   ```

   Saiba mais sobre `init()` método no seguinte:

   * Visualizador de Imagem Interativa - [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visualizador de vídeo interativo - [init](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. Para anexar o pop-up — descrito nas etapas anteriores — ao visualizador, use o seguinte código:

   ```xml {.line-numbers}
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
   * Removido-o do DOM.
   * Identificado o contêiner do visualizador.
   * Anexado o pop-up ao contêiner do visualizador.

1. Todo o código setHandlers é semelhante ao seguinte (o visualizador de Vídeo interativo foi usado):

   ```xml {.line-numbers}
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

1. Após carregar os manipuladores, inicialize o visualizador:

   `*viewerInstance.*init()`

   **Exemplo**
Este exemplo usa o visualizador de imagens interativas.

   `s7interactiveimageviewer.init()`

   Depois de incorporar o visualizador à sua página de host, verifique se a instância do visualizador foi criada. Além disso, verifique se os manipuladores são carregados antes que o visualizador seja chamado usando `init()`.
