---
title: Vídeos interativos
description: Saiba como trabalhar com vídeo interativo e vídeo que pode ser comprado no Dynamic Media.
feature: Vídeos interativos
role: Business Practitioner
exl-id: e4859223-91de-47a1-a789-c2a9447e5f71
source-git-commit: 8cf01af44621bec7edb7e710f0797a070d5bf6db
workflow-type: tm+mt
source-wordcount: '6021'
ht-degree: 4%

---

# Vídeos interativos{#interactive-videos}


Você pode criar facilmente vídeos interativos, conhecidos também como vídeos que podem ser comprados, que impulsionam a conversão diretamente do vídeo. O envolvimento do cliente com o vídeo ocorre em um painel ao lado do reprodutor de vídeo, onde o serviço relacionado, as informações ou as miniaturas do produto são roladas para a exibição com base no que aparece no vídeo. Os clientes podem tocar na miniatura e ser vinculados diretamente ao serviço, adicionar o item ao carrinho para compra imediata ou ser vinculados a uma página da Web para obter mais informações.

Quando o vídeo termina, um resumo visual de todas as ofertas é exibido para acionar uma chamada para a ação. Os clientes têm outra oportunidade de tocar no item desejado. Experiências acionáveis e específicas, como essas, aumentam os envolvimentos e as conversões do cliente.

Consulte também [Imagens interativas](/help/assets/dynamic-media/interactive-images.md).

## Vídeo interativo em ação {#interactive-video-in-action}

Para ver um vídeo interativo e que pode ser comprado, clique em [Demonstrações ao vivo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html), role até o cabeçalho **[!UICONTROL Mídia que pode ser comprada]** da página e clique no vídeo que pode ser comprado para iniciar a reprodução.

* Durante a reprodução, conforme os produtos são usados no vídeo, o produto idêntico aparece à direita como uma imagem em miniatura.

* Para pausar o vídeo e abrir a exibição Rápida do produto, toque na miniatura. Por exemplo, toque na imagem em miniatura de KitchenAid no vídeo para experimentar uma visualização de rotação de 360 graus do mixer ou amplie o zoom para ver os detalhes do mixer.

