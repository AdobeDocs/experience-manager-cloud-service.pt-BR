---
title: Gerenciamento de projetos de tradução
description: Saiba como criar e gerenciar projetos de tradução automática e humana no AEM.
feature: Language Copy
role: Admin
exl-id: dc2f3958-72b5-4ae3-a224-93d8b258bc80
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '3863'
ht-degree: 1%

---

# Gerenciamento de projetos de tradução {#managing-translation-projects}

Os projetos de tradução permitem gerenciar a tradução de AEM conteúdo. Um projeto de tradução é um tipo de AEM [projeto](/help/sites-cloud/authoring/projects/overview.md) que contém recursos a serem traduzidos para outras línguas. Esses recursos são as páginas e os ativos da variável [cópias de idioma](preparation.md) que são criados a partir do idioma principal.

>[!TIP]
>
>Se você é novo em traduzir conteúdo, consulte nosso [Jornada de tradução de sites,](/help/journey-sites/translation/overview.md) que é o caminho orientado pela tradução do conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideais para aqueles sem experiência de AEM ou tradução.

Quando os recursos são adicionados a um projeto de tradução, um trabalho de tradução é criado para eles. Os trabalhos fornecem comandos e informações de status que você usa para gerenciar os workflows de tradução humana e tradução automática que são executados nos recursos.

Os projetos de tradução são itens de longa duração, definidos por idioma e método/provedor de tradução para alinhar-se à governança organizacional para a globalização. Eles devem ser iniciados uma vez, durante a tradução inicial ou manualmente, e permanecer em vigor durante as atividades de atualização de conteúdo e tradução.

Os projetos de tradução e os trabalhos são criados com fluxos de trabalho de preparação de tradução. Esses workflows têm três opções, tanto para a tradução inicial (Criar e traduzir) quanto para as atualizações (Atualizar tradução):

