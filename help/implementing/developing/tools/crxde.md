---
title: Uso do CRXDE Lite
description: O CRXDE Lite faz parte do AEM de início rápido e está disponível para você acessar e modificar o repositório nos ambientes de desenvolvimento local no navegador.
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 3%

---


# Usando CRXDE Lite {#using-crxde-lite}

O CRXDE Lite faz parte do AEM de início rápido e está disponível para você acessar e modificar o repositório nos ambientes de desenvolvimento local no navegador. Com o CRXDE Lite, você pode editar arquivos, pastas, nós e propriedades. O repositório inteiro pode ser acessado nesta interface fácil de usar.

>[!NOTE]
>
>O CRXDE Lite só está disponível nos ambientes de desenvolvimento locais. Não está disponível em AEM como Cloud Service.

## Introdução ao CRXDE Lite {#getting-started-with-crxde-lite}

Para começar a usar o CRXDE Lite:

1. Start seu desenvolvimento local AEM rapidamente.
1. No navegador, abra o URL `https://<host>:<port>/crx/de`.
1. Digite seu **nome de usuário** e **senha**.
1. Clique em **OK**.

A interface do usuário do CRXDE Lite é exibida da seguinte maneira no seu navegador:

![A interface CRXDE Lite](assets/crxde-lite.png)

Agora você pode usar o CRXDE Lite para desenvolver seu aplicativo.

>[!TIP]
>
>Você também pode acessar o CRXDE Lite no menu AEM. No menu principal, selecione **Ferramentas** -> **Geral** -> **CRXDE Lite**.

## Visão geral da interface do usuário {#overview-of-the-user-interface}

A interface do usuário do CRXDE Lite tem muitas partes e muitas funções.

### Barra do comutador superior {#top-switcher-bar}

A barra de comutador superior permite alternar rapidamente entre o CRXDE Lite, o Gerenciador de pacotes e o Compartilhamento de pacotes.

### Widget de caminho de nó {#node-path-widget}

O Widget de caminho de nó exibe o caminho para o nó selecionado no momento.

Você também pode usá-lo para pular para um nó inserindo o caminho manualmente ou colando-o de outro lugar e pressionando Enter.

Também oferece suporte para procurar nós com nome de nó específico. Digite o nome do nó que você deseja localizar e aguarde (ou selecione o ícone de pesquisa no lado direito). Se um determinado nó ou nós forem carregados no painel explorador, a lista será exibida e você poderá selecionar o caminho e pressionar Enter para navegar até ele. Observe que ele só funciona para os nós carregados no momento no aplicativo cliente CRXDE no navegador. Se quiser pesquisar o repositório inteiro, use **Ferramentas** -&amp;gt: **Query**.

### Painel do Explorer {#explorer-pane}

O **Painel do Explorer** exibe uma árvore de todos os nós no repositório.

Clique em um nó para exibir suas propriedades na guia **Propriedades**. Depois de clicar em um nó, você pode selecionar uma ação na barra de ferramentas. Clique no nó novamente para renomeá-lo.

O Filtro de navegação da árvore (o ícone binóculos) permite filtrar os nós no repositório para os quais o nome contém o texto de entrada. Ela se aplica somente aos nós que foram carregados localmente.

### Painel Editar {#edit-pane}

O **Painel de edição** permite que você visualização o conteúdo do arquivo atualmente selecionado no repositório. Cada arquivo aberto será representado como sua própria guia no painel.

A guia **Início** permite que você pesquise o conteúdo e/ou a documentação e acesse a documentação do desenvolvedor e o suporte ao Adobe.

Clique com o duplo do mouse em um arquivo no **Painel do Explorer** para exibir seu conteúdo no **Painel de edição**. Em seguida, você pode modificá-la e salvar as alterações.

Depois que um arquivo é editado no **Painel de edição**, as seguintes ferramentas ficam disponíveis na barra de ferramentas:

* **Mostrar na árvore**  - Mostra o arquivo na árvore do repositório.
* **Pesquisar/Substituir**  - Realiza uma pesquisa ou substituição.

