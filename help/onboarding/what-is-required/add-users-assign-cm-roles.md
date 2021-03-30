---
title: 'Adicionar usuários e atribuir funções do Cloud Manager '
description: Siga esta página para saber como adicionar usuários e atribuí-los às funções do Cloud Manager
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 6%

---


# Adicionar usuários e atribuir funções do Cloud Manager {#add-users-assign}

O Adobe criará um identificador **Organization** para sua empresa no Adobe Identity Management System (IMS), onde todos os usuários e suas permissões podem ser gerenciados. Cada usuário, que precisa ser membro dessa organização e receberá acesso a qualquer um dos serviços [!UICONTROL Experience Cloud], precisará ter seu próprio **Adobe ID**.

## Como entender as funções do usuário {#user-roles}

Muitos recursos no Cloud Manager exigem permissões específicas para operar.

O Cloud Manager atualmente define quatro funções para usuários que controlam a disponibilidade de recursos específicos:

* Proprietário da empresa
* Gerenciador de implantação
* Gerenciador de programas
* Desenvolvedor

>[!NOTE]
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

## Adicionar usuários {#add-users}

>[!NOTE]
>Você deve ser um Administrador do sistema para adicionar um usuário.

1. Se você for o Administrador do sistema, navegue até [Admin Console](https://adminconsole.adobe.com). Como alternativa, você também pode navegar até o Cloud Manager, onde verá o botão **Gerenciar acesso**, conforme descrito abaixo.

1. Clique no botão **Gerenciar acesso**, localizado na parte superior direita da página de aterrissagem do Cloud Manager, para abrir o Admin Console em uma nova guia.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

   No **Admin Console**, é possível adicionar usuários ao Cloud Manager e atribuí-los a Funções, chamadas de Perfis de produto no Admin Console.

1. Selecione **Adobe Experience Manager como Cloud Service** no cartão **Produtos e serviços** como mostrado abaixo.

   ![](/help/onboarding/what-is-required/assets/admin-console-1.png)

1. Selecione a guia **Users** na barra de ações e selecione **Adicionar usuário**.

   ![](/help/onboarding/what-is-required/assets/admin-console-2.png)

1. Selecione o usuário e atribua as funções apropriadas do Cloud Manager ou Perfis de produto ao usuário, conforme mostrado abaixo.

   ![](/help/onboarding/what-is-required/assets/admin-console-3.png)

   >[!NOTE]
   >Consulte as seções anteriores, [Funções e permissões do usuário](#user-roles) e [Permissões associadas a Definições de função](#permissions) para garantir que os usuários certos recebam a(s) Função(ões) correta(s) no **Admin Console**.

   Agora, você adicionou usuários ao Contexto de Produto do Adobe Experience Manager as a Cloud Service e está configurado com as Funções ou Perfis de Produto certos.

   Por exemplo, se você estiver na função de um:

   * ***Proprietário comercial***, você tem a permissão para Adicionar um novo programa ou Editar um programa, adicionar ou atualizar um ambiente, adicionar/editar/excluir o pipeline e executar qualquer pipeline, e implantar o código AEM ambiente ou qualidade de código.

   * ***Gerenciador de implantação***, você tem permissão para adicionar ou atualizar um ambiente, executar qualquer pipeline e implantar código em AEM ambiente ou qualidade de código.

   * ***Desenvolvedor***, você tem a permissão para gerar o Token de acesso pessoal para acessar o Git.

      >[!NOTE]
      > Um usuário pode ser atribuído a várias funções. Por exemplo, atribuir funções de Proprietário comercial e Gerente de implantação a um usuário fornece a combinação ou a soma dessas permissões.
