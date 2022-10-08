---
title: Ferramentas de desenvolvedor do AEM para Eclipse
description: Ferramentas de desenvolvedor do AEM para Eclipse
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 3%

---

# Ferramentas de desenvolvedor do AEM para Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## Visão geral {#overview}

O AEM Developer Tools for Eclipse é um plug-in Eclipse com base no [Plug-in do Eclipse para o Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lançado sob a licença do Apache 2.

Ela oferece vários recursos que facilitam AEM desenvolvimento:

* Integração perfeita com instâncias AEM por meio do Eclipse Server Connector
* Sincronização de pacotes de conteúdo e OSGi
* Suporte à depuração com capacidade de troca dinâmica de código
* Inicialização simples de projetos de AEM por meio de um Assistente de criação de projeto específico
* Edição fácil das propriedades do JCR

## Requisitos {#requirements}

Antes de usar as Ferramentas do desenvolvedor do AEM, é necessário:

* Baixe e instale [Eclipse IDE para desenvolvedores Enterprise Java](https://www.eclipse.org/downloads/packages/).
* Configure sua instalação do eclipse para garantir que você tenha pelo menos 1 gigabyte de memória heap editando seu `eclipse.ini` arquivo de configuração, conforme descrito na [Perguntas frequentes sobre o Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>No macOS, é necessário clicar com o botão direito do mouse em **Eclipse.app** e depois selecione **Mostrar conteúdo do pacote** para encontrar seu `eclipse.ini`**.**

## Como instalar as ferramentas de desenvolvedor do AEM para o Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Quando tiver cumprido [requisitos](#requirements) acima, você pode instalar o plug-in da seguinte maneira:

1. Abra o [Site das ferramentas do desenvolvedor do AEM](https://eclipse.adobe.com/aem/dev-tools/).

1. Copie o **Link de instalação**.

   Observe que, como alternativa, você pode baixar um arquivo em vez de usar o link de instalação. Isso permite a instalação offline, mas você perderá as notificações de atualização automáticas dessa maneira.

1. No Eclipse, abra o **Ajuda** menu.
1. Clique em **Instalar novo software**.
1. Clique em **Adicionar...**.
1. Em **Nome** enter `AEM Developer Tools`.
1. Em **Localização** copie o URL de instalação.
1. Clique em **Adicionar**.
1. Verifique ambos **AEM** e **Sling** plug-ins.
1. Clique em **Avançar**.
1. No **Detalhes da instalação** , clique em **Próximo** novamente.
1. Aceite os contratos de licença e clique em **Concluir**.
1. Clique em **ReiniciarAgora** para reiniciar o Eclipse.

## A perspectiva AEM {#the-aem-perspective}

No Eclipse, uma Perspectiva determina as ações e visualizações disponíveis em uma janela e permite a interação orientada por tarefas com recursos no Eclipse. Para obter mais detalhes sobre a Perspectiva, consulte o [Documentação do Eclipse.](https://help.eclipse.org)

As Ferramentas de desenvolvimento de AEM para o Eclipse fornecem uma Perspectiva AEM que oferece controle total sobre seus projetos e instâncias de AEM. Para abrir a Perspectiva de AEM:

1. Na barra de menu Eclipse , selecione **Window** -> **Perspectiva** -> **Abrir perspectiva** -> **Outras**.
1. Selecionar **AEM** na caixa de diálogo e clique em **Abrir**.

![A perspectiva AEM no Eclipse](assets/eclipse-aem-perspective.png)

## Exemplo de projeto de vários módulos {#sample-multi-module-project}

O AEM Developer Tools for Eclipse vem com uma amostra de projeto de vários módulos que ajuda você a se familiarizar rapidamente com a configuração do projeto no Eclipse, além de servir como um guia de práticas recomendadas para vários recursos AEM. [Saiba mais sobre o Arquétipo de projeto](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

Siga estas etapas para criar o projeto de amostra:

1. No **Arquivo** > **Novo** > **Projeto** navegue até o menu **AEM** e selecione **AEM exemplo de projeto de vários módulos**.

   ![AEM exemplo de projeto de vários módulos](assets/aem-sample-project.png)

1. Clique em **Avançar**.

   >[!NOTE]
   >
   >Esta etapa pode demorar um pouco, pois m2eclipse precisa digitalizar os catálogos de arquétipo.

1. Choose `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` no menu e, em seguida, clique em **Próximo**.

   ![Selecionar versão do arquétipo](assets/select-archetype.png)

1. Forneça os seguintes campos para o projeto de amostra:

   * **Nome**
   * **ID do Grupo**
   * **Id Do Artefato**
   * **appId** - Talvez seja necessário expandir o **Avançado** para definir esse valor.
   * **appTitle** - Talvez seja necessário expandir o **Avançado** para definir esse valor.
   * **Embalagem** - Talvez seja necessário expandir o **Avançado** para definir esse valor.

   ![Definir propriedades de arquétipo](assets/archetype-properties.png)

1. Clique em **Avançar**.

1. Em seguida, configure um servidor AEM ao qual o Eclipse se conectará.

   Para usar o recurso do depurador, é necessário ter iniciado o AEM no modo de depuração - o que pode ser feito, por exemplo, adicionando o seguinte à linha de comando:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Conectar-se ao servidor AEM](assets/connect-server.png)

1. Clique em **Concluir**. A estrutura do projeto é criada.

   >[!NOTE]
   >
   >Em uma nova instalação (mais especificamente, quando as dependências maven nunca foram baixadas), você pode criar o projeto com erros. Neste caso, siga o procedimento descrito em [Resolvendo Definição de Projeto Inválida](#resolving-invalid-project-definition).

## Como Importar Projetos Existentes {#how-to-import-existing-projects}

Você pode usar o **Novo projeto** para criar a estrutura correta para você:

1. Siga as instruções para criar um [Exemplo de projeto de vários módulos](#sample-multi-module-project) e você terá os seguintes projetos criados para você, o que permitirá uma saudável separação de preocupações:

   * `PROJECT.ui.apps` para `/apps` e `/etc` conteúdo
   * `PROJECT.ui.content` para `/content` criado
   * `PROJECT.core` para pacotes Java (eles se tornarão interessantes assim que você quiser adicionar o código Java)
   * `PROJECT.it.launcher` e `PROJECT.it.tests` para testes de integração

1. Substitua o conteúdo de sua `PROJECT.ui.apps` com o `apps` e `etc` pastas do seu pacote:

   1. No painel Explorador de projetos , expanda `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Clique com o botão direito do mouse no `apps` e escolha **Mostrar em** > **Explorador de sistema**.
   1. Exclua o `apps` e `etc` pastas que você deve ver e colocar aqui a variável `apps` e `etc` pastas do seu pacote de conteúdo.
   1. No Eclipse, clique com o botão direito do mouse no `PROJECT.ui.apps` e escolha **Atualizar**.

1. Em seguida, faça o mesmo para o `PROJECT.ui.content` e substitua a pasta de conteúdo pela do pacote:

   1. No painel Explorador de projetos , expanda `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Clique com o botão direito do mouse na pasta de conteúdo mais profunda e escolha **Mostrar em** -> **Explorador de sistema**.
   1. Exclua a pasta de conteúdo que deve ser exibida e coloque aqui a pasta de conteúdo do seu pacote de conteúdo.
   1. No Eclipse, clique com o botão direito do mouse no `PROJECT.ui.content` e escolha **Atualizar**.

1. Agora é necessário atualizar o `filter.xml` Os arquivos desses dois projetos correspondem ao conteúdo do seu pacote de conteúdo. Para isso, abra o `META-INF/vault/filter.xml` arquivo do seu pacote de conteúdo em um editor de texto/código separado.

   * Este é um exemplo de como o `filter.xml` o arquivo pode parecer:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. Quanto ao conteúdo do seu pacote que foi dividido em dois projetos, você também precisará dividir essas regras de filtro em dois e atualizar adequadamente a variável `filter.xml` arquivos dos dois projetos.

   1. No Eclipse, abra `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Substitua o conteúdo da variável `<workspaceFilter>` com as regras do seu pacote que começam com `/apps` e `/etc`
      * Por exemplo:

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/apps/foo"/>
            <filter root="/apps/foundation/components/bar"/>
            <filter root="/etc/designs/foo"/>
         </workspaceFilter>
         ```
   1. Em seguida, abra `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. Substitua as regras pelas do seu pacote que começam com `/content`.
      * Por exemplo:

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. Salve todas as alterações. Agora você pode sincronizar o novo conteúdo para a instância do AEM.

1. No painel Servidores, verifique se a conexão foi iniciada e, se não for iniciada.
1. Clique no botão **Limpar e publicar** ícone .

Depois de concluído, seu pacote deverá estar em execução na instância e, ao salvar, qualquer alteração será sincronizada automaticamente com a instância.

Para reconstruir um pacote do seu projeto, clique com o botão direito do mouse no `PROJECT.ui.apps` ou `PROJECT.ui.content` e escolha **Executar como** -> **Instalação do Maven**.

Agora você tem uma pasta de destino que foi criada com seu pacote dentro do (chamada de , por exemplo, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Resolução de problemas {#troubleshooting}

### Resolvendo Definição de Projeto Inválida {#resolving-invalid-project-definition}

Para resolver dependências inválidas e definição de projeto, proceda da seguinte maneira:

1. Selecione todos os projetos criados.
1. Clique com o botão direito do mouse.
1. No menu de contexto, selecione **Maven** -> **Atualizar projetos**.
1. Verificar **Forçar atualizações de instantâneos/versões**.
1. Clique em **OK**.

O Eclipse baixa as dependências necessárias. Isso pode levar um momento.

## Mais informações {#more-information}

O site oficial Apache Sling IDE tooling for Eclipse fornece informações úteis:

* O [**Ferramentas do Apache Sling IDE para Eclipse** Guia do usuário](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentação guiará você pelos conceitos gerais, pela integração de servidor e pelos recursos de implantação suportados pelas Ferramentas de desenvolvimento de AEM.
* O [Seção Solução de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* O [Lista de problemas conhecidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

O seguinte funcionário [Eclipse](https://eclipse.org/) a documentação pode ajudar a configurar seu ambiente:

* [Introdução ao Eclipse](https://eclipse.org/users/)
* [Sistema de ajuda do Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integração Maven (m2eclipse)](https://www.eclipse.org/m2e/)
