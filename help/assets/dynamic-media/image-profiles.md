---
title: Perfis de imagem do Dynamic Media
description: Saiba como criar Perfis de imagem do Dynamic Media que contêm configurações para a máscara de nitidez e recorte inteligente ou amostra inteligente, ou ambos. Em seguida, aplique o perfil a uma pasta de ativos de imagem.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: c15486fb3de73773fa7e255809ffaa36715cea05
workflow-type: tm+mt
source-wordcount: '3529'
ht-degree: 7%

---

# Perfis de imagem do Dynamic Media {#image-profiles}

Ao fazer upload de imagens, você pode cortar automaticamente a imagem ao fazer upload aplicando um Perfil de imagem à pasta.

>[!IMPORTANT]
>
>Os Perfis de imagem não se aplicam a arquivos PDF, GIF animado ou INDD (Adobe InDesign).

## Opção Tirar nitidez da máscara {#unsharp-mask}

Ao criar um Perfil de imagem, você pode usar a variável **[!UICONTROL Tirar nitidez da máscara]** para ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. Você pode controlar a intensidade do efeito, o raio do efeito (medido em pixels) e um limite de contraste que é ignorado. Esse efeito usa as mesmas opções do filtro &quot;Tirar nitidez da máscara&quot; da Adobe Photoshop.

>[!NOTE]
>
>A Tirar nitidez da máscara é aplicada apenas a representações baixadas dentro do PTIFF (tiff de pirâmide) que têm uma resolução reduzida de mais de 50%. Isso significa que as representações de maior porte dentro do ptiff não são afetadas pela máscara de nitidez. Enquanto as representações de menor tamanho, como miniaturas, são alteradas (e mostram a máscara de nitidez).

Em **[!UICONTROL Tirar nitidez da máscara]**, você tem as seguintes opções de filtragem:

<table>
 <tbody>
  <tr>
   <td><strong>Opção</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Quantidade</td>
   <td>Controla a quantidade de contraste aplicado aos pixels da borda. O padrão é 1,75. Para imagens de alta resolução, é possível aumentá-lo para 5. Pense em Quantia como uma medida de intensidade de filtro. O intervalo é de 0 a 5.</td>
  </tr>
  <tr>
   <td>Raio</td>
   <td>Determina o número de pixels em torno dos pixels de borda que afetam a nitidez. Para imagens de alta resolução, insira de 1 a 2. Um valor baixo aplica nitidez apenas aos pixels de borda; um valor alto aplica nitidez a uma faixa mais ampla de pixels. O valor correto depende da imagem. O valor padrão é 0,2. O intervalo é de 0 a 250.</td>
  </tr>
  <tr>
   <td>Limite</td>
   <td><p>Determina o intervalo de contraste a ser ignorado quando o filtro de máscara de nitidez for aplicado. Em outras palavras, essa opção determina o quão diferentes os pixels com nitidez devem ser da área ao redor antes de serem considerados pixels de borda e terem nitidez. Para evitar a introdução de ruído, experimente valores entre 0 e 255.</p> </td>
  </tr>
 </tbody>
</table>

