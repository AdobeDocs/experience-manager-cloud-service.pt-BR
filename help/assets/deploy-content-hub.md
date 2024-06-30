---
title: Implantar [!DNL Content Hub]
description: Saiba como implantar e ativar o Content Hub e fornecer acesso a usuários com diferentes tipos de privilégios (fazer upload de ativos, usuários de Adobe Express) e como fornecer privilégios de administrador aos usuários.
role: Admin
source-git-commit: 5a968440c8841abe7af2c81c4af12258b7e4547f
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 0%

---


# Implantar o Content Hub {#deploy-content-hub}

![Implantar o Content Hub](assets/deploy-content-hub.png)

O Content Hub está disponível como parte do Experience Manager Assets as a Cloud Service para democratizar o acesso a conteúdo sobre a marca para organizações e seus parceiros de negócios.

Os ativos marcados como Aprovado no Experience Manager Assets as a Cloud Service estão disponíveis para distribuição de ativos no Content Hub.

Este artigo fornece um fluxo de trabalho completo para fornecer aos usuários acesso ao Content Hub, incluindo as variações de privilégios com base em suas necessidades.

As variações de privilégios no Content Hub incluem:

* [Usuários do Content Hub](#onboard-content-hub-users): acesse os ativos aprovados pela marca no portal do Content Hub.

* [Administradores do Content Hub](#onboard-content-hub-administrator): Acesso à [Interface do usuário de configuração](/help/assets/configure-content-hub-ui-options.md) no Content Hub, além de acessar ativos aprovados pela marca, fazer upload de ativos no Content Hub, integração com o Adobe Express para editar imagens (se você tiver direitos ao Adobe Express).

* [Usuários do Content Hub com direito de adicionar ativos](#onboard-content-hub-users-add-assets): Capacidade de [fazer upload de ativos para o Content Hub](/help/assets/upload-brand-approved-assets.md) além de acessar ativos aprovados pela marca no portal Content Hub.

* [Usuários do Content Hub com direitos de remixar ativos para novas variações](#onboard-content-hub-users-remix-assets): [Integração do Adobe Express](/help/assets/edit-images-content-hub.md) (se você tiver direitos de Adobe Express) além de acessar ativos aprovados pela marca no portal da Content Hub.

* [Usuários do Experience Manager Assets](#experience-manager-assets-users): capacidade de aprovar ativos no Experience Manager Assets as a Cloud Service para disponibilizá-los no Content Hub.

## Etapa 1: Ativar o Content Hub para Experience Manager Assets usando o Cloud Manager {#enable-content-hub}

Para acessar o portal Content Hub, primeiro os administradores precisam ativar o Content Hub para Experience Manager Assets as a Cloud Service Cloud Manager. Execute as seguintes etapas:

1. Faça logon no Cloud Manager. Certifique-se de selecionar a organização correta ao fazer logon. O Cloud Manager lista todos os seus programas.

1. Navegue até o programa as a Cloud Service do Experience Manager Assets, clique no ícone Mais opções (...) e selecione **[!UICONTROL Editar programa]**.

   ![Editar programa no Cloud Manager](assets/edit-program-cloud-manager.png)

1. No [!UICONTROL Editar programa] , selecione a **[!UICONTROL Soluções e complementos]** guia.

1. Expandir **[!UICONTROL Assets]** e selecione **[!UICONTROL Content Hub]**.
   ![Selecionar Content Hub no Cloud Manager](assets/edit-program-cloud-manager-content-hub.png)

1. Clique em **[!UICONTROL Atualizar]**.

O Content Hub agora está ativado para o Experience Manager Assets as a Cloud Service.

Se você nunca usou o Experience Manager Assets, clique em **[!UICONTROL Adicionar programa]** e forneça os detalhes do programa (Nome do programa, configurado para produção) e clique em **[!UICONTROL Continuar]**. É possível selecionar **[!UICONTROL Assets]** e **[!UICONTROL Content Hub]** no **[!UICONTROL Soluções e complementos]** guia.

### Instância do Content Hub e perfil de produto no Admin Console{#content-hub-instance-product-profile}

Depois [habilitar o Content Hub para o Assets as a Cloud Service Cloud Manager](#enable-content-hub), há uma nova instância criada no as a Cloud Service Admin Console do AEM Assets com `contenthub` como o sufixo:

![Nova instância para o Content Hub](assets/new-instance-content-hub.png)

Observe que não há `author` ou `publish` no nome da instância do Content Hub.

Clique no nome da instância para exibir o perfil de produto do Content Hub.

![Perfil de produto do Content Hub](assets/content-hub-product-profile.png)

## Etapa 2: integrar o administrador do Content Hub {#onboard-content-hub-administrator}

Os administradores do Content Hub podem acessar o [Interface do usuário de configuração](/help/assets/configure-content-hub-ui-options.md) no Content Hub, além de acessar ativos aprovados pela marca, fazer upload de ativos no Content Hub, integração com o Adobe Express para editar imagens (se você tiver direitos ao Adobe Express).

Para integrar o administrador do Content Hub:

1. [Acesse e clique no perfil de produto do usuário do Content Hub](#content-hub-instance-product-profile).

1. Clique em **[!UICONTROL Adicionar usuários]** para adicionar usuários ou grupos de usuários ao perfil de produto.

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

1. Depois de adicionar o usuário ao perfil de produto do Content Hub, acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos no Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   O Admin Console exibe dois perfis de produto para o AEM as a Cloud Service: Administradores e Usuários.
1. Clique no perfil de produto Administrators e clique em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do administrador](assets/aem-cs-admin-product-profile.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

## Etapa 3: integrar usuários do Content Hub {#onboard-content-hub-users}

Os usuários do Content Hub podem acessar ativos disponíveis no portal, mas não podem adicionar novos ativos ou modificar ativos existentes.

Para integrar usuários do Content Hub:

1. [Acesse e clique no perfil de produto do usuário do Content Hub](#content-hub-instance-product-profile).

1. Clique em **[!UICONTROL Adicionar usuários]** para adicionar usuários ou grupos de usuários ao perfil de produto.

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

Esses usuários agora podem acessar os ativos disponíveis no portal do Content Hub.

>[!NOTE]
>
>Você pode usar todos os recursos avançados da empresa, como a sincronização com Provedores de identidade externos.

Depois de adicionar os usuários apropriados usando o Admin Console, os usuários podem acessar o Content Hub usando o seguinte link:

`https://experience.adobe.com/#/assets/contenthub`

### Desabilitar notificações por email para usuários {#disable-email-notifications}

Se os administradores precisarem desativar as notificações por email enviadas aos usuários quando eles forem adicionados ao perfil de produto do Content Hub:

Clique no ícone de pesquisa ao lado do nome do perfil do produto e desative a opção **[!UICONTROL Notificar usuários por email]** alternar.

![Desabilitar notificações por email](assets/disable-email-notifications.png)


## Etapa 4: integrar usuários do Content Hub com direitos para adicionar ativos (opcional) {#onboard-content-hub-users-add-assets}

Os usuários do Content Hub com direitos para adicionar ativos podem [fazer upload de novos ativos aprovados pela marca para o Content Hub](/help/assets/upload-brand-approved-assets.md).

Para integrar usuários do Content Hub com direitos para adicionar usuários:

1. [Depois de adicionar o usuário ao perfil de produto do Content Hub](#onboard-content-hub-users), acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos no Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   O Admin Console exibe dois perfis de produto para o AEM as a Cloud Service: Administradores e Usuários.
1. Clique no perfil de produto Usuários e clique em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-cs-user-product-profile.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

## Etapa 4: integrar usuários do Content Hub com direitos de remix de ativos a novas variações (Opcional) {#onboard-content-hub-users-remix-assets}

Os usuários do Content Hub com direitos para remixar ativos para novas variações podem [modificar ativos existentes usando o Adobe Express e salvar o ativo no repositório](/help/assets/edit-images-content-hub.md). A edição de ativos usando o Adobe Express só estará disponível se o usuário tiver direitos de Adobe Express.

Para integrar usuários do Content Hub com direitos de remixar ativos a novas variações:

1. [Depois de adicionar o usuário ao perfil de produto do Content Hub](#onboard-content-hub-users), acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos no Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   O Admin Console exibe dois perfis de produto para o AEM as a Cloud Service: Administradores e Usuários.
1. Clique no perfil de produto Usuários e clique em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-cs-user-product-profile.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

## Usuários do Experience Manager Assets {#experience-manager-assets-users}

Os usuários do Experience Manager Assets podem aprovar ativos no AEM as a Cloud Service para que eles fiquem disponíveis no Content Hub.

Para configurar usuários do Experience Manager Assets:

1. Para acessar os perfis de produto do Experience Manager Assets, clique no nome de produto do AEM as a Cloud Service na lista de produtos do Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   O Admin Console exibe dois perfis de produto para o AEM as a Cloud Service: Administradores e Usuários.
1. Clique no perfil de produto Usuários e clique em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-cs-user-product-profile.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

   >[!NOTE]
   >
   > Não é necessário adicionar à [Perfil de produto do Content Hub](#onboard-content-hub-users) para os usuários do Experience Manager Assets.



