---
title: Adição de ativos de Mídia dinâmica a páginas
description: Saiba como adicionar componentes do Dynamic Media a uma página no Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
feature: Gerenciamento de ativos
role: Business Practitioner
exl-id: 2f2fd6cb-8b53-4167-a7e3-453f27549109
source-git-commit: 5e9cf9494ce9d54dd1d3b7818b3b975b2acb4e3c
workflow-type: tm+mt
source-wordcount: '3218'
ht-degree: 20%

---

# Adicionar ativos Dynamic Media às páginas{#adding-dynamic-media-assets-to-pages}

Para adicionar a funcionalidade Dynamic Media aos ativos que você usa nos sites, é possível adicionar o componente **Dynamic Media**, **Mídia interativa**, **Mídia panorâmica** ou **Mídia de vídeo 360** diretamente na página. Você entra no modo Layout e ativa os componentes do Dynamic Media. Em seguida, adicione esses componentes à página e adicione ativos ao componente. Os componentes do Dynamic Media são inteligentes - eles sabem se você está adicionando uma imagem ou um vídeo e as opções de configuração disponíveis mudam de acordo.

Você adiciona ativos do Dynamic Media diretamente à página se estiver usando [!DNL Adobe Experience Manager] como o WCM. Se estiver usando um dispositivo de terceiros no WCM, [link](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) ou [incorpore](/help/assets/dynamic-media/embed-code.md) seus ativos. Para obter um site responsivo de terceiros, consulte [fornecer imagens otimizadas para um site responsivo](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Certifique-se de publicar ativos antes de adicioná-los às páginas em [!DNL Experience Manager]. Consulte [Publicar ativos do Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Adicionar um componente Dynamic Media a uma página {#adding-a-dynamic-media-component-to-a-page}

Adicionar um componente de mídia 3D, Dynamic Media, Mídia interativa, Mídia panorâmica, Vídeo de corte inteligente ou Vídeo 360 a uma página é o mesmo que adicionar um componente a qualquer página.

**Para adicionar um componente Dynamic Media a uma página:**

1. Em [!DNL Experience Manager], abra a página à qual deseja adicionar o componente Dynamic Media.
1. No painel esquerdo, selecione o ícone **[!UICONTROL Components]** e filtre por Dynamic Media.

   Se nenhuma lista de componentes do Dynamic Media estiver disponível, você provavelmente deverá ativar os componentes do Dynamic Media que deseja usar. Consulte [Ativar componentes do Dynamic Media](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Arraste um componente **[!UICONTROL Dynamic Media]** e solte-o no local desejado na página.

1. Passe o ponteiro do mouse diretamente no componente. Quando o componente estiver rodeado por uma caixa azul, selecione uma vez para exibir a barra de ferramentas do componente. Selecione o ícone **[!UICONTROL Configuração (chave)]**.

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. Dependendo do componente do Dynamic Media que você soltou na página, uma caixa de diálogo de configuração é aberta. [Defina as opções do componente, ](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) conforme necessário.

   O exemplo abaixo mostra a caixa de diálogo do componente Mídia **[!UICONTROL Vídeo 360 do Dynamic Media e as opções disponíveis na lista suspensa Predefinição do visualizador.]**

   ![Componente de mídia Video 360](assets/6_5_360video_wcmcomponentviewerpreset.png)

   O componente de mídia Dynamic Media Video 360.

1. Quando terminar, no canto superior direito da caixa de diálogo, selecione a marca de seleção para salvar suas alterações.

### Ativar componentes do Dynamic Media {#enabling-dynamic-media-components}

Se nenhum componente do Dynamic Media estiver disponível para ser adicionado a uma página, isso provavelmente significa que você deve ativar os componentes que deseja usar.

1. Em [!DNL Experience Manager], abra a página à qual deseja adicionar o componente Dynamic Media.
1. À esquerda da barra de ferramentas, perto da parte superior da página, selecione o ícone Informações da página e selecione **[!UICONTROL Editar modelo]** na lista suspensa.

   ![editar modelo](/help/assets/assets-dm/edit-template.png)

1. No lado direito da barra de ferramentas, próximo à parte superior da página, na lista suspensa, selecione **[!UICONTROL Estrutura]**.

   ![Política](/help/assets/assets-dm/structure-mode.png)

1. Próximo à parte inferior da página, selecione **[!UICONTROL Contêiner de layout]** para abrir a barra de ferramentas, em seguida, selecione o ícone Política .
1. Na página **[!UICONTROL Contêiner de layout]**, no cabeçalho **[!UICONTROL Propriedades]**, verifique se a guia **[!UICONTROL Componentes permitidos]** está selecionada.

   ![Componentes permitidos](/help/assets/assets-dm/allowed-components.png)

1. Role até ver **[!UICONTROL Dynamic Media]**.
1. Selecione o ícone > à esquerda de **[!UICONTROL Dynamic Media]** e selecione os componentes do Dynamic Media que deseja ativar.

   ![Lista de componentes do Dynamic Media](/help/assets/assets-dm/dm-components-select.png)

1. Próximo ao canto superior direito da página **[!UICONTROL Contêiner de layout]**, selecione o ícone Concluído (marca de seleção) .

1. No lado direito da barra de ferramentas, próximo à parte superior da página, na lista suspensa, selecione **[!UICONTROL Conteúdo inicial]**.
1. [Adicione um componente Dynamic Media a uma página ](#adding-a-dynamic-media-component-to-a-page) como de costume.

## Localizar componentes do Dynamic Media {#localizing-dynamic-media-components}

Você pode localizar componentes do Dynamic Media de uma das duas maneiras:

* Em uma página da Web no Sites, abra **[!UICONTROL Propriedades]** e selecione a guia **[!UICONTROL Avançado]**. Selecione o idioma desejado para localização.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* No seletor do site, selecione a página ou grupo de páginas desejado. Selecione **[!UICONTROL Properties]** e selecione a guia **[!UICONTROL Advanced]**. Selecione o idioma desejado para localização.

   >[!NOTE]
   >
   >Nem todos os idiomas disponíveis no menu **[!UICONTROL Language]** têm tokens atribuídos no momento.

## Componentes disponíveis do Dynamic Media {#dynamic-media-components}

Os componentes do Dynamic Media estão disponíveis ao selecionar o ícone **[!UICONTROL Componentes]** e, em seguida, filtrar em **[!UICONTROL Dynamic Media]**.

Os componentes do Dynamic Media disponíveis incluem:

* **[!UICONTROL Dynamic Media]** - use para ativos como imagens, vídeo, eCatalogs e conjuntos de rotação.
* **[!UICONTROL Mídia interativa]**  - Use para quaisquer ativos interativos, como vídeo interativo, imagens interativas ou conjuntos de carrossel.
* **[!UICONTROL Mídia panorâmica]**  - Use para imagem panorâmica ou ativos de imagem panorâmica VR.
* **[!UICONTROL Mídia de vídeo 360]**  - Use para vídeos 360 e 360 VR.

>[!NOTE]
>
>Esses componentes não estão disponíveis por padrão e devem ser disponibilizados por meio do editor de modelos antes de usar o . Depois que eles forem disponibilizados no editor de modelo, você poderá adicionar os componentes à sua página como faria com qualquer outro componente [!DNL Experience Manager].

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Componente: Dynamic Media {#dynamic-media-component}

O componente Dynamic Media é inteligente. Se você adicionar uma imagem ou um vídeo, você terá várias opções. O componente oferece suporte a predefinições de imagem, visualizadores baseados em imagem, como conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista e vídeo. Além disso, o visualizador é responsivo: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

>[!NOTE]
>
>Se sua página da Web tiver o seguinte:
>
>* Várias instâncias do componente Dynamic Media sendo usado na mesma página.
>* Cada instância usa o mesmo tipo de ativo.

>
>
Não há suporte para a atribuição de uma predefinição do visualizador diferente para cada componente do Dynamic Media nessa página.
>
>No entanto, você pode usar a mesma predefinição do visualizador para todos os componentes do Dynamic Media que usam ativos do mesmo tipo, na página.

Quando você adiciona o componente Mídia dinâmica e as **[!UICONTROL Configurações de mídia dinâmica]** estão em branco ou não é possível adicionar um ativo corretamente, verifique o seguinte:

* A imagem tem um arquivo tiff de pirâmide. As imagens importadas antes de habilitar o Dynamic Media não têm um arquivo tiff de pirâmide.

#### Ao trabalhar com imagens {#when-working-with-images}

O componente Mídia dinâmica permite adicionar imagens dinâmicas, incluindo conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista. Você pode ampliar, reduzir e, se aplicável, transformar uma imagem em um conjunto de giro ou selecionar uma imagem de outro tipo de conjunto.

Você também pode configurar a predefinição do visualizador, a predefinição da imagem ou o formato da imagem diretamente no componente. Para tornar uma imagem responsiva, você pode definir os pontos de interrupção ou aplicar uma predefinição de imagem responsiva.

É possível editar as seguintes configurações do Dynamic Media selecionando o ícone **[!UICONTROL Editar]** no componente e **[!UICONTROL Configurações do Dynamic Media]**.

![Configurações predefinidas de imagem do Dynamic Media](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Por padrão, o componente de imagem do Dynamic Media é adaptável. Se desejar torná-lo de um tamanho fixo, defina-o no componente na guia **[!UICONTROL Avançado]** com a **[!UICONTROL Largura]** e a **[!UICONTROL Altura]**.

* **[!UICONTROL Predefinição do visualizador]**  - Selecione uma predefinição do visualizador existente na lista suspensa. Se a predefinição do visualizador que você está procurando não estiver visível, você deve torná-la visível. Consulte Gerenciar predefinições do visualizador. Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

   Essa é a única opção disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mídia mista. As predefinições do visualizador exibidas também são exibidas somente para smart viewer.

* **[!UICONTROL Modificadores do visualizador]**  - Os modificadores do visualizador assumem a forma de par name=value com um &amp; delimitador e permitem alterar os visualizadores, conforme descrito no Guia de referência dos visualizadores. Um exemplo de um modificador do visualizador é `posterimage=img.jpg&caption=text.vtt,1`, que define uma imagem diferente para a miniatura do vídeo e associa um arquivo de legenda/subtítulo fechado ao vídeo.

* **[!UICONTROL Predefinição de imagem]**  - Selecione uma predefinição de imagem existente na lista suspensa. Se a predefinição de imagem que você está procurando não estiver visível, você deve torná-la visível. Consulte Gerenciar predefinições de imagens. Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL Modificadores de imagem]**  - Você pode aplicar efeitos de imagem fornecendo mais comandos de imagem. Esses comandos são descritos em Predefinições de imagem e na referência do Comando de disponibilização de imagens.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL Pontos de interrupção]**  - se estiver usando esse ativo em um site responsivo, você deve adicionar os pontos de interrupção da imagem. Os pontos de interrupção da imagem devem ser separados por vírgulas (,). Essa opção funciona quando não há altura ou largura definida em uma predefinição de imagem.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

   Você pode editar as seguintes Configurações avançadas selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Otimizar para dispositivos]**  de resolução mais alta - marque a caixa de seleção (padrão) para permitir a otimização do DPR (Device Pixel Ratio).

   A opção **[!UICONTROL Otimizar para dispositivos de resolução mais alta]** só é mostrada quando o seguinte é verdadeiro:
   * Em Tipo de predefinição, **[!UICONTROL Predefinição de imagem]** é selecionado e **[!UICONTROL RESS_IP]** é selecionado na lista suspensa **[!UICONTROL Predefinição de imagem]**.

   ![configuração da relação de pixels do dispositivo para predefinição de imagem](/help/assets/dynamic-media/assets/dpr-ress-ip.png)

   Consulte também [Sobre a otimização da taxa de pixels do dispositivo](/help/assets/dynamic-media/imaging-faq.md#dpr).

   Qualquer valor [!DNL Experience Manager] do DPR de imagem inteligente da Dynamic Media é ignorado.

* **[!UICONTROL Título]**  - Altere o título da imagem.

* **[!UICONTROL Texto alternativo]**  - Adicione um título à imagem para os usuários que têm os gráficos desativados.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL URL, Abrir em]**  - Você pode definir um ativo para abrir um link. Defina o URL e, em Abrir em, indique se você deseja que ele abra na mesma janela ou em uma nova.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL Largura]**  - insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]**  - Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

#### Ao trabalhar com vídeo {#when-working-with-video}

Use o componente Dynamic Media para adicionar vídeo dinâmico às suas páginas da Web. Ao editar o componente, você pode optar por usar uma predefinição de visualizador de vídeo predefinida para reproduzir o vídeo na página.

![chlimage_1-173](assets/chlimage_1-540.png)

Você pode editar as seguintes configurações do Dynamic Media selecionando **[!UICONTROL Editar]** no componente.

>[!NOTE]
>
>Por padrão, o componente de vídeo Mídia dinâmica é adaptável. Se quiser torná-lo de um tamanho fixo, defina-o no componente com a **[!UICONTROL Largura]** e **[!UICONTROL Altura]** na guia **[!UICONTROL Avançado]**.

* **[!UICONTROL Predefinição do visualizador]**  - Selecione uma predefinição do visualizador de vídeo existente na lista suspensa. Se a predefinição do visualizador que você está procurando não estiver visível, você deve torná-la visível. Consulte Gerenciar predefinições do visualizador.

* **[!UICONTROL Modificadores do visualizador]**  - Os modificadores do visualizador assumem a forma de  `name=value` par com um  `&` delimitador. Eles permitem alterar os visualizadores conforme descrito no Guia de referência de visualizadores do Adobe. Um exemplo de um modificador do visualizador é `posterimage=img.jpg&caption=text.vtt,1`

   Com modificadores do visualizador, você pode, por exemplo, fazer o seguinte:

   * Associar um arquivo de legenda a um vídeo: [legenda](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Associar um arquivo de navegação a um vídeo: [navegação](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      Você pode editar as seguintes Configurações avançadas selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Título]**  - Altere o título do vídeo.

* **[!UICONTROL Largura]**  - insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]**  - Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

#### Ao trabalhar com o Recorte inteligente {#when-working-with-smart-crop}

Use o componente Dynamic Media para adicionar ativos de imagem de Corte inteligente às suas páginas da Web. Ao editar o componente, você pode optar por usar uma predefinição de visualizador de vídeo predefinida para reproduzir o vídeo na página.

Consulte [Usar Corte inteligente com Experience Manager Assets Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html#dynamic-media)

Consulte também [Perfis de imagem](/help/assets/dynamic-media/image-profiles.md).

![Configurações de recorte inteligente do Dynamic Media](assets/dm-settings-smart-crop.png)

Você pode editar a seguinte configuração do Dynamic Media selecionando **[!UICONTROL Editar]** no componente.

>[!NOTE]
>
>Por padrão, o componente de imagem do Dynamic Media é adaptável. Se desejar torná-lo de um tamanho fixo, defina-o no componente na guia **[!UICONTROL Avançado]** com a **[!UICONTROL Largura]** e a **[!UICONTROL Altura]**.

* **[!UICONTROL Modificadores de imagem]**  - Você pode aplicar efeitos de imagem fornecendo mais comandos de imagem. Esses comandos são descritos em Predefinições de imagem e na referência do Comando de disponibilização de imagens.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

   Você pode editar as seguintes Configurações avançadas selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Ativar correspondência de proporção de aspecto]**  - Para permitir que a Dynamic Media escolha uma representação de recorte inteligente com uma proporção de aspecto que melhor corresponda à proporção de aspecto da imagem original, selecione esta opção.

* **[!UICONTROL Otimizar para dispositivos]**  de resolução mais alta - marque a caixa de seleção (padrão) para permitir a otimização do DPR (Device Pixel Ratio).

   A opção **[!UICONTROL Otimizar para dispositivos de resolução mais alta]** só é mostrada quando o seguinte é verdadeiro:

   * Em Tipo de predefinição, a opção **[!UICONTROL Recorte inteligente]** é selecionada.

   ![configuração de proporção de pixels do dispositivo para recorte inteligente](/help/assets/dynamic-media/assets/dpr-smartcrop.png)

   Consulte também [Sobre a otimização da taxa de pixels do dispositivo](/help/assets/dynamic-media/imaging-faq.md#dpr).

   Qualquer valor [!DNL Experience Manager] do DPR de imagem inteligente da Dynamic Media é ignorado.

* **[!UICONTROL Título]**  - Altere o título da imagem de Recorte inteligente.

* **[!UICONTROL Texto alternativo]**  - Adicione um título à imagem de recorte inteligente para os usuários que têm gráficos desativados.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL URL, Abrir em]**  - Você pode definir um ativo para abrir um link. Defina o URL e, em Abrir em, indique se você deseja que ele abra na mesma janela ou em uma nova.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL Largura]**  - insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]**  - Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

