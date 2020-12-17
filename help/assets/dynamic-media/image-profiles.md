---
title: Perfis de imagem do Dynamic Media
description: Crie Perfis de imagem Dynamic Media que contenham configurações para máscara de nitidez e recorte inteligente, ou amostra inteligente, ou ambos, e aplique o perfil a uma pasta de ativos de imagem.
translation-type: tm+mt
source-git-commit: 59c532d8893f6dc6b94d7ec45a4af87ff1e37fff
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 11%

---


# Perfis de imagem do Dynamic Media {#image-profiles}

Ao fazer upload de imagens, você pode cortar automaticamente a imagem ao fazer upload aplicando um Perfil de imagem à pasta.

>[!IMPORTANT]
>
>Perfis de imagem não se aplicam a arquivos PDF, GIF animado ou INDD (Adobe InDesign).

## Opções de corte {#crop-options}

<!-- CQDOC-16069 for the paragraph directly below -->

As coordenadas de Recorte inteligente dependem da proporção. Ou seja, para as várias configurações de recorte inteligente em um Perfil de imagem, se a proporção for a mesma para as dimensões adicionadas no Perfil de imagem, a mesma proporção será enviada para a Dynamic Media. Por isso, o Adobe recomenda que você use a mesma área de corte. Isso garantirá que não haja impacto em diferentes dimensões usadas no Perfil de imagem.

Esteja ciente de que cada geração de Recorte inteligente criada requer processamento extra. Por exemplo, adicionar mais de cinco proporções de Recorte inteligente pode resultar em uma taxa lenta de ingestão de ativos. Ele também pode causar um aumento da carga nos sistemas. Como você pode aplicar o Smart Crop no nível da pasta, o Adobe recomenda usá-lo nas pastas *only* onde for necessário.

Você tem duas opções de recorte de imagem nas quais pode escolher. Você também tem uma opção para automatizar a criação de amostras de cores e imagens.

