---
title: Como publicar e desfazer a publicação de formulários e documentos em formulários AEM?
description: Agende a publicação e o cancelamento da publicação do Adaptive Forms. Os formulários publicados são replicados na instância de publicação.
content-type: reference
topic-tags: publish
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
feature: Adaptive Forms
role: User
hide: true
hidefromtoc: true
exl-id: 9496e4f5-ed74-4b40-b8f9-17153170af66
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 0%

---

# Publicação e cancelamento de publicação de formulários e documentos{#publishing-and-unpublishing-forms-and-documents}

O [!DNL AEM Forms] permite criar, publicar e desfazer a publicação de formulários com facilidade. O servidor [!DNL AEM Forms] fornece duas instâncias: Autor e Publish. A instância do autor é utilizada para criar e gerenciar ativos e recursos de formulários. A instância do Publish serve para manter ativos e recursos relacionados disponíveis para usuários finais.

## Ativos compatíveis   {#supported-assets-nbsp}

O [!DNL AEM Forms] oferece suporte aos seguintes tipos de ativos:

* Formulários adaptáveis
* Documentos adaptáveis
* Fragmentos de formulários adaptáveis
* Temas
* Modelos de formulário <!-- (XFA forms) -->
* PDF forms
* Documento (documentos de PDF simples)
* Conjuntos de formulários
* Recurso (imagens, esquemas e folhas de estilos)

Inicialmente, todos os ativos estão disponíveis somente na instância do Autor. Um administrador ou autor de formulário pode publicar todos os ativos, exceto recursos.

Ao selecionar um formulário e publicá-lo, seus ativos e recursos relacionados também são publicados. No entanto, os ativos dependentes não são publicados. Neste contexto, ativos e recursos relacionados são ativos que um ativo publicado usa ou refere. Ativos dependentes são ativos que se referem a um ativo publicado.

O Adaptive Forms pode utilizar algumas configurações, configurações e personalizações que não são publicadas automaticamente. É recomendável publicar ou ativar esses recursos antes de publicar um Formulário adaptável.

* Modelos editáveis de formulário adaptável
* Configurações de Cloud Service para Adobe Sign, Typekit, reCAPTCHA e Form Data Model (FDM)
* Outras configurações de serviços na nuvem são ativadas somente se o usuário tiver permissões de administrador.
* Personalizações. Isso inclui, mas não se limita a:

   * Layouts personalizados
   * Aparências personalizadas
   * Arquivo CSS - tomado como entrada na caixa de diálogo de propriedades do contêiner Formulário adaptável
   * Categoria da biblioteca do cliente - usada como entrada na caixa de diálogo de propriedades do contêiner de Formulário adaptável
   * Qualquer outra biblioteca do cliente que tenha sido incluída como parte do modelo de Formulário adaptável.
   * Caminhos de design

## Estados do ativo {#asset-states}

Um ativo pode ter os seguintes estados:

* **Publicação desfeita:** um ativo que nunca foi publicado (o estado não publicado é aplicável somente aos ativos do Forms. Os ativos do Gerenciamento de correspondências não têm um estado Não publicado.)
* **Publicado**: um ativo que foi publicado e está disponível na instância do Publish
* **Modificado**: um ativo que é modificado depois de ser publicado

## Publish e um ativo {#publish-an-asset}

1. Faça logon no servidor [!DNL AEM Forms].
1. Use um dos itens a seguir para selecionar e publicar um ativo.

   1. Mova o ponteiro sobre um ativo e selecione **[!UICONTROL Publish]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png).
   1. Siga um destes procedimentos e selecione Publish:

      * Se você estiver na exibição de cartão, selecione **[!UICONTROL Inserir seleção]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png) e selecione o ativo. O ativo está selecionado.
      * Se você estiver na exibição em lista, marque a caixa de seleção de um ativo. O ativo está selecionado.
      * Selecione um ativo para exibir seus detalhes.
      * Exiba as propriedades de um ativo tocando em Propriedades de exibição ![viewproperties](assets/viewproperties.png).

      >[!NOTE]
      >
      >Não selecione vários ativos. Não é possível publicar vários ativos de uma só vez.