### Componente: Mídia interativa {#interactive-media-component}

O componente Mídia interativa é para ativos que possuem interatividade em pontos de acesso ou mapas de imagem. Se você tiver uma imagem interativa, um vídeo interativo ou um banner de carrossel, use o componente **[!UICONTROL Mídia interativa]**.

O componente Mídia interativa é inteligente. Se você adicionar uma imagem ou um vídeo, você terá várias opções. Além disso, o visualizador é responsivo: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

>[!NOTE]
>
>Se sua página da Web tiver o seguinte:
>
>* Várias instâncias do componente Mídia interativa sendo usado na mesma página.
>* Cada instância usa o mesmo tipo de ativo.

>
>
Não há suporte para a atribuição de uma predefinição do visualizador diferente para cada componente de Mídia interativa nessa página.
>
>No entanto, você pode usar a mesma predefinição do visualizador para todos os componentes de Mídia interativa que usam ativos do mesmo tipo, dentro da página.

![chlimage_1-174](assets/chlimage_1-541.png)

Você pode editar as seguintes configurações **[!UICONTROL Geral]** selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Predefinição do visualizador]**  - Selecione uma predefinição do visualizador existente na lista suspensa. Se a predefinição do visualizador que você está procurando não estiver visível, você deve torná-la visível. As Predefinições do visualizador devem ser publicadas para poderem ser usadas. Consulte Gerenciar predefinições do visualizador.

