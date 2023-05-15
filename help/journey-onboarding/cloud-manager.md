---
title: Acessar o Cloud Manager
description: Saiba como acessar o Cloud Manager para poder configurar os recursos do projeto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
source-git-commit: 5c9dbaa25f0142afdae8b09dc18d1e1aaaf4c1fb
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 52%

---

# Acessar o Cloud Manager {#cloud-resources}

Nesta parte do [jornada de integração,](overview.md) saiba como acessar o Cloud Manager para poder configurar os recursos do projeto.

## Objetivo {#objective}

No artigo anterior desta jornada de integração, [Atribuição dos membros da equipe aos perfis de produto do Cloud Manager,](assign-profiles-cloud-manager.md) você concedeu as funções apropriadas à sua equipe do AEMaaCS. Agora saiba como acessar o Cloud Manager para poder configurar os recursos do projeto que sua equipe usa.

Como você concluiu a etapa anterior desta jornada, sua equipe pode acessar o Cloud Manager. O Cloud Manager é usado para criar e gerenciar os recursos do projeto, como programas e ambientes.

Após ler este documento, você deve entender o seguinte:

* Que um administrador de sistema atribuído ao **Proprietário da empresa** deve ser a primeira função em sua organização a fazer logon e acessar o Cloud Manager.
* Como fazer logon no Cloud Manager.

## Cloud Manager {#cloud-manager}

O Cloud Manager é um componente essencial do AEM as a Cloud Service e serve como ponto de entrada único para a equipe. Ele apoia os clientes com configurações de desenvolvimento corporativo e pipelines de CI/CD criados com propósitos específicos, que estão equipados de forma a garantir testes completos e código da mais alta qualidade para fornecer experiências excepcionais. O Cloud Manager fornece tudo o que é necessário para começar a usar os recursos e ambientes de autoatendimento, incluindo a capacidade de criar recursos e ambientes de nuvem.

Normalmente, um membro da equipe com o perfil de produto **Proprietário da empresa** é responsável por adicionar os recursos de nuvem, como programas e ambientes. Esse indivíduo entende as necessidades comerciais e conclui a configuração inicial do Cloud Manager.

Para os fins desta jornada de integração, você, como administrador do sistema, já se atribuiu ao **Proprietário da empresa** perfil do produto e pode configurar os recursos da nuvem. Dependendo dos requisitos reais do projeto, os proprietários de negócios podem ou não ser iguais ao administrador do sistema.

## Acessar o Cloud Manager como um Administrador do sistema e Proprietário da empresa {#access-sysadmin-bo}

Antes dos membros da equipe que você atribuiu à **Proprietário da empresa** pode acessar o cloud manager e começar a criar recursos na nuvem, o administrador do sistema deve receber a função **Proprietário da empresa** função. Eles também devem fazer logon no Cloud Manager como você fez na etapa anterior desta jornada de integração.

1. Certifique-se de que você, como administrador do sistema, receba a função **Proprietário da empresa**.

   * Retorne à etapa anterior desta jornada, [Atribuir membros da equipe aos perfis de produto do Cloud Manager,](assign-profiles-cloud-manager.md) para obter mais informações sobre como atribuir a variável **Proprietário da empresa** para o administrador do sistema.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) para abrir a página de aterrissagem normal.

Ao fazer logon como administrador do sistema com a função **Proprietário da empresa**, você inicializa o Cloud Manager para uso pelos outros usuários com a função **Proprietário da empresa**. Você não recebe uma confirmação ou nenhuma mensagem. Basta fazer logon.

Até você entrar no Cloud Manager como administrador do sistema com a **Proprietário da empresa** , outros usuários com a função **Proprietário da empresa** não pode criar programas no Cloud Manager. Essa regra é verdadeira mesmo se as funções corretas forem atribuídas a elas.

## Acessar o Cloud Manager {#navigate-cloud-manager}

Usuários com a **Proprietário da empresa** recebem um email de boas-vindas com um link para começar. Siga as etapas abaixo para acessar o Cloud Manager usando esse email de boas-vindas.

