---
title: Adicionar tags automaticamente aos ativos com [!DNL Adobe Sensei] serviço inteligente
description: Marque ativos com um serviço artificialmente inteligente que aplica tags comerciais contextuais e descritivas.
contentOwner: AG
feature: Smart Tags,Tagging
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: 9abafe051672de65f042332314445b239f95852b
workflow-type: tm+mt
source-wordcount: '2423'
ht-degree: 5%

---


# Adicionar tags inteligentes aos ativos e melhorar a experiência de pesquisa {#smart-tag-assets-for-faster-search}

As organizações que lidam com ativos digitais cada vez mais usam um vocabulário controlado por taxonomia em metadados de ativos. Basicamente, inclui uma lista de palavras-chave que funcionários, parceiros e clientes costumam usar para consultar e pesquisar seus ativos digitais. Marcar ativos com um vocabulário controlado por taxonomia garante que os ativos possam ser facilmente identificados e recuperados em pesquisas.

Comparado aos vocabulários de linguagem natural, a marcação baseada na taxonomia comercial ajuda a alinhar os ativos aos negócios de uma empresa e garante que os ativos mais relevantes apareçam em pesquisas. Por exemplo, um fabricante de carros pode marcar imagens de carros com nomes de modelo para que somente imagens relevantes sejam exibidas quando pesquisadas para projetar uma campanha promocional.

Em segundo plano, a funcionalidade utiliza a estrutura artificialmente inteligente de [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) para treinar o algoritmo de reconhecimento de imagem na estrutura de tags e na taxonomia comercial. Essa inteligência de conteúdo é então usada para aplicar tags relevantes em um conjunto diferente de ativos. [!DNL Experience Manager Assets] aplica tags inteligentes automaticamente a ativos carregados, por padrão.

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## Tipos de ativos compatíveis {#smart-tags-supported-file-formats}

Você pode adicionar tags aos seguintes tipos de ativos:

