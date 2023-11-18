---
title: Uso do CRXDE Lite
description: o CRXDE Lite faz parte do AEM quickstart e está disponível para você acessar e modificar o repositório em seus ambientes de desenvolvimento locais no navegador.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 1%

---

# Uso do CRXDE Lite {#using-crxde-lite}

o CRXDE Lite faz parte do AEM quickstart e está disponível para você acessar e modificar o repositório em seus ambientes de desenvolvimento locais no navegador. Com o CRXDE Lite, é possível editar arquivos, pastas, nós e propriedades. O repositório inteiro é acessível nesta interface fácil de usar.

>[!NOTE]
>
>O CRXDE Lite só está disponível em seus ambientes de desenvolvimento locais. Não está disponível no AEM as a Cloud Service.

## Introdução ao CRXDE Lite {#getting-started-with-crxde-lite}

Para começar a usar o CRXDE Lite:

1. Inicie rapidamente o desenvolvimento local do AEM.
1. No navegador, abra o URL `https://<host>:<port>/crx/de`.
1. Insira seu **nome de usuário** e **senha**.
1. Clique em **OK**.

A interface do usuário do CRXDE Lite é exibida da seguinte maneira no seu navegador:

![A interface do CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>Você também pode acessar o CRXDE Lite no menu AEM. No menu principal, selecione **Ferramentas** > **Geral** > **CRXDE Lite**.

## Visão geral da interface do usuário {#overview-of-the-user-interface}

A interface de usuário do CRXDE Lite tem muitas partes e muitas funções.

### Barra do seletor superior {#top-switcher-bar}

A barra superior do alternador permite alternar rapidamente entre o CRXDE Lite e [Gerenciador de pacotes.](package-manager.md)

### Widget de caminho de nó {#node-path-widget}

O Widget de caminho do nó exibe o caminho para o nó atualmente selecionado.

Você também pode usá-lo para saltar para um nó, inserindo o caminho manualmente ou colando-o de outro lugar e pressionando Enter.

Também oferece suporte para procurar nós com nomes de nó específicos. Insira o nome do nó que deseja localizar e aguarde (ou selecione o ícone de pesquisa no lado direito). Se um determinado nó ou nós forem carregados no painel do explorador, a lista será exibida, e você poderá selecionar o caminho e pressionar Enter para navegar até ele. Observe que isso só funciona para os nós atualmente carregados no aplicativo cliente CRXDE no navegador. Se quiser pesquisar todo o repositório, use **Ferramentas** ->: **Query**.

### Painel do Explorer {#explorer-pane}

A variável **Painel do Explorer** exibe uma árvore de todos os nós no repositório.

Clique em um nó para exibir suas propriedades na **Propriedades** guia. Depois de clicar em um nó, você pode selecionar uma ação na barra de ferramentas. Clique no nó novamente para renomeá-lo.

O Filtro de Navegação em Árvore (o ícone binóculo ) permite filtrar os nós no repositório cujo nome contém o texto de entrada. Ela se aplica somente a nós que foram carregados localmente.

### Editar Painel {#edit-pane}

A variável **Editar Painel** permite visualizar o conteúdo do arquivo selecionado no momento no repositório. Cada arquivo aberto é representado como sua própria guia no painel.

A variável **Início** A guia permite pesquisar conteúdo e/ou documentação e acessar a documentação do desenvolvedor e o suporte ao Adobe.

Clique duas vezes em um arquivo na **Painel do Explorer** para exibir seu conteúdo no **Editar Painel**. Em seguida, você pode modificá-lo e salvar as alterações.

Quando um arquivo for editado na variável **Editar Painel**, as seguintes ferramentas estão disponíveis na barra de ferramentas:

* **Mostrar na árvore** - Mostra o arquivo na árvore do repositório.
* **Pesquisar/substituir** - Executa uma pesquisa ou substituição.

Clique duas vezes na linha de status da **Editar Painel** abre o **Ir para a linha** para que você possa inserir um número de linha específico.

### Guia Propriedades {#properties-tab}

A variável **Guia Propriedades** exibe as propriedades do nó selecionado. É possível adicionar novas propriedades ou excluir propriedades existentes.

### Guia Controle de acesso {#access-control-tab}

A variável **Guia Controle de acesso** exibe permissões com base no caminho, repositório ou principal atual.

As permissões são divididas nas seguintes categorias.

* **Política do controle de acesso aplicável** - As políticas que podem ser aplicadas à seleção atual
* **Políticas do controle de acesso local** - As políticas atuais aplicadas localmente à seleção atual
* **Políticas do controle de acesso efetivo** - As políticas atuais aplicadas para a seleção atual, que pode ser definida localmente ou herdada dos nós principais

>[!NOTE]
>
Para ver as informações de controle de acesso, o usuário conectado ao CRXDE Lite deve ter direitos de leitura das entradas de ACL.

### Guia Replicação {#replication-tab}

A variável **Guia Replicação** exibe o status de replicação do nó atual. É possível replicar e replicar e excluir o nó atual.

### Guia Console {#console-tab}

A variável **Guia Console** exibe mensagens de logs. Você pode configurar o nível de log, limpar o console, fixar na posição de rolagem selecionada e ativar/desativar a exibição de mensagens.

### Guia Informações da build {#build-info-tab}

A variável **Guia Informações da build** exibe informações quando um pacote está sendo criado.

### Botão Atualizar {#refresh-button}

A variável **Botão Atualizar** atualiza a seleção atual. As alterações de outros usuários são atualizadas na sua visualização do repositório. As alterações feitas não serão afetadas.

### Botão Salvar tudo {#save-all-button}

A variável **Botão Salvar tudo** O salva todas as alterações feitas. Até que você opte por salvar, as alterações serão temporárias e serão perdidas quando você sair do console.

* **Reverter** - Descarta todas as alterações feitas no nó selecionado desde a última ação salva e, em seguida, recarrega o estado atual do repositório para o nó selecionado
* **Reverter tudo** - Descarta todas as alterações feitas em todo o repositório desde a última ação de salvamento e, em seguida, recarrega o estado atual do repositório

### Botão Criar {#create-button}

A variável **Botão Criar** é um menu suspenso para criar o seguinte no nó selecionado:

* Nó - um nó com um tipo de nó arbitrário
* Arquivo - um `nt:file` nó e seu subnó nt:resource
* Pasta - um `nt:folder` nó

### Botão Excluir {#delete-button}

A variável **Botão Excluir** exclui o nó selecionado.

### Botão Copiar {#copy-button}

A variável **Botão Copiar** copia o nó selecionado.

## Botão Colar {#paste-button}

A variável **Botão Colar** cola o nó copiado sob o nó selecionado.

### Botão Mover {#move-button}

A variável **Botão Mover** move o nó selecionado para o nó definido pela caixa de diálogo.

### Renomear {#rename-button}

A variável **Botão Renomear** renomeia o nó selecionado.

### Misturas {#mixins-button}

A variável **Botão Misturas** permite adicionar tipos de mixin ao tipo de nó. Os tipos de mixin são usados principalmente para adicionar recursos avançados.

### Ferramentas {#tools-button}

A variável **Botão Ferramentas** O é um menu suspenso com as seguintes ferramentas disponíveis:

* **Configuração do servidor** - para acessar o Felix Console (também disponível em `https://<host>:<port>/system/console/configMgr`)
* **Query** - para consultar o repositório
* **Privilégios** - para exibir e adicionar privilégios
* **Testar o controle de acesso** - testar a permissão para determinado caminho e/ou principal
* **Exportar tipo de nó** - para exportar tipos de nó no sistema como notação CND
* **Importar tipo de nó** - para importar tipos de nó usando a notação CND.

### Widget de login {#login-widget}

A variável **Widget de login** exibe o usuário conectado no momento.

Clique nele para fazer logon ou refazer logon como outro usuário. A variável `@crx.default` representa que você está no espaço de trabalho padrão (e somente) no repositório.

A variável **Preferências** A opção pode ser usada para definir o idioma da interface do usuário e para exibir e personalizar as teclas de atalho para várias ações, como salvar, pesquisar, criar uma observação etc.

## Criação de pastas {#creating-a-folder}

Para criar uma pasta com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No painel Navegação, clique com o botão direito do mouse na pasta em que deseja criar a nova pasta, selecione **Criar ...**, depois **Criar pasta ...**.

1. Insira a pasta **Nome** e clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

## Criando um nó {#creating-a-node}

Para criar um nó com CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No [**Painel do explorador**,](#explorer-pane) clique com o botão direito do mouse no nó em que deseja criar o novo nó, selecione **Criar**, depois **Criar nó**.
1. Insira o **Nome** e selecione o **Tipo**.
1. Clique em **OK**.
1. Clique em [**Botão Salvar tudo**](#save-all-button) para salvar as alterações no servidor.

Agora você pode adaptar o nó às suas necessidades modificando propriedades ou criando novos nós.

>[!NOTE]
>
A maioria das operações de edição, incluindo **Criar nó** O, mantém todas as alterações na memória e só as armazena no repositório após salvar (usando o [**Botão Salvar tudo**](#save-all-button)). No entanto, algumas operações, como mover, são automaticamente mantidas.
>
A validação relacionada à permissão do nó recém-criado pelo tipo de nó principal também é realizada pelo repositório ao salvar as alterações. Se você receber uma mensagem de erro ao salvar um nó, verifique se a estrutura do conteúdo é válida (por exemplo, não é possível criar um `nt:unstructured` nó como filho de `nt:folder` nó).

## Criação de uma propriedade {#creating-a-property}

Para criar uma propriedade com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No [**Painel do explorador**,](#explorer-pane) selecione o nó onde deseja adicionar a nova propriedade.
1. No [**Guia Propriedades**](#properties-tab) no painel inferior, digite o **Nome**, o **Tipo**, e o **Valor**.
1. Clique em **Adicionar**.
1. Clique em [**Botão Salvar tudo**](#save-all-button) para salvar as alterações no servidor.

## Criação de um arquivo {#creating-a-file}

Para criar um arquivo com o CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. No [**Painel do explorador**,](#explorer-pane) clique com o botão direito do mouse no componente em que deseja criar o arquivo e selecione **Criar**, depois **Criar arquivo**.
1. Insira o arquivo **Nome** incluindo a sua extensão.
1. Clique em **OK**.
1. O novo arquivo é aberto como uma guia no [**Editar Painel**.](#edit-pane)
1. Edite o arquivo.
1. Clique em [**Botão Salvar tudo**](#save-all-button) para salvar as alterações.

## Exportando e importando tipos de nós {#exporting-and-importing-node-types}

Com o CRXDE Lite, você pode importar e/ou exportar definições de tipo de nó no [Namespace compacto e notação CND (Node Type Definition)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar uma definição de tipo de nó no CRXDE Lite:

1. Abra o CRXDE Lite no navegador.
1. Selecione o nó desejado.
1. Selecionar **Ferramentas** depois **Exportar tipo de nó**.
1. A definição é exibida na notação CND em uma nova guia no navegador.
1. Salve as informações, se necessário.

Para importar uma definição de tipo de nó:

1. Abra o CRXDE Lite no navegador.
1. Selecionar **Ferramentas** depois **Importar tipo de nó**.
1. Uma nova guia é aberta na janela [**Editar Painel**](#edit-pane) rotulado **Importar tipo de nó**.
1. Insira a notação CND para a definição na caixa de texto do **Importar tipo de nó** guia.
1. Marcar **Permitir atualização** se estiver atualizando uma definição existente.
1. Clique em **Importar**.

## Logs {#logging}

Com o CRXDE Lite, é possível exibir o arquivo `error.log` que está localizado no sistema de arquivos em `<aem-install-dir>/crx-quickstart/logs` e filtrá-lo com o nível de log apropriado. Proceda da seguinte forma:

1. Abra o CRXDE Lite no navegador.
1. No menu suspenso à direita do [**Guia Console**](#console-tab) na parte inferior da janela, selecione **Logs do servidor**.
1. Clique em **Parar** ícone para exibir as mensagens.

É possível:

* Ajuste os parâmetros de log no Felix Console clicando no ícone **Configurações de registro** ícone.
* Limpe as mensagens clicando no ícone **Limpar console** ícone.
* Fixar a mensagem na seleção atual clicando no **Fixar console** ícone.
* Ative ou desative a exibição de mensagens clicando no link **Parar** ícone.
