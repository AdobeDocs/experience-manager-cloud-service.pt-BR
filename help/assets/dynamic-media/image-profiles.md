---
title: Perfis de imagem do Dynamic Media
description: Saiba como criar Perfis de imagem do Dynamic Media que contêm configurações para Tirar nitidez da máscara e Recorte inteligente, Amostra inteligente ou ambos. Em seguida, aplique o perfil a uma pasta de ativos de imagem.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: 54865fd1be61861b9bed79b1227c6ce209f7e690
workflow-type: tm+mt
source-wordcount: '3490'
ht-degree: 8%

---

# Perfis de imagem do Dynamic Media {#image-profiles}

Ao fazer upload de imagens, você pode cortar automaticamente a imagem após o upload aplicando um Perfil de imagem à pasta.

>[!IMPORTANT]
>
>Os perfis de imagem não se aplicam a arquivos PDF, GIF animados ou INDD (Adobe InDesign).

## Opção Tirar nitidez da máscara {#unsharp-mask}

Ao criar um Perfil de imagem, você pode usar a variável **[!UICONTROL Tirar nitidez da máscara]** opção para ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. É possível controlar a intensidade do efeito, o raio do efeito (medido em pixels) e um limite de contraste que é ignorado. Esse efeito usa as mesmas opções do filtro &quot;Tirar nitidez da máscara&quot; do Adobe Photoshop.

>[!NOTE]
>
>A Tirar nitidez da máscara é aplicada somente a representações em menor escala no PTIFF (tiff de pirâmide) com uma resolução reduzida de mais de 50%. Isso significa que as representações de maior tamanho dentro do ptiff não são afetadas pela máscara não nítida. Enquanto as representações de menor tamanho, como miniaturas, são alteradas (e mostram a máscara não nítida).

Entrada **[!UICONTROL Tirar nitidez da máscara]**, você tem as seguintes opções de filtro:

<table>
 <tbody>
  <tr>
   <td><strong>Opção</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Quantidade</td>
   <td>Controla a quantidade de contraste aplicada aos pixels de borda. O padrão é 1,75. Para imagens de alta resolução, é possível aumentá-las para até 5. Pense na Quantidade como uma medida da intensidade do filtro. O intervalo é de 0 a 5.</td>
  </tr>
  <tr>
   <td>Raio</td>
   <td>Determina o número de pixels em torno dos pixels de borda que afetam a nitidez. Para imagens de alta resolução, insira de 1 a 2. Um valor baixo aplica nitidez apenas aos pixels de borda; um valor alto aplica nitidez a uma faixa mais ampla de pixels. O valor correto depende da imagem. O valor padrão é 0,2. O intervalo é de 0 a 250.</td>
  </tr>
  <tr>
   <td>Limite</td>
   <td><p>Determina o intervalo de contraste que deve ser ignorado quando o filtro Tirar nitidez da máscara é aplicado. Em outras palavras, essa opção determina o quão diferentes os pixels com nitidez devem ser da área ao redor antes de serem considerados pixels de borda e de serem nitidez. Para evitar a introdução de ruídos, experimente valores entre 0 e 255.</p> </td>
  </tr>
 </tbody>
</table>

