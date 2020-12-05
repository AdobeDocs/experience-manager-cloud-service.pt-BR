---
title: Adição de ativos de Mídia dinâmica a páginas
description: Como adicionar componentes do Dynamic Media a uma página no Experience Manager
translation-type: tm+mt
source-git-commit: 79d4e51db99e2c1f8b18edd7249a26f4be7169e1
workflow-type: tm+mt
source-wordcount: '3134'
ht-degree: 30%

---


# Adição de ativos de Mídia dinâmica a páginas{#adding-dynamic-media-assets-to-pages}

Para adicionar a funcionalidade Dynamic Media aos ativos que você usa nos sites, é possível adicionar o componente **Dynamic Media**, **Mídia interativa**, **Mídia panorâmica** ou **Mídia de vídeo 360** diretamente na página. Para fazer isso, entre no modo Layout e ative os componentes do Dynamic Media. Em seguida, adicione esses componentes à página e adicionar ativos ao componente. Os componentes do Dynamic Media são inteligentes - eles sabem se você está adicionando uma imagem ou um vídeo e as opções de configuração disponíveis mudam de acordo.

Você adiciona ativos de Dynamic Media diretamente à página se estiver usando o Experience Manager como seu WCM. Se estiver usando um dispositivo de terceiros no WCM, [vincule](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) ou [incorpore](/help/assets/dynamic-media/embed-code.md) os ativos. Para obter um site responsivo de terceiros, consulte [Fornecer imagens otimizadas para um site responsivo](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>Você deve publicar ativos antes de adicioná-los às páginas no Experience Manager. Consulte [Publicar ativos de mídia dinâmica](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Adicionar um componente de Dynamic Media a uma página {#adding-a-dynamic-media-component-to-a-page}

Adicionar um componente de mídia 3D, Dynamic Media, Interative Media, Panorâmica Media, Smart Crop Video ou Video 360 Media a uma página é o mesmo que adicionar um componente a qualquer página. Os componentes do Dynamic Media estão descritos nas seções a seguir.

**Adicionar um componente de Dynamic Media a uma página**

1. No Experience Manager, abra a página onde deseja adicionar o componente Mídia dinâmica.
1. No painel esquerdo, toque no ícone **[!UICONTROL Components]** e, em seguida, filtre para Dynamic Media.

   Se nenhuma lista de componentes do Dynamic Media estiver disponível, é necessário ativar os componentes do Dynamic Media que você deseja usar. Consulte [Ativando componentes do Dynamic Media](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](assets/6_5_360video_wcmcomponent.png)

1. Arraste um componente **[!UICONTROL Dynamic Media]** e solte-o no local desejado na página.

1. Passe o ponteiro do mouse diretamente no componente. Quando o componente estiver rodeado por uma caixa azul, toque uma vez para exibir a barra de ferramentas do componente. Toque no ícone **[!UICONTROL Configuração (chave)]**.

   ![6_5_360video_wcmcomponentconfigure](assets/6_5_360video_wcmcomponentconfigure.png)

1. Dependendo do componente Dynamic Media que você soltou na página, uma caixa de diálogo de configuração é aberta. [Defina as ](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) opções do componente, conforme necessário.

   O exemplo abaixo mostra a caixa de diálogo do componente Dynamic Media **[!UICONTROL Video 360 Media]** e as opções disponíveis na lista suspensa Visualizador predefinido.

   ![Componente de mídia do Video 360](assets/6_5_360video_wcmcomponentviewerpreset.png)

   O componente Dynamic Media Video 360 Media.

1. Quando terminar, no canto superior direito da caixa de diálogo, toque na marca de seleção para salvar as alterações.

### Ativação dos componentes do Dynamic Media {#enabling-dynamic-media-components}

Se nenhum componente do Dynamic Media estiver disponível para adicionar a uma página, isso provavelmente significa que você precisa primeiro ativar os componentes que deseja usar.

1. No Experience Manager, abra a página onde deseja adicionar o componente Mídia dinâmica.
1. No lado esquerdo da barra de ferramentas próximo à parte superior da página, toque no ícone Informações da página e, em seguida, toque em **[!UICONTROL Editar modelo]** na lista suspensa.

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. No lado direito da barra de ferramentas próximo à parte superior da página, na lista suspensa, toque em **[!UICONTROL Estrutura]**.

   ![Política](/help/assets/assets-dm/structure-mode.png)

1. Próximo à parte inferior da página, toque em **[!UICONTROL Container de layout]** para abrir sua barra de ferramentas e, em seguida, toque no ícone Política.
1. Na página **[!UICONTROL Container de layout]**, sob o cabeçalho **[!UICONTROL Propriedades]**, verifique se a guia **[!UICONTROL Componentes permitidos]** está selecionada.

   ![Componentes permitidos](/help/assets/assets-dm/allowed-components.png)

1. Role até ver **[!UICONTROL Dynamic Media]**.
1. Toque no ícone > à esquerda de **[!UICONTROL Dynamic Media]** para expandir a lista, selecione os componentes do Dynamic Media que deseja ativar.

   ![Lista de componentes do Dynamic Media](/help/assets/assets-dm/dm-components-select.png)

1. Perto do canto superior direito da página **[!UICONTROL Container de layout]**, toque no ícone Concluído (marca de seleção).

1. No lado direito da barra de ferramentas, próximo à parte superior da página, na lista suspensa, toque em **[!UICONTROL Conteúdo inicial]** e [adicione um componente de Mídia dinâmica a uma página](#adding-a-dynamic-media-component-to-a-page), como de costume.

## Localizando componentes de Dynamic Media {#localizing-dynamic-media-components}

Você pode localizar componentes do Dynamic Media de uma das duas maneiras:

* Em uma página da Web no Sites, abra **[!UICONTROL Propriedades]** e selecione a guia **[!UICONTROL Avançado]**. Selecione o idioma desejado para localização.

   ![chlimage_1-172](assets/chlimage_1-538.png)

* No seletor do site, selecione a página ou o grupo de páginas desejado. Toque em **[!UICONTROL Propriedades]** e selecione a guia **[!UICONTROL Avançado]**. Selecione o idioma desejado para localização.

   >[!NOTE]
   >
   >Observe que nem todos os idiomas disponíveis no menu **[!UICONTROL Idioma]** têm tokens atribuídos no momento.

## Componentes disponíveis do Dynamic Media {#dynamic-media-components}

Os componentes do Dynamic Media estão disponíveis quando você toca no ícone **[!UICONTROL Components]** e, em seguida, filtra em **[!UICONTROL Dynamic Media]**.

Os componentes do Dynamic Media disponíveis incluem:

* **[!UICONTROL Dynamic Media]** - use para ativos como imagens, vídeo, eCatalogs e conjuntos de rotação.
* **[!UICONTROL Mídia]**  interativa - use para qualquer ativo interativo, como vídeo interativo, imagens interativas ou conjuntos de carrossel.
* **[!UICONTROL Mídia]**  panorâmica - Use para imagens panorâmicas ou ativos de imagens VR panorâmicas.
* **[!UICONTROL Mídia]**  de vídeo 360 - Use para ativos de vídeo 360 e 360 VR.

>[!NOTE]
>
>Esses componentes não estão disponíveis por padrão e precisam ser disponibilizados por meio do editor de modelos antes de usar. Depois que eles forem disponibilizados no editor de modelo, você poderá adicionar os componentes à sua página como faria com qualquer outro componente Experience Manager.

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Componente: Dynamic Media {#dynamic-media-component}

O componente Dynamic Media é inteligente. Dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. O componente oferece suporte a predefinições de imagem, visualizadores baseados em imagem, como conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista e vídeo. Além disso, o visualizador responde: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

>[!NOTE]
>
>Se sua página da Web tiver o seguinte:
>
>* Várias instâncias do componente Mídia dinâmica sendo usado na mesma página.
>* Cada instância usa o mesmo tipo de ativo.

>
>
Esteja ciente de que não há suporte para a atribuição de uma predefinição de visualizador diferente para cada componente de Dynamic Media nessa página.
>
>Entretanto, é possível usar a mesma predefinição do visualizador para todos os componentes do Dynamic Media que usam ativos do mesmo tipo, na página.

Quando você adiciona o componente Mídia dinâmica e as **[!UICONTROL Configurações de mídia dinâmica]** estão em branco ou não é possível adicionar um ativo corretamente, verifique o seguinte:

* A imagem tem um arquivo tiff de pirâmide. As imagens importadas antes de a mídia dinâmica ser ativada não possuem um arquivo tiff de pirâmide.

#### Ao trabalhar com imagens {#when-working-with-images}

O componente Mídia dinâmica permite adicionar imagens dinâmicas, incluindo conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista. Você pode ampliar, reduzir e, se aplicável, transformar uma imagem em um conjunto de giro ou selecionar uma imagem de outro tipo de conjunto.

Você também pode configurar a predefinição do visualizador, a predefinição da imagem ou o formato da imagem diretamente no componente. Para tornar uma imagem responsiva, você pode definir os pontos de interrupção ou aplicar uma predefinição de imagem responsiva.

Você pode editar as seguintes Configurações de Dynamic Media tocando no ícone **[!UICONTROL Editar]** no componente e, em seguida, **[!UICONTROL Configurações de Dynamic Media]**.

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>Por padrão, o componente de imagem do Dynamic Media é adaptável. Se desejar torná-lo de um tamanho fixo, defina-o no componente na guia **[!UICONTROL Avançado]** com a **[!UICONTROL Largura]** e a **[!UICONTROL Altura]**.

* **[!UICONTROL Predefinição]** do visualizador: selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição de visualizador que você está procurando não estiver visível, pode ser necessário torná-la visível. Consulte Gerenciar predefinições do visualizador. Não é possível selecionar uma predefinição de visualizador se você estiver usando uma predefinição de imagem e vice-versa.

   Essa será a única opção disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia. As predefinições do visualizador exibidas também são inteligentes: apenas as predefinições relevantes do visualizador são exibidas.

* **[!UICONTROL Modificadores]** do visualizador—Os modificadores do visualizador assumem a forma de par name=value com um &amp; delimitador e permitem alterar os visualizadores conforme descrito no Guia de referência do visualizador. Um exemplo de um modificador do visualizador é `posterimage=img.jpg&caption=text.vtt,1`, que define uma imagem diferente para a miniatura do vídeo e associa um arquivo de legenda/legenda ao vídeo.

* **[!UICONTROL Predefinição]** de imagem — Selecione uma predefinição de imagem existente no menu suspenso. Se a predefinição de imagem que você está procurando não estiver visível, pode ser necessário torná-la visível. Consulte Gerenciar predefinições de imagens. Não é possível selecionar uma predefinição de visualizador se você estiver usando uma predefinição de imagem e vice-versa.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL Modificadores]** de imagem—Você pode aplicar efeitos de imagem fornecendo comandos de imagem adicionais. Elas são descritas nas predefinições de imagem e na referência do Comando de disponibilização de imagem.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL Pontos de interrupção]**—Se você estiver usando esse ativo em um site responsivo, precisará adicionar os pontos de interrupção da imagem. Os pontos de interrupção da imagem precisam ser separados por vírgulas (,). Essa opção funciona quando não há altura ou largura definida em uma predefinição de imagem.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

   Você pode editar as seguintes Configurações avançadas tocando em **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Título]**—Altere o título da imagem.

* **[!UICONTROL Texto]** alternativo — Adicione um título à imagem para os usuários que tiverem gráficos desativados.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL URL, Abrir]** - Você pode definir um ativo para abrir um link. Defina o URL e, em Abrir em, indique se você deseja que ele abra na mesma janela ou em uma nova.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL Largura]**—Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]**—Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.


