---
title: Traduzir conteúdo
description: Use o conector e as regras de tradução para traduzir o conteúdo sem cabeçalho.
source-git-commit: 016b1126effb96598c9700377291333fb326c292
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 0%

---

# Traduzir conteúdo {#translate-content}

Use o conector e as regras de tradução para traduzir o conteúdo sem cabeçalho.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de localização sem cabeçalho AEM, [Configurar regras de tradução](translation-rules.md) você aprendeu a usar AEM regras de tradução para identificar o conteúdo de tradução. Agora você deve:

* Entenda o que as regras de tradução fazem.
* Pode definir suas próprias regras de tradução.

Agora que seu conector e as regras de tradução estão configurados, este artigo o orienta pela próxima etapa da tradução do conteúdo sem periféricos.

## Objetivo {#objective}

Este documento ajuda você a entender como usar AEM projetos de tradução junto com o conector e suas regras de tradução para traduzir o conteúdo. Após ler este documento, você deve:

* Entenda o que é um projeto de tradução.
* Pode criar novos projetos de tradução.
* Use projetos de tradução para traduzir o conteúdo sem periféricos.

## Criação de um projeto de tradução {#creating-translation-project}

Os projetos de tradução permitem gerenciar a tradução de conteúdo AEM sem periféricos. Um projeto de tradução contém o conteúdo a ser traduzido para outros idiomas.

Quando o conteúdo é adicionado a um projeto de tradução, um trabalho de tradução é criado para ele. Os trabalhos fornecem comandos e informações de status que você usa para gerenciar os workflows de tradução humana e tradução automática que são executados nos recursos.

Para criar um projeto de tradução:

1. Navegue até **Navegação** -> **Ativos** -> **Arquivos**. Lembre-se de que o conteúdo sem periféricos no AEM é armazenado como ativos conhecidos como Fragmentos de conteúdo.
1. Selecione a raiz do idioma do projeto. Nesse caso, selecionamos `/content/dam/wknd/en`.
1. Toque ou clique no seletor do painel e mostre o painel **Referências**.
1. Toque ou clique em **Cópias de idioma**.
1. Marque a caixa de seleção **Language Copies**.
1. Expanda a seção **Atualizar cópias de idioma** na parte inferior do painel de referências.
1. Na lista suspensa **Project**, selecione **Criar projeto(s) de tradução**.
1. Forneça um título apropriado para o seu projeto de tradução.
1. Toque ou clique em **Iniciar**.

![Criar um novo projeto de tradução](assets/create-translation-project.png)

Você receberá uma mensagem informando que o projeto foi criado.

