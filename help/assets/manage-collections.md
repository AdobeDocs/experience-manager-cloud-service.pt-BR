---
title: Gerenciar coleções de ativos digitais
description: Entenda o conceito de coleção no Adobe Experience Manager Assets. Saiba como coletar, gerenciar, editar e coleções com outros usuários.
contentOwner: AG
mini-toc-levels: 1
feature: Coleções,Gerenciamento de ativos
role: User
exl-id: b0798adc-56a4-4577-b4ee-8d1fca3bff09
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '2400'
ht-degree: 19%

---

# Gerenciar coleções {#manage-collections}

Uma coleção é um conjunto de ativos no Adobe Experience Manager Assets. Use coleções para compartilhar ativos entre usuários. O conjunto pode ser uma coleção estática ou dinâmica baseada em resultados de pesquisa.

Diferente de pastas, uma coleção pode incluir ativos de locais diferentes. Você pode compartilhar coleções com vários usuários aos quais são atribuídos diferentes níveis de privilégios, incluindo exibição, edição e assim por diante.

Você pode compartilhar várias coleções com um usuário. Cada coleção contém referências a ativos. A integridade referencial dos ativos é mantida entre as coleções.

As coleções são dos seguintes tipos, com base na maneira como coletam ativos:

* Uma coleção que contém uma lista de referência estática de ativos, pastas e outras coleções.

* Uma coleção inteligente que inclui dinamicamente ativos com base em critérios de pesquisa.

## Acesse o console Coleções {#navigate-the-collections-console}

Para abrir o console **[!UICONTROL Coleções]**:

Para abrir o **[!UICONTROL Collections]**, toque ou clique no logotipo do Experience Manager. Na página de navegação, vá para **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.

## Criar uma coleção {#create-a-collection}

Você pode criar uma coleção com [referências estáticas](#create-a-collection-with-static-references) ou com base em um [filtro baseado em critérios de pesquisa](#create-a-smart-collection). Você também pode criar uma coleção de um lightbox.

### Criar uma coleção com referências estáticas {#create-a-collection-with-static-references}

Você pode criar uma coleção com referências estáticas, por exemplo, uma coleção com referências a ativos, pastas, coleções, conjuntos de rotação e conjuntos de imagens.

1. Navegue até o console **[!UICONTROL Coleções]**.
1. Na barra de ferramentas, toque/clique em **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Criar coleção]**, insira um título e uma descrição opcional para a coleção.
1. Adicione membros à coleção e atribua as permissões apropriadas. Como alternativa, selecione **[!UICONTROL Coleção pública]** para permitir que todos os usuários acessem a coleção.

   >[!NOTE]
   >
   >Para permitir que os membros compartilhem coleções com outros usuários, forneça as permissões de leitura do grupo `dam-users` no caminho `home/users`. Conceda permissão aos usuários no local `/content/dam/collections` para permitir que eles visualizem as Coleções em listas pop-up. Como alternativa, faça do usuário uma parte do grupo `dam-users`.

