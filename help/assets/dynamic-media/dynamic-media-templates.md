---
title: Como gerenciar  [!DNL Dynamic Media] modelos?
description: Saiba como criar  [!DNL Dynamic Media]  modelos usando um editor de modelo do WYSIWYG e incluir várias camadas de imagens, textos e formas para criar banners e folhetos rapidamente e usá-los em aplicativos downstream.
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: 97be1d044ae23859e263756116c8bac8701178b4
workflow-type: tm+mt
source-wordcount: '3779'
ht-degree: 0%

---


# [!DNL Dynamic Media] modelos{#dynamic-media-templates}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Práticas recomendadas de pesquisa</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas para metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de conteúdo</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos da OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentação do AEM Assets para desenvolvedores</b></a>
        </td>
    </tr>
</table>

Crie modelos personalizáveis em tempo real para seus banners e folhetos usando os modelos do [!DNL Dynamic Media], um editor de modelos do WYSIWYG. Publique seu modelo [!DNL Dynamic Media] e use-o nos aplicativos downstream. Um modelo [!DNL Dynamic Media] inclui camadas de imagem e texto. Adicione parâmetros às camadas de imagem e texto do modelo e use [[!DNL Dynamic Media] URLs](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media) para reposicionar e redimensionar a camada e atualizar seu conteúdo em tempo real.

Alguns dos principais recursos incluem:

* **[!DNL Dynamic Media]Editor de modelos do WYSIWYG:** Crie banners personalizáveis com camadas de imagem e texto.
* **Parametrização de Camada:** Defina pares de valores-chave dinâmicos para camadas para habilitar atualizações em tempo real.
* Suporte a URL **[!DNL Dynamic Media]:** Use URLs [!DNL Dynamic Media] para modelos, integrando valores personalizados de aplicativos próprios ou de terceiros.
* **Controle de Visibilidade de Camada** oculta ou mostra camadas dinamicamente, conforme necessário.
* **Redimensionamento de Texto Inteligente:** Ajuste automaticamente o tamanho do texto para ajustar às áreas designadas.

Alguns dos principais benefícios dos modelos [!DNL Dynamic Media] incluem:

* **Otimizar 1:1 Personalization:** Personalize o conteúdo para sinais de clientes em tempo real.
* **Reduza o esforço manual:** automatize e acelere a criação e o gerenciamento de conteúdo.
* **Garanta Experiências omnicanais Consistentes:** Mantenha a consistência da marca em todos os canais.
* **Reutilizar conteúdo efetivamente:** Evite conteúdo de uso único e dimensione com modelos dinâmicos e parametrizados.
* **Atenuar Riscos** Atualize preços, descontos e links em tempo real.
* **Aprimorar o Engajamento com o Cliente**. Promover experiências interativas e relevantes contextualmente.

>[!NOTE]
>
>Os clientes com assinaturas do SKU de Segurança Aprimorada não podem usar nenhum recurso do [!DNL Dynamic Media], incluindo Modelos do [!DNL Dynamic Media], nesse programa dos Serviços em Nuvem.

Saiba como criar um modelo [!DNL Dynamic Media] passo a passo neste vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## Antes de começar{#prerequisites-for-dynamic-media-wysiwyg-template}

Atenda aos seguintes requisitos para criar um modelo [!DNL Dynamic Media] e gerar sua URL de entrega:

