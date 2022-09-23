---
title: Grupos de usuários para notificações
description: Saiba como criar um grupo de usuários no Admin Console para gerenciar o recebimento de notificações por email importantes.
feature: Onboarding
role: Admin, User, Developer
source-git-commit: b56bb15f8330deefc11d19e784e36590ef674dd8
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 1%

---


# Grupos de usuários para notificações {#user-groups}

Saiba como criar um grupo de usuários no Admin Console para gerenciar o recebimento de notificações por email importantes.

## Visão geral {#overview}

Periodicamente, o Adobe precisa entrar em contato com os usuários com relação aos ambientes as a Cloud Service AEM. Além das notificações no produto, o Adobe também usa ocasionalmente emails para notificações. Há dois tipos de notificações por email:

* **Notificação de Incidente** - Essas notificações são enviadas durante um incidente ou quando o Adobe identificou um problema potencial de disponibilidade com seu ambiente as a Cloud Service AEM.
* **Notificação proativa** - Essas notificações são enviadas quando um membro da equipe de suporte do Adobe deseja fornecer orientação sobre uma possível otimização ou recomendação que pode beneficiar seu ambiente as a Cloud Service AEM.

Para que os usuários corretos recebam essas notificações, é necessário configurar e atribuir grupos de usuários e descritos neste documento.

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

1. Você verá a lista de todos os perfis de produtos do Cloud Manager configurados.

   ![Criar grupo de usuários](assets/cloud_manager_profiles.png)

1. Clique em **Novo perfil** e fornecer as seguintes informações:

   * **Nome do perfil do produto**: `Incident Notification - Cloud Service`
   * **Nome de exibição**: `Incident Notification - Cloud Service`
   * **Descrição**: Perfil do Cloud Manager para os usuários que receberão notificações durante um incidente ou quando o Adobe identificar um possível problema de disponibilidade com seu ambiente as a Cloud Service AEM

1. Clique em **Salvar**.

1. Clique em **Novo perfil** mais uma vez e forneça os seguintes detalhes:

   * **Nome do perfil do produto**: `Proactive Notification - Cloud Service`
   * **Nome de exibição**: `Proactive Notification - Cloud Service`
   * **Descrição**: Perfil do Cloud Manager para usuários que receberão notificações quando um membro da equipe de suporte do Adobe quiser fornecer orientação sobre uma possível otimização ou recomendação para fazer com a configuração do ambiente as a Cloud Service AEM

1. Clique em **Salvar**.

Seus dois novos grupos de notificação são criados.

>[!NOTE]
>
>É importante que o Cloud Manager **nome do perfil do produto** é exatamente o mesmo que foi fornecido. Copie e cole o nome de perfil de produto fornecido para evitar erros. Quaisquer desvios ou erros de digitação farão com que as notificações não sejam enviadas conforme desejado.
>
>Em caso de erro ou se os perfis não tiverem sido definidos, o Adobe assumirá como padrão a notificação de usuários existentes atribuídos à variável **Desenvolvedor do Cloud Manager** ou **Gerenciador de implantação** perfis.

## Atribua os usuários aos novos perfis de produto de notificação {#add-users}

Agora que os grupos foram criados, é necessário atribuir os usuários apropriados. Você pode fazer isso ao criar novos usuários ou ao atualizar usuários existentes.

### Adicionar novos usuários a grupos {#new-user}

Siga estas etapas para adicionar usuários para os quais as Federated IDs ainda não foram configuradas.

1. Identifique os usuários que devem receber notificações de incidente ou proativas.

1. Faça logon no Admin Console at [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) se você ainda não estiver conectado.

1. No **Visão geral** página, selecione **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![Usuários](assets/product_services.png)

1. Se a ID federada dos membros da equipe ainda não tiver sido configurada, selecione a variável **Usuários** na navegação superior, em seguida, selecione **Adicionar usuário**. Caso contrário, pule para a seção [Adicionar usuários existentes a grupos.](#existing-users)

   ![Usuários](assets/cloud_manager_add_user.png)

1. No **Adicionar usuários à equipe** , insira a ID de email do usuário que deseja adicionar e selecione `Adobe ID` para **Tipo de ID**.

1. Clique no botão de mais sob a **Selecionar produtos** para iniciar a seleção do produto.

1. Selecionar **Adobe Experience Manager as a Cloud Service** e atribua um ou ambos os novos grupos ao usuário.

   * **Notificação de incidente - Cloud Service**
   * **Notificação proativa - Cloud Service**

1. Clique em **Salvar** e um email de boas-vindas é enviado ao usuário adicionado.

O usuário convidado receberá as notificações. Repita essas etapas para os usuários de sua equipe que gostaria de receber notificações.

### Adicionar usuários existentes a grupos {#existing-user}

Siga estas etapas para adicionar usuários para os quais já existem IDs federadas.

1. Identifique os usuários que devem receber notificações de incidente ou proativas.

1. Faça logon no Admin Console at [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com) se você ainda não estiver conectado.

1. No **Visão geral** página, selecione **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

1. Selecione o **Usuários** na navegação superior.

1. Se a ID federada já existir para o membro da equipe que você deseja adicionar a um grupo de notificação, localize esse usuário na lista e clique nele. Caso contrário, pule para a seção [Adicionar novos usuários a grupos.](#add-user)

1. No **Produtos** seção da janela de detalhes do usuário, clique no botão reticências e selecione **Editar**.

1. No **Editar produtos** clique no botão de lápis abaixo da janela **Selecionar produtos** para iniciar a seleção do produto.

1. Selecionar **Adobe Experience Manager as a Cloud Service** e atribua um ou ambos os novos grupos ao usuário.

   * **Notificação de incidente - Cloud Service**
   * **Notificação proativa - Cloud Service**

1. Clique em **Salvar** e um email de boas-vindas é enviado ao usuário adicionado.

O usuário convidado receberá as notificações. Repita essas etapas para os usuários de sua equipe que gostaria de receber notificações.