* **Imagens**: As imagens em muitos formatos são marcadas usando os serviços de conteúdo inteligente da Adobe Sensei. Você [criar um modelo de treinamento](#train-model) e as imagens carregadas são marcadas automaticamente. As Tags inteligentes são aplicadas aos tipos de arquivos compatíveis que geram renderizações no formato JPG e PNG.
* **Ativos baseados em texto**: [!DNL Experience Manager Assets] adiciona tags automaticamente aos ativos com base em texto compatíveis quando carregados.
* **Ativos de vídeo**: A marcação de vídeo é ativada por padrão em [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. [Os vídeos são marcados automaticamente](/help/assets/smart-tags-video-assets.md) ao fazer upload de novos vídeos ou reprocessar os existentes.

| Imagens (tipos MIME) | Ativos baseados em texto (formatos de arquivo) | Ativos de vídeo (formatos de arquivo e codecs) |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC, JPEG) |
| image/bmp | HTML | AVI (índeo4) |
| image/gif | PDF | FLV (H264/AVC, vp6f) |
| image/pjpeg | PPT | WMV (WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| imagem/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap |  |  |
| image/x-xpixmap |  |  |
| image/x-icon |  |  |
| imagem/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

[!DNL Experience Manager] adiciona automaticamente as Tags inteligentes aos ativos baseados em texto e aos vídeos por padrão. Para adicionar tags inteligentes automaticamente a imagens, conclua as seguintes tarefas.

* [Entender modelos e diretrizes de tags](#understand-tag-models-guidelines).
* [Treinar o modelo](#train-model).
* [Marque seus ativos digitais](#tag-assets).
* [Gerenciar tags e pesquisas](#manage-smart-tags-and-searches).

## Entender modelos e diretrizes de tags {#understand-tag-models-guidelines}

Um modelo de tag é um grupo de tags relacionadas que estão associadas a vários aspectos visuais das imagens que estão sendo marcadas. As tags estão relacionadas a aspectos visuais distintos das imagens, de modo que, quando aplicadas, as tags ajudem a procurar tipos específicos de imagens. Por exemplo, uma coleção de sapatos pode ter tags diferentes, mas todas as tags estão relacionadas a sapatos e podem pertencer ao mesmo modelo de tag. Quando aplicadas, as tags ajudam a encontrar diferentes tipos de sapatos, por exemplo, por design ou por uso. Para entender a representação de conteúdo de um modelo de treinamento em [!DNL Experience Manager], visualize um modelo de treinamento como uma entidade de nível superior constituída por um grupo de tags adicionadas manualmente e imagens de exemplo para cada tag. Cada tag pode ser aplicada exclusivamente a uma imagem.

Antes de criar um modelo de tag e treinar o serviço, identifique um conjunto de tags exclusivas que descrevam melhor os objetos nas imagens no contexto de sua empresa. Certifique-se de que os ativos em seu conjunto preparado estejam em conformidade com o [as orientações em matéria de formação](#training-guidelines).

### Diretrizes de treinamento {#training-guidelines}

Certifique-se de que as imagens no conjunto de treinamento estejam em conformidade com as seguintes diretrizes:

**Quantidade e tamanho:** Mínimo de 10 imagens e máximo de 50 imagens por tag.

**Coerência**: Verifique se as imagens de uma tag são visualmente semelhantes. É melhor adicionar as tags sobre os mesmos aspectos visuais (como o mesmo tipo de objetos em uma imagem) em um único modelo de tag. Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/coherence.png)

**Cobertura**: As imagens da formação devem ser suficientemente variadas. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que [!DNL Experience Manager] aprende a se concentrar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo. Por exemplo, para a tag *model-down-pose*, inclua mais imagens de treinamento semelhantes à imagem realçada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/coverage_1.png)

**Desvio/obstrução**: O serviço se concentra melhor em imagens com menos distração (planos de fundo proeminentes, acompanhamento não relacionado, como objetos/pessoas com o assunto principal). Por exemplo, para a tag *sapato casual*, a segunda imagem não é um bom candidato à formação.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. Por exemplo, para tags, como *capa de chuva* e *perfil de modelo*, adicione ambas as tags ao ativo elegível antes de incluí-lo para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/completeness.png)

**Número de tags**: O Adobe recomenda treinar um modelo usando pelo menos duas tags distintas e pelo menos dez imagens diferentes para cada tag. Em um único modelo de tag, não adicione mais de 50 tags.

**Número de exemplos**: Para cada tag, adicione pelo menos dez exemplos. No entanto, a Adobe recomenda cerca de 30 exemplos. Há suporte para no máximo 50 exemplos por tag.

**Evitar falsos positivos e conflitos**: O Adobe recomenda criar um modelo de tag único para um único aspecto visual. Estruturar os modelos de tags de forma a evitar sobreposições de tags entre os modelos. Por exemplo, não use tags comuns como `sneakers` em dois nomes de modelos de tags diferentes `shoes` e `footwear`. O processo de treinamento substitui um modelo de tag treinado pelo outro para uma palavra-chave comum.

**Exemplos**: Mais alguns exemplos para orientação são:

* Crie um modelo de tag que inclua apenas,

   * As tags relacionadas a modelos de carros.
   * As etiquetas estão relacionadas com coletes para adultos e crianças.

* Não criar,

   * Um modelo de tag que inclui modelos de carros lançados em 2019 e 2020.
   * Vários modelos de tags que incluem os mesmos poucos modelos de carro.

**Imagens usadas para treinar**: Você pode usar as mesmas imagens para treinar diferentes modelos de tags. No entanto, não associe uma imagem a mais de uma tag em um modelo de tag. É possível marcar a mesma imagem com tags diferentes pertencentes a modelos de tags diferentes.

Não é possível desfazer o treinamento. As diretrizes acima devem ajudá-lo a escolher boas imagens para treinar.

## Treinar o modelo de suas tags personalizadas {#train-model}

Para criar e treinar um modelo para suas tags específicas de negócios, siga estas etapas:

1. Crie as tags necessárias e a estrutura de tags apropriada. Faça upload das imagens relevantes no repositório DAM.
1. Em [!DNL Experience Manager] interface do usuário, acesso **[!UICONTROL Ativos]** > **[!UICONTROL Treinamento em tags inteligentes]**.
1. Clique em **[!UICONTROL Criar]**. Forneça uma **[!UICONTROL Título]**, **[!UICONTROL Descrição]**.
1. Clique no ícone de pasta em **[!UICONTROL Tags]** campo. Uma janela pop-up é aberta.
1. Pesquise ou selecione as tags apropriadas a partir das tags existentes em `cq-tags` que você deseja adicionar ao modelo. Clique em **[!UICONTROL Avançar]**.

   >[!NOTE]
   >
   >Você pode classificar a estrutura das tags em ordem crescente ou decrescente com base na variável **[!UICONTROL Nome]** (ordem alfabética), **[!UICONTROL Criado]** data, ou **[!UICONTROL Modificado]** data.


1. No **[!UICONTROL Selecionar ativos]** , clique em **[!UICONTROL Adicionar ativos]** em relação a cada tag. Pesquise no repositório DAM ou navegue pelo repositório para selecionar pelo menos 10 e no máximo 50 imagens. Selecione ativos e não a pasta. Depois de selecionar as imagens, clique em **[!UICONTROL Selecionar]**.

   ![Exibir status de treinamento](assets/smart-tags-training-status.png)

1. Para visualizar as miniaturas das imagens selecionadas, clique na opção na frente de uma tag. Você pode modificar sua seleção clicando em **[!UICONTROL Adicionar ativos]**. Depois de concluir a seleção, clique em **[!UICONTROL Enviar]**. A interface do usuário exibe uma notificação na parte inferior da página, indicando que o treinamento foi iniciado.
1. Verifique o status do treinamento no **[!UICONTROL Status]** para cada modelo de tag. Os status possíveis são [!UICONTROL Pending], [!UICONTROL Treinado]e [!UICONTROL Falha].

![Fluxo de trabalho para treinar o modelo de marcação para Tags inteligentes](assets/smart-tag-model-training-flow.png)

*Figura: Etapas do fluxo de trabalho de treinamento para treinar o modelo de marcação.*

### Exibir o status e o relatório do treinamento {#training-status}

Para verificar se o serviço de Tags inteligentes é treinado em suas tags no conjunto de ativos de treinamento, analise o relatório do fluxo de trabalho de treinamento no console Relatórios .

1. Em [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. No **[!UICONTROL Relatórios de ativos]** página, clique em **[!UICONTROL Criar]**.
1. Selecione o **[!UICONTROL Treinamento em Tags inteligentes]** e clique em **[!UICONTROL Próximo]** na barra de ferramentas.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Em seguida, clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. Para exibir o relatório, clique em **[!UICONTROL Exibir]** na barra de ferramentas.
1. Revise os detalhes do relatório. O relatório exibe o status do treinamento das tags que você treinou. A cor verde no **[!UICONTROL Status de treinamento]** indica que o serviço de Tags inteligentes é treinado para a tag. A cor amarela indica que o serviço é parcialmente treinado para uma tag específica. Para treinar o serviço completamente para uma tag, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento. Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para estas tags.Tags
1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Baixar]** na barra de ferramentas. O relatório é baixado como uma planilha.

<!--
### Tag assets from the workflow console {#tagging-assets-from-the-workflow-console}

1. In [!DNL Experience Manager] interface, go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then click **[!UICONTROL Start Workflow]** from the toolbar.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Specify a title for the workflow and an optional comment. Click **[!UICONTROL Run]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figure: Navigate to the asset folder and review the tags to verify whether your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).*

### Tag assets from the timeline {#tagging-assets-from-the-timeline}

1. From the [!DNL Assets] user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. From upper-left corner, open the **[!UICONTROL Timeline]**.
1. Open actions from the bottom of the left sidebar and click **[!UICONTROL Start Workflow]**.

   ![start_workflow](assets/start_workflow.png)

1. Select the **[!UICONTROL DAM Smart Tag Assets]** workflow, and specify a title for the workflow.
1. Click **[!UICONTROL Start]**. The workflow applies your tags on assets. Navigate to the asset folder and review the tags to verify that your assets are tagged properly. For details, see [manage smart tags](#manage-smart-tags-and-searches).

>[!NOTE]
>
>In the subsequent tagging cycles, only the modified assets are tagged again with newly trained tags. However, even unaltered assets are tagged if the gap between the last and current tagging cycles for the tagging workflow exceeds 24 hours. For periodic tagging workflows, unaltered assets are tagged when the time gap exceeds six months.

### Tag uploaded assets {#tag-uploaded-assets}

[!DNL Experience Manager] can automatically tag the assets that users upload to DAM. To do so, administrators configure a workflow to add an available step that tags assets. See [how to enable Smart Tags for uploaded assets](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).
-->

## Marcar ativos com tags inteligentes {#tag-assets}

Todos os tipos de ativos compatíveis são marcados automaticamente por [!DNL Experience Manager Assets] quando carregado. A marcação é ativada e funciona, por padrão. [!DNL Experience Manager] aplica as tags apropriadas em tempo quase real. <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* Para imagens e vídeos, as Tags inteligentes são baseadas em algum aspecto visual.

* Para ativos baseados em texto, a eficácia das Tags inteligentes não depende da quantidade de texto no ativo, mas das palavras-chave ou entidades relevantes presentes no texto do ativo. Para ativos baseados em texto, as Tags inteligentes são as palavras-chave que aparecem no texto, mas aquelas que melhor descrevem o ativo. Para ativos compatíveis, [!DNL Experience Manager] O já extrai o texto, que é então indexado e é usado para procurar os ativos. No entanto, as Tags inteligentes com base em palavras-chave no texto fornecem uma faceta de pesquisa dedicada, estruturada e de prioridade mais alta. O último ajuda a melhorar a descoberta de ativos em comparação com um índice de pesquisa.

## Gerenciar tags inteligentes e pesquisas de ativos {#manage-smart-tags-and-searches}

Você pode preparar tags inteligentes para remover quaisquer tags imprecisas que possam ter sido atribuídas aos ativos da sua marca, para que somente as tags mais relevantes sejam exibidas.

A moderação de tags inteligentes também ajuda a refinar pesquisas baseadas em tags para ativos, garantindo que seus ativos apareçam nos resultados da pesquisa para as tags mais relevantes. Essencialmente, ajuda a eliminar as chances de ativos não relacionados aparecerem nos resultados da pesquisa.

Também é possível atribuir uma classificação mais alta a uma tag para aumentar a relevância da tag para o ativo. A promoção de uma tag para um ativo aumenta as chances de o ativo aparecer nos resultados da pesquisa quando uma pesquisa é executada com base na tag específica.

Para moderar as tags inteligentes de seus ativos digitais:

1. No campo de pesquisa , procure por ativos digitais com base em uma tag .

1. Para identificar os ativos digitais que você não acha relevantes para sua pesquisa, inspecione os resultados da pesquisa.

1. Selecione um ativo e depois selecione ![Ícone Gerenciar tags](assets/do-not-localize/manage-tags-icon.png) na barra de ferramentas.

1. No **[!UICONTROL Gerenciar tags]** inspecione as tags. Se você não quiser que o ativo seja pesquisado com base em uma tag específica, selecione a tag e selecione ![Ícone Excluir](assets/do-not-localize/delete-icon.png) na barra de ferramentas. Como alternativa, selecione `X` símbolo ao lado do rótulo.

1. Para atribuir uma classificação mais alta a uma tag, selecione a tag e selecione ![Ícone Promover](assets/do-not-localize/promote-icon.png) na barra de ferramentas. A tag promovida é movida para a variável **[!UICONTROL Tags]** seção.

1. Selecionar **[!UICONTROL Salvar]** e depois selecione **[!UICONTROL OK]** para fechar o [!UICONTROL Sucesso] caixa de diálogo.

1. Navegue até o [!UICONTROL Propriedades] página do ativo. Observe que a tag promovida tem uma relevância alta e, portanto, aparece mais alta nos resultados da pesquisa.

### Entender [!DNL Experience Manager] resultados de pesquisa com tags inteligentes {#understand-search}

Por padrão, [!DNL Experience Manager] a pesquisa combina os termos de pesquisa com um `AND` cláusula. O uso de tags inteligentes não altera esse comportamento padrão. O uso de tags inteligentes adiciona uma `OR` para localizar qualquer um dos termos de pesquisa nas tags inteligentes aplicadas. Por exemplo, considere pesquisar por `woman running`. Ativos com apenas `woman` ou apenas `running` palavras-chave nos metadados não aparecem nos resultados da pesquisa por padrão. No entanto, um ativo marcado com `woman` ou `running` o uso de tags inteligentes é exibido em tal query de pesquisa. Então os resultados da pesquisa são uma combinação de...

* Ativos com `woman` e `running` palavras-chave nos metadados.

* Ativos marcados com tags inteligentes com qualquer uma das palavras-chave.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. correspondências de `woman running` nos vários campos de metadados.
1. correspondências de `woman running` em tags inteligentes.
1. correspondências de `woman` ou `running` em tags inteligentes.

## Limitações e práticas recomendadas relacionadas à marcação {#limitations}

A marcação inteligente aprimorada é baseada em modelos de aprendizagem de imagens e suas tags. Esses modelos nem sempre são perfeitos na identificação de tags. A versão atual das Tags inteligentes tem as seguintes limitações:

* Incapacidade de reconhecer sutis diferenças em imagens. Por exemplo, camisas de ajuste fino versus camisas de ajuste regular.
* Incapacidade de identificar tags com base em pequenos padrões ou partes de uma imagem. Por exemplo, logotipos em camisas.
* A marcação é compatível com os idiomas que [!DNL Experience Manager] suporta.
* As tags que não são manipuladas estão relacionadas a:

   * Aspectos não visuais e abstratos. Por exemplo, o ano ou a estação de lançamento de um produto, estado de espírito ou emoção evocado por uma imagem e uma conotação subjetiva de um vídeo.
   * Diferenças visuais em produtos como camisas com e sem coleiras ou logotipos de produtos pequenos embutidos em produtos.

Para treinar o modelo, use as imagens mais apropriadas. O treinamento não pode ser revertido ou o modelo de treinamento não pode ser removido. A precisão da marcação depende do treinamento atual, portanto, faça isso com cuidado.

<!-- TBD: Add limitations related to text files. -->

Para pesquisar arquivos com tags inteligentes (regulares ou aprimoradas), use o [!DNL Assets] pesquisar (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!NOTE]
>
>A capacidade das Tags inteligentes de treinar em suas tags e aplicá-las em outras imagens depende da qualidade das imagens usadas no treinamento.
>Para obter melhores resultados, o Adobe recomenda o uso de imagens visualmente semelhantes para treinar o serviço para cada tag.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Saiba como as tags inteligentes ajudam a gerenciar seus arquivos digitais](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [Usar tags inteligentes para vídeos](smart-tags-video-assets.md)

