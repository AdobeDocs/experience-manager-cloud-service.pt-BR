---
title: Como conceder acesso ao editor de regras para grupos de usuários selecionados?
description: Existem diferentes tipos de usuários com habilidades variadas que trabalham com o Adaptive Forms. Saiba como limitar o acesso do editor de regras aos usuários com base em sua função ou função.
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---


# Conceder acesso ao editor de regras para grupos de usuários selecionados {#grant-rule-editor-access-to-select-user-groups}

## Visão geral {#overview}

Existem diferentes tipos de usuários com habilidades variadas que trabalham com o Adaptive Forms. Embora os usuários especialistas tenham o conhecimento certo para trabalhar com scripts e regras complexas, pode haver usuários básicos que precisam trabalhar somente com o layout e as propriedades básicas do Adaptive Forms.

[!DNL Experience Manager Forms] permite limitar o acesso do editor de regras aos usuários com base em sua função ou função. Nas configurações do serviço de configuração adaptável Forms, você pode especificar a variável [grupos de usuários](forms-groups-privileges-tasks.md) que pode visualizar e acessar o editor de regras.

## Especificar grupos de usuários que podem acessar o editor de regras {#specify-user-groups-that-can-access-rule-editor}

1. Faça logon em [!DNL Experience Manager Forms] como administrador.
1. Na instância do autor, clique em ![Adobe Experience Manager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Ferramentas ![martelo](assets/hammer-icon.svg) > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**. O Console da Web é aberto em uma nova janela.

   ![1-2](assets/1-2.png)

1. Em [!UICONTROL Console da Web] Janela, localize e clique em **[!UICONTROL Serviço de configuração de formulário adaptável]**. **[!UICONTROL Serviço de configuração de formulário adaptável]** será exibida. Não altere nenhum valor e clique em **[!UICONTROL Salvar]**.

   Ele cria um arquivo `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` no repositório CRX.

1. Faça logon no CRXDE como administrador. Abrir arquivo `/apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config` para edição.
1. Use a seguinte propriedade para especificar o nome de um grupo que pode acessar o editor de regras (por exemplo, RuleEditorsUserGroup) e clique em **[!UICONTROL Salvar tudo]**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Para habilitar o acesso para vários grupos, especifique uma lista de valores separados por vírgula:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Criar usuário](assets/create_user_new.png)

   Agora, quando um usuário que não faz parte do grupo de usuários especificado (aqui    `RuleEditorsUserGroup`) toque em um campo, no ícone Editar regra ( ![edit-rules1](assets/edit-rules1.png)) não está disponível na barra de ferramentas Componentes:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra de ferramentas Componentes visível para um usuário com acesso ao editor de regras:

   ![componentstoolbarwithultre](assets/componentstoolbarwithoutre.png)

   Barra de ferramentas Componentes visível para um usuário sem acesso ao editor de regras

   Para obter instruções sobre como adicionar usuários a grupos, consulte [Administração e segurança do usuário](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).