Clique com o duplo na linha de status do **Painel de edição** abre a caixa de diálogo **Ir para linha** para que você possa inserir um número de linha específico.

### Guia Propriedades {#properties-tab}

A guia **Propriedades** exibe as propriedades do nó selecionado. É possível adicionar novas propriedades ou excluir as existentes.

### Guia controle de acesso {#access-control-tab}

A **guia Controle de acesso** exibe permissões com base no caminho, repositório ou principal atual.

As permissões são divididas nas seguintes categorias.

* **Política**  de Controle de acesso aplicável - As políticas que podem ser aplicadas à seleção atual
* **Políticas**  de Controle de acesso local - As políticas atuais aplicadas localmente à seleção atual
* **Políticas**  de Controle de acesso Efetivas - As políticas atuais aplicadas para a seleção atual, que podem ser definidas localmente ou herdadas dos nós pais

>[!NOTE]
Para poder ver as informações do controle de acesso, o usuário conectado ao CRXDE Lite deve ter direitos de leitura das entradas ACL.

### Guia Replicação {#replication-tab}

A **guia Replicação** exibe o status de replicação do nó atual. É possível replicar e excluir o nó atual.

###  Guia Console {#console-tab}

A **Guia Console** exibe mensagens de registro. Você pode configurar o nível de log, limpar o console, fixar na posição de rolagem selecionada e ativar/desativar a exibição de mensagens.

### Guia Informações da compilação {#build-info-tab}

A **guia Informações da compilação** exibe informações quando um pacote está sendo criado.

### Botão Atualizar {#refresh-button}

O **Botão Atualizar** atualiza a seleção atual. As alterações de outros usuários são atualizadas na visualização do repositório. As alterações efetuadas não são afetadas.

### Botão Salvar tudo {#save-all-button}

O **Botão Salvar tudo** salva todas as alterações feitas. Até que você opte por salvar, as alterações são temporárias e serão perdidas quando você sair do console.

* **Reverter**  - Descarta todas as alterações feitas no nó selecionado desde a última ação de salvar e, em seguida, recarrega o estado atual do repositório para o nó selecionado
* **Reverter tudo**  - Descarta todas as alterações feitas em todo o repositório desde a última ação de salvar e, em seguida, recarrega o estado atual do repositório

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

O **Botão Mover** move o nó selecionado para o nó definido pela caixa de diálogo.

### Renomeie {#rename-button}

O **Botão Renomear** renomeia o nó selecionado.

### Misturas {#mixins-button}

O **Botão Misturas** permite que você adicione tipos de combinação ao tipo de nó. Os tipos de mixin são usados principalmente para adicionar recursos avançados.

### Ferramentas {#tools-button}

O **Botão Ferramentas** é um menu suspenso com as seguintes ferramentas disponíveis:

* **Configuração**  do servidor - para acessar o Console do Felix (também disponível em  `https://<host>:<port>/system/console/configMgr`)
* **Query**  - para query do repositório
* **Privilégios** - para visualização e adicionar privilégios
* **Controle de acesso**  de teste - para testar a permissão para determinado caminho e/ou principal
* **Exportar tipo**  de nó - para exportar tipos de nó no sistema como notação CND
* **Importar tipo**  de nó - para importar tipos de nó usando a notação CND.

### Widget de logon {#login-widget}

O **Widget de logon** exibe o usuário conectado no momento.

Clique nele para fazer logon ou login novamente como outro usuário. O `@crx.default` representa que você está na área de trabalho padrão (e somente) no repositório.

A opção **Preferências** pode ser usada para definir o idioma da interface do usuário e para visualização e personalização das teclas de atalho para várias ações, como salvar, pesquisar, criar nota, etc.

## Criação de uma pasta {#creating-a-folder}

Para criar uma pasta com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No painel de Navegação, clique com o botão direito do mouse na pasta sob a qual deseja criar a nova pasta, selecione **Criar ...**, em seguida **Criar pasta ...**.

1. Digite a pasta **Nome** e clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

## Criação de um nó {#creating-a-node}