1. (Opcional) Adicione uma imagem em miniatura para a coleção.
1. Toque/clique em **[!UICONTROL Criar]** e em **[!UICONTROL OK]** para fechar a caixa de diálogo. Uma coleção com o título e as propriedades especificadas é aberta no console Coleções.

   >[!NOTE]
   >
   >Os Ativos do Experience Manager permitem criar tarefas de revisão para uma coleção semelhante à forma como você cria tarefas de revisão para uma pasta de ativos.

   Para adicionar ativos à coleção, navegue até a interface do usuário Ativos . Para obter detalhes, consulte [Adicionar ativos a uma coleção](#add-assets-to-a-collection).

### Criar coleções usando o dropzone {#create-collections-using-dropzone}

Você pode arrastar ativos da interface do usuário do Assets para uma coleção. Você também pode criar uma cópia de uma coleção e arrastar os ativos para lá.

1. Na interface do usuário do Assets, selecione os ativos que deseja adicionar a uma coleção.
1. Arraste os ativos para a zona **[!UICONTROL Soltar na coleção]**. Como alternativa, toque/clique no ícone **[!UICONTROL To Collection]** na barra de ferramentas.
1. Na página **[!UICONTROL Adicionar à coleção]**, toque/clique no ícone **[!UICONTROL Criar coleção]** na barra de ferramentas. Se desejar adicionar os ativos a uma coleção existente, selecione-a na página e toque/clique em **[!UICONTROL Adicionar]**. Por padrão, a coleção atualizada mais recentemente é selecionada.
1. Na caixa de diálogo **[!UICONTROL Criar nova coleção]**, especifique o nome da coleção. Se quiser que a coleção seja acessível a todos os usuários, selecione **[!UICONTROL Coleção pública]**.
1. Toque/clique em **[!UICONTROL Continuar]** para criar a coleção.

### Criar uma coleção inteligente {#create-a-smart-collection}

Uma coleção inteligente usa critérios de pesquisa para preencher dinamicamente ativos. Você pode criar uma Coleção inteligente usando somente arquivos e não pastas ou arquivos e pastas.

1. Navegue até a interface do usuário do Assets e toque/clique no ícone **[!UICONTROL Pesquisar]**.
1. Insira a palavra-chave de pesquisa na caixa Pesquisa Omni e selecione `Enter`. Toque/clique no ícone de Navegação global para exibir o painel Filtros e aplique um filtro de pesquisa no painel Pesquisar.
1. Na lista **[!UICONTROL Arquivos e pastas]**, selecione **[!UICONTROL Arquivos]**.
1. Toque/clique em **[!UICONTROL Salvar coleção inteligente]**.
1. Especifique um nome para a coleção. Selecione **[!UICONTROL Public]** para adicionar o grupo Usuários do DAM com a função Visualizador à coleção inteligente.

   >[!NOTE]
   >
   >Se você selecionar **[!UICONTROL Público]**, a coleção inteligente ficará disponível para todos com a função Proprietário depois de criá-la. Se você cancelar a opção **[!UICONTROL Public]**, o grupo de usuários do DAM não será mais associado à coleção inteligente.

1. Toque/clique em **[!UICONTROL Salvar]** para criar a coleção inteligente e feche a caixa de mensagem para concluir o processo. A nova coleção inteligente também é adicionada à lista **[!UICONTROL Pesquisas salvas]**.
O rótulo do botão **[!UICONTROL Criar seleção inteligente]** muda para **[!UICONTROL Editar seleção inteligente]**. Para editar as configurações da coleção inteligente, selecione **[!UICONTROL Arquivos]** na lista **[!UICONTROL Arquivos e pastas]**. Em seguida, toque/clique no botão **[!UICONTROL Editar seleção inteligente]**.

## Adicionar ativos a uma coleção {#add-assets-to-a-collection}

Você pode adicionar ativos a uma coleção que contém uma lista de ativos ou pastas referenciados.

>[!NOTE]
>
>As coleções inteligentes usam um query de pesquisa para preencher ativos. Portanto, referências estáticas a ativos e pastas não se aplicam a elas.

1. Na interface do usuário do Assets, navegue até o local do ativo que deseja adicionar a uma coleção.
1. Selecione o ativo e toque/clique no ícone **[!UICONTROL To Collection]** na barra de ferramentas. Como alternativa, você pode arrastar o ativo para a zona **[!UICONTROL Soltar na coleção]**. Solte o botão do mouse quando a área solta se tornar ativa e seu rótulo for alterado para **[!UICONTROL Solte para Adicionar]**.
1. Na página **[!UICONTROL Adicionar à coleção]**, selecione a coleção à qual deseja adicionar o ativo.
1. Toque/clique em **[!UICONTROL Adicionar]** e feche a mensagem de confirmação. O ativo é adicionado à coleção.

## Editar uma coleção inteligente {#edit-a-smart-collection}

As coleções inteligentes são criadas salvando uma pesquisa para que você possa alterar seu conteúdo modificando os parâmetros de pesquisa de [pesquisa salva](#saved-searches).

1. Na interface do usuário do Assets, toque/clique no ícone **[!UICONTROL Pesquisar]** na barra de ferramentas.
1. Com o cursor na caixa Omnisearch, selecione a tecla `Enter`.
1. Toque/clique no ícone de Navegação global para exibir o painel Filtros .
1. Na lista **[!UICONTROL Pesquisas salvas]**, selecione a coleção inteligente que deseja modificar. O painel Pesquisar exibe os filtros configurados para a pesquisa salva.
1. Na lista **[!UICONTROL Arquivos e pastas]**, selecione **[!UICONTROL Arquivos]**.
1. Modifique um ou mais filtros, conforme necessário. Toque/clique em **[!UICONTROL Editar coleção inteligente]**. Também é possível editar o nome da coleção inteligente.
1. Toque/clique em **[!UICONTROL Salvar]**. A caixa de diálogo **[!UICONTROL Editar coleção inteligente]** é exibida.
1. Toque/clique em **[!UICONTROL Substituir]** para substituir a coleção inteligente original pela coleção editada. Como alternativa, selecione **[!UICONTROL Salvar como]** para salvar a coleção editada separadamente.
1. Na caixa de diálogo de confirmação, toque/clique em **[!UICONTROL Salvar]** para concluir o processo.

## Exibir e editar metadados da coleção {#view-and-edit-collection-metadata}

Os metadados da coleção incluem dados sobre a coleção, incluindo quaisquer tags adicionadas.

1. No console Coleções , selecione uma coleção e toque/clique no ícone **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página **[!UICONTROL Metadados da coleção]**, visualize os metadados da coleção nas guias **[!UICONTROL Básico]** e **Avançado**.
1. Modifique os metadados, conforme necessário, e toque/clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas para salvar as alterações.

### Editar metadados de coleção em massa {#edit-collection-metadata-in-bulk}

Você pode editar os metadados de várias coleções simultaneamente. Essa funcionalidade ajuda você a replicar rapidamente metadados comuns em várias coleções.

1. No console Coleções , selecione duas ou mais coleções para as quais deseja editar metadados.
1. Na barra de ferramentas, toque/clique no ícone **[!UICONTROL Propriedades]**.
1. Na página **[!UICONTROL Metadados da coleção]**, edite os metadados nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**, conforme necessário.
1. Toque/clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas e feche a caixa de diálogo de confirmação para concluir o processo.
1. Para anexar os novos metadados aos existentes, selecione o **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Toque/clique em **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >O Modo anexar funciona somente para campos que podem conter vários valores. Em campos que podem conter apenas um valor, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o **[!UICONTROL Modo anexar]**.

## Pesquisar   {#searching}

O recurso Pesquisar em Coleções oferece suporte a [Pesquisar por coleções](#search-collections) e [Pesquisar por ativos em uma Coleção](#search-within-collections).

### Pesquisar coleções {#search-collections}

Você pode pesquisar coleções no console Coleções. Ao pesquisar com palavras-chave na caixa Omnisearch, [!DNL Experience Manager Assets] procura nomes de coleção, metadados e as tags adicionadas às coleções.

Se você pesquisar por coleções do nível superior, somente coleções individuais serão retornadas nos resultados da pesquisa. Os ativos ou pastas nas coleções são excluídos. Em todos os outros casos (por exemplo, em uma coleção individual ou em uma hierarquia de pasta), todos os ativos, pastas e coleções relevantes são retornados.

### Pesquisar em Coleções {#search-within-collections}

No console Coleções , toque/clique em uma coleção para abri-la.

Em uma coleção, a pesquisa [!DNL Experience Manager] é restrita aos ativos (e suas tags e metadados) dentro da coleção que você está visualizando. Ao pesquisar em uma pasta, todos os ativos e pastas filhas correspondentes na pasta atual são retornados. Ao pesquisar em uma coleção, somente os ativos, pastas e outras coleções correspondentes que são membros diretos da coleção são retornados.

## Editar configurações de coleção {#edit-collection-settings}

É possível editar configurações da coleção, como título e descrição, ou adicionar membros a uma coleção.

1. Selecione uma coleção e toque/clique no ícone **[!UICONTROL Configurações]** na barra de ferramentas. Como alternativa, use a ação rápida **[!UICONTROL Settings]** da miniatura da coleção.
1. Modifique as configurações da coleção na página **[!UICONTROL Configurações da coleção]**. Por exemplo, modifique o título da coleção, as descrições, os membros e as permissões, conforme discutido em [Adicionar coleções](#create-a-collection).
1. Toque/clique em **[!UICONTROL Salvar]** para salvar as alterações.

## Excluir uma coleção {#delete-a-collection}

1. No console Coleções , selecione uma ou mais coleções e toque/clique no ícone Excluir na barra de ferramentas.
1. Na caixa de diálogo, toque/clique em **[!UICONTROL Excluir]** para confirmar a ação de exclusão.

   >[!NOTE]
   >
   >Também é possível excluir coleções inteligentes ao [excluir pesquisas salvas](#saved-searches).

## Baixar uma coleção {#download-a-collection}

Ao baixar uma coleção, toda a hierarquia de ativos na coleção é baixada, incluindo pastas e coleções secundárias.

1. No console Coleções , selecione uma ou mais coleções para baixar.
1. Na barra de ferramentas, toque/clique no ícone de download.
1. Na caixa de diálogo **[!UICONTROL Download]**, toque/clique em **[!UICONTROL Download]**. Se quiser baixar as representações dos ativos na coleção, selecione **[!UICONTROL Representações]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   Ao selecionar uma coleção para baixar, a hierarquia completa da pasta na coleção é baixada. Para incluir cada coleção que você baixar (incluindo ativos em coleções secundárias aninhadas sob a coleção pai) em uma pasta individual, selecione **[!UICONTROL Criar pasta separada para cada ativo]**.

## Editar propriedades de metadados de várias coleções {#editing-metadata-properties-of-multiple-collections}

Os Ativos do Adobe Enterprise Manager permitem editar os metadados de muitas coleções em massa. Use a página [!UICONTROL Propriedades] para executar alterações de metadados em várias coleções, por exemplo, altere as propriedades de metadados para um valor comum ou adicione ou modifique tags.

Para personalizar a página de metadados [!UICONTROL Propriedades], incluindo adicionar, modificar, excluir propriedades de metadados, use o editor de Esquema.

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma coleção. Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é possível [atualizar os metadados em massa após pesquisar](/help/assets/search-assets.md#metadata-updates).

1. No console Coleções, selecione as coleções que deseja editar.
1. Na barra de ferramentas, toque/clique em **[!UICONTROL Propriedades]** para abrir a página [!UICONTROL Propriedades] das coleções selecionadas.
1. Modifique as propriedades de metadados para coleções selecionadas nas várias guias.

   >[!NOTE]
   >
   >Os metadados adicionados às coleções selecionadas substituem os metadados anteriores para essas coleções, exceto para tags. Quaisquer tags adicionadas no campo **[!UICONTROL Tags]** são anexadas à lista existente de tags nos metadados.

1. Para exibir as propriedades de metadados de uma coleção específica, cancele a seleção das coleções restantes na lista de coleções. Os campos do editor de metadados são preenchidos com os metadados para a coleção específica.

   >[!NOTE]
   >
   >* Na página de propriedades da coleção, é possível remover coleções da lista de coleções cancelando a seleção. A lista de coleções tem todas as coleções selecionadas por padrão. Os metadados das coleções que você remover não são atualizados.
   >* Na parte superior da lista, marque a caixa de seleção ao lado de **[!UICONTROL Title]** para alternar entre selecionar as coleções e limpar a lista.


1. Salve as alterações.

## Criar coleções aninhadas {#create-nested-collections}

Você pode adicionar uma coleção a outra coleção, criando uma coleção aninhada.

1. No console Coleções , selecione a coleção ou o grupo de coleções desejado e toque ou clique em **[!UICONTROL Para coleção]** na barra de ferramentas.
1. Na página **[!UICONTROL Adicionar à coleção]**, selecione a coleção na qual deseja adicionar a coleção.

   >[!NOTE]
   >
   >A coleção atualizada mais recentemente é selecionada por padrão na página **[!UICONTROL Adicionar à coleção]**.

1. Toque/clique em **[!UICONTROL Adicionar]**. Uma mensagem confirma que a coleção é adicionada à coleção de destino na página **[!UICONTROL Selecionar destino]** . Feche a mensagem para concluir o processo.

>[!NOTE]
>
>Coleções inteligentes não podem ser aninhadas. Em outras palavras, as coleções inteligentes não podem conter nenhuma outra coleção.

## Pesquisas salvas {#saved-searches}

Na interface do usuário do Assets, pesquise ou filtre ativos com base em determinadas regras, critérios de pesquisa ou aspectos de pesquisa personalizados. Se salvá-los como **[!UICONTROL Pesquisas salvas]**, você poderá acessá-los posteriormente na lista **[!UICONTROL Pesquisas salvas]** do painel Filtro. Criar uma pesquisa salva também cria uma coleção inteligente.

Pesquisas salvas são criadas quando você cria uma coleção inteligente. As coleções inteligentes são adicionadas automaticamente à lista **[!UICONTROL Pesquisas salvas]**. A consulta Pesquisas salvas da coleção é salva na propriedade `dam:query`, no CRXDE no local relativo `/content/dam/collections/`. Não há limites para as pesquisas que você pode salvar e nas pesquisas salvas exibidas na lista.

>[!NOTE]
>
>Você pode compartilhar coleções inteligentes da mesma forma que compartilha coleções estáticas.

Editar pesquisas salvas é o mesmo que editar coleções inteligentes. Para obter detalhes, consulte [Editar uma coleção inteligente](#edit-a-smart-collection).

Para excluir pesquisas salvas, siga estas etapas:

1. Na interface do usuário do Assets, toque/clique no ícone de pesquisa na barra de ferramentas.

1. Com o cursor no campo Omnisearch , selecione a tecla `Enter`.
1. Clique ou toque no ícone de Navegação global para exibir o painel Filtros .
1. Na lista **[!UICONTROL Pesquisas salvas]**, toque/clique em **[!UICONTROL Excluir]** ao lado da coleção inteligente que deseja excluir.
1. Na caixa de diálogo, toque/clique em **[!UICONTROL Excluir]** para excluir a pesquisa salva.

## Executar um fluxo de trabalho em uma coleção {#run-a-workflow-on-a-collection}

Você pode executar um fluxo de trabalho para os ativos em uma coleção. Se a coleção contiver coleções aninhadas, o fluxo de trabalho também será executado nos ativos dentro das coleções aninhadas. No entanto, se a coleção e a coleção aninhada contiverem ativos duplicados, o fluxo de trabalho será executado apenas uma vez para esses ativos.

1. No console Coleções , selecione uma coleção em que deseja executar um fluxo de trabalho.
1. Toque/clique no ícone de Navegação global e escolha **[!UICONTROL Linha do tempo]** na lista.
1. Na linha do tempo, selecione ou toque no ícone Cursor na parte inferior e, em seguida, toque/clique em **[!UICONTROL Iniciar fluxo de trabalho]**.
1. Na seção **[!UICONTROL Iniciar fluxo de trabalho]**, selecione um modelo de fluxo de trabalho da lista. Por exemplo, selecione o modelo **[!UICONTROL Atualizar ativo DAM]**.
1. Insira um título para o workflow e toque/clique em **[!UICONTROL Start]**.
1. Na caixa de diálogo, toque/clique em **[!UICONTROL Continuar]**. O fluxo de trabalho é executado em todos os ativos na coleção.

>[!MORELIKETHIS]
>
>* [Criar uma tarefa de revisão para Coleções](/help/assets/bulk-approval.md)

