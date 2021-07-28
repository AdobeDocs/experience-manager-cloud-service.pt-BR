---
title: Marcar ativos automaticamente com o  [!DNL Adobe Sensei] serviço inteligente
description: Marque ativos com um serviço artificialmente inteligente que aplica tags comerciais contextuais e descritivas.
contentOwner: AG
feature: Tags inteligentes,Marcação
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: 632bcb3406fc4bc856e7fcf11cb9826a03e6a5d2
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 5%

---


# Adicionar tags inteligentes aos ativos e melhorar a experiência de pesquisa {#smart-tag-assets-for-faster-search}

As organizações que lidam com ativos digitais cada vez mais usam um vocabulário controlado por taxonomia em metadados de ativos. Basicamente, inclui uma lista de palavras-chave que funcionários, parceiros e clientes costumam usar para consultar e pesquisar seus ativos digitais. Marcar ativos com um vocabulário controlado por taxonomia garante que os ativos possam ser facilmente identificados e recuperados em pesquisas.

Comparado aos vocabulários de linguagem natural, a marcação baseada na taxonomia comercial ajuda a alinhar os ativos aos negócios de uma empresa e garante que os ativos mais relevantes apareçam em pesquisas. Por exemplo, um fabricante de carros pode marcar imagens de carros com nomes de modelo para que somente imagens relevantes sejam exibidas quando pesquisadas para projetar uma campanha promocional.

