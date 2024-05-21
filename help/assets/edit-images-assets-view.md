---
title: Editar imagens
description: Editar imagens usando opções viabilizadas pelo [!DNL Adobe Photoshop Express] e salvar imagens atualizadas como versões.
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
source-git-commit: 89d13f278fdaddbcf6b07a2f3edfc1fda1092aa2
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 72%

---

# Editar imagens no [!DNL Assets view] {#edit-images}

O [!DNL Assets view] fornece opções de edição fáceis de usar viabilizadas pelo [!DNL Adobe Express] e [!DNL Adobe Photoshop Express] As ações de edição disponíveis usando [!DNL Adobe Express] são Redimensionar imagem, Remover plano de fundo, Cortar imagem e Converter JPEG em PNG ou vice-versa.

Após editar uma imagem, você pode salvar a nova imagem como uma nova versão. O controle de versão ajuda você a reverter para o ativo original posteriormente, se necessário. Além disso, o controle de versão está disponível apenas para os tipos de arquivo PNG, o que significa que quando você tenta remover o plano de fundo de um tipo de arquivo JPG, o JPG é convertido automaticamente em PNG. Para editar uma imagem, [abra sua visualização](navigate-assets-view.md) e clique em **[!UICONTROL Editar imagem]**.

>[!NOTE]
>
>É possível editar imagens de arquivos PNG e JPEG usando o [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Edição de imagens usando o Adobe Express {#edit-using-express}

>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Integração do Adobe Express"
>abstract="Ferramentas de edição de imagens fáceis e intuitivas, viabilizadas pelo Adobe Express, disponíveis diretamente no AEM Assets para aumentar a reutilização de conteúdo e acelerar sua velocidade."

### Redimensionar imagem {#resize-image-using-express}

Redimensionar uma imagem para um tamanho específico é um caso de uso comum. O [!DNL Assets view] permite redimensionar rapidamente a imagem para ajustá-la aos tamanhos de foto comuns, fornecendo novas resoluções pré-calculadas para tamanhos de foto específicos. Para redimensionar a imagem usando o [!DNL Assets view], siga as etapas abaixo:

1. Selecione uma imagem da sua [!DNL Experience Manager] Repositório de ativos e clique em **Editar**.
2. Clique em **[!UICONTROL Redimensionar imagem]** nas ações rápidas disponíveis no painel esquerdo.
3. Selecione a plataforma de rede social apropriada na lista suspensa **[!UICONTROL Redimensionar para]** e escolha o tamanho da imagem nas opções exibidas.
4. Dimensione a imagem, se necessário, usando o campo **[!UICONTROL Dimensionamento de imagem]**.
5. Clique em **[!UICONTROL Aplicar]** para aplicar as alterações.
   ![Edição de imagens com o Adobe Express](assets/adobe-express-resize-image.png)

   A imagem editada estará disponível para download. É possível salvar o ativo editado como uma nova versão do mesmo ativo ou como um novo ativo.
   ![Salvamento de imagens com o Adobe Express](assets/adobe-express-resize-save.png)

### Remover fundo {#remove-background-using-express}

Você pode remover o fundo de uma imagem em algumas etapas simples, como mencionado abaixo:

1. Selecione uma imagem da sua [!DNL Experience Manager] Repositório de ativos e clique em **Editar**.
2. Clique em **[!UICONTROL Remover fundo]** nas ações rápidas disponíveis no painel esquerdo. O Experience Manager Assets exibirá a imagem sem o fundo.
3. Clique em **[!UICONTROL Aplicar]** para aplicar as alterações.
   ![Salvamento de imagens com o Adobe Express](assets/adobe-express-remove-background.png)

### Cortar imagem {#crop-image-using-express}

É fácil transformar uma imagem em um tamanho perfeito usando as ações rápidas do [!DNL Adobe Express] incorporadas.

1. Selecione uma imagem da sua [!DNL Experience Manager] Repositório de ativos e clique em **Editar**.
2. Clique em **[!UICONTROL Cortar imagem]** nas ações rápidas disponíveis no painel esquerdo.
3. Arraste as alças nos cantos da imagem para criar o corte desejado.
4. Clique em **[!UICONTROL Aplicar]**.
   ![Salvar imagem com o Adobe Express](assets/adobe-express-crop-image.png)
A imagem cortada estará disponível para download. É possível salvar o ativo editado como uma nova versão do mesmo ativo ou como um novo ativo.

### Converter JPEG em PNG {#convert-jpeg-to-png-using-express}

É possível converter rapidamente uma imagem JPEG em PNG usando o Adobe Express. Execute as seguintes etapas:

1. Selecione uma imagem da sua [!DNL Experience Manager] Repositório de ativos e clique em **Editar**.
2. Clique em **[!UICONTROL Converter em PNG]** nas ações rápidas disponíveis no painel esquerdo.
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
3. Clique em **[!UICONTROL Aplicar]**.
4. Navegue até **[!UICONTROL Salvar como na parte superior direita]** e clique em **[!UICONTROL Salvar como novo ativo]**.

### Converter PNG em JPEG {#convert-png-to-jpeg-using-express}

Você pode converter rapidamente uma imagem PNG em um formato JPEG usando Adobe Express. Execute as seguintes etapas:

1. Selecione uma imagem da sua [!DNL Experience Manager] Repositório de ativos e clique em **Editar**.
2. Clique em **[!UICONTROL Converter em JPEG]** nas ações rápidas disponíveis no painel esquerdo.
3. Clique em **[!UICONTROL Aplicar]**.
4. Navegue até **[!UICONTROL Salvar como na parte superior direita]** e clique em **[!UICONTROL Salvar como novo ativo]**.

### Limitações {#limitations-adobe-express}

* Resolução de imagem compatível: mínimo de 50 pixels e máximo de 6000 pixels por dimensão

* Tamanho de arquivo máximo aceito: 17 MB

## Editar imagens usando o editor integrado do Adobe Express {#edit-using-embedded-editor}

As organizações com acesso ao Adobe Express podem usar as ferramentas integradas de edição e criação de imagens do Adobe Express e do Adobe Firefly disponíveis diretamente na visualização de Ativos para melhorar a reutilização do conteúdo e acelerar a velocidade do conteúdo. Você também pode usar elementos predefinidos para que seu ativo tenha uma aparência incrível ou para executar ações de edição rápidas na imagem com apenas alguns cliques.

Para editar imagens usando o editor integrado do [!DNL Adobe Express], siga as etapas abaixo:

1. Selecione uma imagem do repositório de ativos do [!DNL Experience Manager].
1. Clique em **[!UICONTROL Abrir no Adobe Express]**.

   ![Editor integrado do Adobe Express](assets/embedded-editor.png)

   Você pode aproveitar a funcionalidade do [!DNL Adobe Express] para executar todas as ações relacionadas à edição de imagens, como [redimensionar imagem](https://helpx.adobe.com/br/express/using/resize-image.html), [remover ou alterar a cor do fundo](https://helpx.adobe.com/br/express/using/remove-background.html), [cortar a imagem](https://helpx.adobe.com/br/express/using/crop-image.html) e muito mais.

1. Após concluir a edição de imagens, você pode baixar um ativo como um novo ativo ou salvá-lo como uma nova versão.

## Criar novos ativos usando o Adobe Express {#create-new-embedded-editor}

O [!DNL Assets view] permite criar um novo modelo do zero usando o editor integrado do [!DNL Adobe Express]. Para criar um novo ativo usando o [!DNL Adobe Express], execute as etapas a seguir:

1. Navegue até **[!UICONTROL Meu espaço de trabalho]** e clique em **[!UICONTROL Criar]** no banner Adobe Express que é exibido na parte superior. A tela em branco do [!DNL Adobe Express] é exibida dentro da interface do [!DNL Assets view].
1. Crie o conteúdo usando [modelos](https://helpx.adobe.com/br/express/using/work-with-templates.html). Caso contrário, navegue até **[!UICONTROL Seus itens]** para modificar o conteúdo existente.
1. Após concluir a edição, clique em **[!UICONTROL Salvar como novo ativo]**.
1. Especifique o caminho de destino do ativo criado e clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>* É possível modificar apenas as imagens com tipos de formato `JPEG` e `PNG`.
>* O tamanho do ativo deve ser inferior a 17 MB.
>* É possível salvar uma imagem no `PDF`, `JPEG`ou `PNG` formatos; considerando que, quando há várias páginas, você pode salvá-las como `PDF`.

<!-- 
## Edit images using [!DNL Adobe Photoshop Express] {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->
<!-- 
### Touch up images {#spot-heal-images-using-photoshop-express}

If there are minor spots or small objects on an image, you can edit and remove the spots using the spot healing feature provided by Adobe Photoshop.

The brush samples the retouched area and makes the repaired pixels blend seamlessly into the rest of the image. Use a brush size that is only slightly larger than the spot you want to fix.

![Spot healing edit option](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->
<!-- 
### Crop and straighten images {#crop-straighten-images-using-photoshop-express}

Using the crop and straighten option that you can do basic cropping, rotate image, flip it horizontally or vertically, and crop it to dimensions suitable for popular social media websites.

To save your edits, click **[!UICONTROL Crop Image]**. After editing, you can save the new image as a version.

![Option to crop and straighten](assets/edit-crop-straighten.png)

Many default options let you crop your image to the best proportions that fit various social media profiles and posts.

### Resize image {#resize-image-using-photoshop-express}

You can view the common photo sizes in centimeters or inches to know the dimensions. By default, the resizing method retains the aspect ratio. To manually override the aspect ratio, click ![](assets/do-not-localize/lock-closed-icon.png).

Enter the dimensions and click **[!UICONTROL Resize Image]** to resize the image. Before you save the changes as a version, you can either undo all the changes done before saving by clicking [!UICONTROL Undo] or you can change the specific step in the editing process by clicking [!UICONTROL Revert].

![Options when resizing an image](assets/resize-image.png)

### Adjust image {#adjust-image-using-photoshop-express}

[!DNL Assets view] lets you adjust the color, tone, contrast, and more, with just a few clicks. Click **[!UICONTROL Adjust image]** in the edit window. The following options are available in the right sidebar:

* **Popular**: [!UICONTROL High Contrast & Detail], [!UICONTROL Desaturated Contrast], [!UICONTROL Aged Photo], [!UICONTROL B&W Soft], and [!UICONTROL B&W Sepia Tone].
* **Color**: [!UICONTROL Natural], [!UICONTROL Bright], [!UICONTROL High Contrast], [!UICONTROL High Contrast & Detail], [!UICONTROL Vivid], and [!UICONTROL Matte].
* **Creative**: [!UICONTROL Desaturated Contrast], [!UICONTROL Cool Light], [!UICONTROL Turquoise & Red], [!UICONTROL Soft Mist], [!UICONTROL Vintage Instant], [!UICONTROL Warm Contrast], [!UICONTROL Flat & Green], [!UICONTROL Red Lift Matte], [!UICONTROL Warm Shadows], and [!UICONTROL Aged Photo].
* **B&W**: [!UICONTROL B&W Landscape], [!UICONTROL B&W High Contrast], [!UICONTROL B&W Punch], [!UICONTROL B&W Low Contrast], [!UICONTROL B&W Flat], [!UICONTROL B&W Soft], [!UICONTROL B&W Infrared], [!UICONTROL B&W Selenium Tone], [!UICONTROL B&W Sepia Tone], and [!UICONTROL B&W Split Tone].
* **Vignetting**: [!UICONTROL None], [!UICONTROL Light], [!UICONTROL Medium], and [!UICONTROL Heavy].

![Adjust image by editing](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### Próximas etapas {#next-steps}

* Forneça feedback sobre o produto usando a opção [!UICONTROL Feedback] disponível na interface de visualização do Assets

* Forneça feedback sobre a documentação usando as opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/pt-br?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Ações rápidas no Adobe Express](https://helpx.adobe.com/br/express/using/resize-image.html)
>* [Exibir o histórico de versões de um ativo](navigate-assets-view.md)
