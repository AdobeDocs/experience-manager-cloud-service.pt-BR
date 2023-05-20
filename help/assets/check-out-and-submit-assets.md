---
title: Fazer check-in e check-out de arquivos em [!DNL Assets]
description: Saiba como fazer check-out de ativos para edição e check-in depois que as alterações forem concluídas.
contentOwner: AG
feature: Asset Management
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 5%

---

# Arquivos de check-in e check-out em [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/check-out-and-submit-assets.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

[!DNL Adobe Experience Manager Assets] O permite fazer check-out de ativos para edição e check-in depois que você concluir as alterações. Depois de fazer check-out de um ativo, somente você pode editar, anotar, publicar, mover ou excluir o ativo. Fazer o check-out de um ativo bloqueia o ativo. Outros usuários não podem executar nenhuma dessas operações no ativo até que você faça check-in do ativo novamente em [!DNL Assets]. No entanto, eles ainda podem alterar os metadados do ativo bloqueado.

Para fazer check-out/check-in de ativos, é necessário ter acesso de gravação a eles.

Este recurso ajuda a impedir que outros usuários substituam as alterações feitas por um autor, em que vários usuários colaboram na edição de workflows entre equipes.

## Fazer check-out dos ativos {#checking-out-assets}

1. No [!DNL Assets] selecione o ativo que deseja retirar. Você também pode selecionar vários ativos para fazer check-out.

1. Na barra de ferramentas, clique em **[!UICONTROL Check-out]**. A variável **[!UICONTROL Check-out]** opção alterna para **[!UICONTROL Check-in]**.
Para verificar se outros usuários podem editar o ativo do qual você fez check-out, faça logon como um usuário diferente. O ícone ![ícone de bloqueio de check-out](assets/do-not-localize/checkout_lock.png) é exibido na miniatura do ativo do qual você fez check-out.

   ![ícone de check-out na exibição de cartão](assets/checkout-icon-card-view.png)

   Selecione o ativo. Observe que a barra de ferramentas não exibe nenhuma opção que permita editar, anotar, publicar ou excluir o ativo.

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   Para editar os metadados do ativo bloqueado, clique em **[!UICONTROL Propriedades da exibição]**.

1. Clique em **[!UICONTROL Editar]** para abrir o ativo no modo de edição.

1. Edite o ativo e salve as alterações. Por exemplo, recorte a imagem e salve. Também é possível optar por anotar ou publicar o ativo.

1. Selecione o ativo editado na [!DNL Assets] e clique em **[!UICONTROL Check-in]** na barra de ferramentas. O ativo modificado foi submetido a check-in para [!DNL Assets] e está disponível para edição por outros usuários.

## Check-in forçado {#forced-check-in}

Os administradores podem fazer check-in de ativos que passaram por check-out por outros usuários.

1. Efetue logon no [!DNL Assets] como administrador.
1. No [!DNL Assets] interface do usuário selecione um ou mais ativos que foram verificados por outros usuários.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Na barra de ferramentas, clique em **[!UICONTROL Liberar Bloqueio]**. É feito check-in do ativo e ele fica disponível para edição para outros usuários.

## Práticas recomendadas e limitações {#tips-limitations}

* É possível excluir um *pasta* que contém arquivos de ativos com check-out. Antes de excluir uma pasta, verifique se nenhum ativo digital foi retirado por usuários.

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

>[!MORELIKETHIS]
>
>* [Entender o check-in e o check-out [!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Vídeo tutorial para entender o check-in e o check-out [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