>[!NOTE]
>
>Pressupõe-se que a estrutura de idioma necessária para os idiomas de tradução já tenha sido criada como parte da [definição da estrutura de conteúdo.](getting-started.md#content-structure) Isso deve ser feito em colaboração com o arquiteto de conteúdo.

## Usar um projeto de tradução {#using-translation-project}

Ao criar o projeto de tradução, o AEM avaliou o conteúdo sem cabeçalho no caminho selecionado, bem como com base nas regras definidas anteriormente. Com base nessas regras, ele extraiu o conteúdo que requer tradução para um novo projeto de tradução.

Para exibir o projeto de tradução:

1. Navegue até **Navegação** - e **Projetos**.
1. Toque ou clique no projeto criado na seção anterior.

![Projeto de tradução](assets/translation-project.png)

O projeto é dividido em vários cartões.

* **Resumo**  - Este cartão mostra as informações básicas do cabeçalho do projeto, incluindo o proprietário, o idioma e o provedor de tradução.
* **Tarefa de tradução**  - Esse cartão mostra uma visão geral do trabalho de tradução real, incluindo o status, o número de ativos, etc.
* **Equipe**  - Este cartão mostra os usuários que estão colaborando neste projeto de tradução. Essa jornada não abordará esse tópico.
* **Tarefas**  - Tarefas adicionais associadas à tradução do conteúdo, como fazer itens ou itens de fluxo de trabalho. Essa jornada não abordará esse tópico.

Para ver os detalhes do conteúdo sem cabeçalho incluído neste projeto:

1. Toque ou clique no botão de reticências na parte inferior do cartão **Tarefa de tradução**.
1. A janela **Tarefa de Tradução** lista todos os itens na tarefa.
   ![Detalhes do trabalho de tradução](assets/translation-job-detail.png)
1. Toque ou clique em uma linha para ver os detalhes dessa linha, tendo em mente que uma linha pode representar vários itens de conteúdo a serem traduzidos.
1. Toque ou clique na caixa de seleção de um item de linha para ver mais opções, como a opção para excluí-lo do trabalho ou exibi-lo nos consoles Fragmentos de conteúdo ou Ativos .

![Opções de trabalho de tradução](assets/translation-job-options.png)

Normalmente, o conteúdo do trabalho de tradução começa no estado **Rascunho** conforme indicado pela coluna **Estado** na janela **Tarefa de Tradução**.

Para iniciar o trabalho de tradução, volte para a visão geral do projeto de tradução e toque ou clique no botão divisa na parte superior do cartão **Tarefa de tradução** e selecione **Iniciar**.

![Iniciar trabalho de tradução](assets/start-translation-job.png)

AEM agora se comunica com sua configuração de tradução e seu conector para enviar o conteúdo para o serviço de tradução. Você pode visualizar o progresso da tradução retornando à janela **Tarefa de Tradução** e exibindo a coluna **Estado** das entradas.

![Tarefa de tradução aprovada](assets/translation-job-approved.png)

As traduções da máquina retornam automaticamente com um estado de **Approved**. A tradução humana permite mais interação, mas está além do escopo dessa jornada.

## Revisar conteúdo traduzido {#reviewing}

[Como visto anteriormente, o conteúdo traduzido por máquina do ](#using-translation-project)  retorna ao AEM com o status de  **** Aprovado , pois a suposição é que, como a tradução automática está sendo usada, nenhuma intervenção humana é necessária. No entanto, é claro que ainda é possível rever o conteúdo traduzido.

Basta ir para o trabalho de tradução concluído e selecionar um item de linha tocando ou clicando na caixa de seleção. O ícone **Revelar no Fragmento do conteúdo** é mostrado na barra de ferramentas.

![Revelar no fragmento de conteúdo](assets/reveal-in-content-fragment.png)

Toque ou clique nesse ícone para abrir o fragmento de conteúdo traduzido no console do editor para ver os detalhes do conteúdo traduzido.

![Um fragmento de conteúdo traduzido](assets/translated-content-fragment.png)

Você pode modificar ainda mais o fragmento de conteúdo, conforme necessário, desde que tenha a permissão adequada, mas a edição de fragmentos de conteúdo está além do escopo dessa jornada. Consulte a seção [Recursos adicionais](#additional-resources) no final deste documento para obter mais informações sobre este tópico.

O trabalho do projeto é coletar todos os recursos relacionados a uma tradução em um único local para facilitar o acesso e ter uma visão geral clara. No entanto, como você pode ver ao exibir os detalhes de um item traduzido, as próprias traduções fluem de volta para a pasta de ativos do idioma de tradução. Em nosso exemplo aqui

```text
/content/dam/wknd/es
```

Se você navegar para essa pasta via **Navegação** -> **Arquivos** -> **Ativos**, verá o conteúdo traduzido.

![Estrutura da pasta de conteúdo traduzida](assets/translated-file-content.png)

AEM estrutura de tradução recebe as traduções do conector de tradução e cria automaticamente a estrutura de conteúdo com base na raiz de idioma e usando as traduções fornecidas pelo conector.

É importante entender que esse conteúdo não é publicado. Ele permanece na instância de criação do AEM até que você decida que está pronto para ser publicado. Veremos como fazer isso na próxima etapa da jornada de localização.

## Tradução humana {#human-translation}

Se o seu serviço de tradução fornecer tradução humana, o processo de revisão oferecerá mais opções. Por exemplo, as traduções retornam ao projeto com o status **Rascunho** e devem ser revisadas e aprovadas ou rejeitadas manualmente.

A tradução humana está além do escopo dessa jornada de localização. Consulte a seção [Recursos adicionais](#additional-resources) no final deste documento para obter mais informações sobre este tópico.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada de localização sem cabeçalho, é necessário:

* Entenda o que é um projeto de tradução.
* Pode criar novos projetos de tradução.
* Use projetos de tradução para traduzir o conteúdo sem periféricos.

Aproveite esse conhecimento e continue sua jornada de localização sem cabeçalho AEM revisando o documento [Publicar conteúdo traduzido](publish-content.md), onde você aprenderá a publicar seu conteúdo traduzido e como atualizar essas traduções conforme o conteúdo raiz do seu idioma mudar.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de localização sem periféricos revisando o documento [Publicar conteúdo traduzido,](publish-content.md) os seguintes são alguns recursos adicionais e opcionais que fazem um mergulho mais profundo em alguns conceitos mencionados neste documento, mas eles não são solicitados a continuar com a jornada sem periféricos.

* [Gerenciamento de projetos de tradução](/help/sites-cloud/administering/translation/managing-projects.md)  - saiba mais detalhes de projetos de tradução e recursos adicionais, como fluxos de trabalho de tradução humana e projetos de vários idiomas.
