---
title: Uso do CRXDE Lite
description: O CRXDE Lite faz parte da inicialização rápida do AEM e está disponível para que você acesse e modifique o repositório em seus ambientes de desenvolvimento locais no navegador.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 1%

---

# Uso do CRXDE Lite {#using-crxde-lite}

O CRXDE Lite faz parte da inicialização rápida do AEM e está disponível para que você acesse e modifique o repositório em seus ambientes de desenvolvimento locais no navegador. Com o CRXDE Lite, você pode editar arquivos, pastas, nós e propriedades. O repositório inteiro é acessível nesta interface fácil de usar.

>[!NOTE]
>
>O CRXDE Lite só está disponível em seus ambientes de desenvolvimento locais. Não está disponível no AEM as a Cloud Service.

## Introdução ao CRXDE Lite {#getting-started-with-crxde-lite}

Para começar a usar o CRXDE Lite:

1. Inicie rapidamente o desenvolvimento local do AEM.
1. No navegador, abra a URL `https://<host>:<port>/crx/de`.
1. Digite seu **nome de usuário** e sua **senha**.
1. Clique em **OK**.

A Interface do usuário do CRXDE Lite é exibida da seguinte maneira no seu navegador:

![A interface do CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>Você também pode acessar o CRXDE Lite no menu AEM. No menu principal, selecione **Ferramentas** > **Geral** > **CRXDE Lite**.

## Visão geral da interface do usuário {#overview-of-the-user-interface}

A interface do usuário do CRXDE Lite tem muitas partes e funções.

### Barra do seletor superior {#top-switcher-bar}

A Barra do Alternador Superior permite alternar rapidamente entre o CRXDE Lite e o [Gerenciador de Pacotes](package-manager.md).

### Widget de caminho de nó {#node-path-widget}

O Widget de caminho do nó exibe o caminho para o nó atualmente selecionado.

Você também pode usá-lo para saltar para um nó, inserindo o caminho manualmente ou colando-o de outro lugar e pressionando Enter.

Também oferece suporte para procurar nós com nomes de nó específicos. Insira o nome do nó que deseja localizar e aguarde (ou selecione o ícone de pesquisa no lado direito). Se um determinado nó ou nós forem carregados no painel do explorador, a lista será exibida, e você poderá selecionar o caminho e pressionar Enter para navegar até ele. Ele só funciona para os nós atualmente carregados no aplicativo cliente CRXDE no navegador. Se quiser pesquisar todo o repositório, use **Ferramentas** -&amp;gt: **Consulta**.

### Painel do Explorer {#explorer-pane}

O **Painel do Explorer** exibe uma árvore de todos os nós no repositório.

Clique em um nó para exibir suas propriedades na guia **Propriedades**. Depois de clicar em um nó, você pode selecionar uma ação na barra de ferramentas. Clique no nó novamente para renomeá-lo.

O Filtro de Navegação em Árvore (o ícone binóculo ) permite filtrar os nós no repositório cujo nome contém o texto de entrada. Ela se aplica somente a nós que foram carregados localmente.

### Editar Painel {#edit-pane}

O **Painel de Edição** permite que você exiba o conteúdo do arquivo selecionado no momento no repositório. Cada arquivo aberto é representado como sua própria guia no painel.

A guia **Página inicial** permite pesquisar conteúdo e/ou documentação e acessar a documentação do desenvolvedor e o suporte da Adobe.

Clique duas vezes em um arquivo no **Painel do Explorer** para exibir seu conteúdo no **Painel de Edição**. Em seguida, você pode modificá-lo e salvar as alterações.

Depois que um arquivo é editado no **Painel de Edição**, as seguintes ferramentas ficam disponíveis na barra de ferramentas:

* **Mostrar na árvore** - Mostra o arquivo na árvore do repositório.
* **Pesquisar/Substituir** - Executa uma pesquisa ou substituição.

Clicar duas vezes na linha de status do **Painel de Edição** abre a caixa de diálogo **Ir para a linha** para que você possa inserir um número de linha específico.

### Guia Propriedades {#properties-tab}

A **Guia Propriedades** exibe as propriedades do nó selecionado. É possível adicionar novas propriedades ou excluir propriedades existentes.

### Guia Controle de acesso {#access-control-tab}

A **Guia de Controle de Acesso** exibe permissões com base no caminho, repositório ou entidade de segurança atual.

As permissões são divididas nas seguintes categorias.

* **Política de Controle de Acesso Aplicável** - As políticas que podem ser aplicadas à seleção atual
* **Políticas do Controle de Acesso Local** - As políticas atuais aplicadas localmente à seleção atual
* **Políticas de Controle de Acesso Efetivas** - As políticas atuais aplicadas à seleção atual, que pode ser definida localmente ou herdada dos nós pai

>[!NOTE]
>
>Para ver as informações de controle de acesso, o usuário conectado ao CRXDE Lite deve ter direitos de leitura das entradas de ACL.

### Guia Replicação {#replication-tab}

A **Guia Replicação** exibe o status de replicação do nó atual. É possível replicar e replicar e excluir o nó atual.

### Guia Console {#console-tab}

A **Guia Console** exibe mensagens de logs. Você pode configurar o nível de log, limpar o console, fixar na posição de rolagem selecionada e ativar/desativar a exibição de mensagens.

### Guia Informações da build {#build-info-tab}

A **Guia Informações da Compilação** exibe informações quando um pacote está sendo compilado.

### Botão Atualizar {#refresh-button}

O **Botão Atualizar** atualiza a seleção atual. As alterações de outros usuários são atualizadas na sua visualização do repositório. As alterações feitas não serão afetadas.

### Botão Salvar tudo {#save-all-button}

O **Botão Salvar Tudo** salva todas as alterações feitas. Até que você opte por salvar, as alterações serão temporárias e serão perdidas quando você sair do console.

* **Reverter** - Descarta todas as alterações feitas no nó selecionado desde a última ação salva e recarrega o estado atual do repositório para o nó selecionado
* **Reverter tudo** - Descarta todas as alterações feitas em todo o repositório desde a última ação de salvamento, e recarrega o estado atual do repositório

### Botão Criar {#create-button}

O **Botão Criar** é um menu suspenso para criar o seguinte no nó selecionado:

* Nó - um nó com um tipo de nó arbitrário
* Arquivo - um nó `nt:file` e seu subnó nt:resource
* Pasta - um nó `nt:folder`

### Botão Excluir {#delete-button}

O **Botão Excluir** exclui o nó selecionado.

### Botão Copiar {#copy-button}

O **Botão Copiar** copia o nó selecionado.

## Botão Colar {#paste-button}

O **Botão Colar** cola o nó copiado sob o nó selecionado.

### Botão Mover {#move-button}

O **Botão Mover** move o nó selecionado para o nó definido na caixa de diálogo.

### Renomear {#rename-button}

O **Botão Renomear** renomeia o nó selecionado.

### Mixins {#mixins-button}

O **Botão Misturas** permite adicionar tipos de mixin ao tipo de nó. Os tipos de mixin são usados principalmente para adicionar recursos avançados.

### Ferramentas {#tools-button}

O **Botão Ferramentas** é um menu suspenso com as seguintes ferramentas disponíveis:

* **Configuração do servidor** - para acessar o Felix Console (também disponível em `https://<host>:<port>/system/console/configMgr`)
* **Consulta** - para consultar o repositório
* **Privilégios** - para exibir e adicionar privilégios
* **Testar Controle de Acesso** - para testar a permissão para determinado caminho e/ou entidade de segurança
* **Exportar tipo de nó** - para exportar tipos de nó no sistema como notação CND
* **Importar Tipo de Nó** - para importar tipos de nó usando a notação CND.

### Widget de login {#login-widget}

O **Widget de logon** exibe o usuário conectado no momento.

Clique nele para fazer logon ou refazer logon como outro usuário. O `@crx.default` representa que você está no espaço de trabalho padrão (e somente) no repositório.

A opção **Preferências** pode ser usada para definir seu idioma da interface do usuário e para exibir e personalizar as teclas de atalho para várias ações, como salvar, pesquisar, criar anotação etc.

## Criação de pastas {#creating-a-folder}

Para criar uma pasta com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No painel Navegação, clique com o botão direito do mouse na pasta em que deseja criar a nova pasta, selecione **Criar...** e **Criar Pasta...**.

1. Insira a pasta **Name** e clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

## Criando um nó {#creating-a-node}

Para criar um nó com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No [**Painel do Explorer**](#explorer-pane), clique com o botão direito do mouse no nó em que deseja criar o novo nó, selecione **Criar** e **Criar Nó**.
1. Insira o **Nome** e selecione o **Tipo**.
1. Clique em **OK**.
1. Clique no [**Botão Salvar tudo**](#save-all-button) para salvar as alterações no servidor.

Agora você pode adaptar o nó às suas necessidades modificando propriedades ou criando novos nós.

>[!NOTE]
>
>A maioria das operações de edição, incluindo **Criar Nó**, mantém todas as alterações na memória e só as armazena no repositório após salvar (usando o [**Botão Salvar Tudo**](#save-all-button)). No entanto, algumas operações, como mover, são automaticamente mantidas.
>
>A validação relacionada à permissão do nó criado pelo tipo de nó do nó principal também é realizada pelo repositório ao salvar as alterações. Se você receber uma mensagem de erro ao salvar um nó, verifique se a estrutura do conteúdo é válida (por exemplo, não é possível criar um nó `nt:unstructured` como filho do nó `nt:folder`).

## Criação de uma propriedade {#creating-a-property}

Para criar uma propriedade com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No [**Painel do Explorer**](#explorer-pane), selecione o nó ao qual deseja adicionar a nova propriedade.
1. Na [**Guia Propriedades**](#properties-tab) do painel inferior, digite o **Nome**, o **Tipo** e o **Valor**.
1. Clique em **Adicionar**.
1. Clique no [**Botão Salvar tudo**](#save-all-button) para salvar as alterações no servidor.

## Criação de um arquivo {#creating-a-file}

Para criar um arquivo com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No [**Painel do Explorer**](#explorer-pane), clique com o botão direito do mouse no componente em que deseja criar o arquivo, selecione **Criar** e **Criar arquivo**.
1. Insira o arquivo **Nome**, incluindo sua extensão.
1. Clique em **OK**.
1. O novo arquivo é aberto como uma guia no [**Painel de Edição**](#edit-pane).
1. Edite o arquivo.
1. Clique no [**Botão Salvar tudo**](#save-all-button) para salvar as alterações.

## Exportando e importando tipos de nós {#exporting-and-importing-node-types}

Com o CRXDE Lite, você pode importar e/ou exportar definições de tipo de nó na [notação Compact Namespace and Node Type Definition (CND)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar uma definição de tipo de nó no CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. Selecione o nó desejado.
1. Selecione **Ferramentas** e **Exportar Tipo de Nó**.
1. A definição é exibida na notação CND em uma nova guia no navegador.
1. Salve as informações, se necessário.

Para importar uma definição de tipo de nó:

1. Abra o CRXDE Lite no navegador.
1. Selecione **Ferramentas** e **Importar Tipo de Nó**.
1. Uma nova guia é aberta no [**Painel de Edição**](#edit-pane) rotulado como **Tipo de Nó de Importação**.
1. Insira a notação CND para a definição na caixa de texto da guia **Importar Tipo de Nó**.
1. Marque **Permitir atualização** se estiver atualizando uma definição existente.
1. Clique em **Importar**.

## Logs {#logging}

Com o CRXDE Lite, você pode exibir o arquivo `error.log` que está localizado no sistema de arquivos em `<aem-install-dir>/crx-quickstart/logs` e filtrá-lo com o nível de log apropriado. Proceda da seguinte forma:

1. Abra o CRXDE Lite no navegador.
1. No menu suspenso à direita da [**Guia do Console**](#console-tab), na parte inferior da janela, selecione **Logs do Servidor**.
1. Clique no ícone **Parar** para exibir as mensagens.

É possível:

* Ajuste os parâmetros de log no Felix Console clicando no ícone **Configurações de Log**.
* Limpe as mensagens clicando no ícone **Limpar Console**.
* Fixar a mensagem na seleção atual clicando no ícone **Fixar Console**.
* Habilite ou desabilite a exibição de mensagens clicando no ícone **Parar**.