#### Ao trabalhar com vídeo {#when-working-with-video}

Use o componente Mídia dinâmica para adicionar vídeo dinâmico às páginas da Web. Ao editar o componente, você pode optar por usar uma predefinição de visualizador de vídeo predefinida para reproduzir o vídeo na página.

![chlimage_1-173](assets/chlimage_1-540.png)

Você pode editar as seguintes Configurações de Dynamic Media clicando em **[!UICONTROL Editar]** no componente.

>[!NOTE]
>
>Por padrão, o componente de vídeo Mídia dinâmica é adaptável. Se desejar torná-lo um tamanho fixo, defina-o no componente com **[!UICONTROL Largura]** e **[!UICONTROL Altura]** na guia **[!UICONTROL Avançado]**.

* **[!UICONTROL Predefinição]** do visualizador — Selecione uma predefinição existente do visualizador de vídeo no menu suspenso. Se a predefinição de visualizador que você está procurando não estiver visível, pode ser necessário torná-la visível. Consulte Gerenciar predefinições do visualizador.

* **[!UICONTROL Modificadores]** do visualizador—Os modificadores do visualizador assumem a forma de par nome=valor com um &amp; delimitador e permitem alterar os visualizadores, conforme descrito no Guia de Referência dos Visualizadores de Adobe. Um exemplo de um modificador do visualizador é `posterimage=img.jpg&caption=text.vtt,1`

   Com modificadores do visualizador, você pode, por exemplo, fazer o seguinte:

   * Associe um arquivo de legenda a um vídeo: [legenda](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * Associe um arquivo de navegação a um vídeo: [navegação](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

   Você pode editar as seguintes Configurações avançadas clicando em **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Título]**—Altere o título do vídeo.

* **[!UICONTROL Largura]**—Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]**—Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