<table>
 <tbody>
  <tr>
   <td><strong>Opção</strong></td>
   <td><strong>Quando usar</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Cortar pixel</td>
   <td>Imagens de corte em massa com base apenas em dimensões.</td>
   <td><p>Para usar essa opção, selecione <strong>Pixel Crop</strong> na lista suspensa Opções de Recorte.</p> <p>Para cortar das laterais de uma imagem, insira o número de pixels a serem cortados de qualquer lado ou de cada lado da imagem. A quantidade de imagens cortadas depende da configuração ppi (pixels por polegada) no arquivo de imagem.</p> <p>Um recorte de pixel de Perfil de imagem é renderizado da seguinte maneira:<br /> </p>
    <ul>
     <li>Os valores são Superior, Inferior, Esquerda e Direita.</li>
     <li>A parte superior esquerda é considerada 0,0 e o corte de pixels é calculado a partir daí.</li>
     <li>Ponto de partida do corte: A esquerda é X e a parte superior é Y</li>
     <li>Cálculo horizontal: dimensão em pixels horizontais da imagem original menos Esquerda e depois menos Direita.</li>
     <li>Cálculo vertical: altura vertical do pixel menos Superior e depois menos Inferior.</li>
    </ul> <p>Por exemplo, suponha que você tenha uma imagem de 4000 x 3000 pixels. Você usa valores: Superior=250, Inferior=500, Esquerda=300, Direita=700.</p> <p>Do canto superior esquerdo (300.250) recorte usando o espaço de preenchimento de (4000-300-700, 3000-250-500 ou 3000.2250).</p> </td>
  </tr>
  <tr>
   <td>Corte inteligente</td>
   <td>Imagens de corte em massa com base em seu ponto focal visual.</td>
   <td><p>O Smart Crop usa o poder da inteligência artificial no Adobe Sensei para automatizar rapidamente o recorte de imagens em massa. O Smart Crop detecta e recorta automaticamente o ponto focal em qualquer imagem para capturar o ponto de interesse pretendido, independentemente do tamanho da tela.</p> <p>Para usar o Recorte inteligente, selecione <strong>Recorte inteligente</strong> na lista suspensa Opções de recorte, em seguida, à direita de Recorte de imagem responsiva, ative (ative) o recurso.</p> <p>Os tamanhos padrão de pontos de interrupção Grandes, Médios e Pequenos geralmente abrangem a gama completa de tamanhos que a maioria das imagens são usadas em dispositivos móveis e tablets, desktops e banners. Se desejar, edite os nomes padrão de Grande, Médio e Pequeno.</p> <p>Para adicionar mais pontos de interrupção, clique em <strong>Adicionar Recorte</strong>; para excluir um corte, clique no ícone Garbage Can.</p> </td>
  </tr>
  <tr>
   <td>Amostra de cor e imagem</td>
   <td>Gerar uma amostra de imagem em massa para cada imagem.</td>
   <td><p><strong>Observação</strong>: A Smart Swatch não é compatível com o Dynamic Media Classic.</p> <p>Localize e gere automaticamente amostras de alta qualidade a partir de imagens de produtos que mostram cor ou textura.</p> <p>Para usar a Amostra de cores e imagens, selecione <strong>Recorte inteligente</strong> na lista suspensa Opções de recorte, em seguida, à direita de Amostra de cores e imagens, ative (ative) o recurso. Insira um valor de pixel nas caixas de texto Largura e Altura.</p> <p>Enquanto todos os recortes de imagem estão disponíveis no painel Representações, as amostras são usadas somente por meio do recurso Copiar URL. Observe que você deve usar seu próprio componente de visualização para renderizar a amostra em seu site. (A exceção a isso são banners de carrossel. A Dynamic Media fornece o componente de visualização para a amostra usada em banners de carrossel.)</p> <p><strong>Uso de amostras de imagem</strong></p> <p>O URL para amostras de imagem é direto. Ou seja:</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>em que <code>:Swatch</code> é anexado à solicitação de ativo.</p> <p><strong>Uso de amostras de cores</strong></p> <p>Para usar amostras de cores, faça uma solicitação <code>req=userdata</code> com o seguinte:</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>Por exemplo, este é um ativo de amostra no Dynamic Media Classic:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>e este é o URL <code>req=userdata</code> correspondente do ativo de amostra:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p>A resposta <code>req=userdata</code> é a seguinte:</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>Você também pode solicitar uma resposta <code>req=userdata</code> no formato XML ou JSON, como nos seguintes exemplos de URL:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## Tirar nitidez da máscara {#unsharp-mask}

Use a **[!UICONTROL Tirar nitidez da máscara]** para ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. Controle a intensidade do efeito, o raio do efeito (medido em pixels) e um limite de contraste que será ignorado. Esse efeito usa as mesmas opções do filtro &quot;Tirar nitidez da máscara&quot; do Adobe Photoshop.

>[!NOTE]
>
>A máscara de nitidez só é aplicada a representações em baixa dentro do PTIFF (tiff de pirâmide) com resolução reduzida superior a 50%. Isso significa que as renderizações de maior tamanho dentro do ptiff não são afetadas por máscara de nitidez, enquanto representações de menor tamanho, como miniaturas, são alteradas (e mostrarão a máscara de nitidez).

Em **[!UICONTROL Máscara de nitidez]**, você tem as seguintes opções de filtragem:

<table>
 <tbody>
  <tr>
   <td><strong>Opção</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Quantidade</td>
   <td>Controla a quantidade de contraste aplicada aos pixels da borda. O padrão é 1,75. Para imagens de alta resolução, é possível aumentar para até 5. Pense em Amount como uma medida da intensidade do filtro. O intervalo é de 0 a 5.</td>
  </tr>
  <tr>
   <td>Raio</td>
   <td>Determina o número de pixels em torno dos pixels de borda que afetam a nitidez. Para imagens de alta resolução, insira de 1 a 2. Um valor baixo aplica nitidez apenas aos pixels de borda; um valor alto aplica nitidez a uma faixa mais ampla de pixels. O valor correto depende da imagem. O valor padrão é 0,2. O intervalo é de 0 a 250.</td>
  </tr>
  <tr>
   <td>Limite</td>
   <td><p>Determina o intervalo de contraste a ser ignorado quando o filtro de máscara de nitidez é aplicado. Em outras palavras, essa opção determina o quão diferentes os pixels com nitidez devem ser da área ao redor antes que sejam considerados pixels de borda e sejam apontados. Para evitar a introdução de ruído, experimente valores entre 0 e 255.</p> </td>
  </tr>
 </tbody>
