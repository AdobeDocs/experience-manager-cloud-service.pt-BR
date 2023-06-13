---
title: Tarefas do desenvolvedor e do gerente de implantação
description: Depois que o administrador do sistema configurar os recursos de nuvem necessários, saiba como desenvolvedores e gerentes de implantação podem acessar o Git para desenvolver aplicativos e usar pipelines para implantá-los.
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 77ae5d79ecb8a11a230cee461f247ffe0e9891a5
workflow-type: ht
source-wordcount: '1419'
ht-degree: 100%

---


# Tarefas do desenvolvedor e do gerente de implantação {#developer-deployment-manager}

Nesta parte opcional do [jornada de integração,](overview.md) você aprenderá como desenvolvedores e gerentes de implantação podem acessar o Git para desenvolver aplicativos e usar pipelines para implantá-los.

## A história até agora {#story-so-far}

Você percorreu um longo caminho em sua jornada de integração! Parabéns! O administrador do sistema concluiu a jornada de integração configurando os recursos de nuvem necessários e concedendo acesso conforme o documento [Atribuição de perfis de produto do AEM.](assign-profiles-aem.md)

Neste ponto, os desenvolvedores e gerentes de implantação podem começar a criar seus próprios aplicativos enquanto os usuários do AEM podem começar a criar conteúdo. Nesse sentido, a integração está completa e agora é hora de usar o novo sistema do AEM as a Cloud Service ilustrado neste documento.

## Público {#audience}

Por conseguinte, este documento é escrito na perspectiva do **desenvolvedor** e do **gerente de implantação**.

O administrador do sistema também pode executar essas mesmas tarefas; porém, essas funções geralmente são mantidas por outros usuários.

## Objetivo {#objective}

Este documento é um complemento à jornada de integração para demonstrar as tarefas básicas de um desenvolvedor e de um gerente de implantação, uma vez que o administrador do sistema tenha integrado todos os usuários e criado os recursos de nuvem necessários.

Depois de ler este documento, você deverá:

* Como desenvolvedor, saber como acessar e gerenciar os repositórios Git do Cloud Manager.
* Como gerente de implantação, ser capaz de configurar pipelines e implantar código no Cloud Manager.

## Desenvolvedores e gerentes de implantação {#roles}

Depois que o administrador do sistema conclui as principais tarefas de integração, incluindo criar usuários e configurar recursos na nuvem, os usuários geralmente mais ansiosos para acessar o sistema são os desenvolvedores e os gerentes de implantação. Isso ocorre porque eles são os usuários responsáveis pela criação de aplicativos personalizados com base no AEM as a Cloud Service.

* **Desenvolvedores** - Esses usuários acessam os repositórios Git do Cloud Manager, onde gerenciam o código de seus aplicativos personalizados do AEM.
* **Gerentes de implantação** - Esses usuários usam o Cloud Manager para criar e executar pipelines que implantam o código dos repositórios Git em seus ambientes do AEM em execução.

Dependendo das suas necessidades organizacionais, os mesmos usuários podem ter ambas as funções.

## Pré-requisitos {#prerequisites}

Antes de começar as tarefas descritas neste documento como um desenvolvedor ou gerente de implantação, verifique se o administrador do sistema concluiu todas as etapas desta jornada de integração. Isso significa que:

* O administrador do sistema atribuiu desenvolvedores e gerentes de implantação aos respectivos perfis de produto.
* Os desenvolvedores também devem ser atribuídos aos perfis de produto **Usuários do AEM** ou **Administradores do AEM** para usarem o AEM.
* Os recursos de nuvem foram configurados.

## Acesso ao Git {#accessing-git}