1. [Criar novo projeto](#creating-translation-projects-using-the-references-panel)
1. [Adicionar ao projeto existente](#adding-pages-to-a-translation-project)
1. [Somente a estrutura de conteúdo](#creating-the-structure-of-a-language-copy)

O AEM detecta se um projeto de tradução está sendo criado para a tradução inicial do conteúdo ou para atualizar cópias de idioma já traduzidas. Ao criar um projeto de tradução para uma página e indicar as cópias de idioma para as quais você está traduzindo, o AEM detecta se a página de origem já existe nas cópias de idioma direcionado:

* **A cópia de idioma não inclui a página:** AEM trata essa situação como a tradução inicial. A página é copiada imediatamente para a cópia de idioma e incluída no projeto. Quando a página traduzida é importada para o AEM, o AEM a copia diretamente para a cópia de idioma.
* **A cópia de idioma já inclui a página:** AEM trata essa situação como uma tradução atualizada. Um lançamento é criado e uma cópia da página é adicionada ao lançamento e incluída no projeto. Lançamentos permitem que você revise as traduções atualizadas antes de confirmá-las na cópia de idioma:

   * Quando a página traduzida é importada para o AEM, ela substitui a página na inicialização.
   * A página traduzida substitui a cópia de idioma somente quando o lançamento é promovido.

Por exemplo, a variável `/content/wknd/fr` a raiz do idioma é criada para a tradução em francês do `/content/wknd/en` Idioma principal. Não há outras páginas na cópia em francês.

* Um projeto de tradução é criado para o `/content/wknd/en/products` página e todas as páginas filhas, direcionando a cópia em francês. Porque a cópia de idioma não inclui a variável `/content/wknd/fr/products` AEM copia imediatamente a página `/content/wknd/en/products` e todas as páginas secundárias na cópia em francês. As cópias também são incluídas no projeto de tradução.
* Um projeto de tradução é criado para o `/content/wknd/en` página e todas as páginas filhas, direcionando a cópia em francês. Como a cópia de idioma inclui a página que corresponde ao `/content/wknd/en` página (a raiz do idioma), AEM copia a variável `/content/wknd/en` e todas as páginas filhas e as adiciona a um lançamento. As cópias também são incluídas no projeto de tradução.

## Tradução do console Sites {#performing-initial-translations-and-updating-existing-translations}

Os projetos de tradução podem ser criados ou atualizados diretamente do console de sites.

### Criação de projetos de tradução usando o painel Referências {#creating-translation-projects-using-the-references-panel}

Crie projetos de tradução para que você possa executar e gerenciar o fluxo de trabalho para traduzir os recursos do seu idioma principal. Ao criar projetos, você especifica a página no idioma principal que está traduzindo e as cópias de idioma para as quais está executando a tradução:

* A configuração de nuvem da estrutura de integração de tradução associada à página selecionada determina muitas propriedades dos projetos de tradução, como o fluxo de trabalho de tradução a ser usado.
* Um projeto é criado para cada cópia de idioma selecionada.
* Uma cópia da página selecionada e dos ativos associados é criada e adicionada a cada projeto. Essas cópias são enviadas posteriormente para o provedor de tradução para tradução.

Você pode especificar que as páginas filhas da página selecionada também sejam selecionadas. Nesse caso, cópias das páginas filhas também são adicionadas a cada projeto para serem traduzidas. Quando qualquer página filho é associada a diferentes configurações da estrutura de integração de tradução, o AEM cria projetos adicionais.

Você também pode [criar projetos de tradução manualmente](#creating-a-translation-project-using-the-projects-console).

>[!NOTE]
>
>Para criar um projeto, sua conta deve ser membro do `project-administrators` grupo.

### Traduções iniciais e atualização de traduções {#initial-and-updating}

O painel Referências indica se você está atualizando cópias de idioma existentes ou criando a primeira versão das cópias de idioma. Quando existe uma cópia de idioma para a página selecionada, a guia Atualizar Cópias de idioma aparece para fornecer acesso aos comandos relacionados ao projeto.

![Atualizar cópias de idioma](../assets/update-language-copies.png)

Depois de traduzir, você pode [revisar a tradução](#reviewing-and-promoting-updated-content) antes de substituir a cópia de idioma por ela. Quando não existe uma cópia de idioma para a página selecionada, a guia Criar e traduzir aparece para fornecer acesso aos comandos relacionados ao projeto.

![Criar e traduzir](../assets/create-and-translate.png)

### Criar projetos de tradução para uma nova cópia de idioma {#create-translation-projects-for-a-new-language-copy}

1. Use o console Sites para selecionar a página que você está adicionando aos projetos de tradução.

1. Na barra de ferramentas, abra o **Referências** trilho.

   ![Referências](../assets/references.png)

1. Selecionar **Cópias de idioma** e, em seguida, selecione as cópias de idioma para as quais você está traduzindo as páginas de origem.
1. Clique ou toque em **Criar e traduzir** e configure o trabalho de tradução:

   * Use o **Languages** para selecionar uma cópia de idioma para a qual deseja traduzir. Selecione idiomas adicionais, conforme necessário. Os idiomas exibidos na lista correspondem à variável [raízes de idioma criadas por você](preparation.md#creating-a-language-root).
      * Selecionar vários idiomas cria um projeto com um trabalho de tradução para cada idioma.
   * Para traduzir a página selecionada e todas as páginas filhas, selecione **Selecionar todas as subpáginas**. Para traduzir apenas a página selecionada, desmarque a opção .
   * Para **Projeto**, selecione **Criar projeto(s) de tradução**.
   * Opcionalmente para **Projeto Principal**, selecione um projeto do qual herdar funções e permissões de usuário.
   * Em **Título** digite um nome para o projeto.

   ![Criar projeto de tradução](../assets/create-translation-project.png)

1. Clique ou toque em **Criar**.

### Criar projetos de tradução para uma cópia de idioma existente {#create-translation-projects-for-an-existing-language-copy}

1. Use o console Sites para selecionar a página que você está adicionando aos projetos de tradução.

1. Na barra de ferramentas, abra o **Referências** trilho.

   ![Referências](../assets/references.png)

1. Selecionar **Cópias de idioma** e, em seguida, selecione as cópias de idioma para as quais você está traduzindo as páginas de origem.
1. Clique ou toque em **Atualizar Cópias de Idioma** e configure o trabalho de tradução:

   * Para traduzir a página selecionada e todas as páginas filhas, selecione **Selecionar todas as subpáginas**. Para traduzir apenas a página selecionada, desmarque a opção .
   * Para **Projeto**, selecione **Criar projeto(s) de tradução**.
   * Opcionalmente para **Projeto Principal**, selecione um projeto do qual herdar funções e permissões de usuário.
   * Em **Título** digite um nome para o projeto.

   ![Criar projeto para atualizar cópias de idioma](../assets/create-update-language-copies-project.png)

1. Clique ou toque em **Criar**.

### Adicionar páginas a um projeto de tradução {#adding-pages-to-a-translation-project}

Depois de criar um projeto de tradução, você pode usar a variável **Recursos** painel para adicionar páginas ao projeto. Adicionar páginas é útil quando você está incluindo páginas de diferentes ramificações no mesmo projeto.

Quando você adiciona páginas a um projeto de tradução, as páginas são incluídas em um novo trabalho de tradução. Você também pode [adicionar páginas a um trabalho existente](#adding-pages-assets-to-a-translation-job).

Assim como ao criar um novo projeto, ao adicionar páginas, cópias das páginas são adicionadas a um lançamento quando necessário para evitar a substituição de cópias de idioma existentes. (Consulte [Criação de projetos de tradução para cópias de idioma existentes](#performing-initial-translations-and-updating-existing-translations).)

1. Use o console Sites para selecionar a página que você está adicionando ao projeto de tradução.

1. Na barra de ferramentas, abra o **Referências** trilho.

   ![Referências](../assets/references.png)

1. Selecionar **Cópias de idioma** e, em seguida, selecione as cópias de idioma para as quais você está traduzindo as páginas de origem.

   ![Atualizar cópias de idioma do painel de referências](../assets/update-language-copies-references.png)

1. Clique ou toque em **Atualizar Cópias de Idioma** e configure as propriedades:

   * Para traduzir a página selecionada e todas as páginas filhas, selecione **Selecionar todas as subpáginas**. Para traduzir apenas a página selecionada, desmarque a opção .
   * Para **Projeto**, selecione **Adicionar ao projeto de tradução existente**.
   * Selecione o projeto em **Projeto de tradução existente**.

   >[!NOTE]
   >
   >O idioma de destino definido no projeto de tradução deve corresponder ao caminho da cópia de idioma, como mostrado no painel de referências.

1. Clique ou toque em **Atualizar**.

### Criar a estrutura de uma cópia de idioma {#creating-the-structure-of-a-language-copy}

É possível criar apenas a estrutura da cópia de idioma, permitindo copiar o conteúdo e as alterações estruturais no idioma principal às cópias de idioma (não traduzidas). Isso não está relacionado a um trabalho ou projeto de tradução. Você pode usar isso para manter seus mestres em sincronia, mesmo sem tradução.

Preencha sua cópia de idioma para que ela contenha conteúdo do idioma principal que você está traduzindo. Antes de preencher a cópia de idioma, é necessário ter [criado a raiz de idioma](preparation.md#creating-a-language-root) da cópia do idioma.

1. Use o console Sites para selecionar a raiz do idioma do idioma principal que você está usando como a fonte.
1. Abra o painel de referências clicando ou tocando em **Referências** na barra de ferramentas.

   ![Referências](../assets/references.png)

1. Selecionar **Cópias de idioma** e, em seguida, selecione as cópias de idioma que deseja preencher.

   ![Selecionar cópias de idioma](../assets/language-copy-structure-select.png)

1. Clique ou toque em **Atualizar Cópias de Idioma** para revelar as ferramentas de tradução e configurar as propriedades:

   * Selecione o **Selecionar todas as subpáginas** opção.
   * Para **Projeto**, selecione **Criar apenas estrutura**.

   ![Somente estrutura](../assets/language-copy-structure-only.png)

1. Clique ou toque em **Atualizar**.

### Atualizando a memória de tradução {#updating-translation-memory}

As edições manuais de conteúdo traduzido podem ser sincronizadas de volta ao Sistema de Gerenciamento de Tradução (TMS) para treinar sua Memória de Tradução.

1. No console Sites, depois de atualizar o conteúdo do texto em uma página traduzida, selecione **Atualizar memória de tradução**.
1. Uma exibição de lista mostra uma comparação lado a lado da origem e da tradução para cada componente de texto que foi editado. Selecione quais atualizações de tradução devem ser sincronizadas com a memória de tradução e selecione **Atualizar memória**.

![Comparar alterações da memória de tradução](../assets/update-translation-memory-compare.png)

AEM enviará as cadeias de caracteres selecionadas de volta para o Sistema de gerenciamento de tradução.

### Verificar o status de tradução de uma página {#check-translation-status}

Uma propriedade pode ser selecionada na exibição de lista do console de sites que mostra se uma página foi traduzida, está na tradução ou ainda não foi traduzida.

1. No console do site, alterne para [exibição em lista.](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. Toque ou clique em, **Exibir configurações** no menu suspenso exibição .
1. Na caixa de diálogo , marque a opção **Traduzido** e toque ou clique **Atualizar**.

O console Sites agora exibe a variável **Traduzido** coluna mostrando o status de tradução das páginas listadas.

![Status da tradução na exibição de lista](../assets/translation-status-list-view.png)

## Gerenciamento de projetos de tradução no Console do projeto

Muitas tarefas de tradução e opções avançadas podem ser acessadas no console Projetos .

### Noções básicas sobre o console Projetos

Os projetos de tradução em AEM usam o padrão [AEM console projetos .](/help/sites-cloud/authoring/projects/overview.md) Se você não estiver familiarizado com AEM projetos, revise essa documentação.

Como qualquer outro projeto, um projeto de tradução é composto de blocos que apresentam uma visão geral das tarefas do projeto.

![Projeto de tradução](../assets/translation-project.png)

* **Resumo** - Uma visão geral do projeto
* **Tarefas** - Uma ou mais tarefas de tradução
* **Equipe** - Usuários colaborando no projeto de tradução
* **Tarefas** - Itens que precisam ser preenchidos como parte do esforço de tradução

Use os comandos e botões de reticências na parte superior e inferior dos blocos (respectivamente) para acessar controles e opções para os vários blocos.

![Botão Comandos](../assets/context.png)

![Botão Elipsis](../assets/ellipsis.png)

### Criação de um projeto de tradução usando o console Projetos {#creating-a-translation-project-using-the-projects-console}

Você pode criar manualmente um projeto de tradução se preferir usar o console de projetos em vez do console de sites.

>[!NOTE]
>
>Para criar um projeto, sua conta deve ser membro do `project-administrators` grupo.

Ao criar manualmente um projeto de tradução, você deve fornecer valores para as seguintes propriedades relacionadas à tradução, além da variável [propriedades básicas](/help/sites-cloud/authoring/projects/managing.md#creating-a-project):

* **Nome:** Nome do projeto
* **Idioma de Origem:** O idioma do conteúdo de origem
* **Idioma de Destino:** O idioma ou idiomas em que o conteúdo está sendo traduzido
   * Se vários idiomas forem selecionados, uma tarefa será criada para cada idioma no projeto.
* **Método de tradução:** Selecionar **Tradução humana** para indicar que a tradução deve ser executada manualmente.

1. Na barra de ferramentas do console de projetos, clique ou toque em **Criar**.
1. Selecione o **Projeto de tradução** modelo e, em seguida, clique ou toque em **Próximo**.
1. Insira valores para o **Básico** guia de propriedades.
1. Clique ou toque em **Avançado** e fornecer valores para as propriedades relacionadas à tradução.
1. Clique ou toque em **Criar**. Na caixa de confirmação, clique ou toque em **Concluído** para retornar ao console projetos ou clique ou toque em **Abrir projeto** para abrir e começar a gerenciar o projeto.

### Adicionar páginas e ativos a um trabalho de tradução {#adding-pages-assets-to-a-translation-job}

Você pode adicionar páginas, ativos ou tags ao trabalho de tradução do seu projeto de tradução. Para adicionar páginas ou ativos:

1. Na parte inferior do bloco do trabalho de tradução do seu projeto de tradução, clique ou toque nas reticências.

   ![Mosaico de trabalho de tradução](../assets/translation-job.png)

1. Na próxima janela, clique ou toque no botão **Adicionar** na barra de ferramentas e selecione **Ativos/páginas**.

   ![Adicionar páginas](../assets/add-to-project.png)

1. Na janela modal, selecione o item na extremidade superior da ramificação que deseja adicionar e clique ou toque no ícone de marca de seleção. A seleção múltipla está ativada nesta janela.

   ![Selecionar páginas](../assets/select-pages.png)

1. Como alternativa, você pode selecionar o ícone de pesquisa para procurar facilmente páginas ou ativos que deseja adicionar ao seu trabalho de tradução.

   ![Pesquisar conteúdo](../assets/search-for-content.png)

1. Depois de selecionado, toque ou clique em **Selecionar**. Suas páginas e/ou ativos são adicionados ao trabalho de tradução.

>[!TIP]
>
>Esse método adiciona páginas/ativos e seus filhos ao projeto. Selecionar **Ativo/Página (sem filhos)** se você quiser apenas adicionar os pais.

### Adicionar tags a um trabalho de tradução {#adding-tags-to-a-translation-job}

Você pode adicionar tags a um projeto de tradução semelhante a [como adicionar ativos e páginas a um projeto.](#adding-pages-assets-to-a-translation-job) Basta selecionar **Tags** nos termos do **Adicionar** em seguida, siga as mesmas etapas.

### Visualizar detalhes do projeto de tradução {#seeing-translation-project-details}

As propriedades do projeto de tradução são acessíveis por meio do botão de reticências do bloco de resumo do projeto. Além do genérico [informações do projeto](/help/sites-cloud/authoring/projects/overview.md#project-info), as propriedades do projeto de tradução contêm traduções específicas.

No seu projeto de tradução, clique ou toque nas reticências na parte inferior do bloco Resumo da tradução . A maioria das propriedades específicas do projeto está no **Avançado** guia .

* **Idioma de Origem:** O idioma das páginas que estão sendo traduzidas
* **Idioma de Destino:** O idioma ou os idiomas em que as páginas estão sendo traduzidas
* **Configuração na nuvem:** A configuração de nuvem do conector do serviço de tradução usado para o projeto
* **Método de tradução:** O fluxo de trabalho de tradução, **Tradução humana** ou **Tradução Automática**
* **Provedor de Tradução:** O provedor de serviços de tradução que está executando a tradução
* **Categoria de conteúdo:** (Tradução automática) A categoria de conteúdo usada para tradução
* **Credencial do Provedor de Tradução:** As credenciais para entrar no provedor
* **Promover automaticamente inicializações de tradução:** Depois de receber conteúdo traduzido, as inicializações de tradução são promovidas automaticamente
   * **Excluir lançamento após promoção:** Se as inicializações de tradução forem promovidas automaticamente, exclua a inicialização após a promoção
* **Aprovar traduções automaticamente:** Depois de receber conteúdo traduzido, as tarefas de tradução são aprovadas automaticamente
* **Repetir tradução:** Configure a execução recorrente de um projeto de tradução selecionando a frequência com que o projeto criará e executará automaticamente os trabalhos de tradução

Quando um projeto é criado usando o painel de referências de uma página, essas propriedades são configuradas automaticamente com base nas propriedades da página de origem.

![Propriedades do projeto de tradução](../assets/translation-project-properties.png)

### Monitorar o status de um trabalho de tradução {#monitoring-the-status-of-a-translation-job}

O bloco de trabalho de tradução de um projeto de tradução fornece o status de um trabalho de tradução, bem como o número de páginas e ativos no trabalho.

![Trabalho de tradução](../assets/translation-job.png)

A tabela a seguir descreve cada status que uma ordem de produção ou um item na ordem de produção pode ter:

| Status | Descrição |
|---|---|
| **Rascunho** | O trabalho de tradução não foi iniciado. Os trabalhos de tradução estão em **Rascunho**** status ao serem criadas. |
| **Enviado** | Os arquivos no trabalho de tradução têm esse status quando foram enviados com êxito para o serviço de tradução. Esse status pode ocorrer após a **Escopo da Solicitação** ou o **Iniciar** é emitido. |
| **Escopo solicitado** | Para o fluxo de trabalho de tradução humana, os arquivos no trabalho foram enviados ao fornecedor de tradução para escopo. Este status aparece após a **Escopo da Solicitação** é emitido. |
| **Escopo concluído** | O fornecedor esticou o trabalho de tradução. |
| **Autorizado para tradução** | O proprietário do projeto aceitou o escopo. Esse status indica que o fornecedor de tradução deve começar a traduzir os arquivos na tarefa. |
| **Tradução Em Andamento** | Para uma tarefa, a tradução de um ou mais arquivos na tarefa ainda não foi concluída. Para um item na tarefa, o item está sendo traduzido. |
| **Traduzido** | Para uma tarefa, a tradução de todos os ficheiros na tarefa está concluída. Para um item na tarefa, o item é traduzido. |
| **Pronto Para Revisão** | O item na tarefa é traduzido e o arquivo foi importado para o AEM. |
| **Concluir** | O proprietário do projeto indicou que o contrato de tradução está concluído. |
| **Cancelar** | Indica que o fornecedor de tradução deve parar de trabalhar em um trabalho de tradução. |
| **Atualização de erro** | Ocorreu um erro ao transferir ficheiros entre o AEM e o serviço de tradução. |
| **Estado desconhecido** | Ocorreu um erro desconhecido. |

Para ver o status de cada arquivo no trabalho, clique ou toque nas reticências na parte inferior do bloco.

### Definir a data de vencimento dos trabalhos de tradução {#setting-the-due-date-of-translation-jobs}

Especifique a data antes da qual seu fornecedor de tradução precisa retornar os arquivos traduzidos. A configuração da data de vencimento funciona corretamente somente quando o fornecedor de tradução que você está usando suporta esse recurso.

1. Clique ou toque nas reticências na parte inferior do bloco do resumo de tradução.

   ![Mosaico de resumo da tradução](../assets/translation-summary-tile.png)

1. No **Básico** , use o seletor de datas do **Data de vencimento** para selecionar a data de vencimento.

   ![Propriedades do projeto de tradução](../assets/translation-project-properties-basic.png)

1. Clique ou toque em **Salvar e fechar**.

### Escopo de um trabalho de tradução {#scoping-a-translation-job}

Escopo um trabalho de tradução para obter uma estimativa do custo da tradução do seu provedor de serviços de tradução. Quando você faz um escopo de um trabalho, os arquivos de origem são enviados ao fornecedor da tradução que compara o texto ao pool de traduções armazenadas (memória de tradução). Normalmente, o escopo é o número de palavras que exigem tradução.

Para obter mais informações sobre os resultados do escopo, entre em contato com seu fornecedor de tradução.

>[!NOTE]
>
>O escopo é opcional e se aplica somente à tradução humana. Você pode iniciar um trabalho de tradução sem escopo.

Quando você cria escopo de um trabalho de tradução, o status do trabalho é **Escopo solicitado**. Quando o fornecedor de tradução retorna o escopo, o status é alterado para **Escopo Concluído**. Quando o escopo for concluído, você poderá usar a variável **Mostrar Escopo** para analisar os resultados do escopo.

O escopo funciona corretamente somente quando o fornecedor de tradução que você está usando suporta esse recurso.

1. No console Projetos , abra o projeto de tradução.
1. No título do trabalho de tradução, toque ou clique no menu de comandos e, em seguida, toque ou clique em **Escopo da Solicitação**.
1. Quando o status do trabalho for alterado para **Escopo Concluído**, clique ou toque no menu de comandos e, em seguida, clique ou toque em **Mostrar Escopo**.

### Iniciando trabalhos de tradução {#starting-translation-jobs}

Inicie um trabalho de tradução para traduzir as páginas de origem para o idioma de destino. A tradução é executada de acordo com os valores de propriedade do bloco resumo de tradução.

Você pode iniciar um trabalho individual dentro do projeto.

1. No console Projetos , abra o projeto de tradução.
1. No bloco do trabalho de tradução, clique ou toque no menu de comandos e, em seguida, clique ou toque em **Iniciar**.
1. Na caixa de diálogo de ação que confirma o início da tradução, clique ou toque em **Fechar**.

Depois de iniciar o trabalho de tradução, o bloco de trabalho de tradução mostra a tradução em **Em Andamento** status.

Você também pode iniciar todos os trabalhos de tradução de um projeto.

1. No console do projeto, selecione o projeto de tradução.
1. Na barra de ferramentas, toque ou clique em **Iniciar trabalho de tradução**.
1. Na caixa de diálogo, revise a lista de tarefas que serão iniciadas e confirme com **Iniciar** ou abortar com **Cancelar**.

### Cancelar um trabalho de tradução {#canceling-a-translation-job}

Cancele um trabalho de tradução para interromper o processo de tradução e impedir que o fornecedor de tradução execute mais traduções. Você pode cancelar um trabalho quando ele tiver o valor **Autorizado para tradução** ou **Tradução Em Andamento** status.

1. No console Projetos , abra o projeto de tradução.
1. No bloco do trabalho de tradução, clique ou toque no menu de comandos e, em seguida, clique ou toque em **Cancelar**.
1. Na caixa de diálogo de ação que confirma o cancelamento da tradução, clique ou toque em **OK**.

### Aceitar e Rejeitar Fluxo de Trabalho {#accept-reject-workflow}

Quando o conteúdo volta após a tradução e está em **Pronto para revisão** , você pode acessar o trabalho de tradução e aceitar/rejeitar o conteúdo.

Se você selecionar **Rejeitar tradução**, você tem a opção de adicionar um comentário.

Rejeitar o conteúdo o envia de volta ao fornecedor de tradução, onde ele poderá ver o comentário.

### Concluir e arquivar trabalhos de tradução {#completing-and-archiving-translation-jobs}

Conclua um trabalho de tradução depois de ter revisado os arquivos traduzidos do fornecedor.

1. No console Projetos , abra o projeto de tradução.
1. No bloco do trabalho de tradução, clique ou toque no menu de comandos e, em seguida, clique ou toque em **Concluído**.
1. O trabalho agora tem o status **Concluído**.

Para fluxos de trabalho de tradução humana, concluir uma tradução indica ao fornecedor que o contrato de tradução foi cumprido e que ele deve salvar a tradução na sua memória de tradução.

Arquive um trabalho de tradução depois que ele estiver concluído e não será mais necessário ver os detalhes do status do trabalho.

1. No console Projetos , abra o projeto de tradução.
1. No bloco do trabalho de tradução, clique ou toque no menu de comandos e, em seguida, clique ou toque em **Arquivar**.

Ao arquivar o trabalho, o bloco de trabalho de tradução é removido do projeto.

## Revisar e usar conteúdo traduzido {#reviewing-and-promoting-updated-content}

Você pode usar o console Sites para revisar o conteúdo, comparar cópias de idioma e ativar o conteúdo.

### Promover conteúdo atualizado {#promoting-updated-content}

Quando o conteúdo é traduzido para uma cópia de idioma existente, revise as traduções, faça alterações se necessário e promova as traduções para movê-lo para a cópia de idioma. Você pode revisar arquivos traduzidos quando o trabalho de tradução mostrar a variável **Pronto Para Revisão** status.

![Trabalho pronto para revisão](../assets/job-ready-for-review.png)

1. Selecione a página no idioma principal, clique ou toque em **Referências**, em seguida, clique ou toque em **Cópias de idioma**.
1. Clique ou toque na cópia de idioma para revisar.

   ![Cópia de idioma pronta para revisão](../assets/language-copy-ready-for-review.png)

1. Clique ou toque em **Launch** para revelar os comandos relacionados ao launch.

   ![Início](../assets/language-copy-launch.png)

1. Para abrir a cópia de lançamento da página para revisar e editar o conteúdo, clique em **Abrir página**.
1. Após ter revisado o conteúdo e feito as alterações necessárias, para promover o clique na cópia de lançamento **Promover**.
1. No **Promover lançamento** especifique quais páginas serão promovidas e clique ou toque em **Promover**.

### Comparação de cópias de idioma {#comparing-language-copies}

Para comparar cópias de idioma ao idioma principal:

1. No console Sites, navegue até a cópia de idioma que deseja comparar.
1. Abra o [Trilho de referências.](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)
1. Em **Cópias** seleção de cabeçalho **Cópias de idioma.**
1. Selecione a cópia de idioma específica e, em seguida, clique em **Comparar ao Principal** ou **Comparar com anterior** se aplicável.

   ![Comparar cópias de idioma](../assets/language-copy-compare.png)

1. As duas páginas (lançamento e origem) serão abertas lado a lado.
   * Para obter informações completas sobre como usar esse recurso, consulte [Diferencial de página](/help/sites-cloud/authoring/features/page-diff.md).

## Importar e exportar trabalhos de tradução {#import-export}

Embora o AEM ofereça várias soluções e interfaces de tradução, também é possível importar e exportar as informações do trabalho de tradução manualmente.

### Exportar um trabalho de tradução {#exporting-a-translation-job}

Você pode baixar o conteúdo de um trabalho de tradução, por exemplo, para enviar a um provedor de tradução que não esteja integrado ao AEM por meio de um conector ou para revisar o conteúdo.

1. No menu suspenso do bloco do trabalho de tradução, clique ou toque em **Exportar**.
1. Na caixa de diálogo, clique ou toque em **Baixar arquivo exportado** e, se necessário, use a caixa de diálogo do navegador da Web para salvar o arquivo.
1. Na caixa de diálogo, clique ou toque em **Fechar**.

### Importar um trabalho de tradução {#importing-a-translation-job}

Você pode importar conteúdo traduzido para o AEM, por exemplo, quando seu provedor de tradução o envia para você porque não está integrado ao AEM por meio de um conector.

1. No menu suspenso do bloco do trabalho de tradução, clique ou toque em **Importar**.
1. Use a caixa de diálogo do navegador da Web para selecionar o arquivo a ser importado.
1. Na caixa de diálogo, clique ou toque em **Fechar**.
