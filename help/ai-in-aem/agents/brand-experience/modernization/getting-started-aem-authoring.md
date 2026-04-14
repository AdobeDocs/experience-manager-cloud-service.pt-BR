---
title: Introdução ao Agente de modernização de experiência para projetos de criação do AEM
description: Saiba mais sobre as etapas de configuração específicas necessárias para projetos de criação do AEM ao começar a usar o Agente de modernização de experiência usando o Console de modernização de experiência.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 94a5e40b-af4a-42ed-922b-b1ec9bb82e24
source-git-commit: 7b880e6d776e2eb9c53cef4552b876b051bdc7ba
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Introdução ao Agente de modernização de experiência para projetos de criação do AEM {#getting-started-aem-authoring}

Para projetos de criação do AEM usando o Editor universal, a preparação do Agente de modernização de experiência é diferente do fluxo padrão do Edge Delivery. Este documento aborda essas diferenças de configuração. Quando as etapas abaixo forem concluídas, siga o guia principal [Introdução ao Agente de modernização de experiência](getting-started.md).

## Criar seu repositório de projetos do Edge Delivery Services {#create-repo}

1. Use o repositório [`aem-block-collection-xwalk`](https://github.com/adobe-rnd/aem-block-collection-xwalk) como seu modelo (não o modelo padrão do Edge Delivery Services).
1. Verifique se `fstab.yaml` aponta para o host do AEM, o proprietário do Git e o repositório Git e confirme as alterações em `main` antes de conectar os aplicativos GitHub.
   * Consulte [Configurar fonte de conteúdo](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md) para obter instruções.
1. Siga o [tutorial do Universal Editor](https://www.aem.live/developer/ue-tutorial) para configurar seu repositório.
   * Pare quando for solicitado que você crie um site no AEM.
1. Excluir `paths.json` e confirmar essa alteração em `main`.
1. Adicione o aplicativo [Conector de código do AEM](https://github.com/apps/aem-code-connector/installations/select_target) ao repositório.
   * Isso permite que o console inspecione o código.

## Criar um novo site no AEM {#create-site}

1. No console do AEM Sites, selecione **Criar** > **Site a partir de modelo**.
1. Selecione o **Site do AEM com o Modelo do Edge Delivery Services**.
   * Não o vê listado? [Instalar o modelo.](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)
1. Mantenha o **nome** do site (não o título) conforme fornecido.
   * O nome do site é usado como o identificador exclusivo.
   * O título pode ser alterado para exibição.
1. Clique em **Criar**.
   * Você é redirecionado para a página Sites.
   * Atualize a página se o novo site não for exibido imediatamente.

## Continue com as etapas padrão de introdução {#continue}

Depois que as etapas acima forem concluídas, continue com o guia de introdução padrão para começar a migrar o conteúdo.

![Importação de conteúdo](assets/content-import.png)

Siga estas etapas no guia padrão.

1. [Preparar um repositório GitHub da Edge Delivery](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#prepare-repo)
1. [Abra o Console de Modernização da experiência](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#open-console)
1. [Conectar seu repositório GitHub](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#connect-repo)
1. [Iniciar Solicitação](/help/ai-in-aem/agents/brand-experience/modernization/getting-started.md#start-prompting)

![Conteúdo importado](assets/content-imported-aem-authoring.png)

Após concluir essas etapas para migrar o conteúdo, continue com as etapas a seguir.

## Validar conteúdo {#validate-content}

Valide o conteúdo da página selecionada no painel de visualização. Todos os erros serão exibidos clicando no botão **Erros**.
Continue a conversa de chat com o agente para corrigir os erros. Use o recurso **Adicionar ao chat** para direcionar correções para elementos específicos da página, arquivos de análise ou arquivos de transformador.

![Chat contextual](assets/contextual-chat.png)

## Fazer upload de conteúdo {#upload-content}

Para fazer upload do conteúdo para o AEM:

1. Verifique se você está no modo de exibição **Conteúdo** e clique no botão **Carregar conteúdo** no canto superior direito.
1. Na caixa de diálogo **Criar pacote de conteúdo**, escolha as páginas a serem incluídas no pacote.
   * Opcionalmente, insira um **Nome do pacote** (o padrão é o nome do site, se deixado em branco).
   * Use **Selecionar tudo**, **Limpar seleção**, **Expandir tudo** ou **Recolher tudo** para gerenciar a lista.
1. Clique em **Criar pacote**.

   ![Criar pacote de conteúdo - escolha as páginas e crie](assets/content-package.png)

1. Após a criação do pacote, a caixa de diálogo **Carregar pacote de conteúdo** mostra que o pacote está pronto.
   1. Você pode **Baixar o pacote** para salvá-lo localmente ou prosseguir com o carregamento.
   1. Em **Carregar para o AEM**, confirme o **site do AEM** e o **host do AEM** (preenchido previamente com as configurações do projeto).
      * Opcionalmente, deixe **Carregar imagens** marcado para incluir imagens.
   1. Clique em **Carregar para o AEM**.

   ![Pacote pronto para ser carregado no AEM ou baixado](assets/upload-package-start.png)

1. A caixa de diálogo mostra o progresso do upload à medida que páginas e ativos são enviados para a AEM. Quando o upload é concluído, uma mensagem de sucesso e o log de upload são exibidos. Clique em **Fechar** para fechar a caixa de diálogo.

   ![Progresso e conclusão do upload no AEM](assets/upload-package-complete.png)

O conteúdo importado agora está no AEM. Continue com [Alterações do código de push](getting-started.md#push-code-changes) no guia principal de introdução.

## Recursos adicionais {#additional-resources}

* [Introdução ao Agente de Modernização de Experiência](getting-started.md) - Fluxo de trabalho completo, incluindo console, prompt, carregamento e visualização
* [Console de Modernização da Experiência](console.md) - Referência do console
* [Tutorial do Universal Editor](https://www.aem.live/developer/ue-tutorial) - Configurar um projeto de criação e do Universal Editor do AEM
* [`aem-block-collection-xwalk`](https://github.com/adobe-rnd/aem-block-collection-xwalk) - Repositório de modelo para criação no AEM e projetos do Editor Universal