Você pode acessar e gerenciar os repositórios Git usando o gerenciamento de conta Git por autoatendimento do Cloud Manager.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse o cartão **Pipelines** a partir da página **Visão geral do programa** e localize o botão **Acessar informações do repositório** para acessar e gerenciar o repositório Git.

   ![Botão Acessar informações do repositório no cartão Ambientes](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Clique no botão **Exibir informações do repositório** para abrir uma caixa de diálogo para exibir:

   * A URL do repositório Git do Cloud Manager.
   * O nome de usuário do Git.
   * A senha do Git, cujo valor é mostrado ao clicar no botão **Gerar senha**.

   ![Informações do repositório](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Usando essas credenciais, o usuário pode clonar uma cópia local do repositório e fazer alterações nele, e quando pronto, pode confirmar qualquer alteração no repositório de códigos remotos no Cloud Manager.

## Configuração de pipeline {#setup-pipeline}

Depois que os desenvolvedores adicionam seu código personalizado aos repositórios Git, o gerente de implantação pode criar e executar pipelines para implantar esse código em seus ambientes do AEM.

Siga estas etapas para criar seu primeiro pipeline de implantação de não produção.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse o cartão **Pipelines** na tela inicial do Cloud Manager. Clique em **+Adicionar** e selecione **Adicionar pipeline de não produção**.

   ![Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. Na guia **Configuração** da caixa de diálogo **Adicionar pipeline de não produção**, selecione o tipo de pipeline de não produção que você deseja adicionar. Para este exemplo, selecione **Pipeline de implantação**.

   ![Caixa de diálogo Adicionar pipeline de não produção](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. Forneça um **Nome do pipeline de não produção** para identificar o pipeline junto com as informações adicionais a seguir.

1. Para o **Acionador da implantação**, selecione **Manual**, para que o pipeline somente seja executado quando você o iniciar.

1. Clique em **Continuar**.

1. Na guia **Código fonte** da caixa de diálogo **Adicionar pipeline de não produção**, você deve selecionar o tipo de código que o pipeline deve processar. Para este exemplo, selecione **Código de pilha completa**.

1. Na guia **Código-fonte**, você deve definir as opções a seguir.

   * **Ambientes de implantação qualificados** - Você deve escolher qual ambiente o pipeline deve implantar.
   * **Repositório** - Essa opção define de qual repositório Git o pipeline deve recuperar o código.
   * **Ramificação Git** - Essa opção define de qual ramificação o pipeline selecionado deve recuperar o código.
      * Insira os primeiros caracteres do nome da ramificação e o recurso de preenchimento automático do campo localizará as ramificações correspondentes para ajudá-lo em sua seleção.

   ![Pipeline de pilha completa](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. Clique em **Salvar**.

Agora você criou seu primeiro pipeline! Os usuários com a função de gerente de implantação agora podem iniciar o pipeline da interface do usuário do Cloud Manager.

## Implantar {#deploy}

Agora que os desenvolvedores adicionaram seu código personalizado aos repositórios Git e você criou um pipeline para implantá-lo, é hora de executar o pipeline para realmente mover esse código do Git para o seu ambiente.

![Cartão Pipelines no Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa** e clique no botão de reticências ao lado do pipeline criado na seção anterior e selecione **Executar** no menu.

1. A execução do pipeline começa e é indicada pela coluna **Status**.

Você pode ver os detalhes da execução clicando no botão de reticências novamente e selecionando **Exibir detalhes**.

Parabéns! Agora você implantou o código do repositório Git em um ambiente de não produção!

## O que vem a seguir {#whats-next}

Agora que você leu este documento, deve:

* Como desenvolvedor, saber como acessar e gerenciar os repositórios Git do Cloud Manager.
* Como gerente de implantação, ser capaz de configurar pipelines e implantar código no Cloud Manager.

Você começou com o pé direito como desenvolvedor ou gerente de implantação, não apenas com conhecimento sobre o funcionamento do Cloud Manager, como também sobre ambientes de trabalho, repositórios e pipelines! Ainda há mais a aprender sobre as poderosas ferramentas de CI/CD do AEM as a Cloud Service. Confira a seção [Recursos adicionais](#additional-resources) para obter mais detalhes.

Se você estiver interessado em como os autores de conteúdo acessam e usam o AEM as a Cloud Service, continue até a parte final da jornada de integração, [Tarefas do usuário do AEM.](aem-users.md)

>[!TIP]
>
>Agora que você passou pela integração, saiba como [adicionar facilmente o complemento de demonstrações de referência do AEM](/help/journey-sites/demos-add-on/overview.md) a um ambiente de sandbox com configuração mínima do AEM e sobre poder testar os recursos avançados do AEM com exemplos completos com base nas práticas recomendadas.

## Recursos adicionais {#additional-resources}

A seguir estão recursos adicionais e opcionais se quiser ir além do conteúdo da jornada de integração.

* [Acessar repositórios](/help/implementing/cloud-manager/managing-code/accessing-repos.md) - Saiba como acessar e gerenciar o repositório Git usando o gerenciamento de conta Git por autoatendimento do Cloud Manager.
* [Uso do Git com o Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) - Saiba como usar os repositórios Git do Cloud Manager e como integrar seu próprio repositório Git local gerenciado pelo cliente com o Cloud Manager.
* [Configuração do ambiente de desenvolvimento local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=pt-BR) - Esse tutorial aborda a configuração de um ambiente de desenvolvimento local para o Adobe Experience Manager (AEM) usando o SDK do AEM as a Cloud Service.
* [Introdução ao AEM Sites - Tutorial WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR) - Esse tutorial dividido em várias partes foi projetado para desenvolvedores novos no Adobe Experience Manager (AEM). Esse tutorial aborda a implementação de um site do AEM para uma marca fictícia de estilo de vida, a WKND. O tutorial abrange tópicos fundamentais como configuração de projetos, componentes principais, modelos editáveis, bibliotecas do lado do cliente e desenvolvimento de componentes com o Adobe Experience Manager Sites.
* [Introdução a SPAs no AEM usando o React](/help/implementing/developing/hybrid/getting-started-react.md) - Esse artigo apresenta uma amostra de aplicativo SPA, explica como ele é montado e permite que você comece a usar seu próprio SPA rapidamente usando a estrutura do React.
* [Introdução a SPAs no AEM usando o Angular](/help/implementing/developing/hybrid/getting-started-angular.md) - Esse artigo apresenta uma amostra de aplicativo SPA, explica como ele é montado e permite que você comece a usar seu próprio SPA rapidamente usando a estrutura do Angular.
* [Jornada de desenvolvedores sem periféricos](/help/journey-headless/developer/overview.md) - Inicie aqui um curso orientado para o desenvolvimento de aplicativos sem periféricos com o AEM.