1. Quando o processo do Publish é iniciado, uma caixa de diálogo de confirmação é exibida listando todos os ativos e recursos relacionados. Na caixa de diálogo que contém ativos relacionados, selecione **[!UICONTROL Publish]**. O ativo é publicado e a caixa de diálogo Publish Assets Success é exibida.

   >[!NOTE]
   >
   >Para o Forms adaptável, juntamente com os ativos relacionados, o nome da página do Formulário adaptável também é exibido.

   ![Um diálogo de confirmação com todos os ativos e recursos relacionados](assets/p4.png)

   Uma caixa de diálogo de confirmação com todos os ativos e recursos relacionados.

   >[!NOTE]
   >
   >Para o Forms Manager, se o usuário não tiver permissão para publicar os ativos listados, a ação do Publish será desativada. Um ativo que requer permissões adicionais é mostrado em vermelho.

   Depois que um ativo é publicado, as propriedades de metadados do ativo são copiadas para a instância do Publish e o status do ativo é alterado para Publicado. O status dos ativos dependentes publicados também é alterado para Publicado.

   <!-- After publishing an asset, you can use the Forms Portal to display all the assets on a web page. For more information, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md).-->

## Publish: todas as Assets do gerenciamento de correspondência {#publish-all-the-correspondence-management-assets}

O [!DNL AEM Forms] permite publicar todos os ativos do Gerenciamento de correspondências em um servidor de uma só vez. Os ativos publicados incluem todos os ativos do Gerenciamento de correspondências e dependências relacionadas.

Conclua as seguintes etapas para publicar todos os ativos do Gerenciamento de correspondências em um servidor:

1. Faça logon no servidor [!DNL AEM Forms].
1. Selecione **Adobe Experience Manager** na barra de navegação global.
1. Selecione ![ferramentas](assets/tools.png) e **Forms**.
1. Selecione a **Publish Correspondence Management Assets**.

   ![publicar-cmp-assets](assets/publish-cmp-assets.png)

   A página Assets do Publish All Correspondence Management é exibida e mostra as informações sobre a última vez que o processo Assets do Publish Correspondence Management foi tentado.

   ![publicar-detalhes-última-execução](assets/publish-last-run-details.png)

1. Selecione **Publish** e, na mensagem de confirmação, selecione **OK**.

   Após a conclusão de um processo em lote, é possível exibir os detalhes da última execução. Isso inclui informações como o logon do Administrador e se a execução do lote foi bem-sucedida ou falhou.

   >[!NOTE]
   >
   >O processo do Publish não pode ser cancelado depois de iniciado. Além disso, enquanto a operação do Publish estiver em andamento, não crie, exclua, modifique ou publique quaisquer ativos ou inicie a operação Exportar toda a correspondência do Assets Management.

## Automatizar a publicação e o cancelamento da publicação de Forms e documentos {#automate-publishing-and-unpublishing-for-forms-amp-documents}

O [!DNL AEM Forms] permite agendar a publicação e o cancelamento da publicação de ativos para o Forms e Documentos. Você pode especificar a programação no Editor de metadados. Para obter mais informações sobre o gerenciamento de metadados de formulário, consulte [Gerenciamento de metadados de formulário](manage-form-metadata.md).

Siga estas etapas para agendar a data e a hora de publicação e cancelamento da publicação dos ativos do Forms e do Documents:

1. Selecione um ativo e selecione **[!UICONTROL Exibir Propriedades]**. A página Propriedades de metadados é aberta.
1. Na página Propriedades dos metadados, selecione **[!UICONTROL Avançado]** e **[!UICONTROL Editar]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. Nos campos **[!UICONTROL Publish On Time]** e **[!UICONTROL Publish Off Time]**, selecione a data e a hora.\
   Selecione **[!UICONTROL Concluído]** ![aem6forms_check](assets/aem6forms_check.png).

## Cancelar a publicação de um ativo {#unpublish-an-asset}

