---
title: Organize seus ativos digitais
description: Mover, excluir, copiar, renomear, atualizar e criar versões de seus ativos no [!DNL Assets view].
role: User, Leader
contentOwner: AG
exl-id: 2459d482-828b-4410-810c-ac55ef0a2119
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 93%

---

# Gerenciar ativos {#manage-assets}

É possível realizar várias tarefas de gerenciamento de ativos digitais (DAM) facilmente usando a interface amigável do [!DNL Assets view]. Após adicionar os ativos, é possível pesquisar, baixar, mover, copiar, renomear, excluir, atualizar e editar seus ativos.

Use o [!DNL Assets view] para realizar as seguintes tarefas de gerenciamento de ativos. Quando você seleciona um ativo, as seguintes opções são exibidas na barra de ferramentas na parte superior.

![Opções da barra de ferramentas ao selecionar um ativo](assets/toolbar-image-selected.png)

*Figura: Opções disponíveis na barra de ferramentas para uma imagem selecionada.*

* ![ícone de desmarcar](assets/do-not-localize/close-icon.png) Desmarcar a seleção.

* ![ícone localizar semelhante](assets/do-not-localize/find-similar.svg) Encontrar ativos de imagem semelhantes na interface do Assets com base nos metadados e nas tags inteligentes.

* ![ícone de detalhes](assets/do-not-localize/edit-in-icon.png) Clique para visualizar um ativo e exibir os metadados detalhados. Ao visualizar, você pode exibir as versões e editar uma imagem.

* ![ícone de download](assets/do-not-localize/download-icon.png) Baixar o ativo selecionado para o sistema de arquivos local.

* ![ícone adicionar à coleção](assets/do-not-localize/add-collection.svg) Adicionar o ativo selecionado a uma coleção.

* ![ícone fixar ativos](assets/do-not-localize/pin-quick-access.svg) Fixar um ativo para poder acessá-lo rapidamente quando precisar. Todos os itens fixados são exibidos na seção **Acesso rápido** do Meu espaço de trabalho.

* ![ícone editar no Express](assets/do-not-localize/edit-e.svg) Editar uma imagem no Adobe Express integrado no Adobe Experience Manager Assets.

* ![ícone editar ativo](assets/do-not-localize/edit-e.svg) Editar a imagem usando o Adobe Express.

* ![ícone compartilhar link do ativo](assets/do-not-localize/share-link.svg) Compartilhar links para um ativo com outras pessoas, para que possam acessá-lo e baixá-lo.

* ![ícone de excluir](assets/do-not-localize/delete-icon.png) Excluir o ativo ou a pasta selecionada.

* ![ícone de copiar](assets/do-not-localize/copy-icon.png) Copiar o arquivo ou pasta selecionada.

* ![ícone de mover](assets/do-not-localize/move-icon.png) Mover o ativo ou pasta selecionada para um local diferente na hierarquia do repositório.

* ![ícone de renomear](assets/do-not-localize/rename-icon.png) Renomear o ativo ou a pasta selecionada. Use um nome exclusivo, caso contrário, a renomeação falhará com um aviso. Você pode tentar novamente com um novo nome.
Além disso, é possível clicar no título de um ativo ou de uma pasta para renomeá-lo. Insira o novo texto na caixa de texto **Renomear ativo** e clique em **Salvar**. Esse recurso está disponível nas exibições em grade, galeria, cascata e lista.

* ![ícone de exibição em cascata](assets/do-not-localize/waterfall-view.png) [!UICONTROL Exibição em cascata].

* ![ícone copiar biblioteca](assets/do-not-localize/copy-icon.png) Adicionar um ativo à biblioteca.

* ![ícone de atribuir tarefa](assets/do-not-localize/review-delegate-icon.png) Atribuir tarefas a outros usuários para colaborar em um ativo.

* ![ícone de atribuir tarefa](assets/do-not-localize/watch-asset.svg) Monitorar as operações realizadas em um ativo.

É possível exibir as mesmas opções nas miniaturas de ativos.

![Opções na miniatura de ativos para gerenciar um ativo](assets/options-on-thumbnail.png)

O [!DNL Assets view] exibe somente as opções relevantes na barra de ferramentas que dependem do tipo do ativo selecionado.

![Opções da barra de ferramentas ao selecionar um ativo](assets/toolbar-folder-selected.png)

*Figura: Opções disponíveis na barra de ferramentas para uma pasta selecionada.*

![Opções da barra de ferramentas ao selecionar um ativo](assets/toolbar-pdf-selected.png)

*Figura: Opções disponíveis na barra de ferramentas para um arquivo PDF selecionado.*

## Baixar e distribuir ativos {#download}

