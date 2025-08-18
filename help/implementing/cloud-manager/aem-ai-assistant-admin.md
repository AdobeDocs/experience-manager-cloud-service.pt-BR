---
title: Configurar o assistente de IA no Adobe Experience Manager
description: Saiba como configurar o Assistente de IA usando o Admin Console no Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: a7f3dc14-29f7-473a-9870-d52393e6fa6e
source-git-commit: e853e7b46c762ab724d5eecb344897a83e4fb724
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 2%

---

# Configurar o assistente de IA no Adobe Experience Manager {#aem-ai-asst-admin-setup}

Um administrador precisa definir o acesso, as permissões e as configurações para que os usuários em sua organização possam usar os recursos do AEM (Adobe Experience Manager) AI Assistant.

O processo de configuração do Assistente de IA do AEM consiste nas seguintes etapas:

1. [Crie um novo perfil de produto no Adobe Admin Console](#create-profile).
1. [Habilitar a permissão Conhecimento de Produto do Assistente de IA](#enable-permission).
1. [Criar um novo grupo de usuários (ou usar um grupo de usuários existente)](#create-user-group).
1. [Adicionar usuários ao grupo de usuários](#add-users).
1. [Atribuir o perfil de produto ao grupo de usuários](#assign-product-profile).

**Pré-requisitos**

Antes de começar, verifique se os seguintes pré-requisitos foram atendidos:

* Você deve ter no mínimo direitos de administrador de produto no Adobe Admin Console.
* Você entende a estrutura de gerenciamento de usuários de sua organização.

**Considerações de configuração**

* Tempo de processamento: os recursos criados no Cloud Manager podem levar até 2 minutos para serem exibidos na Admin Console para configuração de permissão.
* Vários perfis: os usuários podem fazer parte de vários perfis e as permissões são combinadas de todos os perfis atribuídos.
* Escopo da organização: algumas permissões podem ser aplicadas no nível da organização em todos os programas.
* Perfis predefinidos: não exclua perfis de permissão predefinidos da Admin Console.


## 1 - Criar um novo perfil de produto no Adobe Admin Console{#create-profile}

1. Siga as instruções detalhadas em [Criar um novo perfil de produto no Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile), encontradas na documentação do Experience Platform.

1. Ao criar o novo perfil de produto, você pode usar os seguintes valores sugeridos para o Assistente de IA.

   | Campo de texto | Valor sugerido |
   | --- | --- |
   | Nome do perfil do produto | `AEM AI Assistant` (ou seu nome descritivo preferido) |
   | Nome de exibição (opcional) | `AI Assistant` |
   | Descrição (opcional) | `Product profile for managing AEM AI Assistant access` |
   | Notificação | Configure com base nas preferências de sua organização |


## 2 - Ativar a permissão de conhecimento do produto AI Assistant{#enable-permission}

O processo para atribuir permissões personalizadas a perfis de produtos segue o fluxo de trabalho padrão de permissões personalizadas do Adobe Cloud Manager.

Artigo de referência: [Atribuir permissões personalizadas ao novo perfil de produto](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Na Admin Console, clique no nome do perfil de produto recém-criado (`AEM AI Assistant`)

   ![Captura de tela](/help/implementing/cloud-manager/assets/ai-assistant-console.png)

1. Para exibir a lista de permissões editáveis, clique na guia **Permissões**.

1. Na lista de tabelas, localize a permissão `AI Assistant Product Knowledge`.

   ![Guia Permissões do Assistente de IA no Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-permission.png)

1. À direita do nome da permissão, clique em ![Ícone de lápis ou ícone Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. Na página **Editar Permissões do Assistente de IA**, ative a opção **Conhecimento de Produto do Assistente de IA**.

   ![Página Editar Permissões para a opção de alternância Conhecimento de Produto do Assistente de IA](/help/implementing/cloud-manager/assets/ai-assistant-prod-knowledge.png)

1. No canto inferior direito da página, clique em **Salvar**.

   O perfil de produto agora tem a permissão Assistente de IA Conhecimento do produto ativada.


## 3 - Criar um novo grupo de usuários (ou usar um grupo de usuários existente){#create-user-group}

1. Siga uma das seguintes opções:

>[!BEGINTABS]

>[!TAB Criar um novo grupo de usuários]

1. Na Admin Console, clique em **Usuários** > **Grupos de usuários**.

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

1. Na página **`Add users to this user group`**, pesquise e selecione os usuários que precisam de acesso ao Assistente do AEM AI.

   ![Adicionar usuários a esta página de grupo de usuários](/help/implementing/cloud-manager/assets/ai-assistant-add-users-to-this-group.png)

1. No canto inferior direito da página, clique em **Salvar**.
1. Agora, atribua o perfil de produto ao grupo de usuários](#assign-product-profile).

>[!TAB Adicionar usuários em massa]

Você pode usar o recurso de upload em massa na Admin Console.

1. Prepare um arquivo CSV com informações do usuário.
1. Use a opção **`Add users by CSV`** para uma adição em massa eficiente.
1. Agora, atribua o perfil de produto ao grupo de usuários](#assign-product-profile).

>[!ENDTABS]


## 5 - Atribuir o perfil de produto ao grupo de usuários{#assign-product-profile}

Esta etapa segue o fluxo de trabalho padrão do Adobe Admin Console para atribuição de perfis de produto a grupos de usuários.

Artigo de referência: [Gerenciar perfis de produto para usuários corporativos](https://helpx.adobe.com/br/enterprise/using/manage-product-profiles.html)

1. Ainda no grupo de usuários do AEM AI Assistant do [4 - Adicionar usuários ao grupo de usuários](#add-users), clique na guia **Perfis de produto atribuídos**.
1. Clique em **Atribuir perfil**.

   ![Página de grupo de usuários do AEM AI Assistant com a guia Perfis de produto atribuídos selecionada](/help/implementing/cloud-manager/assets/ai-assistant-assign-profile.png)

1. Na página **Atribuir produtos e perfis**, na caixa de diálogo **Selecionar perfis de produtos**, pesquise e selecione seu perfil de produto **Assistente de IA**.

   ![A página &quot;Atribuir produtos e perfis&quot;, mostrando a caixa de diálogo &quot;Selecionar perfis de produtos&quot; e o perfil de produto &quot;Assistente de IA&quot; selecionado](/help/implementing/cloud-manager/assets/ai-assistant-select-product-profile.png)

1. Próximo ao canto inferior direito da caixa de diálogo, clique em **Aplicar**.
1. Próximo ao canto inferior direito da página **Atribuir produtos e perfis**, clique em **Salvar**.

   ![O perfil de produto do Assistente de IA mostrado foi atribuído ao grupo de usuários do Assistente de IA da AEM](/help/implementing/cloud-manager/assets/ai-assistant-profile-assigned-to-user-group.png)


## Verificar a configuração

* Verifique se o perfil de produto mostra o número correto de grupos de usuários atribuídos.
* Verifique se o grupo de usuários mostra o número correto de usuários.
* Confirme se a permissão Conhecimento do produto do assistente do AI está ativada e configurada corretamente.


## Testar a configuração

Faça com que um usuário do grupo atribuído faça o seguinte:

1. Faça logon no AEM.
2. Verifique se os recursos do Assistente de IA estão acessíveis.
3. Teste a funcionalidade do Assistente de IA para garantir a ativação correta.

## Consulte também:

* [Controle de acesso do Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
* [Permissões personalizadas do Cloud Manager](/help/implementing/cloud-manager/custom-permissions.md)


