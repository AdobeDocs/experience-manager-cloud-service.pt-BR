---
title: Banners em carrossel
description: Saiba como trabalhar com banners do carrossel no Dynamic Media.
contentOwner: Rick Brough
feature: Carousel Banners
role: User
exl-id: 34541302-6610-4f5e-af93-c95328dda910
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '4492'
ht-degree: 1%

---

# Banners em carrossel{#carousel-banners}

Os banners do carrossel permitem que os profissionais de marketing impulsionem a conversão criando facilmente conteúdo promocional rotativo interativo e entregando-o em qualquer tela.

Criar e modificar conteúdo em destaque em banners promocionais pode ser demorado, limitando sua capacidade de publicar rapidamente novo conteúdo ou torná-lo mais direcionado. Os banners do carrossel permitem criar ou modificar rapidamente banners giratórios e adicionar interatividade, como links de pontos de acesso para detalhes de produtos ou recursos relacionados. Você pode entregá-los em qualquer tela, permitindo que você traga novos conteúdos promocionais para o mercado mais rapidamente.

Os banners do Carousel são designados por um banner com a palavra **[!UICONTROL CAROUSELSET]**:

![chlimage_1-438](assets/chlimage_1-438.png)

Em seu site, um banner de carrossel pode ter a seguinte aparência:

![chlimage_1-439](assets/chlimage_1-439.png)

Aqui você pode navegar pelas imagens selecionando os números. Além disso, os slides giram automaticamente com base em um intervalo de tempo que pode ser personalizado. As imagens em um banner de carrossel são compatíveis com pontos de acesso e mapas de imagem. Os usuários podem selecionar ou acessar um hiperlink ou uma janela de visualização rápida.

Neste exemplo, um usuário selecionou um mapa de imagem e acessou a janela do Quickview para luvas:

![chlimage_1-440](assets/chlimage_1-440.png)

## Veja como os banners do carrossel são criados {#watch-how-carousel-banners-are-created}