</table>

O ajuste de nitidez está descrito em [Imagens de Nitidez.](/help/assets/dynamic-media/assets/sharpening_images.pdf)

## Criando Perfis de Imagem Dynamic Media {#creating-image-profiles}

Para definir parâmetros de processamento avançados para outros tipos de ativos, consulte [Configurando o Processamento de Ativos](config-dm.md#configuring-asset-processing).

Consulte [Sobre Perfis de imagem Dynamic Media e Perfis de vídeo](/help/assets/dynamic-media/about-image-video-profiles.md).

Consulte também [Práticas recomendadas para organizar seus ativos digitais para usar Perfis de processamento](/help/assets/dynamic-media/best-practices-for-file-management.md).

**Para criar Perfis de imagem Dynamic Media**

1. Toque no logotipo AEM e navegue até **[!UICONTROL Ferramentas > Ativos > Perfis de imagem]**.
1. Toque em **[!UICONTROL Criar]** para adicionar um novo Perfil de Imagem.
1. Insira um nome de perfil e valores para máscara de nitidez, recorte ou amostra, ou ambos.

   Você pode achar útil usar um nome de perfil que seja específico para a finalidade pretendida. Por exemplo, se você deseja criar um perfil que gera apenas amostras, ou seja, o Smart Crop está desativado (desativado) e o Color e Image Swatch está ativado (ativado), você pode usar o nome do perfil &quot;Smart Swatches&quot;.

   Consulte também [Opções de recorte inteligente e amostra inteligente](#crop-options) e [Tirar nitidez da máscara](#unsharp-mask).

   ![cortar](assets/crop.png)

1. Toque em **[!UICONTROL Salvar]**. O perfil recém-criado é exibido na lista dos perfis disponíveis.

## Edição ou exclusão de Perfis de imagem Dynamic Media {#editing-or-deleting-image-profiles}

1. Toque no logotipo AEM e navegue até **[!UICONTROL Ferramentas > Ativos > Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja editar ou remover. Para editá-lo, selecione **[!UICONTROL Editar Perfil de processamento de imagem]**. Para removê-lo, selecione **[!UICONTROL Excluir Perfil de processamento de imagem]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Se estiver editando, salve as alterações. Se estiver excluindo, confirme que deseja remover o perfil.

## Aplicar um Perfil de imagem Dynamic Media a pastas {#applying-an-image-profile-to-folders}

Quando você atribui um Perfil de imagem a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta pai. Isso significa que você pode atribuir apenas um Perfil de imagem a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você carrega, armazena, usa e arquiva ativos.

Se você atribuiu um Perfil de imagem diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos adicionados posteriormente à pasta.

As pastas que têm um perfil atribuído a ele são indicadas na interface do usuário pelo nome do perfil que aparece no cartão.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Você pode aplicar Perfis de imagem a pastas específicas ou globalmente a todos os ativos.

Você pode reprocessar ativos em uma pasta que já tenha um Perfil de imagem existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Aplicar Perfis de imagem Dynamic Media a pastas específicas {#applying-image-profiles-to-specific-folders}

Você pode aplicar um Perfil de imagem a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar Perfis de imagem a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Aplicação de Perfis de imagem Dynamic Media a pastas da interface de usuário de Perfis {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Toque no logotipo AEM e navegue até **[!UICONTROL Ferramentas > Ativos > Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja aplicar a uma pasta ou várias pastas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Toque em **[!UICONTROL Aplicar Perfil de processamento à(s) pasta(s)]** e selecione a pasta ou várias pastas que deseja usar para receber os ativos carregados recentemente e toque/clique em **[!UICONTROL Aplicar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

#### Aplicar Perfis de imagem Dynamic Media a pastas a partir de Propriedades {#applying-image-profiles-to-folders-from-properties}

1. Toque no logotipo AEM e navegue até **[!UICONTROL Assets]** e, em seguida, para a pasta à qual deseja aplicar um Perfil de imagem.
1. Na pasta, toque na marca de seleção para selecioná-la e, em seguida, toque em **[!UICONTROL Propriedades]**.
1. Toque na guia **[!UICONTROL Perfis de imagem]**. Na lista suspensa **[!UICONTROL Nome do perfil]**, selecione o perfil e toque em **[!UICONTROL Salvar e fechar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicar um Perfil de imagem Dynamic Media globalmente {#applying-an-image-profile-globally}

Além de aplicar um perfil a uma pasta, também é possível aplicar um globalmente para que qualquer conteúdo carregado AEM ativos em qualquer pasta tenha o perfil selecionado aplicado.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Para aplicar um Perfil de imagem Dynamic Media globalmente**:

1. Faça uma das seguintes opções:

   * Navegue até `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` e aplique o perfil apropriado e toque **[!UICONTROL Salvar]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navegue até CRXDE Lite até o seguinte nó: `/content/dam/jcr:content`.

      Adicione a propriedade `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` e toque em **[!UICONTROL Salvar tudo]**.

      ![configure_image_perfis](assets/configure_image_profiles.png)

## Editar o recorte inteligente ou a amostra inteligente de uma única imagem {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

Você pode realinhar ou redimensionar manualmente a janela de recorte inteligente de uma imagem para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em qualquer lugar em que você usa o recorte para as imagens específicas.

Você pode executar novamente o recorte inteligente para gerar as colheitas adicionais novamente, se necessário.

Consulte também [Editar o recorte inteligente ou a amostra inteligente de várias imagens](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar o recorte inteligente ou a amostra inteligente de uma única imagem**

1. Toque no logotipo AEM e navegue até **[!UICONTROL Assets]**, em seguida, até a pasta que tem um Perfil inteligente de imagens de corte ou amostra inteligente aplicado.

1. Toque na pasta para abrir seu conteúdo.
1. Toque na imagem cujo recorte inteligente ou amostra inteligente você deseja ajustar.
1. Na barra de ferramentas, toque em **[!UICONTROL Recorte inteligente]**.

1. Siga um destes procedimentos:

   * Próximo ao canto superior direito da página, arraste a barra deslizante para a esquerda ou direita para aumentar ou diminuir a exibição da imagem, respectivamente.
   * Na imagem, arraste uma alça de canto para ajustar o tamanho da área visível do corte ou da amostra.
   * Na imagem, arraste a caixa/amostra até um novo local. Você só pode editar amostras de imagem; as amostras de cores são estáticas.
   * Acima da imagem, toque em **[!UICONTROL Reverter]** para desfazer todas as suas edições e restaurar o recorte ou a amostra original.
   * Use as teclas de seta do teclado para cortar o tamanho do quadro, reposicionar a imagem ou ambas.

1. Perto do canto superior direito da página, toque em **[!UICONTROL Salvar]** e, em seguida, toque em **[!UICONTROL Fechar]** para voltar à pasta de ativos.

## Editar o recorte inteligente ou a amostra inteligente de várias imagens {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

Depois de aplicar um Perfil de imagem, contendo o Recorte inteligente, a uma pasta, todas as imagens dessa pasta terão um recorte aplicado a elas. Se desejar, você pode *manualmente* realinhar ou redimensionar a janela de recorte inteligente em várias imagens para refinar ainda mais seu ponto focal.

Depois de editar um recorte inteligente e salvar, a alteração é propagada em qualquer lugar em que você usa o recorte para as imagens específicas.

Você pode executar novamente o recorte inteligente para gerar as colheitas adicionais novamente, se necessário.

**Para editar o recorte inteligente ou a amostra inteligente de várias imagens**

1. Toque no logotipo AEM e navegue até **[!UICONTROL Assets]**, em seguida, para uma pasta que tenha um recorte inteligente ou um Perfil de imagem de amostra inteligente aplicado a ele.
1. Na pasta, toque no ícone **[!UICONTROL Mais ações]** (...) e, em seguida, toque em **[!UICONTROL Recorte inteligente]**.

1. Na página **[!UICONTROL Editar recortes inteligentes]**, execute um dos procedimentos a seguir:

   * Ajuste o tamanho de exibição das imagens na página.

      À direita da lista suspensa do nome do ponto de interrupção, arraste a barra deslizante para a esquerda ou direita para alterar o tamanho da exibição da imagem visível.

      ![edit_smart_ches-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtre a lista de imagens visualizáveis com base em nomes de pontos de interrupção. No exemplo abaixo, as imagens são filtradas no nome do ponto de interrupção &quot;Médio&quot;.

      Próximo ao canto superior direito da página, na lista suspensa, selecione um nome de ponto de interrupção para filtrar as imagens que você vê. (Consulte a imagem acima.)

      ![edit_smart_lines-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Redimensione a caixa de corte inteligente. Execute um dos procedimentos a seguir:

      * Se a imagem tiver apenas um recorte inteligente ou uma amostra inteligente, arraste na imagem a alça do canto da caixa de recorte para ajustar o tamanho da área visível do recorte.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a alça do canto da caixa de recorte para ajustar o tamanho da área visível do recorte. Ou, toque ou clique na amostra inteligente abaixo da imagem (as amostras de cores são estáticas), em seguida, arraste a alça do canto da caixa de corte para ajustar o tamanho da área visível da amostra.

      ![Redimensionamento do recorte inteligente de uma imagem.](assets/edit_smart_crops-resize.png)

   * Mova a caixa de recorte inteligente. Execute um dos procedimentos a seguir:

      * Se a imagem tiver apenas um recorte inteligente ou uma amostra inteligente, arraste a caixa de recorte para um novo local.
      * Se a imagem tiver um recorte inteligente e uma amostra inteligente, arraste a caixa de recorte inteligente para um novo local. Ou, toque ou clique na amostra inteligente abaixo da imagem (as amostras de cores são estáticas) e arraste a caixa de recorte de amostra inteligente para um novo local.

      ![edit_smart_ches-move](assets/edit_smart_crops-move.png)

   * Desfaça todas as edições e restaure o recorte inteligente ou a amostra inteligente original (aplica-se somente à sessão de edição atual).

      Toque em **[!UICONTROL Reverter]** acima da imagem.

      ![edit_smart_lines-revert](assets/edit_smart_crops-revert.png)



1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Salvar]**. em seguida, toque em **[!UICONTROL Fechar]** para retornar à pasta de ativos.

## Removendo um Perfil de imagem das pastas {#removing-an-image-profile-from-folders}

Quando você remove um Perfil de imagem de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta pai. No entanto, qualquer processamento de arquivos que tenha ocorrido dentro das pastas permanece intacto.

Você pode remover um Perfil de imagem de uma pasta do menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, de **[!UICONTROL Propriedades]**. Esta seção descreve como remover Perfis de imagem de pastas de ambas as maneiras.

### Remoção de Perfis de imagem Dynamic Media de pastas por meio da interface de usuário de Perfis {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Toque no logotipo AEM e navegue até **[!UICONTROL Ferramentas > Ativos > Perfis de imagem]**.
1. Selecione o Perfil de imagem que deseja remover de uma pasta ou de várias pastas.
1. Toque em **[!UICONTROL Remover perfil de processamento das pastas]** e selecione uma ou várias pastas que deseja usar para remover o perfil e toque em **[!UICONTROL Remover]**.

   Você pode confirmar que o Perfil de imagem não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

### Remoção de Perfis de imagem Dynamic Media de pastas por meio de Propriedades {#removing-image-profiles-from-folders-via-properties}

1. Toque no logotipo AEM e navegue **[!UICONTROL Assets]** até a pasta da qual você deseja remover um Perfil de imagem.
1. Na pasta, toque na marca de seleção para selecioná-la e, em seguida, toque em **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Perfis de imagem]**.
1. Na lista suspensa **[!UICONTROL Nome do Perfil]**, selecione **[!UICONTROL Nenhum]** e, em seguida, toque em **[!UICONTROL Salvar e fechar]**.

   As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.
