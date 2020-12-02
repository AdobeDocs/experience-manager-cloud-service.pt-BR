---
title: Marcar imagens automaticamente com tags geradas por AI
description: Marque imagens usando serviços inteligentes artificialmente que aplicam tags comerciais contextuais e descritivas usando  [!DNL Adobe Sensei] serviços.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 80171c63e9f3ba9ace4fd948c7997f14a17ccddc
workflow-type: tm+mt
source-wordcount: '2432'
ht-degree: 6%

---


# Treinar o Smart Content Service e marcar automaticamente suas imagens {#train-service-tag-assets}

As organizações que lidam com ativos digitais cada vez mais usam vocabulário controlado por taxonomia em metadados de ativos. Basicamente, inclui uma lista de palavras-chave que os funcionários, parceiros e clientes normalmente usam para consultar e procurar seus ativos digitais. Marcar ativos com um vocabulário controlado por taxonomia garante que esses ativos possam ser facilmente identificados e recuperados por pesquisas baseadas em tags.

Comparado aos vocabulários de linguagem natural, a marcação baseada na taxonomia comercial ajuda a alinhar os ativos a uma empresa empresa e garante que os ativos mais relevantes sejam exibidos nas pesquisas. Por exemplo, um fabricante de carros pode marcar imagens de carros com nomes de modelos para que somente as imagens relevantes sejam exibidas quando pesquisadas para projetar uma campanha promocional.

