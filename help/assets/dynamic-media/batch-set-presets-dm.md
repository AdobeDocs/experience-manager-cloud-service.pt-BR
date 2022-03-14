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

# Sobre predefinições do conjunto de lotes {#about-bsp}

Use **[!UICONTROL Predefinições do conjunto de lotes]** para criar e organizar vários ativos em um conjunto de imagens ou conjunto de rotação no momento em que você faz upload de arquivos de ativos para uma pasta individualmente ou usando a assimilação em massa. É possível executar a predefinição junto com as tarefas de importação de ativos agendadas em [!DNL Dynamic Media]. Cada predefinição é um conjunto de instruções autocontido e nomeado exclusivamente que define como construir o conjunto de imagens ou o conjunto de rotação usando imagens que correspondem às convenções de nomenclatura definidas na receita predefinida.

>[!IMPORTANT]
>
>Você está usando predefinições de conjunto de lotes em [!DNL Dynamic Media Classic]e migrar de [!DNL Dynamic Media Classic] ao Adobe Experience Manager as a Cloud Service? Em caso positivo, é necessário recriar manualmente as definições predefinidas do conjunto de lotes em [!DNL Adobe Experience Manager as a Cloud Service].

**Prática recomendada** - Ao trabalhar com o Adobe de predefinições de conjunto de lotes, o recomenda o seguinte fluxo de trabalho:

1. Crie uma predefinição de conjunto de lotes. Consulte [Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação](#creating-bsp).
1. Crie uma pasta de ativos ou use uma pasta de ativos existente e verifique se ela está sincronizada com [!DNL Dynamic Media]. Consulte [Criar pastas](/help/assets/manage-digital-assets.md#creating-folders).
1. Aplique a predefinição do conjunto de lotes à pasta de ativos. Consulte [Sobre a aplicação de predefinições de conjuntos em lotes a pastas](#apply-bsp).
1. Faça upload de imagens para a pasta de ativos. Consulte [Fazer upload de ativos para conjuntos de imagens](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Fazer upload de ativos para conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)ou [Adicionar ativos digitais ao Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. O conjunto de imagens ou conjunto de rotação é gerado automaticamente na pasta desejada.
1. Publique seu conjunto de imagens ou conjunto de rotação. Consulte [Publicar ativos do Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação {#creating-bsp}

Para criar Predefinições de Conjuntos de Lotes, é desejável que você tenha familiaridade e compreensão de expressões regulares.

Idealmente, sua empresa já definiu uma convenção de nomenclatura para como os ativos são agrupados em um conjunto.
Para ajudar você a entender a importância de usar uma convenção de nomenclatura, suponha que a convenção de nomenclatura definida em sua empresa seja `<style>-<color>-<view>`. E, o nome base do conjunto deve ser sempre `<style>-<color>`e a extensão do nome do conjunto será `-SET`. Se você fizer upload de uma imagem nomeada `0123-RED-01`, um conjunto seria criado com o nome `0123-RED-SET`. Se você fizer upload de imagens posteriormente `0123-RED-03` e `0123-BLUE-01`, em seguida, o `RED-03` imagem seria adicionada ao conjunto na segunda posição porque é classificada como menor que `01`. No entanto, a variável `BLUE-01` seria parte de um novo conjunto chamado `0123-BLUE-SET`. Para o próximo upload de ativo, você adiciona arquivos `0123-RED-02` e `0123-BLUE-02`. Cada ativo seria adicionado ao respectivo conjunto. O `RED-02` a imagem seria classificada automaticamente entre as `01` e `03` imagens, por causa da ordem.

O **[!UICONTROL Predefinição do conjunto de lotes]** em [!DNL Dynamic Media] permite criar, editar ou excluir predefinições de conjuntos em lotes e aplicar ou remover predefinições de conjuntos em lotes de ou para pastas de ativos. Você pode usar as listas suspensas de campo de formulário para definir uma predefinição de conjunto de lotes ou usar o **[!UICONTROL Código bruto]** , que permite digitar a sintaxe de expressão regular.

Você pode criar muitas predefinições de conjuntos em lotes para cobrir todos os trabalhos de assimilação de ativos necessários.

### Sobre a Convenção de Nomenclatura de Ativos

O **[!UICONTROL Convenção de nomenclatura de ativos]** na área **[!UICONTROL Predefinição do conjunto de lotes]** A página tem dois elementos que podem ser usados para definir sua predefinição de conjunto de lotes: **[!UICONTROL Corresponder]** e **[!UICONTROL Nome básico]**. Esses elementos permitem definir uma convenção de nomenclatura e identificar a parte da convenção usada para nomear o conjunto no qual eles estão contidos. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

A convenção de nomenclatura individual de uma empresa geralmente usa uma ou mais linhas de definição de cada um desses dois elementos. Você pode usar quantas linhas para sua definição exclusiva e agrupá-las em elementos distintos, como para Imagem principal, Elemento de cor, Elemento de exibição alternativo e Elemento de amostra.

Por exemplo, a sintaxe de uma expressão regular de correspondência literal pode ser semelhante ao seguinte:

`(\w+)-\w+-\w+`

### Sobre a ordem de sequência

Opcionalmente, é possível definir a ordem em que as imagens são exibidas depois que o conjunto de imagens ou o conjunto de rotação é agrupado em [!DNL Dynamic Media]. Por padrão, os ativos são classificados alfanumérico. No entanto, é possível usar uma lista separada por vírgulas de expressões regulares para definir a ordem.

Com relação à automação de pedido de sequência, você especifica regras para forçar a classificação de ativos de determinada maneira, se necessário. Por exemplo, suponha que seu primeiro ativo seja sempre nomeado `_main` e você quer que ele seja seguido por `_alt1`, `_alt2`, `_alt3`e assim por diante. Nesses casos, você pode criar uma regra de ordenação de sequência com a seguinte sintaxe:

`.*_main,.*_alt[0-9]`

Embora uma sequência de classificação de força seja possível, é melhor confiar na numeração alfanumérica para a ordenação de sequência, na medida do possível. Além disso, você pode usar o conjunto de imagens ou as ferramentas do editor de conjunto de rotação no [!DNL Dynamic Media] para reorganizar a ordem de sequência dos ativos ou adicionar e excluir novos ativos no conjunto usando uma operação de arrastar e soltar.

Quando você terminar de criar uma predefinição de conjunto de lotes, aplique-a a uma ou mais pastas que você criou. Consulte [Sobre a aplicação de predefinições de conjuntos em lotes a pastas](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Para criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação:**

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições do conjunto de lotes]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. No **[!UICONTROL Predefinições do conjunto de lotes]** , próximo ao canto superior direito, selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar predefinição de conjunto de lotes]** na caixa de diálogo , na **[!UICONTROL Nome da predefinição]** campo de texto, insira um nome descritivo. O nome predefinido não é editável se você decidir alterá-lo posteriormente.

1. No **[!UICONTROL Tipo de predefinição]** , selecione **[!UICONTROL ImageSet]** ou **[!UICONTROL SpinSet]**. Certifique-se de escolher o tipo de predefinição correto; não é editável posteriormente.
1. Selecione **[!UICONTROL Criar]**.
1. À direita do **[!UICONTROL Editar predefinição do conjunto de lotes]** , defina as opções editáveis desejadas na página **[!UICONTROL Detalhes da predefinição]** e **[!UICONTROL Definir Convenção de Nomenclatura]** cabeçalhos.
Para saber mais sobre as opções editáveis disponíveis para você, consulte [Detalhes da predefinição, Definir convenção de nomenclatura e resultados da regra - opções RegX](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Crie um ou mais grupos de expressões regulares.

   * À esquerda do **[!UICONTROL Editar predefinição do conjunto de lotes]** página, em **[!UICONTROL Corresponder]**, **[!UICONTROL Nome básico]** ou **[!UICONTROL Ordem de sequência]**, selecione **[!UICONTROL Adicionar grupo]**.
   * O **[!UICONTROL Corresponder]** é obrigatório. **[!UICONTROL Nome básico]** é obrigatório somente se a variável **[!UICONTROL Corresponder]** O campo ainda não especifica um nome base usando um agrupamento de colchetes. **[!UICONTROL Ordem de sequência]** é opcional.
   * Usando as listas suspensas e caixas de texto no formulário do grupo, especifique um grupo de expressões que deseja usar para definir os critérios de nomenclatura para o conjunto de imagens ou para os membros do ativo de conjunto de rotação.
      * À medida que você seleciona e especifica expressões para um grupo, observe que a sintaxe de expressão regular real é refletida perto do canto inferior direito da página, sob a variável **[!UICONTROL Resultados da Regra - RegX]** cabeçalho. Para ver a string de expressão regular atualizada no canto inferior direito, selecione qualquer lugar fora da área do formulário. Essas cadeias de caracteres de expressão regular representam o padrão que você deseja corresponder em uma pesquisa de [!DNL Dynamic Media] ativos para criar seu conjunto de imagens ou conjunto de rotação.
      * Se você adicionou um grupo e deseja removê-lo, selecione **[!UICONTROL X]**.
   * Ao adicionar dois ou mais grupos, na **[!UICONTROL E]** , selecione **[!UICONTROL E]** para associar-se a um grupo recém-adicionado a qualquer grupo de expressão anterior que você tenha adicionado. Ou, selecione **[!UICONTROL Ou]** para adicionar uma alternância entre o grupo de expressões anterior e o novo grupo que você criar. O **[!UICONTROL Ou]** operando é definido pelo uso de um caractere de linha vertical `|` na própria sintaxe da expressão regular.

1. Faça uma das seguintes opções:

   * Para adicionar outro novo grupo, em **[!UICONTROL Corresponder]**, **[!UICONTROL Nome básico]** ou **[!UICONTROL Ordem de sequência]**, selecione **[!UICONTROL Adicionar grupo]**. Crie outro grupo de expressões regulares como fez na etapa anterior.
   * Revise a sintaxe da expressão regular no **[!UICONTROL Resultados da Regra - RegX]** área. Se for necessário alterar a sintaxe, faça as edições no respectivo grupo à esquerda da página.
   * Se tiver terminado de criar grupos de expressão, continue para a próxima etapa.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar]**.

Agora você está pronto para aplicar a predefinição de conjunto de lotes a uma pasta de ativos. Em seguida, faça upload de ativos para essa pasta. Esse fluxo de trabalho resulta na geração automática do conjunto de imagens ou do conjunto de rotação. Consulte [Sobre a aplicação de predefinições de conjuntos em lotes a pastas de ativos](#apply-bsp).

### Detalhes da predefinição, Definir convenção de nomenclatura e resultados da regra - opções RegX {#features-options-bsp}

Essas opções estão disponíveis na **[!UICONTROL Editar predefinição do conjunto de lotes]** ao criar ou editar uma predefinição de conjunto de lotes.

Consulte [Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação](#creating-bsp) ou [Editar uma predefinição de conjunto de lotes](#edit-bsp).

| **[!UICONTROL Detalhes da predefinição]** | Descrição |
| --- | --- |
| Nome da predefinição | Somente leitura. O nome especificado quando você criou o conjunto de lotes pela primeira vez. Se for necessário renomear a predefinição, é possível copiar a predefinição de conjunto de lotes existente e especificar um novo nome. Consulte [Copiar uma predefinição de conjunto de lotes existente](#copy-bsp). |
| Tipo | Somente leitura. O tipo foi especificado quando você criou o conjunto de lotes pela primeira vez. Copiar uma predefinição de conjunto de lotes existente não permite alterar sua [!UICONTROL Tipo]; em vez disso, você deve criar uma predefinição. |
| Incluir ativos derivados | Opcional. Para ter [!DNL Dynamic Media]O IPS do (Sistema de produção de imagens) inclui imagens geradas ou &quot;derivadas&quot; com seu Conjunto de rotação ou Conjunto de imagens, selecione **[!UICONTROL Sim]** (padrão). Um ativo derivado é uma imagem que não foi carregada diretamente por um usuário. Em vez disso, o ativo foi produzido pelo IPS quando um ativo principal foi carregado. Por exemplo, um ativo de imagem que o IPS gerou de uma página em um PDF, no momento em que o PDF foi carregado em [!DNL Dynamic Media], é considerado um ativo derivado. |
| Pasta de destino | Opcional. Se você definir grandes números de conjuntos de imagens ou de rotação, o Adobe recomenda manter esses conjuntos separados das pastas que contêm os próprios ativos. Dessa forma, considere criar uma pasta Conjuntos de imagens ou Conjuntos de rotação e redirecione o aplicativo para colocar conjuntos gerados por conjuntos em lote aqui.<br>Nesse caso, especifique qual pasta dentro da estrutura de pastas do Experience Manager Assets (`/content/dam`) tem a predefinição de conjunto de lotes ativa. Certifique-se de que a pasta esteja ativada para [!DNL Dynamic Media] sincronização para permitir como uma pasta de destino. Consulte [Configurar publicação seletiva no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>Mais de uma pasta pode ter uma determinada predefinição de conjunto de lotes atribuída a ela, se você aplicar a predefinição por meio do **[!UICONTROL Propriedades]**. Consulte [Aplicar predefinições de conjunto de lotes a partir da página Propriedades de uma pasta de ativos](#apply-bsp-to-folders-via-properties).<br>Se você não especificar uma pasta, o conjunto de imagens gerado pela predefinição do conjunto de lotes ou o conjunto de rotação será criado na mesma pasta da pasta de ativos para a qual você fez upload. |
| **[!UICONTROL Definir convenção de nomeação]** |  |
| Prefixo<br>ou<br>Sufixo | Opcional. Insira um prefixo, sufixo ou ambos nos respectivos campos.<br>Os campos de prefixo e sufixo permitem que você crie predefinições de conjuntos de lotes usando uma convenção de nomenclatura de arquivo personalizada e alternativa para um conjunto específico de conteúdo. Esse método é especialmente útil nos casos em que há uma exceção no esquema de nomeação padrão definido por uma empresa.<br>O prefixo ou sufixo é adicionado ao **[!UICONTROL Nome básico]** você define na variável **[!UICONTROL Convenção de nomenclatura de ativos]** área. Ao adicionar um prefixo ou sufixo, você garante que seu conjunto de imagens ou conjunto de rotação seja criado exclusiva e independentemente de outros ativos. Também pode servir para ajudar outras pessoas a identificar os tipos de arquivo. Por exemplo, para determinar o modo de cor usado, é possível adicionar como um prefixo ou sufixo `rgb` ou `cmyk`.<br>Embora não seja necessário especificar uma convenção de nomenclatura de conjunto para usar a funcionalidade predefinida de conjunto de lotes, a prática recomendada é usar a convenção de nomenclatura de conjunto. Essa prática permite definir quantos elementos da convenção de nomenclatura você deseja agrupar em um conjunto para ajudar a simplificar a criação de conjuntos em lotes. |
| **[!UICONTROL Resultados da regra - RegX]** |  |
| Convenção de nomenclatura de ativos - Correspondência | Somente leitura. Exibe a sintaxe da expressão regular com base nas opções de formulário Corresponder escolhidas para o código bruto inserido. |
| Convenção de Nomenclatura de Ativos - Nome Base | Somente leitura. Exibe a sintaxe da expressão regular com base nas opções de formulário Nome base escolhidas para o código bruto inserido. |
| Ordem de sequência - Correspondência | Somente leitura. Exibe a sintaxe da expressão regular com base nas opções de formulário escolhidas para o código bruto inserido. |

## Sobre a aplicação de predefinições de conjuntos em lotes a pastas de ativos {#apply-bsp}

Quando você atribui predefinições de conjuntos em lotes a uma ou mais pastas de ativos, qualquer subpasta herda automaticamente as predefinições da pasta pai.

É possível aplicar várias predefinições de conjuntos em lotes a uma pasta de ativos.

As pastas que têm uma predefinição de lote atribuída a elas são indicadas na interface do usuário com o nome da predefinição que aparece na pasta, na **[!UICONTROL Cartão]** exibir.

Para aplicar predefinições de conjuntos em lotes a pastas de ativos, use um dos dois métodos a seguir:

* [Aplicar predefinições de conjunto de lotes a pastas de ativos na página Predefinição de conjunto de lotes](#apply-bsp-to-folders-via-bsp-page) - Esse método oferece a você a maior flexibilidade possível. É possível aplicar uma única predefinição ou várias predefinições a uma única pasta ou várias pastas.
* [Aplicar predefinições de conjunto de lotes a partir da página Propriedades de uma pasta de ativos](#apply-bsp-to-folders-via-properties) - Esse método permite aplicar uma ou mais predefinições de conjunto de lotes a uma única pasta.

Como prática recomendada, verifique se as pastas de ativos estão sincronizadas [!DNL Dynamic Media], em seguida, aplique as predefinições desejadas.

Reprocesse ativos em uma pasta se você enfrentar uma das duas situações a seguir:

* Você deseja executar uma predefinição de conjunto em lote em uma pasta de ativos existente que já tem ativos carregados nela.
* Posteriormente, você edita uma predefinição de conjunto de lotes existente que era aplicada anteriormente a uma pasta de ativos.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Aplicar predefinições de conjunto de lotes a pastas de ativos na página Predefinição de conjunto de lotes {#apply-bsp-to-folders-via-bsp-page}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições do conjunto de lotes]**.
1. No **[!UICONTROL Predefinições do conjunto de lotes]** à esquerda da página **[!UICONTROL Nome da predefinição]** selecione a caixa de seleção de cada predefinição de conjunto de lotes que deseja aplicar às pastas.
1. Na barra de ferramentas, selecione **[!UICONTROL Aplicar predefinição de lote às pastas]**.
1. No **[!UICONTROL Selecionar pastas]** selecione a caixa de seleção de cada pasta à qual deseja que as predefinições do conjunto de lotes sejam aplicadas.
1. No canto superior direito do **[!UICONTROL Selecionar pastas]** página, selecione **[!UICONTROL Aplicar]**.

### Aplicar predefinições de conjunto de lotes a partir da página Propriedades de uma pasta de ativos {#apply-bsp-to-folders-via-properties}

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Navegue até uma pasta na qual deseja aplicar uma ou mais predefinições de conjunto de lotes.
1. Na página , à esquerda do **[!UICONTROL Nome]** selecione a caixa de seleção de uma pasta.
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Na página Propriedades da pasta, selecione o **[!UICONTROL Processamento Dynamic Media]** guia .

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. Em **[!UICONTROL Predefinições do conjunto de lotes]** do **[!UICONTROL Nome da predefinição]** na caixa de listagem suspensa, selecione o nome de uma predefinição de conjunto de lotes que deseja aplicar. A captura de tela acima mostra duas predefinições de conjunto de lotes selecionadas que são aplicadas à pasta de ativos.

   Se não houver nomes predefinidos de conjuntos de lotes no **[!UICONTROL Nome da predefinição]** na caixa de listagem suspensa, significa que você ainda não criou nenhuma predefinição de conjunto de lotes. Consulte [Criar uma predefinição de conjunto de lotes para um conjunto de imagens ou um conjunto de rotação](#creating-bsp).

   Para remover uma predefinição de conjunto de lotes aplicada, selecione **[!UICONTROL X]** à direita do tipo predefinido.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar e fechar]**.

## Editar uma predefinição de conjunto de lotes {#edit-bsp}

É possível editar uma predefinição de conjunto de lotes existente que você criou. Você pode alterar qualquer um dos grupos de expressão criados para a convenção de nomenclatura de ativos ou ordem de sequência. Se necessário, também é possível atualizar a pasta de destino e definir convenções de nomenclatura.

No entanto, não é possível alterar o nome ou o tipo predefinido da predefinição (Conjunto de imagens ou Conjunto de rotação). Se for necessário alterar o nome de uma predefinição, copie a predefinição existente e especifique um novo nome. Consulte [Copiar uma predefinição de conjunto de lotes](#copy-bsp).

Se você editar uma predefinição de conjunto de lotes aplicada anteriormente a uma pasta, a predefinição de conjunto de lotes recém-editada será aplicada somente aos novos ativos carregados nessa pasta.

Se desejar que a predefinição recém-editada seja reaplicada aos ativos existentes na pasta, será necessário reprocessar a pasta. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->Dessa forma, os ativos existentes agora se qualificariam para fazer parte de um conjunto de imagens ou conjunto de rotação e seriam adicionados. Além disso, os ativos existentes que já foram incluídos no conjunto de imagens ou no conjunto de rotação - com base na predefinição de conjunto de lotes anterior que foi usada - não são removidos e são exibidos como estão. Esse cenário pressupõe que elas não se qualificam mais com base na predefinição recém-editada.

**Para editar uma predefinição de conjunto de lotes:**

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições do conjunto de lotes]**.
1. No **[!UICONTROL Predefinições do conjunto de lotes]** à esquerda da página **[!UICONTROL Nome da predefinição]** marque a predefinição de conjunto de lotes que deseja alterar.
1. Na barra de ferramentas, selecione **[!UICONTROL Editar predefinição do conjunto de lotes]**.
1. Edite a predefinição conforme necessário.
1. No canto superior direito do **[!UICONTROL Predefinição do conjunto de lotes]** página, selecione **[!UICONTROL Salvar]**.

## Copiar uma predefinição de conjunto de lotes existente {#copy-bsp}

Você pode copiar uma predefinição de conjunto de lotes existente para evitar a necessidade de recriar manualmente uma predefinição complexa ou se quiser apenas renomear uma predefinição. No entanto, não é possível alterar o tipo predefinido usado (Conjunto de imagens ou Conjunto de rotação).

Se você copiar uma predefinição existente que é referência por pastas de ativos, essas pastas não serão afetadas.

**Copie uma predefinição de conjunto de lotes existente:**

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições do conjunto de lotes]**.
1. No **[!UICONTROL Predefinições do conjunto de lotes]** à esquerda da página **[!UICONTROL Nome da predefinição]** selecione a caixa de seleção da predefinição de conjunto de lotes que deseja copiar.
1. Na barra de ferramentas, selecione **[!UICONTROL Copiar]**.
1. No **[!UICONTROL Copiar predefinição do conjunto de lotes]** na caixa de diálogo , na **[!UICONTROL Título]** , digite um novo nome para a predefinição.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Selecionar **[!UICONTROL Copiar]**.

## Sobre a remoção de predefinições de conjuntos em lotes de pastas {#remove-bsp-from-folder}

Quando você remove predefinições de conjuntos em lotes de pastas, os novos ativos carregados nessas pastas não têm a predefinição de conjuntos em lotes aplicada a elas. Os ativos existentes na pasta que já foram adicionados ao conjunto de imagens ou ao conjunto de rotação com base na predefinição do conjunto de lotes que foi aplicada à pasta continuam a mostrar como estão.

Se desejar *excluir* predefinições de pastas, consulte [Excluir predefinições de conjuntos de lotes](#delete-bsp).

Há dois métodos que você pode usar para remover predefinições de conjuntos em lotes de pastas.

* [Remova predefinições do conjunto de lotes das pastas por meio da página Predefinição do conjunto de lotes](#remove-bsp-from-folders-via-bsp-page) - Esse método oferece a você a maior flexibilidade possível. Você pode remover uma única predefinição ou várias predefinições de uma única pasta ou de várias pastas.
* [Remova predefinições de conjuntos de lotes da página Propriedades de uma pasta](#remove-bsp-from-folders-via-properties) - Esse método permite remover uma ou mais predefinições de conjunto de lotes de uma única pasta.

### Remova predefinições do conjunto de lotes das pastas por meio da página Predefinição do conjunto de lotes {#remove-bsp-from-folders-via-bsp-page}

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições do conjunto de lotes]**.
1. No **[!UICONTROL Predefinições do conjunto de lotes]** à esquerda da página **[!UICONTROL Nome da predefinição]** selecione a caixa de seleção de uma ou mais predefinições de conjunto de lotes que deseja remover de uma ou mais pastas.
1. Na barra de ferramentas, selecione **[!UICONTROL Remover predefinição de lote das pastas]**.

1. No **[!UICONTROL Selecionar pastas]** selecione uma ou mais pastas nas quais deseja remover as predefinições do conjunto de lotes.
1. No canto superior direito do **[!UICONTROL Selecionar pastas]** página, selecione **[!UICONTROL Remover]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. No **[!UICONTROL Remover perfil]** caixa de diálogo, selecione **[!UICONTROL Remover]**.

### Remova predefinições de conjuntos de lotes da página Propriedades de uma pasta {#remove-bsp-from-folders-via-properties}

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Navegue até a pasta para a qual deseja remover uma ou mais predefinições de conjunto de lotes.
1. Na página , à esquerda do **[!UICONTROL Nome]** selecione a caixa de seleção de uma pasta.
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]**.
1. Na página Propriedades da pasta, selecione **[!UICONTROL Processamento Dynamic Media]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. Em **[!UICONTROL Predefinições do conjunto de lotes]**, selecione **[!UICONTROL X]** à direita do tipo predefinido.

1. No canto superior direito da página, selecione **[!UICONTROL Salvar e fechar]**.

## Excluir predefinições de conjuntos de lotes {#delete-bsp}

É possível excluir predefinições de conjuntos de lotes para removê-las permanentemente de [!DNL Dynamic Media]. Ou seja, eles não aparecem mais no [!UICONTROL Predefinição do conjunto de lotes] nem são mostradas na **[!UICONTROL Predefinições do conjunto de lotes]** lista suspensa da **[!UICONTROL Processamento Dynamic Media]** na guia da pasta **[!UICONTROL Propriedades]** página. Dessa forma, a predefinição não é aplicada aos ativos existentes em um reprocessamento de pasta ou quando novos ativos são carregados na pasta.

Se você excluir uma predefinição aplicada anteriormente a uma ou mais pastas, qualquer conjunto de imagens ou conjunto de rotação que tenha sido criado a partir de ativos nessas pastas continuará a ser exibido como está.

Se desejar *remove* predefinições de pastas, consulte [Remover predefinições de conjuntos de lotes de pastas](#remove-bsp-from-folder).

**Para excluir predefinições de conjunto de lotes:**

1. Selecione o logotipo do Experience Manager e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições do conjunto de lotes]**.
1. No **[!UICONTROL Predefinições do conjunto de lotes]** à esquerda da página **[!UICONTROL Nome da predefinição]** selecione a caixa de seleção de uma ou mais predefinições de conjunto de lotes que deseja excluir.
1. Na barra de ferramentas, selecione **[!UICONTROL Excluir predefinições do conjunto de lotes]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. No **[!UICONTROL Excluir predefinições do conjunto de lotes]** caixa de diálogo, selecione **[!UICONTROL Excluir]**.

   Se a predefinição que você está excluindo tiver sido referenciada por uma pasta de ativos, selecione **[!UICONTROL Forçar exclusão]** em vez disso.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Conjuntos de imagem](/help/assets/dynamic-media/image-sets.md)
>* [Conjuntos de rotação](/help/assets/dynamic-media/spin-sets.md)
>* [Configurar publicação seletiva no nível da pasta no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder) - Consulte &quot;Modo de sincronização&quot; no tópico se quiser saber mais sobre como sincronizar uma única pasta para o [!DNL Dynamic Media].
>* [Criar uma configuração do Dynamic Media no Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) - Consulte &quot;Modo de sincronização Dynamic Media&quot; no tópico se desejar saber mais sobre como sincronizar todas as pastas com o [!DNL Dynamic Media].

