---
title: Ativar o Assets Ultimate
description: Saiba como habilitar o Assets Ultimate para clientes novos e existentes.
feature: Asset Management
role: User, Admin
exl-id: 45cd8ccd-e5cf-42cd-aa7f-4ae59d0587f7
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 1%

---

# Habilitar o as a Cloud Service Ultimate [!DNL Assets] {#enable-assets-cloud-service-ultimate}

![Atualizar para o Asset Cloud Service Ultimate](/help/assets/assets/upgrade-assets-cs-ultimate-package-banner.png)

O Assets as a Cloud Service Ultimate permite executar vários recursos importantes do DAM, como gerenciamento de ativos e serviços de biblioteca, gerenciamento de segurança e direitos, conexões do Creative e do Experience Cloud, extensibilidade da interface do usuário, automação orientada por API, integrações com aplicativos Adobe e não Adobe, implantação de código personalizado e muito mais. Consulte a [Visão geral do Assets as a Cloud Service Ultimate](/help/assets/assets-ultimate-overview.md) para obter a lista completa.

## Ativar o Assets Ultimate {#enable-assets-ultimate}

Os novos clientes do Assets as a Cloud Service devem primeiro ativar o Assets Ultimate criando um novo programa usando o Cloud Manager.

Execute as seguintes etapas:

1. Como administrador do sistema, faça logon no Cloud Manager. Certifique-se de selecionar a organização correta ao fazer logon.

   >[!NOTE]
   >
   >Verifique se você foi adicionado ao perfil de produto apropriado do Cloud Manager para adicionar um novo programa. Para obter mais informações, consulte [Permissões baseadas em função no Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions).

