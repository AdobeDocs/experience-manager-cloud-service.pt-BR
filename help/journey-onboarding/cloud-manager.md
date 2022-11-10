---
title: Acessar o Cloud Manager
description: Saiba como acessar o Cloud Manager para poder configurar os recursos do projeto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 69ac8e444a0f22649b48ec25b549ad60858f8b1b
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# Acessar o Cloud Manager {#cloud-resources}

Nesta parte do [jornada de integração,](overview.md) você aprenderá a acessar o Cloud Manager para poder configurar os recursos do projeto.

## Objetivo {#objective}

No artigo anterior desta jornada de integração, [Atribuir membros da equipe aos perfis de produto do Cloud Manager,](assign-profiles-cloud-manager.md) você concedeu as funções apropriadas à sua equipe do AEMaaCS. Agora saiba como acessar o Cloud Manager para poder configurar os recursos do projeto que a equipe usará.

Como você concluiu a etapa anterior nesta jornada, sua equipe pode acessar o Cloud Manager. O Cloud Manager é usado para criar e gerenciar os recursos do projeto, como programas e ambientes.

Depois de ler este documento, você deve entender:

* Que um administrador de sistema atribuído ao **Proprietário da empresa** deve ser a primeira função em sua organização a fazer logon e acessar o Cloud Manager.
* Como fazer logon no Cloud Manager.

## Cloud Manager {#cloud-manager}

O Cloud Manager é um componente essencial AEM as a Cloud Service e serve como ponto de entrada único para sua equipe. Ele oferece suporte a clientes com configurações de desenvolvimento corporativo com seus pipelines de CI/CD criados especificamente, que são equipados para garantir testes completos e a mais alta qualidade do código para fornecer experiências excepcionais. O Cloud Manager fornece tudo o que é necessário para começar a usar os recursos e ambientes de autoatendimento, incluindo a capacidade de criar recursos e ambientes de nuvem.

Normalmente, um membro da equipe é atribuído à **Proprietário da empresa** o perfil do produto é responsável pela adição dos recursos da nuvem, como programas e ambientes. Esse indivíduo entende as necessidades comerciais e quem conclui a configuração inicial do Cloud Manager.

Para os fins desta jornada de integração, você, como administrador do sistema, já se atribuiu ao **Proprietário da empresa** e configurará os recursos da nuvem. Dependendo dos requisitos reais do projeto, os proprietários de negócios podem ou não ser iguais ao administrador do sistema.

## Acesse o Cloud Manager como Administrador do sistema e Proprietário comercial {#access-sysadmin-bo}

Antes dos membros da equipe que você atribuiu à **Proprietário da empresa** pode acessar o cloud manager e começar a criar recursos na nuvem, o administrador do sistema deve receber a função **Proprietário da empresa** e faça logon no Cloud Manager como fez na etapa anterior desta jornada de integração.

1. Certifique-se de que você, como administrador do sistema, tenha a variável **Proprietário da empresa** função atribuída.

   * Retorne à etapa anterior desta jornada, [Atribuir membros da equipe aos perfis de produto do Cloud Manager,](assign-profiles-cloud-manager.md) para obter mais informações sobre como atribuir a variável **Proprietário da empresa** para o administrador do sistema, se você ainda não tiver feito isso.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e ser apresentada com a página de aterrissagem normal.

Ao fazer logon como administrador do sistema com o **Proprietário da empresa** , você inicializa o Cloud Manager para uso pelos outros usuários com a função **Proprietário da empresa** função. Você não receberá uma confirmação desta ou de qualquer mensagem. Basta fazer logon.

Até você entrar no Cloud Manager como administrador do sistema com a **Proprietário da empresa** , outros usuários com a função **Proprietário da empresa** A função não poderá criar programas no Cloud Manager mesmo se as funções corretas forem atribuídas a eles.

## Navegar para o Cloud Manager {#navigate-cloud-manager}

Usuários com a **Proprietário da empresa** A função receberá um email de boas-vindas com um link para começar. Siga as etapas abaixo para navegar até o Cloud Manager usando esse email de boas-vindas.

