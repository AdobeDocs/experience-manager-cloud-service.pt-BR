---
title: Como fornecer acesso ao editor de regras dos formulários adaptáveis do aem para grupos de usuários selecionados?
description: Há diferentes tipos de usuários com habilidades variadas que trabalham com o Adaptive Forms. Saiba como limitar o acesso do editor de regras aos usuários com base em sua função.
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
hide: true
hidefromtoc: true
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---


# Conceder acesso ao editor de regras para grupos de usuários selecionados {#grant-rule-editor-access-to-select-user-groups}

## Visão geral {#overview}

Há diferentes tipos de usuários com habilidades variadas que trabalham com o Adaptive Forms. Embora os usuários especialistas possam ter o conhecimento certo para trabalhar com scripts e regras complexas, pode haver usuários de nível básico que precisam trabalhar somente com o layout e as propriedades básicas do Adaptive Forms.

[!DNL Experience Manager Forms] permite limitar o acesso do editor de regras aos usuários com base em sua função. Nas definições do Serviço de Configuração do Forms Adaptive, você pode especificar os [grupos de usuários](forms-groups-privileges-tasks.md) que podem exibir e acessar o editor de regras.

## Especificar grupos de usuários que podem acessar o editor de regras {#specify-user-groups-that-can-access-rule-editor}

1. Faça logon em [!DNL Experience Manager Forms] como administrador.
1. Na instância do autor, clique em ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Ferramentas ![martelo](assets/hammer-icon.svg) > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**. O Console da Web é aberto em uma nova janela.

   ![1-2](assets/1-2.png)

1. Na Janela [!UICONTROL Console da Web], localize e clique em **[!UICONTROL Serviço de Configuração de Formulário Adaptável]**. A caixa de diálogo **[!UICONTROL Serviço de Configuração de Formulário Adaptável]** é exibida. Não altere nenhum valor e clique em **[!UICONTROL Salvar]**.

   Ele cria um arquivo `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` no repositório do CRX.

1. Faça logon no CRXDE como administrador. Abra o arquivo `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` para edição.
1. Use a propriedade a seguir para especificar o nome de um grupo que possa acessar o editor de regras (por exemplo, RuleEditorsUserGroup) e clique em **[!UICONTROL Salvar Tudo]**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Para habilitar o acesso para vários grupos, especifique uma lista de valores separados por vírgula:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Criar Usuário](assets/create_user_new.png)

   Agora, quando um usuário que não faz parte do grupo de usuários especificado (aqui    `RuleEditorsUserGroup`) toque em um campo, o ícone Editar regra ( ![edit-rules1](assets/edit-rules1.png)) não está disponível na barra de ferramentas Componentes:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra de ferramentas Componentes visível para um usuário com acesso ao editor de regras:

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra de ferramentas Componentes conforme visível para um usuário sem acesso ao editor de regras

   Para obter instruções sobre como adicionar usuários a grupos, consulte [Administração e Segurança do Usuário](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=pt-BR).

