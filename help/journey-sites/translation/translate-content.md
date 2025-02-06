---
title: Traduzir conteúdo
description: Use o conector e as regras de tradução para traduzir o conteúdo.
index: true
hide: false
hidefromtoc: false
exl-id: b8ab2525-3f15-4844-866c-da47bfc7518c
solution: Experience Manager Sites
feature: Translation
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 66%

---

# Traduzir conteúdo {#translate-content}

Use o conector e as regras de tradução para traduzir o conteúdo.

## A história até agora {#story-so-far}

No documento anterior da jornada de tradução do AEM Sites, [Configurar regras de tradução](translation-rules.md), você aprendeu a usar as regras de tradução do AEM para identificar seu conteúdo de tradução. Agora você deve:

* Entenda o que as regras de tradução fazem.
* Ser capaz de definir suas próprias regras de tradução.

Agora que seu conector e regras de tradução estão configurados, este artigo o orienta através da próxima etapa da tradução de conteúdo do AEM Sites.

## Objetivo {#objective}

Este documento ajuda a entender como usar os projetos de tradução do AEM junto com o conector e suas regras de tradução para traduzir conteúdo. Depois de ler este documento, você deverá:

* Entender o que é um projeto de tradução.
* Ser capaz de criar novos projetos de tradução.
* Usar projetos de tradução para traduzir conteúdo do AEM Sites.

## Criação de um projeto de tradução {#creating-translation-project}

Os projetos de tradução permitem gerenciar a tradução de conteúdo do AEM. Um projeto de tradução reúne o conteúdo a ser traduzido em um local para permitir uma visualização centralizada do esforço de tradução.

Quando conteúdo é adicionado a um projeto de tradução, um trabalho de tradução é criado para ele. Os trabalhos fornecem comandos e informações de status que são usados para gerenciar os fluxos de trabalho de tradução humana e tradução automática que são executados nos recursos.

Projetos de tradução podem ser criados de duas formas:

1. Selecione a raiz de idioma do conteúdo e o AEM criará automaticamente o projeto de tradução com base no caminho do conteúdo.
1. Crie um projeto vazio e selecione manualmente o conteúdo a ser adicionado ao projeto de tradução

Ambas as abordagens são válidas e geralmente diferem apenas com base em quem está executando a tradução:

* O gerente de projetos de tradução (TPM) geralmente precisa da flexibilidade de selecionar manualmente o conteúdo para o projeto de tradução.
* Se o proprietário do conteúdo também for responsável pela tradução, permitir que o AEM crie o projeto automaticamente com base no caminho do conteúdo selecionado geralmente é mais fácil.

Ambas as abordagens são exploradas nas seções a seguir.

### Criação automática de um projeto de tradução com base no caminho do conteúdo {#automatically-creating}

Para proprietários de conteúdo que também são responsáveis pela tradução, geralmente é mais fácil deixar o AEM criar automaticamente o projeto de tradução. Para fazer o AEM criar automaticamente um projeto de tradução com base no caminho do conteúdo:

1. Navegue até **Navegação** > **Sites** e selecione seu projeto.
1. Localize a raiz do idioma do projeto. Por exemplo, se a raiz do idioma for inglês, `/content/<your-project>/en`.
   * Antes da primeira tradução, verifique se as outras pastas de idioma são espaços reservados vazios. Normalmente, estes são criados pelo arquiteto de conteúdo.
1. Localize a raiz do idioma do projeto.
1. Selecione o seletor do painel e exiba o painel **Referências**.
1. Selecione **Cópias de idioma**.
1. Marque a caixa de seleção **Cópias de idioma**.
1. Expanda a seção **Atualizar cópias de Idioma** na parte inferior do painel de referências.
1. Na lista suspensa **Projeto**, selecione **Criar projeto(s) de tradução**.
1. Forneça um título apropriado para o projeto de tradução.
1. Selecione **Atualizar**.