1. [Crie um novo programa](/help/journey-onboarding/create-program.md) e [adicione ambientes](/help/journey-onboarding//create-environments.md) a ele.

   Ao criar o novo programa, na guia **[!UICONTROL Soluções e Complementos]**, selecione **[!UICONTROL Assets Ultimate]**. Você também pode expandir o **[!UICONTROL Assets Ultimate]** e selecionar o **[!UICONTROL Content Hub]** para habilitar o [Content Hub](/help/assets/product-overview.md) para distribuição de ativos.

   ![AEM Assets Ultimate](assets/aem-assets-ultimate-solutions.png)

1. Clique em **[!UICONTROL Criar]** para criar o programa. O Assets Ultimate agora está ativado para o Experience Manager Assets as a Cloud Service.

O Administrador do sistema é automaticamente qualificado como Administrador do AEM no Assets Ultimate e recebe um email para navegar até o Admin Console e gerenciar os perfis de produto disponíveis.

A instância do AEM as a Cloud Service no Admin Console inclui os seguintes perfis de produto:

* Administradores do AEM

* Usuários do AEM

* [Usuários do AEM Assets Collaborator](#onboard-collaborator-users)

* [Usuários avançados do AEM Assets](#onboard-power-users)

  ![Perfis de produto do AEM Assets](assets/aem-assets-product-profiles.png)

Se você habilitou o Content Hub para o Assets as a Cloud Service, há uma nova instância criada no AEM Assets as a Cloud Service no Admin Console com `delivery` como sufixo:

![Nova instância para o Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Se você tiver provisionado o Content Hub antes de 14 de agosto de 2024, a nova instância será criada com `contenthub` como sufixo.

Observe que não há `author` ou `publish` no nome da instância do Content Hub.

Clique no nome da instância para exibir o perfil de produto do Content Hub `AEM Assets Limited Users`.

![Perfil de produto do Content Hub](assets/content-hub-product-profile.png)

Você pode começar a adicionar usuários ou grupos de usuários a esse perfil de produto para fornecer a eles acesso ao Content Hub.

>[!NOTE]
>
>Se você tiver provisionado o Content Hub antes de 14 de agosto de 2024, o perfil de produto do Content Hub terá `contenthub` mencionado depois de `Limited Users` em vez de `delivery`.

## Ativar o Assets Ultimate para clientes existentes {#enable-assets-ultimate-existing-customers}

Os clientes existentes do Assets as a Cloud Service podem atualizar para o Assets Ultimate executando duas etapas simples. Você pode navegar até o programa Assets as a Cloud Service no Cloud Manager e ver o status de atualização no cartão Programa com base na disponibilidade de créditos do Assets Ultimate. Se houver créditos suficientes disponíveis para atualizar para o Assets Ultimate, você poderá ver o status como `Assets license upgrade required`, conforme mostrado na imagem a seguir:

![Atualização do AEM Assets para o Assets Ultimate](assets/aem-assets-upgrade-status-ultimate.png)

Se um cliente existente comprar uma nova licença para o Assets Ultimate, o status de atualização será exibido como `Assets license upgrade available`.

### Pré-requisitos para atualização {#prerequisites-assets-upgrade}

Todos os ambientes devem ser atualizados para a versão mais recente do AEM as a Cloud Service ou uma versão mínima de `2024.10.18175`. Se você não atender aos requisitos mínimos, entre em contato com o representante da Adobe para mudar para a versão necessária do AEM.

### Atualizar para o Assets Ultimate {#upgrade-assets-ultimate}

Execute as seguintes etapas:

1. Depois de alternar para os requisitos mínimos da versão do AEM, clique no nome do programa. Um cartão de Atualização é exibido acima da seção **[!UICONTROL Ambientes]**, conforme mostrado na imagem a seguir:

   ![Atualização do AEM Assets para o Assets Ultimate](assets/aem-assets-upgrade-card.png)

1. Clique em **[!UICONTROL Adicionar perfis de produto]**. O Cloud Manager exibe opções para adicionar novos perfis de produto a todos os ambientes disponíveis no programa ou em ambientes individuais.

   ![Opções de atualização do AEM Assets](assets/aem-assets-upgrade-options.png)

1. Clique em **[!UICONTROL Todos os ambientes]** para adicionar os novos perfis de produto a todos os ambientes no programa ou em **[!UICONTROL Ambientes individuais]** para adicionar os novos perfis de produto aos ambientes selecionados.

   Clicar em **[!UICONTROL Ambientes individuais]** exibe a lista de todos os ambientes disponíveis no programa.

1. Clique no ícone de Mais opções correspondente a um ambiente e selecione **[!UICONTROL Adicionar perfis de produto]** para adicionar os novos perfis de produto ao ambiente selecionado.

   ![Selecionar ambientes individuais do AEM Assets](assets/aem-assets-individual-environments.png)

   Você também pode adicionar perfis de produto a ambientes selecionados navegando até a seção **[!UICONTROL Ambientes]**, clicando no ícone Mais Opções correspondente a um ambiente e selecionando **[!UICONTROL Adicionar Perfis de Produto]**.

   O status do ambiente exibe `Adding Product Profiles` enquanto os novos perfis de produto estão sendo adicionados e, subsequentemente, exibe `Running` quando o processo é concluído.

   Você deve adicionar perfis de produto a todos os ambientes disponíveis no programa, individualmente ou em todos os ambientes, antes de executar a próxima etapa.

1. Clique em **[!UICONTROL Atualizar]**. A opção **[!UICONTROL Atualizar]** é exibida somente quando você adiciona perfis de produto a todos os ambientes disponíveis.

   ![Última etapa do processo de atualização](assets/aem-assets-upgrade-button.png)

   O processo de atualização foi concluído e você atualizou com êxito o Assets as a Cloud Service para o Assets Ultimate. O status do programa exibe `Assets Ultimate`.

   ![Status do programa após a atualização](assets/program-status-post-upgrade.png)

A instância do AEM as a Cloud Service no Admin Console agora inclui os seguintes perfis de produto:

* Administradores do AEM

* Usuários do AEM

* [Usuários do AEM Assets Collaborator](#onboard-collaborator-users)

* [Usuários avançados do AEM Assets](#onboard-power-users)

![Perfis de produto do AEM Assets](assets/aem-assets-product-profiles.png)

Se precisar que o Content Hub esteja habilitado, clique no ícone Mais opções (...) no nome do programa no Cloud Manager e selecione **[!UICONTROL Editar programa]**. Expanda **[!UICONTROL Assets Ultimate]** e clique em **[!UICONTROL Content Hub]**. Esta etapa ativa o Content Hub para Assets Ultimate. Há uma nova instância criada no AEM Assets as a Cloud Service no Admin Console com `delivery` como sufixo:

![Nova instância para o Content Hub](assets/new-instance-content-hub.png)

>[!NOTE]
>
>Se você tiver provisionado o Content Hub antes de 14 de agosto de 2024, a nova instância será criada com `contenthub` como sufixo.

Observe que não há `author` ou `publish` no nome da instância do Content Hub.

Clique no nome da instância para exibir o perfil de produto do Content Hub `AEM Assets Limited Users`.

![Perfil de produto do Content Hub](assets/content-hub-product-profile.png)

Você pode começar a adicionar usuários ou grupos de usuários a esse perfil de produto para fornecer a eles acesso ao Content Hub.

>[!NOTE]
>
>Se você tiver provisionado o Content Hub antes de 14 de agosto de 2024, o perfil de produto do Content Hub terá `contenthub` mencionado depois de `Limited Users` em vez de `delivery`.

## Integrar usuários do AEM Assets Collaborator {#onboard-collaborator-users}

Os usuários do AEM Assets Collaborator podem trabalhar com ativos do Experience Manager por meio de integrações da Assets disponíveis para sua organização em outros produtos da Adobe e aplicativos que não sejam da Adobe, criar e editar ativos usando o Adobe Express e o Firefly integrados, aproveitando modelos, kits de marca, ativos da Adobe Stock e assim por diante projetados profissionalmente, e acessar e aproveitar ativos aprovados de sua organização usando o portal AEM Assets Content Hub.

Para integrar usuários do Collaborator:

1. Acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos do Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Clique no perfil de produto Usuários do Collaborators e clique em **[!UICONTROL Adicionar usuários]** para adicionar usuários ou grupos de usuários ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-assets-collaborator-user-permissions.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

Você também pode acessar e exibir os serviços atribuídos aos usuários do Collaborator, conforme mostrado na imagem a seguir:

![Serviços para usuários do Collaborator](assets/aem-assets-collaborator-users.png)

Os serviços `Adobe Express` e `AEM Assets Collaborator Users` estão habilitados por padrão.

>[!NOTE]
>
>Você pode desativar e ativar o para ativar ou desativar os serviços disponíveis, de acordo com seus requisitos. No entanto, a Adobe recomenda usar os serviços padrão ativados para os perfis de produto.


## Integração de usuários avançados do AEM Assets {#onboard-power-users}

Os usuários avançados da AEM Assets podem acessar todos os recursos da AEM Assets, incluindo o gerenciamento de ativos, permissões, metadados e a governança e automação geral em torno de ativos digitais, trabalhar com ativos do Experience Manager por meio de integrações da Assets disponíveis para sua organização em outros aplicativos da Adobe e que não sejam da Adobe, criar e editar ativos usando o Adobe Express e o Firefly integrados, aproveitando modelos projetados profissionalmente, kits de marca, ativos da Adobe Stock e assim por diante, e acessar e aproveitar os ativos aprovados da sua organização usando o portal AEM Assets da Content Hub da.

Para integrar Usuários avançados:

1. Acesse os perfis de produto do Experience Manager Assets clicando no nome de produto do AEM as a Cloud Service na lista de produtos do Admin Console.

1. Clique na instância do autor de produção para o AEM as a Cloud Service:
   ![Perfis de produto para o AEM as a Cloud Service](assets/aem-cloud-service-instances.png)

1. Clique no perfil de produto Usuários avançados e em **[!UICONTROL Adicionar usuários]** para adicionar usuários ou grupos de usuários ao perfil de produto.
   ![Perfil de produto do usuário](assets/aem-assets-power-user-permissions.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

Você também pode acessar e visualizar os serviços atribuídos aos usuários avançados, conforme ilustrado na imagem a seguir:

![Serviços para usuários avançados](assets/aem-assets-power-users.png)

Os serviços `Adobe Express` e `AEM Assets Power Users` estão habilitados por padrão.

>[!NOTE]
>
>Você pode desativar e ativar o para ativar ou desativar os serviços disponíveis, de acordo com seus requisitos. No entanto, a Adobe recomenda usar os serviços padrão ativados para os perfis de produto.
