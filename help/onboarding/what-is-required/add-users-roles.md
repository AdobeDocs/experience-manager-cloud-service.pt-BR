---
title: Adicionar usuários e funções - O que é necessário
description: Adicionar usuários e funções - O que é necessário
translation-type: tm+mt
source-git-commit: 936e42f273b75f0ea7776c51f57af44ec9e6d96f
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 8%

---


# Adicionar usuários e funções {#add-users-roles}


Muitos recursos no [!UICONTROL Cloud Manager] exigem permissões específicas para operar. Por exemplo, somente alguns usuários podem definir os Indicadores-chave de desempenho (KPIs) para um programa. Essas permissões são logicamente agrupadas em funções.

[!UICONTROL Atualmente, o Cloud ] Manager define quatro funções para usuários que controlam a disponibilidade de recursos específicos:

* Proprietário da empresa
* Gerenciador de programas
* Gerenciador de implantação
* Desenvolvedor

>[!CAUTION]
>
>Para usar o [!UICONTROL Cloud Manager], você deve ter um Contexto de produto Adobe ID e o Adobe Managed Services.

## Definições de função {#role-definitions}

>[!NOTE]
>
>A função Desenvolvedor no Admin Console não está relacionada à função Desenvolvedor no [!UICONTROL Cloud Manager].

A tabela a seguir resume as funções:

| [!UICONTROL Funções ] do Cloud Manager | Descrição |
|--- |--- |
| Proprietário da empresa | Responsável por definir KPIs, aprovar implantações de produção e substituir falhas importantes de 3 níveis. |
| Gerenciador de programas | Usa [!UICONTROL o Cloud Manager] para executar a configuração da equipe, verificar o status e visualização de KPIs. Pode aprovar falhas importantes de 3 níveis. |
| Gerenciador de implantação | Gerencia operações de implantação. Usa [!UICONTROL o Gerenciador de nuvem] para executar implantações de estágio/produção. É possível editar Pipelines de CI/CD. Pode aprovar falhas importantes de 3 níveis. Pode obter acesso ao repositório Git. |
| Desenvolvedor | Desenvolve e testa o código personalizado do aplicativo. Utiliza principalmente [!UICONTROL o Gerenciador de nuvem] para o status da visualização. Pode obter acesso ao repositório Git para confirmação de código. |
| Autor de conteúdo | Geralmente, não interage com [!UICONTROL Gerenciador de nuvem]. Pode usar [!UICONTROL o Gerenciador de nuvem] o Comutador de Programas (navegando de [!UICONTROL Experience Cloud]) para acessar AEM. |