---
title: Gerenciar coleções de ativos digitais
description: Understand the concept of collection in Adobe Experience Manager Assets. Saiba como gerenciar, editar e criar coleções com outros usuários.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '2381'
ht-degree: 20%

---


# Gerenciar coleções {#manage-collections}

A collection is a set of assets within Adobe Experience Manager Assets. Use coleções para compartilhar ativos entre usuários. The set can be static collection or a dynamic collection that is based on search results.

Unlike folders, a collection can include assets from different locations. Você pode compartilhar coleções com vários usuários aos quais são atribuídos diferentes níveis de privilégios, incluindo exibição, edição e assim por diante.

Você pode compartilhar várias coleções com um usuário. Cada coleção contém referências a ativos. A integridade referencial dos ativos é mantida nas coleções.

As coleções são dos seguintes tipos, com base na maneira como elas coletam ativos:

* Uma coleção que contém uma lista de referência estática de ativos, pastas e outras coleções.

* Uma coleção inteligente que inclui dinamicamente ativos com base em critérios de pesquisa.

## Access the collections console {#navigate-the-collections-console}

Para abrir o console **[!UICONTROL Coleções]** :

To open the **[!UICONTROL Collections]**, tap or click the Experience Manager logo. From the navigation page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.

## Criar uma coleção {#create-a-collection}

