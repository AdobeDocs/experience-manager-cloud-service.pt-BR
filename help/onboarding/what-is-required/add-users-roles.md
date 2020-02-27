---
title: Adicionar usuários e funções - O que é necessário
description: Adicionar usuários e funções - O que é necessário
translation-type: tm+mt
source-git-commit: 936e42f273b75f0ea7776c51f57af44ec9e6d96f

---


# Adicionar usuários e funções {#add-users-roles}


Muitos recursos no [!UICONTROL Cloud Manager] exigem permissões específicas para operar. Por exemplo, somente alguns usuários podem definir os Indicadores-chave de desempenho (KPIs) para um programa. Essas permissões são logicamente agrupadas em funções.

[!UICONTROL No momento, o Cloud Manager] define quatro funções para usuários que controlam a disponibilidade de recursos específicos:

* Proprietário da empresa
* Gerente do programa
* Gerenciador de implantação
* Desenvolvedor

>[!CAUTION]
>
>Para usar o [!UICONTROL Cloud Manager], é necessário ter uma Adobe ID e o Contexto de produto dos serviços gerenciados da Adobe.

## Definições de função {#role-definitions}

>[!NOTE]
>
>A função Desenvolvedor no Admin Console não está relacionada à função Desenvolvedor no [!UICONTROL Cloud Manager].

A tabela a seguir resume as funções:

| [!UICONTROL Funções do Gerenciador] da nuvem | Descrição |
|--- |--- |
| Proprietário da empresa | Responsável por definir KPIs, aprovar implantações de produção e substituir falhas importantes de 3 níveis. |
| Gerente do programa | Usa o [!UICONTROL Cloud Manager] para executar a configuração da equipe, verificar o status e exibir os KPIs. Pode aprovar falhas importantes de 3 níveis. |
| Gerenciador de implantação | Gerencia operações de implantação. Usa o [!UICONTROL Cloud Manager] para executar implantações de estágio/produção. É possível editar Pipelines de CI/CD. Pode aprovar falhas importantes de 3 níveis. Pode obter acesso ao repositório Git. |
| Desenvolvedor | Desenvolve e testa o código personalizado do aplicativo. Usa principalmente o Gerenciador [!UICONTROL da] nuvem para exibir o status. Pode obter acesso ao repositório Git para confirmação de código. |
| Autor de conteúdo | Geralmente não interage com o [!UICONTROL Cloud Manager]. Pode usar o [!UICONTROL Cloud Manager] Program Switcher (navegando da [!UICONTROL Experience Cloud]) para acessar o AEM. |