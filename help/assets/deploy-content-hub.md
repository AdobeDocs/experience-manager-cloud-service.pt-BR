---
title: Implantar [!DNL Content Hub]
description: Saiba como implantar e ativar o Content Hub e fornecer acesso a usuários com diferentes tipos de privilégios (fazer upload de ativos, usuários de Adobe Express) e como fornecer privilégios de administrador aos usuários.
role: Admin
exl-id: 58194858-6e1c-460b-bab3-3496176b2851
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 1%

---

# Implantar o Content Hub {#deploy-content-hub}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Implantar Content Hub](assets/deploy-content-hub.png)

O Content Hub está disponível como parte do Experience Manager Assets as a Cloud Service para democratizar o acesso a conteúdo sobre a marca para organizações e seus parceiros de negócios.

Os ativos marcados como Aprovado no Experience Manager Assets as a Cloud Service estão disponíveis para distribuição de ativos no Content Hub.

Este artigo fornece um fluxo de trabalho completo para fornecer aos usuários acesso ao Content Hub, incluindo as variações de privilégios com base em suas necessidades.

As variações de privilégios no Content Hub incluem:

* [Usuários do Content Hub](#onboard-content-hub-users): acessem ativos aprovados pela marca no portal do Content Hub.

* [Administradores do Content Hub](#onboard-content-hub-administrator): acesso à [Interface do Usuário de Configuração](/help/assets/configure-content-hub-ui-options.md) no Content Hub, além de acessar ativos aprovados pela marca, carregar ativos para o Content Hub, integração de Adobe Express para editar imagens (se você tiver direitos de Adobe Express).

* [Usuários do Content Hub com direitos de adicionar ativos](#onboard-content-hub-users-add-assets): capacidade de [carregar ativos para o Content Hub](/help/assets/upload-brand-approved-assets.md) além de acessar ativos aprovados por marca no portal do Content Hub.

* [Usuários do Content Hub com direitos de remixar ativos para novas variações](#onboard-content-hub-users-remix-assets): [Integração com o Adobe Express](/help/assets/edit-images-content-hub.md) (se você tiver direitos de Adobe Express) além de acessar ativos aprovados por marca no portal do Content Hub.

* [Usuários do Experience Manager Assets](#experience-manager-assets-users): capacidade de aprovar ativos no Experience Manager Assets as a Cloud Service para disponibilizar esses ativos no Content Hub.

A tabela a seguir resume os tipos de usuários disponíveis do Content Hub, os privilégios que eles têm e os perfis de produtos necessários para obter esses privilégios:

| Função do usuário | Usuários do Content Hub | Usuários do Content Hub com direito de adicionar ativos | Usuários do Content Hub com direitos de remixar ativos | Administradores do Content Hub |
|---------------|----------|----------|-------------------------|---|
| **Recursos** |
| Acessar ativos aprovados pela marca no portal do Content Hub | ✓ | ✓ | ✓ | ✓ |
| Fazer upload de ativos do portal do Content Hub | − | ✓ | ✓ | ✓ |
| Usar a integração de Adobe Express para editar imagens | − | − | ✓ | − |
| Acessar a interface de configuração do Content Hub | − | − | − | ✓ |
| **O usuário precisa estar nesses perfis de produto (Admin Console)** |
| AEM > Instância de entrega > Usuários limitados da AEM Assets | ✓ | ✓ | ✓ | ✓ |
| AEM > Instância do autor da produção > Usuários AEM | − | ✓ | ✓ | − |
| AEM > Instância do autor da produção > Administradores do AEM | − | − | − | ✓ |
| Adobe Express | − | − | ✓ | − |
| **Mais informações** | Consulte [usuários do Content Hub](#onboard-content-hub-users) | Consulte [Usuários do Content Hub com direitos para adicionar ativos](#onboard-content-hub-users-add-assets) | Consulte [usuários do Content Hub com direitos para remixar ativos para novas variações](#onboard-content-hub-users-remix-assets) | Consulte [Administradores do Content Hub](#onboard-content-hub-administrator) |

>[!NOTE]
>
>[Os usuários do Experience Manager Assets](#experience-manager-assets-users) podem aprovar ativos em um ambiente as a Cloud Service do Experience Manager Assets para torná-los disponíveis no Content Hub. Esses usuários devem ser adicionados ao perfil de produto AEM > Instância do autor da produção > Usuários do AEM usando o Admin Console.

## Etapa 1: Ativar o Content Hub para Experience Manager Assets usando o Cloud Manager {#enable-content-hub}

Para acessar o portal Content Hub, primeiro os administradores precisam ativar o Content Hub para Experience Manager Assets as a Cloud Service Cloud Manager. Execute as seguintes etapas:

1. Faça logon no Cloud Manager. Certifique-se de selecionar a organização correta ao fazer logon. O Cloud Manager lista todos os seus programas.

1. Navegue até o programa as a Cloud Service do Experience Manager Assets, clique no ícone Mais opções (...) e selecione **[!UICONTROL Editar programa]**.

   ![Editar programa no Cloud Manager](assets/edit-program-cloud-manager.png)

1. Na caixa de diálogo [!UICONTROL Editar programa], selecione a guia **[!UICONTROL Soluções e complementos]**.

1. Expanda **[!UICONTROL Assets]** e selecione **[!UICONTROL Content Hub]**.
   ![Selecionar Content Hub no Cloud Manager](assets/edit-program-cloud-manager-content-hub.png)

   >[!NOTE]
   >
   >Se a **[!UICONTROL Atualização]** não estiver habilitada para você depois de selecionar o Content Hub, verifique se você especificou as configurações de ativação do programa.

1. Clique em **[!UICONTROL Atualizar]**.

O Content Hub agora está ativado para o Experience Manager Assets as a Cloud Service. Depois de ativar o Content Hub em um ambiente de Produção, não é possível desativá-lo no autoatendimento.

>[!NOTE]
>
>Você pode acessar e usar o Content Hub com até 250 usuários do Content Hub. Entre em contato com o representante da Adobe em caso de dúvidas adicionais.


Se você é novo no Experience Manager Assets, clique em **[!UICONTROL Adicionar programa]**, forneça os detalhes do programa (Nome do programa, configurar para produção) e clique em **[!UICONTROL Continuar]**. Você pode selecionar **[!UICONTROL Assets]** e **[!UICONTROL Content Hub]** na guia **[!UICONTROL Soluções e Complementos]**.

### Instância do Content Hub e perfil de produto no Admin Console{#content-hub-instance-product-profile}

Depois de [habilitar o Content Hub para o Assets com as a Cloud Service Cloud Manager](#enable-content-hub), há uma nova instância criada no Admin Console as a Cloud Service AEM Assets com `delivery` como sufixo:

![Nova instância para o Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Se você tiver provisionado o Content Hub antes de 14 de agosto de 2024, a nova instância será criada com `contenthub` como sufixo.

Observe que não há `author` ou `publish` no nome da instância do Content Hub.

Clique no nome da instância para exibir o perfil de produto do Content Hub.

![Perfil de produto do Content Hub](assets/content-hub-product-profile.png)

>[!NOTE]
>
>Se você tiver provisionado o Content Hub antes de 14 de agosto de 2024, o perfil de produto do Content Hub terá `contenthub` mencionado depois de `Limited Users` em vez de `delivery`.

## Etapa 2: integrar o administrador do Content Hub {#onboard-content-hub-administrator}

Os administradores do Content Hub podem acessar a [Interface do usuário de configuração](/help/assets/configure-content-hub-ui-options.md) no Content Hub, além de acessar ativos aprovados pela marca, fazer upload de ativos para o Content Hub, integrar o Adobe Express para editar imagens (se você tiver direitos ao Adobe Express).

Para integrar o administrador do Content Hub:

1. [Acesse e clique no perfil de produto de usuário do Content Hub](#content-hub-instance-product-profile).

1. Clique em **[!UICONTROL Adicionar usuários]** para adicionar usuários ou grupos de usuários ao perfil de produto.

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

1. Depois de adicionar o usuário ao perfil de produto do Content Hub, acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos no Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   O Admin Console exibe dois perfis de produto para o AEM as a Cloud Service: Administradores e Usuários.
1. Clique no perfil de produto Administradores e em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do administrador](assets/aem-cs-admin-product-profile.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

## Etapa 3: integrar usuários do Content Hub {#onboard-content-hub-users}

Os usuários do Content Hub podem acessar ativos disponíveis no portal, mas não podem adicionar novos ativos ou modificar ativos existentes.

Para integrar usuários do Content Hub:

1. [Acesse e clique no perfil de produto de usuário do Content Hub](#content-hub-instance-product-profile).

1. Clique em **[!UICONTROL Adicionar usuários]** para adicionar usuários ou grupos de usuários ao perfil de produto.

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

Esses usuários agora podem acessar os ativos disponíveis no portal do Content Hub.

>[!NOTE]
>
>Você pode usar todos os recursos avançados da empresa, como a sincronização com Provedores de identidade externos.

### Como acessar o Content Hub? {#access-content-hub}

O Content Hub pode ser acessado das seguintes maneiras:

* Acesse o Content Hub usando o seguinte link:

  `https://experience.adobe.com/#/assets/contenthub`

* Faça logon em `experience.adobe com` e clique em **[!UICONTROL Experience Manager Assets Content Hub]**, disponível na seção **[!UICONTROL Acesso rápido]**:
  ![Acesso ao Content Hub](assets/access-content-hub.png)

* Faça logon em `experience.adobe com` e clique em **[!UICONTROL Experience Manager Assets Content Hub]** disponível no alternador de produto:
  ![Método de acesso Content Hub 3](assets/access-content-hub-alternate.png)

### Desabilitar notificações por email para usuários {#disable-email-notifications}

Se os administradores precisarem desativar as notificações por email enviadas aos usuários quando eles forem adicionados ao perfil de produto do Content Hub:

Clique no ícone de pesquisa adjacente ao nome do perfil do produto e desative a opção **[!UICONTROL Notificar usuários por email]**.

![Desabilitar notificações por email](assets/disable-email-notifications.png)


## Etapa 4: integrar usuários do Content Hub com direitos para adicionar ativos (opcional) {#onboard-content-hub-users-add-assets}

Os usuários da Content Hub com direitos para adicionar ativos podem [carregar novos ativos aprovados pela marca para a Content Hub](/help/assets/upload-brand-approved-assets.md).

Para integrar usuários do Content Hub com direitos para adicionar usuários:

1. [Depois de adicionar o usuário ao perfil de produto do Content Hub](#onboard-content-hub-users), acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos no Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   O Admin Console exibe dois perfis de produto para o AEM as a Cloud Service: Administradores e Usuários.
1. Clique no perfil de produto Usuários e em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-cs-user-product-profile.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

## Etapa 4: integrar usuários do Content Hub com direitos de remix de ativos a novas variações (Opcional) {#onboard-content-hub-users-remix-assets}

Os usuários do Content Hub com direitos para remixar ativos para novas variações podem [modificar ativos existentes usando o Adobe Express e salvar o ativo no repositório](/help/assets/edit-images-content-hub.md). A edição de ativos usando o Adobe Express só estará disponível se o usuário tiver direitos de Adobe Express.

Para integrar usuários do Content Hub com direitos de remixar ativos a novas variações:

1. [Depois de adicionar o usuário ao perfil de produto do Content Hub](#onboard-content-hub-users), acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos no Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   O Admin Console exibe dois perfis de produto para o AEM as a Cloud Service: Administradores e Usuários.
1. Clique no perfil de produto Usuários e em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-cs-user-product-profile.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

## Usuários do Experience Manager Assets {#experience-manager-assets-users}

Os usuários do Experience Manager Assets podem aprovar ativos no AEM as a Cloud Service para que eles fiquem disponíveis no Content Hub.

Para configurar usuários do Experience Manager Assets:

1. Para acessar os perfis de produto do Experience Manager Assets, clique no nome de produto do AEM as a Cloud Service na lista de produtos do Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

   O Admin Console exibe dois perfis de produto para o AEM as a Cloud Service: Administradores e Usuários.
1. Clique no perfil de produto Usuários e em **[!UICONTROL Adicionar usuários]** para adicionar o usuário ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-cs-user-product-profile.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

   >[!NOTE]
   >
   > Você não precisa ser adicionado ao [perfil de produto do Content Hub](#onboard-content-hub-users) para os usuários do Experience Manager Assets.
