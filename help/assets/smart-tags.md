---
title: Tags inteligentes aprimoradas
description: Aplique tags comerciais contextuais e descritivas usando o serviço AI e ML do Adobe Sensei, para melhorar a descoberta de ativos e a velocidade do conteúdo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: dfa9b099eaf7f0d155986bbab7d56901876d98f6

---


# Marcar seus ativos com tags inteligentes {#smart-tag-assets}

## Visão geral das tags inteligentes {#overview-of-enhanced-smart-tags}

As organizações que lidam com ativos digitais cada vez mais usam vocabulário controlado por taxonomia em metadados de ativos. Basicamente, inclui uma lista de palavras-chave que os funcionários, parceiros e clientes normalmente usam para consultar e procurar ativos digitais de uma classe específica. Marcar ativos com vocabulário controlado por taxonomia garante que eles possam ser facilmente identificados e recuperados por pesquisas baseadas em tags.

Comparado aos vocabulários de linguagem natural, a marcação de ativos digitais com base na taxonomia comercial ajuda a alinhá-los aos negócios de uma empresa e garante que os ativos mais relevantes sejam exibidos nas pesquisas. Por exemplo, um fabricante de carros pode marcar imagens de carros com nomes de modelos para que somente imagens relevantes sejam exibidas quando imagens de vários modelos forem pesquisadas para projetar uma campanha de promoção.

Em segundo plano, o Serviço de conteúdo inteligente usa a estrutura do AI do [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para treinar seu algoritmo de reconhecimento de imagem na estrutura de tags e na taxonomia comercial. Essa inteligência de conteúdo é então usada para aplicar tags relevantes em um conjunto diferente de ativos.

>[!NOTE]
>
>Os Serviços de conteúdo inteligente se aplicam somente aos clientes do Assets. O Serviço de conteúdo inteligente está disponível para compra como um complemento do Experience Manager.

<!-- ![flowchart](assets/flowchart.gif) -->

## Gerenciar tags inteligentes e pesquisas {#manage-smart-tags-and-searches}

É possível preparar tags inteligentes para remover tags imprecisas que possam ter sido atribuídas às imagens da sua marca, de modo que somente as tags mais relevantes sejam exibidas.

A moderação de tags inteligentes também ajuda a refinar pesquisas baseadas em tags para imagens, garantindo que sua imagem apareça nos resultados da pesquisa para as tags mais relevantes. Essencialmente, ajuda a eliminar as chances de imagens não relacionadas aparecerem nos resultados da pesquisa.

Também é possível atribuir uma classificação mais alta a uma tag para aumentar sua relevância em relação a uma imagem. A promoção de uma tag para uma imagem aumenta as chances de a imagem aparecer nos resultados da pesquisa quando uma pesquisa é realizada com base na tag específica.

1. Na caixa Omnisearch, procure ativos com base em uma tag.
1. Inspecione os resultados da pesquisa para identificar uma imagem que não seja relevante para a sua pesquisa.
1. Selecione a imagem e clique/toque no ícone **[!UICONTROL Gerenciar tags]** na barra de ferramentas.
1. Na página **[!UICONTROL Gerenciar tags]** , inspecione as tags. Se você não quiser que a imagem seja pesquisada com base em uma tag específica, selecione a tag e clique/toque no ícone Excluir da barra de ferramentas. Como alternativa, clique/toque no `X` símbolo que aparece ao lado do rótulo.
1. Para atribuir uma classificação superior a uma tag, selecione-a e clique/toque no ícone promover na barra de ferramentas. A tag promovida é movida para a seção **[!UICONTROL Tags]** .
1. Clique/toque em **[!UICONTROL Salvar]** e, em seguida, clique/toque em **[!UICONTROL OK]** para fechar a caixa de diálogo Êxito.
1. Navegue até a página de propriedades da imagem. Observe que a tag promovida tem uma relevância alta e, portanto, aparece mais alta nos resultados da pesquisa.

### Compreender os resultados da pesquisa do AEM com tags inteligentes {#understandsearch}

Por padrão, a pesquisa do AEM combina os termos de pesquisa com uma `AND` cláusula. O uso de tags inteligentes não altera esse comportamento padrão. O uso de tags inteligentes adiciona uma `OR` cláusula adicional para localizar qualquer um dos termos de pesquisa nas tags inteligentes aplicadas. For example, consider searching for `woman running`. Por padrão, os ativos com apenas `woman` ou apenas `running` palavras-chave nos metadados não aparecem nos resultados da pesquisa. No entanto, um ativo marcado com tags inteligentes `woman` ou `running` usando tags inteligentes aparece em uma consulta de pesquisa. Então os resultados da pesquisa são uma combinação de...

* ativos com `woman` e `running` palavras-chave nos metadados.

* ativos marcados com inteligência com qualquer uma das palavras-chave.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos dos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. corresponde `woman running` aos vários campos de metadados.
1. corresponde a `woman running` em tags inteligentes.
1. correspondências de `woman` ou de `running` em tags inteligentes.

<!-- 

## Training the Smart Content Service {#training-the-smart-content-service}

For the Smart Content Service to recognize your business taxonomy, run it on a set of assets that already include tags that are relevant to your business. After training, the service can apply the same taxonomy on a similar set of assets.

You can train the service multiple times to improve its ability to apply relevant tags. After each training cycle, run a tagging workflow and check whether your assets are tagged appropriately.

You can train the Smart Content Service periodically or on requirement basis.

>[!NOTE]
>
>The training workflow runs on folders only.

### Periodic training {#periodic-training}

You can enable the Smart Content Service to train periodically on the assets and associated tags within a folder. Open the properties page of your asset folder, select **[!UICONTROL Enable Smart Tags]** under the **[!UICONTROL Details]** tab, and save the changes.

Once this option is selected for a folder, AEM runs a training workflow automatically to train the Smart Content Service on the folder assets and their tags. By default, the training workflow runs on a weekly basis at 12:30 AM on Saturdays.

### On-demand training {#on-demand-training}

You can train the Smart Content Service whenever required from the Workflow console.

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools > Workflow > Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL Smart Tags Training]** workflow and then tap/click **[!UICONTROL Start Workflow]** from the toolbar.
1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder that includes the tagged assets for training the service.
1. Specify a title for the workflow and a add a comment. Then, tap/click **[!UICONTROL Run]**. The assets and tags are submitted for training.