1. Em seu email de boas-vindas, clique em **Introdução**, conforme mostrado na figura abaixo.
   ![Exemplo de email](/help/journey-onboarding/assets/get-started-email.png)

1. Você navegará até o **Programas e produtos** página.

   >[!TIP]
   >
   >Você também pode navegar diretamente para a página de logon do Cloud Manager a partir de `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Marque esta página para referência futura.

1. Você será direcionado para a página de aterrissagem do Cloud Manager.

Como alternativa, você também pode navegar para o **Programas e produtos** da página inicial do Adobe Experience Cloud seguindo essas etapas

1. Navegue diretamente para [Adobe Experience Cloud](https://experience.adobe.com) e faça logon usando sua Adobe ID.

1. Na página inicial do Adobe Experience Cloud, selecione **Experience Manager**.

   ![Experience Cloud homepage](/help/journey-onboarding/assets/setup-resources2.png)

1. Isso o levará à página inicial da AEM. Aqui, clique em **Launch** no **Cloud Manager** mosaico.

   ![Página inicial do AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Após o logon bem-sucedido, você será direcionado para a página inicial do Cloud Manager. Consulte [Visualização dos programas do Cloud Manager](#viewing-programs) para obter mais detalhes.

A maneira como você acessa seus programas e produtos por meio do Cloud Manager é da sua responsabilidade e não afeta a forma como você usa o Cloud Manager ou como gerencia seus programas.

>[!NOTE]
>
>Dependendo das funções atribuídas no Cloud Manager e do estado do aplicativo, você verá telas diferentes ao usar a interface do usuário do Cloud Manager.

## Exibindo programas {#viewing-programs}

Depois de acessar o Cloud Manager com êxito, o que você vê dependerá do estado dos programas, conforme detalhado nas seções a seguir.

### Quando Não Existem Programas {#no-programs}

Se não houver programas em sua organização, a landing page o direcionará para criar seu primeiro programa.

![Nenhum programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### Quando já existem programas {#programs-exist}

Se programas já existirem em sua organização, sua landing page exibirá seus programas existentes e também oferecerá um botão para adicionar outros programas.

![Existem programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### Quando um programa existe e você é um administrador do sistema {#programs-exist-sysadmin}

Se já houver programas em sua organização e você for um administrador do sistema, sua landing page será exibida **Gerenciar acesso** botão junto com **Adicionar programa** opção.

![Exibição do administrador do sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verificando suas funções de usuário {#verify-user-roles}

Depois de fazer logon no Cloud Manager com êxito, você pode verificar se recebeu a variável **Proprietário da empresa** perfil do produto.

1. Selecione o perfil na parte superior direita da janela.

   ![Perfil de usuário](/help/journey-onboarding/assets/setup-resources5.png)

1. Selecionar **Funções do usuário** para exibir as funções atribuídas ao usuário.

   ![Funções do usuário](/help/journey-onboarding/assets/setup-resources6.png)

1. A caixa de diálogo deve confirmar que o usuário tem a variável **Proprietário da empresa** função.

   ![Lista de funções de usuário](/help/journey-onboarding/assets/setup-resources7.png)

Você fez logon no Cloud Manager as a Business Owner! Se você não receber a atribuição de **Proprietário da empresa** , entre em contato com o administrador do sistema.

## O que vem a seguir {#whats-next}

Agora que você pode acessar o Cloud Manager como administrador do sistema, você está pronto para criar seu primeiro programa.

Você deve continuar sua jornada de integração ao revisar o documento [Criar um programa](create-program.md) onde você aprenderá a fazê-lo.

## Recursos adicionais {#additional-resources}

Siga os recursos adicionais para saber mais sobre:

* [Introdução ao Cloud Manager](/help/onboarding/cloud-manager-introduction.md) - Saiba mais sobre o Cloud Manager, programas e ambientes do Cloud Manager.
* [AEM equipe as a Cloud Service e perfis de produto](/help/onboarding/aem-cs-team-product-profiles.md) - Saiba como AEM equipe as a Cloud Service e os perfis de produto podem conceder e limitar o acesso às soluções de Adobe licenciadas.