Assista a uma apresentação sobre [como os banners do carrossel são criados](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&emailurl=https://s7d5.scene7.com/s7/emailFriend&serverUrl=https://s7d5.scene7.com/is/image/&config=Scene7SharedAssets/Universal_HTML5_Video_social&contenturl=https://s7d5.scene7.com/skins/&asset=S7tutorials/InteractiveCarouselBanner) (Duração: 10 minutos e 33 segundos). Você também aprende a visualizar, editar e entregar banners do carrossel.

>[!NOTE]
>
>Os usuários não administrativos devem ser adicionados ao grupo **[!UICONTROL dam-users]** para poderem criar ou editar banners do carrossel. Se você tiver problemas ao criar ou editar, consulte o administrador do sistema que pode adicioná-lo ao grupo **d[!UICONTROL am-users]**.

## Início rápido: banners do carrossel {#quick-start-carousel-banners}

Para começar a usar o com rapidez:

1. [Identificar variáveis de ponto de acesso e mapa de imagem](#identifying-hotspot-and-image-map-variables) (somente para clientes que usam Adobe Experience Manager Assets + Dynamic Media)

   Comece identificando variáveis dinâmicas usadas pela implementação de Visualização rápida existente. Isso o ajuda a inserir os pontos de acesso e os dados de mapa de imagem corretamente durante o processo de criação do banner do carrossel no Experience Manager Assets.

<!-- LEAVE; COMMERCE BEING ADDED AGAIN IN THE FUTURE

   >[!NOTE]
   >
   >If you are an Experience Manager Sites or Ecommerce customer, you can use the built-in feature to navigate to product pages and lookup the existing skus in the product catalog. You do not need to manually enter hotspot or image map variables.
   >
   >
   >If you are an Experience ManagerAssets and Dynamic Media customer, you will manually enter data for hotspots and image maps, and then integrate the published URL or Embed code with your third-party content management system.

-->

1. Opcional: [crie uma predefinição do visualizador Conjunto de carrossel](/help/assets/dynamic-media/managing-viewer-presets.md), conforme necessário.

   Se você for um administrador, poderá personalizar o comportamento e a aparência do carrossel criando sua própria predefinição do visualizador do Carrossel. O principal benefício é poder reutilizar essa predefinição do visualizador personalizado para vários carrosséis. No entanto, os usuários podem, opcionalmente, personalizar o comportamento e a aparência do carrossel diretamente durante a criação do carrossel. Essa abordagem é preferível quando você deseja um design específico para um determinado carrossel.

1. [Carregar um banner de imagem](#uploading-image-banners).

   Carregue banners de imagem que você deseja tornar interativos.

1. [Criar um conjunto de carrosséis](#creating-carousel-sets).

   Em Conjuntos de carrosséis, os usuários navegam por imagens de banner e selecionam pontos de acesso ou mapas de imagem para acessar conteúdo relevante.

   Para criar um Conjunto de carrossel no Assets, selecione **[!UICONTROL Criar]** e selecione **[!UICONTROL Conjuntos de carrossel]**. Adicione ativos a slides e selecione **[!UICONTROL Salvar]**. Além disso, edite a aparência e o comportamento do carrossel diretamente no editor.

1. [Adicionar pontos de acesso ou mapas de imagem a um banner de imagem](#adding-hotspots-or-image-maps-to-an-image-banner).

   Adicione um ou mais pontos de acesso ou mapas de imagem a um banner de imagem. Em seguida, associe cada um deles a uma ação, como um link, uma Visualização rápida ou um Fragmento de experiência. Depois de adicionar pontos de acesso ou mapas de imagem, conclua essa tarefa publicando o conjunto de carrossel. A publicação cria o código incorporado que pode ser usado para copiar e aplicar à página de aterrissagem do site.

   Consulte [(Opcional) Visualizar banners do carrossel](#optional-previewing-carousel-banners) - Opcional. Se desejar, é possível visualizar uma representação do conjunto de carrossel e testar a interatividade.

1. [Publicar banners do Carousel](#publishing-carousel-banners).

   Publique um Conjunto de carrossel como faria com qualquer ativo. No Assets, navegue até o Conjunto de carrosséis, selecione-o e, em seguida, **[!UICONTROL Publicar]**. A publicação de um Conjunto de carrossel ativa o URL e a sequência de caracteres Incorporada.

1. Siga uma das seguintes opções:

   * [Adicionar um banner de carrossel à página do site](#adding-a-carousel-banner-to-your-website-page)É possível adicionar a URL do banner de carrossel ou o código de inserção copiado na página do site.

      * [Integre o banner do carrossel a uma exibição rápida existente](#integrating-the-carousel-banner-with-an-existing-quickview). Se você estiver usando um sistema de gerenciamento de conteúdo da Web de terceiros, será necessário integrar o novo banner do carrossel à implementação de Visualização rápida existente no seu site.

   * [Adicione um banner de carrossel ao seu site no Experience Manager](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md). Se você for um cliente do Experience Manager Sites, poderá adicionar o conjunto de carrossel diretamente à página usando o componente Mídia interativa.

Se precisar editar Conjuntos de carrossel, consulte [Editar conjuntos de carrossel](#editing-carousel-sets). Além disso, você pode exibir e editar [propriedades do Conjunto de carrosséis](/help/assets/manage-digital-assets.md#editing-properties).

## Identificação das variáveis de ponto de acesso e mapa de imagem {#identifying-hotspot-and-image-map-variables}

Comece identificando variáveis dinâmicas usadas pela implementação de Visualização rápida existente. Esse método ajuda você a inserir pontos de acesso ou dados de mapa de imagem corretamente durante o processo de criação do conjunto de carrossel no Experience Manager Assets.

Ao adicionar pontos de acesso ou mapas de imagem a uma imagem de banner, você atribui uma SKU (Stock Keeping Unit, Unidade de manutenção de estoque). Você também pode atribuir variáveis extras opcionais a cada ponto de acesso ou mapa de imagem. Essas variáveis são usadas posteriormente para corresponder pontos de acesso ou mapas de imagem ao conteúdo de Visualização rápida.

<!-- LEAVE; COMMERCE BEING ADDED LATER

>[!NOTE]
>
>If you are an Experience Manager Sites and/or Experience Manager Ecommerce customer, skip this step. You do not need to manually identify hotspot or image map variables; you can use the integration with Ecommerce for product integration. See information on [setting up eCommerce](/help/sites-cloud/administering/generic.md). In addition, you can use the Interactive component and add it to your web page.
>
>If you are an Experience Manager Assets or Media customer, you publish the URL or Embed code and then integrate with your third-party content management system and identify hotspots and image maps manually.

-->

É importante identificar corretamente o número e o tipo de variáveis a serem associadas aos dados de ponto de acesso ou mapa de imagem. Cada ponto de acesso ou mapa de imagem adicionado a uma imagem de banner deve conter informações suficientes para identificar sem ambiguidade o produto no sistema de back-end existente. Ao mesmo tempo, verifique se cada ponto de acesso ou mapa de imagem não inclui mais dados do que o necessário. O motivo é que isso tornaria o processo de entrada de dados muito complexo e contínuo, como o gerenciamento de pontos de acesso ou de mapas de imagem, mais sujeito a erros.

Há diferentes maneiras de identificar um conjunto de variáveis a serem usadas para dados de ponto de acesso ou mapa de imagem.

Às vezes, basta consultar especialistas de TI responsáveis pela implementação do Quickview existente. Eles provavelmente saberão qual é o conjunto mínimo de dados para identificar a Visualização rápida no sistema. No entanto, é possível simplesmente analisar o comportamento existente do código front-end.

A maioria das implementações do Quickview usa o seguinte paradigma:

* O usuário ativa um elemento da interface do usuário no site. Por exemplo, selecionando um botão **[!UICONTROL Quickview]**.
* O site envia uma solicitação Ajax para o back-end a fim de carregar os dados ou o conteúdo da Visualização rápida, se necessário.
* Os dados do Quickview são traduzidos no conteúdo como preparação para renderização na página da Web.
* Por fim, o código de front-end renderiza visualmente esse conteúdo na tela.

A abordagem então é visitar diferentes áreas do site existente onde o recurso de Visualização rápida é implementado. Em seguida, acione o Quickview e adquira o URL do Ajax enviado pela página da Web para carregar os dados ou conteúdo do Quickview.

Normalmente, não há necessidade de usar ferramentas de depuração especializadas. Navegadores da Web modernos possuem inspetores da Web que fazem um trabalho adequado. A seguir estão alguns exemplos de navegadores da Web que incluem inspetores da Web:

* Para ver todas as solicitações HTTP de saída no Google Chrome, pressione F12 (Windows®) ou Command-Option-I (Mac) para abrir o painel Ferramenta do desenvolvedor. Selecione a guia Rede.
* No Firefox, você pode ativar o plug-in do Firebug pressionando F12 (Windows®) ou Command-Option-I (Mac). Use a guia Rede ou a ferramenta Inspetor integrada e a guia Rede.

Quando o monitoramento de rede estiver ativado no navegador, acione o Quickview na página.

Agora, localize o URL do Ajax de visualização rápida no log de rede e copie o URL gravado para análise futura. Geralmente, quando você aciona a Visualização rápida, várias solicitações são enviadas para o servidor. Normalmente, o URL do Ajax Quickview é um dos primeiros na lista. Ele tem uma parte ou um caminho de cadeia de caracteres de consulta complexo e seu tipo MIME de resposta é `text/html`, `text/xml` ou `text/javascript`.

Durante esse processo, é importante visitar diferentes áreas do site, com diferentes categorias e tipos de produtos. O motivo é que os URLs de exibição rápida têm partes comuns para determinada categoria de site, mas só são alterados se você visitar uma área diferente do site.

No caso mais simples, a única parte variável no URL do Quickview é o SKU do produto. Nesse caso, o valor do SKU é a única parte dos dados necessária para adicionar pontos de acesso ou mapas de imagem à imagem do banner.

No entanto, em casos complexos, o URL do Quickview tem diferentes elementos variáveis, além do SKU. Alguns desses elementos incluem ID de categoria, código de cor, código de tamanho e assim por diante. Nesses casos, cada elemento é uma variável separada na definição de dados de ponto de acesso ou mapa de imagem no recurso de banner do carrossel.

Considere os seguintes exemplos de URLs do Quickview e seus pontos de acesso ou variáveis de mapa de imagem resultantes:

<table>
 <tbody>
  <tr>
   <td>SKU única, encontrada na cadeia de caracteres de consulta.</td>
   <td><p>Os URLs de Visualização rápida gravados incluem o seguinte:</p>
    <ul>
     <li><p><code>https://server/json?productId=866558&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1196184&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1081492&source=100</code></p> </li>
     <li><p><code>https://server/json?productId=1898294&source=100</code></p> </li>
    </ul> <p>A única parte variável na URL é o valor do parâmetro da cadeia de caracteres de consulta <code>productId=</code>, e é claramente um valor de SKU. Portanto, os pontos de acesso ou mapas de imagem precisam apenas de campos SKU preenchidos com valores como <code>866558,</code> <code>1196184,</code> <code>1081492,</code> <code>1898294.</code></p> </td>
  </tr>
  <tr>
   <td>SKU única, encontrada no caminho do URL.</td>
   <td><p>Os URLs de Quickview gravados incluem o seguinte:</p>
    <ul>
     <li><p><code>https://server/product/6422350843</code></p> </li>
     <li><p><code>https://server/product/1607745002</code></p> </li>
     <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>A parte variável está na última parte do caminho e se torna o valor SKU dos pontos de acesso/mapas de imagem:<strong><code>6422350843</code>, <code>1607745002,</code> </strong><code>0086724882.</code></p> </td>
  </tr>
  <tr>
   <td>SKU e ID de categoria na cadeia de caracteres de consulta.</td>
   <td><p>Os URLs de Visualização rápida gravados incluem o seguinte:</p>
    <ul>
     <li><p><code>https://server/quickView/product/?category=1100004&prodId=305466</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1100004&prodId=310181</code></p> </li>
     <li><p><code>https://server/quickView/product/?category=1740148&prodId=308706</code></p> </li>
    </ul> <p>Nesse caso, há duas partes variáveis no URL. O SKU é armazenado no parâmetro <code>prodId</code> e a ID da categoria é armazenada no parâmetro <code>category=</code>.</p> <p>Dessa forma, as definições de ponto de acesso/mapa de imagem são pares. Isto é, um valor de SKU e uma variável extra chamada <code>categoryId</code>. Os pares resultantes são os seguintes:</p>
    <ul>
     <li><p>A SKU é <strong><code>305466</code></strong> e <code>categoryId</code> é <code>1100004</code>.</p> </li>
     <li><p>A SKU é <strong><code>310181</code></strong> e <code>categoryId</code> é <strong><code>1100004</code></strong>.</p> </li>
     <li><p>A SKU é <strong><code>308706</code></strong> e <code>categoryId</code> é <strong><code>1740148</code></strong>.</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Fazer upload de banners de imagem {#uploading-image-banners}

Se você já carregou as imagens que deseja usar, avance para a próxima etapa, [Criar conjuntos de carrosséis](#creating-carousel-sets). As imagens usadas no carrossel devem ser carregadas após a ativação do Dynamic Media.

Para carregar banners de imagem, consulte [Carregar ativos](/help/assets/manage-digital-assets.md).

## Criar conjuntos de carrossel {#creating-carousel-sets}

>[!NOTE]
>
>Os usuários não administrativos devem ser adicionados ao grupo **[!UICONTROL dam-users]** para poderem criar ou editar banners do carrossel. Se você tiver problemas para criar ou editar, consulte o administrador do sistema que pode adicioná-lo ao grupo **[!UICONTROL dam-users]**.

**Para criar Conjuntos de Carrossel:**

1. No Assets, navegue até a pasta em que deseja criar o Conjunto de carrosséis e acesse **[!UICONTROL Criar > Conjunto de carrosséis]**.
1. Na página Editor de banners do Carousel, selecione **[!UICONTROL Toque para abrir o Seletor de ativos]** e selecionar a imagem do primeiro slide.

   Na página Editor de banners do Carousel, siga um destes procedimentos:

   * Próximo ao canto superior esquerdo da página, selecione o ícone **[!UICONTROL Adicionar slide]**.

   * Próximo ao meio da página, selecione **[!UICONTROL Toque para abrir o Seletor de ativos]**.

   Selecione para selecionar os ativos que deseja incluir no Conjunto de carrosséis. Os ativos selecionados têm um ícone de marca de seleção sobre eles. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Selecionar]**.

   Com o Seletor de ativos, procure por ativos ao digitar uma palavra-chave e selecionar **[!UICONTROL Retornar]**. Aplique filtros para refinar os resultados da pesquisa. Filtre por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e, em seguida, o ícone **[!UICONTROL Filtro]** na barra de ferramentas. Altere o modo de exibição clicando no ícone Modo de Exibição e selecionando **[!UICONTROL Modo de Exibição de Coluna]**, **[!UICONTROL Modo de Exibição de Cartão]** ou **[!UICONTROL Modo de Exibição de Lista]**.

   Consulte [Trabalhar com seletores](/help/assets/dynamic-media/working-with-selectors.md) para obter mais informações.

1. Continue a adicionar slides até ter adicionado todas as imagens que deseja girar no Conjunto de carrossel.
1. (Opcional) Siga qualquer um destes procedimentos:

   * Se necessário, arraste o slide para reordenar as imagens na lista.
   * Para excluir uma imagem, selecione-a e, em seguida, **[!UICONTROL Excluir Slide]** na barra de ferramentas.

   * Para aplicar uma predefinição, próximo ao canto superior direito da página, selecione a lista suspensa predefinição e, em seguida, selecione uma predefinição para aplicar simultaneamente ao conjunto.

   Para excluir um slide, selecione-o. Na barra de ferramentas, selecione **[!UICONTROL Excluir slide]**. Para mover um slide, selecione o ícone de reordenação e mova-o para o local desejado.

1. Depois de adicionar as imagens aos slides, é possível adicionar um ponto de acesso, um mapa de imagem ou ambos à imagem. Consulte [Adicionar pontos de acesso ou mapas de imagem a um Banner de imagem](#adding-hotspots-or-image-maps-to-an-image-banner).
1. Você pode alterar o design visual e o comportamento dos conjuntos de carrossel. Selecione as guias **[!UICONTROL Comportamento]** e **[!UICONTROL Aparência]** se desejar ajustar como o banner do carrossel aparece ou como componentes específicos se comportam. Consulte [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/viewer-presets.md) para obter mais informações sobre como usar o editor do visualizador.

   >[!NOTE]
   >
   >Para banners do carrossel, você pode ajustar o seguinte:
   >
   >* Duração da exibição de uma imagem. Por padrão, cada imagem é exibida por 9 segundos.
   >* Animação. Por padrão, cada transição de slide é um fade. Você pode alterá-la para uma transição de slides.
   >* Estilo dos botões. Os usuários podem girar pelos banners selecionando cada ponto ou número. É possível alterar o local em que os botões indicadores definidos são exibidos (e se são numéricos ou de um estilo pontilhado) e o tamanho deles.
   >* Altere o estilo de destaque de um mapa de imagem ou do ícone usado para pontos de acesso.
   >* Antes de editar uma predefinição do visualizador, escolha o estilo no qual deseja basear a predefinição. Se você não escolher um estilo, ao começar a editar a predefinição do visualizador, perderá todas as alterações se alterar para uma predefinição diferente.

   Você também pode visualizar a aparência do banner do carrossel. Consulte [(Opcional) Visualizar banners do carrossel](#optional-previewing-carousel-banners).

1. Selecione **[!UICONTROL Salvar]** quando terminar.

## Adicionar pontos de acesso ou mapas de imagem a um banner de imagem {#adding-hotspots-or-image-maps-to-an-image-banner}

Você pode adicionar pontos de acesso ou mapas de imagem a um banner usando o editor de conjunto de carrossel.

Ao adicionar pontos de acesso ou mapas de imagem, você pode defini-los como uma exibição pop-up de Visualização rápida, como um hiperlink ou um Fragmento de experiência.

Consulte [Fragmento de experiência](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!NOTE]
>
>As ferramentas de compartilhamento de redes sociais no Banner do carrossel não são compatíveis quando você incorpora o visualizador em um Fragmento de experiência.
>
>Para contornar esse problema, é possível usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de redes sociais. Essas predefinições do visualizador permitem incorporá-lo com sucesso aos Fragmentos de experiência.

Ao adicionar pontos de acesso ou mapas de imagem a uma imagem, lembre-se de salvar seu trabalho. As opções Desfazer e Refazer, próximas ao canto superior direito da página, são compatíveis durante a sessão de criação/edição atual.

Ao terminar de criar o banner do carrossel, você pode usar a opção Visualizar para ver uma representação de como o banner do carrossel aparece para os clientes.

Consulte [(Opcional) Visualizar banners do carrossel](#optional-previewing-carousel-banners).

>[!NOTE]
>
>Quando você adiciona pontos de acesso a um banner de imagem, as informações do ponto de acesso são armazenadas no mesmo local de metadados, em relação à localização da imagem. Esse ponto é verdadeiro independentemente de ser uma Imagem interativa ou um Banner de carrossel. Essa funcionalidade significa que você pode reutilizar facilmente a mesma imagem, juntamente com seus dados de ponto de acesso definidos, em qualquer visualizador.
>
>No entanto, esteja ciente de que os banners do carrossel são compatíveis com mapas de imagem em imagens que também podem conter pontos de acesso; uma imagem interativa não é compatível. Lembre-se dessa dica se você pretende criar uma Imagem interativa ou um Banner de carrossel que use a mesma imagem. Considere a criação de imagens interativas e banners do carrossel usando cópias separadas da mesma imagem.

>[!NOTE]
>
>Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, os pontos de acesso serão removidos.

<!-- See also [Adding Image Maps](/help/assets/image-maps.md). -->

**Para adicionar hotspots ou mapas de imagem a um Banner de Imagem:**

1. No Assets, navegue até o conjunto de carrossel que deseja tornar interativo.
1. Selecione o conjunto de carrosséis e selecione **[!UICONTROL Editar]**. O Editor do visualizador do carrossel é aberto.
1. Selecione o slide que deseja tornar interativo.
1. Próximo ao canto superior esquerdo da página, selecione **[!UICONTROL Ponto de acesso]** ou **[!UICONTROL Mapa de imagem]**.
1. Siga um destes procedimentos:

   * Para pontos de acesso: na imagem, selecione um local onde deseja que o ponto de acesso apareça.
   * Para mapas de imagem: na imagem, arraste do canto superior esquerdo para o canto inferior direito para criar a área do mapa de imagem. Você pode ajustar o tamanho do mapa de imagem arrastando os cantos.

   Se necessário, arraste o ponto de acesso ou o mapa de imagem para um novo local. Ou use as teclas de seta do teclado para controlar a posição de um ponto de acesso selecionado. Adicione mais pontos de acesso ou mapas de imagem, conforme necessário.

   Para excluir um ponto de acesso ou mapa de imagem, selecione a guia **[!UICONTROL Ações]**. No cabeçalho **[!UICONTROL Mapas e pontos de acesso]**, na lista suspensa **[!UICONTROL Tipo Selecionado]**, selecione o nome do ponto de acesso ou mapa de imagem que deseja remover. Selecione o ícone **[!UICONTROL Lixeira]** ao lado do menu e selecione **[!UICONTROL Excluir]**.

1. No campo de texto Nome, digite o nome do ponto de acesso ou do mapa de imagem. Esse nome também aparece na lista suspensa **[!UICONTROL Mapas e pontos de acesso]**. Fornecer um nome facilita a identificação do ponto de acesso ou mapa de imagem se você decidir alterá-lo no futuro.
1. Siga um destes procedimentos na guia **[!UICONTROL Ações]**:

   * Selecione **[!UICONTROL Quickview]**.

      * Se você for um cliente do Experience Manager Sites <!-- and Ecommerce-->, selecione o ícone Seletor de produto (lupa) para abrir a página Selecionar produto. Para retornar ao Editor de banners do Carousel, selecione o produto que deseja usar e marque a marca de seleção no canto superior direito da página.
      * Se você não for um cliente do Experience Manager Sites <!-- or Ecommerce -->:

         * Defina variáveis. Consulte [Identificar variáveis de ponto de acesso](#identifying-hotspot-and-image-map-variables).
         * Em seguida, insira manualmente o valor do SKU. No campo de texto Valor do SKU, digite o SKU (Unidade de manutenção de estoque) do produto, que é um identificador exclusivo para cada produto ou serviço distinto que você oferece. O valor SKU inserido preenche automaticamente a parte variável do modelo de Visualização rápida. O sistema agora associa o ponto de acesso selecionado à exibição rápida de um SKU específico.
         * (Opcional) Se houver outras variáveis na exibição Rápida que você deve usar para identificar melhor um produto, selecione **[!UICONTROL Adicionar Variável Genérica]**. No campo de texto, especifique uma variável extra. Por exemplo, category=Mens é uma variável adicionada.

         * Consulte [Trabalhar com seletores](/help/assets/dynamic-media/working-with-selectors.md) para obter mais informações.

   * Selecione **[!UICONTROL Hiperlink]**.

      * Se você for um cliente do Experience Manager Sites, selecione o ícone Seletor de sites (pasta) para navegar até um URL.

        >[!NOTE]
        >
        >O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do Experience Manager Sites.

      * Se você for um cliente independente, no campo de texto href, especifique o caminho completo do URL para uma página da Web vinculada.

   Certifique-se de especificar se o link deve ser aberto em uma nova guia do navegador (padrão recomendado) ou na mesma guia.

   Consulte [Trabalhar com seletores](/help/assets/dynamic-media/working-with-selectors.md) para obter mais informações.

   * Selecione **[!UICONTROL Fragmento de experiência]**.

      * Se você for um cliente do Experience Manager Sites, selecione o ícone Pesquisar (lupa) para abrir a página Fragmento de experiência. Para retornar à página Gerenciamento de pontos de acesso, selecione o Fragmento de experiência que deseja usar e, no canto superior direito da página, selecione **[!UICONTROL Selecionar]**.
Consulte [Fragmentos de experiência](/help/sites-cloud/authoring/fragments/content-fragments.md).

      * Especifique a largura e a altura do Fragmento de experiência conforme ele aparece no banner.

        >[!NOTE]
        >
        >As ferramentas de compartilhamento de redes sociais no Banner do carrossel não são compatíveis quando você incorpora o visualizador em um Fragmento de experiência.
        >
        >Para contornar esse ponto, é possível usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de redes sociais. Essas predefinições do visualizador permitem incorporá-lo com sucesso aos Fragmentos de experiência.

   ![experience_fragment-carouselbanner](assets/experience_fragment-carouselbanner.png)

   Você também pode visualizar a aparência do banner do carrossel. Consulte [(Opcional) Visualizar banners do carrossel](#optional-previewing-carousel-banners).

1. Selecione **[!UICONTROL Salvar]**.
1. Publique o conjunto de carrossel. A publicação cria o código incorporado ou o URL que você pode usar na página do site. Se você for um cliente do Experience Manager Sites, adicione o conjunto de carrossel diretamente à sua página da Web.

   Consulte [Publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   Consulte [Adicionar um conjunto de carrossel à página de aterrissagem de seu site](#adding-a-carousel-banner-to-your-website-page)

## Editar conjuntos de carrossel {#editing-carousel-sets}

>[!NOTE]
>
>Os usuários não administrativos devem ser adicionados ao grupo **[!UICONTROL dam-users]** para poderem criar ou editar banners do carrossel. Se você tiver problemas para criar ou editar, consulte o administrador do sistema que pode adicioná-lo ao grupo **[!UICONTROL dam-users]**.

É possível executar várias tarefas de edição em Conjuntos de carrosséis, como as seguintes:

* Adicione slides a um Conjunto de carrossel. Consulte também [Trabalhar com seletores](/help/assets/dynamic-media/working-with-selectors.md).
* Reordenar slides no Conjunto de carrossel.
* Excluir ativos no conjunto de carrossel.
* Aplicar uma predefinição do visualizador.
* Exclua o conjunto de carrosséis.
* Adicionar ou editar pontos de acesso e mapas de imagem. Consulte também [Trabalhar com seletores](/help/assets/dynamic-media/working-with-selectors.md).

**Para editar Conjuntos de Carrossel:**

1. Siga um destes procedimentos:

   * Passe o mouse sobre um ativo Conjunto de carrossel e selecione **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o mouse sobre um ativo Conjunto de carrosséis, selecione **[!UICONTROL Selecionar]** (ícone de marca de seleção) e, na barra de ferramentas, selecione **[!UICONTROL Editar]**.

   * Selecione um ativo Conjunto de carrossel e, no canto superior esquerdo da página, selecione **[!UICONTROL Editar]** (ícone de lápis).

1. Para editar o Conjunto de carrosséis, siga um destes procedimentos:

   * Para adicionar um slide, selecione o ícone **[!UICONTROL Adicionar Slide]**. Navegue até o ativo que deseja adicionar a esse slide e marque a marca de seleção.
   * Para reordenar slides, arraste um slide para um novo local (selecione o ícone reordenar para mover itens).
   * Para adicionar um ponto de acesso ou mapa de imagem, selecione os ícones de ponto de acesso ou mapa de imagem e consulte [Adicionar pontos de acesso e mapas de imagem a um Banner de imagem](#adding-hotspots-or-image-maps-to-an-image-banner).
   * Para editar a aparência ou o comportamento do conjunto de carrossel, selecione a guia **[!UICONTROL Aparência]** ou a guia **[!UICONTROL Comportamento]** e defina as opções desejadas.
   * Para editar pontos de acesso ou mapas de imagem, no slide apropriado, selecione um ponto de acesso ou mapa de imagem. Na guia **[!UICONTROL Ações]**, faça suas alterações.
   * Para excluir um slide, selecione-o e, em seguida, selecione **[!UICONTROL Excluir Slide]** na barra de ferramentas.
   * Para aplicar uma predefinição, próximo ao canto superior direito da página, selecione a lista suspensa **[!UICONTROL Predefinição]** e selecione uma predefinição do visualizador.
   * Para excluir um Conjunto de carrossel inteiro, navegue até o Conjunto de carrossel, selecione-o e **[!UICONTROL Excluir]**.

   >[!NOTE]
   >
   >Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, os pontos de acesso serão removidos.

## (Opcional) Visualizar banners do carrossel {#optional-previewing-carousel-banners}

Você pode usar a Visualização para ver como o banner do carrossel aparece para os clientes. Usar a visualização também permite que você teste os pontos de acesso e mapas de imagem do banner do carrossel para garantir que eles se comportem conforme esperado.

Quando estiver satisfeito com o banner do carrossel, você poderá publicá-lo.
Consulte [Incorporar o Visualizador de Vídeo ou Imagem a uma Página da Web](/help/assets/dynamic-media/embed-code.md).
Consulte [Vincular URLs ao aplicativo Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do Experience Manager Sites.
Consulte [Adicionar o Dynamic Media Assets às páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Você pode visualizar banners do carrossel no Editor do carrossel (método preferencial) ou na lista **[!UICONTROL Visualizadores]**.

**Para visualizar opcionalmente os banners do Carousel:**

1. No **[!UICONTROL Assets]**, navegue até um banner de carrossel existente que você criou e selecione para abri-lo.
1. Selecione **[!UICONTROL Editar]**.
1. Na lista de predefinições do visualizador, no canto direito da barra de ferramentas, selecione um visualizador para visualizar o banner do carrossel.

   ![experience_fragment-carouselbanner-viewerdropdown](assets/experience_fragment-carouselbanner-viewerdropdown.png)

1. Selecione **[!UICONTROL Visualizar]**.
1. Para testar suas ações associadas, selecione os pontos de acesso ou mapas de imagem na imagem.

**Para visualizar banners do carrossel da lista Visualizadores:**

1. No **[!UICONTROL Assets]**, navegue até um banner de carrossel existente que você criou e selecione para abri-lo.
1. Próximo ao canto superior esquerdo da página Visualizar, selecione o ícone Conteúdo.
1. Na lista **[!UICONTROL Visualizadores]** no painel à esquerda da página, selecione o nome da predefinição do visualizador do banner do carrossel que deseja usar.
1. Para testar suas ações associadas, selecione os pontos de acesso ou mapas de imagem na imagem.

## Publicar banners do Carousel {#publishing-carousel-banners}

Para usar o carrossel, você deve publicá-lo. A publicação de um Conjunto de carrossel ativa o URL e o Código incorporado. Ele também publica o carrossel na nuvem do Dynamic Media, que é integrada a um CDN para entrega escalável e de alto desempenho.

>[!NOTE]
>
>Se você usar uma imagem interativa existente com pontos de acesso para o banner do carrossel, será necessário publicar a imagem interativa separadamente após publicar o banner do carrossel.
>
>Além disso, se você modificar uma imagem interativa publicada pré-existente usada em um banner do carrossel, publique a imagem interativa para que essas alterações sejam refletidas no banner do carrossel.

Consulte [Publicar o Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obter informações sobre como publicar banners do carrossel.

## Adicione um banner de carrossel à página do site {#adding-a-carousel-banner-to-your-website-page}

Depois de carregar as imagens do banner para criar um carrossel, você adicionou pontos de acesso, mapas de imagem ou ambos ao banner. Publicado o conjunto de carrossel. Agora você está pronto para adicioná-lo à página existente do site.

>[!NOTE]
>
>Se você for um cliente do Experience Manager Sites, poderá adicionar o banner do carrossel diretamente à sua página arrastando o componente de Mídia interativa para sua página. Consulte [Adicionar o Dynamic Media Assets às páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

No entanto, se você for um cliente independente do Experience Manager Assets, poderá adicionar manualmente o banner do carrossel à página de aterrissagem do site.

1. Copie o código incorporado do conjunto de carrossel publicado.
Consulte [Incorporar o Visualizador de Vídeo ou Imagem a uma Página da Web](/help/assets/dynamic-media/embed-code.md).

1. Adicione o código incorporado que você copiou do Experience Manager Assets à sua página da Web.
O código incorporado copiado é responsivo, portanto, se ajusta automaticamente à área de incorporação da página.

## Integre o banner do carrossel a uma visualização rápida existente {#integrating-the-carousel-banner-with-an-existing-quickview}

Observação: esta etapa se aplica somente se você for um cliente independente do Experience Manager Assets.

A última etapa deste processo é integrar o banner do carrossel a uma implementação do Quickview existente no seu site. Cada implementação de visualização rápida é única e é necessária uma abordagem específica que geralmente envolve a assistência de um profissional de TI de front-end.

A implementação existente do Quickview normalmente representa uma cadeia de ações inter-relacionadas que ocorrem na página da Web na seguinte ordem:

1. Um usuário aciona um elemento na interface do usuário do seu site.
1. O código front-end obtém um URL de visualização rápida com base no elemento de interface do usuário que foi acionado na etapa 1.
1. O código de front-end envia uma solicitação de Ajax usando o URL obtido na etapa 2.
1. A lógica de back-end retorna os dados ou o conteúdo de visualização rápida correspondentes ao código de front-end.
1. O código de front-end carrega os dados ou o conteúdo da Visualização rápida.
1. Como opção, o código de front-end converte os dados de Visualização rápida carregados em uma representação do HTML.
1. O código de front-end exibe uma caixa de diálogo ou painel modal e renderiza o conteúdo do HTML na tela para o usuário.

Essas chamadas não representam chamadas de API públicas independentes que podem ser chamadas pela lógica da página da Web de uma etapa arbitrária. Em vez disso, é uma chamada encadeada em que cada próxima etapa é ocultada na última fase (retorno de chamada) da etapa anterior.

Ao mesmo tempo em que o banner do carrossel substitui a etapa 1 e parcialmente a etapa 2, quando um usuário seleciona um ponto de acesso ou mapa de imagem, essa interação é realizada pelo visualizador. O visualizador retorna um evento à página da Web que contém todos os dados de ponto de acesso ou mapa de imagem adicionados anteriormente.

Nesse manipulador de eventos, o código de front-end faz o seguinte:

* Escuta um evento emitido pelo banner do carrossel.
* Constrói um URL de visualização rápida com base nos dados do ponto de acesso ou mapa de imagem.
* Aciona o processo de carregar a Visualização rápida do back-end e renderizá-la na tela para exibição.

O código incorporado retornado pelo Experience Manager Assets já tem um manipulador de eventos pronto para uso em vigor que está comentado.

Portanto, é necessário apenas remover o comentário do código e substituir o corpo do manipulador fictício pelo código específico da página da Web.

O processo de construção do URL de visualização rápida é oposto ao processo usado para identificar as variáveis de ponto de acesso e mapa de imagem abordadas anteriormente.

Consulte [Identificar variáveis de ponto de acesso e mapa de imagem](#identifying-hotspot-and-image-map-variables).

A última etapa para acionar o URL de visualização rápida e ativar o painel de Visualização rápida provavelmente requer a assistência de um profissional de TI de front-end do seu departamento de TI. Eles têm o conhecimento para saber como acionar com precisão a implementação da Visualização rápida a partir da etapa adequada, com um URL de Visualização rápida pronto para uso.

## Crie um pop-up personalizado do Windows® usando o Quickview {#using-quickviews-to-create-custom-pop-ups}

Consulte [Criar Windows® pop-up personalizado usando o Quickview](/help/assets/dynamic-media/custom-pop-ups.md).