1. Selecione um ativo que esteja publicado e selecione **[!UICONTROL Cancelar publicação]** ![cancelar publicação](assets/unpublish.png).
1. Use um dos itens a seguir para selecionar e cancelar a publicação de um ativo.

   1. Mova o ponteiro sobre um ativo e selecione **[!UICONTROL Cancelar publicação]** ![cancelar publicação](assets/unpublish.png).
   1. Siga um destes procedimentos e selecione desfazer publicação:

      * Se você estiver na exibição de cartão, selecione **[!UICONTROL Inserir seleção]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png) e selecione o ativo. O ativo está selecionado.

      * Se você estiver na exibição de lista, passe o mouse sobre um ativo e selecione ![selectassetcheckmark](assets/selectassetcheckmark.png). O ativo está selecionado.

      * Selecione um ativo para exibir seus detalhes.
      * Exiba as propriedades de um ativo tocando em Propriedades de exibição ![viewproperties](assets/viewproperties.png).

1. Quando o processo de cancelamento de publicação for iniciado, uma caixa de diálogo de confirmação será exibida. Selecione **[!UICONTROL Cancelar publicação]**.

   >[!NOTE]
   >
   >Somente o ativo selecionado tem a publicação cancelada e seus ativos secundários e referenciados, se houver, não têm a publicação cancelada.

## Reverter um ativo ou uma carta para a versão publicada anteriormente {#revert-an-asset-or-letter-to-the-previously-published-version}

Toda vez que você publica um ativo ou uma carta após a edição, uma versão do ativo ou da carta é criada. É possível reverter um ativo ou carta para uma versão publicada anteriormente. Talvez seja necessário fazer isso se algo der errado com a versão atual do ativo ou documento.

>[!NOTE]
>
>Não reverta uma carta para o último estado publicado se qualquer ativo dependente usado nessa carta publicada for excluído do sistema.

1. Selecione um ativo e selecione **[!UICONTROL Reverter para a versão publicada anteriormente]** ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png).
1. Antes de o ativo ser revertido, uma caixa de diálogo de confirmação é exibida. Selecione **[!UICONTROL Reverter]**.

   O ativo ou a carta é revertido para a versão publicada anteriormente.

## Excluir um ativo {#delete-an-asset}

>[!NOTE]
>
>A exclusão de um ativo o remove da instância de publicação. A exclusão de um ativo também remove seu histórico de versões, exceto a versão base.

1. Selecione um ativo e selecione **[!UICONTROL Excluir]** ![excluir](assets/delete.png).

   >[!NOTE]
   >
   >A opção Excluir também está disponível ao exibir detalhes do ativo tocando em um ativo ou ao exibir as propriedades de um ativo tocando em Propriedades de Exibição ![viewproperties](assets/viewproperties.png).

1. Antes de excluir o ativo, uma caixa de diálogo de confirmação é exibida. Selecione **[!UICONTROL Excluir]**.

   >[!NOTE]
   >
   >Somente o ativo selecionado é excluído, e os ativos dependentes não são excluídos. Para verificar referências de um ativo, selecione ![referências](assets/references.png) e selecione um ativo.
   >
   >
   >Se o ativo que você está tentando excluir for um ativo filho de outro ativo, ele não será excluído. Para excluir um ativo como esse, remova as referências desse ativo de outros ativos e tente novamente.

## Forms adaptável protegido {#protected-adaptive-forms}

Você pode habilitar a autenticação para os formulários aos quais deseja que os usuários selecionados acessem. Quando você habilita a autenticação para seus formulários, os usuários veem uma tela de logon antes de acessá-los. Somente usuários com credenciais autorizadas podem acessar os formulários.

Para habilitar a autenticação para seus formulários:

1. No navegador, abra o configMgr na instância de publicação.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Na Configuração do Console da Web do Adobe Experience Manager, clique em **Apache Sling Authentication Service** para configurá-lo.
1. Na caixa de diálogo Apache Sling Authentication Service exibida, use o botão **+** para adicionar caminhos.\
   Quando você adiciona um caminho, o serviço de autenticação é ativado para formulários nesse caminho.