* **[!UICONTROL Título]**  - Altere o título do vídeo.

* **[!UICONTROL Largura]**  - insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]**  - Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

   Você pode editar as seguintes configurações de **[!UICONTROL Adicionar ao carrinho]** selecionando **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Mostrar ativo do produto]**  - por padrão, esse valor é selecionado. O ativo do produto mostra uma imagem do produto, conforme definido no módulo Comércio. Limpe a marca de seleção para não mostrar o ativo do produto.

* **[!UICONTROL Mostrar preço do produto]**  - por padrão, esse valor é selecionado. O preço do produto mostra o preço do item, conforme definido no módulo Comércio. Limpe a marca de seleção para não mostrar o preço do produto.

* **[!UICONTROL Mostrar formulário do produto]**  - por padrão, esse valor não está selecionado. O Formulário de produto inclui quaisquer variantes de produto, como tamanho e cor. Limpe a marca de seleção para não mostrar as variantes do produto.

### Componente: Mídia panorâmica {#panoramic-media-component}

O componente Mídia panorâmica é para os ativos que são imagens panorâmicas esféricas. Essas imagens fornecem uma experiência de visualização de 360° de uma sala, propriedade, local ou paisagem. Para que uma imagem seja qualificada como um panorama esférico, ela deve ter um OU ambos os itens a seguir:

* Uma proporção de aspecto de 2:1.
* Marcada com as palavras-chave `equirectangular` ou (`spherical` + `panorama`) ou (`spherical` + `panoramic`). Consulte [Uso de tags](/help/sites-cloud/authoring/features/tags.md).

Tanto a proporção quanto os critérios de palavra-chave se aplicam aos ativos panorâmicos da página de detalhes do ativo e o componente **[!UICONTROL Panorâmica Media]** WCM.

>[!NOTE]
>
>Se sua página da Web tiver o seguinte:
>
>* Várias instâncias do componente **[!UICONTROL Mídia panorâmica]** sendo usado na mesma página.
>* Cada instância usa o mesmo tipo de ativo.

>
>
Não há suporte para a atribuição de uma predefinição do visualizador diferente para cada componente **[!UICONTROL Mídia panorâmica]** nessa página.
>
>No entanto, você pode usar a mesma predefinição do visualizador para todos os componentes de Mídia panorâmica que usam ativos do mesmo tipo, dentro da página.

![Predefinição do visualizador de mídia panorâmica](assets/panoramic-media-viewer-preset.png)

Você pode editar a seguinte configuração selecionando **[!UICONTROL Configurar]** no componente.

* **[!UICONTROL Predefinição do visualizador]**  - Selecione um visualizador existente na lista suspensa Predefinição do visualizador.