1. No email de boas-vindas, clique em **Introdução**, conforme mostrado na figura abaixo.
   ![Exemplo de email](/help/journey-onboarding/assets/get-started-email.png)

1. Navegue até o **Programas e produtos** página.

   >[!TIP]
   >
   >Você também pode navegar diretamente para a página de logon do Cloud Manager em `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Marque esta página como favorito para referência futura.

1. Você é direcionado para a página de aterrissagem do Cloud Manager.

Como alternativa, você também pode navegar para a página **Programas e produtos** a partir da página inicial da Adobe Experience Cloud seguindo estas etapas:

1. Navegue diretamente para a [Adobe Experience Cloud](https://experience.adobe.com) e faça logon usando sua Adobe ID.

1. Na página inicial do Adobe Experience Cloud, selecione **Experience Manager** para abrir a página inicial AEM.

   ![Página inicial da Experience Cloud](/help/journey-onboarding/assets/setup-resources2.png)

1. No **Cloud Manager** bloco, selecione **Launch**.

   ![Página inicial do AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Depois de fazer logon com êxito, você é direcionado para a página de aterrissagem do Cloud Manager. Consulte [Visualização dos programas do Cloud Manager](#viewing-programs) para obter mais detalhes.

A maneira como você acessa seus programas e produtos por meio do Cloud Manager é da sua responsabilidade e não afeta a forma como você usa o Cloud Manager ou como gerencia seus programas.

>[!NOTE]
>
>Dependendo das funções atribuídas no Cloud Manager e do estado do aplicativo, você verá telas diferentes ao usar a interface do usuário do Cloud Manager.

## Exibição dos programas {#viewing-programs}

Depois de acessar o Cloud Manager com êxito, o que você vê depende do estado dos programas, conforme detalhado nas seções a seguir.

### Quando não existem programas {#no-programs}

Se não existirem programas em sua organização, a página de aterrissagem o direcionará para criar seu primeiro programa.

![Nenhum programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

### Quando já existem programas {#programs-exist}

Se houver programas em sua organização, a landing page exibirá seus programas existentes e também oferecerá um botão para adicionar outros programas.

![Existem programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

### Quando existe um programa e você é um administrador do sistema {#programs-exist-sysadmin}

Se houver programas em sua organização e você for um administrador do sistema, sua landing page será exibida **Gerenciar acesso** botão junto com **Adicionar programa** opção.

![Exibição do administrador do sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

## Verificação das suas funções de usuário {#verify-user-roles}

Depois de fazer logon no Cloud Manager, você poderá verificar se recebeu o perfil de produto **Proprietário da empresa**.

1. Selecione o perfil na parte superior direita da janela.

   ![Perfil de usuário](/help/journey-onboarding/assets/setup-resources5.png)

1. Para exibir as funções atribuídas ao usuário, selecione **Funções do usuário**.

   ![Funções do usuário](/help/journey-onboarding/assets/setup-resources6.png)

1. A caixa de diálogo deve confirmar que o usuário tem a função **Proprietário da empresa**.

   ![Lista de funções de usuário](/help/journey-onboarding/assets/setup-resources7.png)

Você fez logon no Cloud Manager como Proprietário da empresa! Se você não recebeu a função **Proprietário da empresa**, entre em contato com o administrador do sistema.

## O que vem a seguir {#whats-next}

Agora que você pode acessar o Cloud Manager como administrador do sistema, você está pronto para criar seu primeiro programa.

Continue sua jornada de integração ao revisar o documento [Criar um programa](create-program.md) onde você aprende a fazê-lo.

## Recursos adicionais {#additional-resources}

Veja a seguir recursos adicionais e opcionais, caso deseje ir além do conteúdo da jornada de integração.

* [Introdução ao Cloud Manager](/help/onboarding/cloud-manager-introduction.md) -
Saiba mais sobre o Cloud Manager e seus programas e ambientes.
* [Perfis de produto e de equipe do AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) - Saiba como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às soluções licenciadas da Adobe.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
