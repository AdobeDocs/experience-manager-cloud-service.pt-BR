---
title: Gerenciar coleções de ativos digitais
description: Entenda o conceito de coleção no Adobe Experience Manager Assets. Saiba como criar coleções, gerenciar, editar e coleções com outros usuários.
contentOwner: AG
mini-toc-levels: 1
feature: Collections, Asset Management
role: User
exl-id: b0798adc-56a4-4577-b4ee-8d1fca3bff09
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '2398'
ht-degree: 18%

---

# Gerenciar coleções {#manage-collections}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-collections.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Uma coleção é um conjunto de ativos no Adobe Experience Manager Assets. Use coleções para compartilhar ativos entre usuários. O conjunto pode ser uma coleção estática ou dinâmica com base nos resultados da pesquisa.

Diferente de pastas, uma coleção pode incluir ativos de locais diferentes. Você pode compartilhar coleções com vários usuários aos quais são atribuídos diferentes níveis de privilégios, incluindo visualização, edição etc.

Você pode compartilhar várias coleções com um usuário. Cada coleção contém referências a ativos. A integridade referencial dos ativos é mantida entre as coleções.

As coleções são dos seguintes tipos, com base na maneira como elas agrupam ativos:

* Uma coleção que contém uma lista de referência estática de ativos, pastas e outras coleções.

* Uma coleção inteligente que inclui ativos dinamicamente com base em um critério de pesquisa.

## Acessar o console de coleções {#navigate-the-collections-console}

Para abrir o console **[!UICONTROL Coleções]**:

Para abrir as **[!UICONTROL Coleções]**, selecione o logotipo do Experience Manager. Na página de navegação, vá para **[!UICONTROL Assets]** > **[!UICONTROL Coleções]**.

## Criar uma coleção {#create-a-collection}

Você pode criar uma coleção com [referências estáticas](#create-a-collection-with-static-references) ou com base em um [filtro baseado em critérios de pesquisa](#create-a-smart-collection). Você também pode criar uma coleção de uma lightbox.

### Criar uma coleção com referências estáticas {#create-a-collection-with-static-references}

É possível criar uma coleção com referências estáticas, por exemplo, uma coleção com referências a ativos, pastas, coleções, conjuntos de rotação e conjuntos de imagem.

1. Navegue até o console **[!UICONTROL Coleções]**.
1. Na barra de ferramentas, selecione **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Criar Coleção]**, insira um título e uma descrição opcional para a coleção.
1. Adicione membros à coleção e atribua as permissões apropriadas. Como alternativa, selecione **[!UICONTROL Coleção pública]** para permitir que todos os usuários acessem a coleção.

   >[!NOTE]
   >
   >Para permitir que os membros compartilhem coleções com outros usuários, forneça ao grupo `dam-users` permissões de leitura no caminho `home/users`. Conceda permissão aos usuários no local `/content/dam/collections` para permitir que eles exibam as Coleções em listas pop-up. Como alternativa, torne o usuário parte do grupo `dam-users`.

