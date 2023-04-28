---
title: Pastas privadas para compartilhar ativos
description: Saiba como criar uma pasta privada no [!DNL Adobe Experience Manager Assets] e compartilhá-lo com outros usuários e atribuir vários privilégios a eles.
contentOwner: Vishabh Gupta
role: User
feature: Collaboration
exl-id: d48f6daf-af81-4024-bff2-e8bf6d683b0c
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 3%

---

# Pasta privada em [!DNL Adobe Experience Manager Assets] {#private-folder}

Você pode criar uma pasta privada no [!DNL Adobe Experience Manager Assets] interface do usuário que está disponível exclusivamente para você. Você pode compartilhar essa pasta privada com outros usuários e atribuir vários privilégios a eles. Com base no nível de privilégio atribuído, os usuários podem executar várias tarefas na pasta, por exemplo, visualizar ativos na pasta ou editar os ativos.

>[!NOTE]
>
>A pasta privada tem pelo menos um membro com a função Proprietário.
>
>Para criar uma pasta privada, é necessário `Read` e `Modify` permissões na pasta pai na qual você cria uma pasta privada. Se você não for um administrador, essas permissões não serão ativadas por padrão em `/content/dam`. Nesse caso, primeiro obtenha essas permissões para sua ID/grupo de usuários antes de tentar criar pastas privadas.

## Criar e compartilhar pasta privada  {#create-share-private-folder}

Para criar e compartilhar uma pasta privada:

1. No [!DNL Assets] , clique no botão **[!UICONTROL Criar]** na barra de ferramentas e selecione **[!UICONTROL Pasta]** no menu .

   ![Criar pasta de ativos](assets/create-folder.png)

1. No **[!UICONTROL Criar pasta]** digite um `Title` e `Name` (opcional) para a pasta .

   Selecione o **[!UICONTROL Privado]** e clique em **[!UICONTROL Criar]**.

   ![chlimage_1-413](assets/create-private-folder.png)

   Uma pasta privada é criada. Agora você pode [adicionar ativos](add-assets.md#upload-assets) à pasta e compartilhe-a com outros usuários ou grupos. A pasta não fica visível para nenhum outro usuário até que você a compartilhe e atribua privilégios a ele.

1. Para compartilhar a pasta, selecione-a e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.

1. No **[!UICONTROL Propriedades da pasta]** selecione um usuário ou grupo na página **[!UICONTROL Adicionar usuário]** atribuir uma função (`Viewer`, `Editor`ou `Owner`) na pasta privada e clique em **[!UICONTROL Adicionar]**.

   ![assign-user-group](assets/assign-permissions-private-folder.png)

   Você pode atribuir várias funções, como `Editor`, `Owner`ou `Viewer` ao usuário com quem você compartilha a pasta. Se você atribuir uma `Owner` para o usuário, o usuário tem `Editor` na pasta. Além disso, o usuário pode compartilhar a pasta com outras pessoas. Se você atribuir uma `Editor` , o usuário pode editar os ativos em sua pasta privada. Se você atribuir uma função de visualizador, o usuário só poderá visualizar os ativos em sua pasta privada.

   >[!NOTE]
   >
   >A pasta privada tem pelo menos um membro com `Owner` função. Portanto, o administrador não pode remover todos os membros proprietários de uma pasta privada. No entanto, para remover os proprietários existentes (e o próprio administrador) da pasta privada, o administrador deve adicionar outro usuário como proprietário.

1. Clique em **[!UICONTROL Salvar e fechar]**. Dependendo da função atribuída, o usuário recebe um conjunto de privilégios em sua pasta privada quando ele faz logon no [!DNL Assets].
1. Clique em **[!UICONTROL Ok]** para fechar a mensagem de confirmação.
1. O usuário com quem você compartilha a pasta recebe uma notificação de compartilhamento na interface do usuário.

1. Clique em [!UICONTROL Notificações] para abrir uma lista de notificações.

   ![notificação](assets/notification-icon.png)

1. Clique na entrada da pasta privada compartilhada pelo administrador para abrir a pasta.

## Exclusão de pasta privada {#delete-private-folder}

Você pode excluir uma pasta selecionando e [!UICONTROL Excluir] no menu superior ou usando a tecla Backspace no teclado.

![excluir opção no menu superior](assets/delete-option.png)

>[!CAUTION]
>
>Se você excluir uma pasta privada do CRXDE Lite, os grupos de usuários redundantes serão deixados no repositório.

>[!NOTE]
>
>Se você excluir uma pasta usando o método acima da interface do usuário, os grupos de usuários associados também serão excluídos.
>
>No entanto, os grupos de usuários redundantes, não utilizados e gerados automaticamente existentes podem ser removidos do repositório usando `clean` no JMX na instância do autor (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).

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
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
