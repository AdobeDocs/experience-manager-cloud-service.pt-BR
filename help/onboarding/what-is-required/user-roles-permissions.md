---
title: Funções e permissões do usuário
description: Esta página descreve as funções e permissões do usuário. Siga esta página para saber como adicionar usuários e atribuí-los a funções do Cloud Manager.
translation-type: tm+mt
source-git-commit: 4b9476b094438acd08c945f0102b029b6792cb88
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 10%

---


# Funções do usuário e permissões {#user-roles-permissions}

## Funções de usuário {#user-roles}

Muitos recursos no Cloud Manager exigem permissões específicas para operar e limitam as ações que você executa na interface do usuário com base nas funções e permissões atribuídas. Em alguns casos, se você não tiver a permissão para realizar uma ação, o controle da interface estará presente, mas desativado.

Se houver uma ação que você deseja realizar, mas não puder, marque a seção abaixo, [Funções e permissões do usuário](#permissions). Dependendo da sua meta, você pode entrar em contato com o Administrador do sistema e solicitar a função necessária.

O Cloud Manager atualmente define quatro funções para usuários que controlam a disponibilidade de recursos específicos:

* Proprietário da empresa
* Gerenciador de implantação
* Gerenciador de programas
* Desenvolvedor

>[!NOTE]
>A persona Desenvolvedor no Admin Console não está relacionada à função Desenvolvedor no [!UICONTROL Cloud Manager].

## Exibindo suas funções {#view-roles}

Para exibir sua função no Cloud Manager, faça logon na interface do usuário do Cloud Manager, selecione o ícone de perfil no canto superior direito e selecione **Funções do usuário**, conforme mostrado na figura abaixo.

>[!NOTE]
>Consulte [Navegue até o Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md) para saber mais sobre como fazer logon no Cloud Manager.

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### O Perfil de produto de integração {#integration-product-profile}

Além do acima, o Cloud Manager criará automaticamente um perfil de produto chamado &quot;Integrações - Cloud Service&quot;. Esse perfil de produto é usado para as integrações entre o Adobe Experience Manager e outros produtos do Adobe. Este perfil de produto **não deve** ser excluído. Se você excluir acidentalmente esse perfil, ele precisará ser recriado manualmente. O Nome de Exibição para este perfil **deve** ser `CM_CS_DEFAULT`.


## Funções do usuário e permissões {#permissions}

[!UICONTROL O Cloud Manager tem funções pré-configuradas com permissões apropriadas. ] Por exemplo, um desenvolvedor desenvolve código e tem permissão para enviar o código para o **Repositório Git**. Como alternativa, um proprietário de negócios tem permissões diferentes que permitem adicionar e editar programas, adicionar ambientes e aprovar implantações.

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