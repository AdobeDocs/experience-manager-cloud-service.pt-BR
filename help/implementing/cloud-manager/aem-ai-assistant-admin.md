---
title: Configurar o assistente de IA no Adobe Experience Manager
description: Saiba como configurar o Assistente de IA usando o Admin Console no Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: ab8fefe18e43c1fe937d0d16df65b6137fc8a292
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 3%

---

# Configurar o AEM AI Assistant - Configuração do administrador {#aem-ai-asst-admin-setup}

Um Administrador deve definir o acesso, as permissões e as configurações para que os usuários em sua organização possam usar os recursos no Assistente do AEM AI. Este artigo descreve como ativar o Assistente de IA para sua organização, configurar as credenciais necessárias e salvar as alterações de configuração.

**Visão geral do processo de configuração do AEM AI Assistant**

O processo de configuração consiste nas seguintes etapas:

1. Crie um novo perfil de produto no Adobe Admin Console.
1. Ative a permissão &quot;Conhecimento de produto do assistente de IA&quot;.
1. Criar ou usar um grupo de usuários existente.
1. Adicionar usuários ao grupo de usuários.
1. Atribua o perfil de produto ao grupo de usuários.

**Pré-requisitos**

Antes de começar, verifique se os seguintes pré-requisitos foram atendidos:

* Você deve ter no mínimo direitos de administrador de produto no Adobe Admin Console.
* Você entende a estrutura de gerenciamento de usuários de sua organização.

## 1 - Criar um novo perfil de produto no Adobe Admin Console{#create-profile}

1. Siga as instruções detalhadas em [Criar um novo perfil de produto no Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile) localizado na documentação do Experience Platform.

1. Ao criar o novo perfil de produto, use os exemplos a seguir dos valores que você pode usar para o Assistente de IA.

   | Campo de texto | Valor sugerido |
   | --- | --- |
   | Nome do perfil do produto | `AEM AI Assistant` (ou seu nome descritivo preferido) |
   | Nome de exibição (opcional) | `AI Assistant` |
   | Descrição (opcional) | `Product profile for managing AEM AI Assistant access` |
   | Notificação | Configure com base nas preferências de sua organização |




## 2 - Ativar a permissão &quot;Conhecimento de produto do AI Assistant&quot;{#enable-permission}

O processo para atribuir permissões personalizadas a perfis de produtos segue o fluxo de trabalho padrão de permissões personalizadas do Adobe Cloud Manager.

Artigo de referência: [Atribuir permissões personalizadas ao novo perfil de produto](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Na Admin Console, clique no nome do perfil de produto recém-criado (`AEM AI Assistant`)

   ![Captura de tela](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. Para exibir a lista de permissões editáveis, clique na guia **Permissões**.

1. Na lista de tabelas, localize a permissão `AI Assistant Product Knowledge`.

   ![Guia Permissões do Assistente de IA no Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. À direita do nome da permissão, clique em ![Ícone de lápis ou ícone Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. Na página **Editar Permissões para o Assistente de IA**, ative a opção **Conhecimento de Produto do Assistente de IA**.

   ![Página Editar Permissões para a opção de alternância Conhecimento de Produto do Assistente de IA](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. No canto inferior direito da página, clique em **Salvar**.

   O perfil de produto agora tem a permissão Assistente de IA Conhecimento do produto ativada.


## 3 - Criar um grupo de usuários (ou usar um grupo de usuários existente){#create-user-group}

1. Siga uma das seguintes opções:

>[!BEGINTABS]

>[!TAB Criar um novo grupo de usuários]

1. No Admin Console, clique em **Usuários** > **Grupos de usuários**.

   ![Grupos de usuários](/help/implementing/cloud-manager/assets/ai-assistant-user-groups.png)

1. Na página **Grupos de usuários**, clique em **Novo grupo de usuários**.

   ![Botão Novo grupo de usuários na página Grupos de usuários](/help/implementing/cloud-manager/assets/ai-assistant-new-user-group.png)

1. Na página **Criar um novo grupo de usuários**, forneça as seguintes informações:

   | Opção | Valor sugerido |
   | --- | --- |
   | Nome do grupo de usuários | `AEM AI Assistant` (ou seu nome preferido) |
   | Descrição (opcional) | `User group for managing AEM AI Assistant access` |

   ![Criar uma nova página de grupo de usuários](/help/implementing/cloud-manager/assets/ai-assistant-create-new-user-group.png)

1. No canto inferior direito da página, clique em **Salvar**.

>[!TAB Usar um grupo de usuários existente]

Você pode usar um grupo de usuários existente do AEM se ele atender aos requisitos de acesso do Assistente de IA, em vez de criar um novo grupo.

>[!ENDTABS]

## 4 - Adicionar usuários ao grupo de usuários{#add-users}

1. Siga uma das seguintes opções:

>[!BEGINTABS]

>[!TAB Adicionar usuários individuais]

1. Na página **Grupos de usuários**, na tabela **Nome do grupo**, clique no nome do grupo de usuários recém-criado ou em um nome de grupo de usuários existente.

   ![Página de grupos de usuários mostrando o nome do grupo de usuários do Assistente do AEM AI na tabela](/help/implementing/cloud-manager/assets/ai-assistant-user-group-name-in-table.png)

1. Na página **Grupos de usuários** do **Assistente do AEM AI**, clique na guia **Usuários** e em **Adicionar usuários**.

   ![A página de grupos de usuários do AEM AI Assistant, mostrando a guia Usuários e o botão Adicionar usuários](/help/implementing/cloud-manager/assets/ai-assistant-add-users.png)

1. Na página **Adicionar usuários a este grupo de usuários**, procure e selecione os usuários que precisam de acesso ao Assistente do AEM AI.

   ![Adicionar usuários a esta página de grupo de usuários](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. No canto inferior direito da página, clique em **Salvar**.

>[!TAB Adicionar usuários em massa]

Você pode usar o recurso de upload em massa na Admin Console.

1. Prepare um arquivo CSV com informações do usuário.

1. Use a opção **Adicionar usuários por CSV** para uma adição eficiente em massa.

>[!ENDTABS]




## 5 - Atribuir o perfil de produto ao grupo de usuários{#assign-product-profile}