>[!NOTE]
>
>Once the assets in a folder are processed for training, only the modified assets are processed in subsequent training cycles.

### Viewing training reports {#viewing-training-reports}

To check whether the Smart Content Service is trained on your tags in the training set of assets, review the training workflow report from the Reports console.

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools > Assets > Reports]**.
1. In the **[!UICONTROL Asset Reports]** page, tap/click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then tap/click **[!UICONTROL Next]** from the toolbar.
1. Specify a title and description for the report. Under **[!UICONTROL Schedule Report]**, leave the **[!UICONTROL Now]** option selected. If you want to schedule the report for later, select **[!UICONTROL Later]** and specify a date and time. Then, tap/click **[!UICONTROL Create]** from the toolbar.
1. In the **[!UICONTROL Asset Reports]** page, select the report you generated. To view the report, tap/click the **[!UICONTROL View]** icon from the toolbar.
1. Review the details of the report.

   The report displays the training status for the tags you trained. The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Content Service is trained for the tag. Yellow color indicates that the service is not completely trained for a particular tag. In this case, add more images with the particular tag and run the training workflow to train the service completely on the tag.

   If you do not see your tags in this report, run the training workflow again for these tags.

1. To download the report, select it from the list, and tap/click the **[!UICONTROL Download]** icon from the toolbar. The report downloads as an Excel file.

## Tagging assets automatically {#tagging-assets-automatically}

After you have trained the Smart Content Service, you can trigger the tagging workflow to automatically apply appropriate tags on a different set of similar assets.

You can run the tagging workflow periodically or whenever required.

>[!NOTE]
>
>The tagging workflow runs on both assets and folders.

### Periodic tagging {#periodic-tagging}

You can enable the Smart Content Service to periodically tag assets within a folder. Open the properties page of your asset folder, select **[!UICONTROL Enable Smart Tags]** under the **[!UICONTROL Details]** tab, and save the changes.

