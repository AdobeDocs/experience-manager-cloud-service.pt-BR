---
title: Funções e permissões do usuário
description: Esta página descreve as funções e permissões do usuário. Siga esta página para saber como adicionar usuários e atribuí-los a funções do Cloud Manager.
translation-type: tm+mt
source-git-commit: 98c7105aed1b9092a72005cf2cfab4bcf227601f
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 9%

---


# Funções do usuário e permissões {#user-roles-permissions}

O Adobe criará um identificador **Organization** para sua empresa no Adobe Identity Management System (IMS), onde todos os usuários e suas permissões podem ser gerenciados. Cada usuário, que precisa ser membro dessa organização e receberá acesso a qualquer um dos serviços [!UICONTROL Experience Cloud], precisará ter seu próprio **Adobe ID**.

## Funções de usuário {#user-roles}

Muitos recursos no Cloud Manager exigem permissões específicas para operar.

Muitos recursos no Cloud Manager exigem permissões específicas para operar e limitam as ações que você executa na interface do usuário com base nas funções e permissões atribuídas. Em alguns casos, se você não tiver a permissão para realizar uma ação, o controle da interface estará presente, mas desativado.

Se houver uma ação que você deseja realizar, mas não puder, marque [permissões associadas às definições de função](#permissions). Dependendo da sua meta, você pode entrar em contato com o Administrador do sistema e solicitar a função necessária.

O Cloud Manager atualmente define quatro funções para usuários que controlam a disponibilidade de recursos específicos:

* Proprietário da empresa
* Gerenciador de implantação
* Gerenciador de programas
* Desenvolvedor

>[!NOTE]
>A persona Desenvolvedor no Admin Console não está relacionada à função Desenvolvedor no [!UICONTROL Cloud Manager].

## Definições de função {#role-definitions}

A tabela a seguir resume as funções:

| [!UICONTROL Funções ] do Cloud Manager | Descrição |
|--- |--- |
| Proprietário da empresa | Responsável por definir KPIs, aprovar implantações de produção e substituir falhas importantes de três níveis. |
| Gerenciador de programas | Usa [!UICONTROL Cloud Manager] para executar a configuração da equipe, analisar o status e exibir KPIs. Pode aprovar falhas importantes de três níveis. |
| Gerenciador de implantação | Gerencia operações de implantação. Usa [!UICONTROL Cloud Manager] para executar implantações de estágio/produção. É possível editar pipeline de CI/CD. Pode aprovar falhas importantes de três níveis. Pode obter acesso ao repositório Git. |
| Desenvolvedor | Desenvolve e testa o código de aplicativo personalizado. Usa principalmente [!UICONTROL Cloud Manager] para visualizar o status. Pode obter acesso ao repositório Git para confirmação de código. |
| Autor do conteúdo | Geralmente não interage com [!UICONTROL Cloud Manager]. Pode usar o [!UICONTROL Cloud Manager] Seletor de programa (navegando de [!UICONTROL Experience Cloud]) para acessar o AEM. |

### Exibindo suas funções {#view-roles}

Para exibir sua função no Cloud Manager, faça logon na interface do usuário do Cloud Manager, selecione o ícone de perfil no canto superior direito e selecione **Funções do usuário**, conforme mostrado na figura abaixo.

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### O Perfil de produto de integração {#integration-product-profile}

Além do acima, o Cloud Manager criará automaticamente um perfil de produto chamado &quot;Integrações - Cloud Service&quot;. Esse perfil de produto é usado para as integrações entre o Adobe Experience Manager e outros produtos do Adobe. Este perfil de produto **não deve** ser excluído. Se você excluir acidentalmente esse perfil, ele precisará ser recriado manualmente. O Nome de Exibição para este perfil **deve** ser `CM_CS_DEFAULT`.


## Permissões associadas a Definições de função {#permissions}

[!UICONTROL O Cloud Manager tem funções pré-configuradas com permissões apropriadas. ] Por exemplo, um desenvolvedor desenvolve código e tem permissão para enviar o código para o **Repositório Git**. Como alternativa, um proprietário de negócios tem permissões diferentes que permitem definir os Indicadores-chave de desempenho (KPIs) e aprovar implantações.


Cada uma das funções tem permissões específicas associadas a cada função. A tabela a seguir resume as funções, lista as funções disponíveis e as funções que podem executar a função.

| Permissão | Descrição | Proprietário da empresa | Gerenciador de implantação | Gerenciador de programas | Desenvolvedor |
|--- |--- |--- |--- |--- |--- |
| Adicionar programa | Adicione um novo programa. | x |  |  |  |
| Criar ambiente | Crie Ambientes Prod+Stage, Dev. | x | x |  |  |
| Ambiente de atualização | Atualize Ambientes Prod+Stage, Dev. | x | x |  |  |
| Excluir ambiente | Exclua Ambientes sem produção, desenvolvimento e desenvolvimento. | x | x |  |  |
| Configuração de pipeline | Configurar ou editar pipeline. |  | x |  |  |
| Execução de pipeline | Inicie o pipeline. | x | x |  |  |
| Execução de pipeline | Rejeitar/Aprovar Falhas Importantes De 3 Camadas. | x | x | x |  |
| Execução de pipeline | Forneça Aprovação De GoLive. | x | x | x |  |
| Execução de pipeline | Agendar implantação de produção. | x | x | x |  |
| Exclusão de pipeline | Permite a exclusão de um pipeline. |  | x |  |  |
| Cancelamento de execução | Cancelar Execução Atual. |  | x |  |  |
| Gerar Token de Acesso Pessoal | Acesse o Git. |  | x |  | x |