É possível selecionar um ou mais ativos ou pastas, ou uma combinação dos dois, e baixar os selecionados para o sistema de arquivos local. É possível editar os ativos e carregá-los novamente ou distribuí-los fora do [!DNL Assets view]. Além disso, é possível [baixar as representações](/help/assets/add-delete-assets-view.md#renditions) de um ativo.

## Controle de versão de ativos {#versions-of-assets}

<!-- 
TBD: query for engineering: How many versions are maintained. What happens when we reach that limit? Are old versions automatically removed? -->

O [!DNL Assets view] realiza o controle de versão dos ativos quando eles são carregados novamente, após serem atualizados ou editados. Você pode visualizar o histórico de versões e a lista de versões antigas para restaurar uma versão antiga dos ativos como a versão mais recente, que pode então ser revertida para a versão anterior, se necessário. As versões de ativos são criadas nos seguintes cenários:

* Fazer upload de um novo ativo com o mesmo nome de arquivo de um ativo existente e para a mesma pasta de um ativo existente. O [!DNL Assets view] fornece a opção de substituir o ativo anterior ou de salvar o novo ativo como uma versão. Consulte [fazer upload de ativos duplicados](/help/assets/add-delete-assets-view.md).

  ![Criar versões ao fazer uploads](assets/uploads-manage-duplicates.png)

  *Figura: Ao fazer upload de um ativo com o mesmo nome de um ativo existente, você pode criar uma versão do ativo.*

* Edite uma imagem e clique em **[!UICONTROL Salvar como versão]**. Consulte [editar imagens](/help/assets/edit-images-assets-view.md).

  ![Salvar imagem editada como uma versão](assets/edit-image2.png)

  *Figura: Salvar a imagem editada como uma versão.*

* Abra as versões de um ativo existente. Clique em **[!UICONTROL Nova versão]** e faça upload de uma versão mais recente do ativo para o repositório.

  ![Opção de fazer upload de uma nova versão de um ativo do histórico de versões](assets/view-asset-versions2.png)

### Exibir versões de um ativo {#view-versions}

Ao fazer upload de uma cópia duplicada ou modificada de um ativo, você pode criar suas versões. O controle de versão permite revisar ativos históricos e reverter para uma versão anterior, caso necessário.

Para exibir as versões, abra a pré-visualização de um ativo e clique em **[!UICONTROL Versões]** ![Ícone Versões](assets/do-not-localize/versions-clock-icon.png) na barra lateral direita. Para visualizar uma versão específica, selecione-a. Para reverter para ela, clique em **[!UICONTROL Tornar a mais recente]**.

Você também pode criar versões na linha do tempo de versões. Selecione a versão mais recente, clique em **[!UICONTROL Nova versão]** e faça upload de uma nova cópia do ativo a partir do sistema de arquivos local.

![Exibir versões de um ativo](assets/view-asset-versions1.png)

*Figura: visualizar versões de um ativo, reverter para uma versão anterior ou fazer upload de outra nova versão.*

## Gerenciar o status do ativo {#manage-asset-status}

**Permissões necessárias:** `Can Edit`, `Owner` ou permissões de administrador em um ativo.

A visualização do Assets permite que você defina o status em ativos disponíveis no repositório. Defina um status de ativo para melhor administrar e gerenciar o consumo downstream de ativos digitais.

Você pode definir o seguinte status em ativos:

* Aprovado

* Rejeitado

* Sem status

### Definir status do ativo {#set-asset-status}

Para definir o status do ativo:

1. Selecione o ativo e clique em **[!UICONTROL Detalhes]** na barra de ferramentas.

1. Na guia **[!UICONTROL Básico]**, selecione o status do ativo na lista suspensa **[!UICONTROL Status]**. Os valores possíveis incluem Aprovado, Rejeitado e Sem status (padrão).

   >[!VIDEO](https://video.tv.adobe.com/v/342495)


### Definir data de expiração do ativo {#set-asset-expiration-date}

A visualização Assets também permite definir a data de expiração dos ativos disponíveis no repositório. Você pode [filtrar os resultados da pesquisa](search-assets-view.md#refine-search-results) com base no status `Expired` de um ativo. Além disso, é possível especificar um intervalo de datas para a expiração dos ativos, permitindo filtrar ainda mais os resultados da pesquisa.

Para definir a data de expiração do ativo:

1. Selecione o ativo e clique em **[!UICONTROL Detalhes]** na barra de ferramentas.

1. Na guia **[!UICONTROL Básico]**, defina a data de expiração do ativo usando o campo **[!UICONTROL Data de expiração]**.

O indicador `Expired` do cartão de ativos substitui o indicador `Approved` ou `Rejected` definido para um ativo.

Também é possível filtrar ativos com base em um status de ativo. Para obter mais informações, consulte [Pesquisar ativos no modo de exibição Assets](search-assets-view.md).

## Personalizar formulários de metadados para incluir o campo de status do ativo {#customize-asset-status-metadata-form}

**Permissões necessárias:** Administrador

A visualização Assets fornece muitos campos de metadados padrão por padrão. As organizações têm necessidades adicionais de metadados e precisam de mais campos para adicionar metadados específicos de negócios. Os formulários de metadados permitem que as empresas adicionem campos de metadados personalizados à página [!UICONTROL Detalhes] de um ativo. Os metadados específicos de negócios melhoram a governança e a descoberta de ativos.

Para mais informações sobre como adicionar campos de metadados adicionais ao formulário de metadados, consulte [Formulários de metadados](metadata-assets-view.md#metadata-forms).

**Adicionar o campo de metadados Status do ativo ao formulário**

Para adicionar o campo de metadados Status do ativo ao formulário, arraste o componente **[!UICONTROL Status do ativo]** do painel à esquerda para o formulário. A propriedade de mapeamento é preenchida automaticamente. Salve o formulário para confirmar as alterações.

**Adicionar o campo de metadados Data de expiração ao formulário**

Para adicionar o campo de metadados Data de expiração ao formulário, arraste o componente **[!UICONTROL Data]** do painel à esquerda para o formulário. Especifique **Data de expiração** como o rótulo e `pur:expirationDate` como a propriedade de mapeamento. Salve o formulário para confirmar as alterações.

## Próximas etapas {#next-steps}

* [Assista a um vídeo sobre gerenciamento de ativos no modo de exibição do Assets](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/assets-essentials/basics/managing)

* Forneça feedback sobre o produto usando a opção [!UICONTROL Feedback] disponível na interface de visualização do Assets

* Forneça feedback sobre a documentação usando as opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/pt-br?support-solution=General#support)

