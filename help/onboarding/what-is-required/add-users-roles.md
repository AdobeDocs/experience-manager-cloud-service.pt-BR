---
title: Adicionar usuários e funções - O que é necessário
description: Adicionar usuários e funções - O que é necessário
translation-type: tm+mt
source-git-commit: 2c21414edd6c3178d05c818d2bf57aa152b5956b
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 6%

---


# Adicionar usuários e funções {#add-users-roles}


Muitos recursos no [!UICONTROL Cloud Manager] exigem permissões específicas para operar.

[!UICONTROL O Cloud ] Manager atualmente define quatro funções para usuários que controlam a disponibilidade de recursos específicos:

* Proprietário da empresa
* Gerenciador de programas
* Gerenciador de implantação
* Desenvolvedor

>[!CAUTION]
>
>Para usar o [!UICONTROL Cloud Manager], você deve ter uma Adobe ID e o Contexto de produto do Adobe Experience Manager as a Cloud Service.

## Definições de função {#role-definitions}

>[!NOTE]
>
>A persona do desenvolvedor no Admin Console não está relacionada à função do desenvolvedor no [!UICONTROL Cloud Manager].

A tabela a seguir resume as funções:

| [!UICONTROL Funções ] do Cloud Manager | Descrição |
|--- |--- |
| Proprietário da empresa | Responsável por definir KPIs, aprovar implantações de produção e substituir falhas importantes de três níveis. |
| Gerenciador de programas | Usa [!UICONTROL Cloud Manager] para executar a configuração da equipe, analisar o status e exibir KPIs. Pode aprovar falhas importantes de três níveis. |
| Gerenciador de implantação | Gerencia operações de implantação. Usa [!UICONTROL Cloud Manager] para executar implantações de estágio/produção. É possível editar pipeline de CI/CD. Pode aprovar falhas importantes de três níveis. Pode obter acesso ao repositório Git. |
| Desenvolvedor | Desenvolve e testa o código de aplicativo personalizado. Usa principalmente [!UICONTROL Cloud Manager] para visualizar o status. Pode obter acesso ao repositório Git para confirmação de código. |
| Autor do conteúdo | Geralmente não interage com [!UICONTROL Cloud Manager]. Pode usar o [!UICONTROL Cloud Manager] Alternador de programas (navegando de [!UICONTROL Experience Cloud]) para acessar o AEM. |

## O Perfil de produto de integração {#integration-product-profile}

Além do acima, o Cloud Manager criará automaticamente um perfil de produto chamado &quot;Integrações - Cloud Service&quot;. Esse perfil de produto é usado para as integrações entre o Adobe Experience Manager e outros produtos da Adobe. Este perfil de produto **não deve** ser excluído. Se você excluir acidentalmente esse perfil, ele precisará ser recriado manualmente. O Nome de Exibição para este perfil **deve** ser `CM_CS_DEFAULT`.