Em segundo plano, as Tags inteligentes usam uma estrutura de inteligência artificial de [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para treinar seu algoritmo de reconhecimento de imagem na estrutura de tags e na taxonomia comercial. Essa inteligência de conteúdo é então usada para aplicar tags relevantes em um conjunto diferente de ativos.

<!-- TBD: Create a flowchart for how training works in CS.
![flowchart](assets/flowchart.gif) 
-->

Para usar a marcação inteligente, conclua as seguintes tarefas:

* [Integre o Experience Manager ao Console](#integrate-aem-with-aio) do desenvolvedor do Adobe.
* [Entenda os modelos de tags e as diretrizes](#understand-tag-models-guidelines).
* [Treinar o modelo](#train-model).
* [Marque seus ativos](#tag-assets) digitais.
* [Gerencie as tags e pesquisas](#manage-smart-tags-and-searches).

Tags inteligentes são aplicáveis somente para clientes [!DNL Adobe Experience Manager Assets]. As Tags inteligentes estão disponíveis para compra como um complemento para [!DNL Experience Manager].

<!-- TBD: Is there a link to buy SCS or initiate a sales call. How are AIO services sold? Provide a CTA here to buy or contacts Sales team. -->

## Integre [!DNL Experience Manager] ao Console do desenvolvedor do Adobe {#integrate-aem-with-aio}

>[!IMPORTANT]
>
>As novas implantações [!DNL Experience Manager Assets] são integradas com [!DNL Adobe Developer Console] por padrão. Ajuda a configurar a funcionalidade de tags inteligentes mais rapidamente. Nas implantações mais antigas, os administradores podem [configurar manualmente a integração de tags inteligentes](/help/assets/smart-tags-configuration.md#aio-integration).

Você pode integrar [!DNL Adobe Experience Manager] com as Tags inteligentes usando [!DNL Adobe Developer Console]. Use essa configuração para acessar o serviço de Tags inteligentes em [!DNL Experience Manager]. Consulte [configurar o Experience Manager para a marcação inteligente de ativos](smart-tags-configuration.md) para que o tarefa configure as Tags inteligentes. No back end, o servidor [!DNL Experience Manager] autentica suas credenciais de serviço com o gateway do Console do desenvolvedor do Adobe antes de encaminhar sua solicitação para o serviço de Tags inteligentes.

## Entender os modelos e diretrizes de tags {#understand-tag-models-guidelines}

Um modelo de tag é um grupo de tags relacionadas que são por um aspecto visual da imagem. Por exemplo, uma coleção de sapatos pode ter tags diferentes, mas todas elas estão relacionadas a sapatos e podem pertencer ao mesmo modelo de etiqueta. As tags podem se relacionar somente com os diferentes aspectos visuais das imagens. Para entender a representação de conteúdo de um modelo de treinamento em [!DNL Experience Manager], visualize um modelo de treinamento como uma entidade de nível superior composta por um grupo de tags adicionadas manualmente e imagens de exemplo para cada tag. Cada tag pode ser aplicada exclusivamente a uma imagem.

As tags que não podem ser tratadas realisticamente estão relacionadas a:

* Aspectos não visuais e abstratos, como o ano ou a estação de lançamento de um produto, o estado de espírito ou a emoção evocados por uma imagem.
* Diferenças visuais em produtos como camisas com e sem coleiras ou logotipos de pequenos produtos embutidos em produtos.

Antes de criar um modelo de tag e treinar o serviço, identifique um conjunto de tags exclusivas que descrevam melhor os objetos nas imagens no contexto de sua empresa. Certifique-se de que os ativos no conjunto preparado estejam em conformidade com [as diretrizes de treinamento](#training-guidelines).

### Diretrizes de treinamento {#training-guidelines}

As imagens em seu conjunto de treinamento devem estar em conformidade com as seguintes diretrizes:

**Quantidade e tamanho:** mínimo de 10 imagens e máximo de 50 imagens por tag.

**Coerência**: As imagens de uma tag devem ser visualmente semelhantes. É melhor adicionar as tags sobre os mesmos aspectos visuais (como o mesmo tipo de objetos em uma imagem) juntas em um único modelo de tag. Por exemplo, não é uma boa ideia marcar todas essas imagens como `my-party` (para treinamento) porque elas não são visualmente semelhantes.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](assets/do-not-localize/coherence.png)

**Cobertura**: Deve haver uma variedade suficiente de imagens no treinamento. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que AEM aprenda a focar-se nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo. Por exemplo, para a tag *model-down-pose*, inclua mais imagens de treinamento semelhantes à imagem realçada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](assets/do-not-localize/coverage_1.png)

**Desvio/obstrução**: O serviço treina melhor em imagens com menos distração (fundo proeminente, acompanhamento não relacionado, como objetos/pessoas com o assunto principal). Por exemplo, para a tag *casual-shoe*, a segunda imagem não é um bom candidato a treinamento.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](assets/do-not-localize/distraction.png)

**Integridade:** se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. Por exemplo, para tags, como *capa de chuva* e *perfil de modelo*, adicione ambas as tags ao ativo elegível antes de incluí-lo para treinamento.

![Imagens ilustrativas para exemplificar as diretrizes para treinamento](assets/do-not-localize/completeness.png)

**Número de tags**: O Adobe recomenda que você treine um modelo usando pelo menos duas tags distintas e pelo menos 10 imagens diferentes para cada tag. Em um único modelo de tag, não adicione mais de 50 tags.

**Número de exemplos**: Para cada tag, adicione pelo menos 10 exemplos. No entanto, a Adobe recomenda cerca de 30 exemplos. Há suporte para um máximo de 50 exemplos por tag.

**Evitar falsos positivos e conflitos**: O Adobe recomenda criar um modelo de tag único para um aspecto visual único. Estruturar os modelos de tags de forma a evitar sobreposições de tags entre os modelos. Por exemplo, não use tags comuns como `sneakers` em dois nomes de modelos de tags diferentes `shoes` e `footwear`. O processo de treinamento substitui um modelo de tag treinado pelo outro para uma palavra-chave comum.

**Exemplos**: Mais alguns exemplos para orientação são:

* Crie um modelo de tag que inclua,
   * apenas as etiquetas relacionadas com modelos de automóveis.
   * somente as marcas relacionadas às cores das camisas.
   * apenas as etiquetas relacionadas com casacos para mulheres e homens.
* Não criar,
   * um modelo de etiqueta que inclui modelos de carro lançados em 2019 e 2020.
   * vários modelos de tags que incluem os mesmos poucos modelos de carro.

**Imagens usadas para treinar**: Você pode usar as mesmas imagens para treinar diferentes modelos de tags. No entanto, o não associa uma imagem a mais de uma tag em um modelo de tag. Portanto, é possível marcar a mesma imagem com tags diferentes pertencentes a modelos de tags diferentes.

Não é possível desfazer o treinamento. As diretrizes acima devem ajudá-lo a escolher boas imagens para treinar.

## Treinar o modelo para suas tags personalizadas {#train-model}

Para criar e treinar um modelo para suas tags comerciais específicas, siga estas etapas:

1. Crie as tags necessárias e a estrutura de tags apropriada. Carregue as imagens relevantes no repositório do DAM.
1. Na interface do usuário [!DNL Experience Manager], acesse **[!UICONTROL Ativos]** > **[!UICONTROL Treinamento inteligente de tags]**.
1. Clique em **[!UICONTROL Criar]**. Forneça um **[!UICONTROL Título]**, **[!UICONTROL Descrição]**.
1. Procure e selecione as tags das tags existentes em `cq:tags` para as quais você deseja treinar o modelo. Clique em **[!UICONTROL Avançar]**.
1. Na caixa de diálogo **[!UICONTROL Selecionar ativos]**, clique em **[!UICONTROL Adicionar ativos]** em relação a cada tag. Pesquise no repositório do DAM ou navegue pelo repositório para selecionar pelo menos 10 e no máximo 50 imagens. Selecione os ativos e não a pasta. Depois de selecionar as imagens, clique em **[!UICONTROL Selecionar]**.
1. Para pré-visualização das miniaturas das imagens selecionadas, clique no acordeão na frente de uma tag . Você pode modificar sua seleção clicando em **[!UICONTROL Adicionar ativos]**. Depois de satisfeito com a seleção, clique em **[!UICONTROL Enviar]**. A interface do usuário exibe uma notificação na parte inferior da página, indicando que o treinamento foi iniciado.
1. Verifique o status do treinamento na coluna **[!UICONTROL Status]** para cada modelo de tag. Os possíveis status são [!UICONTROL Pendente], [!UICONTROL Treinado] e [!UICONTROL Falha].

![Fluxo de trabalho para o modelo de marcação para marcação inteligente](assets/smart-tag-model-training-flow.png)

*Figura: Etapas do fluxo de trabalho de treinamento para treinar o modelo de marcação.*

### Status e relatório de treinamento de visualização {#training-status}

Para verificar se o serviço de Tags inteligentes é treinado em suas tags no conjunto de ativos de treinamento, reveja o relatório de fluxo de trabalho de treinamento no console Relatórios.

1. Na interface [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas > Ativos > Relatórios]**.
1. Na página **[!UICONTROL Relatórios de ativos]**, clique em **[!UICONTROL Criar]**.
1. Selecione o relatório **[!UICONTROL Treinamento de tags inteligentes]** e clique em **[!UICONTROL Próximo]** na barra de ferramentas.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Em seguida, clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. Para visualização do relatório, clique em **[!UICONTROL Visualização]** na barra de ferramentas.
1. Revise os detalhes do relatório. O relatório exibe o status do treinamento das tags que você treinou. A cor verde na coluna **[!UICONTROL Status de treinamento]** indica que o serviço de Tags inteligentes é treinado para a tag . A cor amarela indica que o serviço não é completamente treinado para uma tag específica. Nesse caso, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento para treinar o serviço completamente na tag. Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para essas tags.Tags
1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Download]** na barra de ferramentas. O relatório é baixado como uma planilha do Microsoft Excel.

## Marcar ativos {#tag-assets}

Depois de ter treinado o serviço de Tags inteligentes, é possível acionar o fluxo de trabalho de marcação para aplicar automaticamente as tags apropriadas em um conjunto diferente de ativos semelhantes. Você pode aplicar o fluxo de trabalho de marcação periodicamente ou sempre que necessário. O fluxo de trabalho de marcação se aplica a ativos e pastas.

### Marcar ativos do console de fluxo de trabalho {#tagging-assets-from-the-workflow-console}

1. Na interface do Experience Manager, vá para **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]**.
1. Na página **[!UICONTROL Modelos de Fluxo de Trabalho]**, selecione o fluxo de trabalho **[!UICONTROL Ativos de Tags Inteligentes do DAM]** e clique em **[!UICONTROL Fluxo de Trabalho do Start]** na barra de ferramentas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Na caixa de diálogo **[!UICONTROL Executar Fluxo de Trabalho]**, navegue até a pasta de carga que contém ativos nos quais você deseja aplicar suas tags automaticamente.
1. Especifique um título para o fluxo de trabalho e um comentário opcional. Clique em **[!UICONTROL Executar]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Navegue até a pasta de ativos e reveja as tags para verificar se os ativos estão marcados corretamente. Para obter detalhes, consulte [gerenciar tags inteligentes](#manage-smart-tags-and-searches).

### Marcar ativos da linha do tempo {#tagging-assets-from-the-timeline}

1. Na interface do usuário Ativos, selecione a pasta que contém ativos ou ativos específicos aos quais você deseja aplicar tags inteligentes.
1. No canto superior esquerdo, abra a **[!UICONTROL Linha do tempo]**.
1. Abra as ações na parte inferior da barra lateral esquerda e clique em **[!UICONTROL Fluxo de trabalho do Start]**.

   ![start_workflow](assets/start_workflow.png)

1. Selecione o fluxo de trabalho **[!UICONTROL Ativos inteligentes de tags do DAM]** e especifique um título para o fluxo de trabalho.
1. Clique em **[!UICONTROL Start]**. O fluxo de trabalho aplica suas tags em ativos. Navegue até a pasta de ativos e reveja as tags para verificar se seus ativos estão marcados corretamente. Para obter detalhes, consulte [gerenciar tags inteligentes](#manage-smart-tags-and-searches).

>[!NOTE]
>
>Nos ciclos de marcação subsequentes, somente os ativos modificados são marcados novamente com tags treinadas recentemente.No entanto, mesmo ativos inalterados são marcados se a diferença entre os últimos e os atuais ciclos de marcação do fluxo de trabalho de marcação exceder 24 horas. Para workflows de marcação periódica, os ativos inalterados são marcados quando o intervalo de tempo excede 6 meses.

### Marcar ativos carregados {#tag-uploaded-assets}

O Experience Manager pode marcar automaticamente os ativos que os usuários carregam no DAM. Para fazer isso, os administradores configuram um fluxo de trabalho para adicionar uma etapa disponível de aos ativos de tags inteligentes. Consulte [como ativar a marcação inteligente para ativos carregados](/help/assets/smart-tags-configuration.md#enable-smart-tagging-for-uploaded-assets).

## Gerenciar tags inteligentes e pesquisas de ativos {#manage-smart-tags-and-searches}

É possível preparar tags inteligentes para remover tags imprecisas que possam ter sido atribuídas aos ativos da sua marca, para que somente as tags mais relevantes sejam exibidas.

A moderação de tags inteligentes também ajuda a refinar pesquisas baseadas em tags para ativos, garantindo que seus ativos sejam exibidos nos resultados da pesquisa para obter as tags mais relevantes. Essencialmente, ajuda a eliminar as chances de ativos não relacionados aparecerem nos resultados da pesquisa.

Você também pode atribuir uma classificação mais alta a uma tag para aumentar sua relevância em relação a um ativo. A promoção de uma tag para um ativo aumenta as chances de o ativo aparecer nos resultados da pesquisa quando uma pesquisa é realizada com base na tag específica.

Para moderar as tags inteligentes de seus ativos:

1. No campo Omnisearch, procure ativos com base em uma tag.

1. Inspect os resultados da pesquisa para identificar os ativos que você não considera relevantes para a sua pesquisa.

1. Selecione o ativo e, em seguida, ![ícone Gerenciar tags](assets/do-not-localize/manage-tags-icon.png) na barra de ferramentas.

1. Na página **[!UICONTROL Gerenciar tags]**, inspecione as tags. Se você não quiser que o ativo seja pesquisado com base em uma tag específica, selecione a tag e ![Ícone Excluir](assets/do-not-localize/delete-icon.png) na barra de ferramentas. Como alternativa, selecione o símbolo `X` ao lado do rótulo.

1. Para atribuir uma classificação superior a uma tag, selecione a tag e ![Ícone de promoção](assets/do-not-localize/promote-icon.png) na barra de ferramentas. A tag promovida é movida para a seção **[!UICONTROL Tags]**.

1. Selecione **[!UICONTROL Salvar]** e selecione **[!UICONTROL OK]** para fechar a caixa de diálogo [!UICONTROL Êxito].

1. Navegue até a página [!UICONTROL Propriedades] do ativo. Observe que a tag promovida tem uma relevância alta e, portanto, aparece mais alta nos resultados da pesquisa.

### Entenda AEM resultados de pesquisa com tags inteligentes {#understandsearch}

Por padrão, AEM pesquisa combina os termos de pesquisa com uma cláusula `AND`. O uso de tags inteligentes não altera esse comportamento padrão. O uso de tags inteligentes adiciona uma cláusula `OR` adicional para localizar qualquer um dos termos de pesquisa nas tags inteligentes aplicadas. Por exemplo, considere pesquisar por `woman running`. Os ativos com apenas `woman` ou apenas `running` palavra-chave nos metadados não aparecem nos resultados da pesquisa por padrão. No entanto, um ativo marcado com `woman` ou `running` usando tags inteligentes aparece em um query de pesquisa desse tipo. Então os resultados da pesquisa são uma combinação de...

* ativos com `woman` e `running` palavras-chave nos metadados.

* ativos marcados com inteligência com qualquer uma das palavras-chave.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos dos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. corresponde a `woman running` nos vários campos de metadados.
1. corresponde a `woman running` em tags inteligentes.
1. corresponde de `woman` ou de `running` em tags inteligentes.

### Limitações de marcação {#limitations}

Tags inteligentes aprimoradas são baseadas em modelos de aprendizado de imagens de marca e suas tags. Esses modelos nem sempre são perfeitos para identificar tags. A versão atual das Tags inteligentes tem as seguintes limitações:

* Incapacidade de reconhecer diferenças sutis nas imagens. Por exemplo, camisas finas versus camisetas comuns.
* Incapacidade de identificar tags com base em pequenos padrões/partes de uma imagem. Por exemplo, logotipos em camisetas.
* A marcação é suportada nos idiomas suportados pelo Experience Manager. Para obter uma lista de idiomas, consulte [Notas de versão do Smart Content Service](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html#languages).

Para pesquisar ativos com tags inteligentes (regulares ou aprimoradas), use o Assets Omnisearch (pesquisa de texto completo). Não há predicado de pesquisa separado para tags inteligentes.

>[!NOTE]
>
>A capacidade das Tags inteligentes de treinar em suas tags e aplicá-las em outras imagens depende da qualidade das imagens usadas para treinamento.
>Para obter melhores resultados, o Adobe recomenda usar imagens visualmente semelhantes para treinar o serviço de cada tag.

>[!MORELIKETHIS]
>
>* [Configurar Experience Manager para marcação inteligente](smart-tags-configuration.md)
>* [Saiba como as tags inteligentes ajudam a gerenciar ativos](https://medium.com/adobetech/efficient-asset-management-with-enhanced-smart-tags-887bd47dbb3f)
>* [Marcação inteligente de ativos de vídeo](smart-tags-video-assets.md)

