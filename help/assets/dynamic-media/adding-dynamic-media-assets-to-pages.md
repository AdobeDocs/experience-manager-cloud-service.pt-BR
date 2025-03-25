---
title: Adição do Dynamic Media Assets a páginas
description: Saiba como adicionar componentes do Dynamic Media a uma página no Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 2f2fd6cb-8b53-4167-a7e3-453f27549109
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3165'
ht-degree: 5%

---

# Adição do Dynamic Media Assets a páginas{#adding-dynamic-media-assets-to-pages}

Para adicionar a funcionalidade Dynamic Media aos ativos que você usa nos sites, é possível adicionar o componente **Dynamic Media**, **Mídia interativa**, **Mídia panorâmica** ou **Mídia de vídeo 360** diretamente na página. Entre no modo Layout e ative os componentes do Dynamic Media. Em seguida, você adiciona esses componentes à página e adiciona ativos ao componente. Os componentes do Dynamic Media são inteligentes - eles sabem se você está adicionando uma imagem ou um vídeo e as opções de configuração disponíveis mudam de acordo.

Você adiciona ativos do Dynamic Media diretamente à página se estiver usando o [!DNL Adobe Experience Manager] como o WCM. Se estiver usando um dispositivo de terceiros no WCM, [vincule](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) ou [incorpore](/help/assets/dynamic-media/embed-code.md) os ativos. Para obter um site responsivo de terceiros, consulte [fornecendo imagens otimizadas para um site responsivo](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Certifique-se de publicar ativos antes de adicioná-los às páginas em [!DNL Experience Manager]. Consulte [Publicação de Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Adicionar um componente de Mídia dinâmica a uma página {#adding-a-dynamic-media-component-to-a-page}

Adicionar um componente de Mídia 3D, Mídia dinâmica, Mídia interativa, Mídia panorâmica, Recorte inteligente de vídeo ou Mídia de vídeo 360 a uma página é o mesmo que adicionar um componente a qualquer página.

**Para adicionar um componente do Dynamic Media a uma página:**

1. No [!DNL Experience Manager], abra a página em que deseja adicionar o componente do Dynamic Media.
1. No painel esquerdo, selecione o ícone **[!UICONTROL Componentes]** e filtre por Dynamic Media.

   Se nenhuma lista de componentes do Dynamic Media estiver disponível, você provavelmente deverá ativar os componentes do Dynamic Media que deseja usar. Consulte [Habilitar componentes do Dynamic Media](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Arraste um componente **[!UICONTROL Dynamic Media]** e solte-o no local desejado na página.

1. Passe o ponteiro diretamente no componente. Quando o componente estiver rodeado por uma caixa azul, selecione uma vez para exibir a barra de ferramentas do componente. Selecione o ícone **[!UICONTROL Configuração (chave inglesa)]**.

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. Dependendo do componente do Dynamic Media que você soltou na página, uma caixa de diálogo de configuração é aberta. [Defina as opções do componente](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) conforme necessário.

   O exemplo abaixo mostra a caixa de diálogo Mídia Dinâmica **[!UICONTROL Mídia de Vídeo 360]** e as opções disponíveis na lista suspensa Predefinição do Visualizador.

   ![Componente de mídia de vídeo 360](assets/6_5_360video_wcmcomponentviewerpreset.png)

   O componente de mídia do Dynamic Media Video 360.

1. Quando terminar, no canto superior direito da caixa de diálogo, marque a marca de seleção para salvar as alterações.

### Ativar componentes do Dynamic Media {#enabling-dynamic-media-components}

Se nenhum componente do Dynamic Media estiver disponível para adicionar a uma página, isso provavelmente significa que você deve ativar os componentes que deseja usar.

1. No [!DNL Experience Manager], abra a página em que deseja adicionar o componente do Dynamic Media.
1. À esquerda da barra de ferramentas próxima à parte superior da página, selecione o ícone Informações da página e selecione **[!UICONTROL Editar modelo]** na lista suspensa.

   ![editar-modelo](/help/assets/assets-dm/edit-template.png)

1. No lado direito da barra de ferramentas próximo à parte superior da página, na lista suspensa, selecione **[!UICONTROL Estrutura]**.

   ![Política](/help/assets/assets-dm/structure-mode.png)

1. Próximo à parte inferior da página, selecione **[!UICONTROL Contêiner de layout]** para abrir sua barra de ferramentas e, em seguida, selecione o ícone Política.
1. Na página **[!UICONTROL Contêiner de layout]**, no cabeçalho **[!UICONTROL Propriedades]**, verifique se a guia **[!UICONTROL Componentes permitidos]** está selecionada.

   ![Componentes permitidos](/help/assets/assets-dm/allowed-components.png)

1. Role até ver **[!UICONTROL Dynamic Media]**.
1. Selecione o ícone > à esquerda de **[!UICONTROL Dynamic Media]** e selecione os componentes do Dynamic Media que deseja habilitar.

   ![Lista de componentes do Dynamic Media](/help/assets/assets-dm/dm-components-select.png)

1. Próximo ao canto superior direito da página **[!UICONTROL Contêiner de layout]**, selecione o ícone Concluído (marca de seleção).

1. No lado direito da barra de ferramentas próximo à parte superior da página, na lista suspensa, selecione **[!UICONTROL Conteúdo inicial]**.
1. [Adicione um componente do Dynamic Media a uma página](#adding-a-dynamic-media-component-to-a-page) como de costume.

## Localizar componentes do Dynamic Media {#localizing-dynamic-media-components}

Você pode localizar componentes do Dynamic Media de uma das duas formas a seguir:

* Em uma página da Web no Sites, abra **[!UICONTROL Propriedades]** e selecione a guia **[!UICONTROL Avançado]**. Selecione o idioma desejado para localização.

  ![chlimage_1-172](assets/chlimage_1-538.png)

* No seletor de sites, selecione a página ou o grupo de páginas desejado. Selecione **[!UICONTROL Propriedades]** e a guia **[!UICONTROL Avançado]**. Selecione o idioma desejado para localização.

  >[!NOTE]
  >
  >Nem todos os idiomas disponíveis no menu **[!UICONTROL Idioma]** têm tokens atribuídos no momento.

## Componentes disponíveis do Dynamic Media {#dynamic-media-components}

Os componentes do Dynamic Media ficam disponíveis ao selecionar o ícone **[!UICONTROL Componentes]** e filtrar no **[!UICONTROL Dynamic Media]**.

Os componentes do Dynamic Media disponíveis incluem:

* **[!UICONTROL Dynamic Media]** - use para ativos como imagens, vídeo, eCatalogs e conjuntos de rotação.
* **[!UICONTROL Mídia interativa]** - Use para qualquer ativo interativo, como vídeo interativo, imagens interativas ou conjuntos de carrossel.
* **[!UICONTROL Mídia panorâmica]** - Use para ativos de imagem panorâmica ou VR panorâmica.
* **[!UICONTROL Mídia de vídeo 360]** - Use para ativos de vídeo 360 e vídeo 360 VR.

>[!NOTE]
>
>Esses componentes não estão disponíveis por padrão e devem ser disponibilizados por meio do editor de modelo antes de usar. Depois que eles forem disponibilizados no editor de modelo, você poderá adicionar os componentes à sua página como faria com qualquer outro componente [!DNL Experience Manager].

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Componente: Dynamic Media {#dynamic-media-component}

O componente Dynamic Media é inteligente. Ao adicionar uma imagem ou um vídeo, você tem várias opções. O componente oferece suporte a predefinições de imagens, visualizadores baseados em imagem, como conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista e vídeo. Além disso, o visualizador é responsivo — o tamanho da tela muda automaticamente com base no tamanho da tela. Todos os visualizadores são visualizadores do HTML5.

>[!NOTE]
>
>Se sua página da Web tiver o seguinte:
>
>* Várias instâncias do componente Dynamic Media sendo usado na mesma página.
>* Cada instância usa o mesmo tipo de ativo.
>
>Não há suporte para a atribuição de uma predefinição do visualizador diferente para cada componente do Dynamic Media nessa página.
>
>No entanto, é possível usar a mesma predefinição do visualizador para todos os componentes do Dynamic Media que usam ativos do mesmo tipo, na página.

Quando você adicionar o componente Dynamic Media e as **[!UICONTROL Configurações do Dynamic Media]** estiverem em branco ou não for possível adicionar um ativo corretamente, verifique o seguinte:

* A imagem tem um arquivo TIFF de pirâmide. As imagens importadas antes da ativação do Dynamic Media não têm um arquivo TIFF em pirâmide.

#### Ao trabalhar com imagens {#when-working-with-images}

O componente Dynamic Media permite adicionar imagens dinâmicas, incluindo conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista. Você pode ampliar, reduzir e, se aplicável, girar uma imagem em um conjunto de rotação ou selecionar uma imagem de outro tipo de conjunto.

Também é possível configurar a predefinição do visualizador, a predefinição da imagem ou o formato da imagem diretamente no componente. Para tornar uma imagem responsiva, você pode definir os pontos de interrupção ou aplicar uma predefinição de imagem responsiva.

Você pode editar as seguintes Configurações do Dynamic Media selecionando o ícone **[!UICONTROL Editar]** no componente e depois **[!UICONTROL Configurações do Dynamic Media]**.

![Configurações de predefinição de imagem do Dynamic Media](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Por padrão, o componente de imagem do Dynamic Media é adaptável. Se desejar torná-lo de um tamanho fixo, defina-o no componente na guia **[!UICONTROL Avançado]** com a **[!UICONTROL Largura]** e a **[!UICONTROL Altura]**.

* **[!UICONTROL Predefinição do visualizador]** - Selecione uma predefinição do visualizador existente na lista suspensa. Se a predefinição do visualizador que você está procurando não estiver visível, é necessário torná-la visível. Consulte Gerenciamento de predefinições do visualizador. Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

  Essa opção é a única disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista. As predefinições do visualizador exibidas também são predefinições do visualizador relevantes somente para inteligentes.

* **[!UICONTROL Modificadores do visualizador]** - Os modificadores do visualizador tomam a forma do par nome=valor com um delimitador &amp; e permitem alterar os visualizadores conforme descrito no Guia de Referência do Visualizador. Um exemplo de um modificador de visualizador é `posterimage=img.jpg&caption=text.vtt,1` que define uma imagem diferente para a miniatura do vídeo e associa um arquivo de legendas ocultas ao vídeo.

* **[!UICONTROL Predefinição de imagem]** - Selecione uma predefinição de imagem existente na lista suspensa. Se a predefinição de imagem que você está procurando não estiver visível, será necessário torná-la visível. Consulte [Gerenciar predefinições de imagem](/help/assets/dynamic-media/managing-image-presets.md). Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

  Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

* **[!UICONTROL Modificadores de Imagem]** - Você pode aplicar efeitos de imagem fornecendo mais comandos de imagem. Esses comandos são descritos nas Predefinições de imagem e na referência do Comando de disponibilização de imagens.

  Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

* **[!UICONTROL Pontos de interrupção]** - Se estiver usando este ativo em um site responsivo, você deve adicionar os pontos de interrupção da imagem. Os pontos de interrupção da imagem devem ser separados por vírgulas (,). Essa opção funciona quando não há altura ou largura definidas em uma predefinição de imagem.

  Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

  Você pode editar as seguintes Configurações avançadas selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Otimizar para dispositivos de maior resolução]** - Marque (padrão) a caixa de seleção para permitir a otimização de DPR (Proporção de pixels do dispositivo).

  A opção **[!UICONTROL Otimizar para dispositivos de maior resolução]** só é exibida quando o seguinte é verdadeiro:
   * Em Tipo de Predefinição, a **[!UICONTROL Predefinição de Imagem]** está selecionada e o **[!UICONTROL RESS_IP]** está selecionado na lista suspensa **[!UICONTROL Predefinição de Imagem]**.

  ![configuração da proporção de pixels do dispositivo para a predefinição de imagem](/help/assets/dynamic-media/assets/dpr-ress-ip.png)

  Consulte também [Sobre a otimização da proporção de pixels do dispositivo](/help/assets/dynamic-media/imaging-faq.md#dpr).

  Qualquer valor de DPR de Imagem inteligente do Dynamic Media [!DNL Experience Manager] é ignorado.

* **[!UICONTROL Título]** - Alterar o título da imagem.

* **[!UICONTROL Texto Alternativo]** - Adicione um título à imagem para os usuários que têm gráficos desativados.

  Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

* **[!UICONTROL URL, Abrir em]** - Você pode definir um ativo para abrir um link. Defina o URL e, em Abrir no, indique se deseja abri-lo na mesma janela ou em uma nova janela.

  Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

* **[!UICONTROL Largura]** - Insira o valor em pixels se desejar que a imagem seja de tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]** - Insira o valor em pixels se desejar que a imagem seja de tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

#### Ao trabalhar com Vídeo {#when-working-with-video}

Use o componente Dynamic Media para adicionar vídeo dinâmico às suas páginas da Web. Ao editar o componente, você pode optar por usar uma predefinição predefinida do visualizador de vídeo para reproduzir o vídeo na página.

![chlimage_1-173](assets/chlimage_1-540.png)

Você pode editar as seguintes Configurações do Dynamic Media selecionando **[!UICONTROL Editar]** no componente.

>[!NOTE]
>
>Por padrão, o componente de vídeo do Dynamic Media é adaptável. Se quiser torná-lo de um tamanho fixo, defina-o no componente com a **[!UICONTROL Largura]** e a **[!UICONTROL Altura]** na guia **[!UICONTROL Avançado]**.

* **[!UICONTROL Predefinição do visualizador]** - Selecione uma predefinição do visualizador de vídeo existente na lista suspensa. Se a predefinição do visualizador que você está procurando não estiver visível, é necessário torná-la visível. Consulte Gerenciamento de predefinições do visualizador.

* **[!UICONTROL Modificadores do visualizador]** - Os modificadores do visualizador tomam a forma de um par `name=value` com um delimitador `&`. Eles permitem alterar os visualizadores conforme descrito no Guia de referência do visualizador do Adobe. Um exemplo de um modificador de visualizador é `posterimage=img.jpg&caption=text.vtt,1`

  Com os modificadores do visualizador, você pode, por exemplo, fazer o seguinte:

   * Associar um arquivo de legenda a um vídeo: [legenda](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Associar um arquivo de navegação a um vídeo: [navegação](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

     Você pode editar as seguintes Configurações avançadas selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Título]** - Alterar o título do vídeo.

* **[!UICONTROL Largura]** - Insira o valor em pixels se desejar que a imagem seja de tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]** - Insira o valor em pixels se desejar que a imagem seja de tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

#### Ao trabalhar com o Recorte inteligente {#when-working-with-smart-crop}

Use o componente Dynamic Media para adicionar ativos de imagem do Corte inteligente às suas páginas da Web. Ao editar o componente, você pode optar por usar uma predefinição predefinida do visualizador de vídeo para reproduzir o vídeo na página.

Consulte [Usar corte inteligente com o Experience Manager Assets Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use.html?lang=pt-BR)

Consulte também [Perfis de imagem](/help/assets/dynamic-media/image-profiles.md).

![Configurações de corte inteligente do Dynamic Media](assets/dm-settings-smart-crop.png)

Você pode editar a seguinte Configuração do Dynamic Media selecionando **[!UICONTROL Editar]** no componente.

>[!NOTE]
>
>Por padrão, o componente de imagem do Dynamic Media é adaptável. Se desejar torná-lo de um tamanho fixo, defina-o no componente na guia **[!UICONTROL Avançado]** com a **[!UICONTROL Largura]** e a **[!UICONTROL Altura]**.

* **[!UICONTROL Modificadores de Imagem]** - Você pode aplicar efeitos de imagem fornecendo mais comandos de imagem. Esses comandos são descritos nas Predefinições de imagem e na referência do Comando de disponibilização de imagens.

  Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

  Você pode editar as seguintes Configurações avançadas selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Habilitar correspondência de taxa de proporção]** - Para permitir que a Mídia Dinâmica escolha uma representação de recorte inteligente com uma taxa de proporção que melhor corresponda à taxa de proporção da imagem original, selecione esta opção.

* **[!UICONTROL Otimizar para dispositivos de maior resolução]** - Marque (padrão) a caixa de seleção para permitir a otimização de DPR (Proporção de pixels do dispositivo).

  A opção **[!UICONTROL Otimizar para dispositivos de maior resolução]** só é exibida quando o seguinte é verdadeiro:

   * Em Tipo de predefinição, a opção **[!UICONTROL Recorte inteligente]** está selecionada.

  ![configuração de taxa de pixels do dispositivo para corte inteligente](/help/assets/dynamic-media/assets/dpr-smartcrop.png)

  Consulte também [Sobre a otimização da proporção de pixels do dispositivo](/help/assets/dynamic-media/imaging-faq.md#dpr).

  Qualquer valor de DPR de Imagem inteligente do Dynamic Media [!DNL Experience Manager] é ignorado.

* **[!UICONTROL Título]** - Alterar o título da imagem do Corte inteligente.

* **[!UICONTROL Texto Alternativo]** - Adicione um título à imagem de recorte inteligente para os usuários que têm gráficos desativados.

  Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

* **[!UICONTROL URL, Abrir em]** - Você pode definir um ativo para abrir um link. Defina o URL e, em Abrir no, indique se deseja abri-lo na mesma janela ou em uma nova janela.

  Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista.

* **[!UICONTROL Largura]** - Insira o valor em pixels se desejar que a imagem seja de tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]** - Insira o valor em pixels se desejar que a imagem seja de tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

### Componente: mídia interativa {#interactive-media-component}

O componente de Mídia interativa é para os ativos que têm interatividade, como pontos de acesso ou mapas de imagem. Se você tiver uma imagem interativa, vídeo interativo ou banner de carrossel, use o componente **[!UICONTROL Mídia interativa]**.

O componente de Mídia interativa é inteligente. Ao adicionar uma imagem ou um vídeo, você tem várias opções. Além disso, o visualizador é responsivo - o tamanho da tela muda automaticamente com base no tamanho da tela. Todos os visualizadores são visualizadores do HTML5.

>[!NOTE]
>
>Se sua página da Web tiver o seguinte:
>
>* Várias instâncias do componente de Mídia interativa sendo usadas na mesma página.
>* Cada instância usa o mesmo tipo de ativo.
>
>Não há suporte para a atribuição de uma predefinição do visualizador diferente para cada componente de Mídia interativa nessa página.
>
>No entanto, você pode usar a mesma predefinição do visualizador para todos os componentes de Mídia interativa que usam ativos do mesmo tipo, na página.

![chlimage_1-174](assets/chlimage_1-541.png)

Você pode editar as seguintes configurações de **[!UICONTROL Geral]** selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Predefinição do visualizador]** - Selecione uma predefinição do visualizador existente na lista suspensa. Se a predefinição do visualizador que você está procurando não estiver visível, é necessário torná-la visível. As predefinições do visualizador devem ser publicadas antes de serem usadas. Consulte Gerenciamento de predefinições do visualizador.

* **[!UICONTROL Título]** - Alterar o título do vídeo.

* **[!UICONTROL Largura]** - Insira o valor em pixels se desejar que a imagem seja de tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]** - Insira o valor em pixels se desejar que a imagem seja de tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

  Você pode editar as seguintes configurações de **[!UICONTROL Adicionar ao carrinho]** selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Mostrar ativo de produto]** - Por padrão, este valor está selecionado. O ativo do produto mostra uma imagem do produto conforme definido no módulo Commerce. Desmarque a marca de seleção para não mostrar o ativo do produto.

* **[!UICONTROL Mostrar Preço do Produto]** - Por padrão, este valor é selecionado. Preço do produto mostra o preço do item conforme definido no módulo Commerce. Desmarque a marca de seleção para não mostrar o preço do produto.

* **[!UICONTROL Mostrar Formulário de Produto]** - Por padrão, esse valor não está selecionado. O Formulário de produto inclui qualquer variante de produto, como tamanho e cor. Desmarque a marca de seleção para não mostrar as grades de produtos.

### Componente: Mídia panorâmica {#panoramic-media-component}

O componente de Mídia panorâmica é para os ativos que são imagens panorâmicas esféricas. Essas imagens proporcionam uma experiência de visualização de 360° em uma sala, propriedade, local ou paisagem. Para que uma imagem seja qualificada como panorama esférico, ela deve ter uma ou ambas as opções a seguir:

* Uma proporção de 2:1.
* Marcado com as palavras-chave `equirectangular` ou (`spherical` + `panorama`) ou (`spherical` + `panoramic`). Consulte [Usando Tags](/help/sites-cloud/authoring/sites-console/tags.md).

Tanto a proporção quanto os critérios de palavra-chave se aplicam aos ativos panorâmicos da página de detalhes do ativo e o componente **[!UICONTROL Panorâmica Media]** WCM.

>[!NOTE]
>
>Se sua página da Web tiver o seguinte:
>
>* Várias instâncias do componente **[!UICONTROL Mídia panorâmica]** sendo usadas na mesma página.
>* Cada instância usa o mesmo tipo de ativo.
>
>Não há suporte para a atribuição de uma predefinição do visualizador diferente para cada componente de **[!UICONTROL Mídia panorâmica]** nessa página.
>
>No entanto, você pode usar a mesma predefinição do visualizador para todos os componentes de Mídia panorâmica que usam ativos do mesmo tipo, na página.

![Predefinição do visualizador de mídia panorâmica](assets/panoramic-media-viewer-preset.png)

Você pode editar a seguinte configuração selecionando **[!UICONTROL Configurar]** no componente.

* **[!UICONTROL Predefinição do visualizador]** - Selecione um visualizador existente na lista suspensa Predefinição do visualizador.

Se a predefinição do visualizador que você está procurando não estiver visível, verifique se ela foi publicada. Publique as predefinições do visualizador antes de usá-las. Consulte [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

### Componente: mídia de vídeo 360 {#video-media-component}

Use o componente de Mídia **[!UICONTROL de Vídeo 360]** para renderizar vídeo retangular equivalente na sua página da Web. Isso garante uma experiência de visualização imersiva de uma sala, propriedade, local, paisagem ou procedimento médico.

Durante a reprodução em uma tela plana, o usuário tem controle do ângulo de visão; a reprodução em dispositivos móveis geralmente usa seus controles giroscópicos incorporados.

O visualizador inclui suporte nativo para a entrega de 360 ativos de vídeo. Por padrão, nenhuma configuração adicional é necessária para exibir ou reproduzir. Você fornece vídeo 360 usando extensões de vídeo padrão, como .mp4, .mkv e .mov. O codec mais comum é o H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Você pode editar a seguinte configuração selecionando **[!UICONTROL Configurar]** no componente.

* **[!UICONTROL Predefinição do visualizador]** - Selecione um visualizador existente na lista suspensa Predefinição do visualizador. Use o Video360VR para usuários finais que utilizam óculos de realidade virtual. Inclui controles básicos de reprodução de vídeo e recursos de redes sociais. Use Video360_social, que inclui controles básicos de reprodução de vídeo. A renderização de vídeo é feita no modo estéreo. O controle manual do ponto de vista está desativado, mas o controle giroscópico está ativado. Não há recursos de redes sociais.

Se a predefinição do visualizador que você está procurando não estiver visível, verifique se ela foi publicada. Publique as predefinições do visualizador antes de usá-las. Consulte [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

### Usar HTTP/2 para entrega de ativos do Dynamic Media {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como navegadores e servidores se comunicam. Ele possibilita a transferência mais rápida de informações e reduz a quantidade necessária de poder de processamento. A entrega de ativos do Dynamic Media agora pode ser por HTTP/2, o que fornece melhores tempos de resposta e carregamento.

Consulte [Entrega de conteúdo HTTP2](/help/assets/dynamic-media/http2faq.md) para obter detalhes completos sobre a introdução ao uso de HTTP/2 com sua conta do Dynamic Media.

>[!MORELIKETHIS]
>
>* [Usar o reprodutor de vídeo no Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-video-player-feature-video-use.html)
>* [Usar vídeo interativo com o Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-interactive-video-feature-video-use.html)
>* [Entender o Visualizador de Ativos com o Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/viewers/dynamic-media-viewer-feature-video-understand.html)
>* [Usar miniatura de vídeo personalizado com o Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-video-thumbnails-feature-video-use.html)
>* [Entender o gerenciamento de cores com o Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [Usar nitidez de imagem com o Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use.html)
