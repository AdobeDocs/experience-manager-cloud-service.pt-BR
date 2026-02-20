---
title: Adicionar repositórios externos no Cloud Manager
description: Saiba como adicionar um repositório externo no Cloud Manager. O Cloud Manager oferece suporte à integração com repositórios GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: 2ea076c42a6406548bf48cd246227fc8ddb3a080
workflow-type: tm+mt
source-wordcount: '2444'
ht-degree: 23%

---

# Adicionar repositórios externos no Cloud Manager {#external-repositories}

<!-- badge: label="Beta - Azure DevOps only" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket" -->

Saiba como adicionar um repositório externo no Cloud Manager. O Cloud Manager oferece suporte à integração com repositórios GitHub Enterprise, GitLab e Bitbucket.

Os clientes agora também podem integrar seus repositórios Git do Azure DevOps no Cloud Manager, com suporte para repositórios Azure DevOps modernos e VSTS herdados (Visual Studio Team Services).

* Para usuários do Edge Delivery Services, o repositório integrado pode ser usado para sincronizar e implantar o código do site.
* Para usuários do AEM as a Cloud Service e do Adobe Managed Services (AMS), o repositório pode ser vinculado a pipelines de pilha completa e de front-end.

## Configurar um repositório externo

A configuração de um repositório externo no Cloud Manager consiste nas seguintes etapas:

