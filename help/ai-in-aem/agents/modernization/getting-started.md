---
title: Introdução ao Agente de modernização de experiência
description: Saiba mais sobre as primeiras etapas para se tornar produtivo rapidamente com o Agente de modernização de experiência usando o Console de modernização de experiência.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: c80ce5a9fc5f208fd910d5cef72225085248fb4d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Introdução ao Agente de modernização de experiência {#getting-started}

Saiba mais sobre as primeiras etapas para se tornar produtivo rapidamente com o Agente de modernização de experiência usando o Console de modernização de experiência.

>[!NOTE]
>
>Se você estiver interessado em usar o Console de modernização de experiência, poderá solicitar acesso para garantir uma experiência de integração tranquila.

## Preparar um repositório GitHub da Edge Delivery {#prepare-repo}

1. Selecione um repositório do [Edge Delivery Services](/help/edge/overview.md) para usar com o Console de Modernização de Experiência.
   * Pode ser um projeto Edge Delivery Services existente ou você pode criar um novo seguindo o [tutorial do desenvolvedor](https://www.aem.live/developer/tutorial) usando o [repositório padronizado.](https://github.com/adobe/aem-boilerplate)
1. Verifique se o [aplicativo GitHub do AEMY](https://github.com/apps/aem-aemy) está instalado no repositório.
   * Isso permite que o console inspecione o código.
1. Verifique se o [aplicativo GitHub da Sincronização de Código do AEM](https://github.com/apps/aem-code-sync) está instalado no repositório.
   * Isso permite que o Edge Delivery Services sincronize seu código.
   * Se o acordo de recompra se basear no tutorial, esta etapa já estará concluída.

## Abra o Console de Modernização da experiência {#open-console}

1. Navegue até [`aemcoder.adobe.io`.](https://aemcoder.adobe.io)
1. Faça logon com sua Adobe ID.

## Conectar seu repositório GitHub {#connect-repo}

O console solicita um repositório ao fazer logon pela primeira vez.

![Primeira tela de entrada do console](assets/first-sign-on.png)

1. Clique em **Conectar repositório**.
1. O aplicativo AEMY será aberto em uma nova guia do navegador. Clique em **Autorizar AEM AEMY**.
1. De volta ao console, selecione **Proprietário**, **Repositório** e **Seleção de ramificação** e clique em **Fazer check-out para o espaço de trabalho**.
   ![Conectando ao projeto GitHub](assets/connect-to-github-project.png)
1. Quando solicitado a **Substituir espaço de trabalho existente**, clique em **Substituir espaço de trabalho**.
   ![Substituir espaço de trabalho existente](assets/replace-existing-workspace.png)

Seu projeto do GitHub agora está conectado ao console e você está na tela inicial.

![Página inicial do console](assets/console-home.png)

## Iniciar Solicitação {#start-prompting}

Agora que o console pode acessar o código, você está pronto para começar a solicitar.

1. Para começar, você pode importar o conteúdo de um site:
   * &quot;Migrar a página `https://wknd-trendsetters.site`.&quot;
1. Isso importa o conteúdo do site.
   * O console observa a separação de interesses e lida com o conteúdo e a apresentação separadamente.
   * A importação inicial do conteúdo de um site pode levar vários minutos.
   * O console fornece feedback contínuo à medida que inicia seu trabalho, incluindo uma visão geral de suas etapas planejadas.
     ![Importação de conteúdo](assets/content-import.png)
1. Depois que o site for importado, o painel **Workspace** mostrará as páginas. Selecione uma página para visualizá-la no painel direito.
   ![Conteúdo importado](assets/content-imported.png)
1. Agora que você tem conteúdo, é possível solicitar a importação dos estilos da mesma origem.
   * &quot;Importar os estilos gerais de `https://wknd-trendsetters.site`.&quot;
1. Assim como na importação de conteúdo inicial, a importação pode levar vários minutos, e o console fornece feedback enquanto processa sua solicitação e importa os estilos. Quando a tarefa for concluída, clique em **Atualizar visualização** no painel direito para exibir o conteúdo estilizado.
   ![Estilos importados](assets/styles-imported.png)

Agora você tem o conteúdo e os estilos importados para o console.

## Fazer upload de conteúdo {#upload-content}

Para carregar seu conteúdo para a [Criação de Documentos](https://da.live):

1. Verifique se você está no modo de exibição **Conteúdo** e clique no botão **Carregar conteúdo** no canto superior direito.
   * Por padrão, você está no modo de exibição **Conteúdo** ao entrar no console.
   * Sua visualização é indicada pelo ícone destacado na barra lateral ao longo do lado esquerdo do console.
1. A caixa de diálogo **Carregar conteúdo** é aberta com a organização de destino e o repositório preenchidos previamente a partir do `fstab.yaml`.
   * Se um `fstab.yaml` não estiver presente no repositório conectado, você precisará inserir manualmente a **Organização** e o **Repositório**.
   * Se você usou o padrão de formatação, um `fstab.yaml` será fornecido.
1. Selecione os arquivos que você deseja carregar e clique em **Carregar**.
   ![Caixa de diálogo Carregar conteúdo](assets/upload-content.png)
1. O console indica o processo de carregamento esmaecendo o botão **Carregar**.
   ![Carregando](assets/uploading.png)
1. Uma vez concluída, uma notificação será exibida na parte inferior do console.
   ![Exibir no AEM](assets/view-in-aem.png)

Para acessar o conteúdo carregado na Criação de Documentos, clique opcionalmente em **Exibir na AEM** na notificação quando o carregamento for concluído ou navegue até `https://da.live/#/{organization}/{repository}`.

![Conteúdo na criação de documentos](assets/content-in-document-authoring.png)

O conteúdo importado agora está na Criação de documentos.

## Alterações no código push {#push-code-changes}

Quando estiver satisfeito com as alterações feitas no código, você poderá enviá-las para o repositório do GitHub.

1. Alterne para a exibição **Código** (`</>` ícone na barra lateral esquerda) e, em seguida, para a guia **Alterações do Git** (ícone de ramificação na parte superior direita).
   ![Modo de exibição de código](assets/code-view-git-changes.png)
1. Na lista de arquivos alterados, se alguns arquivos forem exibidos como não rastreados, clique no botão `+` para prepará-los.
1. Clique no botão **Ações do GitHub** no canto superior direito e selecione **Push** no menu suspenso.
1. Na caixa de diálogo **Enviar alterações**, escolha enviar alterações para uma nova PR (padrão) ou para a ramificação atual e clique em **Confirmar** para enviar.
   * Na dúvida, você pode enviar para a ramificação atual para manter as coisas simples.
1. Uma vez concluída, uma notificação será exibida na parte inferior do console.
   ![Exibir PR](assets/view-pr.png)

Se quiser acessar diretamente as alterações enviadas no GitHub, clique em **Exibir PR** na notificação quando o envio for concluído.

![Código no GitHub](assets/code-in-github.png)

Seu código agora está no GitHub.

## Visualizar site {#preview-site}

Para exibir as alterações no ambiente de visualização:

1. Volte para Criação de documentos.
   * Ela ainda pode estar aberta em uma guia do navegador que você abriu depois de clicar em **Exibir no AEM** depois de carregar o conteúdo.
   * Ou navegue até `https://da.live/#/{organization}/{repository}`
1. Abra uma das páginas que você carregou anteriormente no AEM.
1. Clique no ícone de plano de papel (canto superior direito) e selecione **Visualizar**.
   ![Publicar para visualização](assets/publish-to-preview.png)

Parabéns! O conteúdo e os estilos migrados agora estão ativos no ambiente de visualização do AEM.

![Conteúdo de visualização publicado](assets/published-preview.png)

Se você enviou seu código para uma ramificação diferente de `main`, a visualização aberta da Criação de documentos não mostrará os estilos. Altere para a ramificação atualizando o URL da visualização e você poderá ver seus estilos.

## Recursos adicionais {#additional-resources}

Os documentos a seguir podem ser úteis à medida que você continua explorando o Agente de modernização de experiência e seu console.

* [Console de Modernização da Experiência](/help/ai-in-aem/agents/modernization/console.md) - Detalhes sobre o console, suas visualizações, opções e recursos
* [Tutorial do desenvolvedor do Edge Delivery Services](https://www.aem.live/developer/tutorial) - Útil se você é novo em projetos AEM e Edge Delivery Services
* [Criação de documentos](https://da.live) - Útil se você é novo na criação de documentos para gerenciamento de conteúdo
