---
title: Imagens interativas
description: Saiba como trabalhar com imagens interativas no Dynamic Media.
translation-type: tm+mt
source-git-commit: ad626d9722f1942249197d96aa5fac3d8f7ed947
workflow-type: tm+mt
source-wordcount: '4246'
ht-degree: 1%

---


# Imagens interativas{#interactive-images}

Você pode facilmente tornar as imagens estáticas excelentes e envolventes experiências para os clientes, arrastando e soltando pontos de conexão &quot;compráveis&quot; em uma imagem. Os hotspots que podem ser comprados combinam informações adicionais sobre um produto ou serviço com um recurso direto de &quot;Adicionar ao carrinho&quot; ou &quot;Comprar&quot; no ponto de venda. Os clientes podem tocar nesses pontos de conexão que se vinculam diretamente ao produto ou serviço, adicioná-lo a um carrinho de compras ou ser vinculados a uma página da Web. Experiências diretas, como essas, aumentam o envolvimento do cliente e as conversões em seu site.

A seguir está um banner que pode ser comprado com uma janela pop-up visualização rápida. Um usuário ativa a visualização Rápida tocando no círculo ou no &quot;ponto de acesso&quot; no modelo.

![chlimage_1-152](assets/chlimage_1-368.png)

Consulte [imagens interativas em action](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion-QVzoom/index2-shoppable.html) na página da Web mostrada acima.

## Veja como os banners de imagem interativos são criados {#watch-how-interactive-image-banners-are-created}

Assista a uma apresentação de 10 minutos e 33 segundos sobre [como os banners de imagem interativos são criados](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveCarouselBanner). Você também aprenderá a pré-visualização, edição e fornecimento de banners de imagem interativos.

## Start rápido: Imagens interativas {#quick-start-interactive-images}

A seguinte descrição passo a passo do fluxo de trabalho foi projetada para ajudá-lo a iniciar e executar rapidamente com imagens interativas no AEM Assets.

Procure o cabeçalho **Example** em algumas das tarefas do Start rápido. Ele contém um breve tutorial que se baseia em um [exemplo de página da Web que ainda não tem Imagens interativas adicionadas a ele](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).



O tutorial ajuda a ilustrar as etapas da integração de imagens interativas em seu próprio site.

Etapas de imagens interativas:

1. **(Opcional) Identificação de variáveis** de hotspots. Se você usar o Adobe Experience Manager Assets e o Dynamic Media separadamente, identifique as variáveis dinâmicas usadas na implementação da visualização rápida existente. Isso garante que você possa inserir dados de ponto de acesso ao criar a imagem interativa. Consulte [(Opcional) Identificando variáveis de ponto de acesso](#optional-identifying-hotspot-variables).
No entanto, se você usar o AEM Sites, AEM eCommerce, ou ambos, essa etapa não será necessária.

1. **(Opcional) Criação de uma predefinição** do visualizador de imagens interativas. Personalize a imagem gráfica usada para representar pontos de acesso. A criação de sua própria predefinição do visualizador de Imagem interativa não é necessária se você pretende usar a predefinição do visualizador de Imagem interativa predefinida `Shoppable_Banner`.
Consulte [(Opcional) Criação de uma predefinição do visualizador de Imagem interativa](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset).

1. **Carregando um banner** de imagem. Faça upload de banners de imagem que deseja tornar interativos.
Consulte [Carregar um banner de imagem](#uploading-an-image-banner).

1. **Adicionar pontos de acesso a um banner** de imagem. Adicione um ou mais pontos de acesso a um banner de imagem. Associe cada um a uma ação, como um hiperlink, uma visualização rápida ou um fragmento de experiência. Depois de adicionar pontos de acesso, você concluirá essa tarefa publicando a imagem interativa.
Consulte [Adicionar pontos de acesso a um banner de imagem](#adding-hotspots-to-an-image-banner).
Consulte [Pré-visualização de imagens interativas](#optional-previewing-interactive-images) - Opcional. Se desejar, você pode visualização uma representação do banner que pode ser comprado e testar sua interatividade.
Consulte [Publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar ativos de imagem interativos.

1. **Adicionar uma imagem interativa ao seu site ou ao seu site no Experience Manager**. Se você usar Sites, eCommerce ou ambos, poderá adicionar imagens interativas diretamente a uma página da Web no Experience Manager. Arraste o componente de Mídia interativa até a página. Consulte [Adicionar ativos Dynamic Media a páginas.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
Se você usar o Experience Manager Assets e o Dynamic Media de forma independente, copie o código incorporado em seu site. Em seguida, integre-o à sua visualização Rápida existente. Consulte [Integrar uma imagem interativa ao seu site](#integrating-an-interactive-image-with-your-website).
Se você usar um WCM de terceiros (Web Content Manager), integre o novo vídeo interativo com a visualização Rápida existente usada em seu site. Consulte [Integrar uma imagem interativa a uma visualização Rápida existente](#integrating-an-interactive-image-with-an-existing-quickview).

## (Opcional) Identificação de variáveis de hotspot {#optional-identifying-hotspot-variables}

>[!NOTE]
>
>Essa tarefa só é necessária se as seguintes condições forem verdadeiras:
>
>* Você deseja adicionar interatividade à imagem, acionando para visualizações rápidas.
>* Sua implementação do Experience Manager *e não* usa uma estrutura de integração de eCommerce para inserir dados de produto no Experience Manager a partir de qualquer solução de eCommerce. Essas soluções incluem IBM WebSphere® Commerce, Elastic Path, hybris ou Intershop.

>
>
Se sua implementação do AEM usar o eCommerce, você poderá pular essa tarefa e seguir para a próxima tarefa.

Start, identificando as variáveis dinâmicas usadas pela implementação da visualização Rápida existente para que você possa digitar os dados do ponto de acesso para criar a imagem interativa.

Quando você adiciona pontos de acesso a uma imagem de banner nos ativos Experience Manager, atribua um SKU (Stock Keeping Unit). O SKU é um identificador exclusivo para cada produto ou serviço distinto que você oferta. Além disso, adicione quaisquer variáveis opcionais adicionais a cada ponto de conexão. Essas variáveis de ponto de conexão são usadas posteriormente para corresponder a pontos de conexão com conteúdo de visualização rápida.

É importante identificar corretamente o número e o tipo de variáveis a serem associadas aos dados dos pontos de conexão. Cada ponto de conexão adicionado a uma imagem de banner deve ter informações suficientes para identificar inequivocamente o produto no sistema de backend existente.

Existem diferentes maneiras de identificar um conjunto de variáveis a serem usadas para dados de pontos de conexão.

Às vezes, basta consultar os especialistas de TI responsáveis pela implementação da visualização Rápida. Essas pessoas provavelmente saberão qual é o conjunto mínimo de dados necessário para identificar a visualização rápida no sistema. No entanto, também é possível simplesmente analisar o comportamento existente do código front-end.

A maioria das implementações de visualização rápida usa o seguinte paradigma:

* O usuário ativa um elemento da interface do usuário no site. Por exemplo, ao clicar em um botão &quot;visualização rápida&quot;.
* O site envia uma solicitação do Ajax para o backend para carregar os dados ou o conteúdo da visualização rápida, se necessário.
* Os dados de visualização rápida são traduzidos para o conteúdo em preparação para renderização na página da Web.
* Por fim, o código front-end exibe visualmente esse conteúdo na tela.

A abordagem então é visitar diferentes áreas do site existente onde o recurso visualização rápida é implementado. Em seguida, dispare a visualização Rápida e capture o URL Ajax enviado pela página da Web para carregar os dados ou o conteúdo da visualização Rápida.

Normalmente, não é necessário usar nenhuma ferramenta de depuração especializada. Os navegadores da Web modernos dispõem de inspetores da Web que fazem um trabalho adequado. A seguir estão alguns exemplos de navegadores da Web que incluem inspetores da Web:

* Para ver todas as solicitações HTTP de saída no Google Chrome, pressione F12 para abrir o painel Ferramentas do desenvolvedor e clique na guia Rede.
No Mac, pressione Command+Option+I para abrir o painel Ferramentas do desenvolvedor e clique na guia Rede.

* No Firefox, você pode ativar o plug-in Firebug pressionando a tecla F12 e usando sua guia Net (Rede). Ou você pode usar a ferramenta Inspetor integrada e sua guia Rede.
No Mac, pressione Command+Option+I para abrir o painel Ferramentas do desenvolvedor e clique na guia Inspetor.

Quando o monitoramento de rede estiver ativado no navegador, dispare a visualização Rápida na página.

Agora, encontre o URL Ajax de visualização rápida no registro de rede e copie o URL gravado para análises futuras. Normalmente, quando você aciona a visualização Rápida, há várias solicitações que são enviadas para o servidor. Normalmente, o URL Ajax de visualização rápida é um dos primeiros na lista. Ele tem uma parte ou um caminho complexo de cadeia de caracteres de query, e seu tipo MIME de resposta é `text/html`, `text/xml` ou `text/javascript`.

Durante esse processo, é importante visitar diferentes áreas do seu site, com diferentes categorias e tipos de produtos. O motivo é que os URLs de visualização rápida podem ter partes comuns para uma determinada categoria do site. No entanto, elas são alteradas somente se você visitar uma área diferente do site.

No caso mais simples, a única parte variável no URL de visualização rápida é o SKU do produto. Nesse caso, o valor SKU é o único dado necessário para adicionar pontos de acesso à imagem do banner.

No entanto, em casos complexos, o URL de visualização rápida tem elementos variáveis diferentes além do SKU. Por exemplo, elementos variáveis podem incluir ID de categoria, código de cor e código de tamanho. Nesses casos, cada elemento é uma variável separada na definição dos dados do ponto de acesso no recurso de imagem interativa que pode ser comprado nos Ativos do Experience Manager.

Considere os seguintes exemplos de URLs de visualização rápida e suas variáveis de ponto de acesso resultantes:

<table>
  <tbody>
  <tr>
    <td><p>SKU único, encontrado na string do query.</p> </td>
    <td><p>Os URLs de visualização rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>A única parte variável no URL é o valor do parâmetro da string de query productId= e é claramente um valor SKU. Portanto, os pontos de conexão precisam apenas de campos SKU preenchidos com valores como <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU único, encontrado no caminho do URL.</p> </td>
    <td><p>Os URLs de visualização rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>A parte variável está na última parte do caminho e se torna o valor SKU dos pontos de acesso: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID da categoria na sequência do query.</p> </td>
    <td><p>Os URLs de visualização rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>Nesse caso, há duas partes diferentes no URL. O SKU é armazenado no parâmetro <code>prodId</code> e a ID da categoria<code></code> é armazenada no parâmetro <code>category=</code>.</p> <p>Dessa forma, as definições dos pontos de conexão são pares. Ou seja, um valor de SKU e uma variável extra chamada <code>categoryId</code>. Os pares resultantes são os seguintes:</p>
    <ul>
      <li><p>O SKU é <strong><code>305466</code></strong> e <code>categoryId</code> é <code>1100004</code>.</p> </li>
      <li><p>O SKU é <strong><code>310181</code></strong> e <code>categoryId</code> é <strong><code>1100004</code></strong>.</p> </li>
      <li><p>O SKU é <strong><code>308706</code></strong> e <code>categoryId</code> é <strong><code>1740148</code></strong>.</p> </li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Exemplo**

Você pode aplicar a mesma abordagem usada nos três exemplos acima à [página da Web de demonstração](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html).

A página da Web de demonstração tem várias miniaturas de produtos, cada uma com um botão de visualização rápida chamado &quot;Ver mais&quot;. Com a ferramenta de depuração do navegador da Web ainda ativada, clique em cada botão e observe os URLs de visualização rápida gravados. Depois de ativar as quatro visualizações rápidas de produtos disponíveis na página, você tem a seguinte lista de solicitações de visualização rápida feitas no backend:

* `/datafeed/Men-Windbreaker.json`
* `/datafeed/Men-SimpleHenley.json`
* `/datafeed/Men-CamoPullover.json`
* `/datafeed/Women-QuiltedDownJacket.json`

Analisando as chamadas do servidor, você pode ver que informações específicas do produto estão presentes apenas no caminho da solicitação. Você também observa que a sequência de caracteres do query não é usada e que há dois tipos distintos de partes de dados envolvidas:

* O primeiro tipo é Homens ou Mulheres. Você pode chamar isso de &quot;categoria do produto&quot;.
* O segundo tipo é o nome do produto, como CamoPullover, que provavelmente é o SKU do produto.

Considerando essas informações, todo o URL da visualização Rápida tem o seguinte padrão:

`/datafeed/$categoryId$-$SKU$.json`

Com base nessa análise, você usaria `categoryId` e `SKU` para pontos de conexão.

Agora você está pronto para carregar um banner de imagem e adicionar pontos de acesso a ele usando o recurso de imagem interativa que pode ser comprado no AEM Assets.

## (Opcional) Criação de uma predefinição do visualizador de imagens interativas {#optional-creating-an-interactive-image-viewer-preset}

Você pode optar por usar a predefinição padrão do visualizador de Imagem interativa e pronta para uso chamada `Shoppable_Banner` que acompanha o AEM Assets. Ou você pode criar sua própria predefinição do visualizador personalizado para usar com imagens interativas.

Ao criar uma predefinição personalizada do visualizador de Imagem interativa, você pode determinar a aparência dos pontos de acesso no banner de imagem. Como parte da criação da predefinição do visualizador, você pode optar por usar um gráfico de ponto de acesso de uma galeria de imagens predefinidas.

Depois de salvar a predefinição do visualizador, ela é ativada automaticamente (ativada) na página lista predefinida do visualizador no AEM Assets. Essa funcionalidade significa que é visível no componente de Mídia interativa e sempre que você visualização um ativo. Entretanto, para *fornecer* um banner interativo com essa predefinição do visualizador, *publique* também sua predefinição do visualizador. Essa regra é verdadeira para predefinições de visualizador personalizadas ou predefinidas.

**Para criar uma predefinição do visualizador de Imagem interativa**

1. No painel esquerdo, toque em **[!UICONTROL Ferramentas > Ativos > Predefinições do visualizador]**.
1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Criar]**.
1. Na caixa de diálogo Nova predefinição do visualizador, digite um nome para descrever a predefinição do visualizador de banner interativo.

   Este título é exibido na página lista Predefinição do visualizador depois que você salvar.

1. No menu suspenso Rich Media Type (Tipo de mídia avançada), selecione **[!UICONTROL Imagem interativa]**.
1. Toque em **[!UICONTROL Criar]**.
1. Na página Editar predefinição do visualizador, toque na guia **[!UICONTROL Aparência]**.
1. Faça uma das seguintes opções:

   * Para carregar sua própria imagem de ponto de acesso que você deseja usar nas imagens, toque no ícone Seletor de ativos. Na página Selecionar conteúdo, navegue até a imagem do ponto de acesso que deseja usar e selecione-a. Toque no ícone Marca de seleção no canto superior direito.
   * Para selecionar uma imagem de ponto de acesso predefinida, toque no ícone Galeria de pontos de acesso. Na paleta Galeria de pontos de acesso, toque na imagem do ponto de acesso que deseja usar.

1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Salvar]**.

   Certifique-se de publicar a nova predefinição do visualizador.

   Consulte [Predefinições do Visualizador de Publicação](/help/assets/dynamic-media/managing-viewer-presets.md#publishing-viewer-presets).

   Agora você está pronto para carregar um banner de imagem.

## Carregando um banner de imagem {#uploading-an-image-banner}

Se você já carregou as imagens que deseja usar, avance para a próxima etapa, [Adicionar pontos de acesso a um banner de imagem](#adding-hotspots-to-an-image-banner).

**Para carregar um banner de imagem**

1. Faça upload de banners de imagem que deseja tornar interativos.

   Consulte [Carregar ativos](/help/assets/manage-digital-assets.md#uploading-assets).

   Agora você está pronto para adicionar pontos de acesso ao banner de imagem; veja a próxima tarefa abaixo.

## Adicionar pontos de acesso a um banner de imagem {#adding-hotspots-to-an-image-banner}

Você pode adicionar pontos de acesso a um banner de imagem usando o editor na página Gerenciamento de pontos de conexão.

Quando você adiciona pontos de acesso, pode defini-los como uma exibição pop-up de visualização rápida, como um hiperlink ou um Fragmento de experiência.

Consulte [Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
>
>As ferramentas de compartilhamento de mídia social na Imagem interativa não são suportadas quando você incorpora o visualizador em um Fragmento de experiência. Em vez disso, use ou crie predefinições do visualizador que não tenham ferramentas de compartilhamento de mídia social. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.

As opções Desfazer e Refazer, perto do canto superior direito da página, são suportadas durante a sessão atual de criação/edição.

Ao terminar de criar sua imagem interativa, você pode usar a Pré-visualização para ver uma representação de como sua imagem interativa aparece para os clientes.

Consulte [(Opcional) Visualização de imagens interativas](#optional-previewing-interactive-images).

>[!NOTE]
>
>Quando você adiciona pontos de acesso a uma imagem em uma imagem interativa ou em um banner de carrossel, as informações do ponto de acesso são armazenadas no mesmo local de metadados. Esse local é relativo ao local da imagem, independentemente de ser uma imagem interativa ou um banner de carrossel. Essa funcionalidade significa que você pode reutilizar facilmente a mesma imagem - juntamente com seus dados de ponto de acesso definidos - em qualquer um dos visualizadores.
Esteja ciente, no entanto, de que os Carousel Banners oferecem suporte para mapas de imagem em imagens que também podem conter pontos de conexão; uma imagem interativa não. Lembre-se disso se você pretende criar uma imagem interativa ou um banner de carrossel que use a mesma imagem. Você pode criar Imagens interativas e Banners de carrossel usando cópias separadas da mesma imagem.
Consulte também [Banners do carrossel](/help/assets/dynamic-media/carousel-banners.md).

>[!NOTE]
Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, seus pontos de acesso serão removidos.

**Para adicionar pontos de acesso a um banner de imagem**

1. Na visualização Ativos, navegue até o banner de imagem que deseja tornar interativo.
1. Faça uma das seguintes opções:

   * Passe o cursor do mouse sobre a imagem e toque em **[!UICONTROL Select]** (ícone de marca de seleção). Na barra de ferramentas, toque em **[!UICONTROL Editar]**.

   * Passe o cursor do mouse sobre a imagem e toque em **[!UICONTROL Mais ações]** (ícone de três pontos) **[!UICONTROL > Editar]**.

   * Para abri-la na página Visualização de detalhes, toque na imagem. Na barra de ferramentas, toque em **[!UICONTROL Editar]**.

1. Próximo ao canto superior esquerdo da página, toque em **[!UICONTROL Adicionar ponto de acesso]** (ícone de toque com o dedo) para abrir a página Gerenciamento de ponto de acesso.
1. Próximo ao canto superior esquerdo da página, toque em **[!UICONTROL Ponto de acesso]**.

   1. Próximo ao canto superior esquerdo da página Gerenciamento de hotspots, toque em **[!UICONTROL Hotspot]**.
   1.  Na imagem, toque em um local onde deseja que o ponto de acesso apareça. Se necessário, arraste o ponto de conexão para ajustar sua localização. Ou use as teclas de seta do teclado para controlar a posição de um ponto ativo selecionado.
   1. Adicione mais hotspots, conforme necessário, repetindo as etapas a e b.
   1. (Opcional) Para excluir um ponto de acesso, selecione-o na imagem e toque em **[!UICONTROL Excluir]** (ícone de lixeira) no cabeçalho **[!UICONTROL Pontos de acesso]**.

1. No campo de texto Nome, digite o nome do ponto de acesso. Esse nome também aparece na lista suspensa Ponto de acesso selecionado.
1. Faça uma das seguintes opções:

   * Toque em **[!UICONTROL visualização rápida]**.

      * Se você for um cliente da AEM Sites ou do eCommerce, toque ou clique no ícone Seletor de produto (lupa) para abrir a página Selecionar produto. Toque no produto que deseja usar e toque em **Selecionar** no canto superior direito da página. Você será redirecionado para a página de gerenciamento do Hotspot.
      * Se você for *não* um cliente Experience Manager Sites ou eCommerce

         * Consulte [Identificação de variáveis de hotspot](#optional-identifying-hotspot-variables); você deve definir essas variáveis.
         * Em seguida, insira manualmente o valor SKU. No campo de texto Valor SKU, digite o SKU do produto. O valor SKU inserido preenche automaticamente a parte variável do modelo de visualização Rápida. Ela garante que o sistema saiba associar o ponto de conexão tocado à visualização rápida de um SKU específico.
         * (Opcional) Se houver outras variáveis na visualização Rápida usadas para identificar um produto, toque em **[!UICONTROL Adicionar variável genérica]**. No campo de texto, especifique uma variável extra. Por exemplo, `category=Mens` é uma variável adicionada.
   * Toque em **[!UICONTROL Hiperlink]**.

      * Se você for um cliente do Experience Manager Sites, toque no ícone Seletor de site (pasta). Navegue até um URL. O método baseado em URL de vinculação não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas de Sites de Experience Manager.
      * Se você for um cliente independente, no campo de texto HREF, especifique o caminho do URL completo para uma página da Web vinculada.

   Certifique-se de especificar se deseja abrir o link em uma nova guia do navegador (padrão recomendado) ou na mesma guia.

   Consulte [Trabalhando com seletores](/help/assets/dynamic-media/working-with-selectors.md) para obter mais informações.

   * Toque em **[!UICONTROL Fragmento de experiência]**.

      * Se você for um cliente da AEM Sites, toque ou clique no ícone Pesquisar (lupa) para abrir a página Fragmento de experiência. Toque no Fragmento de experiência que deseja usar. Em seguida, toque em **[!UICONTROL Select]** no canto superior direito da página. Você será redirecionado para a página de gerenciamento do Hotspot.
Consulte [Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

      * Especifique a largura e a altura do Fragmento de experiência como deseja que ele apareça no banner.

         >[!NOTE]
         As ferramentas de compartilhamento de mídia social na Imagem interativa não são suportadas quando você incorpora o visualizador em um Fragmento de experiência. Em vez disso, use ou crie predefinições do visualizador que não tenham ferramentas de compartilhamento de mídia social. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.



1. Toque em **[!UICONTROL Salvar]** para salvar seu trabalho e retornar à página Procurar.
1. Publique a imagem interativa. A publicação fornece o banner pela nuvem e também gera código incorporado que permite a integração com um site de terceiros.

   Consulte [Publicar ativos](/help/assets/manage-digital-assets.md#publish-assets).

   Depois de adicionar pontos de acesso e publicar a imagem interativa, você está pronto para adicioná-la ao seu site existente.

   Consulte [Integrar uma imagem interativa ao seu site](#integrating-an-interactive-image-with-your-website).

   >[!NOTE]
   Se você estiver editando imagens interativas com pontos de acesso e recortar a imagem, seus pontos de acesso serão excluídos.

### (Opcional) Visualização de imagens interativas {#optional-previewing-interactive-images}

Você pode usar a Pré-visualização para ver uma representação da aparência da imagem interativa para os clientes. A pré-visualização também permite que você teste os pontos de conexão da imagem para garantir que eles se comportem como esperado.

Quando estiver satisfeito com a imagem interativa, você poderá publicá-la.
Consulte [Incorporar o Visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md).
Consulte [Vincular URLs ao seu aplicativo da Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). O método baseado em URL de vinculação não é possível se o conteúdo interativo tiver links com URLs relativos, principalmente links para páginas do AEM Sites.
Consulte [Adicionar ativos Dynamic Media a páginas.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

**Para pré-visualização de imagens interativas**

1. Na visualização Ativos, navegue até uma imagem interativa existente que você criou e toque para abri-la na Pré-visualização.
1. Próximo ao canto superior esquerdo da página de Pré-visualização, na lista suspensa Conteúdo, toque em **[!UICONTROL Visualizadores]**.
1. Na lista Visualizadores, toque em **[!UICONTROL Shoppable_Banner]** ou no nome da predefinição do visualizador de imagens interativo que você criou.
1. Para testar as ações associadas de pontos de acesso, toque em pontos de acesso na imagem.

## Publicar ativos de imagem interativos {#publishing-interactive-image-assets}

Consulte [Publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar ativos de imagem interativos.

## Integração de uma imagem interativa com seu site {#integrating-an-interactive-image-with-your-website}

Depois de carregar uma imagem de banner, adicionar pontos de acesso a ela e publicar a imagem interativa, você estará pronto para adicioná-la à página do site.

Se você for um cliente da AEM Sites, poderá adicionar a imagem interativa arrastando o componente de Mídia interativa para a página. Consulte [Adicionar ativos Dynamic Media a páginas.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

Se você for um cliente independente da AEM Assets, poderá adicionar manualmente a imagem interativa ao seu site, conforme descrito nesta seção.

1. Copie o código incorporado da imagem interativa publicada.
Consulte [Incorporar o Visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md).

1. Adicione o código incorporado copiado no local desejado na página da Web.
O código incorporado copiado é definido para um ambiente responsivo para que ele se ajuste automaticamente à área atribuída.

**Exemplo**

Usando o site de demonstração [como exemplo](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-0.html), observe que a imagem dos três homens é uma tag `IMG` estática:

```xml
<img class="img-responsive" width="100%" title="Hero Image 2" alt="Hero Image 2" src="images/shoppable-banner.jpg">
```

A integração é tão simples quanto remover a tag `IMG` e substituí-la pelo código incorporado copiado da AEM Assets. Você pode ver que o resultado [mostra a imagem interativa que pode ser comprada na página com três pontos de acesso circulares](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-1.html).

>[!NOTE]
Como esse ponto, os pontos de conexão na imagem interativa que pode ser comprada do site de demonstração são apenas para fins de exibição. Eles ainda não estão integrados às visualizações rápidas existentes.

Para aplicar um &quot;recorte&quot; a uma imagem interativa que pode ser comprada para um ambiente responsivo, inclua o atributo de configuração de Imagem interativa `ZoomView.iscommand` no caminho. Nesse caso, o componente `ZoomView` é chamado e `iscommand` é o comando &quot;cortar&quot; o serviço de imagem que você aplica.

Consulte [Atributo de configuração ZoomView.iscommand](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/command-reference-configuration-attributes-interactive-images/r-html5-aem-interactive-image-config-attrib-zoomview-iscommand.html).

Consulte [comando de serviço de imagem ](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-crop.html).

Agora você está pronto para integrar a imagem interativa com uma visualização rápida existente em seu site.

## Integração de uma imagem interativa com uma visualização Rápida existente {#integrating-an-interactive-image-with-an-existing-quickview}

>[!NOTE]
Esta tarefa só se aplica se você for um cliente independente da AEM Assets.

A última etapa desse processo é integrar a imagem interativa com uma implementação de visualização rápida existente em seu site. Não há solução para a integração que funcione para todos os casos. Toda implementação de visualização rápida é exclusiva e é necessária uma abordagem específica. Como tal, envolver a assistência de uma pessoa de TI de front-end é útil.

A implementação da visualização Rápida existente normalmente representa uma cadeia de ações inter-relacionadas que ocorrem na página da Web na seguinte ordem:

1. Um usuário aciona um elemento na interface do usuário do seu site.
1. O código front-end obtém um URL de visualização Rápida com base no elemento da interface do usuário que foi acionado na etapa 1.
1. O código de front-end envia uma solicitação do Ajax usando o URL obtido na etapa 2.
1. A lógica de backend retorna os dados ou o conteúdo da visualização rápida correspondentes de volta ao código de front-end.
1. O código front-end carrega os dados ou o conteúdo da visualização rápida.
1. Como opção, o código front-end converte os dados de visualização rápida carregados em uma representação HTML.
1. O código front-end exibe uma caixa de diálogo modal ou um painel e renderiza o conteúdo HTML na tela do usuário final.

Essas chamadas não representam necessariamente chamadas de API públicas independentes chamadas pela lógica da página da Web de uma etapa arbitrária. Em vez disso, é uma chamada encadeada na qual cada próxima etapa está oculta na última fase (retorno de chamada) da etapa anterior.

Quando a imagem interativa que pode ser comprada está substituindo a etapa 1 e, parcialmente, a etapa 2, um usuário toca em um ponto de acesso dentro da imagem que pode ser comprada. Essa interação do usuário é feita pelo visualizador. O visualizador retorna um evento para a página da Web que contém todos os dados de ponto de acesso adicionados anteriormente ao AEM Assets.

Nesse manipulador de eventos, o código front-end faz o seguinte:

* Escuta um evento emitido pela imagem interativa que pode ser comprada.
* Constrói um URL de visualização rápida com base nos dados do ponto de acesso.
* Aciona o processo de carregamento da visualização Rápida do backend e renderização na tela para exibição.

O código incorporado retornado pelo Experience Manager Assets tem um manipulador de eventos pronto para uso que é comentado, como visto no trecho de código destacado a seguir:

```xml
        var s7interactiveimageviewer = new s7viewers.InteractiveImage({
            "containerId" : "s7interactiveimage_div",
            "params" : {
                "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
                "contenturl" : "https://aodmarketingna.assetsadobe.com/",
                "config" : "/etc/dam/presets/viewer/Shoppable_Media",
                "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
        })
        /* // Example of interactive image event for Quickview.
             s7interactiveimageviewer.setHandlers({
                "quickViewActivate": function(inData) {
                    var sku=inData.sku; //SKU for product ID
                    //To pass other parameter from the hotspot, you will need to add custom parameter during the hotspot setup as parameterName=value
                    loadQuickView(sku); //Replace this call with your Quickview plugin
                    //Please refer to your Quickviewer plugin for the Quickview call
                 },
             });
        */
        s7interactiveimageviewer.init();
```

Portanto, é necessário remover as barras de comentário do código e substituir o corpo do manipulador de simulação pelo código específico da página da Web em particular.

O processo de construção do URL de visualização Rápida é o oposto do processo usado para identificar as variáveis de ponto de acesso abordadas anteriormente.

Consulte [Identificando variáveis de ponto de acesso](#optional-identifying-hotspot-variables).

Usando os exemplos anteriores de URL de visualização rápida, você pode ver nos seguintes exemplos como o URL de visualização rápida é construído em cada caso:

<table>
 <tbody>
  <tr>
   <td><p>SKU único, encontrado na string do query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU único, encontrado no caminho do URL</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
   <td><p>SKU e ID de categoria na sequência de query</p> </td>
   <td><code class="code">s7interactiveimageviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
 </tbody>
</table>

A última etapa para acionar o URL de visualização rápida e ativar o painel visualização rápida requer a assistência de uma pessoa de TI front-end de sua empresa. Eles têm conhecimento para saber melhor como acionar com precisão a implementação da visualização Rápida a partir da etapa correta, tendo um URL de visualização Rápida pronto para uso.

Você pode ver como essas etapas são aplicadas ao site de demonstração para integrar totalmente uma imagem interativa que pode ser comprada com o código de visualização rápida. Anteriormente, a estrutura do URL de visualização Rápida era identificada como a seguinte:

```xml
/datafeed/$categoryId$-$SKU$.json
```

Para reconstruir esse URL dentro do manipulador `quickViewActivate`, você pode usar os campos `categoryId` e `SKU`. Esses campos estão disponíveis no objeto `inData` que é passado ao manipulador pelo código do visualizador:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

O site de demonstração está acionando a caixa de diálogo visualização rápida usando uma chamada de função `loadQuickView()` simples. Essa função utiliza apenas um argumento, que é o URL de dados da visualização rápida. Dessa forma, a última etapa para integrar a imagem interativa que pode ser comprada é adicionar a seguinte linha de código ao manipulador `quickViewActivate`:

```xml
loadQuickView(quickViewUrl);
```

Este é o código fonte completo:

```xml
 var s7interactiveimageviewer = new s7viewers.InteractiveImage({
  "containerId" : "s7interactiveimage_div",
  "params" : {
   "serverurl" : "https://aodmarketingna.assetsadobe.com/is/image",
   "contenturl" : "https://aodmarketingna.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Media",
   "asset" : "/content/dam/mac/aodmarketingna/shoppable-banner/shoppable-banner.jpg" }
 })
   s7interactiveimageviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku;
     var categoryId=inData.categoryId;
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   });
 s7interactiveimageviewer.init();
```

O [site de demonstração final com a imagem interativa totalmente integrada](https://marketing.adobe.com/resources/help/en_US/dm/shoppable-banner/we-fashion/landing-3.html).

## Usando visualizações rápidas para criar pop-ups personalizados {#using-quickviews-to-create-custom-pop-ups}

Consulte [Usando visualizações rápidas para criar janelas pop-up personalizadas](/help/assets/dynamic-media/custom-pop-ups.md).