A nitidez é descrita em [Nitidez de imagens](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## Opções de corte {#crop-options}

Quando você implementa o recorte inteligente em imagens, o Adobe recomenda a seguinte prática recomendada e aplica o seguinte limite:

| Ativo - Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| **Imagem** - Número de Smart Crops por imagem | 5 | 100 |

Consulte também [Limitações do Dynamic Media](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

As coordenadas de recorte inteligente dependem da taxa de proporção. Para as configurações de Recorte inteligente em um Perfil de imagem, se a proporção for a mesma para as dimensões adicionadas no Perfil de imagem, a mesma proporção de aspecto será enviada para a Dynamic Media. O Adobe recomenda usar a mesma área de corte. Isso garante que não haja impacto para diferentes dimensões usadas no Perfil de imagem.

Cada geração de recorte inteligente criada requer processamento extra. Por exemplo, adicionar mais de cinco taxas de proporção de recorte inteligente pode resultar em uma taxa lenta de ingestão de ativos. Também pode causar um aumento da carga nos sistemas. Como você pode aplicar o Recorte inteligente no nível da pasta, o Adobe recomenda usá-lo nas pastas *only* quando necessário.

**Diretrizes para definir o Recorte inteligente em um perfil de imagem**
Para manter o uso do Smart Crop sob controle e otimizar o tempo de processamento e o armazenamento de colheitas, o Adobe recomenda as seguintes diretrizes e dicas:

* Os ativos de imagem que terão um recorte inteligente aplicado a eles devem ter no mínimo 50 x 50 pixels ou mais.
* Idealmente, tenha 10 a 15 recortes inteligentes por imagem para otimizar as taxas de tela e o tempo de processamento.
* Nomeie as culturas inteligentes com base em dimensões de corte, não no uso final. Isso ajuda a otimizar para duplicatas, onde uma única dimensão é usada em várias páginas.
* Crie perfis de imagem em toda a página/no tipo de ativo para pastas e subpastas específicas em vez de um perfil de recorte inteligente comum aplicado a todas as pastas ou a todos os ativos.
* Um perfil de Imagem aplicado às subpastas substitui um perfil de Imagem aplicado à pasta.
* Não é permitido um Perfil de imagem que contenha dimensões de recorte inteligente duplicadas.
* Não são permitidos perfis de imagem com nome duplicado que tenham opções de recorte inteligente definidas.

Você tem duas opções de recorte de imagem para escolher: Corte de pixels e Corte inteligente. Você também pode optar por automatizar a criação de amostras de cores e imagens ou preservar o conteúdo de corte nas resoluções do target.

>[!IMPORTANT]
>
>O Adobe recomenda que você analise todas as culturas e amostras geradas para garantir que elas sejam apropriadas e relevantes para sua marca e valores.

| Opção | Quando usar | Descrição |
| --- | --- | --- |
| **[!UICONTROL Cortar pixel]** | Imagens de corte em massa com base somente em dimensões. | No **[!UICONTROL Opções de corte]** , selecione **[!UICONTROL Corte de pixels]**.<br>Para cortar das laterais de uma imagem, você insere o número de pixels para cortar de qualquer lado ou de cada lado da imagem. A quantidade de imagens cortadas depende da configuração ppi (pixels por polegada) no arquivo de imagem.<br>Um corte de pixels do Perfil de imagem é renderizado da seguinte maneira:<br>・ Os valores são Superior, Inferior, Esquerda e Direita.<br>・ A parte superior esquerda é considerada `0,0` e o corte de pixels é calculado a partir daí.<br>・ Ponto de partida do corte: A esquerda é X e a parte superior é Y<br>・ Cálculo horizontal: tamanho de pixel horizontal da imagem original menos Esquerda e depois menos Direita.<br>・ Cálculo vertical: altura vertical do pixel menos Superior e depois menos Inferior.<br>Por exemplo, suponha que você tenha uma imagem de 4000 x 3000 pixels. Você usa valores: Superior=250, Inferior=500, Esquerda=300, Direita=700.<br>Do corte superior esquerdo (300.250) usando o espaço de preenchimento de (4000-300-700, 3000-250-500 ou 3000.2250). |
| **[!UICONTROL Corte inteligente]** | Imagens de corte em massa com base em seu ponto focal visual. | O Smart Crop usa o poder da inteligência artificial no Adobe Sensei para automatizar rapidamente o corte de imagens em massa. O Recorte inteligente detecta e recorta automaticamente o ponto focal em qualquer imagem para adquirir o ponto de interesse pretendido, independentemente do tamanho da tela.<br>No **[!UICONTROL Opções de corte]** , selecione **[!UICONTROL Corte inteligente]**, em seguida à direita de **[!UICONTROL Recorte responsivo de imagem]**, ative (ative) o recurso.<br>Os tamanhos padrão do ponto de interrupção (**[!UICONTROL Grande]**, **[!UICONTROL Médio]**, **[!UICONTROL Pequeno]**) cobre a gama completa de tamanhos que a maioria das imagens é usada em dispositivos móveis e tablets, desktops e banners. Se desejar, você pode editar os nomes padrão de Grande, Médio e Pequeno.<br>Para adicionar mais pontos de interrupção, selecione **[!UICONTROL Adicionar corte]**; para excluir um corte, selecione o ícone Garbage Can . |
| **[!UICONTROL Amostra de cor e imagem]** | Em massa gera uma amostra de imagem para cada imagem. | **Observação**: O Smart Swatch não é compatível com o Dynamic Media Classic.<br>Localize e gere automaticamente amostras de alta qualidade a partir de imagens de produto que mostram cor ou textura.<br>No **[!UICONTROL Opções de corte]** , selecione **[!UICONTROL Corte inteligente]**. Então à direita de **[!UICONTROL Amostra de cor e imagem]**, ative (ative) o recurso. Insira um valor de pixel na variável **[!UICONTROL Largura]** e **[!UICONTROL Altura]** caixas de texto.<br>Embora todas as culturas de imagens estejam disponíveis no painel Representações , as amostras são usadas somente por meio do **[!UICONTROL Copiar URL]** recurso. Use seu próprio componente de visualização para renderizar a amostra em seu site. A exceção a essa regra são os banners de carrossel. O Dynamic Media fornece o componente de visualização para a amostra usada em banners de carrossel.<br><br>**Uso de amostras de imagem**<br> O URL para amostras de imagem é direto:<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>Onde `:Swatch` é anexada à solicitação de ativo.<br><br>**Uso de amostras de cores**<br> Para usar amostras de cores, você cria uma `req=userdata` com o seguinte:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Por exemplo, o seguinte é um ativo de amostra no Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>E aqui está o ativo de amostra correspondente `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>O `req=userdata` A resposta é a seguinte:<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>Você também pode solicitar um `req=userdata` resposta no formato XML ou JSON, como nos seguintes exemplos de URL respectivos:<br>・ ・`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>・ ・`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Observação**: Você deve criar seu próprio componente WCM para solicitar uma amostra de cores e analisar a `SmartSwatchColor` , representado por um valor RGB hexadecimal de 24 bits.<br>Consulte também [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) no Guia de referência de visualizadores. |
| **[!UICONTROL Preservar conteúdo de corte nas resoluções de destino]** | Para manter o conteúdo de corte na mesma proporção | Use ao criar um perfil de recorte inteligente.<br>Para gerar novo conteúdo de corte - mantendo o ponto focal - para uma determinada proporção em diferentes resoluções, desmarque esta opção <br>Se você decidir desmarcar esta caixa, verifique se a resolução da imagem original é maior que as resoluções definidas para o seu perfil de Recorte inteligente.<br><br>Por exemplo, suponha que você tenha definido as taxas de proporção em 600 x 600 (Grande), 400 x 400 (Médio) e 300 x 300 (Pequeno).<br>When **[!UICONTROL Preservar conteúdo de corte nas resoluções do target]** é *verificado*, você verá o mesmo corte em todas as três resoluções, semelhante à seguinte saída de amostra de imagens (somente para fins ilustrativos):<br>![Opção marcada](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>When **[!UICONTROL Preservar conteúdo de corte nas resoluções do target]** é *desmarcado*, o conteúdo de corte é novo em todas as três resoluções, semelhante à seguinte saída de exemplo de imagens (somente para fins ilustrativos):<br>![Opção desmarcada](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### Formatos de arquivo de imagem compatíveis com o Recorte inteligente e Amostras de cores

A resolução máxima de tamanho de arquivo de entrada compatível é de 16K.

>[!NOTE]
>
>Resolução de 16K é uma resolução de exibição com aproximadamente 16.000 pixels horizontalmente. A resolução de 16K mais comumente discutida é de 15360 × 8640, o que dobra a contagem de pixels de 8K UHD em cada dimensão, para um total de quatro vezes mais pixels. Essa resolução tem 132,7 megapixels, 16 vezes mais pixels do que a resolução de 4K e 64 vezes mais pixels do que a resolução de 1080p.

| Formato de imagem | Extensão de arquivo que não diferencia maiúsculas de minúsculas | Tipo MIME | Espaço de cores de entrada suportado | Tamanho máximo suportado do arquivo de entrada | Formato de imagem suportado? |
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

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configuração do processamento de ativos](config-dm.md#configuring-asset-processing).

Consulte [Sobre perfis de imagem e perfis de vídeo do Dynamic Media](/help/assets/dynamic-media/about-image-video-profiles.md).

Consulte também [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).

**Para criar perfis de imagem do Dynamic Media:**

1. Selecione o logotipo do Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de imagem]**.
1. Para adicionar um Perfil de imagem, selecione **[!UICONTROL Criar]**.
1. Insira um nome de perfil e valores para Tirar nitidez da máscara, recortar ou amostra, ou ambos.

   Dica: Use um nome de perfil específico para a finalidade pretendida. Por exemplo, suponha que você queira criar um perfil que gere somente amostras. Ou seja, o Recorte inteligente está desativado (desativado) e a Amostra de cor e imagem está ativada (ativada). Nesses casos, você pode usar o nome de perfil &quot;Smart Swatches&quot;.

   Consulte também [Opções de recorte inteligente e amostra inteligente](#crop-options) e [Tirar nitidez da máscara](#unsharp-mask).

   ![cultura](assets/crop.png)

1. Selecione **[!UICONTROL Salvar]**. O perfil recém-criado aparece na lista de perfis disponíveis.

## Editar ou excluir perfis de imagem do Dynamic Media {#editing-or-deleting-image-profiles}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja editar ou remover. Para editá-lo, selecione **[!UICONTROL Editar perfil de processamento de imagem]**. Para removê-lo, selecione **[!UICONTROL Excluir perfil de processamento de imagem]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Se estiver editando, salve as alterações. Se estiver excluindo, confirme se deseja remover o perfil.

## Aplicar um perfil de imagem do Dynamic Media a pastas {#applying-an-image-profile-to-folders}

Ao atribuir um Perfil de imagem a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta pai. Dessa forma, você pode atribuir somente um Perfil de imagem a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você faz upload, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de imagem diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos que são adicionados à pasta posteriormente.

As pastas que têm um perfil atribuído a elas são indicadas na interface do usuário com o nome do perfil que aparece no cartão.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Você pode aplicar Perfis de imagem a pastas específicas ou globalmente a todos os ativos.

Você pode reprocessar ativos em uma pasta que já tenha um Perfil de imagem existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Aplicar perfis de imagem do Dynamic Media a pastas específicas {#applying-image-profiles-to-specific-folders}

Você pode aplicar um Perfil de imagem a uma pasta de dentro do **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Aplicar perfis de imagem do Dynamic Media a pastas da interface do usuário Perfis {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja aplicar a uma ou várias pastas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Selecionar **[!UICONTROL Aplicar perfil de processamento a pastas]** e selecione a pasta ou várias pastas que deseja usar para receber os ativos carregados recentemente e selecione **[!UICONTROL Aplicar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

#### Aplicar perfis de imagem do Dynamic Media a pastas de Propriedades {#applying-image-profiles-to-folders-from-properties}

1. Toque no logotipo do Experience Manager e navegue até **[!UICONTROL Ativos]**.
1. Navegue até um *pasta* (não é um ativo) ao qual você deseja aplicar um perfil de imagem.
1. Dependendo da exibição em que você estiver, execute um dos seguintes procedimentos:
   * Na Exibição de cartão, passe o ponteiro sobre a pasta e selecione a marca de seleção para selecioná-la.
   * Em Exibição de coluna ou Exibição de lista, marque a caixa de seleção à esquerda do nome da pasta.
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Selecione o **[!UICONTROL Processamento Dynamic Media]** guia .
1. Em **[!UICONTROL Perfil de imagem]** do **[!UICONTROL Nome do perfil]** selecione o perfil a ser aplicado.
1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Salvar e fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicar um perfil de imagem do Dynamic Media globalmente {#applying-an-image-profile-globally}

Além de aplicar um perfil a uma pasta, também é possível aplicá-lo globalmente. Qualquer conteúdo carregado no Experience Manager Assets em qualquer pasta tem o perfil selecionado aplicado.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessar ativos em uma pasta depois de ter editado seu perfil de processamento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Para aplicar um Perfil de imagem do Dynamic Media globalmente:**

1. Siga uma das seguintes opções:

   * Navegar para `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e aplique o perfil apropriado e selecione **[!UICONTROL Salvar]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navegue até CRXDE Lite para o seguinte nó: `/content/dam/jcr:content`.

      Adicionar a propriedade `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e selecione **[!UICONTROL Salvar tudo]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## Editar o recorte inteligente ou a amostra inteligente de uma única imagem {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>O Adobe recomenda que você analise todas as culturas inteligentes e amostras inteligentes geradas para garantir que elas sejam apropriadas e relevantes para sua marca e valores.

Você pode realinhar ou redimensionar manualmente a janela de recorte inteligente de uma imagem para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em todos os locais em que você usa o recorte para as imagens específicas.

>[!IMPORTANT]
>
>Quando você realinha ou redimensiona manualmente a janela de recorte inteligente de um ativo, essa edição é mantida e preservada, mesmo se posteriormente você decidir reprocessar o ativo. No entanto, se você editar a largura, a altura ou ambos na variável **[!UICONTROL Recorte responsivo de imagem]** do Perfil de imagem, esse ativo está sujeito ao reprocessamento.
>Consulte [Reprocessar ativos do Dynamic Media em uma pasta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Você pode executar o recorte inteligente novamente para gerar as culturas adicionais, se necessário.

Consulte também [Editar o recorte inteligente ou a amostra inteligente de várias imagens](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar o recorte inteligente ou a amostra inteligente de uma única imagem:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ativos]**, em seguida, na pasta que tem um recorte inteligente ou um Perfil de imagem de amostra inteligente aplicado a ele.
1. Para abrir seu conteúdo, selecione a pasta .
1. Selecione a imagem cujo recorte inteligente ou amostra inteligente você deseja ajustar.
1. Na barra de ferramentas, selecione **[!UICONTROL Corte inteligente]**.

1. Siga um destes procedimentos:

   * Próximo ao canto superior direito da página, arraste a barra de controle deslizante para a esquerda ou para a direita para aumentar ou diminuir a exibição da imagem, respectivamente.
   * Na imagem, arraste uma alça de canto para ajustar o tamanho da área visível do corte ou amostra.
   * Na imagem, arraste a caixa/amostra para um novo local. Você só pode editar amostras de imagens; amostras de cores são estáticas.
   * Acima da imagem, selecione  **[!UICONTROL Reverter]** para desfazer todas as edições e restaurar o corte ou a amostra original.
   * Use as teclas de seta do teclado para recortar o tamanho do quadro, ou reposicionar a imagem, ou ambos.

1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Salvar]**, em seguida selecione **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Editar o recorte inteligente ou a amostra inteligente de várias imagens {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>O Adobe recomenda que você analise todas as culturas inteligentes e amostras inteligentes geradas para garantir que elas sejam apropriadas e relevantes para sua marca e valores.

Depois de aplicar um Perfil de imagem - contendo Recorte inteligente - a uma pasta, todas as imagens nessa pasta têm um recorte aplicado a elas. Se desejar, é possível *manualmente* realinhar ou redimensionar a janela de recorte inteligente em várias imagens para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em todos os locais em que você usa o recorte para as imagens específicas.

>[!IMPORTANT]
>
>Ao realinhar ou redimensionar manualmente a janela de recorte inteligente de vários ativos, essas edições são mantidas e preservadas, mesmo que você decida reprocessar esses ativos posteriormente. No entanto, se você editar a largura, a altura ou ambos na área **[!UICONTROL Recorte de imagem responsivo]** do Perfil de imagem, esses ativos estarão sujeitos a reprocessamento.
>Consulte [Reprocessar ativos do Dynamic Media em uma pasta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Você pode executar o recorte inteligente novamente para gerar as culturas adicionais, se necessário.

**Para editar o recorte inteligente ou a amostra inteligente de várias imagens:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ativos]**, em seguida, em uma pasta que tenha um recorte inteligente ou um Perfil de imagem de amostra inteligente aplicado a ele.
1. Na pasta , selecione o **[!UICONTROL Mais ações]** ícone (...) e selecione **[!UICONTROL Corte inteligente]**.

1. No **[!UICONTROL Editar recortes inteligentes]** , siga um destes procedimentos:

   * Ajuste o tamanho de visualização das imagens na página.

      À direita da lista suspensa nome do ponto de interrupção, arraste a barra de controle deslizante para a esquerda ou para a direita para alterar o tamanho da exibição da imagem visível.

      ![edit_smart_measures-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtre a lista de imagens visíveis com base nos nomes dos pontos de interrupção. No exemplo abaixo, as imagens são filtradas no nome do ponto de interrupção &quot;Médio&quot;.

      Próximo ao canto superior direito da página, na lista suspensa, selecione um nome de ponto de interrupção para filtrar quais imagens você vê. (Veja a imagem acima.)

      ![edit_smart_measures-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Redimensione a caixa de recorte inteligente. Siga um destes procedimentos:

      * Se a imagem tiver um recorte inteligente ou apenas uma amostra inteligente, arraste a alça do canto da caixa de recorte na imagem. Ajuste o tamanho da área visível da cultura.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a alça do canto da caixa de recorte na imagem. Ajuste o tamanho da área visível da cultura. Ou selecione a amostra inteligente abaixo da imagem (as amostras de cores são estáticas), em seguida, arraste a alça do canto da caixa de recorte. Ajuste o tamanho da área visível da amostra.

      ![Redimensionamento do recorte inteligente de uma imagem](assets/edit_smart_crops-resize.png).

   * Mova a caixa de recorte inteligente. Siga um destes procedimentos:

      * Se a imagem tiver um recorte inteligente ou apenas uma amostra inteligente, arraste a caixa de recorte para um novo local.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a caixa de recorte inteligente para um novo local. Ou selecione a amostra inteligente abaixo da imagem (as amostras de cores são estáticas), em seguida, arraste a caixa de recorte da amostra inteligente para um novo local.

      ![edit_smart_measures-move](assets/edit_smart_crops-move.png)

   * Desfaça todas as suas edições e restaure o recorte inteligente original ou a amostra inteligente (aplica-se somente à sessão de edição atual).

      Selecionar **[!UICONTROL Reverter]** acima da imagem.

      ![edit_smart_measures-revert](assets/edit_smart_crops-revert.png)



1. Ao lado do canto superior direito da página, selecione **[!UICONTROL Salvar]**, em seguida selecione **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Remover um perfil de imagem das pastas {#removing-an-image-profile-from-folders}

Ao remover um Perfil de imagem de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta pai. No entanto, o processamento de arquivos que ocorreu dentro das pastas permanece intacto.

Você pode remover um Perfil de imagem de uma pasta de dentro do **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**.

### Remover perfis de imagem do Dynamic Media das pastas por meio da interface do usuário de Perfis {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja remover de uma pasta ou de várias pastas.
1. Selecionar **[!UICONTROL Remover perfil de processamento das pastas]** e selecione a pasta ou várias pastas que deseja usar para remover o perfil e selecione **[!UICONTROL Remover]**.

   Você pode confirmar que o Perfil de imagem não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remover perfis de imagem do Dynamic Media das pastas por meio de Propriedades {#removing-image-profiles-from-folders-via-properties}

1. Selecione o logotipo do Experience Manager e navegue **[!UICONTROL Ativos]** e, em seguida, na pasta da qual você deseja remover um Perfil de imagem.
1. Na pasta , selecione a marca de seleção para selecioná-la e, em seguida, selecione **[!UICONTROL Propriedades]**.
1. Selecione o **[!UICONTROL Perfis de imagem]** guia .
1. No **[!UICONTROL Nome do perfil]** , selecione **[!UICONTROL Nenhum]**, em seguida selecione **[!UICONTROL Salvar e fechar]**.

   As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.
