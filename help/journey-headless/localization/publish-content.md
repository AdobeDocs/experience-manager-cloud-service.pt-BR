---
title: Publicar conteúdo traduzido
description: Saiba como publicar seu conteúdo localizado.
source-git-commit: 3ab886361dc01c943bd00025695d34a218b1aa41
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---

# Publicar conteúdo traduzido {#publish-content}

Saiba como publicar seu conteúdo localizado.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de localização sem cabeçalho AEM, [Traduza conteúdo,](configure-connector.md) você aprendeu a usar AEM Projetos de tradução para traduzir seu conteúdo sem cabeçalho. Agora você deve:

* Entenda o que é um projeto de tradução.
* Pode criar novos projetos de tradução.
* Use projetos de tradução para traduzir o conteúdo sem periféricos.

Agora que sua tradução inicial foi concluída, este artigo o orienta pela próxima etapa da publicação desse conteúdo e o que fazer para atualizar suas traduções conforme o conteúdo raiz do idioma subjacente muda.

## Objetivo {#objective}

Este documento ajuda você a entender como publicar conteúdo sem periféricos no AEM e como criar um fluxo de trabalho contínuo para manter suas traduções atualizadas. Após ler este documento, você deve:

* Entenda o modelo de AEM de publicação de autor.
* Saiba como publicar seu conteúdo traduzido.
* É possível implementar um modelo de atualização contínuo para o seu conteúdo traduzido.

## Modelo de publicação do autor do AEM {#author-publish}

Antes de publicar seu conteúdo, é uma boa ideia entender AEM modelo de publicação do autor. Nos seus termos mais simples, AEM divide os usuários do sistema em dois grupos.

1. Aqueles que criam e gerenciam o conteúdo e o sistema
1. Aqueles que consomem o conteúdo do sistema.

Portanto, AEM é fisicamente separado em duas instâncias.

1. A instância **author** é o sistema no qual os autores e administradores de conteúdo trabalham para criar e gerenciar conteúdo.
1. A instância **publish** é o sistema que entrega o conteúdo aos consumidores.

Depois que o conteúdo é criado na instância do autor, ele deve ser transferido para a instância de publicação para que esteja disponível para consumo. O processo de transferência do autor para a publicação é chamado de **publication**.

## Publicar seu conteúdo traduzido {#publishing}

Quando estiver satisfeito com o estado do conteúdo traduzido, você poderá publicá-lo para que os serviços sem periféricos possam consumi-lo. A maneira mais fácil de fazer isso é navegar até a pasta de ativos do projeto.

```text
/content/dam/<your-project>/
```

Nesse caminho, você tem subpastas para cada idioma de tradução e pode escolher qual publicar.

1. Vá para **Navegação** -> **Ativos** -> **Arquivos** e abra a pasta do projeto.
1. Aqui você verá a pasta raiz do idioma e todas as outras pastas de idioma. Selecione o idioma ou idiomas localizados que deseja publicar.
   ![Selecionar pasta de idioma](assets/select-language-folder.png)
1. Toque ou clique em **Gerenciar publicação**.
1. Na janela **Gerenciar publicação**, verifique se **Publicar** é automaticamente selecionado em **Ação** e se **Agora** é selecionado em **Agendamento**. Toque ou clique em **Próximo**.
   ![Gerenciar opções de publicação](assets/manage-publication-options.png)
1. Na próxima janela **Gerenciar publicação**, confirme se os caminhos adequados estão selecionados. Toque ou clique em **Publicar**.
   ![Gerenciar escopo de publicação](assets/manage-publication-scope.png)
1. AEM confirma a ação de publicação com uma mensagem pop-up na parte inferior da tela.
   ![Banner publicado de recursos](assets/resources-published-message.png)

Seu conteúdo localizado sem cabeçalho foi publicado! Agora ele pode ser acessado e consumido pelos serviços sem periféricos.

>[!TIP]
>
>Você pode selecionar vários itens (ou seja, várias pastas de idioma) ao publicar para publicar várias localizações ao mesmo tempo.

