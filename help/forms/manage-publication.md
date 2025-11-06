---
title: Como publicar ou desfazer a publicação de formulários em instâncias de pré-visualização ou publicação?
description: Saiba como publicar ou desfazer a publicação de formulários do ambiente de criação do AEM para visualizar ou publicar instâncias. Quer você esteja testando seus formulários em um ambiente de preparo ou implantando-os em tempo real para usuários finais, a AEM fornece ferramentas simplificadas para gerenciar esse processo com eficiência.
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
exl-id: 6ade40f1-bad5-4f5e-aa0e-84b7c6a82e02
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---


# &#x200B;Gerenciar publicação no Experience Manager Forms

Como administrador do Adobe Experience Manager (AEM) Forms, você pode publicar formulários da sua instância de autor no Experience Manager Forms. Você também tem a opção de agendar a publicação de um formulário ou pasta para uma data ou hora posterior. Após a publicação, os usuários podem acessar e preencher os formulários.

No Experience Manager Forms, você pode publicar um formulário usando um dos seguintes métodos:

* [Opção Publicar](#publish-forms-using-the-publish-option)
* [Opção Gerenciar publicação](#publish-forms-using-the-manage-publication-option)

## Itens a serem considerados

* Somente membros do grupo `forms-users` podem usar a opção **Gerenciar Publicação** para publicar os formulários.
* As alterações feitas em formulários ou pastas no Experience Manager Forms não aparecem na instância **Publish** até serem republicadas. Isso garante que atualizações de trabalho em andamento permaneçam indisponíveis na instância **Publicar**. Somente as alterações publicadas explicitamente por um administrador são refletidas na instância **Publicar**.

## Publicar formulários usando a opção Publicar

A opção **Publicar** permite publicar um formulário imediatamente. Para publicar um Formulário do Experience Manager usando o botão **Publicar** na barra de ferramentas. Para publicar formulários usando a opção Publicar, são:

1. No console Experience Manager Forms, navegue até a pasta principal e selecione um formulário que deseja publicar.
1. Clique na opção **Publicar** da barra de ferramentas e veja todos os ativos de referência que seriam publicados com o formulário.
1. Clique em **[!UICONTROL Publicar]**.

   ![Publicar e desfazer a publicação do formulário](/help/edge/docs/forms/assets/publish-form-option.png)

   Depois que o formulário e seus ativos relacionados forem publicados com êxito, uma caixa de diálogo **Êxito** será exibida.
1. Clique em **Fechar**.

   ![Caixa de diálogo de sucesso](/help/forms/assets/publish-success1.png)

### Cancelar publicação do formulário

Depois de publicar o formulário com êxito usando a opção **Publicar** e seus ativos relacionados, você pode até mesmo desfazer a publicação usando o botão **[!UICONTROL Cancelar publicação]** disponível na barra de ferramentas. Para desfazer a publicação do formulário:

1. Para desfazer a publicação do formulário e de seus ativos relacionados, selecione o formulário e clique em **[!UICONTROL Desfazer publicação]** na barra de ferramentas

   Ao clicar no botão **[!UICONTROL Cancelar publicação]**, a caixa de diálogo **Cancelar publicação de ativo** é exibida.
1. Clique em **[!UICONTROL Cancelar publicação]** para iniciar o processo de cancelamento da publicação

   ![Caixa de diálogo de Unplish](/help/forms/assets/unpublish-asset.png)

   Depois que a publicação do formulário e seus ativos relacionados for desfeita com êxito, uma caixa de diálogo **Êxito** será exibida.
1. Clique em **Fechar**.

   ![cancelamento de publicação bem-sucedido](/help/forms/assets/unpublishing-start.png)

## Publicar formulários usando a opção Gerenciar publicação

Gerenciar publicação permite publicar ou desfazer a publicação de conteúdo de e para o destino selecionado, adicionar conteúdo à lista de publicação em toda a pasta `forms&documents`, selecionar referências para publicar e agendar publicações para uma data ou hora posterior.  Para publicar formulários usando a opção **Gerenciar Publicação** são:

1. No console Experience Manager Forms, navegue até a pasta principal e selecione um formulário que deseja publicar.
1. Clique na opção **[!UICONTROL Gerenciar publicação]** na barra de ferramentas.

   ![Opção Gerenciar publicação](/help/forms/assets/manage-publication-option.png)

   A interface do usuário **Gerenciar Publicação** é exibida:

   ![Gerenciar publicação](/help/forms/assets/manage-publication.png)

   As seguintes opções estão disponíveis na interface do usuário do **Gerenciar publicação**:

   * **Ações**

      * **Publicar**: publicar formulários no destino selecionado
      * **Cancelar publicação**: cancelar a publicação de formulários do destino

   * **Destino**

      * **Publicar**: publicar formulários na instância de publicação do Experience Manager Forms (AEM).
      * **Visualizar**: publicar formulários na instância de Visualização do Experience Manager Forms (AEM).

   * **Programação**

      * **Agora**: publicar formulários imediatamente
      * **Mais tarde**: publicar formulários com base na **Data de ativação** ou na hora

1. Clique em **Avançar** para continuar.
1. (Opcional) Na guia **Escopo**, use a opção [Adicionar conteúdo](#add-content) para adicionar mais conteúdo para publicação. Por exemplo, você pode adicionar mais arquivos Forms ou Documento de registro.
   ![guia de escopo](/help/forms/assets/scope-tab.png)
1. Clique em **[!UICONTROL Publicar]** para publicar os formulários e os ativos relacionados e a mensagem de êxito será exibida.
   ![publicar mensagem com êxito](/help/forms/assets/publish-successful.png)

### Adicionar conteúdo

A publicação no Experience Manager Forms permite adicionar mais conteúdo (formulários) à lista de publicação.
Para adicionar mais formulários para publicação:

1. Clique no botão **Adicionar Conteúdo** para adicionar mais conteúdo.

   ![Adicionar conteúdo](/help/forms/assets/add-content.png)

2. Selecione o formulário na tela **Selecionar caminho**.

   ![Adicionar conteúdo](/help/forms/assets/add-assets.png)

   >[!NOTE]
   >
   > Você pode adicionar mais formulários ou pastas à lista da pasta `formsanddocuments`. Mas não é possível adicionar formulários de várias pastas de uma vez.

3. Para configurar as referências para publicar ou não publicar para um formulário, selecione o formulário e clique em **[!UICONTROL Referências publicadas]**.

   ![referências publicadas](/help/forms/assets/published-references.png)

4. Na caixa de diálogo **Referências publicadas**, desmarque os ativos que você planeja não publicar novamente e clique em **[!UICONTROL Concluído]**.
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


### Publicar ou desfazer a publicação de um formulário mais tarde

Além de permitir a publicação ou o cancelamento da publicação de formulários em uma data e hora posteriores, a opção publicar ou desfazer a publicação mais tarde também permite configurar um fluxo de trabalho. Os formulários são publicados ou não após a conclusão do fluxo de trabalho.

Para agendar um formulário para publicação ou cancelamento da publicação:

1. No console Experience Manager Forms, navegue até a pasta principal e selecione o formulário que deseja agendar a publicação.
1. Clique na opção **[!UICONTROL Gerenciar publicação]** na barra de ferramentas.

   ![Gerenciar publicação](/help/forms/assets/manage-publication.png)

1. Clique em **Publicar** ou **Cancelar publicação** da **[!UICONTROL Ação]**.
1. Selecione o **[!UICONTROL Destino]** onde deseja publicar ou cancelar a publicação do conteúdo.
   * **Visualizar**: use a opção **Visualizar** para publicar ou desfazer a publicação em um ambiente de visualização do Experience Manager Forms. Os ambientes de visualização do Experience Manager Forms são usados para testar em formulários de desenvolvimento.
   * **Publicar**: use a opção **Publicar** do Experience Manager Forms para enviar o formulário para o ambiente de publicação do Experience Manager Forms depois que ele estiver pronto para uso em um ambiente de produção.

1. Selecione **[!UICONTROL Depois]** em **Agendando**.

   ![Gerenciar publicação mais tarde](/help/forms/assets/manage-publication-later.png)

1. Selecione uma **[!UICONTROL Data de ativação]** e especifique a data e a hora.
1. Clique em **[!UICONTROL Avançar]**.
1. (Opcional) Na guia **Escopo**, adicione conteúdo usando **[!UICONTROL Adicionar Conteúdo]**.
   ![Gerenciar publicação para adicionar conteúdo mais tarde](/help/forms/assets/publish-later-add-content.png)
1. Clique em **[!UICONTROL Avançar]**.
1. Na guia **Fluxos de Trabalho**, especifique um **[!UICONTROL título de Fluxo de Trabalho]**.
1. Clique em **[!UICONTROL Publicar Mais Tarde]**.

   ![Gerenciar Fluxo de Trabalho de Publicação](/help/forms/assets/manage-publication-workflows.png)

## Determinação do status de publicação

Há várias maneiras de determinar o status de publicação:

* Faça logon na instância de destino para verificar os formulários publicados e outros ativos (dependendo da data ou hora agendada).

* Use a exibição de linha do tempo para determinar o status da publicação.

* Use o menu de informações da página no editor Forms adaptável.