![Criar um novo projeto de tradução](assets/create-translation-project.png)

Você receberá uma mensagem informando que o projeto foi criado.

>[!NOTE]
>
>Pressupõe-se que a estrutura necessária para os idiomas das traduções já tenha sido criada como parte da [definição da sua estrutura de conteúdo](getting-started.md#content-structure). Isso deve ser feito em colaboração com o arquiteto de conteúdo.
>
>Se as pastas de idioma não forem criadas com antecedência, você não será capaz de criar cópias de idioma conforme descrito nas etapas anteriores.

### Criação manual de um projeto de tradução selecionando o conteúdo {#manually-creating}

Para gerentes de projeto de tradução, geralmente é necessário selecionar manualmente o conteúdo específico para incluir em um projeto de tradução. Para criar esse projeto de tradução manual, você deve começar criando um projeto vazio e depois selecionar o conteúdo a ser adicionado.

1. Navegue até **Navegação** > **Projetos**.
1. Selecione **Criar** > **Pasta** para criar uma pasta para seus projetos.
   * Isso é opcional, mas útil para organizar seus esforços de tradução.
1. Na janela **Criar Projeto**, adicione um **Título** para a pasta e selecione **Criar**.

   ![Criar pasta de projeto](assets/create-project-folder.png)

1. Selecione a pasta para abrir a pasta.
1. Na nova pasta do projeto, selecione **Criar** > **Projeto**.
1. Os projetos são baseados em modelos. Selecione o modelo do **Projeto de tradução** para selecioná-lo e selecione **Próximo**.

   ![Selecionar modelo de projeto de tradução](assets/select-translation-project-template.png)

1. Na guia **Básico**, digite um nome para o novo projeto.

   ![Guia Básico do projeto](assets/project-basic-tab.png)

1. Na guia **Avançado**, use a lista suspensa **Idioma de Destino** para selecionar os idiomas nos quais seu conteúdo deve ser traduzido. Selecione **Criar**.

   ![Guia Avançado do projeto](assets/project-advanced-tab.png)

1. Selecione **Abrir** no diálogo de confirmação.

   ![Caixa de diálogo de confirmação do projeto](assets/project-confirmation-dialog.png)

O projeto foi criado, mas não contém conteúdo para tradução. A próxima seção detalha como o projeto está estruturado e como adicionar conteúdo.

## Usar um projeto de tradução {#using-translation-project}

Os projetos de tradução são projetados para coletar todo o conteúdo e tarefas relacionadas a um esforço de tradução em um único local, tornando sua tradução simples e fácil de gerenciar.

Para exibir o projeto de tradução:

1. Navegue até **Navegação** > **Projetos**.
1. Selecione o projeto criado na seção anterior ([Criação automática de um projeto de tradução com base no caminho do conteúdo](#automatically-creating) ou [Criação manual de um projeto de tradução ao selecionar seu conteúdo](#manually-creating), dependendo da sua situação).

![Projeto de tradução](assets/translation-project.png)

O projeto é dividido em vários cartões.

* **Resumo** — este cartão mostra as informações básicas do cabeçalho do projeto, incluindo o proprietário, o idioma e o provedor de tradução.
* **Tarefa de tradução** - Este cartão ou estes cartões apresentam uma visão geral do trabalho de tradução real, incluindo o status, o número de ativos, etc. Geralmente, há uma tarefa por idioma com o código de idioma ISO-2 anexado ao nome da tarefa.
   * Ao [criar trabalhos de tradução automaticamente](#automatically-creating), o AEM cria os trabalhos de forma assíncrona e eles podem não aparecer imediatamente no projeto.
* **Equipe** — este cartão mostra os usuários que estão colaborando neste projeto de tradução. Essa jornada não aborda esse tópico.
* **Tarefas** — tarefas adicionais associadas à tradução do conteúdo, como itens por fazer ou itens de fluxo de trabalho. Essa jornada não aborda esse tópico.

Para entender melhor o fluxo de tradução no AEM, é útil fazer uma alteração nas configurações do projeto. Essa etapa não é necessária para traduções em produção, mas auxilia na compreensão do processo.

1. No cartão **Resumo**, selecione o botão de reticências na parte inferior do cartão.
1. Na guia **Avançado**, desmarque a opção **Excluir lançamento após promoção**.

   ![Excluir lançamento após promoção](assets/delete-launch-option.png)

1. Selecione **Salvar e fechar**.

Agora você está pronto para usar seu projeto de tradução. A forma como você usa um projeto de tradução depende de como ele foi criado: automaticamente pelo AEM ou manualmente.

### Usar um projeto de tradução criado automaticamente {#using-automatic-project}

Ao criar automaticamente o projeto de tradução, o AEM avalia o conteúdo no caminho selecionado com base nas regras de tradução definidas anteriormente. Com base nessa avaliação, ele extrai o conteúdo que requer tradução para um novo projeto de tradução.

Para ver os detalhes do conteúdo incluído neste projeto:

1. Selecione o botão de reticências na parte inferior do cartão **Tarefa de tradução**.
1. A janela **Tarefa de tradução** lista todos os itens na tarefa.

   ![Detalhes do trabalho de tradução](assets/translation-job-detail.png)

1. Selecione uma linha para ver os detalhes dela, tendo em mente que uma linha pode representar vários itens de conteúdo a serem traduzidos.
1. Marque a caixa de seleção de um item de linha para ver outras opções, como a opção para excluí-lo do trabalho ou exibi-lo no console Sites.

   ![Opções do trabalho de tradução](assets/translation-job-options.png)

Normalmente, o conteúdo do trabalho de tradução começa no estado de **Rascunho**, conforme indicado pela coluna **Estado** na janela **Tarefa de tradução**.

Para iniciar o trabalho de tradução, volte para a visão geral do projeto de tradução e selecione o botão de divisa na parte superior do cartão **Trabalho de tradução** e selecione **Iniciar**.

![Iniciar tarefa de tradução](assets/start-translation-job.png)

O AEM agora se comunica com sua configuração de tradução e conector para enviar o conteúdo para o serviço de tradução. Você pode visualizar o progresso da tradução retornando à janela **Tarefa de tradução** e exibindo a coluna **Estado** das entradas.

![Tarefa de tradução aprovada](assets/translation-job-approved.png)

As traduções automáticas retornam automaticamente com um estado de **Aprovado**. A tradução humana permite mais interação, mas está além do escopo dessa jornada.

>[!TIP]
>
>O processamento de uma tarefa de tradução pode levar algum tempo, e você pode ver seus itens de tradução moverem-se do estado de **Rascunho**, para **Tradução em andamento**, para **Pronto para revisão** antes de chegarem ao estado **Aprovado**. Isso é de se esperar.

>[!NOTE]
>
>Se você não desativou a opção de projeto **Excluir Inicialização Após Promoção** como [descrito na seção anterior](#using-translation-project), os itens traduzidos aparecerão com o estado **Excluído**. Isso é normal, pois o AEM descarta automaticamente os registros de tradução quando os itens traduzidos chegam. Os itens traduzidos foram importados como cópias de idioma. Somente os registros de tradução foram excluídos, pois não são mais necessários.
>
>Não se preocupe se isso não está claro. Este é um detalhamento aprofundado de como o AEM funciona e não afeta sua compreensão da jornada. Se quiser se aprofundar em como o AEM processa traduções, consulte a seção [recursos adicionais](#additional-resources) no final deste artigo.

### Usar um projeto de tradução criado manualmente {#using-manual-project}

Ao criar manualmente um projeto de tradução, o AEM cria as tarefas necessárias, mas não seleciona automaticamente qualquer conteúdo para incluir nessas tarefas. Isso permite que o gerente do projeto de tradução tenha flexibilidade para escolher qual conteúdo traduzir.

Para adicionar conteúdo a uma tarefa de tradução:

1. Selecione o botão de reticências na parte inferior de um dos cartões de **Tarefa de tradução**.
1. Veja se a tarefa não contém conteúdo. Selecione o botão **Adicionar** na parte superior da janela e, em seguida, **Assets/Páginas** no menu suspenso.

   ![Tarefa de tradução vazia](assets/empty-translation-job.png)

1. Um navegador de caminho é aberto, permitindo que você selecione especificamente qual conteúdo adicionar. Localize o conteúdo e selecione para seleção.

   ![Navegador de caminho](assets/path-browser.png)

1. Selecione **Selecionar** para adicionar o conteúdo selecionado ao trabalho.
1. Na caixa de diálogo **Traduzir**, especifique que deseja **Criar Cópia de Idioma**.

   ![Criar cópia de idioma](assets/translate-copy-master.png)

1. O conteúdo agora está incluído na tarefa.

   ![Conteúdo adicionado à tarefa de tradução](assets/content-added.png)

1. Marque a caixa de seleção de um item de linha para ver outras opções, como a opção para excluí-lo do trabalho ou exibi-lo no console Sites.

   ![Opções de tarefa de tradução](assets/translation-job-options.png)

1. Repita essas etapas para incluir todo o conteúdo necessário na tarefa.

>[!TIP]
>
>O navegador de caminho é uma ferramenta poderosa que permite pesquisar, filtrar e navegar pelo seu conteúdo. Selecione o botão **Somente conteúdo/Filtros** para alternar o painel lateral e revelar filtros avançados como **Data de Modificação** ou **Status da Tradução**.
>
>Você pode saber mais sobre o navegador de caminho na [seção de recursos adicionais](#additional-resources).

Você pode usar as etapas anteriores para adicionar o conteúdo necessário a todos os idiomas (tarefas) do projeto. Após selecionar todo o conteúdo, você pode iniciar a tradução.

Normalmente, o conteúdo do trabalho de tradução começa no estado de **Rascunho**, conforme indicado pela coluna **Estado** na janela **Tarefa de tradução**.

Para iniciar o trabalho de tradução, volte para a visão geral do projeto de tradução e selecione o botão de divisa na parte superior do cartão **Trabalho de tradução** e selecione **Iniciar**.

![Iniciar tarefa de tradução](assets/start-translation-job.png)

O AEM agora se comunica com sua configuração de tradução e conector para enviar o conteúdo para o serviço de tradução. Você pode visualizar o progresso da tradução retornando à janela **Tarefa de tradução** e exibindo a coluna **Estado** das entradas.

![Tarefa de tradução aprovada](assets/translation-job-approved.png)

As traduções automáticas retornam automaticamente com um estado de **Aprovado**. A tradução humana permite mais interação, mas está além do escopo dessa jornada.

>[!TIP]
>
>O processamento de uma tarefa de tradução pode levar algum tempo, e você pode ver seus itens de tradução moverem-se do estado de **Rascunho**, para **Tradução em andamento**, para **Pronto para revisão** antes de chegarem ao estado **Aprovado**. Isso é de se esperar.

>[!NOTE]
>
>Se você não desativou a opção de projeto **Excluir Inicialização Após Promoção** como [descrito na seção anterior](#using-translation-project), os itens traduzidos aparecerão com o estado **Excluído**. Isso é normal, pois o AEM descarta automaticamente os registros de tradução quando os itens traduzidos chegam. Os itens traduzidos foram importados como cópias de idioma. Somente os registros de tradução foram excluídos, pois não são mais necessários.
>
>Não se preocupe se isso não está claro. Este é um detalhamento aprofundado de como o AEM funciona e não afeta sua compreensão da jornada. Se quiser se aprofundar em como o AEM processa traduções, consulte a seção [recursos adicionais](#additional-resources) no final deste artigo.

## Revisar conteúdo traduzido {#reviewing}

[Como visto anteriormente](#using-translation-project), o conteúdo de tradução automática volta ao AEM com o status **Aprovado**, pois se presume que, devido à utilização de tradução automática, não é necessária qualquer intervenção humana. No entanto, ainda é possível revisar o conteúdo traduzido.

Basta ir até o trabalho de tradução concluído e selecionar um item da linha tocando ou clicando na caixa de seleção. O ícone **Visualizar no Sites** é exibido na barra de ferramentas.

![Revelar no Sites](assets/reveal-in-sites.png)

Selecione esse ícone para abrir o conteúdo traduzido no console e ver os detalhes dele.

![Uma página traduzida](assets/translated-page.png)

É possível modificar ainda mais o conteúdo traduzido necessário, desde que você tenha a permissão adequada; mas a edição de conteúdo está fora do escopo dessa jornada. Consulte a seção [Recursos adicionais](#additional-resources) no final deste documento para obter mais informações sobre este tópico.

O objetivo do projeto é coletar todos os recursos relacionados a uma tradução em um único local para facilitar o acesso e dar uma visão geral clara. No entanto, como você pode ver ao visualizar os detalhes de um item traduzido, as próprias traduções fluem de volta para a pasta de sites do idioma de tradução. Neste exemplo, a pasta é

```text
/content/<your-project>/es
```

Se você navegar até esta pasta por meio da **Navegação** > **Sites**, verá o conteúdo traduzido.

![Estrutura da pasta de conteúdo traduzido](assets/translated-sites-content.png)

A estrutura de tradução do AEM recebe as traduções do conector de tradução e cria automaticamente a estrutura de conteúdo, com base na raiz de idioma e usando as traduções fornecidas pelo conector.

É importante entender que esse conteúdo não foi publicado e, portanto, não está disponível para consumo. Você aprende sobre essa estrutura de criação-publicação e vê como publicar nosso conteúdo traduzido na próxima etapa da jornada de tradução.

## Tradução humana {#human-translation}

Se o seu serviço de tradução fornecer tradução humana, o processo de revisão oferecerá mais opções. Por exemplo, as traduções retornam ao projeto com o status de **Rascunho** e devem ser revisadas e aprovadas ou rejeitadas manualmente.

A tradução humana está fora do escopo dessa jornada de localização. Consulte a seção [Recursos adicionais](#additional-resources) no final deste documento para obter mais informações sobre este tópico. No entanto, além das opções de aprovação adicionais, o fluxo de trabalho para traduções humanas é o mesmo das traduções automáticas, conforme descrito nesta jornada.

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada de tradução do AEM Sites, você deve:

* Entender o que é um projeto de tradução.
* Ser capaz de criar novos projetos de tradução.
* Use projetos de tradução para traduzir o conteúdo.

Desenvolva esse conhecimento e prossiga com sua jornada de tradução do AEM Sites revisando a seguir o documento [Conteúdo traduzido do Publish](publish-content.md), no qual você aprenderá a publicar seu conteúdo traduzido e a atualizar essas traduções conforme o conteúdo da raiz do idioma mudar.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de tradução revisando o documento [Conteúdo traduzido do Publish](publish-content.md), os recursos opcionais a seguir fornecerão uma melhor explicação dos conceitos mencionados neste documento. Porém, eles não são obrigatórios para continuar na jornada.

* [Gerenciamento de projetos de tradução](/help/sites-cloud/administering/translation/managing-projects.md) - Saiba mais sobre os detalhes de projetos de tradução e recursos adicionais, como fluxos de trabalho de tradução humana e projetos multilíngues.
* [Ambiente e ferramentas de criação](/help/sites-cloud/authoring/path-selection.md#path-selection) - O AEM fornece vários mecanismos para organização e edição de conteúdo, incluindo um navegador de caminhos robusto.