#### Ao trabalhar com o Smart Crop {#when-working-with-smart-crop}

Use o componente Mídia dinâmica para adicionar ativos de imagem de Recorte inteligente às suas páginas da Web. Ao editar o componente, você pode optar por usar uma predefinição de visualizador de vídeo predefinida para reproduzir o vídeo na página.

Consulte [Usando o Smart Crop com Experience Manager Assets Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/smart-crop-feature-video-use.html)

Consulte também [Perfis de imagem](/help/assets/dynamic-media/image-profiles.md).

![dm-settings-smart-cut](assets/dm-settings-smart-crop.png)

Você pode editar a seguinte Configuração de Mídia Dinâmica clicando em **[!UICONTROL Editar]** no componente.

>[!NOTE]
>
>Por padrão, o componente de imagem do Dynamic Media é adaptável. Se desejar torná-lo de um tamanho fixo, defina-o no componente na guia **[!UICONTROL Avançado]** com a **[!UICONTROL Largura]** e a **[!UICONTROL Altura]**.

* **[!UICONTROL Modificadores]** de imagem—Você pode aplicar efeitos de imagem fornecendo comandos de imagem adicionais. Elas são descritas nas predefinições de imagem e na referência do Comando de disponibilização de imagem.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

   Você pode editar as seguintes Configurações avançadas clicando em **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Ativar a correspondência]** de proporção — Selecione essa opção para permitir que o Dynamic Media escolha uma execução de recorte inteligente com uma proporção que melhor corresponda à proporção da imagem original.