1. [Adicionar um repositório externo](#add-external-repo) a um programa selecionado
1. [Vincular um repositório externo validado a um pipeline](#validate-ext-repo)
   <!-- 1. Provide an access token to the external repository.
    1. Validate ownership of the private GitHub repository. -->
1. [Configure um webhook](#configure-webhook) para um repositório externo.


## Adicione um repositório externo {#add-ext-repo}

<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa ao qual deseja vincular um repositório externo.

1. No menu lateral, em **Programa**, clique em ![Ícone de estrutura de tópicos de pastas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Repositórios**.

   ![A página Repositórios](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Próximo ao canto superior direito da página **Repositórios**, clique em **Adicionar Repositório**.

1. Na caixa de diálogo **Adicionar repositório**, selecione **Repositório privado** para vincular um repositório Git externo ao seu programa.

   ![Adicionar repositório próprio](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. Em cada campo respectivo, forneça os seguintes detalhes sobre o repositório:

   | Texto | Descrição |
   | --- | --- |
   | **Nome do repositório** | Obrigatório. Um nome expressivo para o novo repositório. |
   | **URL do repositório** | Obrigatório. O URL do repositório.<br><br>Se você estiver usando um repositório hospedado pelo GitHub, o caminho deverá terminar em `.git`.<br>Por exemplo, *`https://github.com/org-name/repo-name.git`* (o caminho do URL é apenas para fins ilustrativos).<br><br>Se você estiver usando um repositório externo, ele deverá usar o seguinte formato de caminho de URL:<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> ou<br>`https://self-hosted-domain/org-name/repo-name.git`<br>e corresponder ao seu fornecedor de Git. |
   | **Selecionar tipo de repositório** | Obrigatório. Selecione o tipo de repositório que você está usando. Se o caminho do URL do repositório incluir o nome do fornecedor do Git, como GitLab ou Bitbucket, o tipo de repositório já estará pré-selecionado para você.:<ul><li>**GitHub** (GitHub Enterprise e a versão auto-hospedada do GitHub)</li><li>**GitLab** (o `gitlab.com` e a versão auto-hospedada do GitLab) </li><li>Há suporte para **Bitbucket** (somente `bitbucket.org` - versão em nuvem). A versão auto-hospedada do Bitbucket foi substituída a partir de 15 de fevereiro de 2024.</li><li>**DevOps do Azure** (`dev.azure.com`) </ul> |
   | **Descrição** | Opcional. Uma descrição detalhada do repositório. |

1. Clique em **Salvar** para adicionar o repositório.

   Agora, forneça um token de acesso para validar a propriedade do repositório externo.

1. Na caixa de diálogo **Validação de Propriedade de Repositório Privado**, forneça um token de acesso para validar a propriedade do repositório externo para que você possa acessá-lo e clique em **Validação**.

   ![Seleção de um token de acesso para um repositório](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *Selecionando um token de acesso existente para um repositório Bitbucket (somente para ilustração).*

>[!BEGINTABS]

>[!TAB GitHub Enterprise]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

| Opção de token de acesso | Descrição |
| --- | --- |
| **Usar token de acesso já existente** | Se você já forneceu um token de acesso ao repositório para sua organização e tem acesso a vários repositórios, você pode selecionar um token. Use a lista suspensa **Nome do token** para escolher o token que deseja aplicar ao repositório. Caso contrário, adicione um novo token de acesso. |
| **Adicionar novo token de acesso** | <ul><li> No campo de texto **Nome do token**, digite um nome para o token de acesso que você está criando.<li>Crie um token de acesso pessoal seguindo as instruções na [documentação do GitHub](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).<li>Permissões necessárias para o GitHub Enterprise Personal Access Token (PAT)<br>Essas permissões garantem que o Cloud Manager possa validar solicitações de pull, gerenciar verificações de status de confirmação e acessar detalhes do repositório necessários.<br>Ao gerar o PAT no GitHub Enterprise, verifique se ele inclui as seguintes permissões de repositório:<ul><li>Solicitação de pull (leitura e gravação)<li>Status de confirmação (leitura e gravação)<li>Metadados do repositório (somente leitura)</li></li></ul></li></ul></ul></ul><ul><li>No campo **Token de acesso**, cole o token que acabou de criar. |

Após a validação, o repositório externo estará pronto para ser usado e vinculado a um pipeline.

Consulte também [Gerenciar tokens de acesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

| Opção de token de acesso | Descrição |
| --- | --- |
| **Usar token de acesso já existente** | Se você já forneceu um token de acesso ao repositório para sua organização e tem acesso a vários repositórios, você pode selecionar um token. Use a lista suspensa **Nome do token** para escolher o token que deseja aplicar ao repositório. Caso contrário, adicione um novo token de acesso. |
| **Adicionar novo token de acesso** | <ul><li>No campo de texto **Nome do token**, digite um nome para o token de acesso que você está criando.<li>Crie um token de acesso pessoal seguindo a instrução na [documentação do GitLab](https://docs.gitlab.com/user/profile/personal_access_tokens/).<li>Permissões necessárias para o GitLab Personal Access Token (PAT)<br>Esses escopos permitem que o Cloud Manager acesse dados do repositório e informações do usuário, conforme necessário, para validação e integração com webhook.<br>Ao gerar o PAT no GitLab, certifique-se de que ele inclua os seguintes escopos de token:<ul><li>api<li>read_user</li></li></ul></li></li></ul></ul></ul><ul><li>No campo **Token de acesso**, cole o token que acabou de criar. |

Após a validação, o repositório externo estará pronto para ser usado e vinculado a um pipeline.

Consulte também [Gerenciar tokens de acesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

>[!TAB Bitbucket]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

| Opção de token de acesso | Descrição |
| --- | --- |
| **Usar token de acesso já existente** | Se você já forneceu um token de acesso ao repositório para sua organização e tem acesso a vários repositórios, você pode selecionar um token. Use a lista suspensa **Nome do token** para escolher o token que deseja aplicar ao repositório. Caso contrário, adicione um novo token de acesso. |
| **Adicionar novo token de acesso** | <ul><li>No campo de texto **Nome do token**, digite um nome para o token de acesso que você está criando.<li>Crie um token de acesso do repositório usando a [documentação do Bitbucket](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/).<li>Permissões necessárias para o PAT (token de acesso pessoal) do Bitbucket<br>Essas permissões permitem que o Cloud Manager acesse o conteúdo do repositório, gerencie solicitações de pull e configure ou reaja a eventos de webhook.<br>Ao criar a senha de aplicativo no Bitbucket, verifique se ela inclui as seguintes permissões de senha de aplicativo necessárias:<ul><li>Repositório (somente leitura)<li>Solicitações de pull (leitura e gravação)<li>Webhooks (leitura e gravação)</li></li></ul></li></li></ul></ul></ul><ul><li>No campo **Token de acesso**, cole o token que acabou de criar. |

Após a validação, o repositório externo estará pronto para ser usado e vinculado a um pipeline.

Consulte também [Gerenciar tokens de acesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

>[!TAB DevOps do Azure]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/azure_devops -->

| Opção de token de acesso | Descrição |
| --- | --- |
| **Usar token de acesso já existente** | Se você já forneceu um token de acesso ao repositório para sua organização e tem acesso a vários repositórios, você pode selecionar um token. Use a lista suspensa **Nome do token** para escolher o token que deseja aplicar ao repositório. Caso contrário, adicione um novo token de acesso. |
| **Adicionar novo token de acesso** | <ul><li>No campo de texto **Nome do token**, digite um nome para o token de acesso que você está criando.<li>Crie um token de acesso do repositório usando a [documentação do Azure DevOps](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows).<li>Permissões necessárias para o PAT (Personal Access Token) DevOps da Azure.<br>Essas permissões permitem que o Cloud Manager acesse o conteúdo do repositório, gerencie solicitações de pull e configure ou reaja a eventos de webhook.<br>Ao criar a senha de aplicativo no Azure DevOps, verifique se ela inclui as seguintes permissões de senha de aplicativo necessárias:<ul><li>Código (Leitura)</li><li>Código (Status)</li><li>Solicitação de pull Threads (leitura e gravação)</li></ul></li></li></ul></ul></ul><ul><li>No campo **Token de acesso**, cole o token que acabou de criar. |

Após a validação, o repositório externo estará pronto para ser usado e vinculado a um pipeline.

Consulte também [Gerenciar tokens de acesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

>[!ENDTABS]


## Vincular um repositório externo validado a um pipeline {#validate-ext-repo}

1. Adicionar ou editar um pipeline:
   * [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [Editar um pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

   <!-- Add an Edge Delivery Pipeline -->

   ![Repositório de código-fonte do pipeline e ramificação Git](/help/implementing/cloud-manager/managing-code/assets/pipeline-repo-gitbranch.png)
   *Caixa de diálogo Adicionar pipeline de não produção com o repositório selecionado e a ramificação Git,*

1. Ao adicionar ou editar um pipeline, para especificar o local do **Código-fonte** para seu pipeline novo ou já existente, escolha o repositório externo que deseja usar na lista suspensa **Repositório**.

1. Na lista suspensa **Ramificação Git**, selecione a ramificação como a origem do pipeline.

1. Clique em **Salvar**.


>[!TIP]
>
>Para obter detalhes sobre como gerenciar repositórios no Cloud Manager, consulte [Repositórios do Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).


## Configurar um webhook para um repositório externo {#configure-webhook}

O Cloud Manager permite configurar webhooks para repositórios Git externos adicionados. Consulte [Adicionar um repositório externo](#add-ext-repo). Esses webhooks permitem que o Cloud Manager receba eventos relacionados a diferentes ações na solução do fornecedor Git.

Por exemplo, webhooks permitem que o Cloud Manager acione ações com base em eventos como os seguintes:

* Criação de solicitação de pull (PR) - Inicia a funcionalidade de validação de PR.
* Eventos de push - Inicia pipelines quando o acionador &quot;Na confirmação do Git&quot; está ativado (ativado).
* Ações futuras baseadas em comentários - Permite fluxos de trabalho, como implantação direta de uma PR, em um RDE (Rapid Development Environment, ambiente de desenvolvimento rápido).

A configuração do Webhook não é necessária para repositórios hospedados em `GitHub.com` porque o Cloud Manager se integra diretamente por meio do aplicativo GitHub.

Para todos os outros repositórios externos integrados com um token de acesso, como GitHub Enterprise, GitLab, Bitbucket e Azure DevOps, a configuração de webhook está disponível e deve ser definida manualmente.

**Para configurar um webhook para um repositório externo:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa para o qual deseja configurar um webhook para um repositório Git externo.

1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo.

1. No menu à esquerda, no cabeçalho **Programa**, clique em ![Ícone de estrutura de tópicos de pastas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Repositórios**.

1. Na página **Repositórios**, usando a coluna **Tipo** para orientá-lo na sua seleção, localize o repositório desejado e clique em ![Reticências - Ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) ao lado dele.

   ![Opção de Webhook de configuração no menu suspenso para um repositório selecionado](/help/implementing/cloud-manager/managing-code/assets/repository-config-webhook.png)

1. No menu suspenso, clique em **Configurar Webhook**.

   ![Caixa de diálogo Configurar Webhook](/help/implementing/cloud-manager/managing-code/assets/config-webhook.png)

1. Na caixa de diálogo **Webhook de configuração**, faça o seguinte:

   1. Ao lado do campo **URL do Webhook**, clique em ![Ícone de cópia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg).
Cole o URL em um arquivo de texto sem formatação. A URL copiada é necessária para as configurações do Webhook do fornecedor do Git.
   1. Ao lado do campo de token/chave **Segredo do Webhook**, clique em **Gerar** e em ![Ícone Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg).
Cole o segredo em um arquivo de texto simples. O segredo copiado é necessário para as configurações de Webhook do fornecedor de Git.
1. Clique em **Fechar**.
1. Navegue até sua solução de fornecedor do Git (GitHub Enterprise, GitLab, Bitbucket ou Azure DevOps).

   Todos os detalhes sobre a configuração do webhook e os eventos necessários para cada fornecedor estão disponíveis em [Adicionar um repositório externo](#add-ext-repo). Na etapa 8, consulte a tabela com guias.

1. Localize a seção Configurações do **Webhook** da solução.
1. Cole o URL do Webhook copiado anteriormente no campo de texto do URL.
   1. Substitua o parâmetro de consulta `api_key` na URL do Webhook pela sua própria chave de API real.

      Para gerar uma chave de API, você deve criar um projeto de integração no Adobe Developer Console. Consulte [Criando um Projeto de Integração de API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) para obter detalhes completos.

1. Cole o Segredo do Webhook copiado anteriormente no campo de texto **Segredo** (ou **Chave secreta** ou **Token secreto**).
1. Configure o webhook para enviar os eventos exigidos pelo Cloud Manager. Use a tabela a seguir para determinar os eventos corretos para seu provedor Git.

>[!BEGINTABS]

>[!TAB GitHub Enterprise]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

| Eventos de webhook necessários |
| --- |
| Esses eventos permitem que o Cloud Manager responda à atividade do GitHub, como validação de solicitação de pull, acionadores baseados em push para pipelines ou sincronização de código do Edge Delivery Services.<br>Verifique se o webhook está configurado para disparar os seguintes eventos do webhook necessários:<ul><li>Solicitações de pull<li>Envios por push<li>Comentários do problema</li></li></li></ul></ul></ul> |

>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

| Eventos de webhook necessários |
| --- |
| Esses eventos de webhook permitem que o Cloud Manager acione pipelines quando o código é enviado por push ou uma solicitação de mesclagem é enviada. Eles também rastreiam comentários relacionados à validação da solicitação de pull (por meio de eventos de observação).<br>Verifique se o webhook está configurado para ser acionado nos seguintes eventos necessários do webhook<ul><li>Eventos de push<li>Mesclar eventos de solicitação<li>Anotar eventos</li></li></li></ul></ul></ul> |

>[!TAB Bitbucket]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

| Eventos de webhook necessários |
| --- |
| Esses eventos garantem que o Cloud Manager possa validar solicitações de pull, responder a envios por código e interagir com comentários para coordenação de pipeline.<br>Verifique se o webhook está configurado para ser acionado nos seguintes eventos necessários do webhook<ul><li>Solicitação de pull: criada<li>Solicitação de pull: atualizada<li>Solicitações de pull: mescladas<li>Solicitação de pull: comentário<li>Repositório: push</li></li></li></ul></ul></ul> |

>[!TAB DevOps do Azure]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/azure_devops -->

| Eventos e autenticação necessários do webhook |
| --- |
| Esses eventos garantem que o Cloud Manager possa validar solicitações de pull, responder a envios por código e interagir com comentários para coordenação de pipeline.<br>Verifique se o webhook está configurado para ser acionado nos seguintes eventos necessários do webhook<ul><li>Código enviado por push</li><li>Solicitação de pull comentada em</li><li>Solicitação de pull criada</li><li>Solicitação de pull atualizada</li></ul>Definir autenticação:<br>1. No campo **Nome de usuário de autenticação básica**, digite `cloudmanager`.<br>2. No campo **Senha de autenticação básica**, digite o Segredo do Webhook gerado pela interface do usuário do Cloud Manager. |

>[!ENDTABS]


### Validação de pull requests com webhooks

Depois que os webhooks forem configurados corretamente, o Cloud Manager acionará automaticamente as execuções de pipeline ou as verificações de validação de PR para o repositório.

O comportamento varia dependendo do provedor Git que você usa, conforme descrito abaixo.

>[!BEGINTABS]


>[!TAB GitHub Enterprise]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/github -->

Quando a verificação é criada, ela é exibida como a seguinte captura de tela abaixo. A principal diferença em relação a `GitHub.com` é que `GitHub.com` usa uma execução de verificação, enquanto o GitHub Enterprise (usando tokens de acesso pessoal) gera um status de confirmação:

![Confirmar status para indicar o processo de validação de PR no GitHub Enterprise](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)


>[!TAB GitLab]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/gitlab -->

As interações do GitLab dependem apenas de comentários. Quando a validação começar, um comentário será adicionado. Quando a validação for concluída (com êxito ou com falha), o comentário inicial será removido e substituído por um novo comentário que conterá os resultados da validação ou os detalhes do erro.

Quando a validação de qualidade do código estiver em execução:

![Quando a validação de qualidade do código estiver em execução](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

Quando a validação da qualidade a frio for concluída:

![Quando a validação da qualidade a frio for concluída](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

Quando a validação da qualidade do código falha com um erro:

![Quando a validação de qualidade do código falha com um erro](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)

Quando a validação da qualidade do código falhar devido a problemas do cliente:

![Quando a validação da qualidade do código falhar devido a problemas do cliente](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


>[!TAB Bitbucket]

<!-- https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/bitbucket -->

Quando a validação de qualidade do código estiver em execução:

![Status enquanto a validação de qualidade do código está em execução](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

Usa o status de confirmação para rastrear o progresso da validação da PR. No caso a seguir, a captura de tela mostra o que acontece quando uma validação de qualidade de código falha devido a um problema do cliente. Um comentário é adicionado com informações detalhadas sobre o erro e uma verificação de confirmação é criada, mostrando a falha (visível à direita):

![Status de validação da solicitação de pull para Bitbucket](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)

>[!TAB DevOps do Azure]

O Azure DevOps rastreia a validação da solicitação de pull por meio de verificações de status. Quando o Cloud Manager executa a validação de solicitação de pull, ele adiciona verificações de status que aparecem na interface de solicitação de pull do Azure DevOps.

Durante a validação da qualidade do código, uma verificação de status mostra que o processo está em andamento:

![Validação de DevOps do Azure de solicitações de pull com webhooks-1](/help/implementing/cloud-manager/managing-code/assets/azure-devops-validation-of-pull-requests-with-webhooks-1.png)

Quando a validação da qualidade do código for concluída, a verificação de status será atualizada para refletir os resultados:

![Validação de DevOps do Azure de solicitações de pull com webhooks-2](/help/implementing/cloud-manager/managing-code/assets/azure-devops-validation-of-pull-requests-with-webhooks-2.png)

Se a validação falhar, informações detalhadas sobre o erro serão fornecidas nos detalhes da verificação de status. Você pode clicar na verificação de status para exibir os resultados completos da validação no Cloud Manager.

![Validação de DevOps do Azure de solicitações de pull com webhooks-3](/help/implementing/cloud-manager/managing-code/assets/azure-devops-validation-of-pull-requests-with-webhooks-3.png)

Para comentários e comentários sobre solicitação de pull, o Cloud Manager adiciona comentários diretamente à solicitação de pull no Azure DevOps com detalhes de validação e todas as ações necessárias necessárias.

![Validação de DevOps do Azure de solicitações de pull com webhooks-4](/help/implementing/cloud-manager/managing-code/assets/azure-devops-validation-of-pull-requests-with-webhooks-4.png)


>[!ENDTABS]


## Solução de problemas de webhook

* Verifique se o URL do Webhook inclui uma chave de API válida.
* Verifique se os eventos do webhook estão configurados corretamente nas configurações do fornecedor do Git.
* Se a validação de PR ou os acionadores de pipeline não estiverem funcionando, verifique se o Segredo do Webhook está atualizado no Cloud Manager e no fornecedor do Git.


