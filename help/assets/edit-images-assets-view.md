---
title: Editar imagens
description: Editar imagens usando opções viabilizadas pelo [!DNL Adobe Express] e salvar imagens atualizadas como versões.
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: 23b43f22b62451c9d0a5460999fcd43479438d7e
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 33%

---

# Editar imagens no [!DNL Assets view] {#edit-images-in-assets-view}

A visualização Assets permite a edição básica de imagens, incluindo redimensionamento, remoção de plano de fundo, recorte e conversão entre formatos JPEG e PNG. Além disso, permite a edição avançada por meio da integração com o Adobe Express. Após editar uma imagem, você pode salvar a nova imagem como uma nova versão. O controle de versão ajuda você a reverter para o ativo original posteriormente, se necessário. Para editar uma imagem, [abra sua visualização](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/navigate-view#preview-assets) e clique em **Editar imagem**.

>[!NOTE]
>
>É possível editar imagens de arquivos PNG e JPEG usando o [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Editar imagem {#edit-image}

Acessar a Exibição do Assets, usando o link - [Visualização do Assets](https://experience.adobe.com/#/assets) e selecionando o repositório correto. Para receber acesso, entre em contato com o administrador da organização.
Para obter informações de referência adicionais, consulte - [Introdução ao uso do Adobe Experience Manager Assets View](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view), [Entender a interface de exibição do Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/navigate-assets-view#understand-interface-navigation), e [Casos de uso do Assets View](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/get-started-assets-view#use-cases).
<!--
>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Adobe Express Integration"
>abstract="Easy and intuitive image-editing tools powered by Adobe Express available directly within AEM Assets to increase content reuse and accelerate content velocity."-->

### Editar imagem na visualização Assets usando o Adobe Express {#edit-image-on-assets-view-using-adobe-express}

Depois de acessar a Exibição do Assets, clique em **Assets**, selecione uma imagem e clique em **Editar** do painel superior. A nova tela exibe as opções de edição disponíveis, incluindo redimensionamento, remoção do plano de fundo, recorte e conversão entre formatos JPEG e PNG.

#### Redimensionar imagem {#resize-image-using-express}

Redimensionar uma imagem para um tamanho específico é um caso de uso comum. O Assets View permite redimensionar rapidamente as imagens para ajustá-las aos tamanhos de foto comuns, fornecendo novas resoluções pré-calculadas para tamanhos de foto específicos. Para redimensionar a imagem usando a Exibição do Assets, siga as etapas abaixo:

1. Clique em **Redimensionar imagem** no painel esquerdo.
1. Selecione a plataforma de rede social apropriada na lista suspensa Redimensionar e selecione o tamanho da imagem nas opções exibidas.
1. Dimensione a imagem, se necessário, usando o campo **Dimensionamento de imagem**.
1. Clique em **[!UICONTROL Aplicar]** para aplicar as alterações.
   ![Edição de imagens com o Adobe Express](assets/adobe-express-resize-image.png)

   A imagem editada estará disponível para download. É possível salvar o ativo editado como uma nova versão do mesmo ativo ou como um novo ativo.
   ![Salvamento de imagens com o Adobe Express](assets/adobe-express-resize-save.png)

#### Remover fundo {#remove-background-using-express}

Você pode remover o plano de fundo de uma imagem seguindo as etapas mencionadas abaixo:

1. Clique em **Remover plano de fundo** no painel esquerdo. O Experience Manager Assets exibirá a imagem sem o fundo.
1. Clique em **[!UICONTROL Aplicar]** para aplicar as alterações.
   ![Salvamento de imagens com o Adobe Express](assets/adobe-express-remove-background.png)

   A imagem editada estará disponível para download. É possível salvar o ativo editado como uma nova versão do mesmo ativo ou como um novo ativo.

#### Cortar imagem {#crop-image-using-express}

Transformar uma imagem em um tamanho perfeito é simples usando incorporado [!DNL Adobe Express] ações rápidas.

1. Clique em **[!UICONTROL Cortar imagem]** no painel esquerdo.
2. Arraste as alças nos cantos da imagem para criar o corte desejado.
3. Clique em **[!UICONTROL Aplicar]**.
   ![Salvar imagem com o Adobe Express](assets/adobe-express-crop-image.png)
A imagem cortada estará disponível para download. É possível salvar o ativo editado como uma nova versão do mesmo ativo ou como um novo ativo.

#### Converter entre tipos de arquivo de imagem {#convert-image-types-using-express}

É possível converter rapidamente entre formatos de imagem JPEG e PNG usando o Adobe Express. Execute as seguintes etapas:

1. Clique em **JPEG para PNG** ou **PNG para JPEG** no painel esquerdo.
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
1. Clique em **[!UICONTROL Baixar]**.

#### Limitações {#limitations-adobe-express}

* Resolução da imagem compatível: mínimo de 50 pixels e máximo de 6.000 pixels por dimensão.

* Tamanho máximo do arquivo aceito: 17 MB.

### Editar imagens no editor incorporado do Adobe Express {#edit-images-in-adobe-express-embedded-editor}

Os usuários com direito ao Express podem usar o editor Express incorporado na Exibição do Assets para editar conteúdo facilmente e criar novo conteúdo com GenAI do Adobe Firefly. Isso melhora a reutilização do conteúdo e acelera a velocidade do conteúdo. Você também pode usar elementos predefinidos para que seu ativo tenha uma aparência incrível ou executar ações rápidas para editar sua imagem com apenas alguns cliques.
![express na interface do usuário do essentials](/help/assets/assets/express-in-essentials-ui.jpg)
Para editar imagens usando [!DNL Adobe Express] editor incorporado, siga as etapas abaixo:

1. Acesse a Exibição do AEM Assets usando o link - [Visualização do AEM Assets](https://experience.adobe.com/#/assets) e selecione o repositório correto.
1. Clique em **Assets**, insira uma pasta e selecione uma imagem.
1. Clique em **Abrir no Adobe Express**. A imagem é aberta em uma tela expressa.
1. Faça as edições necessárias na imagem.
1. Se o projeto exigir que você adicione mais páginas, clique em **Adicionar**, selecione ativos, insira uma pasta, selecione uma imagem para trazer para a página da tela e faça as edições necessárias na imagem.
1. Para salvar as imagens, clique em **Salvar**. A caixa de diálogo Salvar é exibida.

   >[!NOTE]
   >
   > **1. Para Página Única**
   >
   > **Salvar como versão:** Esse recurso suporta salvar apenas um único ativo. Selecione essa opção para exportar a imagem como uma nova versão (mantendo o formato original) e salvá-la na mesma pasta.
   > **Salvar como novo ativo:** Selecione essa opção para exportar o ativo em um formato diferente do original e salvá-lo em qualquer pasta como um novo ativo.
   >  
   > **2. Para várias páginas**
   >
   > **Salvar como versão:** Esse recurso suporta salvar apenas um único ativo. Se quiser salvar uma única página de várias páginas, selecione essa opção para salvar o ativo no formato e no local originais.\
   > **Salvar como novo ativo:** Com essa opção, você exporta vários ativos ou um único ativo para qualquer pasta e os salva como novos ativos com o formato de arquivo original ou diferente.

1. Na caixa de diálogo Salvar:
   1. Insira um nome para o arquivo na variável **Salvar como** campo.
   1. Selecione uma pasta de destino.
   1. Opcional: forneça detalhes como nome do projeto ou da campanha, palavras-chave, canais, intervalo de tempo e região.
1. Clique em **Salvar como versão** ou **Salvar como novo ativo** para salvar o(s) ativo(s).

#### Limitações da edição de imagens no Express Editor {#limitations-of-editing-images-in-the-express-editor}

* Tipo de arquivo suportado: JPEG ou PNG.
* Tamanho máximo do arquivo aceito: 40 MB.
* Intervalo de largura e altura compatível: entre 50 e 8000 pixels.
* Recarregue a página para ver o novo ativo salvo mais recentemente na pasta de origem.

### Criar novos ativos usando o Adobe Express {#create-new-embedded-editor}

O [!DNL Assets view] permite criar um novo modelo do zero usando o editor integrado do [!DNL Adobe Express]. Para criar um novo ativo usando o [!DNL Adobe Express], execute as etapas a seguir:

1. Navegue até **[!UICONTROL Meu Workspace]** e clique em **[!UICONTROL Criar]** no banner Adobe Express que é exibido na parte superior. A tela em branco do [!DNL Adobe Express] é exibida dentro da interface do [!DNL Assets view].
1. Crie o conteúdo usando [modelos](https://helpx.adobe.com/br/express/using/work-with-templates.html). Caso contrário, navegue até **[!UICONTROL Seus itens]** para modificar o conteúdo existente.
1. Após concluir a edição, clique em **[!UICONTROL Salvar]**.
1. Especifique o caminho de destino para o ativo criado e clique em **[!UICONTROL Salvar como novo ativo]**.

#### Limitações {#limitations}

* É possível modificar apenas as imagens com tipos de formato `JPEG` e `PNG`.
* O tamanho do ativo deve ser inferior a 40 MB.
* É possível salvar uma imagem nos formatos `PDF`, `JPEG` ou `PNG`.

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

* Forneça feedback sobre o produto usando o [!UICONTROL Feedback] opção disponível na interface de usuário de visualização do Assets.

* Forneça feedback sobre a documentação por meio das opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita.

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/pt-br?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Ações rápidas no Adobe Express](https://helpx.adobe.com/br/express/using/resize-image.html)
>* [Exibir o histórico de versões de um ativo](navigate-assets-view.md)