A nitidez é descrita em [Nitidez de imagens](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## Opções de corte {#crop-options}

Ao implementar o recorte inteligente em imagens, o Adobe recomenda a seguinte prática recomendada e impõe o seguinte limite:

| Ativo - Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| **Imagem** - Número de cortes inteligentes por imagem | 5 | 100 |

Consulte também [Limitações do Dynamic Media](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

As coordenadas de corte inteligente dependem da taxa de proporção. Para as configurações de Corte inteligente em um Perfil de imagem, se a proporção for a mesma para as dimensões adicionadas no Perfil de imagem, a mesma proporção será enviada para o Dynamic Media. A Adobe recomenda usar a mesma área de corte. Isso garante que não haja impacto em diferentes dimensões usadas no Perfil de imagem.

Cada geração de corte inteligente criada requer processamento extra. Por exemplo, adicionar mais de cinco taxas de proporção de corte inteligente pode resultar em uma taxa de assimilação de ativos lenta. Isso também pode causar um aumento de carga nos sistemas. Como você pode aplicar o Corte inteligente no nível da pasta, o Adobe recomenda usá-lo em pastas *somente* onde for necessário.

**Diretrizes para definir o Recorte inteligente em um perfil de imagem**
Para manter o uso do Corte inteligente sob controle e otimizar o tempo de processamento e o armazenamento das lavouras, a Adobe recomenda as seguintes diretrizes e dicas:

* Evite criar perfis de corte inteligente duplicados que tenham os mesmos valores de largura e altura.
* Nomeie os cortes inteligentes com base nas dimensões do corte, não no uso final. Isso ajuda a otimizar para duplicatas em que uma única dimensão é usada em várias páginas.
* Crie perfis de imagem ao nível da página/tipo de ativo para pastas e subpastas específicas em vez de um perfil de recorte inteligente comum que é aplicado a todas as pastas ou todos os ativos.
* Um perfil de imagem aplicado a subpastas substitui um perfil de imagem aplicado à pasta.
* Idealmente, tenha de 10 a 15 recortes inteligentes por imagem para otimizar as taxas de tela e o tempo de processamento.

Há duas opções de corte de imagem para escolher. Também é possível optar por automatizar a criação de amostras de cores e imagens ou preservar o conteúdo do recorte nas resoluções de destino.

>[!IMPORTANT]
>
>A Adobe recomenda que você analise todas as culturas e amostras geradas para garantir que elas sejam apropriadas e relevantes para sua marca e valores.

| Opção | Quando usar | Descrição |
| --- | --- | --- |
| **[!UICONTROL Cortar pixel]** | Imagens de corte em massa somente com base em dimensões. | No **[!UICONTROL Opções de corte]** selecione **[!UICONTROL Cortar pixel]**.<br>Para recortar das laterais de uma imagem, digite o número de pixels a serem recortados de qualquer lado ou de cada lado da imagem. O quanto da imagem é cortada depende da configuração ppi (pixels por polegada) no arquivo de imagem.<br>Um corte de pixel do Perfil de imagem é renderizado da seguinte maneira:<br>· Os valores são Superior, Inferior, Esquerdo e Direito.<br>· Superior esquerdo é considerado `0,0` e o corte de pixels é calculado a partir daí.<br>· Ponto inicial do corte: À esquerda é X e Acima é Y<br>· Cálculo horizontal: tamanho do pixel horizontal da imagem original menos Esquerda e menos Direita.<br>· Cálculo vertical: altura de pixel vertical menos Superior e menos Inferior.<br>Por exemplo, suponha que você tenha uma imagem de 4000 x 3000 pixels. Você usa valores: Top=250, Bottom=500, Left=300, Right=700.<br>A partir da parte superior esquerda (300,250), recorte usando o espaço de preenchimento de (4000-300-700, 3000-250-500 ou 3000,2250). |
| **[!UICONTROL Corte inteligente]** | Recorte de imagens em massa com base em seu ponto focal visual. | O Recorte inteligente usa o poder da inteligência artificial no Adobe Sensei para automatizar rapidamente o recorte de imagens em massa. O Corte inteligente detecta automaticamente e recorta até o ponto focal em qualquer imagem para adquirir o ponto de interesse desejado, independentemente do tamanho da tela.<br>No **[!UICONTROL Opções de corte]** selecione **[!UICONTROL Corte inteligente]**, depois à direita de **[!UICONTROL Recorte responsivo de imagem]**, ative (ative) o recurso.<br>Os tamanhos padrão dos pontos de interrupção (**[!UICONTROL Grande]**, **[!UICONTROL Medium]**, **[!UICONTROL Pequeno]**) abrangem a gama completa de tamanhos que a maioria das imagens é usada em dispositivos móveis e tablets, desktops e banners. Se desejar, você pode editar os nomes padrão Grande, Médio e Pequeno.<br>Para adicionar mais pontos de interrupção, selecione **[!UICONTROL Adicionar corte]**; para excluir um corte, selecione o ícone Lixeira. |
| **[!UICONTROL Amostra de cor e imagem]** | O gera uma amostra de imagem em massa para cada imagem. | **Nota**: a amostra inteligente não é compatível com o Dynamic Media Classic.<br>Localize e gere automaticamente amostras de alta qualidade a partir de imagens de produtos que mostram cor ou textura.<br>No **[!UICONTROL Opções de corte]** selecione **[!UICONTROL Corte inteligente]**. Em seguida, à direita de **[!UICONTROL Amostra de cor e imagem]**, ative (ative) o recurso. Insira um valor de pixel no campo **[!UICONTROL Largura]** e **[!UICONTROL Altura]** caixas de texto.<br>Embora todas as recortes de imagem estejam disponíveis no painel Representações, as amostras são usadas somente por meio da **[!UICONTROL Copiar URL]** recurso. Use seu próprio componente de visualização para renderizar a amostra em seu site. A exceção a essa regra são os banners do carrossel. O Dynamic Media fornece o componente de visualização para a amostra usada nos banners do carrossel.<br><br>**Uso de amostras de imagem**<br> O URL para amostras de imagem é simples:<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>Onde `:Swatch` está anexado à solicitação de ativo.<br><br>**Uso de amostras de cores**<br> Para usar amostras de cores, você faz um `req=userdata` solicitação com o seguinte:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Por exemplo, este é um ativo de amostra no Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>E aqui está a amostra do ativo correspondente `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>A variável `req=userdata` resposta é a seguinte:<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>Você também pode solicitar uma `req=userdata` resposta no formato XML ou JSON, como nos seguintes exemplos de URL:<br>·`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>·`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Nota**: crie seu próprio componente WCM para solicitar uma amostra de cor e analisar o `SmartSwatchColor` atributo, representado por um valor hexadecimal RGB de 24 bits.<br>Consulte também [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) no Guia de referência de visualizadores. |
| **[!UICONTROL Preservar conteúdo de corte nas resoluções de destino]** | Para manter o conteúdo do corte na mesma proporção | Use quando criar um perfil de recorte inteligente.<br>Desmarque essa opção para gerar novo conteúdo de corte, mantendo o ponto focal, para uma determinada taxa de proporção em diferentes resoluções.<br>Se você decidir desmarcar essa caixa, verifique se a resolução da imagem original é superior às resoluções definidas para o seu perfil de Recorte inteligente.<br><br>Por exemplo, suponha que você tenha definido as taxas de proporção em 600 x 600 (Grande), 400 x 400 (Médio) e 300 x 300 (Pequeno).<br>Quando **[!UICONTROL Preservar conteúdo de corte nas resoluções de destino]** opção é *marcado*, você verá o mesmo recorte em todas as três resoluções, semelhante ao seguinte exemplo de saída de imagens (somente para fins ilustrativos):<br>![Opção marcada](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>Quando **[!UICONTROL Preservar conteúdo de corte nas resoluções de destino]** opção é *desmarcado*, o conteúdo do recorte é novo para todas as três resoluções, semelhante ao seguinte exemplo de saída de imagens (somente para fins ilustrativos):<br>![Opção desmarcada](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### Formatos de arquivo de imagem compatíveis com Recorte inteligente e Amostras de cor

A resolução máxima de tamanho de arquivo de entrada é de 16K.

>[!NOTE]
>
>A resolução de 16K é uma resolução de tela com aproximadamente 16.000 pixels horizontalmente. A resolução de 16 K mais comumente discutida é 15360 × 8640, o que dobra a contagem de pixels de 8K UHD em cada dimensão, para um total de quatro vezes mais pixels. Essa resolução tem 132,7 megapixels, 16 vezes mais pixels do que a resolução 4K e 64 vezes mais pixels do que a resolução 1080p.

| Formato da imagem | Extensão de arquivo que não diferencia maiúsculas de minúsculas | Tipo MIME | Espaço de cor de entrada compatível | Tamanho máximo de arquivo de entrada com suporte | Formato de imagem compatível? |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | Sim |
| CMYK |  |  |  |  | Sim |
| EPS |  |  |  |  | Não |
| GIF | `.gif` | image/gif | sRGB | 15 GB | Sim; o primeiro quadro do GIF animado é usado para a representação. Não é possível configurar ou alterar o primeiro quadro. |
| JPEG | `.jpg` e `.jpeg` | image/jpeg | sRGB | 15 GB | Sim |
| PNG | `.png` | image/png | sRGB | 15 GB | Sim |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | Sim |
| SVG |  |  |  |  | Não |
| TIFF | `.tif` e `.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | Sim |
| WebP/WebP animado |  |  |  |  | Não |

## Criar perfis de imagem do Dynamic Media {#creating-image-profiles}

Para definir parâmetros de processamento avançado para outros tipos de ativos, consulte [Configuração do processamento de ativos](config-dm.md#configuring-asset-processing).

Consulte [Sobre perfis de imagem e perfis de vídeo do Dynamic Media](/help/assets/dynamic-media/about-image-video-profiles.md).

Consulte também [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).

**Para criar perfis de imagem do Dynamic Media:**

1. Selecione o logotipo do Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de imagem]**.
1. Para adicionar um Perfil de imagem, selecione **[!UICONTROL Criar]**.
1. Insira um nome de perfil e valores para Tirar nitidez da máscara, do recorte ou da amostra, ou ambos.

   Dica: use um nome de perfil específico para sua finalidade. Por exemplo, suponha que você queira criar um perfil que gere apenas amostras. Ou seja, o Corte inteligente está desativado (desativado) e a opção Cor e amostra de imagem está ativada (ativada). Nesses casos, você pode usar o nome de perfil &quot;Amostras inteligentes&quot;.

   Consulte também [Opções de recorte inteligente e amostra inteligente](#crop-options) e [Tirar nitidez da máscara](#unsharp-mask).

   ![cortar](assets/crop.png)

1. Selecione **[!UICONTROL Salvar]**. O perfil recém-criado aparece na lista de perfis disponíveis.

## Editar ou excluir perfis de imagem do Dynamic Media {#editing-or-deleting-image-profiles}

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja editar ou remover. Para editá-lo, selecione **[!UICONTROL Editar perfil de processamento da imagem]**. Para removê-lo, selecione **[!UICONTROL Excluir perfil de processamento da imagem]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Se estiver editando, salve as alterações. Se estiver excluindo, confirme se deseja remover o perfil.

## Aplicar um perfil de imagem do Dynamic Media a pastas {#applying-an-image-profile-to-folders}

Quando você atribui um Perfil de imagem a uma pasta, todas as subpastas herdam automaticamente o perfil da pasta principal. Dessa forma, você pode atribuir apenas um Perfil de imagem a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você faz upload, armazena, usa e arquiva ativos.

Se você atribuiu um Perfil de imagem diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos que são adicionados à pasta posteriormente.

As pastas que têm um perfil atribuído a elas são indicadas na interface com o nome do perfil que aparece no cartão.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Aplique Perfis de imagem a pastas específicas ou globalmente a todos os ativos.

É possível reprocessar ativos em uma pasta que já tenha um Perfil de imagem existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Aplicar perfis de imagem do Dynamic Media a pastas específicas {#applying-image-profiles-to-specific-folders}

Aplique um Perfil de imagem a uma pasta na **[!UICONTROL Ferramentas]** ou se estiver na pasta, em **[!UICONTROL Propriedades]**.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Aplicar Perfis de imagem do Dynamic Media a pastas da interface do usuário Perfis {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja aplicar a uma ou várias pastas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Selecionar **[!UICONTROL Aplicar perfil de processamento às pastas]** e selecione uma ou várias pastas que deseja usar para receber os ativos carregados recentemente e selecione **[!UICONTROL Aplicar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

#### Aplicar perfis de imagem do Dynamic Media a pastas de propriedades {#applying-image-profiles-to-folders-from-properties}

1. Toque no logotipo do Experience Manager e acesse **[!UICONTROL Assets]**.
1. Navegue até um *pasta* (não um ativo) ao qual você deseja aplicar um perfil de imagem.
1. Dependendo da exibição em que você estiver, execute um dos procedimentos a seguir:
   * Na Exibição de cartão, passe o mouse sobre o ponteiro na pasta e selecione a marca de seleção para selecioná-lo.
   * Na Exibição de coluna ou na Exibição de lista, marque a caixa de seleção à esquerda do nome da pasta.
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Selecione o **[!UICONTROL Processamento Dynamic Media]** guia.
1. Em **[!UICONTROL Perfil de imagem]**, do **[!UICONTROL Nome do perfil]** selecione o perfil a ser aplicado.
1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar e fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicar um perfil de imagem do Dynamic Media globalmente {#applying-an-image-profile-globally}

Além de aplicar um perfil a uma pasta, você também pode aplicar um globalmente. Qualquer conteúdo carregado no Experience Manager Assets em qualquer pasta tem o perfil selecionado aplicado.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Para aplicar um Perfil de imagem do Dynamic Media globalmente:**

1. Siga uma das seguintes opções:

   * Navegue até `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e aplique o perfil apropriado e selecione **[!UICONTROL Salvar]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navegue até o CRXDE Lite para o seguinte nó: `/content/dam/jcr:content`.

      Adicionar a propriedade `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e selecione **[!UICONTROL Salvar tudo]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## Editar o recorte inteligente ou a amostra inteligente de uma única imagem {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>A Adobe recomenda que você analise todas as culturas inteligentes geradas e amostras inteligentes para garantir que elas sejam apropriadas e relevantes para sua marca e valores.

Você pode realinhar ou redimensionar manualmente a janela de recorte inteligente de uma imagem para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em todos os lugares em que você usa o recorte para as imagens específicas.

>[!IMPORTANT]
>
>Ao realinhar ou redimensionar manualmente a janela de recorte inteligente de um ativo, essa edição é mantida e preservada, mesmo que você decida reprocessar o ativo posteriormente. No entanto, se você editar a largura, a altura ou ambos no **[!UICONTROL Recorte responsivo de imagem]** do Perfil de imagem, esse ativo estará sujeito a reprocessamento.
>Consulte [Reprocessar ativos do Dynamic Media em uma pasta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Você pode executar novamente o corte inteligente para gerar os cortes adicionais novamente, se necessário.

Consulte também [Editar o recorte inteligente ou a amostra inteligente de várias imagens](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar o recorte inteligente ou a amostra inteligente de uma única imagem:**

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Assets]**, em seguida, para a pasta que tem um recorte inteligente ou um Perfil de imagem de amostra inteligente aplicado a ela.
1. Para abrir o conteúdo, selecione a pasta.
1. Selecione a imagem cujo recorte inteligente ou amostra inteligente você deseja ajustar.
1. Na barra de ferramentas, selecione **[!UICONTROL Corte inteligente]**.

1. Siga um destes procedimentos:

   * Próximo ao canto superior direito da página, arraste a barra deslizante para a esquerda ou direita para aumentar ou diminuir a exibição da imagem, respectivamente.
   * Na imagem, arraste uma alça de canto para ajustar o tamanho da área visível do corte ou da amostra.
   * Na imagem, arraste a caixa/amostra para um novo local. Só é possível editar amostras de imagens; as amostras de cores são estáticas.
   * Acima da imagem, selecione  **[!UICONTROL Reverter]** para desfazer todas as edições e restaurar o recorte ou a amostra original.
   * Use as teclas de seta do teclado para recortar o tamanho do quadro ou reposicionar a imagem, ou ambos.

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]** e selecione **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Editar o recorte inteligente ou a amostra inteligente de várias imagens {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>A Adobe recomenda que você analise todas as culturas inteligentes geradas e amostras inteligentes para garantir que elas sejam apropriadas e relevantes para sua marca e valores.

Depois de aplicar um Perfil de imagem - contendo Recorte inteligente - a uma pasta, todas as imagens nessa pasta têm um recorte aplicado a elas. Se desejar, é possível *manualmente* realinhar ou redimensionar a janela de recorte inteligente em várias imagens para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em todos os lugares em que você usa o recorte para as imagens específicas.

>[!IMPORTANT]
>
>Ao realinhar ou redimensionar manualmente a janela de recorte inteligente de vários ativos, essas edições são mantidas e preservadas, mesmo que você decida reprocessar esses ativos posteriormente. No entanto, se você editar a largura, a altura ou ambos na área **[!UICONTROL Recorte de imagem responsivo]** do Perfil de imagem, esses ativos estarão sujeitos a reprocessamento.
>Consulte [Reprocessar ativos do Dynamic Media em uma pasta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Você pode executar novamente o corte inteligente para gerar os cortes adicionais novamente, se necessário.

**Para editar o recorte inteligente ou a amostra inteligente de várias imagens:**

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Assets]**, em seguida, para uma pasta que tenha um Recorte inteligente ou um Perfil de imagem de amostra inteligente aplicado a ela.
1. Na pasta, selecione o **[!UICONTROL Mais ações]** (...) e selecione **[!UICONTROL Corte inteligente]**.

1. No **[!UICONTROL Editar cortes inteligentes]** faça o seguinte:

   * Ajuste o tamanho de exibição das imagens na página.

      À direita da lista suspensa de nomes dos pontos de interrupção, arraste a barra deslizante para a esquerda ou direita para alterar o tamanho da exibição da imagem visível.

      ![edit_smart_crop-slibar](assets/edit_smart_crops-sliderbar.png)

   * Filtrar a lista de imagens visualizáveis com base nos nomes dos pontos de interrupção. No exemplo abaixo, as imagens são filtradas no nome do ponto de interrupção &quot;Médio&quot;.

      Próximo ao canto superior direito da página, na lista suspensa, selecione um nome de ponto de interrupção para filtrar em quais imagens você vê. (Veja a imagem acima.)

      ![edit_smart_crop-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Redimensionar a caixa de corte inteligente. Siga um destes procedimentos:

      * Se a imagem tiver apenas um recorte inteligente ou uma amostra inteligente, arraste a alça do canto da caixa de recorte. Ajuste o tamanho da área visível do corte.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a alça de canto da caixa de recorte. Ajuste o tamanho da área visível do corte. Ou selecione a amostra inteligente abaixo da imagem (as amostras de cores são estáticas) e arraste a alça do canto da caixa de corte. Ajuste o tamanho da área visível da amostra.

      ![Redimensionamento do recorte inteligente de uma imagem](assets/edit_smart_crops-resize.png).

   * Mova a caixa de corte inteligente. Siga um destes procedimentos:

      * Se a imagem tiver apenas um recorte inteligente ou uma amostra inteligente, arraste a caixa de recorte para um novo local na imagem.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a caixa de recorte inteligente para um novo local na imagem. Ou selecione a amostra inteligente abaixo da imagem (as amostras de cores são estáticas) e arraste a caixa de recorte da amostra inteligente para um novo local.

      ![edit_smart_crop-move](assets/edit_smart_crops-move.png)

   * Desfazer todas as edições e restaurar o recorte inteligente original ou a amostra inteligente (aplica-se somente à sessão de edição atual).

      Selecionar **[!UICONTROL Reverter]** acima da imagem.

      ![edit_smart_crop-revert](assets/edit_smart_crops-revert.png)



1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]** e selecione **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Remover um perfil de imagem das pastas {#removing-an-image-profile-from-folders}

Ao remover um Perfil de imagem de uma pasta, todas as subpastas herdam automaticamente a remoção do perfil da pasta principal. No entanto, qualquer processamento de arquivos que tenha ocorrido nas pastas permanece intacto.

Remova um Perfil de imagem de uma pasta na **[!UICONTROL Ferramentas]** ou se estiver na pasta, em **[!UICONTROL Propriedades]**.

### Remover perfis de imagem do Dynamic Media de pastas por meio da interface do usuário Perfis {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja remover de uma ou várias pastas.
1. Selecionar **[!UICONTROL Remover perfil de processamento das pastas]** e selecione uma ou várias pastas que deseja usar para remover o perfil e selecione **[!UICONTROL Remover]**.

   É possível confirmar que o Perfil de imagem não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remova Perfis de imagem do Dynamic Media das pastas por meio de Propriedades {#removing-image-profiles-from-folders-via-properties}

1. Selecione o logotipo do Experience Manager e navegue **[!UICONTROL Assets]** e, em seguida, na pasta da qual você deseja remover um Perfil de imagem.
1. Na pasta, marque a marca de seleção para selecioná-la e, em seguida, selecione **[!UICONTROL Propriedades]**.
1. Selecione o **[!UICONTROL Perfis de imagem]** guia.
1. No **[!UICONTROL Nome do perfil]** selecione **[!UICONTROL Nenhum]** e selecione **[!UICONTROL Salvar e fechar]**.

   As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.
