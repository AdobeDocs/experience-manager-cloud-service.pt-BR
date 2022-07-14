---
title: Tarefas do desenvolvedor e do gerenciador de implantação
description: Depois que o administrador do sistema configurar os recursos de nuvem necessários, saiba como desenvolvedores e gerentes de implantação podem acessar o git para desenvolver aplicativos e usar pipelines para implantá-los.
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 2%

---


# Tarefas do desenvolvedor e do gerenciador de implantação {#developer-deployment-manager}

Nesta parte opcional do [jornada de integração,](overview.md) você aprenderá como desenvolvedores e gerentes de implantação podem acessar o git para desenvolver aplicativos e usar pipelines para implantá-los.

## A história até agora {#story-so-far}

Você percorreu um longo caminho em sua jornada de integração! Parabéns. O administrador do sistema concluiu a jornada de integração configurando os recursos de nuvem necessários e concedendo acesso ao documento [Atribuindo Perfis de Produto AEM.](assign-profiles-aem.md)

Neste ponto, seus desenvolvedores e gerentes de implantação podem começar a criar seus próprios aplicativos enquanto seus usuários de AEM podem começar a criar conteúdo. Nesse sentido, a integração está completa e agora é hora de usar seu novo sistema AEM as a Cloud Service, que este documento ilustrará.

## Público {#audience}

Por conseguinte, o presente documento é redigido na perspectiva da **desenvolvedor** e **gerenciador de implantação**.

O administrador do sistema também pode executar essas mesmas tarefas, mas geralmente essas funções são mantidas por usuários diferentes.

## Objetivo {#objective}

Este documento é um complemento da jornada de integração para demonstrar as tarefas básicas de um desenvolvedor e gerenciador de implantação depois que o administrador do sistema integrar todos os usuários e criar os recursos de nuvem necessários.

Após ler este documento, você deve:

* Como desenvolvedor, entenda como acessar e gerenciar os repositórios git do Cloud Manager.
* Como gerente de implantação, você pode configurar pipelines e implantar seu código no Cloud Manager.

## Desenvolvedores e gerenciadores de implantação {#roles}

Depois que o administrador do sistema concluir as principais tarefas de integração da criação de usuários e da configuração de recursos na nuvem, os usuários geralmente mais ansiosos para acessar o sistema são os desenvolvedores e os gerentes de implantação. Isso ocorre porque eles são os usuários responsáveis pela criação de aplicativos personalizados além AEM as a Cloud Service.

* **Desenvolvedores** - Esses usuários acessam os repositórios git do Cloud Manager, onde gerenciarão o código de seus aplicativos personalizados AEM.
* **Gerentes de implantação** - Esses usuários usam o Cloud Manager para criar e executar pipelines que implantam o código dos repositórios git em seus ambientes AEM em execução.

Dependendo das suas necessidades organizacionais, os mesmos usuários podem ter ambas as funções.

## Pré-requisitos {#prerequisites}

Antes de começar as tarefas descritas neste documento como desenvolvedor ou gerente de implantação, verifique se o administrador do sistema concluiu todas as etapas desta jornada de integração. Isso significa que:

* O administrador do sistema atribuiu desenvolvedores e gerentes de implantação aos respectivos perfis de produto.
* Os desenvolvedores também devem ser atribuídos a **Usuários AEM** ou **Administradores de AEM** perfis de produto para também usar o AEM.
* Os recursos da nuvem foram configurados.

## Acesso ao git {#accessing-git}