You can create a collection either with [static references](#create-a-collection-with-static-references) or based on a [search criteria-based filter](#create-a-smart-collection). You can also create a collection from a lightbox.

### Create a collection with static references {#create-a-collection-with-static-references}

You can create a collection with static references, for example a collection with references to assets, folders, collections, spin sets, and image sets.

1. Navigate to the **[!UICONTROL Collections]** console.
1. From the toolbar, tap/click **[!UICONTROL Create]**.
1. Na página **[!UICONTROL Criar coleção]** , digite um título e uma descrição opcional para a coleção.
1. Adicione membros à coleção e atribua as permissões apropriadas. Como alternativa, selecione **[!UICONTROL Coleção pública]** para permitir que todos os usuários acessem a coleção.

   >[!NOTE]
   >
   >To enable the members to share collections with other users, provide the `dam-users` group read permissions at the path `home/users`. Give permission to the users at `/content/dam/collections` location to allow the users to view the Collections in pop up lists. Alternatively, make the user a part of `dam-users` group.

1. (Optional) Add a thumbnail image for the collection.
1. Toque/clique em **[!UICONTROL Criar]** e em **[!UICONTROL OK]** para fechar a caixa de diálogo. Uma coleção com o título e as propriedades especificadas é aberta no console Coleções.

   >[!NOTE]
   >
   >Experience Manager Assets lets you create review tasks for a collection similar to the way you create review tasks for an assets folder.

   To add assets to the collection, navigate to the Assets user interface. For details, see [Add assets to a collection](#add-assets-to-a-collection).

### Create collections using dropzone {#create-collections-using-dropzone}

You can drag assets from the Assets UI to a collection. You can also create a copy of a collection and drag the assets there.

1. From the Assets user interface, select the assets you want to add to a collection.
1. Arraste os ativos até a zona **[!UICONTROL Soltar na coleção]** . Alternatively, tap/click the **[!UICONTROL To Collection]** icon from the toolbar.
1. Na página **[!UICONTROL Adicionar à coleção]**, toque/clique no ícone **[!UICONTROL Criar coleção]** na barra de ferramentas. Se desejar adicionar os ativos a uma coleção existente, selecione-a na página e toque/clique em **[!UICONTROL Adicionar]**. Por padrão, a coleção atualizada mais recentemente é selecionada.
1. Na caixa de diálogo **[!UICONTROL Criar nova coleção]**, especifique o nome da coleção. Se quiser que a coleção seja acessível a todos os usuários, selecione **[!UICONTROL Coleção pública]**.
1. Tap/click **[!UICONTROL Continue]** to create the collection.

### Criar uma coleção inteligente {#create-a-smart-collection}

A Smart Collection uses a search criteria to dynamically populate assets. Você pode criar uma coleção inteligente usando apenas arquivos e não pastas ou arquivos e pastas.

1. Navegue até a interface do usuário do Assets e toque/clique no ícone **[!UICONTROL Pesquisar]**.
1. Enter search keyword in the Omni Search box and press Enter. Tap/click the GlobalNav icon to display the Filters panel and apply a search filter from the Search panel.
1. Na lista **[!UICONTROL Arquivos e pastas]** , selecione **[!UICONTROL Arquivos]**.
1. Tap/click **[!UICONTROL Save Smart Collection]**.
1. Specify a name for the collection. Select **[!UICONTROL Public]** to add the DAM Users group with the Viewer role to the smart collection.

   >[!NOTE]
   >
   >If you select **[!UICONTROL Public]**, the smart collection becomes available to everyone with the Owner role after you create it. Se você desmarcar a opção **[!UICONTROL Público]** , o grupo de usuários do DAM não estará mais associado à coleção inteligente.

1. Toque/clique em **[!UICONTROL Salvar]** para criar a coleção inteligente e feche a caixa de mensagem para concluir o processo. A nova coleção inteligente também é adicionada à lista **[!UICONTROL Pesquisas salvas]**.
O rótulo do botão **[!UICONTROL Criar seleção inteligente]** muda para **[!UICONTROL Editar seleção inteligente]**. Para editar as configurações da coleção inteligente, selecione **[!UICONTROL Arquivos]** na lista **[!UICONTROL Arquivos e pastas]**. Em seguida, toque/clique no botão **[!UICONTROL Editar seleção inteligente]**.

## Add assets to a collection {#add-assets-to-a-collection}

Você pode adicionar ativos a uma coleção que contenha uma lista de ativos ou pastas referenciados.

>[!NOTE]
>
>Smart collections use a search query to populate assets. Therefore, static references to assets and folders are not applicable to them.

1. In the Assets UI, navigate to the location of the asset that you want to add to a collection.
1. Select the asset and tap/click the **[!UICONTROL To Collection]** icon from the toolbar. Alternatively, you can drag the asset to the **[!UICONTROL Drop in Collection]** zone. Solte o botão do mouse quando a zona solta se tornar ativa e seu rótulo se alterar para **[!UICONTROL Soltar para Adicionar]**.
1. Na página **[!UICONTROL Adicionar à coleção]** , selecione a coleção à qual deseja adicionar o ativo.
1. Toque/clique em **[!UICONTROL Adicionar]** e feche a mensagem de confirmação. O ativo é adicionado à coleção.

## Editar uma coleção inteligente {#edit-a-smart-collection}

Smart collections are built by saving a search so you can alter their content by modifying the search parameters of the [saved search](#saved-searches).

1. In the Assets user interface, tap/click the **[!UICONTROL Search]** icon from the toolbar.
1. With the cursor in the Omnisearch box, press the Enter key.
1. Tap/click the GlobalNav icon to display the Filters panel.
1. Na lista **[!UICONTROL Pesquisas salvas]**, selecione a coleção inteligente que deseja modificar. O painel Pesquisar exibe os filtros configurados para a pesquisa salva.
1. Na lista **[!UICONTROL Arquivos e pastas]** , selecione **[!UICONTROL Arquivos]**.
1. Modifique um ou mais filtros, conforme necessário. Toque/clique em **[!UICONTROL Editar coleção]** inteligente. Você também pode editar o nome da coleção inteligente.
1. Tap/click **[!UICONTROL Save]**. The **[!UICONTROL Edit Smart Collection]** dialog appears.
1. Toque/clique em **[!UICONTROL Substituir]** para substituir a coleção inteligente original pela coleção editada. Como alternativa, selecione **[!UICONTROL Salvar como]** para salvar a coleção editada separadamente.
1. Na caixa de diálogo de confirmação, toque/clique em **[!UICONTROL Salvar]** para concluir o processo.

## Visualização e edição de metadados da coleção {#view-and-edit-collection-metadata}

Os metadados da coleção incluem dados sobre a coleção, incluindo quaisquer tags adicionadas.

1. No console Coleções, selecione uma coleção e toque/clique no ícone **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página **[!UICONTROL Metadados da coleção]**, visualize os metadados da coleção nas guias **[!UICONTROL Básico]** e **Avançado**.
1. Modifique os metadados, conforme necessário, e toque/clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas para salvar as alterações.

### Editar metadados da coleção em massa {#edit-collection-metadata-in-bulk}

Você pode editar os metadados de várias coleções simultaneamente. Essa funcionalidade ajuda a replicar rapidamente metadados comuns em várias coleções.

1. No console Coleções, selecione duas ou mais coleções para as quais deseja editar metadados.
1. Na barra de ferramentas, toque/clique no ícone **[!UICONTROL Propriedades]** .
1. Na página **[!UICONTROL Metadados da coleção]**, edite os metadados nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**, conforme necessário.
1. Toque/clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas e feche a caixa de diálogo de confirmação para concluir o processo.
1. Para anexar os novos metadados aos existentes, selecione o **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Toque/clique em **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >O Modo anexar funciona somente para campos que podem conter vários valores. Em campos que podem conter apenas um valor, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o **[!UICONTROL Modo anexar]**.

## Pesquisar {#searching}

O recurso Pesquisar em coleções oferece suporte à [Pesquisa por coleções](#search-collections) e [Pesquisa por ativos em uma coleção](#search-within-collections).

### Pesquisar coleções {#search-collections}

Você pode pesquisar coleções no console Coleções. Quando você pesquisa com palavras-chave na caixa Omnisearch, o AEM Assets pesquisa nomes de coleção, metadados e as tags adicionadas às coleções.

Se você pesquisar por coleções do nível superior, somente coleções individuais serão retornadas nos resultados da pesquisa. Os ativos ou pastas dentro das coleções são excluídos. Em todos os outros casos (por exemplo, em uma coleção individual ou em uma hierarquia de pastas), todos os ativos, pastas e coleções relevantes são retornados.

### Pesquisar em coleções {#search-within-collections}

No console Coleções, toque/clique em uma coleção para abri-la.

Em uma coleção, a pesquisa do AEM Asset está restrita aos ativos (e suas tags e metadados) dentro da coleção que você está visualizando. Quando você pesquisar em uma pasta, todos os ativos correspondentes e pastas secundárias dentro da pasta atual serão retornados. Quando você pesquisa em uma coleção, somente os ativos, pastas e outras coleções correspondentes que são membros diretos da coleção são retornados.

## Editar configurações de coleção {#edit-collection-settings}

Você pode editar configurações da coleção, como título e descrição, ou adicionar membros a uma coleção.

1. Selecione uma coleção e toque/clique no ícone **[!UICONTROL Configurações]** na barra de ferramentas. Como alternativa, use a ação rápida **[!UICONTROL Configurações]** na miniatura da coleção.
1. Modifique as configurações da coleção na página **[!UICONTROL Configurações da coleção]**. Por exemplo, modifique o título da coleção, as descrições, os membros e as permissões, conforme discutido em [Adicionar coleções](#create-a-collection).
1. Tap/click **[!UICONTROL Save]** to save the changes.

## Excluir uma coleção {#delete-a-collection}

1. No console Coleções, selecione uma ou mais coleções e toque/clique no ícone Excluir na barra de ferramentas.
1. Na caixa de diálogo, toque/clique em **[!UICONTROL Excluir]** para confirmar a ação de exclusão.

   >[!NOTE]
   >
   >Também é possível excluir coleções inteligentes ao [excluir pesquisas](#saved-searches)salvas.

## Baixar uma coleção {#download-a-collection}

Quando você baixa uma coleção, toda a hierarquia de ativos dentro dela é baixada, incluindo pastas e coleções-filho.

1. No console Coleções, selecione uma ou mais coleções para baixar.
1. Na barra de ferramentas, toque/clique no ícone de download.
1. Na caixa de diálogo **[!UICONTROL Download]** , toque/clique em **[!UICONTROL Download]**. Se desejar baixar as representações dos ativos dentro da coleção, selecione **[!UICONTROL Representações]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   Quando você seleciona uma coleção para download, a hierarquia completa da pasta sob a coleção é baixada. Para incluir cada coleção que você baixa (incluindo ativos em coleções secundárias aninhadas sob a coleção pai) em uma pasta individual, selecione **[!UICONTROL Criar pasta separada para cada ativo]**.

## Editar propriedades de metadados de várias coleções {#editing-metadata-properties-of-multiple-collections}

Os ativos Adobe Enterprise Manager (AEM) permitem que você edite os metadados de muitas coleções em massa. Use a página [!UICONTROL Propriedades] para executar alterações nos metadados em várias coleções, por exemplo, altere as propriedades dos metadados para um valor comum ou adicione ou modifique tags.

Para personalizar a página [!UICONTROL Propriedades] de metadados, incluindo adicionar, modificar e excluir propriedades de metadados, use o editor de Schemas.

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma coleção. Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é possível atualizar [em massa os metadados após a pesquisa](/help/assets/search-assets.md#metadataupdates).

1. No console de coleções, selecione as coleções que deseja editar.
1. Na barra de ferramentas, toque/clique em **[!UICONTROL Propriedades]** para abrir a página [!UICONTROL Propriedades] das coleções selecionadas.
1. Modifique as propriedades de metadados para coleções selecionadas nas várias guias.

   >[!NOTE]
   >
   >Os metadados adicionados para as coleções selecionadas substituem os metadados anteriores para essas coleções, exceto as tags. Quaisquer tags adicionadas no campo **[!UICONTROL Tags]** serão anexadas à lista existente de tags nos metadados.

1. Para visualização das propriedades de metadados de uma coleção específica, desmarque as coleções restantes na lista de coleções. Os campos do editor de metadados são preenchidos com os metadados da coleção específica.

   >[!NOTE]
   >
   >* Na página de propriedades da coleção, é possível remover coleções da lista de coleções desmarcando-as. A lista de coleções tem todas as coleções selecionadas por padrão. Os metadados das coleções que você remover não são atualizados.
   >* Na parte superior da lista, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre a seleção das coleções e a limpeza da lista.


1. Salve as alterações.

## Criar coleções aninhadas {#create-nested-collections}

É possível adicionar uma coleção a outra coleção, criando uma coleção aninhada.

1. No console Coleções, selecione a coleção ou o grupo de coleções desejado e toque ou clique em **[!UICONTROL Para coleção]** na barra de ferramentas.
1. Na página **[!UICONTROL Adicionar à coleção]** , selecione a coleção na qual deseja adicionar a coleção.

   >[!NOTE]
   >
   >A coleção atualizada mais recentemente é selecionada por padrão na página **[!UICONTROL Adicionar à coleção]** .

1. Toque/clique em **[!UICONTROL Adicionar]**. Uma mensagem confirma que a coleção é adicionada à coleção de públicos alvos na página **[!UICONTROL Selecionar destino]** . Feche a mensagem para concluir o processo.

>[!NOTE]
>
>Coleções inteligentes não podem ser aninhadas. Em outras palavras, as coleções inteligentes não podem conter nenhuma outra coleção.

## Pesquisas salvas {#saved-searches}

Na interface do usuário do Assets, pesquise ou filtre ativos com base em determinadas regras, critérios de pesquisa ou aspectos de pesquisa personalizados. Se salvá-los como **[!UICONTROL Pesquisas salvas]**, você poderá acessá-los posteriormente na lista **[!UICONTROL Pesquisas salvas]** do painel Filtro. Criar uma pesquisa salva também cria uma coleção inteligente.

Pesquisas salvas são criadas quando você cria uma coleção inteligente. As coleções inteligentes são adicionadas automaticamente à lista **[!UICONTROL Pesquisas salvas]**. A consulta Pesquisas salvas da coleção é salva na propriedade `dam:query`, no CRXDE no local relativo `/content/dam/collections/`.

>[!NOTE]
>
>Você pode compartilhar coleções inteligentes da mesma forma que compartilha coleções estáticas.

Editar pesquisas salvas é o mesmo que editar coleções inteligentes. Para obter detalhes, consulte [Editar uma coleção](#edit-a-smart-collection)inteligente.

Para excluir pesquisas salvas, siga estas etapas:

1. Na interface do usuário do Assets, toque/clique no ícone de pesquisa na barra de ferramentas.

1. Com o cursor no campo Omnisearch, pressione a tecla Enter.
1. Clique ou toque no ícone GlobalNav para exibir o painel Filtros.
1. Na lista **[!UICONTROL Pesquisas salvas]**, toque/clique em **[!UICONTROL Excluir]** ao lado da coleção inteligente que deseja excluir.
1. Na caixa de diálogo, toque/clique em **[!UICONTROL Excluir]** para excluir a pesquisa salva.

## Executar um fluxo de trabalho em uma coleção {#run-a-workflow-on-a-collection}

Você pode executar um fluxo de trabalho para os ativos em uma coleção. Se a coleção contiver coleções aninhadas, o fluxo de trabalho também será executado nos ativos dentro das coleções aninhadas. No entanto, se a coleção e a coleção aninhada contiverem ativos de duplicado, o fluxo de trabalho só será executado uma vez para esses ativos.

1. No console Coleções, selecione uma coleção na qual deseja executar um fluxo de trabalho.
1. Toque/clique no ícone GlobalNav e escolha **[!UICONTROL Linha]** do tempo na lista.
1. Na linha do tempo, clique ou toque no ícone Cursor na parte inferior e, em seguida, toque/clique em **[!UICONTROL Iniciar fluxo de trabalho]**.
1. Na seção **[!UICONTROL Iniciar fluxo de trabalho]**, selecione um modelo de fluxo de trabalho da lista. Por exemplo, selecione o modelo **[!UICONTROL Atualizar ativo DAM]**.
1. Insira um título para o fluxo de trabalho e toque/clique em **[!UICONTROL Start]**.
1. Na caixa de diálogo, toque/clique em **[!UICONTROL Continuar]**. O fluxo de trabalho é executado em todos os ativos na coleção.

>[!MORELIKETHIS]
>
>* [Criar uma tarefa de revisão para coleções](/help/assets/bulk-approval.md)