* **[!UICONTROL Título]**—Altere o título da imagem de Recorte inteligente.

* **[!UICONTROL Texto]** alternativo — Adicione um título à imagem de recorte inteligente para os usuários que têm gráficos desativados.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL URL, Abrir]** - Você pode definir um ativo para abrir um link. Defina o URL e, em Abrir em, indique se você deseja que ele abra na mesma janela ou em uma nova.

   Essa opção não estará disponível se você estiver visualizando conjuntos de imagens, conjuntos de rotação ou conjuntos de mix de mídia.

* **[!UICONTROL Largura]**—Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]**—Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

### Componente: Interative Media {#interactive-media-component}

O componente Mídia interativa é para ativos que possuem interatividade em pontos de acesso ou mapas de imagem. Se você tiver uma imagem interativa, um vídeo interativo ou um banner de carrossel, use o componente **[!UICONTROL Mídia interativa]**.

O componente de Mídia interativa é inteligente. Dependendo de você adicionar uma imagem ou um vídeo, você terá várias opções. Além disso, o visualizador responde: o tamanho da tela muda automaticamente com base no tamanho da tela. Todos são visualizadores HTML5.

>[!NOTE]
>
>Se sua página da Web tiver o seguinte:
>
>* Várias instâncias do componente de Mídia interativa sendo usado na mesma página.
>* Cada instância usa o mesmo tipo de ativo.

>
>
Esteja ciente de que não há suporte para a atribuição de uma predefinição de visualizador diferente para cada componente de Mídia interativa nessa página.
>
>Entretanto, é possível usar a mesma predefinição do visualizador para todos os componentes de Mídia interativa que usam ativos do mesmo tipo, na página.

![chlimage_1-174](assets/chlimage_1-541.png)

Você pode editar as seguintes configurações **[!UICONTROL Geral]** tocando em **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Predefinição]** do visualizador: selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição de visualizador que você está procurando não estiver visível, pode ser necessário torná-la visível. As Predefinições do visualizador devem ser publicadas para poderem ser usadas. Consulte Gerenciar predefinições do visualizador.

* **[!UICONTROL Título]**—Altere o título do vídeo.

* **[!UICONTROL Largura]**—Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

* **[!UICONTROL Altura]**—Insira o valor em pixels se desejar que a imagem tenha um tamanho fixo. Deixar esse valor em branco torna o ativo adaptável.

   É possível editar as seguintes configurações de **[!UICONTROL Adicionar ao carrinho]** clicando em **[!UICONTROL Editar]** no componente.

* **[!UICONTROL Mostrar ativo]** do produto — Por padrão, esse valor é selecionado. O ativo do produto mostra uma imagem do produto, conforme definido no módulo Comércio. Limpe a marca de seleção para não mostrar o ativo do produto.

* **[!UICONTROL Mostrar preço]** do produto — Por padrão, esse valor é selecionado. O preço do produto mostra o preço do item, conforme definido no módulo Comércio. Limpe a marca de seleção para não mostrar o preço do produto.

