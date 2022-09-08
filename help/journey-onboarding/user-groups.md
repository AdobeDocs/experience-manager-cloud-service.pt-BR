---
title: Grupos de usuários para notificações
description: Saiba como criar um grupo de usuários no Admin Console para gerenciar o recebimento de notificações por email importantes.
feature: Onboarding
role: Admin, User, Developer
source-git-commit: a663e21d100953f87c012a1d7962fb0e88e6a7f2
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---


# Grupos de usuários para notificações {#user-groups}

Saiba como criar um grupo de usuários no Admin Console para gerenciar o recebimento de notificações por email importantes.

## Visão geral {#overview}

De tempos em tempos, o Adobe precisa entrar em contato com relação aos ambientes as a Cloud Service AEM. Além da notificação no produto, o Adobe também usa ocasionalmente emails para essas notificações. Existem dois tipos de notificação:

* **Notificação de Incidente - Cloud Service** - Essas notificações são enviadas durante um incidente ou quando o Adobe identificou um problema potencial de disponibilidade com seu ambiente as a Cloud Service AEM.
* **Notificação proativa - Cloud Service** - Essas notificações são enviadas quando um membro da equipe de suporte do Adobe deseja fornecer orientação sobre uma possível otimização ou recomendação que pode beneficiar seu ambiente as a Cloud Service AEM.

Para que os usuários corretos recebam essas notificações, é necessário configurar os grupos de usuários.

## Pré-requisitos {#prerequisites}

Como os grupos de usuários são criados e mantidos no Admin Console, antes de criar grupos de usuários para notificações, você deve:

* Ter permissões para adicionar e editar associações de grupo.
* Ter um perfil Adobe Admin Console válido.

## Criar novos perfis de produto do Cloud Manager {#create-groups}

Para configurar corretamente o recebimento de notificações, será necessário criar dois grupos de usuários. Essas etapas só devem ser feitas uma vez.

1. Faça logon no Admin Console at [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. No **Visão geral** página, selecione **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![Grupos de usuários](assets/products_services.png)

1. Navegue até o **Cloud Manager** da lista de todas as instâncias.

   ![Criar grupo de usuários](assets/cloud_manager_instance.png)

1. Você verá a lista de todos os perfis de produtos do Cloud Manager configurados. Por exemplo:

   ![Criar grupo de usuários](assets/cloud_manager_profiles.png)

1. Clique em Novo perfil e insira os seguintes detalhes:

* Nome do perfil de produto: Notificação de incidente - Cloud Service
* Nome de exibição: Notificação de incidente - Cloud Service
* Descrição: Perfil do Cloud Manager para os usuários que receberão notificações durante um incidente ou quando o Adobe identificar um possível problema de disponibilidade com seu ambiente as a Cloud Service AEM.

1. Clique em Salvar e repita a etapa 4 com os seguintes detalhes:

* Nome do perfil de produto: Notificação proativa - Cloud Service
* Nome de exibição: Notificação proativa - Cloud Service
* Descrição: Perfil do Cloud Manager para os usuários que receberão notificações quando um membro da equipe de suporte do Adobe quiser fornecer orientação sobre uma possível otimização ou recomendação para fazer com a configuração do ambiente as a Cloud Service AEM.

>[!NOTE]
>
>É importante que o nome do perfil do Cloud Manager seja exatamente o mesmo que acima. Copie e cole o nome do perfil do produto na descrição fornecida. Quaisquer desvios ou erros de digitação farão com que as notificações não sejam enviadas conforme desejado. Em caso de erro ou se os perfis não tiverem sido definidos, o Adobe assumirá como padrão a notificação de usuários existentes atribuídos ao Desenvolvedor do Cloud Manager (é ele ou , ou e) aos perfis do Gerenciador de implantação.

## Atribua os usuários aos novos perfis de produto de notificação {#add-users}

Agora que os grupos foram criados, é necessário atribuir os usuários apropriados. Você pode fazer isso ao criar novos usuários ou ao atualizar usuários existentes.

### Adicionar novos usuários a grupos {#new-user}

1. Identifique os usuários que devem receber notificações de incidente ou proativas.

1. Faça logon no Admin Console at [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) se você ainda não estiver conectado.

1. No **Visão geral** página, selecione **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![Usuários](assets/product_services.png)

1. Selecione o **Usuários** na navegação superior, em seguida, selecione **Adicionar usuário**.

![Usuários](assets/cloud_manager_add_user.png)

1. Na caixa de diálogo Adicionar usuários à equipe , digite a ID do email do usuário que deseja adicionar.

* Se a ID federada dos membros da equipe ainda não tiver sido configurada, selecione Adobe ID para o Tipo de ID.
* Se o usuário já existir, consulte a etapa 7.

1. Clique no botão de mais sob a **Selecionar produtos** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribuir **Notificação de incidente - Cloud Service** ou **Notificação proativa - Cloud Service**, ou ambos para o usuário.

1. Clique em **Salvar** e um email de boas-vindas é enviado ao usuário adicionado. O usuário convidado receberá as notificações.

1. Repita essas etapas para os usuários de sua equipe que gostaria de receber as notificações.

1. Caso o usuário já exista, pesquise o nome do usuário e:

* Clique no nome do usuário.
* No **Produtos** seção , clique em **Editar**.
* Clique no botão de lápis no **Selecionar produtos** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribuir **Notificação de incidente - Cloud Service** ou **Notificação proativa - Cloud Service**, ou ambos para o usuário.
* Clique em **Salvar** e um email de boas-vindas é enviado ao usuário adicionado. O usuário convidado receberá as notificações.
