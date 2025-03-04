---
title: Adicionar repositórios externos no Cloud Manager - beta limitado
description: Saiba como adicionar um repositório externo no Cloud Manager. O Cloud Manager oferece suporte à integração com repositórios GitHub, GitLab e Bitbucket.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: aebda813-2eb0-4c67-8353-6f8c7c72656c
source-git-commit: 5e2db30d9a505000881a0781dd5c4c2412a17ca8
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 39%

---

# Adicionar repositórios externos no Cloud Manager - beta limitado {#external-repositories}

Saiba como adicionar um repositório externo no Cloud Manager. O Cloud Manager oferece suporte à integração com repositórios GitHub, GitLab e Bitbucket.

>[!NOTE]
>
>Esse recurso só está disponível por meio do programa de adoção antecipada. Para obter mais detalhes e se inscrever como um dos primeiros usuários, consulte [Traga seu próprio Git - agora com suporte para GitLab e Bitbucket](/help/implementing/cloud-manager/release-notes/2024/2024-10-0.md#gitlab-bitbucket).

## Configurar um repositório externo

A configuração de um repositório externo no Cloud Manager consiste em três etapas:

1. [Adicionar um repositório externo](#add-external-repo) a um programa selecionado.
1. Forneça um token de acesso ao repositório externo.
1. Valide a propriedade do repositório GitHub privado.



## Adicione um repositório externo {#add-ext-repo}

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa ao qual deseja vincular um repositório externo.

1. No menu lateral, em **Serviços**, clique em ![Ícone de estrutura de tópicos de pasta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_FolderOutline_18_N.svg) **Repositórios**.

   ![A página Repositórios](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Próximo ao canto superior direito da página **Repositórios**, clique em **Adicionar Repositório**.

1. Na caixa de diálogo **Adicionar repositório**, selecione **Repositório privado** para vincular um repositório Git externo ao seu programa.

   ![Adicionar repositório próprio](/help/implementing/cloud-manager/managing-code/assets/repositories-private-repo-type.png)

1. Em cada campo respectivo, forneça os seguintes detalhes sobre o repositório:

   | Texto | Descrição |
   | --- | --- |
   | **Nome do repositório** | Obrigatório. Um nome expressivo para o novo repositório. |
   | **URL do repositório** | Obrigatório. O URL do repositório.<br><br>Se você estiver usando um repositório hospedado pelo GitHub, o caminho deverá terminar em `.git`.<br>Por exemplo, *`https://github.com/org-name/repo-name.git`* (o caminho do URL é apenas para fins ilustrativos).<br><br>Se você estiver usando um repositório externo, ele deverá usar o seguinte formato de caminho de URL:<br>`https://git-vendor-name.com/org-name/repo-name.git`<br> ou<br>`https://self-hosted-domain/org-name/repo-name.git`<br>e corresponder ao seu fornecedor de Git. |
   | **Selecionar tipo de repositório** | Obrigatório. Selecione o tipo de repositório que você está usando:<ul><li>**GitHub** (GitHub Enterprise Server e a versão auto-hospedada do GitHub)</li><li>**GitLab** (o `gitlab.com` e a versão auto-hospedada do GitLab) </li><li>**Bitbucket** (o `bitbucket.org` e o Servidor de Bitbucket e a versão auto-hospedada do Bitbucket)</li></ul>Se o caminho do URL do repositório acima incluir o nome do fornecedor do Git, como GitLab ou Bitbucket, o tipo de repositório já estará pré-selecionado. |
   | **Descrição** | Opcional. Uma descrição detalhada do repositório. |

1. Clique em **Salvar** para adicionar o repositório.

1. Na caixa de diálogo **Validação de propriedade de repositório privado**, forneça um token de acesso para validar a propriedade do repositório externo para que você possa acessá-lo.

   ![Seleção de um token de acesso para um repositório](/help/implementing/cloud-manager/managing-code/assets/repositories-exisiting-access-token.png)
   *Selecionando um token de acesso existente para um repositório Bitbucket.*

   | Tipo de token | Descrição |
   | --- | --- |
   | **Usar token de acesso já existente** | Se você já forneceu um token de acesso ao repositório para sua organização e tem acesso a vários repositórios, você pode selecionar um token. Use a lista suspensa **Nome do token** para escolher o token que deseja aplicar ao repositório. Caso contrário, adicione um novo token de acesso. |
   | **Adicionar novo token de acesso** | **Tipo de repositório: GitHub**<br>• No campo de texto **Nome do token**, digite um nome para o token de acesso que você está criando.<br>• Crie um token de acesso pessoal seguindo as instruções na [documentação do GitHub](https://docs.github.com/en/enterprise-server@3.14/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).<br>· Para obter as permissões necessárias, consulte [Criar novo PAT para GitHub](https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/create-new-github-pat).<br>• No campo **Token de acesso**, cole o token que você acabou de criar. |
   |  | **Tipo de repositório: GitLab**<br>• No campo de texto **Nome do token**, digite um nome para o token de acesso que você está criando.<br>• Crie um token de acesso pessoal seguindo as instruções na [documentação do GitLab](https://docs.gitlab.com/user/profile/personal_access_tokens/).<br>· Para obter as permissões necessárias, consulte [Criar um novo PAT para GitLab](https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/create-new-gitlab-pat).<br>• No campo **Token de acesso**, cole o token que você acabou de criar. |
   |  | **Tipo de repositório: Bitbucket**<br>• No campo de texto **Nome do token**, digite um nome para o token de acesso que você está criando.<br>• Crie um token de acesso ao repositório usando a [documentação do Bitbucket](https://support.atlassian.com/bitbucket-cloud/docs/create-a-repository-access-token/).<br>· Para obter as permissões necessárias, consulte [Criar um novo PAT para o Bitbucket](https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/create-new-bitbucket-path). |

   >[!NOTE]
   >
   >O recurso **Adicionar novo token de acesso** está atualmente na fase de Adoção antecipada. Funcionalidades adicionais estão sendo planejadas. Como resultado, as permissões necessárias para tokens de acesso podem mudar. Além disso, a interface de usuário para gerenciamento de tokens pode ser atualizada, possivelmente incluindo recursos como datas de expiração de tokens. E verificações automatizadas para garantir que os tokens vinculados aos repositórios permaneçam válidos.

1. Clique em **Validar**.

Após a validação, o repositório externo estará pronto para ser usado e vinculado a um pipeline.

## Vincular um repositório externo validado a um pipeline {#validate-ext-repo}

1. Adicionar ou editar um pipeline:
   * [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Adicionar pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)
   * [Editar um pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#editing-pipelines)

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
Para todos os outros repositórios externos integrados com um token de acesso, como GitHub Enterprise Server, GitLab e Bitbucket, a configuração de webhook está disponível e deve ser definida manualmente.

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
1. Navegue até a solução do fornecedor de Git (GitHub Enterprise, GitLab ou Bitbucket).
1. Localize a seção Configurações do **Webhook** da solução.
1. Cole o URL do Webhook copiado anteriormente no campo de texto do URL.
   1. Substitua o parâmetro de consulta `api_key` na URL do Webhook pela sua própria chave de API real.

      Para gerar uma chave de API, você deve criar um projeto de integração no Adobe Developer Console. Consulte [Criando um Projeto de Integração de API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/) para obter detalhes completos.

1. Cole o Segredo do Webhook copiado anteriormente no campo de texto **Segredo** (ou **Chave secreta** ou **Token secreto**).
1. Configure o webhook para enviar os eventos apropriados que o Cloud Manager espera.

   Todos os detalhes sobre a configuração do webhook e os eventos necessários para cada fornecedor estão disponíveis no link a seguir:

   * [Configurar webhooks do GitHub Enterprise Server](https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/create-new-github-pat?id=webhook-events).
   * [Configurar webhooks para GitLab](https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/create-new-gitlab-pat?id=webhook-events).
   * [Configurar webhooks para o Bitbucket](https://git.corp.adobe.com/pages/experience-platform/cloud-manager-repository-service/#/./git-vendors/create-new-bitbucket-pat?id=webhook-events).

### Validação de pull requests com webhooks

Depois que os webhooks forem configurados corretamente, o Cloud Manager acionará automaticamente as execuções de pipeline ou as verificações de validação de PR para o repositório.

Os seguintes comportamentos se aplicam:

* **GitHub Enterprise Server**

  Quando a verificação é criada, ela é exibida como a seguinte captura de tela abaixo. A principal diferença em relação a `GitHub.com` é que `GitHub.com` usa uma execução de verificação, enquanto o GitHub Enterprise Server (usando tokens de acesso pessoal) gera um status de confirmação:

  ![Confirmar status para indicar o processo de validação de PR no GitHub Enterprise Server](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-github-pr-validation.png)

* **Bitbucket**

  Quando a validação de qualidade do código estiver em execução:

  ![Status enquanto a validação de qualidade do código está em execução](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket1.png)

  Usa o status de confirmação para rastrear o progresso da validação da PR. No caso a seguir, a captura de tela mostra o que acontece quando uma validação de qualidade de código falha devido a um problema do cliente. Um comentário é adicionado com informações detalhadas sobre o erro e uma verificação de confirmação é criada, mostrando a falha (visível à direita):

  ![Status de validação da solicitação de pull para Bitbucket](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-bitbucket2.png)

* **GitLab**

  As interações do GitLab dependem apenas de comentários. Quando a validação começar, um comentário será adicionado. Quando a validação for concluída (com êxito ou com falha), o comentário inicial será removido e substituído por um novo comentário que conterá os resultados da validação ou os detalhes do erro.

  Quando a validação de qualidade do código estiver em execução:

  ![Quando a validação de qualidade do código estiver em execução](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab1.png)

  Quando a validação da qualidade a frio for concluída:

  ![Quando a validação da qualidade a frio for concluída](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab2.png)

  Quando a validação da qualidade do código falha com um erro:

  ![Quando a validação de qualidade do código falha com um erro](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab3.png)

  Quando a validação da qualidade do código falhar devido a problemas do cliente:

  ![Quando a validação da qualidade do código falhar devido a problemas do cliente](/help/implementing/cloud-manager/managing-code/assets/repository-webhook-gitlab4.png)


## Solução de problemas de webhook

* Verifique se o URL do Webhook inclui uma chave de API válida.
* Verifique se os eventos do webhook estão configurados corretamente nas configurações do fornecedor do Git.
* Se a validação de PR ou os acionadores de pipeline não estiverem funcionando, verifique se o Segredo do Webhook está atualizado no Cloud Manager e no fornecedor do Git.








## Limitações

* Repositórios externos não podem ser vinculados aos Pipelines de configuração.
* Os pipelines com repositórios externos (não hospedados no GitHub) e o acionador &quot;Nas alterações do Git&quot; não são iniciados automaticamente. Eles só podem ser iniciados manualmente.


<!-- THIS BULLET REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2024.12.0+Release. THEY CAN NOW START AUTOMATICALLY>
* Pipelines using external repositories (excluding GitHub-hosted repositories) and the **Deployment Trigger** option [!UICONTROL **On Git Changes**], triggers are not automatically started. They must be manually started. -->


