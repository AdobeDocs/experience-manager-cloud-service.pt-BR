---
title: Gerenciar coleções de ativos digitais
description: Entenda o conceito de coleção no Adobe Experience Manager Assets. Saiba como coletar, gerenciar, editar e coleções com outros usuários.
contentOwner: AG
mini-toc-levels: 1
feature: Collections,Asset Management
role: User
exl-id: b0798adc-56a4-4577-b4ee-8d1fca3bff09
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '2447'
ht-degree: 23%

---

# Gerenciar coleções {#manage-collections}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-collections.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Uma coleção é um conjunto de ativos no Adobe Experience Manager Assets. Use coleções para compartilhar ativos entre usuários. O conjunto pode ser uma coleção estática ou dinâmica baseada em resultados de pesquisa.

Diferente de pastas, uma coleção pode incluir ativos de locais diferentes. Você pode compartilhar coleções com vários usuários aos quais são atribuídos diferentes níveis de privilégios, incluindo exibição, edição e assim por diante.

Você pode compartilhar várias coleções com um usuário. Cada coleção contém referências a ativos. A integridade referencial dos ativos é mantida entre as coleções.

As coleções são dos seguintes tipos, com base na maneira como coletam ativos:

* Uma coleção que contém uma lista de referência estática de ativos, pastas e outras coleções.

* Uma coleção inteligente que inclui dinamicamente ativos com base em critérios de pesquisa.

## Acesse o console Coleções {#navigate-the-collections-console}

Para abrir o **[!UICONTROL Coleções]** console:

Para abrir o **[!UICONTROL Coleções]**, toque ou clique no logotipo do Experience Manager. Na página de navegação, vá para **[!UICONTROL Ativos]** > **[!UICONTROL Coleções]**.

## Criar uma coleção {#create-a-collection}

Você pode criar uma coleção com [referências estáticas](#create-a-collection-with-static-references) ou com base em [filtro baseado em critérios de pesquisa](#create-a-smart-collection). Você também pode criar uma coleção de um lightbox.

### Criar uma coleção com referências estáticas {#create-a-collection-with-static-references}

Você pode criar uma coleção com referências estáticas, por exemplo, uma coleção com referências a ativos, pastas, coleções, conjuntos de rotação e conjuntos de imagens.

1. Navegue até o **[!UICONTROL Coleções]** console.
1. Na barra de ferramentas, toque/clique **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar coleção]** , insira um título e uma descrição opcional para a coleção.
1. Adicione membros à coleção e atribua as permissões apropriadas. Como alternativa, selecione **[!UICONTROL Coleção pública]** para permitir que todos os usuários acessem a coleção.

   >[!NOTE]
   >
   >Para permitir que os membros compartilhem coleções com outros usuários, forneça a variável `dam-users` permissões de leitura de grupo no caminho `home/users`. Conceder permissão aos usuários em `/content/dam/collections` local para permitir que os usuários visualizem as Coleções em listas pop-up. Como alternativa, faça do usuário parte de `dam-users` grupo.