Se a predefinição do visualizador que você está procurando não estiver visível, verifique se ela foi publicada. Publique predefinições do visualizador antes de usá-las. Consulte [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

### Componente: Mídia de vídeo 360 {#video-media-component}

Use o componente **[!UICONTROL Mídia de vídeo 360]** para renderizar o vídeo tangível em sua página da Web. Isso garante uma experiência de visualização imersiva de uma sala, propriedade, localização, paisagem ou procedimento médico.

Durante a reprodução num ecrã plano, o utilizador controla o ângulo de visualização; a reprodução em dispositivos móveis geralmente usa seus controles giroscópicos incorporados.

O visualizador inclui suporte nativo para a entrega de 360 ativos de vídeo. Por padrão, nenhuma configuração adicional é necessária para visualizar ou reproduzir. Você fornece 360 vídeos usando extensões de vídeo padrão, como .mp4, .mkv e .mov. O codec mais comum é o H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Você pode editar a seguinte configuração selecionando **[!UICONTROL Configurar]** no componente.

* **[!UICONTROL Predefinição do visualizador]**  - Selecione um visualizador existente na lista suspensa Predefinição do visualizador. Use o Video360VR para usuários finais que usam óculos de realidade virtual. Inclui controles básicos de reprodução de vídeo e recursos de redes sociais. Use Video360_social, que inclui controles básicos de reprodução de vídeo. A renderização do vídeo é feita no modo estéreo. O controlo manual do ponto de vista está desativado, mas o controlo giroscópico está ativado. Não há recursos de redes sociais.

Se a predefinição do visualizador que você está procurando não estiver visível, verifique se ela foi publicada. Publique predefinições do visualizador antes de usá-las. Consulte [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

### Usar HTTP/2 para fornecer ativos do Dynamic Media {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como os navegadores e servidores se comunicam. Ele oferece transferência mais rápida de informações e reduz a quantidade de poder de processamento necessário. A entrega de ativos do Dynamic Media agora pode ser feita via HTTP/2, o que oferece melhor resposta e tempo de carregamento.

Consulte [HTTP2 Delivery of Content](/help/assets/dynamic-media/http2faq.md) para obter detalhes completos sobre como começar a usar HTTP/2 com sua conta Dynamic Media.

>[!MORELIKETHIS]
>
>* [Usar o reprodutor de vídeo no Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html#dynamic-media)
>* [Usar vídeo interativo com Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html#dynamic-media)
>* [Entender o visualizador de ativos com o Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html#dynamic-media)
>* [Usar a miniatura de vídeo personalizada com o Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html#dynamic-media)
>* [Entenda o gerenciamento de cores com o Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html#dynamic-media)
>* [Usar a nitidez da imagem com o Experience Manager Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media)

