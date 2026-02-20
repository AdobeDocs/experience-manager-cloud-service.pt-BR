---
title: Gerenciar tokens de acesso de repositórios externos no Cloud Manager
description: Saiba como visualizar, editar e excluir tokens de acesso usados para Trazer seu próprio Git para o AEM Cloud Manager.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: bc9f392c-61f5-4d39-972b-4c6c8f9bab4a
source-git-commit: 2ea076c42a6406548bf48cd246227fc8ddb3a080
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 3%

---

# Gerenciar tokens de acesso para repositórios externos {#manage-access-tokens}

<!-- badge: label="Private beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#manage-access-tokens" -->

O Cloud Manager usa tokens de acesso para gerenciar repositórios hospedados em plataformas Git externas. Anteriormente, se um token expirasse, o repositório associado precisaria ser reintegrado para permanecer operacional.

Agora, o recurso **`Manage Access Tokens`** permite gerenciar tokens com mais eficiência. Você pode visualizar, renomear ou remover tokens conectados a provedores Git externos compatíveis, incluindo GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Consulte também [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

## Exibir tokens de acesso {#view-access-tokens}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa cujo token de acesso do Bring Your Own Git você deseja gerenciar.
1. No menu lateral, em **Programa**, clique em ![Ícone de estrutura de tópicos de pastas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Repositórios**.
1. Próximo ao canto superior direito da página, clique em **Gerenciar tokens de acesso**.

   O botão **Gerenciar tokens de acesso** só estará visível se o programa estiver usando o recurso Trazer seu próprio Git.

   ![Caixa de diálogo Gerenciar Tokens de Acesso listando um token que está ativo e um token que está inativo](/help/implementing/cloud-manager/managing-code/assets/access-tokens-manage.png)

1. Na caixa de diálogo **Gerenciar Tokens de Acesso**:
   * Todos os tokens de acesso são listados.
   * Você pode **editar** qualquer token de acesso.
   * Você pode **excluir** somente os tokens de acesso que estão *não em uso*. Se um token estiver em uso, o botão ![Excluir ícone da estrutura de tópicos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg) será desabilitado.

## Editar um token de acesso {#edit-access-tokens}

1. Na caixa de diálogo **Gerenciar Tokens de Acesso**, à direita de um nome de token, clique em ![Ícone Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).
1. Na caixa de diálogo **Editar Token de Acesso**, atualize o **Nome do Token** ou o valor do **Token de Acesso**, ou ambos.

   ![Caixa de diálogo Editar Token de Acesso](/help/implementing/cloud-manager/managing-code/assets/access-tokens-edit.png)

1. Se o **Token de acesso** estiver em uso no momento, uma notificação será exibida avisando que todos os repositórios associados são revalidados automaticamente após a atualização.

1. Clique em **Atualizar** para salvar as alterações.

## Excluir um token de acesso {#delete-access-token}

1. Na caixa de diálogo **Gerenciar Tokens de Acesso**, à direita de um nome de token, clique em ![Ícone Excluir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)

   O ícone está desabilitado (![Excluir ícone da estrutura de tópicos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)) para tokens que estão em uso no momento.

1. Na caixa de diálogo **`Delete Access Token`**, clique em **Excluir** para remover o token permanentemente.
