---
title: Guia de introdução do desenvolvedor para criação de AEM com o Edge Delivery Services
description: Este guia colocará você em funcionamento com um novo site do Adobe Experience Manager usando o Edge Delivery Services e o Editor universal para criação de conteúdo
feature: Edge Delivery Services
source-git-commit: 5967bd78b9c23cf3451ac3b0ec2118da5200ddc1
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---


# Criação de AEM com o Edge Delivery Services {#edge-dev-getting-started}

Este guia colocará você em funcionamento com um novo site do Adobe Experience Manager usando o Edge Delivery Services e o Editor universal para criação de conteúdo.

{{aem-authoring-edge-early-access}}

## Pré-requisitos {#prerequisites}

Antes de começar este guia, você já deve estar familiarizado com as noções básicas do e ter acesso ao Edge Delivery Services, incluindo:

* Você concluiu o [Tutorial do Edge Delivery Service.](/help/edge/developer/tutorial.md)
* Você tem acesso a um [sandbox AEM Cloud Service.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
* Você tem [ativou o Editor universal no mesmo ambiente de sandbox.](/help/implementing/universal-editor/getting-started.md)

## Escolha o editor direito {#editor-choice}

O AEM oferece dois editores de conteúdo diferentes e a escolha de qual usar depende da sua situação.

* **Editor universal** - Essa deve ser a opção padrão para novos sites.
* **Editor de página AEM** - Essa opção deve ser escolhida para uma migração existente do AEM Sites para o Edge Delivery Services.

Este guia tem como foco projetos AEM em Edge Delivery Services usando o Editor universal. Consulte o documento [Desenvolvimento do Edge Delivery Services](/help/edge/developing.md) para obter mais detalhes sobre a escolha do editor correto e a migração dos sites de AEM existentes para o Edge Delivery Services.

## Introdução à criação e ao Edge Delivery Services do AEM {#getting-started}

Depois de ter cumprido [os pré-requisitos](#prerequisites) e tenham feito [a opção de usar o Editor universal,](#editor-choice) você pode começar com seu próprio projeto.

### Criar seu projeto do GitHub {#create-github-project}

Primeiro, será necessário criar um novo projeto no GitHub, com base no modelo de Adobe.

1. Navegue até [`https://github.com/adobe-rnd/aem-boilerplate-xwalk`](https://github.com/adobe-rnd/aem-boilerplate-xwalk) e clique em **Usar este modelo** e selecione **Criar um novo repositório**.

   * Você precisará fazer logon no GitHub para ver essa opção.

   ![Copiar projeto do repositório](assets/edge-dev-getting-started/use-template-project.png)

1. Por padrão, o repositório será atribuído a você. Altere isso conforme necessário, forneça um nome de repositório e uma descrição e clique em **Criar repositório**.

   ![Criação do repositório](assets/edge-dev-getting-started/create-repo.png)

1. Em uma nova guia no mesmo navegador, navegue até [`https://github.com/apps/aem-code-sync`](https://github.com/apps/aem-code-sync) e clique em **Configurar**.

   ![Sincronização de código](assets/edge-dev-getting-started/configure-code-sync.png)

1. Clique em **Configurar** para a organização em que você criou o novo repositório na etapa anterior.

   ![Escolha da organização para sincronização de código](assets/edge-dev-getting-started/code-sync-org.png)

1. Na página GitHub de sincronização de código do AEM, em **Acesso ao repositório**, selecione **Selecionar apenas repositórios**, selecione o repositório criado na etapa anterior e clique em **Salvar**.

   ![Conceder acesso à Sincronização de código AEM](assets/edge-dev-getting-started/grant-code-sync-acces.png)

1. Depois que a Sincronização de código AEM estiver instalada, você receberá uma tela de confirmação. Retorne à guia do navegador do novo repositório.

   ![Confirmação de instalação da Sincronização de código](assets/edge-dev-getting-started/confirmation.png)

1. Clique em `fstab.yaml` para abri-lo e, em seguida, o **Editar este arquivo** ícone para editá-lo.

   ![fstab.yaml](assets/edge-dev-getting-started/fstab.png)

1. Edite o `fstab.yaml` arquivo para atualizar o ponto de montagem do projeto. Substitua o URL padrão dos documentos do Google pelo URL da sua instância de criação do AEM as a Cloud Service e clique em **Confirmar alterações...**.

   * `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`
   * Alterar o ponto de montagem informa ao Edge Delivery Services onde localizar o conteúdo do site.

   ![Atualizando fstab](assets/edge-dev-getting-started/fstab-update.png)

1. Adicione uma mensagem de confirmação conforme desejado e clique em **Confirmar alterações**, comprometendo-os diretamente com a `main` filial.

   ![Confirmando alterações](assets/edge-dev-getting-started/commit-fstab-changes.png)

1. Retorne à raiz do repositório e clique em `paths.yaml` e, em seguida, o **Editar este arquivo** ícone.

   ![caminhos.yaml](assets/edge-dev-getting-started/paths.png)

1. Substituir os mapeamentos padrão por `/content/<site-name>/:/` e clique em **Confirmar alterações...**.

   * Forneça o seu próprio `<site-name>`. Você precisará dele em uma etapa posterior.
   * Os mapeamentos informam ao Edge Delivery Services como mapear o conteúdo no repositório AEM para o URL do site.

   ![Atualizando paths.yaml](assets/edge-dev-getting-started/paths-update.png)

1. Adicione uma mensagem de confirmação conforme desejado e clique em **Confirmar alterações**, comprometendo-os diretamente com a `main` filial.

   ![Confirmando alterações](assets/edge-dev-getting-started/commit-fstab-changes.png)

### Criar e editar um novo site AEM {#create-aem-site}

Agora que você tem um projeto GitHub, deve criar um novo site AEM que o projeto possa usar.

>[!NOTE]
>
>Para editar o site usando o Editor universal, é necessário usar um navegador com base em Chromium.

1. Solicite a mais recente criação de AEM com o modelo de site Edge Delivery Services da engenharia de Adobe por meio de [canal Slack do projeto.](/help/edge/docs/slack.md)

1. Faça logon na instância de criação do AEM as a Cloud Service e navegue até o console Sites e toque ou clique **Criar** -> **Site do modelo**.

   ![Criar um novo site por meio do console](assets/edge-dev-getting-started/create-site-console.png)

1. No **Selecionar um modelo de site** do assistente criar site, clique na guia **Importar** botão para importar um novo template.

   ![Importação de modelos](assets/edge-dev-getting-started/site-templates.png)

1. Carregue o AEM Authoring com o modelo de site Edge Delivery Services fornecido pelo Adobe Engineering.

1. Depois que o modelo for importado, ele aparecerá no assistente. Toque ou clique para selecioná-lo e, em seguida, toque ou clique **Próxima**.

   ![Selecionar modelo](assets/edge-dev-getting-started/select-template.png)

1. Forneça os seguintes campos e toque ou clique **Criar**.

   * **Título do site** - Adicione um título descritivo para o site.
   * **Título do site** - Use o `<site-name>` definido na variável [etapa anterior.](#create-github-project)
   * **URL do GitHub** - Use o URL do projeto GitHub criado na etapa anterior.

   ![Detalhes do site](assets/edge-dev-getting-started/create-site-details.png)

1. O AEM confirma a criação do site com uma caixa de diálogo. Toque ou clique **OK** de indeferimento.

   ![Confirmação de criação do site](assets/edge-dev-getting-started/site-creation-confirmation.png)

1. No console Sites, navegue até a `index.html` do site recém-criado e toque ou clique **Editar** na barra de ferramentas.

   ![Edição do novo site](assets/edge-dev-getting-started/new-site.png)

1. O Editor universal é aberto em uma nova guia. Talvez seja necessário tocar ou clicar **Entrar com o Adobe** para autenticar e editar sua página.

   ![Editor universal](assets/edge-dev-getting-started/universal-editor.png)

Agora você pode editar seu site usando o Editor universal. Consulte a [Documentação do Universal Editor](/help/implementing/universal-editor/authoring.md) para obter mais informações.

### Publicar seu novo site {#publishing}

Quando terminar de editar o novo site usando o Editor universal, você poderá publicar o conteúdo.

1. No console Sites, selecione todas as páginas criadas para o novo site e toque ou clique **Publicação rápida** na barra de ferramentas.

   ![Seleção de páginas para publicação](assets/edge-dev-getting-started/publishing.png)

1. Toque ou clique **Publish** no diálogo de confirmação para iniciar o processo.

   ![Caixa de diálogo Publicar](assets/edge-dev-getting-started/publish-confirmation.png)

1. Abra uma nova guia no mesmo navegador e navegue até o URL do novo site.

   * `https://main--<site-name>--<owner>.hlx.page`

1. Veja seu conteúdo publicado.

   ![Conteúdo publicado](assets/edge-dev-getting-started/published-site.png)