Há opções adicionais ao publicar seu conteúdo, como agendar um tempo de publicação, que estão além do escopo dessa jornada. Consulte a seção [Recursos adicionais](#additional-resources) no final do documento para obter mais informações.

## Atualização do seu conteúdo traduzido {#updating-translations}

A localização e a tradução raramente são um exercício pontual. Normalmente, seus autores de conteúdo continuam a adicionar e modificar seu conteúdo na raiz do idioma depois que a localização inicial é concluída. Isso significa que também será necessário atualizar o conteúdo traduzido.

Requisitos específicos do projeto definirão com que frequência você precisará atualizar suas traduções e qual processo de decisão será seguido antes de executar uma atualização. Depois de decidir atualizar suas traduções, o processo no AEM é muito simples. Como a tradução inicial foi baseada em um projeto de tradução, também há atualizações.

1. Navegue até **Navegação** -> **Ativos** -> **Arquivos**. Lembre-se de que o conteúdo sem periféricos no AEM é armazenado como ativos conhecidos como Fragmentos de conteúdo.
1. Selecione a raiz do idioma do projeto. Nesse caso, selecionamos `/content/dam/wknd/en`.
1. Toque ou clique no seletor do painel e mostre o painel **Referências**.
1. Toque ou clique em **Cópias de idioma**.
1. Marque a caixa de seleção **Language Copies**.
1. Expanda a seção **Atualizar cópias de idioma** na parte inferior do painel de referências.
1. Na lista suspensa **Project**, selecione **Adicionar a um Projeto de Tradução existente**.
1. Na lista suspensa **Projeto de tradução existente**, selecione o projeto criado para a tradução inicial.
1. Toque ou clique em **Iniciar**.

![Adicionar itens ao projeto de tradução existente](assets/add-to-existing-project.png)

O conteúdo é adicionado ao projeto de tradução existente. Para exibir o projeto de tradução:

1. Navegue até **Navegação** - e **Projetos**.
1. Toque ou clique no projeto que você acabou de atualizar.
1. Toque ou clique no idioma ou em um dos idiomas atualizados.

Você verá que um novo cartão de trabalho foi adicionado ao projeto. Neste exemplo, foi adicionada outra tradução em espanhol.

![Tarefa de tradução adicional adicionada](assets/additional-translation-job.png)

Você observará que as estatísticas listadas no novo cartão (número de ativos e fragmentos de conteúdo) são diferentes. Isso ocorre porque o AEM reconhece o que foi alterado desde a última tradução e inclui apenas o novo conteúdo que precisa ser traduzido (tanto o conteúdo atualizado retraduzido quanto a primeira tradução do novo conteúdo).

A partir deste ponto, você [inicia e gerencia seu trabalho de tradução exatamente como fazia no original.](translate-content.md#using-translation-project)

## Fim da Jornada? {#end-of-journey}

Parabéns! Você concluiu a jornada de localização sem cabeçalho! Agora você deve:

* Ter uma visão geral do que é a entrega de conteúdo sem periféricos.
* Tenha um Compreensão básica AEM recursos headless.
* Entenda AEM recursos de localização e como eles estão relacionados ao conteúdo sem periféricos.
* Tenha a capacidade de começar a localizar seu próprio conteúdo sem periféricos.

Agora você está pronto para localizar seu próprio conteúdo sem periféricos no AEM. No entanto, AEM é uma ferramenta poderosa e há muitas opções adicionais disponíveis. Confira alguns dos recursos adicionais disponíveis na próxima seção para saber mais sobre os recursos que você viu nesta jornada.

## Recursos adicionais {#additional-resources}

* [Gerenciamento de projetos de tradução](/help/sites-cloud/administering/translation/managing-projects.md)  - saiba mais detalhes de projetos de tradução e recursos adicionais, como fluxos de trabalho de tradução humana e projetos de vários idiomas.
* [Criação de conceitos](/help/sites-cloud/authoring/getting-started/concepts.md)  - saiba mais sobre o modelo de criação e publicação de AEM com mais detalhes. Este documento está focado na criação de páginas em vez de Fragmentos de conteúdo, mas a teoria ainda se aplica.
* [Publicação de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)  - saiba mais sobre os recursos adicionais disponíveis ao publicar conteúdo. Este documento está focado na criação de páginas em vez de Fragmentos de conteúdo, mas a teoria ainda se aplica.