1. Acesso a [!DNL Dynamic Media].
1. Na página inicial do [!DNL Assets View], você tem uma pasta no **[!UICONTROL Dynamic Media Assets]** para salvar seu modelo. [Crie uma pasta](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) no ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets ]**para replicar essa pasta no**[!UICONTROL  Dynamic Media Assets ]**.
1. [Sincronize as imagens disponíveis na sua [!DNL AEM Assets] instância com [!DNL Dynamic Media] para usá-las para criar o modelo](/help/assets/dynamic-media/config-dm.md).
1. Publique as imagens que serão usadas na criação do modelo para gerar o URL de entrega do modelo após criá-lo. O URL do delivery pode ser usado em aplicativos downstream.
1. Para usar uma fonte diferente da fonte padrão [!UICONTROL Adobe Sans F2] na camada de texto do modelo, [carregue e publique o arquivo de fonte no AEM e no Dynamic Media simultaneamente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation). [Os formatos de arquivo de fonte com suporte são: AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Além disso, certifique-se de [reprocessar](/help/assets/reprocessing-assets-view.md) as fontes existentes para usá-las. Consulte [Fontes](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/support-files/fonts) para obter mais informações.<!--(On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**)-->
1. verifique o seguinte na interface para toque:
   * Na página **[!UICONTROL Editar Configuração [!DNL Dynamic Media]]**, o modo de sincronização **[!UICONTROL [!DNL Dynamic Media]]**, definido como **[!UICONTROL Desabilitado por padrão]**, não é aplicado a todas as pastas do AEM (**[!UICONTROL Sincronizar todo o conteúdo]** está desmarcado). Consulte [configurando o Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md) para obter mais informações.
   * O modo de sincronização **[!UICONTROL [!DNL Dynamic Media]]** está definido como **[!UICONTROL Habilitar para subpastas]** para a pasta ou subpasta de destino onde você salvará o modelo após a criação. Consulte [configurando [!DNL Dynamic Media] Cloud Service](/help/assets/dynamic-media/config-dm.md) para obter mais informações.

## Criar modelo [!DNL Dynamic Media]{#how-to-create-dynamic-media-template}

Execute as seguintes etapas para criar um modelo [!DNL Dynamic Media]:

<!--
1. Navigate to your [!DNL Assets View] and [create a folder](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**. The folder tree in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** replicates in **[!UICONTROL Dynamic Media Assets]**. Save your [!DNL Dynamic Media] template in this [!UICONTROL Dynamic Media Assets] folder.
1. Select ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** and [upload and publish your images to [!DNL AEM] and [!DNL Dynamic Media] simultaneously](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm#dynamic-media-publish-mode-set-to-upon-activation) to use them in creating the template. Publishing images is required to generate the template's delivery URL, after creating the template. The delivery URL can be used in downstream applications.
1. [Execute these asset uploading and publishing steps](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation) to upload and publish a font file to AEM and Dynamic Media simultaneously to use it in creating the template. [!UICONTROL Adobe Sans F2] is the only default font available in the text layer. [The supported font file formats are, AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Ensure to [reprocess](/help/assets/reprocessing-assets-view.md) the existing fonts to use them in creating the template (On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**). See [Fonts](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/support-files/fonts) to know more about fonts.
-->

1. [Criar uma tela em branco](#create-a-canvas)
1. [Adicionar imagens à tela](#add-images-to-the-canvas)
1. [Adição de camadas de texto à tela de desenho](#add-text-to-the-canvas)
1. [Adicionar formas à tela de desenho](#add-shapes-to-the-canvas)
1. [Editar ou excluir uma camada](#edit-or-delete-a-layer)
1. [Camadas de parâmetros](#parameterise-a-layer)

### Criar uma tela em branco{#create-a-canvas}

Execute estas etapas para criar uma tela em branco:

1. Navegue até [!DNL Assets View], selecione **[!UICONTROL Dynamic Media Assets]**, disponível no painel esquerdo, e navegue até a pasta para salvar o modelo nessa pasta.

   ![Modelos do Dynamic Media](/help/assets/assets/DM-Assets1.png)

1. Selecione **[!UICONTROL Criar Modelo]**. A caixa de diálogo **[!UICONTROL Novo Modelo]** é exibida.

   ![como criar modelos dinâmicos que podem ser personalizados em tempo real](/help/assets/assets/new-template.png)

   >[!NOTE]
   >
   >  O modelo é salvo no local onde foi criado. Na página inicial do [!DNL Assets View], selecione **[!UICONTROL Dynamic Media Assets]** e clique em **[!UICONTROL Criar Modelo]** para salvar o modelo na pasta raiz do **[!UICONTROL Dynamic Media Assets]**.

1. Especifique um nome de modelo, defina a largura e a altura da tela e clique em **[!UICONTROL Criar]**. Uma tela de desenho em branco é exibida com opções de menu em ambos os lados para ser usada na criação do modelo. Passe o mouse sobre as opções de menu para ver a dica de ferramenta.
   ![modelo personalizável em tempo real](/help/assets/assets/blank-canvas-page.png)

   >[!NOTE]
   >
   > A faixa de largura e altura permitida é de 50 a 5000.

**Opções de menu no painel direito:** Use essas opções para adicionar as imagens e camadas de texto necessárias à tela.

* ![Modelos DM](/help/assets/assets/add-image.svg): clique para adicionar imagens à tela.
* ![modelos personalizáveis](/help/assets/assets/add-text.svg): clique para adicionar textos à tela.
* ![modelos personalizáveis](/help/assets/assets/show-layers-list.svg): clique para ver a lista de todas as camadas (imagem e texto) na tela. Cada imagem e texto adicionados à tela de desenho é representado como uma camada separada.

**Opções de menu no painel esquerdo:** Use essas opções para as seguintes ações comuns do editor.

* ![Modelos DM](/help/assets/assets/layer-selector.svg): selecione ![Modelos DM](/help/assets/assets/layer-selector.svg) e clique em uma camada na tela para selecioná-la.
* ![modelos com suporte para personalização](/help/assets/assets/bring-forward.svg): clique em ![modelos com suporte para personalização](/help/assets/assets/bring-forward.svg) ou use o atalho de teclado, **Ctrl** + **`]`** (Windows) ou **Cmd** + **`]`** (Mac) para avançar uma camada selecionada.
* ![como criar um modelo que possa ser personalizado facilmente](/help/assets/assets/send-backward.svg): clique em ![como criar um modelo que possa ser personalizado facilmente](/help/assets/assets/send-backward.svg) ou use o atalho de teclado, **Ctrl** + **`[`** (Windows) ou **Cmd** + **`[`** (Mac) para voltar uma camada selecionada.
* ![crie um modelo que possa ser personalizado instantaneamente](/help/assets/assets/undo.svg): clique em ![criar um modelo que possa ser personalizado instantaneamente](/help/assets/assets/undo.svg) ou use o atalho de teclado, **Ctrl** + **Z** (Windows) ou **Cmd** + **Z** (Mac) para desfazer a última ação.
* ![modelo para criar banners rapidamente](/help/assets/assets/redo.svg): clique em ![modelo para criar banners rapidamente](/help/assets/assets/redo.svg) ou use o atalho de teclado, **Ctrl** + **Y** (Windows) ou **Cmd** + **Y** (Mac) para refazer a última ação.
* ![modelo para criar panfletos rapidamente](/help/assets/assets/zoom-in.svg): clique em ![modelo para criar panfletos rapidamente](/help/assets/assets/zoom-in.svg) ou use o atalho de teclado, **Ctrl** + **+** (Windows) ou **Cmd** + **+** (Mac) para ampliar a tela.
* ![modelo para criar banners rapidamente](/help/assets/assets/Zoom-out.svg): clique ![modelo para criar banners rapidamente](/help/assets/assets/Zoom-out.svg) ou use o atalho de teclado, **Ctrl** + **-** (Windows) ou **Cmd** + **-** (Mac) para reduzir a tela.
* Pressione **backspace** ou **delete** para excluir a camada selecionada se nenhum texto ou propriedade estiver sendo editado.

Clique em ![modelo para criar panfletos rapidamente](/help/assets/assets/show-layers-list.svg) e selecione mais opções (![](/help/assets/assets/three-dots.svg)) na camada Tela de Pintura para editar as dimensões da tela de desenho a qualquer momento durante a criação do modelo.
![](/help/assets/assets/edit-canvas1.png)

>[!NOTE]
>
> Os modelos permitem no máximo 20 camadas, incluindo a Tela de Pintura.

### Adicionar imagens à tela{#add-images-to-the-canvas}

Execute estas etapas para adicionar imagens à tela:

1. Clique em ![criar um banner rapidamente](/help/assets/assets/add-image.svg) para abrir o painel [Seletor de ativos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector). O painel exibe as imagens na sua instância do AEM Assets que são sincronizadas com o [!DNL Dynamic Media].
1. Navegue pelo painel ou use palavras-chave na barra de pesquisa para localizar uma imagem específica.
1. Arraste e solte uma imagem na tela para usá-la. Consulte o [**[!UICONTROL Painel Propriedades]**](#reposition-resize-delete-a-layer) para redimensionar ou reposicionar uma camada na tela de desenho.
   ![criar um banner em segundos](/help/assets/assets/add-image-to-canvas.png)
1. Habilite o botão de alternância **[!UICONTROL Raio Uniforme]** e use o controle deslizante **[!UICONTROL Raio do Canto]** para ajustar o arredondamento de todos os quatro cantos de uma imagem uniformemente. Desative o botão de alternância para personalizar o arredondamento do canto, atribuindo valores de raio específicos a cada canto.
   ![ajustar o arredondamento do canto da imagem](/help/assets/assets/enable-uniform-radius-image.png)

### Adição de camadas de texto à tela de desenho{#add-text-to-the-canvas}

Execute estas etapas para adicionar camadas de texto à tela de desenho:

1. Clique ![criando novos banners rapidamente](/help/assets/assets/add-text.svg) para adicionar uma camada de texto à tela e abrir o painel Propriedades.
1. Selecione a camada e clique no texto para atualizá-la.
1. Selecione **[!UICONTROL Redimensionamento do Texto Inteligente]** no painel Propriedades para ajustar automaticamente o comprimento do texto e o tamanho da fonte para que se ajustem de forma ideal à área designada.
   ![melhores banners personalizáveis](/help/assets/assets/add-text-layer.png)

Consulte o [**[!UICONTROL Painel Propriedades]**](#reposition-resize-delete-a-layer) para reposicionar, redimensionar, girar ou excluir a camada. Formate o texto para a fonte, o tamanho, a cor, o estilo e o alinhamento necessários (na camada) alterando os valores nos respectivos campos na seção **[!UICONTROL Texto]** do painel. O campo **[!UICONTROL Família da Fonte]** exibe a fonte padrão [!UICONTROL Adobe Sans F2], as fontes existentes reprocessadas e as fontes recém-carregadas e publicadas. Consulte o ponto 5 na seção [Antes de começar](#prerequisites-for-dynamic-media-wysiwyg-template) acima para obter mais informações.

[Aplique formatação a substrings para estilizar e controlar partes específicas do texto independentemente.](#apply-formatting-to-substring)

#### Formatar texto seletivo{#apply-formatting-to-substring}

Execute as seguintes etapas para formatar partes específicas de uma string:

1. Selecione um ou mais caracteres na cadeia de caracteres a ser formatada.
1. Aplicar formatação à seleção usando o [painel de propriedades](#properties-panel). As seguintes opções de formatação são aplicáveis a substrings e suas partes:
   * **Estilo da Fonte**: Negrito, itálico, sublinhado, subscrito e sobrescrito usando a opção **[!UICONTROL Estilo da Fonte]**.
   * **Propriedades da Fonte**: altere a família, a cor e o tamanho da fonte usando as respectivas opções de painel.
     ![formato-subcadeia](/help/assets/assets/format-substring.png)

[Cada parte da cadeia de caracteres formatada é exibida como uma subsequência no seletor de subsequências, disponível no painel de parâmetros. Adicione parâmetros a essas partes formatadas para formatá-las dinamicamente usando a URL de entrega do modelo ](#substring-parameterisation).

### Adicionar formas à tela de desenho {#add-shapes-to-the-canvas}

Execute estas etapas para adicionar formas à tela de desenho:

1. Clique em ![criando formas](/help/assets/assets/Shapes.svg), selecione uma forma (retângulo ou círculo) para adicioná-la à tela de desenho. Use o [[!UICONTROL Painel de Propriedades]](#reposition-resize-delete-a-layer) da forma para reposicionar, redimensionar, girar ou excluir a camada.
1. Role até a seção **[!UICONTROL Estilo]** do painel, defina um código hexadecimal no campo **[!UICONTROL Cor da Forma]** ou use o seletor de cores para preencher a cor na forma selecionada.
1. Habilite o botão de alternância **[!UICONTROL Raio Uniforme]** e use o controle deslizante **[!UICONTROL Raio do Canto]** para ajustar o arredondamento de todos os quatro cantos do retângulo uniformemente. Desative o botão de alternância para personalizar o arredondamento do canto, atribuindo valores de raio específicos a cada canto.
   ![ajustar o arredondamento de canto das formas](/help/assets/assets/enable-uniform-radius-shape.png)
1. [Adicione o parâmetro **[!UICONTROL Hide]** à camada selecionada](#parameterise-a-layer) para mostrar ou ocultar a camada no modelo em tempo real usando a URL do modelo.
1. Selecione a camada para [adicionar um link [!UICONTROL CTA]](#add-CTA-in-dynamic-media-templates) a ela, permitindo que os usuários cliquem na forma como um hiperlink no modelo ativo.

### Editar ou excluir uma camada {#edit-or-delete-a-layer}

Execute estas etapas para editar ou excluir uma camada da tela de desenho:

1. Clique em ![modelos com suporte a atualizações dinâmicas](/help/assets/assets/show-layers-list.svg) e selecione a camada na tela ou na lista Camadas.
1. Clique em **[!UICONTROL mais opções]** (![modelos com suporte a atualizações em tempo real](/help/assets/assets/three-dots.svg)) para editar ou excluir a camada.
1. Clique em **[!UICONTROL Excluir]** para excluir a camada.
1. Clique em **[!UICONTROL Editar]** para editar a camada usando o [**[!UICONTROL Painel de Propriedades]**](#reposition-resize-delete-a-layer).
   ![criação rápida de banner](/help/assets/assets/dm-templates/edit-delete-layer.png)

### Painel Propriedades{#properties-panel}

O painel [!UICONTROL Propriedades] inclui seções para [reposicionar](#reposition-resize-delete-a-layer), [redimensionar](#reposition-resize-delete-a-layer) e [girar](#reposition-resize-delete-a-layer) uma camada.  Também fornece opções de preenchimento de cores para [camadas de forma](#add-shapes-to-the-canvas), [opções de formatação de texto](#text-formatting-options-on-properties-panel) para [camadas de texto](#add-text-to-the-canvas) e uma opção para [adicionar um link [!UICONTROL CTA]](#add-CTA-in-dynamic-media-templates) a qualquer camada selecionada.
Para navegar até o painel de propriedades de uma camada, clique em ![criação rápida de conteúdo](/help/assets/assets/show-layers-list.svg) e selecione a camada na lista para exibir seu painel [!UICONTROL Propriedades].

![criação rápida de conteúdo](/help/assets/assets/properties-panel.png)

No painel [!UICONTROL Propriedades] de uma camada, selecione outra camada na tela para navegar até o painel [!UICONTROL Propriedades].

#### Reposicionar, redimensionar, girar ou excluir uma camada{#reposition-resize-delete-a-layer}

Veja estas ações comuns de edição de camadas para editar um texto ou uma camada de imagem:

* **Reposicionar a camada:** Arraste a camada para movê-la para qualquer lugar na tela. Essa ação atualiza os valores X e Y no painel de propriedades. X e Y são as coordenadas do centro da camada no plano da tela de desenho.
* **Redimensionar a camada:** Selecione a camada e arraste suas alças de borda para redimensioná-la. Essa ação atualiza os valores L (largura) e A (altura) no painel de propriedades.
* **Girar a camada:** arraste a alça quadrada colocada verticalmente acima da camada para girá-la em torno de seu centro. Essa ação atualiza os valores de ângulo no painel de propriedades.
* **Excluir a camada:** Pressione **Backspace** ou **delete** e clique em **[!UICONTROL Confirmar]** para excluir uma camada selecionada.

#### Opções de formatação de texto{#text-formatting-options-on-properties-panel}

Formate o texto para a fonte, o tamanho, a cor, o estilo e o alinhamento necessários (dentro da camada) alterando os valores nos respectivos campos na seção **[!UICONTROL Texto]** do painel.
Certifique-se de incluir **[!UICONTROL Redimensionamento de Texto Inteligente]**. O [!UICONTROL Redimensionamento de Texto Inteligente] funciona no algoritmo [Ajuste de Texto](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting) para preencher o texto de maneira ideal na área de texto, evitar o excesso de texto e minimizar o espaço extra na parte inferior do texto.

![criação rápida de conteúdo](/help/assets/assets/smart-text-resize.png)

### Camadas de parâmetros {#parameterise-a-layer}

Depois de criar um modelo com várias camadas de imagens, textos e formas, parametrize as camadas selecionadas. Quando uma camada ou sua propriedade é parametrizada, ela obtém um par de valores-chave (também chamado de parâmetro ). Esse parâmetro pode ser incluído no URL do modelo para atualizar a posição, o tamanho ou o conteúdo da camada em tempo real, resultando na personalização rápida do modelo.

Para parametrizar uma camada:

1. clique em ![criação de conteúdo instantâneo](/help/assets/assets/show-layers-list.svg), selecione uma camada e clique em **[!UICONTROL Parâmetros]**. O painel **[!UICONTROL Parâmetros]** é exibido.
1. Alternar **[!UICONTROL Incluir Parâmetro]** para parametrizar uma propriedade. Consulte a [opção de painel Parâmetros](#parameterisation-options-or-allowed-parameters) para saber o comportamento da propriedade após a parametrização.
1. **Opcional:** Renomeie o nome do parâmetro. Um nome de parâmetro tem um nome de camada seguido por um sufixo. Para uma camada selecionada, todas as suas propriedades parametrizadas compartilham o mesmo nome de camada seguido por um sufixo variável. Renomeie o nome da camada seguindo a convenção de nomenclatura semântica para que, ao incluir o parâmetro no URL, o próprio nome do parâmetro explique sobre o conteúdo da camada ou sua finalidade.
1. Clique em **[!UICONTROL Salvar]**.
   ![criação instantânea de conteúdo](/help/assets/assets/parameterise-a-layer.png)
Para alternar entre o painel Parâmetro de uma imagem e uma camada de texto, selecione a camada na tela e clique em **[!UICONTROL Parâmetros]**.

#### Opção do painel Parâmetros {#parameterisation-options-or-allowed-parameters}

As propriedades com parâmetros podem ser incluídas como parâmetros de URL no URL do modelo para editar o modelo em tempo real usando o URL.

##### Parâmetros de camada{#layer-parameters}

A seguir estão os parâmetros de camada que se aplicam às camadas de imagem e texto.

**[!UICONTROL X]:** Inclua para mover a camada horizontalmente ao longo de sua linha central, paralelamente ao eixo X do plano de modelo, alterando o valor do parâmetro na URL.
**[!UICONTROL Y]:** Inclua para mover a camada verticalmente ao longo de sua linha central, paralelamente ao eixo Y do plano de modelo, alterando o valor do parâmetro na URL.
**[!UICONTROL Largura]:** Inclua para ajustar a largura da camada alterando o valor do parâmetro na URL.
**[!UICONTROL Altura]:** Inclua para ajustar a altura da camada alterando o valor do parâmetro na URL.
**[!UICONTROL Ocultar]:** Incluir para ocultar ou mostrar a camada no modelo usando 0 (mostrar) e 1 (ocultar).

##### Parâmetro de imagem{#image-parameter}

Inclua o parâmetro **[!UICONTROL Source]** para substituir a imagem da camada por uma nova imagem alterando o caminho da imagem no valor do parâmetro na URL.
![parâmetro de origem da imagem](/help/assets/assets/image-parameter.png)

##### Parâmetros de formatação de texto{#text-formatting-parameters}

Inclua os seguintes parâmetros para editar o texto, sua fonte, cor e tamanho no URL de entrega atualizando os valores de parâmetro no URL:

**[!UICONTROL Texto]:** Incluir para atualizar o texto da URL.
**[!UICONTROL Família da Fonte]:** Incluir para atualizar a fonte do texto da URL.
**[!UICONTROL Tamanho da Fonte]:** Incluir para atualizar o tamanho da fonte do texto da URL.
**[!UICONTROL Cor do texto]:** Incluir para atualizar a cor da fonte do texto da URL.

##### Parametrizar substrings{#substring-parameterisation}

No painel **[!UICONTROL Parâmetros]**, role até a seção **[!UICONTROL Parâmetros da Substring]**. Esta seção inclui um **seletor de subsequência** que exibe a sequência completa (camada de texto selecionada) com formatação consistente ou suas partes formatadas como subsequências separadas. Selecione uma subcadeia de caracteres para [parametrizar seu texto, família de fontes, tamanho da fonte e cor](#text-formatting-parameters).
Use o seletor de subcadeia de caracteres para [dividir subcadeias de caracteres](#split-substring) para parametrizar suas partes individuais ou [mesclar subcadeias de caracteres](#merge-substring) para aplicar parâmetros uniformes.

###### Dividir subcadeia de caracteres{#split-substring}

Para parametrizar parte de uma substring, puxe-a para fora para transformá-la em uma substring separada para seleção e parametrização individuais.
Execute as seguintes etapas para dividir uma substring em substrings separadas:

1. No seletor de substring, selecione os caracteres em uma substring para separá-la.
1. Clique em ![dividir subsequência](/help/assets/assets/unmerge.svg) para extraí-la e torná-la uma subsequência separada dentro do **seletor de subsequência**.
   ![subcadeia de caracteres dividida](/help/assets/assets/split-a-substring.png)
Você pode selecionar a subcadeia necessária para [parametrizar seu texto, família de fontes, tamanho da fonte e cor](#text-formatting-parameters).

###### Mesclar subcadeia de caracteres{#merge-substring}

A mesclagem de substrings remove seus parâmetros individuais existentes e permite aplicar parâmetros consistentes na substring recém-formada.
Execute as seguintes etapas para mesclar duas substrings adjacentes para aplicar parâmetros uniformes à substring resultante:

1. No seletor de subsequência, selecione os caracteres em duas subsequências adjacentes com a mesma formatação.
1. Clique em ![mesclar subsequência](/help/assets/assets/merge.svg) para mesclar as subsequências.
   ![mesclar subcadeias idênticas](/help/assets/assets/merge-two-substrings.png)
Você pode aplicar parâmetros uniformes à substring recém-formada.
   >[!NOTE]
   >
   >Somente substrings com formatação idêntica podem ser mescladas.

### Agrupar camadas para controlar sua visibilidade simultaneamente{#group-layers}

Outra maneira de manter seus modelos flexíveis é usar um único nome de parâmetro para controlar várias camadas. Essa estratégia é útil para o parâmetro de visibilidade (ocultar ou mostrar camadas), para atualizar o design ou os gráficos de um único modelo.

Siga estas etapas para atribuir o mesmo nome aos [!UICONTROL Ocultar] parâmetros (![criação rápida de conteúdo](/help/assets/assets/Visibility-icon.svg)) de várias camadas, permitindo que você as oculte ou mostre simultaneamente.

1. Navegue até o [**[!UICONTROL Painel Propriedades]**](#parameterise-a-layer) de uma camada.
1. Alternar o parâmetro **[!UICONTROL Hide]** se não for parametrizado anteriormente.
1. **Opcional:** Renomeie o Parâmetro **[!UICONTROL Hide]**.
1. Copie o nome do parâmetro **[!UICONTROL Hide]**.
1. Vá para o painel Parâmetro de outras camadas selecionando-as na tela e alterne seu Parâmetro **[!UICONTROL Hide]** se não for parametrizado.
1. Substitua o nome **[!UICONTROL Hide parameter]** pelo nome copiado.
1. Clique em **[!UICONTROL Salvar]** para agrupar as camadas.
1. Execute a etapa 3 e depois a etapa 4 na seção [**[!UICONTROL Visualizar e Publicar]**](#preview-and-publish-template-and-copy-template-deliver-url) para ver suas alterações.

## Pré-visualizar e publicar o modelo para copiar o URL de entrega{#preview-and-publish-template-and-copy-template-deliver-url}

Execute estas etapas para visualizar e publicar o modelo e copiar o URL do delivery:

1. Na página da tela, clique em **[!UICONTROL Visualizar]**. Você também pode navegar para o **[!UICONTROL Modo de Exibição do Assets]** **>** **[!UICONTROL Dynamic Media Assets]** **>** localizar e selecionar seu modelo **>** clicar em **[!UICONTROL Editar Modelo]** **>** clicar em **[!UICONTROL Visualizar]**. A página de visualização exibe o modelo, seus parâmetros (camadas e propriedades com parâmetros), status de publicação e a opção **[!UICONTROL Publicar]**.
1. Selecione parâmetros do painel **[!UICONTROL Parâmetros do modelo]** para editar seus valores e atualizar instantaneamente o conteúdo, o tamanho, a posição ou a formatação de texto da camada de modelo correspondente na visualização. Por exemplo:
   1. Selecione uma camada de texto e edite seu texto ou
   1. Selecione uma camada de imagem, clique em ![criar conteúdo rapidamente](/help/assets/assets/add-image.svg), selecione uma imagem no seletor de ativos e clique em **[!UICONTROL Atualizar]**.

   O modelo é atualizado imediatamente, exibindo o texto editado e substituindo a imagem anterior pela nova. Além disso, o valor do parâmetro de imagem reflete o novo caminho de imagem. Da mesma forma, é possível redimensionar uma camada ajustando seus valores, e as alterações são aplicadas ao modelo em tempo real.
1. Selecione o parâmetro **[!UICONTROL Hide]** para [camadas agrupadas](#group-layers) da lista para exibi-las ou ocultá-las no modelo.
1. **Opcional:** Altere o valor do parâmetro **[!UICONTROL Ocultar]** entre 0 e 1 e clique em **[!UICONTROL Atualizar]** para ver as alterações. Camadas com o mesmo parâmetro **[!UICONTROL Hide]** oculta ou é exibido junto. Da mesma forma, é possível controlar a visibilidade das camadas a partir do URL.

   ![criando conteúdo em tempo real](/help/assets/assets/dm-templates-publish-status.png)
Você também pode alternar **[!UICONTROL Incluir todos os parâmetros]** para editar todos os valores de parâmetros exibidos e ver as atualizações na visualização do modelo.
   <br>
1. Para publicar o modelo a partir da página de visualização, clique em **[!UICONTROL Publicar]** e confirme para publicar. Uma mensagem **[!UICONTROL Publicação concluída]** é exibida e o status de publicação é atualizado para **[!UICONTROL Publicado]**.

### Copiar o URL de entrega

Os parâmetros selecionados na página **[!UICONTROL Visualização]** tornam-se os parâmetros de URL na URL de modelo.

Verifique se as imagens no modelo já estão publicadas no AEM e no Dynamic Media para gerar o URL de entrega do modelo.

Execute as seguintes etapas para copiar o URL de entrega do modelo:

1. Clique em **[!UICONTROL Copiar URL]**. A caixa de diálogo **[!UICONTROL Copiar URL]** é exibida. Selecione e copie o URL exibido. O primeiro parâmetro na URL começa após um ponto de interrogação **([!UICONTROL ?])** e um par chave-valor começam com **[!UICONTROL $]** e terminam com **[!UICONTROL &amp;]**. A chave e o valor são separados por um sinal de igual **([!UICONTROL =])**, com a chave à esquerda e o valor à direita.
1. Cole esse URL na guia do navegador e veja seu modelo em tempo real. Personalize o modelo em tempo real atualizando o valor do parâmetro necessário (valor da chave) diretamente na URL, conforme demonstrado na [etapa 2](#preview-and-publish-template-and-copy-template-deliver-url) da seção **Visualizar e Publicar**.
1. Use este URL para um merchandising rápido de seus produtos ou serviços. Você pode compartilhar esse URL com seus clientes ou integrá-lo ao seu site ou a qualquer aplicativo downstream de terceiros para exibir o banner e fazer atualizações em tempo real nele para refletir as ofertas em andamento.

## Faça atualizações em tempo real no modelo a partir do URL{#update-the-template-from-the-url}

Editar parâmetros diretamente no URL pode ser entediante. Para simplificar:

1. Copie o URL e cole-o em um bloco de notas.
1. Use Cmd+F (Mac) ou Ctrl+F (Windows) para localizar e editar os valores de parâmetro. Tais como:
   * Localizar e substituir caminhos de imagem para camadas de imagem.
   * Localize as coordenadas [parametrizadas](#parameterise-a-layer) da camada, a largura e a altura, para ajustar seus valores.
   * Editar texto, fonte, cor, tamanho ou alinhamento para camadas de texto.
   * Altere os valores de visibilidade entre 0 e 1.

Cole esse URL atualizado no navegador para visualizar as alterações.

## Editar o modelo{#edit-the-template}

Edite o template seguindo estas etapas:

1. No [!DNL Assets view], clique em **[!UICONTROL Dynamic Media Assets]**.
2. Navegue até o local do modelo.
3. Selecione o template.
4. Clique em **[!UICONTROL Editar Modelo]**. A tela de modelo exibe o modelo e a lista de todas as suas camadas no painel Camadas. Comece a editar o modelo de acordo com seus requisitos.

## Adicionar link do Call to action (CTA) à camada de modelo{#add-CTA-in-dynamic-media-templates}

Transforme qualquer camada de imagem, texto ou forma do modelo [!DNL Dynamic Media] em um hiperlink adicionando um link do CTA a ela que direcione os usuários para uma página de destino.

Execute estas etapas para adicionar um link do CTA a uma camada:

1. Navegue até o local do modelo, selecione o modelo e clique em ![editar](/help/assets/assets/edit-pen-icon.svg) **[!UICONTROL Editar Modelo]**. O modelo é exibido na tela.
1. Selecione a camada de modelo e [navegue até o painel de propriedades](#edit-or-delete-a-layer) para adicionar um link de CTA a ela.
1. No painel de propriedades, selecione **[!UICONTROL Adicionar CTA]**, especifique a URL de destino no campo **[!UICONTROL URL]** e clique em **[!UICONTROL Salvar]**.

   ![adicionar CTA](/help/assets/assets/add-cta.png)

1. Clique em **[!UICONTROL Visualizar]** e selecione **[!UICONTROL Publicar]** para publicar seu modelo, se não tiver sido publicado anteriormente.
1. Navegue até a pasta onde este modelo está salvo, selecione este modelo e clique em ![página de detalhes](/help/assets/assets/details-page-icon.svg) **[!UICONTROL Detalhes]**.
1. Clique em **[!UICONTROL Opções de Cópia]** e selecione **[!UICONTROL Copiar Código de Inserção]**. Certifique-se de publicar as imagens do modelo em [!DNL AEM and Dynamic Media] para copiar o código de inserção.

   ![copiar código de inserção](/help/assets/assets/copy-options1.png)

   Veja a seguir um exemplo do Código incorporado:

   ```json
    <div class="adobe-dynamicmedia-template-embed-container">
    <img id="<Image ID>>" src="<Image Source>>" alt="adobe dynamicmedia template" usemap="#adobe-dynamicmedia-template-map" width="800" height="300">
    <map name="adobe-dynamicmedia-template-map">
    <area shape="rect" coords="417,-60,817,340" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    <area shape="rect" coords="6,206.57,129,231.43" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    </map>
    </div>
   ```

1. Adicione o código incorporado copiado ao arquivo HTML do site e execute-o no navegador para exibir o modelo.

Clique no elemento CTA no modelo para navegar até a página de destino.

Assista a este vídeo passo a passo para saber como adicionar um link do CTA a uma camada de modelo.

>[!VIDEO](https://video.tv.adobe.com/v/3457616)

## Pontos importantes a observar {#important-points-to-note}

* Depois de criar um modelo com camadas de imagem com parâmetros para atualizações dinâmicas, verifique se as imagens destinadas a atualizações futuras compartilham as mesmas dimensões que as imagens com parâmetros. Isso garante que as imagens se encaixem perfeitamente dentro das camadas sem transbordar ou deixar espaços vazios. Atualmente, o modelo não oferece suporte a ajustes de dimensão automáticos para ajustar imagens às camadas.
* Não há suporte para substring em uma camada de texto. O usuário não pode aplicar propriedades de fonte diferentes em uma substring de uma camada de texto.
* Atualmente, o suporte para várias empresas do [!DNL Dynamic Media] não está disponível com os Modelos do [!DNL Dynamic Media].
* No caso de copiar ou mover, o Seletor de Destino mostra todas as pastas (incluindo pastas sincronizadas que não são [!DNL Dynamic Media]). Além disso, no momento, ele não exibe os [!DNL Dynamic Media] ativos do modelo (ambos são limitações do seletor de destino).
* Qualquer operação de atualização em uma pasta (por exemplo, Publicar ou Excluir) da seção Assets afeta os [!DNL Dynamic Media] Modelos disponíveis nessa pasta.
* A lixeira não funciona para Modelos [!DNL Dynamic Media]. Se um ativo for movido para o lixo e depois restaurado, ele será restaurado no AEM, mas não no [!DNL Dynamic Media]. O mesmo é válido para [!DNL Dynamic Media] Modelos.

## Consulte também:

1. Explorar [[!DNL Dynamic Media] e seus recursos](/help/assets/dynamic-media/dynamic-media.md)
1. Explorar [[!DNL Dynamic Media] com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md)