1. (Opcional) Adicione uma imagem em miniatura para a coleção.
1. Toque/clique em **[!UICONTROL Criar]** e em **[!UICONTROL OK]** para fechar a caixa de diálogo. Uma coleção com o título e as propriedades especificadas é aberta no console Coleções.

   >[!NOTE]
   >
   >O Experience Manager Assets permite criar tarefas de revisão para uma coleção semelhante à forma como você cria tarefas de revisão para uma pasta de ativos.

   Para adicionar ativos à coleção, navegue até a interface do usuário Ativos . Para obter detalhes, consulte [Adicionar ativos a uma coleção](#add-assets-to-a-collection).

### Criar coleções usando o dropzone {#create-collections-using-dropzone}

Você pode arrastar ativos da interface do usuário do Assets para uma coleção. Você também pode criar uma cópia de uma coleção e arrastar os ativos para lá.

1. Na interface do usuário do Assets, selecione os ativos que deseja adicionar a uma coleção.
1. Arraste os ativos para a **[!UICONTROL Quebra na coleção]** zona. Como alternativa, toque/clique no botão **[!UICONTROL Para Coleção]** ícone na barra de ferramentas.
1. Na página **[!UICONTROL Adicionar à coleção]**, toque/clique no ícone **[!UICONTROL Criar coleção]** na barra de ferramentas. Se desejar adicionar os ativos a uma coleção existente, selecione-a na página e toque/clique em **[!UICONTROL Adicionar]**. Por padrão, a coleção atualizada mais recentemente é selecionada.
1. Na caixa de diálogo **[!UICONTROL Criar nova coleção]**, especifique o nome da coleção. Se quiser que a coleção seja acessível a todos os usuários, selecione **[!UICONTROL Coleção pública]**.
1. Toque/clique **[!UICONTROL Continuar]** para criar a coleção.

### Criar uma coleção inteligente {#create-a-smart-collection}

Uma coleção inteligente usa critérios de pesquisa para preencher dinamicamente ativos. Você pode criar uma Coleção inteligente usando somente arquivos e não pastas ou arquivos e pastas.

1. Navegue até a interface do usuário do Assets e toque/clique no ícone **[!UICONTROL Pesquisar]**.
1. Digite a palavra-chave de pesquisa na caixa Pesquisa Omni e selecione `Enter`. Toque/clique no ícone de Navegação global para exibir o painel Filtros e aplique um filtro de pesquisa no painel Pesquisar.
1. No **[!UICONTROL Arquivos e pastas]** lista, selecione **[!UICONTROL Arquivos]**.
1. Toque/clique **[!UICONTROL Salvar coleção inteligente]**.
1. Especifique um nome para a coleção. Selecionar **[!UICONTROL Público]** para adicionar o grupo Usuários de DAM com a função Visualizador à coleção inteligente.

   >[!NOTE]
   >
   >Se você selecionar **[!UICONTROL Público]**, a coleção inteligente fica disponível para todos com a função Proprietário depois de criá-la. Se você cancelar a **[!UICONTROL Público]** , o grupo de usuários do DAM não está mais associado à coleção inteligente.

1. Toque/clique em **[!UICONTROL Salvar]** para criar a coleção inteligente e feche a caixa de mensagem para concluir o processo. A nova coleção inteligente também é adicionada à lista **[!UICONTROL Pesquisas salvas]**.
O rótulo do botão **[!UICONTROL Criar seleção inteligente]** muda para **[!UICONTROL Editar seleção inteligente]**. Para editar as configurações da coleção inteligente, selecione **[!UICONTROL Arquivos]** na lista **[!UICONTROL Arquivos e pastas]**. Em seguida, toque/clique no botão **[!UICONTROL Editar seleção inteligente]**.

## Adicionar ativos a uma coleção {#add-assets-to-a-collection}

Você pode adicionar ativos a uma coleção que contém uma lista de ativos ou pastas referenciados.

>[!NOTE]
>
>As coleções inteligentes usam um query de pesquisa para preencher ativos. Portanto, referências estáticas a ativos e pastas não se aplicam a elas.

1. Na interface do usuário do Assets, navegue até o local do ativo que deseja adicionar a uma coleção.
1. Selecione o ativo e toque/clique no botão **[!UICONTROL Para Coleção]** ícone na barra de ferramentas. Como alternativa, você pode arrastar o ativo para a **[!UICONTROL Quebra na coleção]** zona. Solte o botão do mouse quando a área solta se tornar ativa e seu rótulo mudar para **[!UICONTROL Soltar para adicionar]**.
1. No **[!UICONTROL Adicionar à coleção]** selecione a coleção à qual deseja adicionar o ativo.
1. Toque/clique **[!UICONTROL Adicionar]** e então feche a mensagem de confirmação. O ativo é adicionado à coleção.

## Editar uma coleção inteligente {#edit-a-smart-collection}

As coleções inteligentes são criadas salvando uma pesquisa para que você possa alterar seu conteúdo modificando os parâmetros de pesquisa do [pesquisa salva](#saved-searches).

1. Na interface do usuário do Assets, toque/clique no botão **[!UICONTROL Pesquisar]** ícone na barra de ferramentas.
1. Com o cursor na caixa Omnisearch, selecione o `Enter` chave.
1. Toque/clique no ícone de Navegação global para exibir o painel Filtros .
1. Na lista **[!UICONTROL Pesquisas salvas]**, selecione a coleção inteligente que deseja modificar. O painel Pesquisar exibe os filtros configurados para a pesquisa salva.
1. No **[!UICONTROL Arquivos e pastas]** lista, selecione **[!UICONTROL Arquivos]**.
1. Modifique um ou mais filtros, conforme necessário. Toque/clique **[!UICONTROL Editar coleção inteligente]**. Também é possível editar o nome da coleção inteligente.
1. Toque/clique **[!UICONTROL Salvar]**. O **[!UICONTROL Editar coleção inteligente]** será exibida.
1. Toque/clique **[!UICONTROL Substituir]** para substituir a coleção inteligente original pela coleção editada. Como alternativa, selecione **[!UICONTROL Salvar como]** para salvar a coleção editada separadamente.
1. Na caixa de diálogo de confirmação, toque/clique em **[!UICONTROL Salvar]** para concluir o processo.

## Exibir e editar metadados da coleção {#view-and-edit-collection-metadata}

Os metadados da coleção incluem dados sobre a coleção, incluindo quaisquer tags adicionadas.

1. No console Coleções , selecione uma coleção e toque/clique no link **[!UICONTROL Propriedades]** ícone na barra de ferramentas.
1. Na página **[!UICONTROL Metadados da coleção]**, visualize os metadados da coleção nas guias **[!UICONTROL Básico]** e **Avançado**.
1. Modifique os metadados, conforme necessário, e toque/clique **[!UICONTROL Salvar e fechar]** na barra de ferramentas para salvar as alterações.

### Editar metadados de coleção em massa {#edit-collection-metadata-in-bulk}

Você pode editar os metadados de várias coleções simultaneamente. Essa funcionalidade ajuda você a replicar rapidamente metadados comuns em várias coleções.

1. No console Coleções , selecione duas ou mais coleções para as quais deseja editar metadados.
1. Na barra de ferramentas, toque/clique no botão **[!UICONTROL Propriedades]** ícone .
1. Na página **[!UICONTROL Metadados da coleção]**, edite os metadados nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**, conforme necessário.
1. Toque/clique **[!UICONTROL Salvar e fechar]** na barra de ferramentas e feche a caixa de diálogo de confirmação para concluir o processo.
1. Para anexar os novos metadados aos existentes, selecione o **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Toque/clique em **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >O Modo anexar funciona somente para campos que podem conter vários valores. Em campos que podem conter apenas um valor, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o **[!UICONTROL Modo anexar]**.

## Pesquisar {#searching}

O recurso Pesquisar em Coleções suporta ambos [Pesquisar por coleções](#search-collections) e [Pesquisar ativos em uma coleção](#search-within-collections).

### Pesquisar coleções {#search-collections}

Você pode pesquisar coleções no console Coleções. Ao pesquisar com palavras-chave na caixa Omnisearch, [!DNL Experience Manager Assets] pesquisa nomes de coleção, metadados e as tags adicionadas às coleções.

Se você pesquisar por coleções do nível superior, somente coleções individuais serão retornadas nos resultados da pesquisa. Os ativos ou pastas nas coleções são excluídos. Em todos os outros casos (por exemplo, em uma coleção individual ou em uma hierarquia de pasta), todos os ativos, pastas e coleções relevantes são retornados.

### Pesquisar em Coleções {#search-within-collections}

No console Coleções , toque/clique em uma coleção para abri-la.

Em uma coleção, [!DNL Experience Manager] a pesquisa é restrita aos ativos (e suas tags e metadados) dentro da coleção que você está visualizando. Ao pesquisar em uma pasta, todos os ativos e pastas filhas correspondentes na pasta atual são retornados. Ao pesquisar em uma coleção, somente os ativos, pastas e outras coleções correspondentes que são membros diretos da coleção são retornados.

## Editar configurações de coleção {#edit-collection-settings}

É possível editar configurações da coleção, como título e descrição, ou adicionar membros a uma coleção.

1. Selecione uma coleção e toque/clique no botão **[!UICONTROL Configurações]** na barra de ferramentas. Como alternativa, use o **[!UICONTROL Configurações]** ação rápida da miniatura da coleção.
1. Modifique as configurações da coleção na página **[!UICONTROL Configurações da coleção]**. Por exemplo, modifique o título da coleção, as descrições, os membros e as permissões, conforme discutido em [Adicionar coleções](#create-a-collection).
1. Toque/clique **[!UICONTROL Salvar]** para salvar as alterações.

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
1. No **[!UICONTROL Baixar]** , toque/clique **[!UICONTROL Baixar]**. Se desejar baixar as representações dos ativos na coleção, selecione **[!UICONTROL Representações]**. <!-- Select the **[!UICONTROL Email]** option to send an email notification to the owner of the collection. -->

   Ao selecionar uma coleção para baixar, a hierarquia completa da pasta na coleção é baixada. Para incluir cada coleção que você baixar (incluindo ativos em coleções secundárias aninhadas sob a coleção pai) em uma pasta individual, selecione **[!UICONTROL Criar uma pasta separada para cada ativo]**.

## Editar propriedades de metadados de várias coleções {#editing-metadata-properties-of-multiple-collections}

Os Ativos do Adobe Enterprise Manager permitem editar os metadados de muitas coleções em massa. Use o [!UICONTROL Propriedades] para executar alterações nos metadados em várias coleções, por exemplo, altere as propriedades dos metadados para um valor comum ou adicione ou modifique tags.

Como personalizar os metadados [!UICONTROL Propriedades] , incluindo adicionar, modificar, excluir propriedades de metadados, use o editor de Esquema .

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma coleção. Para os ativos que estão disponíveis em pastas ou que correspondem a um critério comum, é possível [atualização em massa dos metadados após a pesquisa](/help/assets/search-assets.md#metadata-updates).

1. No console Coleções, selecione as coleções que deseja editar.
1. Na barra de ferramentas, toque/clique **[!UICONTROL Propriedades]** para abrir o [!UICONTROL Propriedades] para as coleções selecionadas.
1. Modifique as propriedades de metadados para coleções selecionadas nas várias guias.

   >[!NOTE]
   >
   >Os metadados adicionados às coleções selecionadas substituem os metadados anteriores para essas coleções, exceto para tags. Qualquer tag adicionada na **[!UICONTROL Tags]** , são anexadas à lista existente de tags nos metadados.

1. Para exibir as propriedades de metadados de uma coleção específica, cancele a seleção das coleções restantes na lista de coleções. Os campos do editor de metadados são preenchidos com os metadados para a coleção específica.

   >[!NOTE]
   >
   >* Na página de propriedades da coleção, é possível remover coleções da lista de coleções cancelando a seleção. A lista de coleções tem todas as coleções selecionadas por padrão. Os metadados das coleções que você remover não são atualizados.
   >* Na parte superior da lista, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre selecionar as coleções e limpar a lista.


1. Salve as alterações.

## Criar coleções aninhadas {#create-nested-collections}

Você pode adicionar uma coleção a outra coleção, criando uma coleção aninhada.

1. No console Coleções , selecione a coleção ou o grupo de coleções desejado e toque ou clique em **[!UICONTROL Para Coleção]** na barra de ferramentas.
1. No **[!UICONTROL Adicionar à coleção]** selecione a coleção na qual deseja adicionar a coleção.

   >[!NOTE]
   >
   >A coleção atualizada mais recentemente é selecionada por padrão no **[!UICONTROL Adicionar à coleção]** página.

1. Toque/clique **[!UICONTROL Adicionar]**. Uma mensagem confirma que a coleção é adicionada à coleção de público-alvo na **[!UICONTROL Selecionar destino]** página. Feche a mensagem para concluir o processo.

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

1. Com o cursor no campo Omnisearch , selecione o `Enter` chave.
1. Clique ou toque no ícone de Navegação global para exibir o painel Filtros .
1. Na lista **[!UICONTROL Pesquisas salvas]**, toque/clique em **[!UICONTROL Excluir]** ao lado da coleção inteligente que deseja excluir.
1. Na caixa de diálogo, toque/clique em **[!UICONTROL Excluir]** para excluir a pesquisa salva.

## Executar um fluxo de trabalho em uma coleção {#run-a-workflow-on-a-collection}

Você pode executar um fluxo de trabalho para os ativos em uma coleção. Se a coleção contiver coleções aninhadas, o fluxo de trabalho também será executado nos ativos dentro das coleções aninhadas. No entanto, se a coleção e a coleção aninhada contiverem ativos duplicados, o fluxo de trabalho será executado apenas uma vez para esses ativos.

1. No console Coleções , selecione uma coleção em que deseja executar um fluxo de trabalho.
1. Toque/clique no ícone de Navegação global e escolha **[!UICONTROL Linha do tempo]** na lista.
1. Na linha do tempo, selecione ou toque no ícone Cursor na parte inferior e, em seguida, toque/clique **[!UICONTROL Iniciar fluxo de trabalho]**.
1. Na seção **[!UICONTROL Iniciar fluxo de trabalho]**, selecione um modelo de fluxo de trabalho da lista. Por exemplo, selecione o modelo **[!UICONTROL Atualizar ativo DAM]**.
1. Insira um título para o fluxo de trabalho e toque/clique em **[!UICONTROL Iniciar]**.
1. Na caixa de diálogo, toque/clique em **[!UICONTROL Continue]**. O fluxo de trabalho é executado em todos os ativos na coleção.

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

>[!MORELIKETHIS]
>
>* [Criar uma tarefa de revisão para Coleções](/help/assets/bulk-approval.md)