Once this option is selected for a folder, the Smart Content Service automatically tags the assets within the folder. By default, the tagging workflow runs every day at 12:00 AM.

### On-demand tagging {#on-demand-tagging}

You can trigger the tagging workflow from the following to instantly tag your assets:

* Workflow console
* Timeline

>[!NOTE]
>
>If you run the tagging workflow from the timeline, you can apply tags on a maximum of 15 assets at a time.

#### Tagging assets from the Workflow console {#tagging-assets-from-the-workflow-console}

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools > Workflow > Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then tap/click **[!UICONTROL Start Workflow]** from the toolbar.
1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Specify a title for the workflow and an optional comment. Then, tap/click **[!UICONTROL Run]**.

Navigate to the asset folder and review the tags to verify whether the Smart Content Service tagged your assets properly. For details, see [Managing Smart Tags](manage-smart-tags.md).

#### Tagging assets from the timeline {#tagging-assets-from-the-timeline}

1. From the Assets user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. Tap/click the GlobalNav icon and open the timeline.
1. Tap/click the arrow at the bottom, and then tap/click **[!UICONTROL Start Workflow]**.
1. Select the **[!UICONTROL DAM Smart Tag Assets]** workflow, and specify a title for the workflow.
1. Tap/click **[!UICONTROL Start]**. The workflow applies your tags on assets. Navigate to the asset folder and review the tags to verify whether the Smart Content Service tagged your assets properly. For details, see [Managing Smart Tags](manage-smart-tags.md).

>[!NOTE]
>
>In the subsequent tagging cycles, only the modified assets are tagged again with newly-trained tags.
>
>However, even unaltered assets are tagged if the gap between the last and current tagging cycles for the tagging workflow exceeds 24 hours.
>
>For periodic tagging workflows, unaltered assets are tagged when the gap exceeds 6 months.


## Smart Content Service Training Guidelines {#smart-content-service-training-guidelines}

To be able to effectively tag your brand images, the Smart Content Service requires that the training images conform to certain guidelines. For best results, images in your training set should conform to the following guidelines:

**Quantity and size:** Minimum 30 images per tag. Minimum of 500 pixels on the longer side.

**Coherence**: Images for a tag should be visually similar.

For example, it is not a good idea to tag all of these images as `my-party` (for training) because they are not visually similar.

![Illustrative images to exemplify the guidelines for training](assets/do-not-localize/coherence.png)

**Coverage**: There should be sufficient variety in the images in the training. The idea is to supply a few but reasonably diverse examples so that AEM learns to focus on the right things. If you're applying the same tag on visually dissimilar images, include at least five examples of each kind.

For example, for the tag *model-down-pose*, include more training images similar to the highlighted image below for the service to identify similar images more accurately during tagging.

![Illustrative images to exemplify the guidelines for training](assets/do-not-localize/coverage_1.png)

**Distraction/obstruction**: The service trains better on images that have less distraction (prominent backgrounds, unrelated accompaniments, such as objects/persons with the main subject).

For example, for the tag *casual-shoe*, the second image is not a good training candidate.

![Illustrative images to exemplify the guidelines for training](assets/do-not-localize/distraction.png)

**Completeness:** If an image qualifies for more than one tag, add all applicable tags before including the image for training. For example, for tags, such as *raincoat* and *model-side-view*, add both the tags on the eligible asset before including it for training.

![Illustrative images to exemplify the guidelines for training](assets/do-not-localize/completeness.png)

### Training limitations {#limitations}

Enhanced smart tags are based on learning models of brand images and their tags. These models are not always perfect at identifying tags. The current version of the Smart Content Service has the following limitations:

* Inability to recognize subtle differences in images. For example, slim versus regular fitted shirts.
* Inability to identify tags based on tiny patterns/parts of an image. For example, logos on T-shirts.
* Tagging is supported in the locales that AEM is supported in. For a list of languages, see [Smart Content Services release notes](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html).

To search for assets with smart tags (regular or enhanced), use the Assets Omnisearch (full-text search). There is no separate search predicate for smart tags. 

>[!NOTE]
>
>The ability of the Smart Content Service to train on your tags and apply them on other images depends on the quality of images you use for training. 
>
>For best results, Adobe recommends that you use visually similar images to train the service for each tag.

-->