Consulte também [Usar vídeo interativo com Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html?lang=en#dynamic-media)

<!-- 

There was a link here that showed the video frame of an interactive video and when the reader clicked the frame the video would play https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/AXIS/index.html. This now needs to call a new interactive video

-->

<!-- 

[A frame from an interactive, shoppable video](assets/chlimage_1-126.png) *A video frame capture from an interactive, shoppable video.*

-->

>[!NOTE]
>
>Se você criar um vídeo interativo para iniciar uma página da Web quando um usuário tocar em uma imagem em miniatura, alguns dispositivos bloqueiam a abertura da página da Web pop-up. Nesses casos, altere a configuração do bloqueador de pop-ups no dispositivo. Por exemplo, em um Apple iPhone 6, toque em **[!UICONTROL Configurações > Safari > Bloquear pop-ups]** e deslize o controle para **[!UICONTROL Desligado]**. Agora, ao reproduzir um vídeo interativo e clicar em uma miniatura, você será solicitado a abrir a janela pop-up. Se você aceitar, a página da Web será aberta.

### Veja como os vídeos interativos são criados {#watch-how-interactive-videos-are-created}

Assista a uma apresentação sobre [como os vídeos interativos são criados](https://s7d5.scene7.com/s7viewers/html5/VideoViewer.html?videoserverurl=https://s7d5.scene7.com/is/content/&amp;emailurl=https://s7d5.scene7.com/s7/emailFriend&amp;serverUrl=https://s7d5.scene7.com/is/image/&amp;config=Scene7SharedAssets/Universal_HTML5_Video_social&amp;contenturl=https://s7d5.scene7.com/skins/&amp;asset=S7tutorials/InteractiveVideo)(7 minutos e 30 segundos).
(Embora a apresentação em vídeo tenha a marca Assets on Demand, os princípios e etapas ainda se aplicam a Vídeo interativo nos ativos Adobe Experience Manager.)

### Webinar de sucesso do cliente do Adobe {#adobe-customer-success-webinar}

O webinário [Usar vídeo interativo, compartilhamento de link e compartilhamento de YouTube no Experience Manager Assets](https://adobecustomersuccess.adobeconnect.com/p1yxzdo4aec/) ensina como usar o vídeo interativo e outros recursos para unir eventos orientados por conversão ao conteúdo de marketing de vídeo.

## Início rápido: Vídeos interativos {#quick-start-interactive-videos}

A seguinte descrição passo a passo do fluxo de trabalho foi criada para ajudar você a ativar e executar rapidamente com vídeos interativos no Dynamic Media.

Procure o cabeçalho **Exemplo** em algumas das tarefas de Início rápido. Ele contém um breve tutorial baseado nesta [página da Web de demonstração inicial que *não* tem interatividade adicionada a ela ainda](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html).

Os **Exemplos** ajudam a ilustrar as etapas da integração de vídeos interativos em seu próprio site.

Quando você terminar o tutorial na última seção de exemplo, [sua página da Web de demonstração final com o vídeo interativo totalmente integrado aparecerá dessa forma](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html).



Etapas de vídeo interativo:

1. **(Opcional) Identificar as variáveis**  de exibição rápida - Comece identificando as variáveis dinâmicas usadas pela implementação existente do Quick view. Você usa as variáveis para mapear miniaturas de produto para a exibição Rápida de produto correspondente ao criar o vídeo interativo. Consulte [(Opcional) Identificação das variáveis de Exibição rápida](#optional-identifying-quickview-variables).
   **Essa etapa só será necessária se todas as opções a seguir forem verdadeiras:**
 ・ Você deseja adicionar interatividade ao vídeo, acionando para Visualizações rápidas.
・ Sua implementação do Experience Manager faz 
** note uma estrutura de integração do eCommerce para inserir dados de produtos no Experience Manager a partir de qualquer solução de eCommerce, como IBM® WebSphere® Commerce, Elastic Path, SAP Hybris ou Intershop.

1. **(Opcional) Criar uma predefinição do visualizador de Vídeo interativo**  - Personalize a aparência e o comportamento de vários componentes que compõem o player, como o depurador de vídeo e as miniaturas interativas.
Não é necessário criar sua própria predefinição do visualizador de Vídeo interativo se você pretende usar as predefinições do visualizador de Vídeo interativo prontas para uso `Shoppable_Video_Light` ou `Shoppable_Video_Dark`.
Consulte [Criando uma Nova Predefinição do Visualizador](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) (opcional) e [Considerações especiais para criar uma predefinição do Visualizador Interativo](/help/assets/dynamic-media/managing-viewer-presets.md#special-considerations-for-creating-an-interactive-viewer-preset).

1. **Carregar um vídeo e seus ativos de imagem associados**  - Carregue um vídeo e imagens associadas que você deseja tornar interativas.
Consulte [Fazer upload de um vídeo e seus ativos de miniatura associados](#uploading-a-video-and-its-associated-thumbnail-assets).

1. **Adicionar interatividade ao vídeo**  - Adicione um ou mais segmentos de tempo ao vídeo. Em seguida, associe as miniaturas de imagem nesses segmentos de tempo. Atribua cada miniatura de imagem a uma ação, como um hiperlink, uma Exibição rápida ou um Fragmento de experiência.
(O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas de Experience Manager Sites .)
Termine publicando os ativos interativos de vídeo. A publicação cria o código incorporado ou URL que você eventualmente copia e aplica à página de aterrissagem do site. Consulte [Adicionar interatividade ao vídeo](#adding-interactivity-to-your-video).
Consulte [Publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. **Adicione um vídeo interativo ao seu site ou ao seu site no Experience Manager**  - Se você usar o Experience Manager Sites ou eCommerce, ou ambos, adicione o vídeo interativo a uma página da Web no Experience Manager. Arraste o componente Mídia interativa para a página. Consulte [Adicionar ativos Dynamic Media às páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).
Use o código incorporado ou URL para integrar seu vídeo interativo com as experiências do site. Consulte [Integrar um vídeo interativo com seu site](#integrating-an-interactive-video-with-your-website).
Se você estiver usando um WCM (Web Content Manager, Gerenciador de conteúdo da Web) de terceiros, é necessário integrar o novo vídeo interativo à implementação do Quick View existente usada em seu site. Consulte [Integração de um vídeo interativo com uma visualização rápida existente](#integrating-an-interactive-video-with-an-existing-quickview).
   [Adição de ativos de Mídia dinâmica a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

## (Opcional) Identificação de variáveis de Exibição rápida {#optional-identifying-quickview-variables}

>[!NOTE]
Essa tarefa só será necessária se o seguinte for verdadeiro:
* Você deseja adicionar interatividade ao vídeo, acionando para as visualizações rápidas.
* Sua implementação do Experience Manager *not* usa uma estrutura de integração de eCommerce para inserir dados de produtos no Experience Manager a partir de qualquer solução de eCommerce, como IBM® WebSphere® Commerce, Elastic Path, SAP Hybris ou Intershop. <!-- See [eCommerce concepts in Experience Manager Assets](/help/sites-administering/concepts.md).-->

Se sua implementação do Experience Manager usar o eCommerce, você poderá ignorar esta tarefa e prosseguir para a próxima tarefa.

Comece identificando as variáveis dinâmicas usadas pela implementação do Quick view existente, para que seja possível mapear as miniaturas do produto para a exibição Rápida do produto correspondente durante o processo de criação do vídeo interativo.

Ao adicionar segmentos de tempo a um vídeo, você atribui um SKU (Stock Keeping Unit) e quaisquer variáveis adicionais a cada miniatura que você adicionar a um segmento. Essas variáveis são usadas posteriormente para exibir o produto de exibição Rápida correto.

É importante identificar corretamente quais variáveis são necessárias para acionar exclusivamente uma exibição rápida do produto.

Às vezes, basta consultar especialistas de TI responsáveis pela implementação do Quick view. Eles provavelmente conhecerão o conjunto mínimo de dados que identifica a visualização rápida no sistema. No entanto, é possível simplesmente analisar o comportamento existente do código front-end.

A maioria das implementações da Exibição rápida usa o seguinte paradigma:

* O usuário ativa um elemento da interface do usuário no site. Por exemplo, clicar em um botão &quot;Exibição rápida&quot;.
* O site envia uma solicitação do Ajax para o backend para carregar os dados ou o conteúdo da Exibição rápida, se necessário.
* Os dados da Exibição rápida são traduzidos para o conteúdo em preparação para renderização na página da Web.
* Por fim, o código front-end renderiza visualmente esse conteúdo na tela.

A abordagem, portanto, é visitar diferentes áreas de seu site existente, onde a Visualização rápida está implementada. Em seguida, acione a exibição Rápida e adquira o URL Ajax enviado pela página da Web para carregar os dados ou o conteúdo da exibição Rápida.

Normalmente, não há necessidade de usar ferramentas de depuração especializadas. Os navegadores modernos da Web apresentam inspetores da Web que fazem um trabalho adequado. A seguir estão alguns exemplos de navegadores da Web que incluem inspetores da Web:

* Para ver todas as solicitações HTTP de saída no Google Chrome, pressione **F12** (Windows®) ou **Command+Options+I** (Mac) para abrir o painel Ferramentas do desenvolvedor e clique na guia **Rede**.

* No Firefox, você pode ativar o plug-in do Firebug pressionando **F12** (Windows®) ou **Command+Option+I** (Mac) e usar a guia **[!UICONTROL Net]** ou usar a ferramenta Inspetor integrada e a guia Rede.

* No Internet Explorer, ative a ferramenta de depuração pressionando **F12**.

Quando o monitoramento de rede estiver ativado no navegador, acione a exibição Rápida na página.

Agora, encontre o URL Ajax de exibição rápida no log da rede e copie o URL registrado para análise futura. Geralmente, quando você aciona a exibição Rápida, há várias solicitações que são enviadas para o servidor. Normalmente, o URL Ajax de exibição rápida é um dos primeiros na lista. Ela tem uma parte ou um caminho complexo da sequência de consulta e seu tipo MIME de resposta é `text/html`, `text/xml` ou `text/javascript`.

Durante esse processo, é importante visitar diferentes áreas de seu site, com diferentes categorias e tipos de produtos. O motivo é que os URLs de visualização rápida têm partes comuns para uma determinada categoria de site, mas são alteradas somente se você visitar uma área diferente do site.

No caso mais simples, a única parte variável no URL de exibição rápida é o SKU do produto. Nesse caso, o valor do SKU do produto é o único dado necessário para adicionar miniaturas a um segmento de tempo no vídeo interativo no Experience Manager.

No entanto, em casos complexos, o URL de exibição rápida tem elementos variáveis diferentes além do SKU do produto, como ID de categoria e código de cor. Nesses casos, cada elemento se torna uma variável separada na definição de dados de miniatura no Experience Manager.

Considere os seguintes exemplos de URLs de visualização rápida e suas variáveis de miniatura resultantes:

<table>
  <tbody>
  <tr>
    <td><p>SKU único, encontrado na string de consulta.</p> </td>
    <td><p>Os URLs de visualização rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/json?productId=866558&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1196184&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1081492&amp;source=100</code></p> </li>
      <li><p><code>https://server/json?productId=1898294&amp;source=100</code></p> </li>
    </ul> <p>A única parte variável no URL é o valor do parâmetro da string de consulta <code>productId=</code> e é claramente um valor SKU. Portanto, as miniaturas precisam apenas de campos SKU preenchidos com valores como <strong><code>866558</code></strong>, <strong><code>1196184</code></strong>, <strong><code>1081492</code></strong>, <strong><code>1898294</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU único, encontrado no caminho do URL.</p> </td>
    <td><p>Os URLs de visualização rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/product/6422350843</code></p> </li>
      <li><p><code>https://server/product/1607745002</code></p> </li>
      <li><p><code>https://server/product/0086724882</code></p> </li>
    </ul> <p>A parte variável está na última parte do caminho e se torna o valor SKU das miniaturas de Experience Manager: <strong><code>6422350843</code></strong>, <strong><code>1607745002</code></strong>, <strong><code>0086724882</code></strong>.</p> </td>
  </tr>
  <tr>
    <td><p>SKU e ID de categoria na sequência de consulta.</p> </td>
    <td><p>Os URLs de visualização rápida gravados incluem o seguinte:</p>
    <ul>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=305466</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1100004&amp;prodId=310181</code></p> </li>
      <li><p><code>https://server/quickView/product/?category=1740148&amp;prodId=308706</code></p> </li>
    </ul> <p>Nesse caso, há duas partes variáveis no URL. O SKU é armazenado no parâmetro <code>prodId</code> e a ID da categoria é armazenada no parâmetro <code>category=</code>.</p> <p>Dessa forma, as definições de miniatura são pares. Ou seja, um valor SKU e uma variável extra chamada <code>categoryId</code>. Os pares resultantes são os seguintes:</p>
    <ul>
      <li>O SKU é <code>305466</code> e <code>categoryId</code> é <code>1100004</code></li>
      <li>O SKU é <code>310181</code> e <code>categoryId</code> é <code>1100004</code></li>
      <li>O SKU é <code>308706</code> e <code>categoryId</code> é <code>1740148</code></li>
    </ul> <p> </p> </td>
  </tr>
  </tbody>
</table>

**Exemplo**

Quando a abordagem acima é aplicada ao site de exemplo, você tem uma página da Web com várias miniaturas de produto, cada uma com um botão &quot;VER MAIS&quot;:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

Depois de ativar todas as visualizações rápidas de produto disponíveis na página, você obtém a seguinte lista de solicitações de visualização rápida feitas no back-end:

* datafeed/candles-233396346.json
* datafeed/candles-233978050.json
* datafeed/candles-234024346.json
* datafeed/candles-234024356.json
* datafeed/candles-234024359.json
* datafeed/cushions-233939848.json
* datafeed/cushions-234019477.json
* datafeed/cushions-234019483.json
* datafeed/furniture-231747479.json
* datafeed/furniture-232625621.json
* datafeed/furniture-232625626.json
* datafeed/furniture-233939810.json
* datafeed/furniture-233939825.json
* datafeed/furniture-233939828.json
* datafeed/furniture-233939853.json
* datafeed/furniture-233940334.json
* datafeed/glassware-000064007.json
* datafeed/glassware-230722193.json
* datafeed/glassware-233916550.json
* datafeed/glassware-233916597.json

Ao examinar as chamadas do servidor, as informações específicas do produto só estão presentes no caminho da solicitação. Você também percebe que a sequência de consulta não é usada e que há dois tipos distintos de partes de dados envolvidos:

* O primeiro tipo são velas, almofadas, móveis e artigos de vidro. Você pode chamar esta &quot;categoria de produto&quot;.
* O segundo tipo é o código do produto, como 233916597. Você pode assumir que é &quot;SKU do produto&quot;.

Diante dessas informações, todo o URL da visualização rápida tem o seguinte padrão:

`/datafeed/$categoryId$-$SKU$.json`

Com base nessa análise, você conclui que pode usar as duas variáveis a seguir para as miniaturas: `categoryId` e `SKU`.

Agora você está pronto para fazer upload de um vídeo e seus ativos de miniatura associados.

## (Opcional) Criação de uma predefinição do visualizador de Vídeo interativo {#optional-creating-an-interactive-video-viewer-preset}

Ignore esta tarefa e continue para a próxima se pretender utilizar os tipos predefinidos predefinidos do Visualizador de Vídeo Interativo e predefinidos `Shoppable_Video_dark` ou `Shoppable_Video_light`.

Quando uma miniatura é tocada no ambiente de criação, uma visualização da caixa de diálogo Exibição rápida é exibida.

![chlimage_1-21](assets/chlimage_1-127.png)

Opcionalmente, é possível criar sua própria predefinição personalizada do visualizador de Vídeo interativo. Você pode determinar, entre outras coisas, o estilo do reprodutor de vídeo, as miniaturas interativas e a exibição da grade de miniatura que aparece no final do vídeo.

Uma predefinição do visualizador de Vídeo interativo renderiza apropriadamente o vídeo e todos os segmentos de linha do tempo adicionados. Ele também usa um exemplo padrão de Exibição rápida quando você clica em uma miniatura de produto no modo Visualização , para que você possa testar sua interatividade antes da publicação.

Após salvar a predefinição do visualizador, seu estado é automaticamente definido como **Ativado **in na página Predefinições do visualizador. Esse estado significa que está visível no componente do Dynamic Media e sempre que você visualiza um vídeo com ele. Certifique-se de publicar manualmente a nova predefinição do visualizador.

Consulte [Criação de uma nova predefinição do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) para criar sua própria predefinição do visualizador de vídeo interativo.

## Fazer upload de um vídeo e de seus ativos em miniatura associados {#uploading-a-video-and-its-associated-thumbnail-assets}

Se você já tiver carregado seus ativos de vídeo e miniatura, continue para [Adicionar interatividade ao vídeo](#adding-interactivity-to-your-video).

Se você carregou os vídeos ou imagens errados, ou quiser excluir os vídeos ou imagens carregados que não são mais necessários, consulte [Exclusão de ativos](/help/assets/manage-digital-assets.md#delete-assets).

Para fazer upload de um vídeo e seus ativos de miniatura associados:

1. Faça upload do vídeo e dos ativos de miniatura associados à pasta ou pastas desejadas.

   Consulte [Fazer upload de ativos](/help/assets/manage-digital-assets.md).
Consulte [Fazer upload de ativos usando o agendamento de tarefas FTP](/help/assets/manage-digital-assets.md).

   Agora, adicione interatividade ao vídeo.

## Adicionar interatividade ao vídeo {#adding-interactivity-to-your-video}

Você adiciona segmentos de linha do tempo a um vídeo usando o editor visual local na página Criar vídeo interativo .

Após adicionar segmentos de linha do tempo, adicione imagens em miniatura em cada segmento. Para cada miniatura adicionada, você aplica uma ação a ela. Por exemplo, você pode aplicar uma Visualização rápida à miniatura, ou atribuir um hiperlink a ela ou um Fragmento de experiência.

Consulte [Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md).

>[!NOTE]
As ferramentas de compartilhamento de mídia social em Vídeo interativo não são compatíveis quando você incorpora o visualizador em um Fragmento de experiência. Em vez disso, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de redes sociais. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.

>[!NOTE]
O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas de Experience Manager Sites .

As opções Desfazer e Refazer, próximo ao canto superior direito da página, são compatíveis durante a sessão de criação/edição atual.

Depois de salvar o vídeo interativo, ele é aberto imediatamente na Visualização. A partir daí, você pode selecionar uma predefinição do visualizador de Vídeo interativo e reproduzir o vídeo para ver uma representação aproximada de como ele aparece para os clientes.

**Para adicionar interatividade ao vídeo:**

1. Na exibição Ativos, navegue até o vídeo que você carregou e deseja tornar interativo.
1. Faça uma das seguintes opções:

   * Passe o mouse sobre a imagem e toque em **[!UICONTROL Selecionar]** (ícone de marca de seleção). Na barra de ferramentas, toque em **[!UICONTROL Editar]**.

   * Passe o mouse sobre a imagem, em seguida, toque em **[!UICONTROL Mais ações]** (ícone de três pontos) **[!UICONTROL > Editar]**.

   * Para abri-la na página Exibição de detalhes , toque na imagem. Na barra de ferramentas, toque em **[!UICONTROL Editar]**.

1. Na página Criar vídeo interativo , siga um destes procedimentos:

   * Para começar a reproduzir o vídeo, toque no botão **[!UICONTROL Reproduzir]**. Quando um produto, serviço ou detalhe específico que você deseja destacar aparecer na exibição, toque em **[!UICONTROL Adicionar segmento]** na barra de ferramentas. Repita até chegar ao fim do vídeo.

      Para cada segmento de tempo adicionado, é possível atribuir uma ou mais imagens em miniatura a ele. Em seguida, é possível vincular essas miniaturas às páginas de produto de Visualização rápida para que os clientes comprem ou às páginas da Web para obter mais informações.

   * Para começar a reproduzir o vídeo, toque no botão **[!UICONTROL Reproduzir]**. Quando um produto, serviço ou detalhe específico que você deseja destacar for exibido, toque em **[!UICONTROL Pausar]**. Toque em **[!UICONTROL Adicionar segmento]**.

      Continue reproduzindo e pausando o vídeo em pontos da linha do tempo em que deseja adicionar um segmento até chegar ao fim do vídeo.

1. (Opcional) Arraste a barra no **[!UICONTROL controle deslizante Escala da linha do tempo]** para a esquerda para aumentar ou diminuir o zoom e para direita para diminuir o zoom. Essa ação permite controlar quantos detalhes você vê dos segmentos adicionados.

   ![chlimage_1-22](assets/chlimage_1-128.png)

   Dependendo da duração do vídeo, o padrão da Duração do segmento é os seguintes valores:

   <table>
      <tbody>
        <tr>
        <td><strong>Se a duração do vídeo for...</strong></td>
        <td><strong>O padrão da configuração Duração do segmento é...</strong></td>
        </tr>
        <tr>
        <td>3 minutos ou mais</td>
        <td>60 segundos</td>
        </tr>
        <tr>
        <td>2 a 3 minutos</td>
        <td>30 segundos</td>
        </tr>
        <tr>
        <td>1-2 minutos</td>
        <td>20 segundos<br /> </td>
        </tr>
        <tr>
        <td>30 a 60 segundos</td>
        <td>10 segundos</td>
        </tr>
        <tr>
        <td>30 segundos ou menos</td>
        <td>5 segundos</td>
        </tr>
      </tbody>
    </table>

   A linha do tempo do vídeo utiliza tantas propriedades de tela quanto o que é disponibilizado para ele. Dessa forma, ao redimensionar o navegador, os segmentos adicionados mantêm a largura correta.

   Para ilustrar, as três capturas de tela a seguir estão usando o mesmo vídeo. Observe que a largura de cada segmento muda de acordo com a configuração Escala da linha do tempo.

   ![chlimage_1-23](assets/chlimage_1-129.png)

   Captura de tela A

   Captura de tela A acima mostra a exibição padrão de um vídeo de produto de 29 segundos. A Escala da Linha do Tempo é definida como padrão de 5 segundos.

   ![chlimage_1-130](assets/chlimage_1-130.png)

   Captura de tela B

   Na Captura de tela B acima, o controle deslizante Escala da linha do tempo foi arrastado do padrão de 5 segundos para 3 segundos. Observe que os carimbos de data e hora individuais da Escala da linha do tempo agora são definidos em intervalos de 3 segundos.

   ![chlimage_1-25](assets/chlimage_1-131.png)

   Captura de tela C

   Na Captura de tela C acima, a configuração Escala da linha do tempo foi movida para 8 segundos. Observe como os segmentos que contêm miniaturas de produto foram reduzidos. Reduzir dessa maneira será útil se você tiver um vídeo longo e quiser ver uma visão geral de mais segmentos que normalmente se encaixariam na largura da página.

1. (Opcional) Siga um destes procedimentos:

   * Para ajustar a hora de início e a hora de término de um segmento.

      Selecione um segmento e arraste a oval azul à esquerda ou à direita para ajustar a hora inicial ou final, respectivamente. O quadro de vídeo exibido se move para o tempo adequado no vídeo, com base nos ajustes. O movimento do segmento da linha do tempo é restrito com base em qualquer segmento adjacente na linha do tempo. O tempo mínimo permitido do segmento é de um segundo.

      Use os seguintes atalhos de navegação para verificar e ajustar rapidamente seus segmentos de vídeo:

      * Para buscar o vídeo diretamente no início desse segmento, toque no botão azul à esquerda.
      * Para buscar o vídeo diretamente no final desse segmento, toque no botão azul à direita oval.
      * Para retornar a reprodução do vídeo ao início desse segmento, toque no segmento inteiro.

   ![chlimage_1-26](assets/chlimage_1-132.png)

   Reposicionamento do final de um segmento de linha do tempo

   * Para excluir um segmento

      Selecione o último segmento que está na linha do tempo e, na barra de ferramentas, toque em **[!UICONTROL Excluir segmento]**. Se dois ou mais segmentos forem selecionados, o recurso Excluir segmento será desativado.

      Você só pode excluir o último segmento. Por exemplo, se quiser excluir todos os segmentos na linha do tempo, sempre selecione o último, em seguida, toque em **[!UICONTROL Excluir segmento]**.


1. Selecione um segmento de tempo ao qual deseja associar uma ou mais imagens em miniatura.
1. À direita do vídeo, toque na guia **[!UICONTROL Content]**.
1. Na guia Conteúdo, toque em **[!UICONTROL Selecionar ativos]**, em seguida, navegue e selecione todos os ativos de imagem que deseja usar com o vídeo. Os ativos selecionados são adicionados ao painel Seletor de ativos na guia Conteúdo .

1. No seletor de ativos abaixo da guia Conteúdo, siga um destes procedimentos:

   <table>
      <tbody>
        <tr>
        <td>Para associar uma miniatura ao segmento de linha do tempo selecionado</td>
        <td><p>Toque na imagem no painel do seletor de ativos à direita.</p> <p>É possível adicionar quantas miniaturas quiser a um segmento de linha do tempo. Para cada imagem selecionada, uma marca de seleção aparece sobre a imagem no seletor de ativos.</p> </td>
        </tr>
        <tr>
        <td>Para remover uma miniatura do segmento de linha do tempo selecionado</td>
        <td><p>Siga um destes procedimentos:</p>
          <ul>
          <li>No painel do seletor de ativos, toque em uma imagem com uma marca de seleção para desmarcá-la. O ativo de imagem é removido do segmento da linha do tempo.<br /> </li>
          <li>No segmento da linha do tempo selecionado, toque em uma imagem e, na barra de ferramentas, toque em <strong>Excluir produto</strong>.</li>
          </ul> </td>
        </tr>
      </tbody>
    </table>

   ![Seletor de ativos](assets/chlimage_1-133.png)

   Tocar em uma imagem no painel do seletor de ativos a adiciona ao segmento de linha do tempo selecionado.

1. Selecione uma única imagem em miniatura em um dos segmentos de linha do tempo e toque na guia **[!UICONTROL Actions]**.
1. Siga um destes procedimentos:
   <table> 
    <tbody> 
      <tr> 
      <td>Para associar a imagem de miniatura selecionada a uma exibição Rápida</td> 
      <td><p>Em Tipo de ação, toque em <strong>Exibição rápida</strong>.</p> <p>Se você for um cliente do Experience Manager Sites e Ecommerce:</p> 
       <ul> 
       <li>Observe que o campo de texto Valor SKU é preenchido previamente com o SKU do produto selecionado (unidade de manutenção de estoque). O SKU é um identificador exclusivo para cada produto ou serviço distinto que você oferece. Este campo é preenchido automaticamente quando a imagem é associada a um produto no Experience Manager Commerce.</li> 
       <li>Se o SKU preenchido anteriormente estiver incorreto, toque ou clique no ícone Seletor de produto (lupa) para abrir a página Selecionar produto . Toque no produto que deseja usar e toque na marca de seleção no canto superior direito da página. Você é retornado ao Editor de vídeo interativo.</li> 
       </ul> <p> Se você for <em>not</em> um cliente Experience Manager Sites ou Ecommerce</p> 
       <ul> 
       <li>Consulte <a href="/help/assets/dynamic-media/carousel-banners.md#identifying-hotspot-and-image-map-variables">Identificação de variáveis de ponto de acesso</a>. Essas variáveis devem ser definidas.</li> 
       <li>Por padrão, esse campo SKU usa o nome de arquivo do ativo de imagem sem a extensão. Se você seguir uma convenção de nomenclatura padrão para seus arquivos com base no SKU, esse campo normalmente não exigirá edições adicionais. </li> 
       <li>Caso contrário, edite o valor padrão e insira o valor SKU correto. No campo de texto Valor SKU , digite o SKU (Stock Keeping Unit) do produto, que é um identificador exclusivo para cada produto ou serviço distinto que você oferece. O valor de SKU inserido preenche automaticamente a parte variável do modelo de Exibição rápida, de modo que o sistema saiba associar a imagem tocada à exibição rápida de um SKU específico.</li> 
       </ul> <p>(Opcional) Se houver outras variáveis na exibição Rápida que você deve usar para identificar ainda mais um produto, toque em <strong>Adicionar variável genérica</strong>. No campo de texto, especifique uma variável extra. Por exemplo, <code>category=Womens</code> é uma variável adicionada.</p> <p> </p> </td> 
      </tr> 
      <tr> 
      <td>Para associar a imagem em miniatura selecionada a um hiperlink</td> 
      <td><p>Em Tipo de ação, toque em <strong>Hiperlink</strong> e siga um destes procedimentos:</p> 
       <ul> 
       <li>Se você for um cliente do Experience Manager Sites , toque no ícone do Seletor de site (pasta) para navegar até uma página da Web. O método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas de Experience Manager Sites .</li> 
       <li>Se você for um cliente independente do Dynamic Media, no campo de texto HREF , especifique o caminho do URL completo para uma página da Web vinculada.</li> 
       </ul> <p>Certifique-se de especificar se deseja abrir o link em uma nova guia do navegador ou na guia atual.</p> </td> 
      </tr> 
      <tr> 
      <td>Para associar a imagem em miniatura selecionada a um Fragmento de experiência</td> 
      <td><p>Em Tipo de ação, toque em <strong>Fragmento de experiência</strong> e faça o seguinte:<p> 
       <ul> 
       <li>Se você for um cliente do Experience Manager Sites , toque no ícone Pesquisar (lupa) para abrir a página Fragmento de experiência . Toque ou clique no Fragmento de experiência que deseja usar e toque em <strong>Para retornar ao painel Ações na página anterior, selecione </strong>no canto superior direito da página.<br /> Consulte Fragmentos  <a href="/help/sites-cloud/authoring/fundamentals/experience-fragments.md">de experiência</a>.</li> 
      </ul> 
       <ul> 
       <li>Especifique a largura e a altura do Fragmento de experiência como ele aparece no vídeo.</li>
       </ul><strong>Observação</strong>: As ferramentas de compartilhamento de mídia social em Vídeo interativo não são compatíveis quando você incorpora o visualizador em um Fragmento de experiência. Em vez disso, você pode usar ou criar predefinições do visualizador que não tenham ferramentas de compartilhamento de redes sociais. Essas predefinições do visualizador permitem que você as incorpore com êxito aos Fragmentos de experiência.</p></tr>&lt;&gt; 
      <tr> 
      <td>Para editar uma ação já atribuída a uma imagem em miniatura</td> 
      <td>Em um segmento de linha do tempo, toque em uma imagem em miniatura que tenha um link de cadeia à direita de seu rótulo de texto. O link de cadeia indica que uma ação foi atribuída a ela. Para fazer suas alterações, toque na guia <strong>Actions</strong>.</td> 
      </tr> 
      <tr> 
      <td>Para alterar o rótulo de texto de uma imagem em miniatura</td> 
      <td><p>Por padrão, o rótulo do texto usa o campo de metadados <code>Title</code> da imagem em miniatura. Se <code>Title</code> não estiver presente, o nome de arquivo da imagem em miniatura será usado, mas sem a extensão .</p> <p>Para alterar o rótulo do texto de uma imagem em miniatura, na guia <strong>Actions </strong>, logo abaixo do ativo de imagem exibido, insira o texto desejado. Veja a imagem abaixo.</p> <p>O novo rótulo de texto é usado somente pelo próprio reprodutor de vídeo e o texto em miniatura exibido no segmento da linha do tempo. A alteração no rótulo não afeta o campo de metadados Título da imagem em miniatura nem seu nome de arquivo.</p> </td> 
      </tr> 
      <tr> 
      <td>Para reverter uma alteração</td> 
      <td>Próximo ao canto superior direito da página, toque em <strong>Desfazer</strong> ou <strong>Refazer</strong>.</td> 
      </tr> 
    </tbody> 
   </table>

   ![experiencefragment_interactivevideos](assets/experiencefragment_interactivevideos.png)

   Um novo rótulo de texto é adicionado à imagem em miniatura.

1. Faça uma das seguintes opções:

   * Repita as etapas 6 a 11 para adicionar mais imagens em miniatura a segmentos de linha do tempo no vídeo.
   * Prossiga para a etapa opcional 13.

1. (Opcional) Siga um destes procedimentos:

   * **[!UICONTROL Mesclar segmentos]**  - é possível combinar dois segmentos adjacentes (com ou sem miniaturas de produto atribuídas a eles) em um segmento.

      Na linha do tempo, toque em dois ou mais segmentos contíguos que deseja mesclar em um. Não há alças de arrastar ovais azuis nos dois segmentos selecionados na imagem abaixo.

      Toque em **[!UICONTROL Unir segmento]** na barra de ferramentas.
   ![chlimage_1-134](assets/chlimage_1-134.png)

   Mesclar dois segmentos selecionados de cinco segundos em um segmento de dez segundos.

   * **[!UICONTROL Dividir segmento]**  - é possível dividir um único segmento em dois segmentos igualmente cronometrados. Se houver miniaturas de produto já atribuídas ao segmento, elas serão combinadas no segmento esquerdo.

      Na linha do tempo, toque em um segmento que deseja dividir ao meio e em **[!UICONTROL Dividir segmento]** na barra de ferramentas.

      Selecionar dois ou mais segmentos desativa o recurso **[!UICONTROL Dividir segmento]**.
   ![chlimage_1-133](assets/chlimage_1-135.png)

   Divisão de um segmento selecionado de dez segundos em dois segmentos de cinco segundos cada.

1. Próximo ao canto superior direito da página **[!UICONTROL Criar vídeo interativo]**, o nome da predefinição do visualizador selecionado no momento, usada com o vídeo, é exibido. Para selecionar uma predefinição do visualizador diferente, toque no nome.

   Por exemplo, a predefinição do visualizador `Shoppable_Video_light` permite reproduzir o vídeo com uma área de exibição branca ao lado do vídeo. A área de exibição é onde as imagens em miniatura clicáveis são exibidas durante a reprodução. A predefinição do visualizador `Shoppable_Video_dark` permite reproduzir o vídeo com uma área de exibição preta ao lado do vídeo.

   Se você criou sua própria predefinição do visualizador de Vídeo interativo, é possível visualizá-la na lista de predefinições que você pode escolher.

   Quando terminar, toque em **[!UICONTROL Salvar]**.

   >[!NOTE]
   Ao salvar o vídeo interativo, um arquivo associado é automaticamente salvo com ele. `.vtt` O arquivo `.vtt` é salvo na pasta `_VTT` na raiz de **[!UICONTROL Assets]**. O arquivo e a pasta são necessários para que o vídeo interativo seja reproduzido corretamente no site. Sendo assim, não mova, edite ou exclua a pasta `_VTT` ou seu conteúdo.

1. Publique o vídeo interativo. A publicação cria o código incorporado ou URL que você eventualmente copia e cola nas experiências do site.

   Se você adicionou interatividade com visualizações rápidas, use somente o código de inserção; se você tiver adicionado a interatividade com páginas da Web com hiperlink, também poderá usar o URL publicado. Observe, no entanto, que o método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas de Experience Manager Sites .

   Consulte [Publicação de ativos](publishing-dynamicmedia-assets.md).

   >[!NOTE]
   Para publicar um vídeo que pode ser comprado com visualizações rápidas, certifique-se de publicar também cada um dos ativos de imagem relacionados do vídeo de sua área de comércio, separadamente.

   Depois de adicionar segmentos de linha do tempo e publicar o vídeo interativo, você estará pronto para adicioná-lo à página de aterrissagem do site. Consulte [Integrar um vídeo interativo com seu site](#integrating-an-interactive-video-with-your-website).

## Publicar ativos de vídeo interativos {#publishing-interactive-video-assets}

Consulte [Publicação de ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar ativos de vídeo interativos.

## Integração de um vídeo interativo com seu site {#integrating-an-interactive-video-with-your-website}

Depois de fazer upload de um vídeo, adicionar segmentos de linha do tempo a ele e publicar o vídeo interativo, você estará pronto para adicioná-lo ao seu site atual.

Se você for um cliente do Experience Manager Sites , é possível adicionar o vídeo interativo arrastando o componente Mídia interativa para a página. Consulte [Adicionar ativos Dynamic Media às páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

Se você for um cliente independente do Experience Manager Assets, poderá adicionar manualmente o vídeo interativo ao seu site, conforme descrito nesta seção.

1. Copie o código incorporado ou URL do vídeo interativo publicado.
Consulte [Incorporando o visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md).
Se você adicionou interatividade com visualizações rápidas, use somente o código de inserção; se você tiver adicionado a interatividade com páginas da Web com hiperlink, também poderá usar o URL publicado. Observe, no entanto, que o método de vinculação baseado em URL não é possível se o conteúdo interativo tiver links com URLs relativos, especialmente links para páginas de Experience Manager Sites .

1. No código da página da Web do target, identifique onde o vídeo estático está localizado.
1. Remova o vídeo estático e substitua o código pelo código incorporado ou URL que você copiou do Experience Manager Assets, como está.
O código incorporado copiado é definido para um ambiente responsivo, de modo que se ajuste automaticamente à área ocupada anteriormente pelo vídeo estático.

>[!NOTE]
Nesse ponto, se você adicionou interatividade somente com páginas da Web com hiperlink, foi concluído.
No entanto, se você tiver adicionado qualquer interatividade para acionar uma exibição Rápida, as miniaturas ao lado do vídeo interativo serão apenas para fins de exibição; eles ainda não estão integrados às suas visualizações rápidas existentes. Nesse caso, é necessário integrar o vídeo interativo com as Exibições rápidas existentes no site.

**Exemplo**

Usando o site de demonstração como exemplo:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-0.html)

Observe que o código de inserção do vídeo é padrão:

```xml
<style type="text/css">
 #s7video_div.s7videoviewer{
   width:100%;
   height:auto;
 }
</style>

<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/VideoViewer.js"></script>
<div id="s7video_div"></div>
<script type="text/javascript">
 var s7videoviewer = new s7viewers.VideoViewer({
  "containerId" : "s7video_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Video",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "posterimage": "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 }).init();
</script>
```

A integração é tão simples como remover o código de inserção do vídeo e substituí-lo pelo código de inserção do vídeo interativo do Experience Manager. Você pode ver o resultado no seguinte URL. Embora ele mostre um Vídeo interativo presente na página, ele ainda não está integrado às visualizações rápidas existentes:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-1.html)

## Integração de um vídeo interativo com uma visualização rápida {#integrating-an-interactive-video-with-an-existing-quickview} existente

>[!NOTE]
Essa tarefa só se aplica se você for um cliente independente do Experience Manager Assets.

A última etapa desse processo é integrar o vídeo interativo com uma implementação de visualização rápida existente usada no site. Não há solução para a integração que funcione para todos os casos. Cada implementação da Exibição rápida é exclusiva. Como tal, é necessária uma abordagem específica que envolva a assistência de uma pessoa de TI front-end.

A implementação do Quick View existente geralmente representa uma cadeia de ações inter-relacionadas que ocorrem na página da Web na seguinte ordem:

1. Um usuário aciona um elemento na interface do usuário do site.
1. O código front-end obtém um URL de visualização rápida com base no elemento da interface do usuário acionado na etapa 1.
1. O código de front-end envia uma solicitação de AJAX usando o URL obtido na etapa 2.
1. A lógica de back-end retorna os dados de visualização rápida ou o conteúdo correspondentes de volta ao código de front-end.
1. O código front-end carrega os dados ou o conteúdo da visualização rápida.
1. Como opção, o código front-end converte os dados de visualização rápida carregados em uma representação HTML.
1. O código front-end exibe uma caixa de diálogo ou painel modal e renderiza o conteúdo HTML na tela do usuário final.

Essas chamadas não representam chamadas de API públicas independentes que podem ser chamadas pela lógica da página da Web de uma etapa arbitrária. Em vez disso, é uma chamada encadeada em que cada próxima etapa está oculta na última fase (retorno de chamada) da etapa anterior.

Ao mesmo tempo em que o vídeo interativo substitui a etapa 1 e parcialmente a etapa 2, quando um usuário toca em uma miniatura dentro do vídeo interativo, essa interação do usuário é realizada pelo visualizador. O visualizador retorna um evento para a página da Web que contém todos os dados em miniatura adicionados anteriormente ao Experience Manager.

Nesse manipulador de evento, o código front-end faz o seguinte:

* Escuta um evento emitido pelo vídeo interativo.
* Constrói um URL de visualização rápida com base nos dados de miniatura.
* Aciona o processo de carregamento da visualização Rápida do back-end e renderização dela na tela para exibição.

Além disso, o visualizador de Vídeo interativo oferece suporte ao modo de operação de tela cheia. O usuário final aciona as Exibições rápidas clicando em uma miniatura sem sair da tela cheia. Para obter essa funcionalidade, altere o código front-end para que a caixa de diálogo modal Exibição rápida esteja anexada ao contêiner do visualizador. Não adicione o BODY do documento ou outro elemento de página da Web que não esteja disponível quando o visualizador estiver no modo de tela cheia. O código que executa essa tarefa escuta mais um retorno de chamada do visualizador enviado depois que o visualizador é carregado na página.

O código incorporado retornado pelo Experience Manager já tem um manipulador de eventos pronto para uso no lugar. Ele é comentado como visto no seguinte trecho de código destacado:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "config2": "/etc/dam/presets/analytics",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 /* // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
    //To pass other parameter from the hotspot, you need to add custom parameter during the hotspot setup as parameterName=value
    loadQuickView(sku); //Replace this call with your quickview plugin
    //Please refer to your quickviewer plugin for the quickview call
    },
"initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var popup = document.getElementById('quickview_div'); // get custom quickview container
    popup.parentNode.removeChild(popup); // remove it from current DOM
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(popup); //Attach custom quickview container to viewer
    }
   });
 */
 s7interactivevideoviewer.init();
</script>
```

Portanto, é necessário remover o comentário do trecho de código destacado acima e substituir o corpo dos manipuladores de teste pelo código específico da página da Web em particular.

Há dois manipuladores de retorno de chamada padrão presentes no código incorporado padrão: `quickViewActivate` e `initComplete`. O manipulador `quickViewActivate` dispara quando uma miniatura é clicada no visualizador. Use-o para integrar o visualizador com a lógica de ativação da visualização rápida. O manipulador `initComplete` dispara somente uma vez quando o visualizador é carregado na página. Esse manipulador é usado para ajustar o local da caixa de diálogo Exibição rápida no DOM da página da Web.

O processo de construção do URL de visualização rápida é oposto ao processo de identificação das variáveis de miniatura abordadas anteriormente neste tópico. Usando os exemplos de URL de exibição rápida identificados anteriormente, você pode ver como o URL de exibição rápida é construído em cada caso:

<table>
  <tbody>
  <tr>
    <td><p>SKU único, encontrado na sequência de consulta</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/json?productId=" + inData.sku + "&amp;source=100";
      },
      });</code></td>
  </tr>
  <tr>
    <td>SKU único, encontrado no caminho do URL</td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/product/" + inData.sku;
      },
      });</code></td>
  </tr>
  <tr>
    <td><p>SKU e ID de categoria na sequência de consulta</p> </td>
    <td><code class="code">s7interactivevideoviewer.setHandlers({
      "quickViewActivate": function(inData) {
      var quickViewUrl = "https://server/quickView/product/?category=" + inData.categoryId + "&amp;prodId=" + inData.sku;
      },
      });</code></td>
  </tr>
  </tbody>
</table>

A última etapa para acionar o URL de visualização rápida e ativar o painel de visualização rápida provavelmente requer a assistência de uma pessoa de TI front-end do seu departamento de TI. Eles têm o conhecimento de saber mais sobre como acionar com precisão a implementação da visualização rápida a partir da etapa adequada, com um URL de visualização rápida pronto para uso.

Você pode ver como essas etapas são aplicadas ao site de demonstração para integrar totalmente um vídeo interativo ao código de exibição rápida. Anteriormente neste tópico, a estrutura do URL de exibição Rápida era identificada como a seguinte:

```xml
/datafeed/$CategoryId$-$SKU$.json
```

É fácil reconstruir esse URL dentro do manipulador `quickViewActivate` usando os campos `categoryId` e `sku` disponíveis no objeto `inData` passado para o manipulador por meio do código do visualizador, como no seguinte:

```xml
var sku=inData.sku;
var categoryId=inData.categoryId;
var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
```

O site de demonstração está acionando a caixa de diálogo Exibição rápida usando uma chamada de função `loadQuickView()` simples. Essa função aceita apenas um argumento, que é o URL dos dados da visualização rápida. Assim, a última etapa para integrar o vídeo interativo é adicionar a seguinte linha de código ao manipulador `quickViewActivate`:

```xml
loadQuickView(quickViewUrl);
```

Finalmente, verifique se a caixa de diálogo Exibição rápida está anexada ao elemento do contêiner do visualizador. O padrão do código incorporado fornece etapas de amostra para obter essa funcionalidade. Para obter uma referência ao elemento de contêiner do visualizador, você pode usar as seguintes linhas de código:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
```

Onde `inner_container` é uma referência a um elemento `DIV` gerenciado pelo visualizador. Você deseja que a caixa de diálogo seja filha desse `DIV`.

As etapas para localizar o elemento da caixa de diálogo modal e anexá-lo ao contêiner acima são específicas de maiúsculas e minúsculas. Novamente, você pode obter a ajuda do desenvolvedor de front-end familiarizado com a implementação do Quick View necessária.

Para o site de exemplo, a caixa de diálogo modal Exibição rápida é implementada como um `DIV` com a ID modal do quickview anexada diretamente ao documento `BODY`. Portanto, o código para mover essa caixa de diálogo para o contêiner do visualizador é tão simples quanto o seguinte:

```xml
var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
var inner_container = document.getElementById(sdkContainerId);
inner_container.appendChild(document.getElementById("quickview-modal"));
```

O código-fonte completo é o seguinte:

```xml
<style type="text/css">
 #s7interactivevideo_div.s7interactivevideoviewer{
   width:100%;
   height:auto;
 }
</style>
<script type="text/javascript" src="https://demos-pub.assetsadobe.com/etc/dam/viewers/s7viewers/html5/js/InteractiveVideoViewer.js"></script>

<div id="s7interactivevideo_div"></div>
<script type="text/javascript">
 var s7interactivevideoviewer = new s7viewers.InteractiveVideoViewer({
  "containerId" : "s7interactivevideo_div",
  "params" : {
   "serverurl" : "https://adobedemo62-h.assetsadobe.com/is/image",
   "contenturl" : "https://demos-pub.assetsadobe.com/",
   "config" : "/etc/dam/presets/viewer/Shoppable_Video_light",
   "videoserverurl": "https://gateway-na.assetsadobe.com/DMGateway/public/demoCo",
   "interactivedata": "content/dam/_VTT/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4.svideo.vtt",
   "VideoPlayer.contenturl": "https://adobedemo62-h.assetsadobe.com/is/content",
   "asset" : "/content/dam/marketing/shoppable-video/john-lewis/shoppable-video-john-lewis-2014.mp4" }
 })
 // Example of interactive video event for quickview.
   s7interactivevideoviewer.setHandlers({
   "quickViewActivate": function(inData) {
     var sku=inData.sku; //SKU for product ID
     var categoryId=inData.categoryId; //categoryId
    var quickViewUrl = "datafeed/" + categoryId + "-" + sku + ".json";
    loadQuickView(quickViewUrl);
    },
   "initComplete":function() {
    //--- Attach quickview popup to viewer container so popup will work in fullscreen mode ---
    var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId(); // get viewer container component
    var inner_container = document.getElementById(sdkContainerId);
    inner_container.appendChild(document.getElementById("quickview-modal"));
    }
   });
 s7interactivevideoviewer.init();
</script>
```

O site de demonstração final com o vídeo interativo totalmente integrado é exibido da seguinte maneira:

[https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html](https://experienceleague.adobe.com/tools/dynamic-media-demo/shoppable-video/john-lewis/landing-3.html)

## Usando visualizações rápidas para criar pop-up personalizado do Windows® {#using-quickviews-to-create-custom-pop-ups}

Consulte [Usar visualizações rápidas para criar janelas pop-up personalizadas do Windows®](/help/assets/dynamic-media/custom-pop-ups.md).
—>
