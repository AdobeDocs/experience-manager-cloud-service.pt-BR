---
title: Organize seus ativos digitais
description: Mover, excluir, copiar, renomear, atualizar e criar versões de seus ativos no [!DNL Assets view].
role: User, Leader
contentOwner: AG
exl-id: 2459d482-828b-4410-810c-ac55ef0a2119
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: fb7ce7dbb58be9fef5ab087441457770828d73c8
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 64%

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

### Exibir e comparar versões de um ativo {#view-and-compare-versions}

Faça upload de uma cópia duplicada ou modificada de um ativo, para criar suas versões. O controle de versão permite rastrear as modificações em um ativo ao longo do tempo e reverter para uma versão anterior, se necessário.

Para exibir e comparar versões:

1. Navegue até a página de detalhes do ativo.
1. Clique em ![Versões](/help/assets/assets/Clock.svg) no painel direito para exibir o painel **[!UICONTROL Versões]**. As miniaturas do ativo original e suas versões carregadas são exibidas nesse painel.
1. Selecione uma versão no painel para visualizá-la na área de visualização.
1. Selecione qualquer versão diferente da mais recente e clique em **[!UICONTROL Tornar a mais recente]** para defini-la como a versão mais recente.
1. Arraste o controle deslizante na visualização para a esquerda e para a direita para ver rapidamente a versão selecionada de uma imagem e sua versão mais recente em uma única visualização. Isso permite comparar rapidamente a versão selecionada da imagem com sua versão mais recente.

   >[!NOTE]
   >
   > A comparação de versões é habilitada somente para ativos de imagem.

   ![comparar versões do ativo](/help/assets/assets/version-compare2.png)

<!-- old content
To view versions, open an asset's preview and click **[!UICONTROL Versions]** ![Versions icon](assets/do-not-localize/versions-clock-icon.png) from the right sidebar. To preview a specific version, select it. To revert to it, click **[!UICONTROL Make Latest]**. 
-->

Selecione a versão mais recente e clique em **[!UICONTROL Nova versão]** para carregar uma nova cópia do ativo a partir do sistema de arquivos local para criar uma versão do ativo.

<!-- old content
You can also create versions from the versions timeline. Select the latest version, click **[!UICONTROL New Version]**, and upload a new copy of the asset from your local file system.

![View versions of an asset](assets/view-asset-versions1.png)

*Figure: View versions of an asset, revert to a previous version, or upload another new version.* 
-->

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
Se você tiver o Dynamic Media com recursos do OpenAPI provisionados para o seu ambiente, o Experience Manager Assets gera um URL público assim que você marca o ativo como `Approved`.

   >[!VIDEO](https://video.tv.adobe.com/v/342495)



### Definir público alvo de aprovação {#set-approval-target}

A exibição do Assets permite publicar ativos aprovados no Dynamic Media com recursos OpenAPI, Content Hub ou ambos com base no valor definido no campo **Destino de aprovação**, disponível na página Detalhes do ativo.

Para definir o público alvo de aprovação:

1. Selecione o ativo e clique em **[!UICONTROL Detalhes]** na barra de ferramentas.

1. Na guia **[!UICONTROL Básico]**, selecione o status do ativo na lista suspensa **[!UICONTROL Status]**. Os valores possíveis incluem Aprovado, Rejeitado e Sem status (padrão).

1. Se você selecionar **Aprovado** na etapa 2, selecione um destino de aprovação. Os valores possíveis incluem Delivery e Content Hub.

   * **Delivery** é a opção padrão selecionada no menu suspenso e publica o ativo no [Dynamic Media com OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) e no [Content Hub](/help/assets/product-overview.md), se ambos estiverem habilitados para Experience Manager Assets.

   * Selecionar **Content Hub** publica o ativo apenas no Content Hub. O Content Hub é exibido como uma opção somente se estiver ativado para o Experience Manager Assets.

   * Se você não selecionar uma opção na lista suspensa, a opção padrão ativada para o ambiente do AEM as a Cloud Service será aplicada automaticamente ao ativo.


   Para obter mais informações sobre as opções disponíveis, consulte [Destino de aprovação padrão e destinos de publicação para ativos aprovados](#default-approval-target-options-publish-destinations).

   ![Status de aprovação](/help/assets/assets/approval-status-delivery.png)

1. Especifique outras propriedades do ativo e clique em **[!UICONTROL Salvar]**.

Alguns pontos adicionais a serem observados incluem:

* Quando você não estiver usando o formulário de metadados padrão e não puder exibir o campo **[!UICONTROL Destino da Aprovação]**, [edite o formulário de metadados](/help/assets/metadata-assets-view.md#metadata-forms) para arrastar o campo **[!UICONTROL Aprovação para]** dos componentes disponíveis para o formulário de metadados e clique em **[!UICONTROL Salvar]**.

* Ao selecionar o público alvo de aprovação como `Content Hub` usando a exibição do Assets, os ativos são disponibilizados no Content Hub para os usuários que fazem parte da mesma organização.

#### Destino de aprovação padrão e destinos de publicação para ativos aprovados {#default-approval-target-options-publish-destinations}

A tabela a seguir ilustra os pré-requisitos para exibição da lista suspensa `Approval Target` e do público alvo de aprovação padrão com base na habilitação do DM com OpenAPI e Content Hub no seu ambiente AEM as a Cloud Service:

| Dynamic Media com OpenAPI | Centro de conteúdo | A lista suspensa Approval Target é exibida? | Público alvo de aprovação padrão para ativos aprovados | Destino de publicação |
| --- | --- | --- | --- |---|
| Habilitado | Habilitado | Sim | Entrega | Dynamic Media com OpenAPI e Content Hub |
| Não habilitado | Habilitado | Sim | Centro de conteúdo | Centro de conteúdo |
| Habilitado | Não habilitado | Sim | Entrega | Dynamic Media com OpenAPI |
| Não habilitado | Não habilitado | Não | N/A | N/A |

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

