---
title: Uso do CRXDE Lite
description: O CRXDE Lite faz parte do AEM quickstart e está disponível para você acessar e modificar o repositório em seus ambientes de desenvolvimento local no navegador.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
source-git-commit: ae79dbf490c5e8b819c287b3013bbd93cdb6a59f
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 3%

---

# Uso do CRXDE Lite {#using-crxde-lite}

O CRXDE Lite faz parte do AEM quickstart e está disponível para você acessar e modificar o repositório em seus ambientes de desenvolvimento local no navegador. Com o CRXDE Lite, você pode editar arquivos, pastas, nós e propriedades. O repositório inteiro é acessível a você nessa interface fácil de usar.

>[!NOTE]
>
>O CRXDE Lite só está disponível em seus ambientes de desenvolvimento locais. Não está disponível AEM as a Cloud Service.

## Introdução ao CRXDE Lite {#getting-started-with-crxde-lite}

Para começar a usar o CRXDE Lite:

1. Inicie o desenvolvimento de AEM local rapidamente.
1. No seu navegador, abra o URL `https://<host>:<port>/crx/de`.
1. Insira seu **username** e **senha**.
1. Clique em **OK**.

A interface do usuário do CRXDE Lite é exibida da seguinte maneira em seu navegador:

![A interface do CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>Você também pode acessar o CRXDE Lite no menu AEM. No menu principal, selecione **Ferramentas** -> **Geral** -> **CRXDE Lite**.

## Visão geral da interface do usuário {#overview-of-the-user-interface}

A interface do usuário do CRXDE Lite tem muitas partes e muitas funções.

### Barra do comutador superior {#top-switcher-bar}

A Barra do Alternador Superior permite que você alterne rapidamente entre o CRXDE Lite e [Gerenciador de pacotes.](package-manager.md)

### Widget do caminho do nó {#node-path-widget}

O widget Caminho do nó exibe o caminho para o nó selecionado no momento.

Você também pode usá-lo para pular para um nó inserindo o caminho manualmente ou colando de outro lugar e pressionando Enter.

Também oferece suporte para procurar nós com nome de nó específico. Insira o nome do nó que deseja localizar e aguarde (ou selecione o ícone de pesquisa no lado direito). Se um determinado nó ou nós forem carregados no painel explorador, a lista será exibida e você poderá selecionar o caminho e pressionar Enter para navegar até ele. Observe que ele só funciona para os nós atualmente carregados no aplicativo cliente CRXDE no navegador. Se quiser pesquisar o repositório inteiro, use **Ferramentas** ->: **Query**.

### Painel do Explorer {#explorer-pane}

O **Painel do Explorer** exibe uma árvore de todos os nós no repositório.

Clique em um nó para exibir suas propriedades na **Propriedades** guia . Depois de clicar em um nó, você pode selecionar uma ação na barra de ferramentas. Clique no nó novamente para renomeá-lo.

O Filtro de navegação em árvore (o ícone binóculos) permite filtrar os nós no repositório para o qual o nome contém o texto de entrada. Ela se aplica somente aos nós que foram carregados localmente.

### Painel Editar {#edit-pane}

O **Painel Editar** permite exibir o conteúdo do arquivo atualmente selecionado no repositório. Cada arquivo aberto será representado como sua própria guia no painel .

O **Início** permite pesquisar conteúdo e/ou documentação e acessar a documentação do desenvolvedor e o suporte ao Adobe.

Clique duas vezes em um arquivo na **Painel do Explorer** para exibir seu conteúdo no **Painel Editar**. Em seguida, você pode modificá-la e salvar as alterações.

Depois que um arquivo é editado no **Painel Editar**, as seguintes ferramentas estão disponíveis na barra de ferramentas:

* **Mostrar na árvore** - Mostra o arquivo na árvore de repositório.
* **Pesquisar/Substituir** - Realiza uma pesquisa ou substituição.

Clique duas vezes na linha de status do **Painel Editar** abre o **Ir para linha** para inserir um número de linha específico.

### Guia Propriedades {#properties-tab}

O **Guia Propriedades** exibe as propriedades do nó selecionado. É possível adicionar novas propriedades ou excluir as existentes.

### Guia Controle de acesso {#access-control-tab}

O **Guia Controle de acesso** exibe permissões com base no caminho, repositório ou principal atual.

As permissões são divididas nas seguintes categorias.

* **Política de Controle de Acesso Aplicável** - As políticas que podem ser aplicadas à seleção atual
* **Políticas de Controle de Acesso Local** - As políticas atuais aplicadas localmente à seleção atual
* **Políticas de Controle de Acesso Efetivas** - As políticas atuais aplicadas para a seleção atual, que pode ser definida localmente ou herdada dos nós pai

>[!NOTE]
Para poder ver as informações de controle de acesso, o usuário conectado ao CRXDE Lite deve ter direitos para ler as entradas ACL.

### Guia Replicação {#replication-tab}

O **Guia Replicação** exibe o status de replicação do nó atual. Você pode replicar e excluir o nó atual.

###  Guia Console {#console-tab}

O **Guia Console** exibe mensagens de log. Você pode configurar o nível de log, limpar o console, fixar na posição de rolagem selecionada e ativar/desativar a exibição de mensagens.

### Guia Informações da compilação {#build-info-tab}

O **Guia Informações da compilação** exibe informações quando um pacote está sendo criado.

### Botão Atualizar {#refresh-button}

O **Botão Atualizar** atualiza a seleção atual. As alterações de outros usuários são atualizadas na visualização do repositório. As alterações efetuadas não são afetadas.

### Botão Salvar tudo {#save-all-button}

O **Botão Salvar tudo** salva todas as alterações feitas. Até você optar por salvar, as alterações são temporárias e serão perdidas ao sair do console.

* **Reverter** - Descarta todas as alterações feitas no nó selecionado desde a última ação de salvar e, em seguida, recarrega o estado atual do repositório para o nó selecionado
* **Reverter tudo** - Descarta todas as alterações feitas em todo o repositório desde a última ação de salvar e, em seguida, recarrega o estado atual do repositório

### Botão Criar {#create-button}

O **Botão Criar** é um menu suspenso que cria o seguinte no nó selecionado:

* Nó - um nó com um tipo de nó arbitrário
* Arquivo - um `nt:file` nó e seu subnó nt:resource
* Pasta - um `nt:folder` nó

### Botão Excluir {#delete-button}

O **Botão Excluir** exclui o nó selecionado.

### Botão Copiar {#copy-button}

O **Botão Copiar** copia o nó selecionado.

## Botão Colar {#paste-button}

O **Botão Colar** cola o nó copiado no nó selecionado.

### Botão Mover {#move-button}

O **Botão Mover** move o nó selecionado para o nó definido na caixa de diálogo.

### Renomeie {#rename-button}

O **Botão Renomear** renomeia o nó selecionado.

### Misturas {#mixins-button}

O **Botão Mixins** O permite adicionar tipos mixin ao tipo de nó. Os tipos mixin são usados principalmente para adicionar recursos avançados.

### Ferramentas {#tools-button}

O **Botão Ferramentas** O é um menu suspenso com as seguintes ferramentas disponíveis:

* **Configuração do servidor** - para acessar o Felix Console (também disponível em `https://<host>:<port>/system/console/configMgr`)
* **Query** - para consultar o repositório
* **Privilégios** - para visualizar e adicionar privilégios
* **Testar controle de acesso** - testar a permissão para determinados caminhos e/ou principais
* **Exportar tipo de nó** - para exportar tipos de nó no sistema como notação CND
* **Importar Tipo de Nó** - para importar tipos de nó usando a notação CND.

### Widget de logon {#login-widget}

O **Widget de logon** exibe o usuário conectado no momento.

Clique nele para fazer logon ou fazer logon novamente como outro usuário. O `@crx.default` representa que você está no espaço de trabalho padrão (e somente) no repositório.

O **Preferências** pode ser usada para definir o idioma da interface do usuário e exibir e personalizar as teclas de atalho para várias ações, como salvar, pesquisar, criar nota, etc.

## Criação de uma pasta {#creating-a-folder}

Para criar uma pasta com o CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No painel Navegação, clique com o botão direito do mouse na pasta na qual deseja criar a nova pasta e selecione **Criar ...**, em seguida **Criar pasta ...**.

1. Insira a pasta **Nome** e clique em **OK**.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

## Criação de um nó {#creating-a-node}

Para criar um nó com CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No [**Painel do explorador**,](#explorer-pane) clique com o botão direito do mouse no nó onde deseja criar o novo nó, selecione **Criar**, em seguida **Criar nó**.
1. Insira o **Nome** e selecione o **Tipo**.
1. Clique em **OK**.
1. Clique no botão [**Botão Salvar tudo**](#save-all-button) para salvar as alterações no servidor.

Agora você pode adaptar o nó às suas necessidades modificando propriedades ou criando novos nós.

>[!NOTE]
A maioria das operações de edição, incluindo **Criar nó**, mantém todas as alterações na memória e as armazena somente no repositório ao salvar (usando o [**Botão Salvar tudo**](#save-all-button)). No entanto, algumas operações, como mover, são automaticamente persistentes.
A validação com relação a se o nó recém-criado é permitido pelo tipo de nó do nó pai também é realizada pelo repositório ao salvar as alterações. Se você receber uma mensagem de erro ao salvar um nó, verifique se a estrutura de conteúdo é válida (por exemplo, não é possível criar um `nt:unstructured` nó como filho de `nt:folder` nó ).

## Criação de uma propriedade {#creating-a-property}

Para criar uma propriedade com o CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No [**Painel do explorador**,](#explorer-pane) selecione o nó no qual deseja adicionar a nova propriedade.
1. No [**Guia Propriedades**](#properties-tab) no painel inferior, insira o **Nome**, o **Tipo** e o **Valor**.
1. Clique em **Adicionar**.
1. Clique no botão [**Botão Salvar tudo**](#save-all-button) para salvar as alterações no servidor.

## Criação de um arquivo {#creating-a-file}

Para criar um novo arquivo com o CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. No [**Painel do explorador**,](#explorer-pane) clique com o botão direito do mouse no componente onde deseja criar o arquivo, selecione **Criar**, em seguida **Criar arquivo**.
1. Insira o arquivo **Nome** incluindo a sua extensão.
1. Clique em **OK**.
1. O novo arquivo é aberto como uma guia no [**Painel Editar**.](#edit-pane)
1. Edite o arquivo .
1. Clique no botão [**Botão Salvar tudo**](#save-all-button) para salvar as alterações.

## Como exportar e importar tipos de nó {#exporting-and-importing-node-types}

Com o CRXDE Lite, você pode importar e/ou exportar definições de tipo de nó em [Notação Compact Namespace e Definição de Tipo de Nó (CND)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar uma definição de tipo de nó no CRXDE Lite:

1. Abra o CRXDE Lite no seu navegador da 
1. Selecione o nó desejado.
1. Selecionar **Ferramentas** then **Exportar tipo de nó**.
1. A definição será exibida na notação CND em uma nova guia no navegador.
1. Salve as informações, se necessário.

Para importar uma definição de tipo de nó:

1. Abra o CRXDE Lite no seu navegador da 
1. Selecionar **Ferramentas** then **Importar Tipo de Nó**.
1. Uma nova guia é aberta no [**Painel Editar**](#edit-pane) rotulado **Importar Tipo de Nó**.
1. Insira a notação de CND para a definição na caixa de texto da variável **Importar Tipo de Nó** guia .
1. Verificar **Permitir atualização** se estiver atualizando uma definição existente.
1. Clique em **Importar**.

## Logs {#logging}

Com o CRXDE Lite, você pode exibir o arquivo `error.log` que está localizado no sistema de arquivos em `<aem-install-dir>/crx-quickstart/logs` e filtrá-lo com o nível de log apropriado. Proceda do seguinte modo:

1. Abra o CRXDE Lite no seu navegador da 
1. No menu suspenso , à direita do [**Guia Console**](#console-tab) na parte inferior da janela, selecione **Logs do servidor**.
1. Clique no botão **Stop** ícone para exibir as mensagens.

É possível:

* Ajuste os parâmetros de log no Felix Console clicando no botão **Configurações de registro** ícone .
* Limpe as mensagens clicando no botão **Limpar Console** ícone .
* Fixar a mensagem na seleção atual clicando no botão **Console de pinos** ícone .
* Ative ou desative a exibição de mensagens clicando no botão **Stop** ícone .
