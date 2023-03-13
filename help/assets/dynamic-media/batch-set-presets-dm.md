---
title: Predefinições de conjunto de lotes
description: Saiba como automatizar a criação de conjuntos de imagens e conjuntos de rotação usando predefinições de conjuntos de lotes no Dynamic Media.
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 1%

---

# Sobre predefinições de conjunto de lotes {#about-bsp}

Uso **[!UICONTROL Predefinições de conjunto de lotes]** para criar e organizar vários ativos em um conjunto de imagens ou conjunto de rotação no momento em que você faz upload de arquivos de ativos para uma pasta individualmente ou usando a assimilação em massa. A predefinição pode ser executada junto com os trabalhos de importação de ativos agendados no [!DNL Dynamic Media]. Cada predefinição é um conjunto de instruções com nome exclusivo e independente que define como construir o conjunto de imagens ou o conjunto de rotação usando imagens que correspondem às convenções de nomenclatura definidas na fórmula predefinida.

>[!IMPORTANT]
>
>Você está usando predefinições de conjunto de lotes no [!DNL Dynamic Media Classic]e migrando do [!DNL Dynamic Media Classic] para o Adobe Experience Manager as a Cloud Service? Nesse caso, você deve recriar manualmente as definições de predefinições de conjunto de lotes no [!DNL Adobe Experience Manager as a Cloud Service].

**Prática recomendada** - Ao trabalhar com predefinições de conjunto de lotes, o Adobe recomenda o seguinte fluxo de trabalho:

1. Criar uma predefinição de conjunto de lotes. Consulte [Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação](#creating-bsp).
1. Crie uma pasta de ativos ou use uma pasta de ativos existente e verifique se ela está sincronizada com o [!DNL Dynamic Media]. Consulte [Criar pastas](/help/assets/manage-digital-assets.md#creating-folders).
1. Aplicar a predefinição de conjunto de lotes à pasta de ativos. Consulte [Sobre a aplicação de predefinições de conjunto de lotes a pastas](#apply-bsp).
1. Faça upload de imagens para a pasta de ativos. Consulte [Fazer upload de ativos para conjuntos de imagens](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Fazer upload de ativos para Conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)ou [Adicionar ativos digitais ao Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. O conjunto de imagens ou o conjunto de rotação é gerado automaticamente na pasta desejada.
1. Publique seu conjunto de imagens ou conjunto de rotação. Consulte [Publicar ativos do Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação {#creating-bsp}

Para criar Predefinições de conjunto de lotes, é desejável que você tenha alguma familiaridade e compreensão de expressões regulares.

Idealmente, sua empresa já definiu uma convenção de nomenclatura para como os ativos são agrupados em um conjunto.
Para ajudá-lo a entender a importância de usar uma convenção de nomenclatura, suponha que a convenção de nomenclatura definida pela sua empresa seja `<style>-<color>-<view>`. E, o nome base do conjunto sempre deve ser `<style>-<color>`e a extensão do nome do conjunto seja `-SET`. Se você fizer upload de uma imagem chamada `0123-RED-01`, um conjunto será criado com o nome `0123-RED-SET`. Posteriormente, se você fizer upload de imagens `0123-RED-03` e `0123-BLUE-01`, depois o `RED-03` a imagem seria adicionada ao conjunto na segunda posição porque está classificada abaixo de `01`. No entanto, a `BLUE-01` a imagem faria parte de um novo conjunto chamado `0123-BLUE-SET`. No próximo upload de ativo, você adiciona arquivos `0123-RED-02` e `0123-BLUE-02`. Cada ativo seria adicionado ao respectivo conjunto. A variável `RED-02` a imagem seria classificada automaticamente entre as variáveis existentes `01` e `03` imagens, devido à ordem de classificação.

A variável **[!UICONTROL Predefinição de conjunto de lotes]** página em [!DNL Dynamic Media] permite criar, editar ou excluir predefinições de conjunto de lotes e aplicar ou remover predefinições de conjunto de lotes de ou para pastas de ativos. Você pode usar as listas suspensas do campo de formulário para definir uma predefinição de conjunto de lotes ou usar o **[!UICONTROL Código bruto]** , que permite digitar a sintaxe da expressão regular.

É possível criar muitas predefinições de conjunto de lotes para abranger todos os trabalhos de assimilação de ativos necessários.

### Sobre a convenção de nomeação de ativos

A variável **[!UICONTROL Convenção de nomeação de ativos]** área na **[!UICONTROL Predefinição de conjunto de lotes]** A página tem dois elementos que podem ser usados para definir a predefinição de conjunto de lotes: **[!UICONTROL Corresponder]** e **[!UICONTROL Nome base]**. Esses elementos permitem definir uma convenção de nomenclatura e identificar a parte da convenção usada para nomear o conjunto no qual eles estão contidos. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

A convenção de nomenclatura individual de uma empresa geralmente usa uma ou mais linhas de definição de cada um desses dois elementos. É possível usar quantas linhas forem necessárias para a definição exclusiva e agrupá-las em elementos distintos, como Imagem principal, Elemento de cor, Elemento de exibição alternativa e Elemento de amostra.

Por exemplo, a sintaxe de uma expressão regular de correspondência literal pode ser semelhante ao seguinte:

`(\w+)-\w+-\w+`

### Sobre a ordenação de sequência

Opcionalmente, é possível definir a ordem em que as imagens são exibidas depois que o conjunto de imagens ou o conjunto de rotação é agrupado em [!DNL Dynamic Media]. Por padrão, seus ativos são ordenados alfanumericamente. No entanto, você pode usar uma lista separada por vírgulas de expressões regulares para definir a ordem.

Em relação à automação de solicitação de sequência, especifique regras para forçar a classificação de ativos de uma determinada maneira, se necessário. Por exemplo, suponha que seu primeiro ativo seja sempre nomeado como `_main` e você quer que ele seja seguido com `_alt1`, `_alt2`, `_alt3`e assim por diante. Nesses casos, você pode criar uma regra de ordenação de sequência com a seguinte sintaxe:

`.*_main,.*_alt[0-9]`

Embora uma sequência de classificação forçada seja possível, é melhor confiar na numeração alfanumérica para a ordenação de sequência, na medida do possível. Além disso, você pode usar as ferramentas do editor de conjunto de imagens ou de conjunto de rotação em [!DNL Dynamic Media] para reorganizar a ordem de sequência dos ativos ou adicionar e excluir novos ativos no conjunto usando uma operação de arrastar e soltar.

Quando terminar de criar uma predefinição de conjunto de lotes, aplique-a a uma ou mais pastas criadas. Consulte [Sobre a aplicação de predefinições de conjunto de lotes a pastas](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Para criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação:**

1. Selecione o logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de conjunto de lotes]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. No **[!UICONTROL Predefinições de conjunto de lotes]** próximo ao canto superior direito, selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar predefinição de conjunto de lotes]** caixa de diálogo, no campo **[!UICONTROL Nome da predefinição]** campo de texto, digite um nome descritivo. O nome da predefinição não pode ser editado se você decidir alterá-lo posteriormente.

1. No **[!UICONTROL Tipo de predefinição]** selecione **[!UICONTROL ImageSet]** ou **[!UICONTROL SpinSet]**. Certifique-se de escolher o tipo de predefinição correto; ele não poderá ser editado posteriormente.
1. Selecione **[!UICONTROL Criar]**.
1. À direita do **[!UICONTROL Editar predefinição de conjunto de lotes]** defina as opções editáveis desejadas na seção **[!UICONTROL Detalhes da predefinição]** e **[!UICONTROL Definir convenção de nomeação]** cabeçalhos.
Para saber mais sobre as opções editáveis disponíveis, consulte [Detalhes da predefinição, Definir convenção de nomeação e Resultados da regra - Opções de RegX](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Crie um ou mais grupos de expressões regulares.

   * À esquerda do **[!UICONTROL Editar predefinição de conjunto de lotes]** página, em **[!UICONTROL Corresponder]**, **[!UICONTROL Nome base]** ou **[!UICONTROL Ordenação de sequência]**, selecione **[!UICONTROL Adicionar grupo]**.
   * A variável **[!UICONTROL Corresponder]** campo é obrigatório. **[!UICONTROL Nome base]** é obrigatório somente se a variável **[!UICONTROL Corresponder]** O campo ainda não especifica um nome base usando um agrupamento de colchetes. **[!UICONTROL Ordenação de sequência]** é opcional.
   * Usando as listas suspensas e caixas de texto no formulário do grupo, especifique um grupo de expressões que você deseja usar para definir os critérios de nomeação para membros do ativo do conjunto de imagens ou do conjunto de rotação.
      * Ao selecionar e especificar expressões para um grupo, observe que a sintaxe de expressão regular real é refletida próximo ao canto inferior direito da página, na **[!UICONTROL Resultados da regra - RegX]** cabeçalho. Para ver a sequência de caracteres da expressão regular atualizada no canto inferior direito, selecione qualquer lugar fora da área do formulário. Essas cadeias de caracteres de expressão regular representam o padrão que você deseja corresponder em uma pesquisa de [!DNL Dynamic Media] ativos para criar seu conjunto de imagens ou seu conjunto de rotação.
      * Se tiver adicionado um grupo e quiser removê-lo, selecione **[!UICONTROL X]**.
   * Quando você adiciona dois ou mais grupos, no campo **[!UICONTROL E]** selecione **[!UICONTROL E]** para unir um grupo recém-adicionado a qualquer grupo de expressão anterior que você tenha adicionado. Ou selecione **[!UICONTROL Ou]** para adicionar uma alternância entre o grupo de expressões anterior e o novo grupo que você criar. A variável **[!UICONTROL Ou]** é definido pelo uso de um caractere de linha vertical `|` na própria sintaxe da expressão regular.

1. Siga uma das seguintes opções:

   * Para adicionar outro novo grupo, em **[!UICONTROL Corresponder]**, **[!UICONTROL Nome base]** ou **[!UICONTROL Ordem de sequenciamento]**, selecione **[!UICONTROL Adicionar grupo]**. Crie outro grupo de expressão regular, como você fez na etapa anterior.
   * Revise a sintaxe da expressão regular no **[!UICONTROL Resultados da regra - RegX]** área. Se precisar alterar a sintaxe, faça as edições no respectivo grupo à esquerda da página.
   * Se você tiver terminado de criar grupos de expressões, continue para a próxima etapa.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]**.

Agora você está pronto para aplicar a predefinição de conjunto de lotes a uma pasta de ativos. Em seguida, você faz upload dos ativos para essa pasta. Esse fluxo de trabalho resulta na geração automática do conjunto de imagens ou do conjunto de rotação. Consulte [Sobre a aplicação de predefinições de conjunto de lotes a pastas de ativos](#apply-bsp).

### Detalhes da predefinição, Definir convenção de nomeação e Resultados da regra - Opções de RegX {#features-options-bsp}

Essas opções estão disponíveis no **[!UICONTROL Editar predefinição de conjunto de lotes]** ao criar ou editar uma predefinição de conjunto de lotes.

Consulte [Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação](#creating-bsp) ou [Editar uma predefinição de conjunto de lotes](#edit-bsp).

| **[!UICONTROL Detalhes da predefinição]** | Descrição |
| --- | --- |
| Nome da predefinição | Somente leitura. O nome especificado quando você criou o conjunto de lotes pela primeira vez. Se for necessário renomear a predefinição, copie a predefinição de conjunto de lotes existente e especifique um novo nome. Consulte [Copiar uma predefinição de conjunto de lotes existente](#copy-bsp). |
| Tipo | Somente leitura. O tipo foi especificado quando você criou o conjunto de lotes pela primeira vez. Copiar uma predefinição de conjunto de lotes existente não permite alterar sua [!UICONTROL Tipo]; em vez disso, você deve criar uma predefinição. |
| Incluir ativos derivados | Opcional. Para ter [!DNL Dynamic Media]O IPS (Sistema de Produção de Imagens) do inclui imagens geradas ou &quot;derivadas&quot; com seu Spin Set ou Conjunto de Imagens, selecione **[!UICONTROL Sim]** (padrão). Um ativo derivado é uma imagem que não foi carregada diretamente por um usuário. Em vez disso, o ativo era produzido pelo IPS quando um ativo principal era carregado. Por exemplo, um ativo de imagem que o IPS gerou de uma página em um PDF, no momento em que o PDF foi carregado no [!DNL Dynamic Media], é considerado um ativo derivado. |
| Pasta de destino | Opcional. Se você definir um grande número de conjuntos de imagens ou conjuntos de rotação, a Adobe recomenda manter esses conjuntos separados das pastas que contêm os próprios ativos. Dessa forma, considere a criação de uma pasta Conjuntos de imagens ou Conjuntos de rotação e redirecione o aplicativo para colocar conjuntos de lotes gerados aqui.<br>Nesse caso, especifique qual pasta na estrutura de pastas do Experience Manager Assets (`/content/dam`) tem a predefinição de conjunto de lotes ativa. Verifique se a pasta está ativada para [!DNL Dynamic Media] sincronização para permitir que ele seja uma pasta de destino. Consulte [Configurar a publicação seletiva no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>É possível atribuir uma determinada predefinição de conjunto de lotes a mais de uma pasta, caso você aplique a predefinição por meio da função **[!UICONTROL Propriedades]**. Consulte [Aplicar predefinições de conjunto de lotes a partir da página Propriedades de uma pasta de ativos](#apply-bsp-to-folders-via-properties).<br>Se você não especificar uma pasta, a predefinição de conjunto de lotes do conjunto de imagens gerado ou o conjunto de rotação será criado na mesma pasta da pasta de ativos na qual você fez upload. |
| **[!UICONTROL Definir convenção de nomeação]** |  |
| Prefixo<br>ou<br>Sufixo | Opcional. Insira um prefixo, um sufixo ou ambos nos respectivos campos.<br>Os campos de prefixo e sufixo permitem criar várias predefinições de conjunto de lotes usando uma convenção de nomenclatura de arquivo alternativa e personalizada para um conjunto específico de conteúdo. Esse método é especialmente útil nos casos em que há uma exceção no esquema de nomenclatura padrão definido por uma empresa.<br>O prefixo ou sufixo é adicionado à variável **[!UICONTROL Nome base]** você define no **[!UICONTROL Convenção de nomeação de ativos]** área. Ao adicionar um prefixo ou sufixo, você garante que o conjunto de imagens ou o conjunto de rotação seja criado de forma exclusiva e independente de outros ativos. Ele também pode ajudar outras pessoas a identificar tipos de arquivos. Por exemplo, para determinar um modo de cor usado, é possível adicionar como prefixo ou sufixo `rgb` ou `cmyk`.<br>Embora a especificação de uma convenção de nomenclatura de conjunto não seja necessária para usar a funcionalidade de predefinição de conjunto de lotes, a prática recomendada é usar a convenção de nomenclatura de conjunto. Essa prática permite definir quantos elementos de sua convenção de nomenclatura você desejar que sejam agrupados em um conjunto para ajudar a simplificar a criação do conjunto de lotes. |
| **[!UICONTROL Resultados da regra - RegX]** |  |
| Convenção de nomeação de ativos - Correspondência | Somente leitura. Exibe a sintaxe da expressão regular com base nas opções de formulário Corresponder escolhidas ou no código bruto inserido. |
| Convenção de nomeação de ativos - Nome de base | Somente leitura. Exibe a sintaxe da expressão regular com base nas opções de formulário do Nome de base escolhidas ou no código bruto inserido. |
| Ordem de sequência - Correspondência | Somente leitura. Exibe a sintaxe da expressão regular com base nas opções de formulário escolhidas ou no código bruto inserido. |

## Sobre a aplicação de predefinições de conjunto de lotes a pastas de ativos {#apply-bsp}

Ao atribuir predefinições de conjunto de lotes a uma ou mais pastas de ativos, qualquer subpasta herda automaticamente as predefinições de sua pasta principal.

É possível aplicar várias predefinições de conjunto de lotes a uma pasta de ativos.

As pastas que têm uma predefinição de lote atribuída a elas são indicadas na interface com o nome da predefinição que aparece na pasta, no campo **[!UICONTROL Cartão]** exibição.

Para aplicar predefinições de conjunto de lotes a pastas de ativos, use um dos dois métodos a seguir:

* [Aplicar predefinições de conjunto de lotes às pastas de ativos na página Predefinição de conjunto de lotes](#apply-bsp-to-folders-via-bsp-page) - Este método oferece a você mais flexibilidade. É possível aplicar uma única predefinição ou várias predefinições a uma única pasta ou a várias pastas.
* [Aplicar predefinições de conjunto de lotes a partir da página Propriedades de uma pasta de ativos](#apply-bsp-to-folders-via-properties) - Esse método permite aplicar uma ou mais predefinições de conjunto de lotes a uma única pasta.

Como prática recomendada, verifique se as pastas de ativos estão sincronizadas [!DNL Dynamic Media], em seguida, aplique as predefinições desejadas.

Reprocessamento de ativos em uma pasta se você encontrar um dos dois cenários a seguir:

* Você deseja executar uma predefinição de conjunto de lotes em uma pasta de ativos existente que já tenha ativos carregados nela.
* Posteriormente, você pode editar uma predefinição de conjunto de lotes existente que foi aplicada anteriormente a uma pasta de ativos.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Aplicar predefinições de conjunto de lotes às pastas de ativos na página Predefinição de conjunto de lotes {#apply-bsp-to-folders-via-bsp-page}

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de conjunto de lotes]**.
1. No **[!UICONTROL Predefinições de conjunto de lotes]** à esquerda do campo **[!UICONTROL Nome da predefinição]** , marque a caixa de seleção de cada predefinição de conjunto de lotes que deseja aplicar às pastas.
1. Na barra de ferramentas, selecione **[!UICONTROL Aplicar predefinição de lote a pastas]**.
1. No **[!UICONTROL Selecionar pastas]** marque a caixa de seleção de cada pasta à qual deseja aplicar as predefinições de conjunto de lotes.
1. No canto superior direito da **[!UICONTROL Selecionar pastas]** selecione **[!UICONTROL Aplicar]**.

### Aplicar predefinições de conjunto de lotes a partir da página Propriedades de uma pasta de ativos {#apply-bsp-to-folders-via-properties}

1. Selecione o logotipo do Experience Manager e vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Navegue até uma pasta na qual deseja aplicar uma ou mais predefinições de conjunto de lotes.
1. Na página, à esquerda da guia **[!UICONTROL Nome]** selecione a caixa de seleção de uma pasta.
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Na página Propriedades da pasta, selecione o **[!UICONTROL Processamento Dynamic Media]** guia.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. Em **[!UICONTROL Predefinições de conjunto de lotes]**, do **[!UICONTROL Nome da predefinição]** , selecione o nome de uma predefinição de conjunto de lotes que deseja aplicar. A captura de tela acima mostra duas predefinições de conjunto de lotes selecionadas aplicadas à pasta de ativos.

   Se não houver nomes de predefinições de conjuntos de lotes na **[!UICONTROL Nome da predefinição]** significa que você ainda não criou predefinições de conjunto de lotes. Consulte [Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação](#creating-bsp).

   Para remover uma predefinição de conjunto de lotes aplicada, selecione **[!UICONTROL X]** à direita do tipo predefinido.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar e fechar]**.

## Editar uma predefinição de conjunto de lotes {#edit-bsp}

É possível editar uma predefinição de conjunto de lotes existente que você criou. É possível alterar qualquer um dos grupos de expressão criados para a convenção de nomenclatura de ativos ou ordem de sequência. Se necessário, você também pode atualizar a pasta de destino e definir convenções de nomenclatura.

No entanto, não é possível alterar o nome ou o tipo de predefinição da predefinição (Conjunto de imagens ou Conjunto de rotação). Se for necessário alterar o nome de uma predefinição, copie a predefinição existente e especifique um novo nome. Consulte [Copiar uma predefinição de conjunto de lotes](#copy-bsp).

Se você editar uma predefinição de conjunto de lotes que foi aplicada anteriormente a uma pasta, a predefinição de conjunto de lotes recém-editada será aplicada somente aos novos ativos carregados nessa pasta.

Se quiser que a predefinição recém-editada seja reaplicada aos ativos existentes na pasta, reprocesse a pasta. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->Dessa forma, os ativos existentes agora seriam qualificados para fazer parte de um conjunto de imagens ou de uma rotação e seriam adicionados. Além disso, os ativos existentes que já estavam incluídos no conjunto de imagens ou no conjunto de rotação, com base na predefinição anterior do conjunto de lotes que foi usada, não são removidos e são exibidos como estão. Este cenário pressupõe que eles não se qualifiquem mais com base na predefinição recém-editada.

**Para editar uma predefinição de conjunto de lotes:**

1. Selecione o logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de conjunto de lotes]**.
1. No **[!UICONTROL Predefinições de conjunto de lotes]** à esquerda do campo **[!UICONTROL Nome da predefinição]** , verifique a predefinição de conjunto de lotes que deseja alterar.
1. Na barra de ferramentas, selecione **[!UICONTROL Editar predefinição de conjunto de lotes]**.
1. Edite a predefinição conforme necessário.
1. No canto superior direito da **[!UICONTROL Predefinição de conjunto de lotes]** selecione **[!UICONTROL Salvar]**.

## Copiar uma predefinição de conjunto de lotes existente {#copy-bsp}

É possível copiar uma predefinição de conjunto de lotes existente para evitar a necessidade de recriar manualmente uma predefinição complexa ou apenas renomear uma predefinição. No entanto, não é possível alterar o tipo de predefinição usado (Conjunto de imagens ou Conjunto de rotação).

Se você copiar uma predefinição existente que seja referência por pastas de ativos, essas pastas não serão afetadas.

**Copiar uma predefinição de conjunto de lotes existente:**

1. Selecione o logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de conjunto de lotes]**.
1. No **[!UICONTROL Predefinições de conjunto de lotes]** à esquerda do campo **[!UICONTROL Nome da predefinição]** , marque a caixa de seleção da predefinição de conjunto de lotes que deseja copiar.
1. Na barra de ferramentas, selecione **[!UICONTROL Copiar]**.
1. No **[!UICONTROL Copiar predefinição de conjunto de lotes]** caixa de diálogo, no campo **[!UICONTROL Título]** digite um novo nome para a predefinição.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Selecionar **[!UICONTROL Copiar]**.

## Sobre a remoção de predefinições de conjunto de lotes de pastas {#remove-bsp-from-folder}

Ao remover predefinições de conjunto de lotes de pastas, os novos ativos carregados nessas pastas não terão a predefinição de conjunto de lotes aplicada a eles. Os ativos existentes na pasta que já foram adicionados ao conjunto de imagens ou ao conjunto de dicas com base na predefinição de conjunto de lotes aplicada à pasta continuam sendo exibidos como estão.

Se você quiser *excluir* predefinições de pastas, consulte [Excluir predefinições de conjunto de lotes](#delete-bsp).

Há dois métodos que podem ser usados para remover predefinições de conjunto de lotes das pastas.

* [Remover predefinições de conjunto de lotes das pastas por meio da página Predefinição de conjunto de lotes](#remove-bsp-from-folders-via-bsp-page) - Este método oferece a você mais flexibilidade. É possível remover uma única predefinição ou várias predefinições de uma única pasta ou várias pastas.
* [Remover predefinições de conjunto de lotes da página Propriedades de uma pasta](#remove-bsp-from-folders-via-properties) - Esse método permite remover uma ou mais predefinições de conjunto de lotes de uma única pasta somente.

### Remover predefinições de conjunto de lotes das pastas por meio da página Predefinição de conjunto de lotes {#remove-bsp-from-folders-via-bsp-page}

1. Selecione o logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de conjunto de lotes]**.
1. No **[!UICONTROL Predefinições de conjunto de lotes]** à esquerda do campo **[!UICONTROL Nome da predefinição]** , marque a caixa de seleção de uma ou mais predefinições de conjunto de lotes que deseja remover de uma ou mais pastas.
1. Na barra de ferramentas, selecione **[!UICONTROL Remover predefinição de lote das pastas]**.

1. No **[!UICONTROL Selecionar pastas]** selecione uma ou mais pastas nas quais deseja remover as predefinições de conjunto de lotes.
1. No canto superior direito da **[!UICONTROL Selecionar pastas]** selecione **[!UICONTROL Remover]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. No **[!UICONTROL Remover perfil]** caixa de diálogo, selecione **[!UICONTROL Remover]**.

### Remover predefinições de conjunto de lotes da página Propriedades de uma pasta {#remove-bsp-from-folders-via-properties}

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Navegue até uma pasta para a qual deseja remover uma ou mais predefinições de conjunto de lotes.
1. Na página, à esquerda da guia **[!UICONTROL Nome]** selecione a caixa de seleção de uma pasta.
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Na página Propriedades da pasta, selecione **[!UICONTROL Processamento Dynamic Media]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. Em **[!UICONTROL Predefinições de conjunto de lotes]**, selecione **[!UICONTROL X]** à direita do tipo predefinido.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar e fechar]**.

## Excluir predefinições de conjunto de lotes {#delete-bsp}

É possível excluir predefinições de conjunto de lotes para removê-las permanentemente do [!DNL Dynamic Media]. Ou seja, elas não aparecem mais no [!UICONTROL Predefinição de conjunto de lotes] página nem são mostradas no campo **[!UICONTROL Predefinições de conjunto de lotes]** lista suspensa de **[!UICONTROL Processamento Dynamic Media]** na guia da pasta **[!UICONTROL Propriedades]** página. Dessa forma, a predefinição não é aplicada a ativos existentes em um reprocessamento de pasta ou quando novos ativos são carregados na pasta.

Se você excluir uma predefinição aplicada anteriormente a uma ou mais pastas, os conjuntos de imagens ou conjuntos de rotação criados a partir dos ativos nessas pastas continuarão sendo exibidos como estão.

Se você quiser *remover* predefinições de pastas, consulte [Remover predefinições de conjunto de lotes das pastas](#remove-bsp-from-folder).

**Para excluir predefinições de conjunto de lotes:**

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de conjunto de lotes]**.
1. No **[!UICONTROL Predefinições de conjunto de lotes]** à esquerda do campo **[!UICONTROL Nome da predefinição]** , marque a caixa de seleção de uma ou mais predefinições de conjunto de lotes que deseja excluir.
1. Na barra de ferramentas, selecione **[!UICONTROL Excluir predefinições de conjunto de lotes]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. No **[!UICONTROL Excluir predefinições de conjunto de lotes]** caixa de diálogo, selecione **[!UICONTROL Excluir]**.

   Se a predefinição que você está excluindo foi referenciada por uma pasta de ativos, selecione **[!UICONTROL Forçar Exclusão]** em vez disso.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Conjuntos de imagem](/help/assets/dynamic-media/image-sets.md)
>* [Conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md)
>* [Configurar a publicação seletiva no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder) - Consulte &quot;Modo de sincronização&quot; no tópico se quiser saber mais sobre como sincronizar uma única pasta com o [!DNL Dynamic Media].
>* [Criar uma configuração do Dynamic Media no Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) - Consulte &quot;Modo de sincronização do Dynamic Media&quot; no tópico se quiser saber mais sobre como sincronizar todas as pastas com o [!DNL Dynamic Media].

