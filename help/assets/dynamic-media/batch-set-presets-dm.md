---
title: Predefinições do conjunto de lotes
description: Saiba como automatizar a criação de conjuntos de imagens e conjuntos de rotação usando predefinições de conjuntos de lotes no Dynamic Media.
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: 5a50226bfae12440d07f9a21233ea06e118addac
workflow-type: tm+mt
source-wordcount: '3427'
ht-degree: 1%

---


# Sobre predefinições de conjuntos de lotes {#about-bsp}

Use **[!UICONTROL Predefinições de Conjunto de Lotes]** para ajudar a facilitar a criação e a organização de vários ativos em um conjunto de imagens ou conjunto de rotação no momento em que você carrega arquivos de ativos em uma pasta individualmente ou usando a ingestão em massa. É possível executar a predefinição juntamente com as tarefas de importação de ativos programadas em [!DNL Dynamic Media]. Cada predefinição é um conjunto exclusivo de instruções autocontidas e nomeadas que define como construir o conjunto de imagens ou o conjunto de rotação usando imagens que correspondem às convenções de nomenclatura definidas na fórmula predefinida.

>[!IMPORTANT]
>
>Se você usou predefinições de conjuntos de lotes em [!DNL Dynamic Media Classic] e está migrando de [!DNL Dynamic Media Classic] para o Adobe Experience Manager como Cloud Service, é necessário recriar manualmente as definições de predefinições de conjuntos de lotes em [!DNL Adobe Experience Manager as a Cloud Service].

**Prática**  recomendada - ao trabalhar com o Adobe de predefinições de conjuntos de lotes, o fluxo de trabalho a seguir é recomendado:

1. Crie uma predefinição de conjunto de lotes. Consulte [Criar um conjunto de lotes predefinido para um conjunto de imagens ou um conjunto de rotação](#creating-bsp).
1. Crie uma pasta de ativos ou use uma pasta de ativos existente e verifique se ela está sincronizada com [!DNL Dynamic Media]. Consulte [Criação de pastas](/help/assets/manage-digital-assets.md#creating-folders).
1. Aplique a predefinição do conjunto de lotes à pasta de ativos. Consulte [Sobre a aplicação de predefinições de conjuntos de lotes a pastas](#apply-bsp).
1. Carregue imagens para a pasta de ativos. Consulte [Carregar ativos para Conjuntos de imagens](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Carregar ativos para Conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets) ou [Adicionar ativos digitais ao Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. Crie seu conjunto de imagens ou conjunto de rotação. Consulte [Conjuntos de imagens](/help/assets/dynamic-media/image-sets.md) ou [Conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md).
1. Publique seu conjunto de imagens ou conjunto de rotação. Consulte [Publicar ativos Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação {#creating-bsp}

Para criar predefinições de conjuntos de lotes, é desejável que você tenha alguma familiaridade e compreensão sobre expressões comuns.

Idealmente, sua empresa já definiu uma convenção de nomenclatura para como os ativos são agrupados em um conjunto.
Para ajudá-lo a entender a importância de usar uma convenção de nomenclatura, suponha que sua convenção de nomenclatura definida pela empresa seja `<style>-<color>-<view>`. Além disso, o nome base do conjunto sempre deve ser `<style>-<color>` e a extensão do nome do conjunto deve ser `-SET`. Se você fizer upload de uma imagem chamada `0123-RED-01`, um conjunto será criado com o nome `0123-RED-SET`. Se você carregar posteriormente as imagens `0123-RED-03` e `0123-BLUE-01`, então a imagem `RED-03` será adicionada ao conjunto na segunda posição, pois é classificada como inferior a `01`. No entanto, a imagem `BLUE-01` faria parte de um novo conjunto chamado `0123-BLUE-SET`. Para o próximo upload de ativos, adicione arquivos `0123-RED-02` e `0123-BLUE-02`. Cada ativo seria adicionado ao respectivo conjunto. A imagem `RED-02` seria automaticamente classificada entre as imagens `01` e `03` existentes, devido à ordem de classificação.

A página **[!UICONTROL Predefinição de conjunto de lotes]** em [!DNL Dynamic Media] permite criar, editar ou excluir predefinições de conjuntos de lotes e aplicar ou remover predefinições de conjuntos de lotes de pastas de ativos. Você pode usar as listas suspensas do campo de formulário para definir uma predefinição de conjunto de lotes ou usar o campo **[!UICONTROL Código Bruto]**, que permite digitar a sintaxe de expressão regular.

Você pode criar quantas predefinições de conjuntos de lotes forem necessárias para cobrir todas as tarefas de assimilação de ativos forem necessárias.

**Sobre a Convenção de nomenclatura de ativos**

A área **[!UICONTROL Convenção de nomenclatura de ativos]** na página **[!UICONTROL Predefinição de conjunto de lotes]** tem dois elementos que podem ser usados para definir a predefinição do conjunto de lotes: **[!UICONTROL Corresponder]** e **[!UICONTROL Nome base]**. Esses elementos permitem que você defina uma convenção de nomenclatura e identifique a parte da convenção usada para nomear o conjunto no qual eles estão contidos. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

A convenção de nomenclatura individual de uma empresa geralmente usa uma ou mais linhas de definição de cada um desses dois elementos. Você pode usar quantas linhas desejar para sua definição exclusiva e agrupá-las em elementos distintos, como para a Imagem principal, o elemento Cor, o elemento Visualização alternativa e o elemento Amostra.

Por exemplo, a sintaxe para uma expressão regular de correspondência literal pode ser semelhante ao seguinte:

`(\w+)-\w+-\w+`

**Sobre o pedido de sequência**

Opcionalmente, você pode definir a ordem na qual as imagens são exibidas depois que o conjunto de imagens ou o conjunto de rotação é agrupado em [!DNL Dynamic Media]. Por padrão, seus ativos são ordenados alfanuméricos. Entretanto, é possível usar uma lista separada por vírgulas de expressões regulares para definir a ordem.

Em relação à automação de ordem de sequência, especifique regras para forçar a classificação de ativos de uma certa maneira, se necessário. Por exemplo, suponha que seu primeiro ativo seja sempre chamado de `_main` e você queira que ele seja seguido por `_alt1`, `_alt2`, `_alt3` e assim por diante. Nesses casos, é possível criar uma regra de ordem de sequência com a seguinte sintaxe:

`.*_main,.*_alt[0-9]`

Embora uma sequência de classificação de força seja possível, é melhor confiar na numeração alfanumérica para a ordenação de sequência, tanto quanto possível. Além disso, você pode usar o conjunto de imagens ou as ferramentas do editor de conjunto de rotação em [!DNL Dynamic Media] para reorganizar facilmente a ordem de sequência dos ativos, ou adicionar e excluir novos ativos no conjunto usando uma operação de arrastar e soltar.

Quando você terminar de criar uma predefinição de conjunto de lotes, aplique-a a uma ou mais pastas criadas. Consulte [Sobre a aplicação de predefinições de conjuntos de lotes a pastas](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Para criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação:**

1. Toque no logotipo Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições de conjunto de lotes]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. Na página **[!UICONTROL Predefinições de conjunto de lotes]**, próximo ao canto superior direito, toque em **[!UICONTROL Criar]**.
1. Na caixa de diálogo **[!UICONTROL Criar predefinição de conjunto de lotes]**, no campo de texto **[!UICONTROL Nome da predefinição]**, digite um nome descritivo. O nome predefinido não é editável se você decidir alterá-lo posteriormente.

1. Na lista suspensa **[!UICONTROL Tipo de predefinição]**, selecione **[!UICONTROL ImageSet]** ou **[!UICONTROL SpinSet]**. Escolha o tipo predefinido correto; não é editável mais tarde.
1. Toque em **[!UICONTROL Criar]**.
1. À direita da página **[!UICONTROL Editar predefinição de conjunto de lotes]**, defina as opções editáveis desejadas nos cabeçalhos **[!UICONTROL Predefinir detalhes]** e **[!UICONTROL Definir convenção de nomenclatura]**.
Para saber mais sobre as opções editáveis disponíveis para você, consulte [Detalhes da predefinição, Definir convenção de nomenclatura e Resultados da regra - Opções de RegX](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Crie um ou mais grupos de expressões regulares.

   * À esquerda da página **[!UICONTROL Editar predefinição de conjunto de lotes]**, em **[!UICONTROL Corresponder]**, **[!UICONTROL Nome de base]**, ou **[!UICONTROL Pedido de sequência]**, toque em **[!UICONTROL Adicionar grupo]**.
   * O campo **[!UICONTROL Match]** é obrigatório. **[!UICONTROL O]** Nome básico é obrigatório somente se o campo  **** Correspondência ainda não especificar um nome base usando um agrupamento entre colchetes. **[!UICONTROL A]** ordem de sequência é opcional.
   * Usando as listas suspensas e as caixas de texto no formulário do grupo, especifique um grupo de expressões que deseja usar para definir os critérios de nomeação para o conjunto de imagens ou para os membros do ativo do conjunto de rotação.
      * Conforme você seleciona e especifica expressões para um grupo, observe que a sintaxe de expressão regular real é refletida perto da parte inferior direita da página, sob o cabeçalho **[!UICONTROL Resultados da regra - RegX]** (toque em qualquer lugar fora da área do formulário para ver a string de expressão regular atualizada na parte inferior direita). Essas sequências de expressão comuns representam o padrão que você deseja corresponder em uma pesquisa de [!DNL Dynamic Media] ativos para criar seu conjunto de imagens ou conjunto de rotação.
      * Para remover um grupo adicionado, toque em **[!UICONTROL X]**.
   * Ao adicionar dois ou mais grupos, na lista suspensa **[!UICONTROL E]**, selecione **[!UICONTROL E]** para associar um grupo recém-adicionado a qualquer grupo de expressões anterior que você tenha adicionado. Ou selecione **[!UICONTROL Or]** para adicionar uma alternância entre o grupo de expressões anterior e o novo grupo que você criou. O operando **[!UICONTROL Or]** é definido pelo uso de um caractere de linha vertical `|` na própria sintaxe de expressão regular.

1. Faça uma das seguintes opções:

   * Para adicionar outro novo grupo, em **[!UICONTROL Corresponder]**, **[!UICONTROL Nome Base]** ou **[!UICONTROL Ordem de Sequência]**, toque em **[!UICONTROL Adicionar Grupo]**. Crie outro grupo de expressões regular, como fez na etapa anterior.
   * Analise a sintaxe de expressão regular na área **[!UICONTROL Resultados da regra - RegX]**. Se for necessário alterar a sintaxe, faça as edições no respectivo grupo à esquerda da página.
   * Se você tiver terminado de criar grupos de expressões, continue com a próxima etapa.

1. No canto superior direito da página, toque **[!UICONTROL Salvar]**.

Agora você é lido para aplicar a predefinição do conjunto de lotes a uma ou mais pastas de ativos, fazer upload de ativos para a pasta e, em seguida, criar seu conjunto de imagens ou conjunto de rotação. Consulte [Sobre a aplicação de predefinições de conjuntos de lotes a pastas](#apply-bsp).

### Detalhes predefinidos, Definir convenção de nomenclatura e resultados da regra - Opções RegX {#features-options-bsp}

Essas opções estão disponíveis na página **[!UICONTROL Editar predefinição de conjunto de lotes]** quando você cria ou edita uma predefinição de conjunto de lotes.

Consulte [Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação](#creating-bsp) ou [Editar uma predefinição de conjunto de lotes](#edit-bsp).

| **[!UICONTROL Detalhes da predefinição]** | Descrição |
| --- | --- |
| Nome da predefinição | Somente leitura. O nome especificado quando você criou o conjunto de lotes pela primeira vez. Se for necessário renomear a predefinição, é possível copiar a predefinição do conjunto de lotes existente e especificar um novo nome. Consulte [Copiando um conjunto de lotes existente predefinido](#copy-bsp). |
| Tipo | Somente leitura. O tipo foi especificado quando você criou o conjunto de lotes pela primeira vez. A cópia de uma predefinição de conjunto de lotes existente não permite alterar seu [!UICONTROL Tipo]; em vez disso, você deve criar uma predefinição. |
| Incluir ativos derivados | Opcional. Para que o IPS de [!DNL Dynamic Media] (Image Production System) inclua imagens geradas ou &quot;derivadas&quot; com seu Spin Set ou Image Set, selecione **[!UICONTROL Yes]** (padrão). Um ativo derivado é uma imagem que não foi carregada diretamente por um usuário. Em vez disso, o ativo foi produzido pelo IPS quando um ativo principal foi carregado. Por exemplo, um ativo de imagem que o IPS gerou a partir de uma página em um PDF, no momento em que o PDF foi carregado em [!DNL Dynamic Media], é considerado um ativo derivado. |
| Pasta de destino | Opcional. Se você definir grandes números de conjuntos de imagens ou de rotação, o Adobe recomenda manter esses conjuntos separados das pastas que contêm os próprios ativos. Dessa forma, considere a criação de uma pasta Conjuntos de imagens ou Conjuntos de rotação e redirecione o aplicativo para colocar os conjuntos gerados pelo conjunto de lotes aqui.<br>Nesse caso, especifique qual pasta na estrutura de pastas dos Ativos do Experience Manager (`/content/dam`) tem o lote definido como predefinido ativo. Certifique-se de que a pasta esteja habilitada para a sincronização [!DNL Dynamic Media] para permitir como uma pasta de destino. Consulte [Configurando a publicação seletiva no nível de pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>Mais de uma pasta pode ter uma predefinição de conjunto de lotes atribuída a ela, se você aplicar a predefinição por meio das  **[!UICONTROL Propriedades]** da pasta. Consulte [Aplicando predefinições de conjuntos de lotes da página Propriedades de uma pasta de ativos](#apply-bsp-to-folders-via-properties).<br>Se você não especificar uma pasta, a predefinição do conjunto de lotes será criada na mesma pasta da pasta de upload de ativos. |
| **[!UICONTROL Definir convenção de nomeação]** |  |
| Prefixo<br>ou<br>Sufixo | Opcional. Insira um prefixo, sufixo ou ambos nos respectivos campos.<br>Os campos de prefixo e sufixo permitem criar quantas predefinições de conjuntos de lotes usam uma convenção de nomenclatura de arquivos personalizada e alternativa para um conjunto específico de conteúdo. Esse método é especialmente útil em casos em que há uma exceção a um esquema de nomeação padrão definido pela empresa.<br>O prefixo ou sufixo é adicionado ao Nome  **[!UICONTROL básico]** definido na área de  **[!UICONTROL Nomeação de]** ativos Convenciontionarea. Ao adicionar um prefixo ou sufixo, você garante que seu conjunto de imagens ou conjunto de rotação seja criado exclusiva e independentemente de outros ativos. Também pode servir para ajudar outras pessoas a identificar tipos de arquivos. Por exemplo, para determinar o modo de cor usado, é possível adicionar como prefixo ou sufixo `rgb` ou `cmyk`.<br>Embora a especificação de uma convenção de nomenclatura de conjunto não seja necessária para usar a funcionalidade predefinida de conjunto de lotes, a prática recomendada é usar a convenção de nomenclatura de conjunto. Essa prática permite definir quantos elementos da convenção de nomenclatura você deseja agrupar em um conjunto para ajudar a simplificar a criação do conjunto de lotes. |
| **[!UICONTROL Resultados da regra - RegX]** |  |
| Convenção de nomenclatura de ativos - Correspondência | Somente leitura. Exibe a sintaxe de expressão normal com base nas opções de formulário Corresponder escolhidas para o código bruto inserido. |
| Convenção de nomenclatura de ativos - Nome básico | Somente leitura. Exibe a sintaxe de expressão regular com base nas opções de formulário Nome básico escolhidas para o código bruto inserido. |
| Ordem de sequência - Correspondência | Somente leitura. Exibe a sintaxe de expressão regular com base nas opções de formulário escolhidas ou no código bruto inserido. |

## Sobre a aplicação de predefinições de conjuntos de lotes a pastas {#apply-bsp}

Quando você atribui predefinições de conjuntos de lotes a uma ou mais pastas, qualquer subpasta herda automaticamente as predefinições de sua pasta pai.

É possível aplicar várias predefinições de conjuntos de lotes a uma pasta.

As pastas com uma predefinição de lote atribuída a ela são indicadas na interface do usuário com o nome da predefinição que aparece na pasta, na visualização **[!UICONTROL Card]**.

Para aplicar predefinições de conjuntos de lotes a pastas, use um dos dois métodos a seguir:

* [Aplicar predefinições de conjuntos de lotes a pastas de ativos na página](#apply-bsp-to-folders-via-bsp-page)  Predefinição de conjunto de lotes - Esse método oferta a maior flexibilidade possível. É possível aplicar uma única predefinição ou várias predefinições a uma única pasta ou a várias pastas.
* [Aplicar predefinições de conjuntos de lotes da página](#apply-bsp-to-folders-via-properties)  Propriedades de uma pasta de ativos - Esse método permite aplicar uma ou mais predefinições de conjuntos de lotes a uma única pasta.

Como prática recomendada, certifique-se de que as pastas de ativos estejam sincronizadas [!DNL Dynamic Media] e aplique as predefinições desejadas.

Reprocesse ativos em uma pasta se você tiver uma das duas situações a seguir:

* Você deseja executar uma predefinição de conjunto em lote em uma pasta de ativos existente que já tenha ativos carregados nela.
* Posteriormente, você edita uma predefinição de conjunto de lotes existente que foi aplicada anteriormente a uma pasta de ativos.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Aplicar predefinições de conjuntos de lotes às pastas de ativos da página Predefinição de conjunto de lotes {#apply-bsp-to-folders-via-bsp-page}

1. Toque no logotipo Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições de conjunto de lotes]**.
1. Na página **[!UICONTROL Predefinições de conjunto de lotes]**, à esquerda da coluna **[!UICONTROL Nome da predefinição]**, marque a caixa de seleção de cada predefinição de conjunto de lotes que você deseja aplicar às pastas.
1. Na barra de ferramentas, toque em **[!UICONTROL Aplicar predefinição de lote às pastas]**.
1. Na página **[!UICONTROL Selecionar Pastas]**, marque a caixa de seleção de cada pasta à qual você deseja que as predefinições do conjunto de lotes sejam aplicadas.
1. No canto superior direito da página **[!UICONTROL Selecionar pastas]**, toque em **[!UICONTROL Aplicar]**.

### Aplicar predefinições de conjuntos de lotes da página Propriedades de uma pasta de ativos {#apply-bsp-to-folders-via-properties}

1. Toque no logotipo da Adobe Experience Manager e navegue até **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Navegue até uma pasta à qual deseja aplicar uma ou mais predefinições de conjuntos de lotes.
1. Na página, à esquerda da coluna **[!UICONTROL Nome]**, marque a caixa de seleção de uma pasta.
1. Na barra de ferramentas, toque em **[!UICONTROL Propriedades]**.
1. Na página Propriedades da pasta, toque na guia **[!UICONTROL Processamento Dynamic Media]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. Em **[!UICONTROL Predefinições de conjunto de lotes]**, na caixa de lista suspensa **[!UICONTROL Nome da predefinição]**, selecione o nome de uma predefinição de conjunto de lotes que deseja aplicar. A captura de tela acima mostra duas predefinições de conjunto de lotes selecionadas aplicadas à pasta.

   Se nenhum nome predefinido de conjunto de lotes existir na caixa de lista suspensa **[!UICONTROL Nome da predefinição]**, isso significa que você ainda não criou nenhuma predefinição de conjunto de lotes. Consulte [Criar um conjunto de lotes predefinido para um conjunto de imagens ou um conjunto de rotação](#creating-bsp).

   Para remover uma predefinição de conjunto de lotes aplicada, toque em **[!UICONTROL X]** à direita do tipo predefinido.

1. No canto superior direito da página, toque em **[!UICONTROL Salvar e fechar]**.

## Editar uma predefinição de conjunto de lotes {#edit-bsp}

Você pode editar uma predefinição de conjunto de lotes existente que tenha criado. É possível alterar qualquer um dos grupos de expressão criados para a convenção de nomenclatura de ativos ou ordem de sequência. Se necessário, você também pode atualizar a pasta de destino e definir convenções de nomenclatura.

No entanto, não é possível alterar o nome ou o tipo predefinido da predefinição (Conjunto de imagens ou Conjunto de rotação). Se for necessário alterar o nome de uma predefinição, basta copiar a predefinição existente e especificar um novo nome. Consulte [Copiando um conjunto de lotes predefinido](#copy-bsp).

Se você editar uma predefinição de conjunto de lotes aplicada anteriormente a uma pasta, a predefinição recém-editada será aplicada somente a novos ativos que forem carregados na pasta.

Se desejar que a predefinição recém-editada seja reaplicada aos ativos existentes na pasta, você deverá reprocessar a pasta. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->Dessa forma, os ativos existentes se qualificariam para fazer parte de um conjunto de imagens ou conjunto de rotação e seriam adicionados. Além disso, os ativos existentes que já estavam incluídos no conjunto de imagens ou no conjunto de rotação com base na predefinição do conjunto de lotes anterior que foi usado - não são removidos (assumindo que não se qualificam mais com base na predefinição editada recentemente) e são exibidos como estão.

**Para editar uma predefinição de conjunto de lotes:**

1. Toque no logotipo Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições de Conjunto de Lotes.]**
1. Na página **[!UICONTROL Predefinições de conjunto de lotes]**, à esquerda da coluna **[!UICONTROL Nome da predefinição]**, verifique a predefinição de conjunto de lotes que deseja alterar.
1. Na barra de ferramentas, toque em **[!UICONTROL Editar predefinição de conjunto de lotes.]**
1. Edite a predefinição conforme necessário.
1. No canto superior direito da página **[!UICONTROL Predefinição do Conjunto de Lotes]**, toque em **[!UICONTROL Guardar.]**

## Copiando uma predefinição de conjunto de lotes existente {#copy-bsp}

Você pode copiar uma predefinição de conjunto de lotes existente para evitar a necessidade de recriar manualmente uma predefinição complexa ou se quiser apenas renomear uma predefinição. No entanto, não é possível alterar o tipo predefinido usado (Conjunto de imagens ou Conjunto de rotação).

Se você copiar uma predefinição existente que seja referência por pastas de ativos, essas pastas não serão afetadas.

**Para copiar uma predefinição de conjunto de lotes existente:**

1. Toque no logotipo Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições de Conjunto de Lotes.]**
1. Na página **[!UICONTROL Predefinições de conjunto de lotes]**, à esquerda da coluna **[!UICONTROL Nome da predefinição]**, marque a caixa de seleção da predefinição de conjunto de lotes que deseja copiar.
1. Na barra de ferramentas, toque em **[!UICONTROL Copiar]**.
1. Na caixa de diálogo **[!UICONTROL Copiar predefinição de conjunto de lotes]**, na caixa de texto **[!UICONTROL Título]**, digite um novo nome para a predefinição.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Toque em **[!UICONTROL Copiar]**.

## Sobre a remoção de predefinições de conjuntos de lotes de pastas {#remove-bsp-from-folder}

Quando você remove predefinições de conjuntos de lotes de pastas, todos os novos ativos carregados nessas pastas não têm a predefinição de conjuntos de lotes aplicada. Os ativos existentes na pasta que já foram adicionados ao conjunto de imagens ou ao conjunto de spint com base na predefinição do conjunto de lotes que foi aplicado à pasta continuam mostrando como estão.

Se desejar *excluir* predefinições de pastas, consulte [Excluindo predefinições de conjuntos de lotes](#delete-bsp).

Existem dois métodos que você pode usar para remover predefinições de conjuntos de lotes de pastas.

* [Remoção de predefinições de conjuntos de lotes de pastas por meio da página](#remove-bsp-from-folders-via-bsp-page)  Predefinição de conjunto de lotes - Este método oferta a maior flexibilidade possível. É possível remover uma única predefinição ou várias predefinições de uma única pasta ou de várias pastas.
* [Remoção de predefinições de conjuntos de lotes da página](#remove-bsp-from-folders-via-properties)  Propriedades de uma pasta - Esse método permite remover uma ou mais predefinições de conjuntos de lotes somente de uma única pasta.

### Remoção de predefinições de conjuntos de lotes de pastas por meio da página Predefinição de conjunto de lotes {#remove-bsp-from-folders-via-bsp-page}

1. Toque no logotipo Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições de conjunto de lotes]**.
1. Na página **[!UICONTROL Predefinições de conjunto de lotes]**, à esquerda da coluna **[!UICONTROL Nome da predefinição]**, marque a caixa de seleção de uma ou mais predefinições de conjunto de lotes que você deseja remover de uma ou mais pastas.
1. Na barra de ferramentas, toque em **[!UICONTROL Remover predefinição de lote das pastas]**.

1. Na página **[!UICONTROL Selecionar pastas]**, selecione uma ou mais pastas nas quais deseja que as predefinições de conjuntos de lotes sejam removidas.
1. No canto superior direito da página **[!UICONTROL Selecionar pastas]**, toque em **[!UICONTROL Remover]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. Na caixa de diálogo **[!UICONTROL Remover perfil]**, toque em **[!UICONTROL Remover]**.

### Remoção de predefinições de conjuntos de lotes da página Propriedades de uma pasta {#remove-bsp-from-folders-via-properties}

1. Toque no logotipo da Adobe Experience Manager e navegue até **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Navegue até a pasta para a qual deseja remover uma ou mais predefinições de conjunto de lotes.
1. Na página, à esquerda da coluna **[!UICONTROL Nome]**, marque a caixa de seleção de uma pasta.
1. Na barra de ferramentas, toque em **[!UICONTROL Propriedades]**.
1. Na página Propriedades da pasta, toque em **[!UICONTROL Processamento Dynamic Media]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. Em **[!UICONTROL Predefinições de conjunto de lotes]**, toque em **[!UICONTROL X]** à direita do tipo predefinido.

1. No canto superior direito da página, toque em **[!UICONTROL Salvar e fechar]**.

## Excluindo predefinições de conjuntos de lotes {#delete-bsp}

É possível excluir predefinições de conjuntos de lotes para removê-las permanentemente de [!DNL Dynamic Media]. Ou seja, eles não são mais exibidos na página [!UICONTROL Predefinição do conjunto de lotes], nem na lista suspensa **[!UICONTROL Predefinições do conjunto de lotes]** da guia **[!UICONTROL Processamento Dynamic Media]** na página **[!UICONTROL Propriedades]** da pasta. Dessa forma, a predefinição não é aplicada aos ativos existentes em um reprocessamento de pasta ou quando novos ativos são carregados na pasta.

Se você excluir uma predefinição anteriormente aplicada a uma ou mais pastas, todos os conjuntos de imagens ou conjuntos de rotação criados a partir de ativos nessas pastas continuarão a ser exibidos como estão.

Se desejar *remover* predefinições de pastas, consulte [Remover predefinições de conjuntos de lotes de pastas](#remove-bsp-from-folder).

**Para excluir predefinições de conjuntos de lotes:**

1. Toque no logotipo Adobe Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições de conjunto de lotes]**.
1. Na página **[!UICONTROL Predefinições de conjunto de lotes]**, à esquerda da coluna **[!UICONTROL Nome da predefinição]**, marque a caixa de seleção de uma ou mais predefinições de conjunto de lotes que você deseja excluir.
1. Na barra de ferramentas, toque em **[!UICONTROL Excluir predefinições de conjuntos de lotes]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. Na caixa de diálogo **[!UICONTROL Excluir predefinições de conjunto de lotes]**, toque em **[!UICONTROL Excluir]**.

   Se a predefinição que você está excluindo tiver sido referenciada por uma pasta de ativos, toque **[!UICONTROL Forçar exclusão]** em vez disso.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Conjuntos de imagem](/help/assets/dynamic-media/image-sets.md)
>* [Conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md)
>* [Configuração da publicação seletiva no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder)  - Consulte &quot;Modo de sincronização&quot; no tópico para saber mais sobre como sincronizar uma única pasta com  [!DNL Dynamic Media].
>* [Criação de uma configuração do Dynamic Media em Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)  - Consulte &quot;Modo de sincronização do Dynamic Media&quot; no tópico para saber mais sobre como sincronizar todas as pastas com  [!DNL Dynamic Media].