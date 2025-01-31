---
title: Como publicar ou desfazer a publicação de formulários em instâncias de pré-visualização ou publicação?
description: Saiba como publicar ou desfazer a publicação de formulários do ambiente do autor do AEM para visualizar ou publicar instâncias. Se você estiver testando seus formulários em um ambiente de preparo ou implantando-os em tempo real para usuários finais, o AEM fornece ferramentas simplificadas para gerenciar esse processo com eficiência.
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: d3c089dcca80255f53c0888d46ee1b4b6246741e
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# &#x200B;Gerenciar publicação no Experience Manager Forms

Como administrador do Adobe Experience Manager Forms, você pode publicar formulários da instância do autor no Experience Manager Forms. Você pode agendar a publicação de um formulário ou pasta em uma data ou hora posterior. Após a publicação, os usuários podem acessar e preencher os formulários.

Na interface do Experience Manager Forms, você pode publicar um formulário usando o:
* [Opção do Publish](#publish-forms-using-the-publish-option)
* [Opção Gerenciar publicação](#publish-forms-using-the-manage-publication-option)

Se você fizer modificações subsequentes nos formulários ou pastas originais no Experience Manager Forms, as alterações não serão refletidas na instância do **Publish** até que você publique novamente pelo Experience Manager Forms. Isso garante que as alterações de trabalho em andamento não estejam disponíveis na instância do **Publish**. Somente as alterações publicadas por um administrador estão disponíveis na instância **Publish**.

## Formulários Publish usando a opção Publish

A opção **Publish** permite publicar um formulário imediatamente. Para publicar um Formulário Experience Manager usando o botão **Publish** na barra de ferramentas. Para publicar formulários usando a opção Publish são:

1. No console Experience Manager Forms, navegue até a pasta principal e selecione um formulário que deseja publicar.
1. Clique na opção **Publish** da barra de ferramentas e veja todos os ativos de referência que serão publicados com o formulário.
1. Clique em **[!UICONTROL Publicar]**.

   ![Publish e Cancelar publicação do formulário](/help/edge/docs/forms/assets/publish-form-option.png)

   Depois que o formulário e seus ativos relacionados forem publicados com êxito, uma caixa de diálogo **Êxito** será exibida. Clique em **Fechar** para fechar a caixa de diálogo.

   ![Caixa de diálogo de sucesso](/help/forms/assets/publish-success.png)

### Cancelar publicação do formulário

Depois de publicar o formulário com êxito usando a opção **Publish** e seus ativos relacionados, você pode até mesmo desfazer a publicação usando o botão **[!UICONTROL Cancelar publicação]** na barra de ferramentas. Para desfazer a publicação do formulário:

1. Para desfazer a publicação do formulário e de seus ativos relacionados, selecione o formulário e clique em **[!UICONTROL Desfazer publicação]** na barra de ferramentas

   Ao clicar no botão **[!UICONTROL Cancelar publicação]**, a caixa de diálogo **Cancelar publicação de ativo** é exibida.
1. Clique em **[!UICONTROL Cancelar publicação]** para iniciar o processo de cancelamento da publicação

   ![Caixa de diálogo de Unplish](/help/forms/assets/unpublish-asset.png)

   Depois que a publicação do formulário e seus ativos relacionados for desfeita com êxito, uma caixa de diálogo **Êxito** será exibida. Clique em **Fechar** para fechar a caixa de diálogo.

   ![cancelamento de publicação bem-sucedido](/help/forms/assets/unpublishing-start.png)

## Formulários Publish usando a opção Gerenciar publicação

Gerenciar publicação permite publicar ou desfazer a publicação de conteúdo de e para o destino selecionado, adicionar conteúdo à lista de publicação em toda a pasta de formulários e documentos, selecionar referências para publicar e agendar publicações para uma data ou hora posterior.  Para publicar formulários usando a opção Gerenciar publicação são:

1. No console Experience Manager Forms, navegue até a pasta principal e selecione um formulário que deseja publicar.
1. Clique na opção **[!UICONTROL Gerenciar publicação]** na barra de ferramentas.

   ![Opção Gerenciar publicação](/help/forms/assets/manage-publication-option.png)

   A interface **Gerenciar Publicação** aparece:

   ![Gerenciar publicação](/help/forms/assets/manage-publication.png)

   As seguintes opções estão disponíveis na interface **Gerenciar Publicação**:

   * **Ações**

      * **Publish**: formulários do Publish para o destino selecionado
      * **Cancelar publicação**: cancelar a publicação de formulários do destino

   * **Destino**

      * **Publish**: o Publish se forma com a instância do Publish do Experience Manager Forms (AEM).
      * **Visualização**: formulários do Publish para a instância de visualização do Experience Manager Forms (AEM).

   * **Programação**

      * **Agora**: formulários do Publish imediatamente
      * **Mais tarde**: formulários do Publish baseados em **Data de ativação** ou hora

1. Clique em **Avançar** para continuar.
1. Na guia **Escopo**, use a opção [Adicionar Conteúdo](#add-content) para adicionar mais conteúdo para publicação. Por exemplo, você pode adicionar mais arquivos Forms ou Documento de registro.
   ![guia de escopo](/help/forms/assets/scope-tab.png)
1. Clique em **[!UICONTROL Publish]** para publicar os formulários e os ativos relacionados, e a mensagem de êxito será exibida.
   ![publicar mensagem com êxito](/help/forms/assets/publish-successful.png)

### Adicionar conteúdo

A publicação no Experience Manager Forms permite adicionar mais conteúdo (formulários e pastas) à lista de publicação. Você pode adicionar mais formulários ou pastas à lista da pasta `formsanddocuments`. Mas não é possível adicionar formulários de várias pastas de uma vez. Para adicionar mais formulários para publicação:

1. Clique no botão **Adicionar Conteúdo** para adicionar mais conteúdo.

   ![Adicionar conteúdo](/help/forms/assets/add-content.png)

1. Selecione o formulário na tela **Selecionar caminho**. É possível adicionar vários formulários de uma pasta ou adicionar várias pastas de uma vez. Mas não é possível adicionar formulários de várias pastas de uma vez.

   ![Adicionar conteúdo](/help/forms/assets/add-assets.png)

1. Para configurar as referências para publicar ou não publicar para um formulário, selecione o formulário e clique em **[!UICONTROL Referências publicadas]**.

   ![referências publicadas](/help/forms/assets/published-references.png)

1. Na caixa de diálogo **Referências publicadas**, desmarque os ativos que você planeja não publicar novamente e clique em **[!UICONTROL Concluído]**.
   ![caixa de diálogo de referências publicadas](/help/forms/assets/published-references-dialog.png)

<!--
### Include Folder Settings
By default, publishing a folder to Experience Manager Forms publishes all the assets, subfolders, and their references. To filter the folder for publishing:

1. Click **[Include Folder Settings]** to filter the folder.

    ![Include folder](/help/forms/assets/include-folder.png)

    The **[UICONTROL Include Folder Settings]** dialog appears. 
    
    ![Include folder dialog](/help/forms/assets/include-folder-dialog.png)
    
    The **[UICONTROL Include Folder Settings]** includes following options:

    * **[!UICONTROL Include folder contents]** checkbox. 
        * If selected, all forms and assets in the chosen folder, its subfolders (including all forms and assets within them), and references are published.
        * If not selected, only the forms and assets in the selected folder are published, while subfolder forms and assets are not.

    * **[!UICONTROL Include only immediate folder contents]** checkbox
        Selecting the **[!UICONTROL Include folder contents]** checkbox enables the **[!UICONTROL Include only immediate folder contents]** checkbox for selection.

        * If you select both options, all the forms and assets of the selected folder, subfolders (empty), and references are published. The forms and assets of the subfolders are not published.
        * -->


### Publish ou cancele a publicação de um formulário mais tarde

Além de permitir a publicação ou o cancelamento da publicação de formulários em uma data e hora posteriores, a opção publicar ou desfazer a publicação mais tarde também permite configurar um fluxo de trabalho. Os formulários são publicados ou não após a conclusão do fluxo de trabalho. Para agendar um formulário para publicação ou cancelamento da publicação:

1. No console Experience Manager Forms, navegue até a pasta principal e selecione o formulário que deseja agendar a publicação.
1. Clique na opção **[!UICONTROL Gerenciar publicação]** na barra de ferramentas.

   ![Gerenciar publicação](/help/forms/assets/manage-publication.png)

1. Clique em **Publish** ou **Cancelar publicação** de **[!UICONTROL Ação]** e selecione o **[!UICONTROL Destino]** onde deseja publicar ou cancelar a publicação do conteúdo.
   * **Visualizar**: use a opção **Visualizar** para publicar ou desfazer a publicação em um ambiente de visualização do Experience Manager Forms. Os ambientes de visualização do Experience Manager Forms são usados para testar em formulários de desenvolvimento.
   * **Publish**: use a opção Experience Manager Forms Publish para enviar o formulário ao ambiente de publicação do Experience Manager Forms depois que ele estiver pronto para uso em um ambiente de produção.

1. Selecione **[!UICONTROL Depois]** em Agendamento.

   ![Gerenciar publicação mais tarde](/help/forms/assets/manage-publication-later.png)

1. Selecione uma **[!UICONTROL Data de ativação]** e especifique a data e a hora.
1. Clique em **[!UICONTROL Avançar]**.
1. Na guia **Escopo**, **[!UICONTROL Adicionar Conteúdo]** (se necessário).
   ![Gerenciar publicação para adicionar conteúdo mais tarde](/help/forms/assets/publish-later-add-content.png)
1. Clique em **[!UICONTROL Avançar]**.
1. (Opcional) Na guia **Fluxos de trabalho**, especifique um **[!UICONTROL título de fluxo de trabalho]**.
1. Clique em **[!UICONTROL Publish Depois]**.

   ![Gerenciar Fluxo de Trabalho de Publicação](/help/forms/assets/manage-publication-workflows.png)

## Determinação do status de publicação

Há várias maneiras de determinar o status de publicação:

* Faça logon na instância de destino para verificar os formulários publicados e outros ativos (dependendo da data ou hora agendada).

* Use a exibição de linha do tempo para determinar o status da publicação.

* Use o menu de informações da página no editor Forms adaptável.
