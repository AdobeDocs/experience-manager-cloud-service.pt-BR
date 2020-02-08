---
title: Adicionar usuários e funções - O que é necessário
description: Adicionar usuários e funções - O que é necessário
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# Adicionar usuários e funções - O que é necessário {#add-users-roles}


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

## Usando o Admin Console para criar um perfil {#using-admin-console-to-create-a-profile}

As funções são gerenciadas para o [!UICONTROL Cloud Manager] no Adobe Admin Console. Associações de função específicas são fornecidas adicionando o usuário a um Perfil de produto do [!UICONTROL Cloud Manager] no Admin Console.

Você pode atribuir associações de função específicas adicionando o usuário a um Perfil [!UICONTROL de] produto do **Cloud Manager** no Adobe Admin Console, um local central para gerenciar seus direitos da Adobe em toda a organização. Para saber mais sobre o Adobe Admin Console, consulte a documentação do [Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html).

>[!NOTE]
>
>Para acessar o Admin Console e configurar sua equipe (usuários e funções), abra um navegador e visite [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise).

Para fornecer as permissões apropriadas com base em funções aos usuários do [!UICONTROL Cloud Manager] , um administrador na **organização** do cliente deve criar novos Perfis de produto no Contexto de produto dos Serviços [!UICONTROL gerenciados do] AEM.

Para fornecer as permissões com base em funções apropriadas aos usuários do [!UICONTROL Cloud Manager] , como administrador, você deve criar quatro novos Perfis de produto no Contexto de produto do [!UICONTROL AEM Managed Services] , correspondentes a cada uma das quatro funções do [!UICONTROL Cloud Manager] :

* Proprietário da empresa
* Gerenciador de implantação
* Desenvolvedor
* Gerente do programa

Você pode criar ou adicionar usuários/grupos a esses Perfis de produto com o [Admin Console](https://adminconsole.adobe.com/) para o [!UICONTROL Cloud Manager], como mostra a figura abaixo:

1. Faça logon no Admin Console e clique em **Novo perfil** para adicionar um novo perfil.

1. Preencha os campos para configurar uma nova função para o [!UICONTROL Cloud Manager].

   Insira Nome **do** perfil, Nome **de** exibição para criar um novo perfil. Além disso, você pode selecionar um Grupo **de** permissões para o perfil.

   Clique em **Concluído** para concluir a etapa de criação do perfil.

   >[!NOTE]
   >
   >Ao criar esses perfis de produto, o Nome **de** exibição deve ser o valor técnico definido pelo [!UICONTROL Cloud Manager] (consulte a tabela abaixo). O Nome **do** perfil pode ser qualquer coisa, embora, para evitar confusão, é recomendável usar os valores na coluna Nome *do perfil* recomendado abaixo. Para fazer isso, ao criar o Perfil do produto, desmarque a opção **Igual ao Nome** do perfil e especifique o valor correspondente ao Nome **de** exibição.

   | **Função** | **Nome de exibição (obrigatório)** | **Nome de perfil recomendado** |
   |---|---|---|
   | Proprietário da empresa | CM_BUSINESS_OWNER_ROLE_PROFILE | [!UICONTROL Gerenciador] da nuvem - Função do proprietário da empresa |
   | Gerenciador de implantação | CM_DEPLOYMENT_MANAGER_ROLE_PROFILE | [!UICONTROL Gerenciador] de nuvem - Função do Gerenciador de implantação |
   | Desenvolvedor | CM_DEVELOPER_ROLE_PROFILE | [!UICONTROL Gerenciador] de nuvem - Função de desenvolvedor |
   | Gerente do programa | CM_PROGRAM_MANAGER_ROLE_PROFILE | [!UICONTROL Gerenciador] da nuvem - Função do gerente do programa |

1. Depois de criar o perfil do produto, você pode adicionar usuários (ou grupos) aos Perfis do produto.


