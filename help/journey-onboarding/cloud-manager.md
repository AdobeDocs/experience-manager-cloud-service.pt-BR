---
title: Acessar o Cloud Manager
description: Saiba como acessar o Cloud Manager para poder configurar os recursos do projeto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 225b34f081a942d67dfc1f6faeb09763ea9fde03
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 100%

---

# Acessar o Cloud Manager {#cloud-resources}

Nesta parte da [jornada de integração,](overview.md) você aprenderá a acessar o Cloud Manager para poder configurar os recursos do projeto.

## Objetivo {#objective}

No artigo anterior desta jornada de integração, [Atribuição dos membros da equipe aos perfis de produto do Cloud Manager,](assign-profiles-cloud-manager.md) você concedeu as funções apropriadas à sua equipe do AEMaaCS. Agora saiba como acessar o Cloud Manager para poder configurar os recursos do projeto que a equipe usará.

Como você concluiu a etapa anterior desta jornada, sua equipe pode acessar o Cloud Manager. O Cloud Manager é usado para criar e gerenciar os recursos do projeto, como programas e ambientes.

Depois de ler este documento, você deverá entender:

* Que um administrador do sistema atribuído à função **Proprietário da empresa** deve ser o primeiro em sua organização a fazer logon e acessar o Cloud Manager.
* Como fazer logon no Cloud Manager.

## Cloud Manager {#cloud-manager}

O Cloud Manager é um componente essencial do AEM as a Cloud Service e serve como ponto de entrada único para a equipe. Ele apoia os clientes com configurações de desenvolvimento corporativo e pipelines de CI/CD criados com propósitos específicos, que estão equipados de forma a garantir testes completos e código da mais alta qualidade para fornecer experiências excepcionais. O Cloud Manager fornece tudo o que é necessário para começar a usar os recursos e ambientes de autoatendimento, incluindo a capacidade de criar recursos e ambientes de nuvem.

Normalmente, um membro da equipe com o perfil de produto **Proprietário da empresa** é responsável por adicionar os recursos de nuvem, como programas e ambientes. Esse indivíduo entende as necessidades comerciais e conclui a configuração inicial do Cloud Manager.

Para os fins desta jornada de integração, você, como administrador do sistema, já atribuiu a si mesmo o perfil de produto **Proprietário da empresa** e configurará os recursos de nuvem. Dependendo dos requisitos reais do projeto, os proprietários da empresa podem ou não ser os mesmos indivíduos que os administradores do sistema.

## Acessar o Cloud Manager como um Administrador do sistema e Proprietário da empresa {#access-sysadmin-bo}

Para que os membros da equipe com função **Proprietário da empresa** possam acessar o Cloud Manager e começar a criar recursos de nuvem, o Administrador do sistema deve receber a função **Proprietário da empresa** e fazer logon no Cloud Manager como descrito na etapa anterior desta jornada de integração.

1. Certifique-se de que você, como administrador do sistema, receba a função **Proprietário da empresa**.

   * Retorne à etapa anterior desta jornada, [Atribuir membros da equipe aos perfis de produto do Cloud Manager,](assign-profiles-cloud-manager.md) para obter mais informações sobre como atribuir a função **Proprietário da empresa** ao administrador do sistema, se você ainda não tiver feito isso.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) para abrir a página de aterrissagem normal.

Ao fazer logon como administrador do sistema com a função **Proprietário da empresa**, você inicializa o Cloud Manager para uso pelos outros usuários com a função **Proprietário da empresa**. Você não receberá uma confirmação ou qualquer mensagem do tipo. Basta fazer logon.

Até você entrar no Cloud Manager como administrador do sistema com a função **Proprietário da empresa**, outros usuários com a função **Proprietário da empresa** não poderão criar programas no Cloud Manager, mesmo que as funções corretas sejam atribuídas a eles.

## Acessar o Cloud Manager {#navigate-cloud-manager}

Usuários com a função **Proprietário da empresa** receberão um email de boas-vindas com um link para começar. Siga as etapas abaixo para acessar o Cloud Manager usando esse email de boas-vindas.

