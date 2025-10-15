---
title: 'Adicionar marcas automáticas a ativos com o serviço inteligente  [!DNL Adobe Sensei] '
description: Adicione tags a ativos com um serviço artificialmente inteligente que aplica tags comerciais contextuais e descritivas.
feature: Smart Tags,Tagging
role: Admin,User
source-git-commit: a579e2e25ecff93f6f1487ec0bcd317df09751cf
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 5%

---


# Treinamento de tags inteligentes

O treinamento de tags inteligentes permite treinar suas tags para especificar os detalhes se as tags relevantes não estiverem lá. Ele usa uma estrutura artificialmente inteligente do [Adobe Sensei](https://business.adobe.com/br/why-adobe/experience-cloud-artificial-intelligence.html) para treinar o algoritmo de reconhecimento de imagem de acordo com sua estrutura de tags e sua taxonomia comercial. Essa inteligência de conteúdo é usada para aplicar tags relevantes em um conjunto diferente de ativos. O [!DNL Experience Manager Assets] aplica tags inteligentes automaticamente a ativos carregados, por padrão.

## Determinar o requisito do treinamento de tags inteligentes {#smart-tag-training-requirement}

O treinamento de tags inteligentes é necessário nos seguintes cenários:

* Para adicionar um seletor automatizado para salvar iterações de adição de rótulos sempre que você fizer upload do mesmo ativo.
* Para melhorar a capacidade dos ativos de aplicar tags relevantes.
* Para aumentar a precisão das tags que aparecem em um ativo.
* Para adicionar rótulos indisponíveis ou ausentes.


>[!NOTE]
>
>O treinamento de tags inteligentes é aplicável somente em um ***tipo de imagem*** do ativo.

## Etapas envolvidas no treinamento de tags inteligentes

[!DNL Experience Manager] como [!DNL Cloud Service] gera automaticamente as Tags inteligentes para os ativos baseados em texto e para vídeos por padrão. Para treinar tags inteligentes para imagens, conclua as seguintes tarefas:

* [Entender modelos e diretrizes de tags](#understand-tag-models-guidelines)
* [Treinar o modelo](#train-model)
* [Marque seus ativos digitais](#tag-assets)
* [Gerenciar tags e pesquisas](#manage-smart-tags-and-searches)

## Entender modelos e diretrizes de tags {#understand-tag-models-guidelines}

Um modelo de tag é um grupo de tags relacionadas associadas a vários aspectos visuais das imagens que estão sendo marcadas. As tags estão relacionadas a aspectos visuais distintamente diferentes de imagens, de modo que, quando aplicadas, as tags ajudam a pesquisar tipos específicos de imagens. Por exemplo, uma coleção de sapatos pode ter tags diferentes, mas todas as tags estão relacionadas a sapatos e podem pertencer ao mesmo modelo de tag. Quando aplicadas, as tags ajudam a encontrar diferentes tipos de sapatos, por exemplo, por design ou uso.

Antes de criar um modelo de tag e treinar o serviço, identifique um conjunto de tags exclusivas que descrevam melhor os objetos nas imagens no contexto de sua empresa. Verifique se os ativos do conjunto preparado confirmam as [diretrizes de treinamento](#training-guidelines).

### Diretrizes de treinamento {#training-guidelines}

Verifique se as imagens no conjunto de treinamento estão em conformidade com as seguintes diretrizes:

<table>
   <tr>
      <th> Métricas </th>
      <th> Descrição </th>
   </tr>
   <tr>
      <td> <b>Quantidade e tamanho </b></td>
      <td> Mínimo de 10 e máximo de 50 imagens por tag. </td>
   </tr>
   <tr>
      <td> <b>Coerência</b> </td>
      <td> Verifique se as imagens de uma tag são visualmente semelhantes. É melhor adicionar tags sobre os mesmos aspectos visuais (como o mesmo tipo de objetos em uma imagem) em um único modelo de tag. Por exemplo, não é uma boa ideia marcar todas essas imagens como <i>my-party</i> (para treinamento) porque elas não são visualmente semelhantes. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/coherence.png"><br><i>Figura: imagens ilustrativas de coerência para exemplificar as diretrizes de treinamento</i>
      </td>
   </tr>
   <tr>
      <td> <b>Cobertura</b></td>
      <td> Deve haver variedade suficiente nas imagens no treinamento. A ideia é fornecer alguns exemplos, mas razoavelmente diversos, para que o aprenda a focar nas coisas certas. Se você estiver aplicando a mesma tag em imagens visualmente diferentes, inclua pelo menos cinco exemplos de cada tipo. Por exemplo, para a tag <i>model-down-pose</i>, inclua mais imagens de treinamento semelhantes à imagem destacada abaixo para que o serviço identifique imagens semelhantes com mais precisão durante a marcação.</td>
   </tr>
   <tr>
   <td colspan="2"> <img src="assets/do-not-localize/coverage_1.png"><br><i>Figura: imagens ilustrativas da cobertura para exemplificar as diretrizes de treinamento</i>
   </td>
   </tr>
   <tr>
      <td><b>Distração/obstrução</b> </td>
      <td> O serviço treina melhor em imagens com menos distração (fundo proeminente, acompanhamento não relacionado, como objetos/pessoas com o assunto principal). Por exemplo, para a tag <i>casual-shoes</i>, a segunda imagem não é um bom candidato para treinamento. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/distraction.png"><br><i>Figura: imagens ilustrativas de Distração/obstrução para exemplificar as diretrizes de treinamento</i>
      </td>
   </tr>
   <tr>
      <td> <b>Integridade</b> </td>
      <td> Se uma imagem se qualificar para mais de uma tag, adicione todas as tags aplicáveis antes de incluir a imagem para treinamento. Por exemplo, para tags, como <i>capa de chuva</i> e <i>perfil de modelo</i>, adicione ambas as tags ao ativo elegível antes de incluí-lo para treinamento. </td>
   </tr>
   <tr>
      <td colspan="2"> <img src="assets/do-not-localize/completeness.png"><br><i>Figura: imagens ilustrativas da integridade para exemplificar as diretrizes de treinamento</i>
      </td>
   </tr>
   <tr>
      <td> <b>Número de marcas</b> </td>
      <td> A Adobe recomenda que você treine um modelo usando pelo menos duas tags distintas e pelo menos dez imagens diferentes para cada tag. Em um modelo de tag única, não adicione mais de 50 tags. </td>
   </tr>
   <tr>
      <td> <b>Número de exemplos</b> </td>
      <td> Para cada tag, adicione pelo menos dez exemplos. No entanto, a Adobe recomenda cerca de 30 exemplos. Há suporte para no máximo 50 exemplos por tag. </td>
   </tr>
   <tr>
      <td> <b>Impedir falsos positivos e conflitos</b> </td>
      <td> A Adobe recomenda criar um modelo de tag única para um único aspecto visual. Estruturar os modelos de tags de forma a evitar a sobreposição de tags entre os modelos. Por exemplo, não use tags comuns como <i>tênis</i> em dois modelos de tag diferentes chamados <i>sapatos</i> e <i>calçados</i>. O processo de treinamento substitui um modelo de tag treinado pelo outro para uma palavra-chave comum. </td>
   </tr>
</table>

**Exemplos**: mais alguns exemplos para orientação:

* Crie um modelo de tag que inclua apenas,

   * As tags relacionadas aos modelos de carro.
   * As tags relacionadas a jaquetas para adultos e crianças.

* Não criar,

   * Um modelo de etiqueta que inclui modelos de carros lançados em 2019 e 2020.
   * Vários modelos de tag que incluem os mesmos poucos modelos de carro.

>[!NOTE]
>
>É possível usar as mesmas imagens para treinar modelos de tags diferentes. No entanto, não associe uma imagem a mais de uma tag em um modelo de tag. É possível marcar a mesma imagem com tags diferentes pertencentes a modelos de tags diferentes.
>&#x200B;>Não é possível desfazer o treinamento. As diretrizes acima devem ajudá-lo a escolher boas imagens para treinar.

## Treine o modelo para suas tags personalizadas {#train-model}

Para criar e treinar um modelo para suas tags específicas de negócios, siga estas etapas:

1. Crie as tags necessárias e a estrutura de tags apropriada. Faça upload das imagens relevantes no repositório DAM.
1. Na interface de usuário do [!DNL Experience Manager Cloud Service], acesse o **[!UICONTROL Assets]** > **[!UICONTROL Treinamento de Marca Inteligente]**.
1. Clique em **[!UICONTROL Criar]**. Forneça um **[!UICONTROL Título]**, **[!UICONTROL Descrição]**.
1. Clique no ícone de pasta no campo **[!UICONTROL Marcas]**. Uma janela pop-up é aberta.
1. Pesquise ou selecione as marcas apropriadas nas marcas existentes em `cq-tags` que você deseja adicionar ao modelo. Clique em **[!UICONTROL Avançar]**.

   >[!NOTE]
   >
   >Você pode classificar a estrutura de marcas em ordem crescente ou decrescente com base na data **[!UICONTROL Nome]** (ordem alfabética), **[!UICONTROL Criada]** ou **[!UICONTROL Modificada]**.


1. Na caixa de diálogo **[!UICONTROL Selecionar Assets]**, clique em **[!UICONTROL Adicionar Assets]** para cada marca. Pesquise no repositório DAM ou navegue pelo repositório para selecionar pelo menos 10 e no máximo 50 imagens. Selecione ativos, e não a pasta. Após selecionar as imagens, clique em **[!UICONTROL Selecionar]**.

   ![Exibir status do treinamento](assets/smart-tags-training-status.png)

1. Para visualizar as miniaturas das imagens selecionadas, clique no acordeão na frente de uma tag. Você pode modificar sua seleção clicando em **[!UICONTROL Adicionar Assets]**. Depois de satisfeito com a seleção, clique em **[!UICONTROL Enviar]**. A interface do usuário exibe uma notificação na parte inferior da página indicando que o treinamento foi iniciado.
1. Verifique o status do treinamento na coluna **[!UICONTROL Status]** para cada modelo de marca. Os status possíveis são [!UICONTROL Pendente], [!UICONTROL Treinado] e [!UICONTROL Falha].

![Fluxo de trabalho para treinar o modelo de marcação para Tags Inteligentes](assets/smart-tag-model-training-flow.png)

*Figura: etapas do fluxo de trabalho de treinamento para treinar o modelo de marcação.*

### Exibir status e relatório do treinamento {#training-status}

Para verificar se o serviço de Tags inteligentes é treinado em suas tags no conjunto de ativos de treinamento, revise o relatório de fluxo de trabalho de treinamento no console Relatórios.

1. Na interface do [!DNL Experience Manager Cloud Service], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Relatórios]**.
1. Na página **[!UICONTROL Relatórios de ativos]**, clique em **[!UICONTROL Criar]**.
1. Selecione o relatório **[!UICONTROL Treinamento de Tags Inteligentes]** e clique em **[!UICONTROL Avançar]** na barra de ferramentas.
1. Especifique um título e uma descrição para o relatório. Em **[!UICONTROL Agendar relatório]**, deixe a opção **[!UICONTROL Agora]** selecionada. Se desejar agendar o relatório para posteriormente, selecione **[!UICONTROL Posteriormente]** e especifique uma data e hora. Em seguida, clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Relatórios de ativos]**, selecione o relatório gerado. Para exibir o relatório, clique em **[!UICONTROL Exibir]** na barra de ferramentas.
1. Revise os detalhes do relatório. O relatório exibe o status do treinamento das tags que você treinou. A cor verde na coluna **[!UICONTROL Status do treinamento]** indica que o serviço de Tags inteligentes foi treinado para a tag. A cor amarela indica que o serviço foi parcialmente treinado para uma tag específica. Para treinar o serviço completamente para uma tag, adicione mais imagens com a tag específica e execute o fluxo de trabalho de treinamento. Se você não vir suas tags neste relatório, execute o fluxo de trabalho de treinamento novamente para essas tags.Tags
1. Para baixar o relatório, selecione-o na lista e clique em **[!UICONTROL Baixar]** na barra de ferramentas. O relatório é baixado como uma planilha.

>[!NOTE]
>
>E se eu desejar transferir o treinamento de Tags inteligentes de uma instância para outra por meio de uma exportação?
>&#x200B;>Não é necessário exportar o treinamento de Tags inteligentes se o ambiente pertencer à mesma Organização IMS. Ele é compartilhado automaticamente. Se o ambiente estiver entre organizações IMS, não há como compartilhar ou exportar o treinamento de Tags inteligentes.

## Limitações e práticas recomendadas relacionadas às tags inteligentes {#limitations-smart-tags-training}

* Para treinar o modelo, use as imagens mais apropriadas. O treinamento não pode ser revertido ou o modelo de treinamento não pode ser removido. A precisão da marcação depende do treinamento atual, portanto, faça isso com cuidado.
* Não é possível treinar o serviço que aplica Tags inteligentes a vídeos usando vídeos específicos. Funciona com as configurações padrão [!DNL Adobe Sensei].


>[!NOTE]
>
>A capacidade das Tags inteligentes de treinar em suas tags e aplicá-las em outras imagens depende da qualidade de imagens usadas para treinamento.
>&#x200B;>Para obter melhores resultados, a Adobe recomenda usar imagens visualmente semelhantes para treinar o serviço para cada tag.