Para criar um nó com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No [**Painel do Explorador**,](#explorer-pane) clique com o botão direito do rato no nó onde pretende criar o novo nó, selecione **Criar**, em seguida **Criar Nó**.
1. Insira **Nome** e selecione **Tipo**.
1. Clique em **OK**.
1. Clique no [**Botão Salvar tudo**](#save-all-button) para salvar as alterações no servidor.

Agora você pode adaptar o nó às suas necessidades modificando as propriedades ou criando novos nós.

>[!NOTE]
A maioria das operações de edição, incluindo **Criar nó**, mantém todas as alterações na memória e só as armazena no repositório ao salvar (usando o [**Botão Salvar tudo**](#save-all-button)). No entanto, algumas operações, como mover, são automaticamente persistentes.
A validação para determinar se o nó recém-criado é permitido pelo tipo de nó do nó pai também é realizada pelo repositório ao salvar alterações. Se você receber uma mensagem de erro ao salvar um nó, verifique se a estrutura de conteúdo é válida (por exemplo, não é possível criar um nó `nt:unstructured` como filho do nó `nt:folder`).

## Criação de uma propriedade {#creating-a-property}

Para criar uma propriedade com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No [**Painel do Explorador**,](#explorer-pane) selecione o nó onde deseja adicionar a nova propriedade.
1. Na guia [**Propriedades**](#properties-tab) no painel inferior, digite **Nome**, **Tipo** e **Valor**.
1. Clique em **Adicionar**.
1. Clique no [**Botão Salvar tudo**](#save-all-button) para salvar as alterações no servidor.

## Criando um Arquivo {#creating-a-file}

Para criar um novo arquivo com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No [**Painel do Explorador**,](#explorer-pane), clique com o botão direito do rato no componente onde pretende criar o ficheiro, selecione **Criar** e, em seguida, **Criar Ficheiro**.
1. Insira o arquivo **Name** incluindo sua extensão.
1. Clique em **OK**.
1. O novo arquivo é aberto como uma guia no [**Painel de edição**.](#edit-pane)
1. Edite o arquivo.
1. Clique no [**Botão Salvar tudo**](#save-all-button) para salvar as alterações.

## Exportando e importando tipos de nó {#exporting-and-importing-node-types}

Com o CRXDE Lite, você pode importar e/ou exportar definições de tipo de nó na notação [Namespace compacta e Definição de tipo de nó (CND)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar uma definição de tipo de nó no CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. Selecione o nó desejado.
1. Selecione **Ferramentas** em seguida **Exportar tipo de nó**.
1. A definição será exibida na notação CND em uma nova guia no seu navegador.
1. Salve as informações, se necessário.

Para importar uma definição de tipo de nó:

1. Abra o CRXDE Lite no seu navegador da 
1. Selecione **Ferramentas** e **Importar Tipo de Nó**.
1. Uma nova guia é aberta no [**Painel de edição**](#edit-pane) rotulado **Tipo de nó de importação**.
1. Digite a notação CND para a definição na caixa de texto da guia **Importar tipo de nó**.
1. Marque **Permitir atualização** se estiver atualizando uma definição existente.
1. Clique em **Importar**.

## Logs {#logging}

Com o CRXDE Lite, você pode exibir o arquivo `error.log` localizado no sistema de arquivos em `<aem-install-dir>/crx-quickstart/logs` e filtrá-lo com o nível de log apropriado. Proceda do seguinte modo:

1. Abra o CRXDE Lite no seu navegador da 
1. No menu suspenso à direita de [**Guia do console**](#console-tab), na parte inferior da janela, selecione **Logs do servidor**.
1. Clique no ícone **Parar** para exibir as mensagens.

É possível:

* Ajuste os parâmetros de log no Console do Felix clicando no ícone **Configurações de registro**.
* Limpe as mensagens clicando no ícone **Limpar Console**.
* Fixar a mensagem na seleção atual clicando no ícone **Console de pinos**.
* Ative ou desative a exibição de mensagens clicando no ícone **Parar**.
