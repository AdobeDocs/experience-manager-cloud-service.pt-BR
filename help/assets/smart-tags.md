---
title: Marcar ativos automaticamente com o  [!DNL Adobe Sensei] serviço inteligente
description: Marque ativos com um serviço artificialmente inteligente que aplica tags comerciais contextuais e descritivas.
contentOwner: AG
feature: Tags inteligentes,Marcação
role: Administrator,Business Practitioner
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
translation-type: tm+mt
source-git-commit: 87d7cbb4463235a835d18fce49d06315a7c87526
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 6%

---


# Adicionar tags inteligentes aos ativos para melhorar a experiência de pesquisa {#smart-tag-assets-for-faster-search}

As organizações que lidam com ativos digitais cada vez mais usam um vocabulário controlado por taxonomia em metadados de ativos. Basicamente, inclui uma lista de palavras-chave que funcionários, parceiros e clientes costumam usar para consultar e pesquisar seus ativos digitais. Marcar ativos com um vocabulário controlado por taxonomia garante que os ativos possam ser facilmente identificados e recuperados em pesquisas.

Comparado aos vocabulários de linguagem natural, a marcação baseada na taxonomia comercial ajuda a alinhar os ativos aos negócios de uma empresa e garante que os ativos mais relevantes apareçam em pesquisas. Por exemplo, um fabricante de carros pode marcar imagens de carros com nomes de modelo para que somente imagens relevantes sejam exibidas quando pesquisadas para projetar uma campanha promocional.