1. No email de boas-vindas, clique em **Começar**, conforme mostrado na figura abaixo.
   ![Exemplo de email](/help/journey-onboarding/assets/get-started-email.png)

1. Você navegará para a página **Programas e produtos**.

   >[!TIP]
   >
   >Você também pode navegar diretamente para a página de logon do Cloud Manager em `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Adicione esta página aos favoritas para referência futura.

1. Você será direcionado para a página de aterrissagem do Cloud Manager.

Como alternativa, você também pode navegar para a página **Programas e produtos** a partir da página inicial da Adobe Experience Cloud seguindo estas etapas:

1. Navegue diretamente para a [Adobe Experience Cloud](https://experience.adobe.com) e faça logon usando sua Adobe ID.

1. Na página inicial da Adobe Experience Cloud, selecione **Experience Manager**.

   ![Página inicial da Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. Você será direcionado para a página inicial do AEM. Aqui, clique em **Iniciar** no bloco do **Cloud Manager**.

   ![Página inicial do AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Depois de fazer logon, você será direcionado para a página inicial do Cloud Manager. Consulte [Visualização dos programas do Cloud Manager](#viewing-programs) para obter mais detalhes.

A maneira como você acessa seus programas e produtos por meio do Cloud Manager é da sua responsabilidade e não afeta a forma como você usa o Cloud Manager ou como gerencia seus programas.

>[!NOTE]
>
>Dependendo das funções atribuídas no Cloud Manager e do estado do aplicativo, você verá telas diferentes ao usar a interface do usuário do Cloud Manager.

## Exibição dos programas {#viewing-programs}

Ao acessar o Cloud Manager, o conteúdo exibido dependerá do estado dos seus programas, conforme detalhado nas seções a seguir.

### Quando não existem programas {#no-programs}

Se não existirem programas em sua organização, a página de aterrissagem o direcionará para criar seu primeiro programa.

![Nenhum programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### Quando já existem programas {#programs-exist}

Se programas já existirem em sua organização, a página de aterrissagem exibirá os programas existentes e também oferecerá um botão para adicionar mais programas.

![Existem programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### Quando existe um programa e você é um administrador do sistema {#programs-exist-sysadmin}

Se já existirem programas em sua organização e você for um administrador do sistema, a página de aterrissagem exibirá o botão **Gerenciar acesso** junto com a opção **Adicionar programa**.

![Exibição do administrador do sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verificação das suas funções de usuário {#verify-user-roles}

Depois de fazer logon no Cloud Manager, você poderá verificar se recebeu o perfil de produto **Proprietário da empresa**.

1. Selecione o perfil na parte superior direita da janela.

   ![Perfil de usuário](/help/journey-onboarding/assets/setup-resources5.png)

1. Selecione **Funções do usuário** para exibir as funções atribuídas ao seu usuário.

   ![Funções do usuário](/help/journey-onboarding/assets/setup-resources6.png)

1. A caixa de diálogo deve confirmar que o usuário tem a função **Proprietário da empresa**.

   ![Lista de funções de usuário](/help/journey-onboarding/assets/setup-resources7.png)

Você fez logon no Cloud Manager como Proprietário da empresa! Se você não recebeu a função **Proprietário da empresa**, entre em contato com o administrador do sistema.

## O que vem a seguir {#whats-next}

Agora que você pode acessar o Cloud Manager como administrador do sistema, você está pronto para criar seu primeiro programa.

Você deve continuar sua jornada de integração revisando em seguida o documento [Criar um programa](create-program.md), no qual você aprenderá a fazer isso.

## Recursos adicionais {#additional-resources}

Acesse os recursos adicionais para saber mais sobre:

* [Introdução ao Cloud Manager](/help/onboarding/cloud-manager-introduction.md) -
Saiba mais sobre o Cloud Manager e seus programas e ambientes.
* [Perfis de produto e de equipe do AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) - Saiba como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às soluções licenciadas da Adobe.
