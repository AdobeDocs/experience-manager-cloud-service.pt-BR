---
title: Direitos de acesso concedidos - O que é necessário
description: Direitos de acesso concedidos - O que é necessário
translation-type: tm+mt
source-git-commit: 4904d7728befd3562940b35c7d44dbf9cae87fee
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 11%

---


# Direitos de acesso concedidos {#access-rights-granted}

O Adobe criará um identificador **Organization** para sua empresa no Adobe Identity Management System (IMS), onde todos os usuários e suas permissões podem ser gerenciados. Cada usuário, que precisa ser membro dessa organização e receberá acesso a qualquer um dos serviços [!UICONTROL Experience Cloud], precisará ter seu próprio **Adobe ID**.

## Tipos de identidade do usuário {#user-identity-types}

Para começar a usar uma Adobe ID, visite [Gerenciar tipos de identidade do Adobe](https://helpx.adobe.com/enterprise/using/identity.html) para obter instruções detalhadas sobre como obter uma Adobe ID usando um dos tipos de identidade disponíveis.

## Usuários e funções {#users-and-roles}

Depois que a Adobe criar uma organização para sua empresa, o administrador designado será adicionado como o primeiro membro dessa organização. Por padrão, o administrador receberá as permissões de administrador e será atribuído ao [!UICONTROL AEM Managed Services] **Product** e um ou mais [!UICONTROL Perfis de] produto do **Cloud Manager**.

1. Assim que o Administrador do sistema conceder acesso ao Cloud Manager, você receberá um email que o levará até a página de logon do Cloud Manager, que também é acessível por meio do [Adobe Experience Cloud](https://my.cloudmanager.adobe.com/).

1. Na página inicial do Cloud Manager, clique em **Gerenciar acesso**.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

1. Depois de clicar em **Gerenciar Acesso**, você navega até **Admin Console** de onde pode gerenciar as funções ou permissões do usuário para o Cloud Manager.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin1.png)

   No Admin Console, é possível executar tarefas do SysAdmin, como:
   * [Gerenciando funções](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-roles)
   * [Gerenciamento do acesso à instância do autor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-access-aem)

>[!NOTE]
>Visite a seção [Usuários e funções](#users-roles) para saber mais sobre usuários e definições de funções no Cloud Manager.

Com esses direitos concedidos, seu administrador agora está configurado com um logon único (usando o Adobe ID) para acessar os serviços [!UICONTROL Experience Cloud], fazer logon nos ambientes de nuvem AEM e usar o [!UICONTROL Cloud Manager].

## Usuários e funções {#users-roles}

Muitos recursos no [!UICONTROL Cloud Manager] exigem permissões específicas para operar.

[!UICONTROL O Cloud ] Manager atualmente define quatro funções para usuários que controlam a disponibilidade de recursos específicos:

* Proprietário da empresa
* Gerenciador de programas
* Gerenciador de implantação
* Desenvolvedor

>[!CAUTION]
>
>Para usar o [!UICONTROL Cloud Manager], você deve ter um Adobe ID e o Adobe Experience Manager como um Contexto de Produto Cloud Service.

### Definições de função {#role-definitions}

>[!NOTE]
>
>A persona Desenvolvedor no Admin Console não está relacionada à função Desenvolvedor no [!UICONTROL Cloud Manager].

A tabela a seguir resume as funções:

| [!UICONTROL Funções ] do Cloud Manager | Descrição |
|--- |--- |
| Proprietário da empresa | Responsável por definir KPIs, aprovar implantações de produção e substituir falhas importantes de três níveis. |
| Gerenciador de programas | Usa [!UICONTROL Cloud Manager] para executar a configuração da equipe, analisar o status e exibir KPIs. Pode aprovar falhas importantes de três níveis. |
| Gerenciador de implantação | Gerencia operações de implantação. Usa [!UICONTROL Cloud Manager] para executar implantações de estágio/produção. É possível editar pipeline de CI/CD. Pode aprovar falhas importantes de três níveis. Pode obter acesso ao repositório Git. |
| Desenvolvedor | Desenvolve e testa o código de aplicativo personalizado. Usa principalmente [!UICONTROL Cloud Manager] para visualizar o status. Pode obter acesso ao repositório Git para confirmação de código. |
| Autor do conteúdo | Geralmente não interage com [!UICONTROL Cloud Manager]. Pode usar o [!UICONTROL Cloud Manager] Seletor de programa (navegando de [!UICONTROL Experience Cloud]) para acessar o AEM. |

### O Perfil de produto de integração {#integration-product-profile}

Além do acima, o Cloud Manager criará automaticamente um perfil de produto chamado &quot;Integrações - Cloud Service&quot;. Esse perfil de produto é usado para as integrações entre o Adobe Experience Manager e outros produtos do Adobe. Este perfil de produto **não deve** ser excluído. Se você excluir acidentalmente esse perfil, ele precisará ser recriado manualmente. O Nome de Exibição para este perfil **deve** ser `CM_CS_DEFAULT`.