Você pode acessar e gerenciar os repositórios git usando o gerenciamento de conta git de autoatendimento do Cloud Manager.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegar para **Pipelines** cartão de seu **Visão geral do programa** e localize a **Acessar informações do repositório** para acessar e gerenciar o repositório Git.

   ![Botão Acessar informações do repositório no cartão Ambientes](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Clique no botão **Exibir informações do acordo de recompra** para abrir uma caixa de diálogo para exibir:

   * O URL para o repositório Git do Cloud Manager.
   * O nome de usuário do git.
   * A senha git, cujo valor é mostrado quando a variável **Gerar senha** é clicado.

   ![Informações do repositório](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Usando essas credenciais, o usuário pode clonar uma cópia local do repositório e fazer alterações nesse repositório local, e quando pronto pode confirmar qualquer alteração de código no repositório de código remoto no Cloud Manager.

## Configuração de pipeline {#setup-pipeline}

Depois que os desenvolvedores adicionarem seu código personalizado aos repositórios git, o gerenciador de implantação poderá criar e executar pipelines para implantar esse código em seus ambientes AEM.

Siga estas etapas para criar seu primeiro pipeline de implantação de não produção.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Acesse o **Pipelines** na tela inicial do Cloud Manager. Clique em **+Adicionar** e selecione **Adicionar pipeline de não-produção**.

   ![Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. No **Configuração** da guia **Adicionar pipeline de não-produção** , selecione o tipo de pipeline de não produção com o qual você deseja adicionar. Para este exemplo, selecione **Pipeline de implantação**.

   ![Caixa de diálogo Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Forneça uma **Nome do pipeline de não produção** para identificar o pipeline junto com as seguintes informações adicionais.

1. Para o **Acionador da implantação** select **Manual** para que o pipeline só seja executado quando você o iniciar.

1. Clique em **Continuar**.

1. No **Código fonte** da guia **Adicionar pipeline de não-produção** , você deve selecionar o tipo de código que o pipeline deve processar. Para este exemplo, selecione **Código de pilha completo**.

1. No **Código fonte** , você deve definir as seguintes opções.

   * **Ambientes de implantação qualificados** - Você deve escolher qual ambiente o pipeline deve implantar.
   * **Repositório** - Essas opções definem a partir de qual Git repo o pipeline deve recuperar o código.
   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático desse campo encontrará as ramificações correspondentes para ajudá-lo a selecionar.

   ![pipeline de pilha completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Clique em **Salvar**.

Agora você criou seu primeiro pipeline! Os usuários com a função de gerente de implantação agora podem iniciar o pipeline da interface do usuário do Cloud Manager.

## Implantar {#deploy}

Agora que os desenvolvedores adicionaram seu código personalizado aos repositórios git e você criou um pipeline para implantar esse código, é hora de executar o pipeline para realmente mover esse código do git para seu ambiente.

![Cartão de pipeline no Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até o **Pipelines** do cartão **Visão geral do programa** clique no botão de reticências ao lado do pipeline criado na seção anterior e selecione **Executar** no menu .

1. A execução do pipeline começa e é indicada pela variável **Status** coluna.

Você pode ver os detalhes da execução clicando no botão de reticências novamente e selecionando **Exibir detalhes**.

Parabéns. Agora você implantou o código do repositório Git em um ambiente de não-produção!

## O que vem a seguir {#whats-next}

Agora que leu este documento, você deve:

* Como desenvolvedor, entenda como acessar e gerenciar os repositórios git do Cloud Manager.
* Como gerente de implantação, você pode configurar pipelines e implantar seu código no Cloud Manager.

Você chegou ao fim da execução como um desenvolvedor ou gerente de implantação com não apenas conhecimento em funcionamento do Cloud Manager, mas também ambientes de trabalho, repositórios e pipelines! Mas há mais a aprender sobre as poderosas ferramentas de CI/CD AEM as a Cloud Service. Confira o [Recursos adicionais](#additional-resources) para obter mais detalhes.

Se você estiver interessado em como os autores de conteúdo acessam e usam o AEM as a Cloud Service, continue até a parte final da jornada de integração, [AEM Tarefas do usuário.](aem-users.md)

>[!TIP]
>
>Agora que você está integrado, você pode [saiba como adicionar facilmente o complemento Demonstrações de referência de AEM](/help/journey-sites/demos-add-on/overview.md) para um ambiente de sandbox com configuração mínima de AEM e poder testar os recursos avançados de AEM com exemplos avançados com base nas práticas recomendadas.

## Recursos adicionais {#additional-resources}

* [Acessar repositórios](/help/implementing/cloud-manager/managing-code/accessing-repos.md) - Saiba como acessar e gerenciar o repositório Git usando o gerenciamento de conta Git de autoatendimento do Cloud Manager.
* [Uso do Git com o Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) - Saiba como usar os repositórios Git do Cloud Manager e como integrar seu próprio repositório Git gerenciado pelo cliente no local com o Cloud Manager.
* [Configuração do Ambiente de Desenvolvimento Local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=pt-BR) - Este tutorial aborda a configuração de um ambiente de desenvolvimento local para o Adobe Experience Manager (AEM) usando o SDK as a Cloud Service AEM.
* [Introdução ao AEM Sites - Tutorial do WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR) - Este tutorial em várias partes foi projetado para desenvolvedores novos no Adobe Experience Manager (AEM). Este tutorial aborda a implementação de um site de AEM para uma marca fictícia de estilo de vida na WKND. O tutorial aborda tópicos fundamentais como configuração de projeto, Componentes principais, Modelos editáveis, bibliotecas do lado do cliente e desenvolvimento de componentes com o Adobe Experience Manager Sites.
* [Introdução ao SPA no AEM usando o React](/help/implementing/developing/hybrid/getting-started-react.md) - Este artigo apresenta uma amostra de aplicativo SPA, explica como ele é montado e permite que você entre em funcionamento com sua própria SPA rapidamente usando a estrutura React.
* [Introdução ao SPA no AEM usando o Angular](/help/implementing/developing/hybrid/getting-started-angular.md) - Este artigo apresenta um exemplo de aplicativo SPA, explica como ele é montado e permite que você entre em funcionamento com seu próprio SPA rapidamente usando a estrutura do Angular.
* [Jornada de desenvolvedores headless](/help/journey-headless/developer/overview.md) - Inicie aqui um curso orientado para o desenvolvimento de aplicativos sem periféricos com AEM.