Em segundo plano, a funcionalidade usa a estrutura artificialmente inteligente de [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para treinar seu algoritmo de reconhecimento de imagem em sua estrutura de tags e taxonomia comercial. Essa inteligência de conteúdo é então usada para aplicar tags relevantes em um conjunto diferente de ativos. As novas implantações [!DNL Experience Manager Assets] são integradas a [!DNL Adobe Developer Console] por padrão. Ajuda a configurar a funcionalidade de tags inteligentes com mais rapidez. Nas implantações mais antigas, os administradores podem [configurar manualmente a integração de tags inteligentes](/help/assets/smart-tags-configuration.md#aio-integration).

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

## Tipos de ativos compatíveis {#smart-tags-supported-file-formats}

Você pode adicionar tags aos seguintes tipos de ativos:

* **Imagens**: As imagens em muitos formatos são marcadas usando os serviços de conteúdo inteligente da Adobe Sensei. Você [cria um modelo de treinamento](#train-model) e então [aplica tags inteligentes](#tag-assets) a imagens. As Tags inteligentes são aplicadas aos tipos de arquivo compatíveis que geram renderizações no formato JPG e PNG.
* **Ativos** baseados em texto:  [!DNL Experience Manager Assets] adiciona tags automaticamente aos ativos com base em texto compatíveis quando carregados. Saiba mais sobre como [marcar ativos baseados em texto](#smart-tag-text-based-assets).
* **Ativos** de vídeo: A marcação de vídeo é ativada por padrão no  [!DNL Adobe Experience Manager] as a  [!DNL Cloud Service]. [Os vídeos são ](/help/assets/smart-tags-video-assets.md) marcados automaticamente ao fazer upload de novos vídeos ou reprocessar os existentes.

| Imagens (tipos MIME) | Ativos baseados em texto (formatos de arquivo) | Ativos de vídeo (formatos de arquivo e codecs) |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC, Motion JPEG) |
| image/bmp | HTML | AVI (índeo4) |
| image/gif | JSON  | FLV (H264/AVC, vp6f) |
| image/pjpeg | PDF | WMV (WMV2) |
| image/x-portable-anymap | PPT |  |
| image/x-portable-bitmap | PPTX |  |
| image/x-portable-graymap | RTF |  |
| imagem/x-portable-pixmap | SRT |  |
| image/x-rgb | TXT |  |
| image/x-xbitmap | VTT |  |
| image/x-xpixmap | XML |  |
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

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? Provide a CTA here to buy or contacts Sales team. -->

## Marcação de ativos baseados em texto com Tags inteligentes {#smart-tag-text-based-assets}

Os ativos baseados em texto são marcados automaticamente por [!DNL Experience Manager Assets] quando carregados. Está ativada por padrão. A eficácia das Tags inteligentes não depende da quantidade de texto no ativo, mas das palavras-chave ou entidades relevantes presentes no texto do ativo. Para ativos baseados em texto, as Tags inteligentes são as palavras-chave que aparecem no texto, mas aquelas que melhor descrevem o ativo. Para ativos compatíveis, [!DNL Experience Manager] já extrai o texto, que é então indexado e usado para procurar os ativos. No entanto, as Tags inteligentes com base em palavras-chave no texto fornecem uma faceta de pesquisa dedicada, estruturada e de prioridade mais alta usada para melhorar a descoberta de ativos em comparação com o índice de pesquisa completo.

Em comparação, para imagens e vídeos, as Tags inteligentes são derivadas de algum aspecto visual.

## Entender modelos e diretrizes de tags {#understand-tag-models-guidelines}

Um modelo de tag é um grupo de tags relacionadas que estão associadas a vários aspectos visuais das imagens que estão sendo marcadas. As tags estão relacionadas a aspectos visuais distintos das imagens, de modo que, quando aplicadas, as tags ajudem a procurar tipos específicos de imagens. Por exemplo, uma coleção de sapatos pode ter tags diferentes, mas todas as tags estão relacionadas a sapatos e podem pertencer ao mesmo modelo de tag. Quando aplicadas, as tags ajudam a encontrar diferentes tipos de sapatos, por exemplo, por cor, por design ou por uso. Para entender a representação de conteúdo de um modelo de treinamento em [!DNL Experience Manager], visualize um modelo de treinamento como uma entidade de nível superior constituída por um grupo de tags adicionadas manualmente e imagens de exemplo para cada tag. Cada tag pode ser aplicada exclusivamente a uma imagem.

Antes de criar um modelo de tag e treinar o serviço, identifique um conjunto de tags exclusivas que descrevam melhor os objetos nas imagens no contexto de sua empresa. Certifique-se de que os ativos em seu conjunto preparado estejam em conformidade com [as diretrizes de treinamento](#training-guidelines).

### Diretrizes de treinamento {#training-guidelines}

Certifique-se de que as imagens no conjunto de treinamento estejam em conformidade com as seguintes diretrizes:

**Quantidade e tamanho:** mínimo de 10 imagens e máximo de 50 imagens por tag.

**Coerência**: Verifique se as imagens de uma tag são visualmente semelhantes. É melhor adicionar as tags sobre os mesmos aspectos visuais (como o mesmo tipo de objetos em uma imagem) em um único modelo de tag. Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque elas não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/coherence.png)

**Cobertura**: As imagens da formação devem ser suficientemente variadas. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que AEM aprenda a se concentrar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo. Por exemplo, para a tag *model-down*, inclua mais imagens de treinamento semelhantes à imagem realçada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/coverage_1.png)

**Desvio/obstrução**: O serviço se concentra melhor em imagens com menos distração (planos de fundo proeminentes, acompanhamento não relacionado, como objetos/pessoas com o assunto principal). Por exemplo, para a tag *casual-shoe*, a segunda imagem não é um bom candidato a treinamento.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. Por exemplo, para tags, como *capa de chuva* e *perfil de modelo*, adicione ambas as tags ao ativo elegível antes de incluí-lo para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes de treinamento](assets/do-not-localize/completeness.png)

**Número de tags**: O Adobe recomenda treinar um modelo usando pelo menos duas tags distintas e pelo menos dez imagens diferentes para cada tag. Em um único modelo de tag, não adicione mais de 50 tags.

**Número de exemplos**: Para cada tag, adicione pelo menos dez exemplos. No entanto, a Adobe recomenda cerca de 30 exemplos. Há suporte para no máximo 50 exemplos por tag.

**Evite falsos positivos e conflitos**: O Adobe recomenda criar um modelo de tag único para um único aspecto visual. Estruturar os modelos de tags de forma a evitar sobreposições de tags entre os modelos. Por exemplo, não use tags comuns como `sneakers` em dois nomes de modelos de tags diferentes `shoes` e `footwear`. O processo de treinamento substitui um modelo de tag treinado pelo outro para uma palavra-chave comum.

**Exemplos**: Mais alguns exemplos para orientação são:

* Crie um modelo de tag que inclua,
   * apenas as etiquetas relacionadas com modelos de automóveis.
   * apenas as marcas relacionadas às cores das camisas.
   * apenas as etiquetas relacionadas com coletes para mulheres e homens.
* Não criar,
   * um modelo de etiquetas que inclui modelos de automóveis lançados em 2019 e 2020.
   * vários modelos de tags que incluem os mesmos modelos de carro.

**Imagens usadas para treinar**: Você pode usar as mesmas imagens para treinar diferentes modelos de tags. No entanto, não associe uma imagem a mais de uma tag em um modelo de tag. É possível marcar a mesma imagem com tags diferentes pertencentes a modelos de tags diferentes.

Não é possível desfazer o treinamento. As diretrizes acima devem ajudá-lo a escolher boas imagens para treinar.

## Treine o modelo para suas tags personalizadas {#train-model}

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

### Exibir o status e o relatório de treinamento {#training-status}

Para verificar se o serviço de Tags inteligentes é treinado em suas tags no conjunto de ativos de treinamento, analise o relatório do fluxo de trabalho de treinamento no console Relatórios .

1. Na interface [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. Na página **[!UICONTROL Relatórios de ativos]**, clique em **[!UICONTROL Criar]**.
1. Selecione o relatório **[!UICONTROL Treinamento de Tags inteligentes]** e clique em **[!UICONTROL Avançar]** na barra de ferramentas.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Em seguida, clique em **[!UICONTROL Create]** na barra de ferramentas.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. Para exibir o relatório, clique em **[!UICONTROL Exibir]** na barra de ferramentas.
1. Revise os detalhes do relatório. O relatório exibe o status do treinamento das tags que você treinou. A cor verde na coluna **[!UICONTROL Status de treinamento]** indica que o serviço de Tags inteligentes é treinado para a tag. A cor amarela indica que o serviço não é completamente treinado para uma tag específica. Nesse caso, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento para treinar o serviço completamente na tag. Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para estas tags.Tags
1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Download]** na barra de ferramentas. O relatório é baixado como uma planilha [!DNL Microsoft Excel].

## Marcar ativos {#tag-assets}

Depois de ter treinado o serviço de Tags inteligentes, você pode acionar o fluxo de trabalho de marcação para aplicar tags automaticamente em um conjunto diferente de ativos. Você pode aplicar o workflow de marcação sob demanda ou agendá-lo para execução periódica. O fluxo de trabalho de marcação se aplica a ativos e pastas.

### Marque ativos no console do fluxo de trabalho {#tagging-assets-from-the-workflow-console}

1. Na interface [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o fluxo de trabalho **[!UICONTROL Ativos de tags inteligentes do DAM]** e clique em **[!UICONTROL Iniciar fluxo de trabalho]** na barra de ferramentas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Na caixa de diálogo **[!UICONTROL Executar fluxo de trabalho]**, navegue até a pasta de carga que contém ativos nos quais você deseja aplicar suas tags automaticamente.
1. Especifique um título para o fluxo de trabalho e um comentário opcional. Clique em **[!UICONTROL Executar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   *Figura: Navegue até a pasta de ativos e revise as tags para verificar se os ativos estão marcados corretamente. Para obter detalhes, consulte [gerenciar tags inteligentes](#manage-smart-tags-and-searches).*

### Marque ativos na linha do tempo {#tagging-assets-from-the-timeline}

1. Na interface do usuário [!DNL Assets], selecione a pasta que contém ativos ou ativos específicos aos quais deseja aplicar tags inteligentes.
1. No canto superior esquerdo, abra a **[!UICONTROL Linha do tempo]**.
1. Abra as ações na parte inferior da barra lateral esquerda e clique em **[!UICONTROL Iniciar fluxo de trabalho]**.

   ![start_workflow](assets/start_workflow.png)

1. Selecione o fluxo de trabalho **[!UICONTROL Ativos de tags inteligentes do DAM]** e especifique um título para o fluxo de trabalho.
1. Clique em **[!UICONTROL Iniciar]**. O fluxo de trabalho aplica suas tags em ativos. Navegue até a pasta de ativos e revise as tags para verificar se os ativos estão marcados corretamente. Para obter detalhes, consulte [gerenciar tags inteligentes](#manage-smart-tags-and-searches).

>[!NOTE]
>
>Nos ciclos de marcação subsequentes, somente os ativos modificados são marcados novamente com tags recém-treinadas. No entanto, mesmo ativos inalterados são marcados se a diferença entre os últimos e os atuais ciclos de marcação do fluxo de trabalho de marcação exceder 24 horas. Para workflows de marcação periódica, os ativos inalterados são marcados quando o intervalo de tempo excede seis meses.

### Marcar ativos carregados {#tag-uploaded-assets}

[!DNL Experience Manager] O pode marcar automaticamente os ativos que os usuários fazem upload para o DAM. Para fazer isso, os administradores configuram um fluxo de trabalho para adicionar uma etapa disponível que marca ativos. Consulte [como ativar as Tags inteligentes para ativos carregados](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).

## Gerenciar tags inteligentes e pesquisas de ativos {#manage-smart-tags-and-searches}

Você pode preparar tags inteligentes para remover quaisquer tags imprecisas que possam ter sido atribuídas aos ativos da sua marca, para que somente as tags mais relevantes sejam exibidas.

A moderação de tags inteligentes também ajuda a refinar pesquisas baseadas em tags para ativos, garantindo que seus ativos apareçam nos resultados da pesquisa para as tags mais relevantes. Essencialmente, ajuda a eliminar as chances de ativos não relacionados aparecerem nos resultados da pesquisa.

Também é possível atribuir uma classificação mais alta a uma tag para aumentar a relevância da tag para o ativo. A promoção de uma tag para um ativo aumenta as chances de o ativo aparecer nos resultados da pesquisa quando uma pesquisa é executada com base na tag específica.

Para moderar as tags inteligentes de seus ativos:

1. No campo de pesquisa , procure por ativos com base em uma tag .

1. Inspect os resultados da pesquisa para identificar os ativos que você não considera relevantes para a sua pesquisa.

1. Selecione o ativo e, em seguida, selecione ![o ícone Gerenciar tags](assets/do-not-localize/manage-tags-icon.png) na barra de ferramentas.

1. Na página **[!UICONTROL Gerenciar tags]**, inspecione as tags. Se você não quiser que o ativo seja pesquisado com base em uma tag específica, selecione a tag e selecione ![Delete icon](assets/do-not-localize/delete-icon.png) na barra de ferramentas. Como alternativa, selecione o símbolo `X` ao lado do rótulo.

1. Para atribuir uma classificação mais alta a uma tag, selecione a tag e selecione ![Ícone de promoção](assets/do-not-localize/promote-icon.png) na barra de ferramentas. A tag promovida é movida para a seção **[!UICONTROL Tags]**.

1. Selecione **[!UICONTROL Save]** e selecione **[!UICONTROL OK]** para fechar a caixa de diálogo [!UICONTROL Success].

1. Navegue até a página [!UICONTROL Propriedades] do ativo. Observe que a tag promovida tem uma relevância alta e, portanto, aparece mais alta nos resultados da pesquisa.

### Entender AEM resultados de pesquisa com tags inteligentes {#understand-search}

Por padrão, AEM pesquisa combina os termos de pesquisa com uma cláusula `AND`. O uso de tags inteligentes não altera esse comportamento padrão. O uso de tags inteligentes adiciona uma cláusula `OR` para localizar qualquer um dos termos de pesquisa nas tags inteligentes aplicadas. Por exemplo, considere pesquisar por `woman running`. Os ativos com apenas `woman` ou apenas `running` palavra-chave nos metadados não aparecem nos resultados da pesquisa por padrão. No entanto, um ativo marcado com `woman` ou `running` usando tags inteligentes aparece em tal query de pesquisa. Então os resultados da pesquisa são uma combinação de...

* ativos com `woman` e `running` palavras-chave nos metadados.

* ativos marcados com tags inteligentes com uma das palavras-chave.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. corresponde a `woman running` nos vários campos de metadados.
1. corresponde de `woman running` em tags inteligentes.
1. correspondências de `woman` ou de `running` em tags inteligentes.

## Limitações de marcação e práticas recomendadas {#limitations}

A marcação inteligente aprimorada é baseada em modelos de aprendizagem de imagens e suas tags. Esses modelos nem sempre são perfeitos na identificação de tags. A versão atual das Tags inteligentes tem as seguintes limitações:

* Incapacidade de reconhecer sutis diferenças em imagens. Por exemplo, camisas finas versus camisas fixas regulares.
* Incapacidade de identificar tags com base em pequenos padrões/partes de uma imagem. Por exemplo, logotipos em T-shirts.
* A marcação é suportada nos idiomas que [!DNL Experience Manager] suporta. Para obter uma lista de idiomas, consulte [Notas de versão do Serviço de conteúdo inteligente](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages).
* Tags que não são tratadas realisticamente estão relacionadas a:

   * Aspectos não visuais e abstratos. Por exemplo, o ano ou a estação de lançamento de um produto, o estado de espírito ou a emoção evocados por uma imagem, a conotação subjetiva de um vídeo e assim por diante.
   * Diferenças visuais em produtos como camisas com e sem coleiras ou logotipos de produtos pequenos embutidos em produtos.

<!-- TBD: Add limitations related to text-based assets. -->

Para pesquisar ativos com tags inteligentes (regulares ou aprimoradas), use a pesquisa [!DNL Assets] (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!NOTE]
>
>A capacidade das Tags inteligentes de treinar em suas tags e aplicá-las em outras imagens depende da qualidade das imagens usadas no treinamento.
>Para obter melhores resultados, o Adobe recomenda o uso de imagens visualmente semelhantes para treinar o serviço para cada tag.

>[!MORELIKETHIS]
>
>* [ [!DNL Experience Manager] Configurar para marcação inteligente](smart-tags-configuration.md)
>* [Saiba como as tags inteligentes ajudam a gerenciar ativos](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [Marcação inteligente de ativos de vídeo](smart-tags-video-assets.md)