* **[!UICONTROL Mostrar formulário]** do produto — Por padrão, esse valor não está selecionado. O Formulário de produto inclui quaisquer variantes de produto, como tamanho e cor. Limpe a marca de seleção para não mostrar as variantes do produto.

### Componente: Mídia panorâmica {#panoramic-media-component}

O componente de Mídia panorâmica é destinado aos ativos que são imagens panorâmicas esféricas. Essas imagens fornecem uma experiência de visualização de 360° de uma sala, propriedade, local ou paisagem. Para que uma imagem seja qualificada como um panorama esférico, ela deve ter um OU ambos os seguintes:

* Uma proporção largura/altura de 2:1.
* Marcado com as palavras-chave `equirectangular` ou (`spherical` + `panorama`) ou (`spherical` + `panoramic`). Consulte [Usando tags](/help/sites-cloud/authoring/features/tags.md).

Tanto a proporção quanto os critérios de palavra-chave se aplicam aos ativos panorâmicos da página de detalhes do ativo e o componente **[!UICONTROL Panorâmica Media]** WCM.

>[!NOTE]
>
>Se sua página da Web tiver o seguinte:
>
>* Várias instâncias do componente **[!UICONTROL Mídia panorâmica]** sendo usado na mesma página.
>* Cada instância usa o mesmo tipo de ativo.

>
>
Observe que não há suporte para a atribuição de uma predefinição do visualizador diferente para cada componente de **[!UICONTROL Mídia panorâmica]** nessa página.
>
>Entretanto, é possível usar a mesma predefinição do visualizador para todos os componentes de Mídia panorâmica que usam ativos do mesmo tipo, na página.

![panorâmico-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

Você pode editar a seguinte configuração tocando em **[!UICONTROL Configurar]** no componente.

* **[!UICONTROL Predefinição]** do visualizador — selecione um visualizador existente no menu suspenso Predefinição do visualizador.

Se a predefinição do visualizador que você está procurando não estiver visível, verifique se ela foi publicada. É necessário publicar as predefinições do visualizador antes de usá-las. Consulte [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

### Componente: Mídia de vídeo 360 {#video-media-component}

Use o componente **[!UICONTROL Vídeo 360 Media]** para renderizar vídeo obrigatório em sua página da Web para obter uma experiência de visualização imersiva de uma sala, propriedade, local, paisagem ou procedimento médico.

Durante a reprodução num visor plano, o utilizador controla o ângulo de visualização; a reprodução em dispositivos móveis normalmente aproveita seus controles giroscópicos incorporados.

O visualizador inclui suporte nativo para o delivery de 360 ativos de vídeo. Por padrão, nenhuma configuração adicional é necessária para exibir ou reproduzir. Você fornece 360 vídeos usando extensões de vídeo padrão, como .mp4, .mkv e .mov. O codec mais comum é H.264.

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

Você pode editar a seguinte configuração tocando em **[!UICONTROL Configurar]** no componente.

* **[!UICONTROL Predefinição]** do visualizador — selecione um visualizador existente no menu suspenso Predefinição do visualizador. Use o Video360VR para usuários finais que usam óculos de realidade virtual. Inclui controles básicos de reprodução de vídeo e recursos de mídia social. Use Video360_social, que inclui controles básicos de reprodução de vídeo. A renderização de vídeo é feita no modo estéreo. O controle manual de ponto de visualização está desligado, mas o controle giroscópico está ligado. Não há recursos de mídia social.

Se a predefinição do visualizador que você está procurando não estiver visível, verifique se ela foi publicada. É necessário publicar as predefinições do visualizador antes de usá-las. Consulte [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

### Usar HTTP/2 para delivery de ativos de Dynamic Media {#using-http-to-delivery-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como os navegadores e servidores se comunicam. Fornece transferência de informações mais rápida e reduz a quantidade de poder de processamento necessário. O delivery de ativos de Dynamic Media agora pode estar acima de HTTP/2, o que oferece melhor resposta e tempo de carregamento.

Consulte [Delivery HTTP2 de Content](/help/assets/dynamic-media/http2faq.md) para obter detalhes completos sobre como começar a usar HTTP/2 com sua conta de Dynamic Media.

>[!MORELIKETHIS]
>
>* [Uso do reprodutor de vídeo no Experience Manager Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html)
>* [Usando vídeo interativo com mídia dinâmica Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html)
>* [Como entender o Asset Viewer com o Experience Manager Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html)
>* [Usando a miniatura de vídeo personalizada com o Experience Manager Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html)
>* [Como entender o gerenciamento de cores com o Experience Manager Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html)
>* [Usando o ajuste de nitidez de imagem com o Experience Manager Dynamic Media](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html)