1. (Opcional) Adicione uma imagem em miniatura para a coleção.
1. Selecione **[!UICONTROL Criar]** e **[!UICONTROL OK]** para fechar a caixa de diálogo. Uma coleção com o título e as propriedades especificadas é aberta no console Coleções.

   >[!NOTE]
   >
   >O Experience Manager Assets permite criar tarefas de revisão para uma coleção semelhante à maneira como você cria tarefas de revisão para uma pasta de ativos.

   Para adicionar ativos à coleção, navegue até a interface do usuário do Assets. Para obter detalhes, consulte [Adicionar ativos a uma coleção](#add-assets-to-a-collection).

### Criar coleções usando a zona de destino {#create-collections-using-dropzone}

Você pode arrastar ativos da interface do Assets para uma coleção. Também é possível criar uma cópia de uma coleção e arrastar os ativos para lá.

1. Na interface do usuário do Assets, selecione os ativos que deseja adicionar a uma coleção.
1. Arraste os ativos para a zona **[!UICONTROL Soltar na coleção]**. Como alternativa, selecione o ícone **[!UICONTROL Para Coleção]** na barra de ferramentas.
1. Na página **[!UICONTROL Adicionar à Coleção]**, selecione o ícone **[!UICONTROL Criar Coleção]** na barra de ferramentas. Para adicionar os ativos a uma coleção existente, selecione-a na página e selecione **[!UICONTROL Adicionar]**. Por padrão, a coleção atualizada mais recentemente é selecionada.
1. Na caixa de diálogo **[!UICONTROL Criar nova coleção]**, especifique o nome da coleção. Se quiser que a coleção seja acessível a todos os usuários, selecione **[!UICONTROL Coleção pública]**.
1. Selecione **[!UICONTROL Continuar]** para criar a coleção.

### Criar uma coleção inteligente {#create-a-smart-collection}

Uma coleção inteligente usa critérios de pesquisa para preencher ativos dinamicamente. Você pode criar uma coleção inteligente usando somente arquivos e não pastas ou arquivos e pastas.

1. Navegue até a interface do Assets e selecione o ícone **[!UICONTROL Pesquisar]**.
1. Insira a palavra-chave de pesquisa na caixa Pesquisa Omni e selecione `Enter`. Selecione o ícone GlobalNav para exibir o painel Filtros e aplicar um filtro de pesquisa do painel Pesquisar.
1. Na lista **[!UICONTROL Arquivos e pastas]**, selecione **[!UICONTROL Arquivos]**.
1. Selecione **[!UICONTROL Salvar coleção inteligente]**.
1. Especifique um nome para a coleção. Selecione **[!UICONTROL Público]** para adicionar o grupo Usuários DAM com a função de Visualizador à coleção inteligente.

   >[!NOTE]
   >
   >Se você selecionar **[!UICONTROL Público]**, a coleção inteligente ficará disponível para todos com a função Proprietário depois de criá-la. Se você cancelar a opção **[!UICONTROL Pública]**, o grupo de usuários do DAM não será mais associado à coleção inteligente.

1. Selecione **[!UICONTROL Salvar]** para criar a coleção inteligente e feche a caixa de mensagem para concluir o processo. A nova coleção inteligente também foi adicionada à lista **[!UICONTROL Pesquisas salvas]**.
O rótulo do botão **[!UICONTROL Criar seleção inteligente]** muda para **[!UICONTROL Editar seleção inteligente]**. Para editar as configurações da coleção inteligente, selecione **[!UICONTROL Arquivos]** na lista **[!UICONTROL Arquivos e pastas]**. Em seguida, selecione o botão **[!UICONTROL Editar Seleção Inteligente]**.

## Adicionar ativos a uma coleção {#add-assets-to-a-collection}

É possível adicionar ativos a uma coleção que contém uma lista de ativos ou pastas referenciados.

>[!NOTE]
>
>As coleções inteligentes usam uma consulta de pesquisa para preencher ativos. Portanto, as referências estáticas a ativos e pastas não se aplicam a eles.

1. Na interface do Assets, navegue até o local do ativo que deseja adicionar a uma coleção.
1. Selecione o ativo e o ícone **[!UICONTROL Para Coleção]** na barra de ferramentas. Como alternativa, você pode arrastar o ativo para a zona **[!UICONTROL Soltar na coleção]**. Solte o botão do mouse quando a zona de soltar se tornar ativa e seu rótulo mudar para **[!UICONTROL Soltar para Adicionar]**.
1. Na página **[!UICONTROL Adicionar à coleção]**, selecione a coleção à qual deseja adicionar o ativo.
1. Selecione **[!UICONTROL Adicionar]** e feche a mensagem de confirmação. O ativo é adicionado à coleção.

## Editar uma coleção inteligente {#edit-a-smart-collection}

As coleções inteligentes são criadas salvando uma pesquisa para que você possa alterar o conteúdo modificando os parâmetros de pesquisa da [pesquisa salva](#saved-searches).

1. Na interface do usuário do Assets, selecione o ícone **[!UICONTROL Pesquisar]** na barra de ferramentas.
1. Com o cursor na caixa Omnisearch, selecione a chave `Enter`.
1. Selecione o ícone GlobalNav para exibir o painel Filtros.
1. Na lista **[!UICONTROL Pesquisas salvas]**, selecione a coleção inteligente que deseja modificar. O painel Pesquisar exibe os filtros configurados para a pesquisa salva.
1. Na lista **[!UICONTROL Arquivos e pastas]**, selecione **[!UICONTROL Arquivos]**.
1. Modifique um ou mais filtros, conforme necessário. Selecione **[!UICONTROL Editar coleção inteligente]**. Também é possível editar o nome da coleção inteligente.
1. Selecione **[!UICONTROL Salvar]**. A caixa de diálogo **[!UICONTROL Editar coleção inteligente]** é exibida.
1. Selecione **[!UICONTROL Substituir]** para substituir a coleção inteligente original pela coleção editada. Como alternativa, selecione **[!UICONTROL Salvar como]** para salvar a coleção editada separadamente.
1. Na caixa de diálogo de confirmação, selecione **[!UICONTROL Salvar]** para concluir o processo.

## Exibir e editar metadados da coleção {#view-and-edit-collection-metadata}

Os metadados da coleção incluem dados sobre a coleção, incluindo tags adicionadas.

1. No console Coleções, selecione uma coleção e selecione o ícone **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página **[!UICONTROL Metadados da coleção]**, visualize os metadados da coleção nas guias **[!UICONTROL Básico]** e **Avançado**.
1. Modifique os metadados, conforme necessário, e selecione **[!UICONTROL Salvar e fechar]** na barra de ferramentas para salvar as alterações.

### Editar metadados da coleção em massa {#edit-collection-metadata-in-bulk}

É possível editar os metadados de várias coleções simultaneamente. Essa funcionalidade ajuda a replicar rapidamente metadados comuns em várias coleções.

1. No console Coleções, selecione duas ou mais coleções para as quais deseja editar metadados.
1. Na barra de ferramentas, selecione o ícone **[!UICONTROL Propriedades]**.
1. Na página **[!UICONTROL Metadados da coleção]**, edite os metadados nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**, conforme necessário.
1. Selecione **[!UICONTROL Salvar e fechar]** na barra de ferramentas e feche a caixa de diálogo de confirmação para concluir o processo.
1. Para anexar os novos metadados aos existentes, selecione o **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Selecione **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >O Modo anexar funciona somente para campos que podem conter vários valores. Em campos que podem conter apenas um valor, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o **[!UICONTROL Modo anexar]**.

## Pesquisar {#searching}

O recurso Pesquisar em Coleções oferece suporte a [Pesquisar coleções](#search-collections) e [Pesquisar ativos em uma Coleção](#search-within-collections).

### Pesquisar coleções {#search-collections}

Você pode pesquisar coleções no console Coleções. Quando você pesquisa com palavras-chave na caixa Omnisearch, o [!DNL Experience Manager Assets] pesquisa por nomes de coleções, metadados e as tags adicionadas às coleções.

Se você pesquisar por coleções no nível superior, somente coleções individuais serão retornadas nos resultados da pesquisa. O Assets ou as pastas dentro das coleções são excluídos. Em todos os outros casos (por exemplo, em uma coleção individual ou em uma hierarquia de pastas), todos os ativos, pastas e coleções relevantes são retornados.

### Pesquisar em coleções {#search-within-collections}

No console Coleções, selecione uma coleção para abri-la.

Em uma coleção, a pesquisa do [!DNL Experience Manager] está restrita aos ativos (e suas marcas e metadados) dentro da coleção que você está visualizando. Quando você pesquisa em uma pasta, todos os ativos e pastas secundárias correspondentes na pasta atual são retornados. Quando você pesquisa em uma coleção, somente ativos, pastas e outras coleções correspondentes que são membros diretos da coleção são retornados.

## Editar configurações da coleção {#edit-collection-settings}

É possível editar as configurações da coleção, como título e descrição, ou adicionar membros a uma coleção.

1. Selecione uma coleção e o ícone **[!UICONTROL Configurações]** na barra de ferramentas. Como alternativa, use a ação rápida **[!UICONTROL Configurações]** da miniatura da coleção.
1. Modifique as configurações da coleção na página **[!UICONTROL Configurações da coleção]**. Por exemplo, modifique o título da coleção, as descrições, os membros e as permissões, conforme discutido em [Adicionar coleções](#create-a-collection).
1. Selecione **[!UICONTROL Salvar]** para salvar as alterações.

## Excluir uma coleção {#delete-a-collection}

1. No console Coleções, selecione uma ou mais coleções e selecione o ícone Excluir na barra de ferramentas.
1. Na caixa de diálogo, selecione **[!UICONTROL Excluir]** para confirmar a ação de exclusão.

   >[!NOTE]
   >
   >Também é possível excluir coleções inteligentes ao [excluir pesquisas salvas](#saved-searches).

## Baixar uma coleção {#download-a-collection}

Ao baixar uma coleção, toda a hierarquia de ativos dentro dela é baixada, incluindo pastas e coleções secundárias.

1. No console Coleções, selecione uma ou mais coleções para baixar.
1. Na barra de ferramentas, selecione o ícone de download.
1. Na caixa de diálogo **[!UICONTROL Download]**, selecione **[!UICONTROL Download]**. Para baixar as representações dos ativos dentro da coleção, selecione **[!UICONTROL Representações]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   Quando você seleciona uma coleção para download, a hierarquia completa de pastas na coleção é baixada. Para incluir cada coleção baixada (incluindo ativos em coleções secundárias aninhadas na coleção principal) em uma pasta individual, selecione **[!UICONTROL Criar pasta separada para cada ativo]**.

## Editar propriedades de metadados de várias coleções {#editing-metadata-properties-of-multiple-collections}

O Adobe Enterprise Manager Assets permite que você edite os metadados de muitas coleções em massa. Use a página [!UICONTROL Propriedades] para executar alterações de metadados em várias coleções, por exemplo, alterar propriedades de metadados para um valor comum ou adicionar ou modificar marcas.

Para personalizar a página de metadados [!UICONTROL Propriedades], incluindo adição, modificação e exclusão de propriedades de metadados, use o Editor de esquemas.

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma coleção. Para os ativos que estão disponíveis em pastas ou correspondem a um critério comum, é possível [atualizar os metadados em massa após a pesquisa](/help/assets/search-assets.md#metadata-updates).

1. No console de coleções, selecione as coleções que deseja editar.
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]** para abrir a página [!UICONTROL Propriedades] das coleções selecionadas.
1. Modifique as propriedades de metadados das coleções selecionadas nas várias guias.

   >[!NOTE]
   >
   >Os metadados adicionados às coleções selecionadas substituem os metadados anteriores dessas coleções, exceto as tags. Todas as marcas adicionadas no campo **[!UICONTROL Marcas]** são anexadas à lista existente de marcas nos metadados.

1. Para exibir as propriedades de metadados de uma coleção específica, cancele a seleção das coleções restantes na lista de coleções. Os campos do editor de metadados são preenchidos com os metadados da coleção específica.

   >[!NOTE]
   >
   >* Na página de propriedades da coleção, é possível remover coleções da lista de coleções ao cancelar a seleção. A lista de coleções tem todas as coleções selecionadas por padrão. Os metadados das coleções removidas não são atualizados.
   >* Na parte superior da lista, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre a seleção das coleções e a limpeza da lista.

1. Salve as alterações.

## Criar coleções aninhadas {#create-nested-collections}

Você pode adicionar uma coleção a outra coleção, criando assim uma coleção aninhada.

1. No console Coleções, selecione a coleção ou o grupo de coleções desejado e selecione **[!UICONTROL Para coleção]** na barra de ferramentas.
1. Na página **[!UICONTROL Adicionar à coleção]**, selecione a coleção na qual adicionar a coleção.

   >[!NOTE]
   >
   >A coleção atualizada mais recentemente é selecionada por padrão na página **[!UICONTROL Adicionar à coleção]**.

1. Selecione **[!UICONTROL Adicionar]**. Uma mensagem confirma que a coleção é adicionada à coleção de destino na página **[!UICONTROL Selecionar destino]**. Feche a mensagem para concluir o processo.

>[!NOTE]
>
>As coleções inteligentes não podem ser aninhadas. Em outras palavras, as coleções inteligentes não podem conter nenhuma outra coleção.

## Pesquisas salvas {#saved-searches}

Na interface do usuário do Assets, pesquise ou filtre ativos com base em determinadas regras, critérios de pesquisa ou aspectos de pesquisa personalizados. Se salvá-los como **[!UICONTROL Pesquisas salvas]**, você poderá acessá-los posteriormente na lista **[!UICONTROL Pesquisas salvas]** do painel Filtro. Criar uma pesquisa salva também cria uma coleção inteligente.

Pesquisas salvas são criadas quando você cria uma coleção inteligente. As coleções inteligentes são adicionadas automaticamente à lista **[!UICONTROL Pesquisas salvas]**. A consulta Pesquisas Salvas da coleção é salva na propriedade `dam:query` no CRXDE no local relativo `/content/dam/collections/`. Não há limites para as pesquisas que você pode salvar e nas pesquisas salvas exibidas na lista.

>[!NOTE]
>
>Você pode compartilhar coleções inteligentes da mesma maneira que compartilha coleções estáticas.

Editar pesquisas salvas é o mesmo que editar coleções inteligentes. Para obter detalhes, consulte [Editar uma coleção inteligente](#edit-a-smart-collection).

Para excluir pesquisas salvas, siga estas etapas:

1. Na interface do usuário do Assets, selecione o ícone de pesquisa na barra de ferramentas.

1. Com o cursor no campo Omnisearch, selecione a chave `Enter`.
1. Selecione o ícone GlobalNav para exibir o painel Filtros.
1. Na lista **[!UICONTROL Pesquisas salvas]**, selecione **[!UICONTROL Excluir]** ao lado da coleção inteligente que deseja excluir.
1. Na caixa de diálogo, selecione **[!UICONTROL Excluir]** para excluir a pesquisa salva.

## Executar um fluxo de trabalho em uma coleção {#run-a-workflow-on-a-collection}

Você pode executar um fluxo de trabalho para os ativos em uma coleção. Se a coleção contiver coleções aninhadas, o fluxo de trabalho também será executado nos ativos dentro das coleções aninhadas. No entanto, se a coleção e a coleção aninhada contiverem ativos duplicados, o fluxo de trabalho será executado apenas uma vez para esses ativos.

1. No console Coleções, selecione uma coleção na qual deseja executar um fluxo de trabalho.
1. Selecione o ícone GlobalNav e escolha **[!UICONTROL Linha do tempo]** na lista.
1. Na linha do tempo, selecione o ícone Cursor na parte inferior e selecione **[!UICONTROL Iniciar Fluxo de Trabalho]**.
1. Na seção **[!UICONTROL Iniciar fluxo de trabalho]**, selecione um modelo de fluxo de trabalho da lista. Por exemplo, selecione o modelo **[!UICONTROL Atualizar ativo DAM]**.
1. Insira um título para o fluxo de trabalho e selecione **[!UICONTROL Iniciar]**.
1. Na caixa de diálogo, selecione **[!UICONTROL Continuar]**. O fluxo de trabalho é executado em todos os ativos na coleção.

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
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Criar uma tarefa de revisão para Coleções](/help/assets/bulk-approval.md)