Em segundo plano, a funcionalidade usa a estrutura artificialmente inteligente de [Adobe Sensei](https://business.adobe.com/why-adobe/experience-cloud-artificial-intelligence.html) para treinar seu algoritmo de reconhecimento de imagem em sua estrutura de tags e taxonomia comercial. Essa inteligência de conteúdo é então usada para aplicar tags relevantes em um conjunto diferente de ativos. [!DNL Experience Manager Assets] aplica tags inteligentes automaticamente a ativos carregados, por padrão.

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## Tipos de ativos compatíveis {#smart-tags-supported-file-formats}

Você pode adicionar tags aos seguintes tipos de ativos:

* **Imagens**: As imagens em muitos formatos são marcadas usando os serviços de conteúdo inteligente da Adobe Sensei. Você [cria um modelo de treinamento](#train-model) e, em seguida, as imagens carregadas são marcadas automaticamente. As Tags inteligentes são aplicadas aos tipos de arquivo compatíveis que geram renderizações no formato JPG e PNG.
* **Ativos** baseados em texto:  [!DNL Experience Manager Assets] adiciona tags automaticamente aos ativos com base em texto compatíveis quando carregados.
* **Ativos** de vídeo: A marcação de vídeo é ativada por padrão no  [!DNL Adobe Experience Manager] as a  [!DNL Cloud Service]. [Os vídeos são ](/help/assets/smart-tags-video-assets.md) marcados automaticamente ao fazer upload de novos vídeos ou reprocessar os existentes.

| Imagens (tipos MIME) | Ativos baseados em texto (formatos de arquivo) | Ativos de vídeo (formatos de arquivo e codecs) |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC, Motion JPEG) |
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

* [Entenda os modelos e as diretrizes de tags](#understand-tag-models-guidelines).
* [Treine o modelo](#train-model).
* [Marque seus ativos](#tag-assets) digitais.
* [Gerencie as tags e pesquisas](#manage-smart-tags-and-searches).

## Entender modelos e diretrizes de tags {#understand-tag-models-guidelines}

Um modelo de tag é um grupo de tags relacionadas que estão associadas a vários aspectos visuais das imagens que estão sendo marcadas. As tags estão relacionadas a aspectos visuais distintos das imagens, de modo que, quando aplicadas, as tags ajudem a procurar tipos específicos de imagens. Por exemplo, uma coleção de sapatos pode ter tags diferentes, mas todas as tags estão relacionadas a sapatos e podem pertencer ao mesmo modelo de tag. Quando aplicadas, as tags ajudam a encontrar diferentes tipos de sapatos, por exemplo, por design ou por uso. Para entender a representação de conteúdo de um modelo de treinamento em [!DNL Experience Manager], visualize um modelo de treinamento como uma entidade de nível superior constituída por um grupo de tags adicionadas manualmente e imagens de exemplo para cada tag. Cada tag pode ser aplicada exclusivamente a uma imagem.

Antes de criar um modelo de tag e treinar o serviço, identifique um conjunto de tags exclusivas que descrevam melhor os objetos nas imagens no contexto de sua empresa. Certifique-se de que os ativos em seu conjunto preparado estejam em conformidade com [as diretrizes de treinamento](#training-guidelines).

### Diretrizes de treinamento {#training-guidelines}

Certifique-se de que as imagens no conjunto de treinamento estejam em conformidade com as seguintes diretrizes:

**Quantidade e tamanho:** mínimo de 10 imagens e máximo de 50 imagens por tag.

**Coerência**: Verifique se as imagens de uma tag são visualmente semelhantes. É melhor adicionar as tags sobre os mesmos aspectos visuais (como o mesmo tipo de objetos em uma imagem) em um único modelo de tag. Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque elas não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/coherence.png)

**Cobertura**: As imagens da formação devem ser suficientemente variadas. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que [!DNL Experience Manager] aprenda a se concentrar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo. Por exemplo, para a tag *model-down*, inclua mais imagens de treinamento semelhantes à imagem realçada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/coverage_1.png)

**Desvio/obstrução**: O serviço se concentra melhor em imagens com menos distração (planos de fundo proeminentes, acompanhamento não relacionado, como objetos/pessoas com o assunto principal). Por exemplo, para a tag *casual-shoe*, a segunda imagem não é um bom candidato a treinamento.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. Por exemplo, para tags, como *capa de chuva* e *perfil de modelo*, adicione ambas as tags ao ativo elegível antes de incluí-lo para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/completeness.png)

**Número de tags**: O Adobe recomenda treinar um modelo usando pelo menos duas tags distintas e pelo menos dez imagens diferentes para cada tag. Em um único modelo de tag, não adicione mais de 50 tags.

**Número de exemplos**: Para cada tag, adicione pelo menos dez exemplos. No entanto, a Adobe recomenda cerca de 30 exemplos. Há suporte para no máximo 50 exemplos por tag.

**Evite falsos positivos e conflitos**: O Adobe recomenda criar um modelo de tag único para um único aspecto visual. Estruturar os modelos de tags de forma a evitar sobreposições de tags entre os modelos. Por exemplo, não use tags comuns como `sneakers` em dois nomes de modelos de tags diferentes `shoes` e `footwear`. O processo de treinamento substitui um modelo de tag treinado pelo outro para uma palavra-chave comum.

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
1. Na interface do usuário [!DNL Experience Manager], acesse **[!UICONTROL Ativos]** > **[!UICONTROL Treinamento de tags inteligentes]**.
1. Clique em **[!UICONTROL Criar]**. Forneça um **[!UICONTROL Título]**, **[!UICONTROL Descrição]**.
1. Navegue e selecione as tags nas tags existentes em `cq:tags` para as quais deseja treinar o modelo. Clique em **[!UICONTROL Avançar]**.
1. Na caixa de diálogo **[!UICONTROL Selecionar ativos]**, clique em **[!UICONTROL Adicionar ativos]** em relação a cada tag. Pesquise no repositório DAM ou navegue pelo repositório para selecionar pelo menos 10 e no máximo 50 imagens. Selecione ativos e não a pasta. Depois de selecionar as imagens, clique em **[!UICONTROL Selecionar]**.

   ![Exibir status de treinamento](assets/smart-tags-training-status.png)

1. Para visualizar as miniaturas das imagens selecionadas, clique na opção na frente de uma tag. Você pode modificar sua seleção clicando em **[!UICONTROL Adicionar ativos]**. Depois de satisfeito com a seleção, clique em **[!UICONTROL Enviar]**. A interface do usuário exibe uma notificação na parte inferior da página, indicando que o treinamento foi iniciado.
1. Verifique o status do treinamento na coluna **[!UICONTROL Status]** para cada modelo de tag. Os status possíveis são [!UICONTROL Pending], [!UICONTROL Trained] e [!UICONTROL Failed].

![Fluxo de trabalho para treinar o modelo de marcação para Tags inteligentes](assets/smart-tag-model-training-flow.png)

*Figura: Etapas do fluxo de trabalho de treinamento para treinar o modelo de marcação.*

### Exibir o status e o relatório do treinamento {#training-status}

Para verificar se o serviço de Tags inteligentes é treinado em suas tags no conjunto de ativos de treinamento, analise o relatório do fluxo de trabalho de treinamento no console Relatórios .

1. Na interface [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. Na página **[!UICONTROL Relatórios de ativos]**, clique em **[!UICONTROL Criar]**.
1. Selecione o relatório **[!UICONTROL Treinamento de Tags inteligentes]** e clique em **[!UICONTROL Avançar]** na barra de ferramentas.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Em seguida, clique em **[!UICONTROL Create]** na barra de ferramentas.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. Para exibir o relatório, clique em **[!UICONTROL Exibir]** na barra de ferramentas.
1. Revise os detalhes do relatório. O relatório exibe o status do treinamento das tags que você treinou. A cor verde na coluna **[!UICONTROL Status de treinamento]** indica que o serviço de Tags inteligentes é treinado para a tag. A cor amarela indica que o serviço é parcialmente treinado para uma tag específica. Para treinar o serviço completamente para uma tag, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento. Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para estas tags.Tags
1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Download]** na barra de ferramentas. O relatório é baixado como uma planilha.

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

Todos os tipos de ativos compatíveis são marcados automaticamente por [!DNL Experience Manager Assets] quando carregados. A marcação é ativada e funciona, por padrão. [!DNL Experience Manager] aplica as tags apropriadas em tempo quase real.  <!-- TBD: You can also apply the tagging workflow on-demand. The workflow applies to both, assets and folders. -->

* Para imagens e vídeos, as Tags inteligentes são baseadas em algum aspecto visual.

* Para ativos baseados em texto, a eficácia das Tags inteligentes não depende da quantidade de texto no ativo, mas das palavras-chave ou entidades relevantes presentes no texto do ativo. Para ativos baseados em texto, as Tags inteligentes são as palavras-chave que aparecem no texto, mas aquelas que melhor descrevem o ativo. Para ativos compatíveis, [!DNL Experience Manager] já extrai o texto, que é então indexado e usado para procurar os ativos. No entanto, as Tags inteligentes com base em palavras-chave no texto fornecem uma faceta de pesquisa dedicada, estruturada e de prioridade mais alta. O último ajuda a melhorar a descoberta de ativos em comparação com um índice de pesquisa.

## Gerenciar tags inteligentes e pesquisas de ativos {#manage-smart-tags-and-searches}

Você pode preparar tags inteligentes para remover quaisquer tags imprecisas que possam ter sido atribuídas aos ativos da sua marca, para que somente as tags mais relevantes sejam exibidas.

A moderação de tags inteligentes também ajuda a refinar pesquisas baseadas em tags para ativos, garantindo que seus ativos apareçam nos resultados da pesquisa para as tags mais relevantes. Essencialmente, ajuda a eliminar as chances de ativos não relacionados aparecerem nos resultados da pesquisa.

Também é possível atribuir uma classificação mais alta a uma tag para aumentar a relevância da tag para o ativo. A promoção de uma tag para um ativo aumenta as chances de o ativo aparecer nos resultados da pesquisa quando uma pesquisa é executada com base na tag específica.

Para moderar as tags inteligentes de seus ativos digitais:

1. No campo de pesquisa , procure por ativos digitais com base em uma tag .

1. Para identificar os ativos digitais que você não acha relevantes para sua pesquisa, inspecione os resultados da pesquisa.

1. Selecione um ativo e, em seguida, selecione ![o ícone Gerenciar tags](assets/do-not-localize/manage-tags-icon.png) na barra de ferramentas.

1. Na página **[!UICONTROL Gerenciar tags]**, inspecione as tags. Se você não quiser que o ativo seja pesquisado com base em uma tag específica, selecione a tag e selecione ![Delete icon](assets/do-not-localize/delete-icon.png) na barra de ferramentas. Como alternativa, selecione o símbolo `X` ao lado do rótulo.

1. Para atribuir uma classificação mais alta a uma tag, selecione a tag e selecione ![Ícone de promoção](assets/do-not-localize/promote-icon.png) na barra de ferramentas. A tag promovida é movida para a seção **[!UICONTROL Tags]**.

1. Selecione **[!UICONTROL Save]** e selecione **[!UICONTROL OK]** para fechar a caixa de diálogo [!UICONTROL Success].

1. Navegue até a página [!UICONTROL Propriedades] do ativo. Observe que a tag promovida tem uma relevância alta e, portanto, aparece mais alta nos resultados da pesquisa.

### Entender os resultados da pesquisa [!DNL Experience Manager] com tags inteligentes {#understand-search}

Por padrão, a pesquisa [!DNL Experience Manager] combina os termos de pesquisa com uma cláusula `AND`. O uso de tags inteligentes não altera esse comportamento padrão. O uso de tags inteligentes adiciona uma cláusula `OR` para localizar qualquer um dos termos de pesquisa nas tags inteligentes aplicadas. Por exemplo, considere pesquisar por `woman running`. Os ativos com apenas `woman` ou apenas `running` palavra-chave nos metadados não aparecem nos resultados da pesquisa por padrão. No entanto, um ativo marcado com `woman` ou `running` usando tags inteligentes aparece em tal query de pesquisa. Então os resultados da pesquisa são uma combinação de...

* Ativos com palavras-chave `woman` e `running` nos metadados.

* Ativos marcados com tags inteligentes com qualquer uma das palavras-chave.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. corresponde a `woman running` nos vários campos de metadados.
1. corresponde de `woman running` em tags inteligentes.
1. correspondências de `woman` ou de `running` em tags inteligentes.

## Limitações e práticas recomendadas relacionadas à marcação {#limitations}

A marcação inteligente aprimorada é baseada em modelos de aprendizagem de imagens e suas tags. Esses modelos nem sempre são perfeitos na identificação de tags. A versão atual das Tags inteligentes tem as seguintes limitações:

* Incapacidade de reconhecer sutis diferenças em imagens. Por exemplo, camisas de ajuste fino versus camisas de ajuste regular.
* Incapacidade de identificar tags com base em pequenos padrões ou partes de uma imagem. Por exemplo, logotipos em camisas.
* A marcação é suportada nos idiomas que [!DNL Experience Manager] suporta. Para obter uma lista de idiomas, consulte [Notas de versão do Serviço de conteúdo inteligente](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages).
* As tags que não são manipuladas estão relacionadas a:

   * Aspectos não visuais e abstratos. Por exemplo, o ano ou a estação de lançamento de um produto, estado de espírito ou emoção evocado por uma imagem e uma conotação subjetiva de um vídeo.
   * Diferenças visuais em produtos como camisas com e sem coleiras ou logotipos de produtos pequenos embutidos em produtos.

Para treinar o modelo, use as imagens mais apropriadas. O treinamento não pode ser revertido ou o modelo de treinamento não pode ser removido. A precisão da marcação depende do treinamento atual, portanto, faça isso com cuidado.

<!-- TBD: Add limitations related to text files. -->

Para pesquisar arquivos com tags inteligentes (regulares ou aprimoradas), use a pesquisa [!DNL Assets] (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!NOTE]
>
>A capacidade das Tags inteligentes de treinar em suas tags e aplicá-las em outras imagens depende da qualidade das imagens usadas no treinamento.
>Para obter melhores resultados, o Adobe recomenda o uso de imagens visualmente semelhantes para treinar o serviço para cada tag.

>[!MORELIKETHIS]
>
>* [Saiba como as tags inteligentes ajudam a gerenciar seus arquivos digitais](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [Usar tags inteligentes para vídeos](smart-tags-video-assets.md)

