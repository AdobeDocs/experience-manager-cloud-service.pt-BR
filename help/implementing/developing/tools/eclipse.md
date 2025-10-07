---
title: Ferramentas de desenvolvedor do AEM para Eclipse
description: Saiba como usar as Ferramentas de desenvolvedor do AEM para Eclipse, um plug-in Eclipse baseado no plug-in Eclipse para Apache Sling.
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ba42d58a4e55efdada35cc7706d736a7314ba743
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 2%

---

# Ferramentas de desenvolvedor do AEM para Eclipse{#aem-developer-tools-for-eclipse}

![Ferramentas para desenvolvedores do Experience Manager para o logotipo Eclipse](assets/eclipse-logo.png)

## Visão geral {#overview}

As _Ferramentas para desenvolvedores do Experience Manager para Eclipse_ são um plug-in Eclipse baseado no [plug-in Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lançado com a Licença do Apache 2.

Ele oferece vários recursos que facilitam o desenvolvimento do AEM:

* Integração perfeita com instâncias do AEM por meio do Eclipse Server Connector
* Sincronização para conteúdo e pacotes OSGi
* Suporte à depuração com recurso de troca a quente de código
* Bootstrap simples de projetos do AEM por meio de um assistente de criação de projeto específico
* Fácil edição das propriedades do JCR

## Requisitos {#requirements}

Antes de usar as Ferramentas do desenvolvedor do AEM, é necessário:

* Baixe e instale o [Eclipse IDE para desenvolvedores Enterprise Java™](https://www.eclipse.org/downloads/packages/).
* Configure a instalação do eclipse para garantir que você tenha pelo menos 1 GB de memória heap, editando o arquivo de configuração `eclipse.ini` conforme descrito nas [Perguntas frequentes sobre o Eclipse.](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)

>[!NOTE]
>
>No macOS, clique com o botão direito do mouse em **Eclipse.app** e selecione **Mostrar Conteúdo do Pacote** para encontrar seu `eclipse.ini`**.**

## Como instalar as ferramentas de desenvolvedor do AEM para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Quando tiver atendido aos [requisitos](#requirements) acima, você poderá instalar o plug-in da seguinte maneira:

1. Abra o [Site de Ferramentas do Desenvolvedor do AEM](https://eclipse.adobe.com/).

<!-- had to update the link again - was https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip -->
<!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. Copie o **Link de Instalação**.

   Como alternativa, você pode baixar um arquivo em vez de usar o link de instalação. Este método permite a instalação offline, mas você não recebe notificações de atualização automática perdida dessa maneira.

1. No Eclipse, abra o menu **Ajuda**.
1. Clique em **Instalar novo software**.
1. Clique em **Adicionar...**.
1. No campo **Nome**, digite `AEM Developer Tools`.
1. No campo **Local**, copie a URL de instalação.
1. Clique em **Adicionar**.
1. Verifique os plug-ins do **AEM** e do **Sling**.
1. Clique em **Avançar**.
1. Na janela **Detalhes da Instalação**, clique novamente em **Avançar**.
1. Aceite os contratos de licença e clique em **Concluir**.
1. Clique em **RestartNow** para reiniciar o Eclipse.

## A perspectiva da AEM {#the-aem-perspective}

No Eclipse, uma Perspectiva determina as ações e visualizações disponíveis em uma janela e permite a interação orientada a tarefas com recursos no Eclipse. Para obter mais detalhes sobre Perspectiva, consulte a [documentação do Eclipse](https://help.eclipse.org/latest/index.jsp).

As _Ferramentas de desenvolvimento do Experience Manager para Eclipse_ fornecem uma Perspectiva do AEM que oferece controle total sobre seus Projetos e instâncias do AEM. Para abrir a Perspectiva do AEM:

1. Na barra de menus do Eclipse, selecione **Janela** > **Perspectiva** > **Abrir Perspectiva** > **Outras**.
1. Selecione **AEM** no diálogo e clique em **Abrir**.

![A perspectiva do AEM no Eclipse](assets/eclipse-aem-perspective.png)

## Exemplo de projeto de vários módulos {#sample-multi-module-project}

As _Ferramentas de desenvolvedor do Experience Manager para Eclipse_ vêm com uma amostra de projeto de vários módulos que ajuda você a se familiarizar rapidamente com a configuração de um projeto no Eclipse. Ele também serve como um guia de práticas recomendadas para vários recursos do AEM. [Saiba mais sobre o Arquétipo de Projeto](https://github.com/adobe/aem-project-archetype).

Siga estas etapas para criar o projeto de amostra:

1. No menu **Arquivo** > **Novo** > **Projeto**, navegue até a seção **AEM** e selecione **Projeto de vários módulos de exemplo do AEM**.

   ![Projeto de vários módulos de amostra do AEM](assets/aem-sample-project.png)

1. Clique em **Avançar**.

   >[!NOTE]
   >
   >Esta etapa pode demorar porque o m2eclipse deve verificar os catálogos de arquétipo.

1. Escolha `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` no menu e clique em **Avançar**.

   ![Selecionar versão do arquétipo](assets/select-archetype.png)

1. Forneça os seguintes campos para o projeto de amostra:

   * **Nome**
   * **Id Do Grupo**
   * **Id do artefato**
   * **appId** - Talvez seja necessário expandir as opções **Avançado** para definir esse valor.
   * **appTitle** - Talvez seja necessário expandir as opções **Avançado** para definir esse valor.
   * **Pacote** - Talvez seja necessário expandir as opções **Avançado** para definir este valor.

   ![Definir propriedades do arquétipo](assets/archetype-properties.png)

1. Clique em **Avançar**.

1. Em seguida, você configura um servidor AEM ao qual o Eclipse se conecta.

   Para usar o recurso do depurador, é necessário iniciar o AEM no modo de depuração, o que pode ser obtido ao adicionar o seguinte à linha de comando:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Conectar-se ao servidor do AEM](assets/connect-server.png)

1. Clique em **Concluir**. A estrutura do projeto é criada.

   >[!NOTE]
   >
   >Em uma nova instalação (mais especificamente, quando as dependências do Maven nunca foram baixadas), você pode criar o projeto com erros. Nesse caso, siga o procedimento descrito em [Resolvendo Definição de Projeto Inválida](#resolving-invalid-project-definition).

## Como Importar Projetos Existentes {#how-to-import-existing-projects}

Você pode usar o recurso **Novo Projeto** para criar a estrutura correta para você:

1. Siga as instruções para criar um [Projeto de vários módulos de amostra](#sample-multi-module-project) e você terá os seguintes projetos criados para você, que permitem uma separação saudável das preocupações:

   * `PROJECT.ui.apps` para conteúdo de `/apps` e `/etc`
   * `PROJECT.ui.content` para `/content` criado
   * `PROJECT.core` para pacotes Java™ (eles se tornam interessantes quando você deseja adicionar um código Java™)
   * `PROJECT.it.launcher` e `PROJECT.it.tests` para testes de integração

1. Substitua o conteúdo do projeto `PROJECT.ui.apps` pelas pastas `apps` e `etc` do pacote:

   1. No painel Explorador de projetos, abra `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Clique com o botão direito do mouse na pasta `apps` e escolha **Mostrar em** > **System Explorer**.
   1. Exclua as pastas `apps` e `etc` que você deve ver e coloque aqui as pastas `apps` e `etc` do seu pacote de conteúdo.
   1. No Eclipse, clique com o botão direito do mouse no projeto `PROJECT.ui.apps` e escolha **Atualizar**.

1. Em seguida, faça o mesmo para `PROJECT.ui.content` e substitua sua pasta de conteúdo pela de seus pacotes:

   1. No painel Explorador de projetos, abra `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Clique com o botão direito do mouse na pasta de conteúdo mais profundo e escolha **Mostrar em** > **System Explorer**.
   1. Exclua a pasta de conteúdo que você deve ver e coloque aqui a pasta de conteúdo do seu pacote de conteúdo.
   1. No Eclipse, clique com o botão direito do mouse no projeto `PROJECT.ui.content` e escolha **Atualizar**.

1. Agora você precisa atualizar os `filter.xml` arquivos desses dois projetos para corresponder ao conteúdo do seu pacote de conteúdo. Para isso, abra o arquivo `META-INF/vault/filter.xml` do seu pacote de conteúdo em um editor de texto/código separado.

   * Este é um exemplo de como o arquivo `filter.xml` pode ser:

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

1. Quanto ao conteúdo do seu pacote que foi dividido em dois projetos, você também deve dividir essas regras de filtro em dois e atualizar adequadamente os arquivos `filter.xml` dos dois projetos.

   1. No Eclipse, abra `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Substitua o conteúdo do elemento `<workspaceFilter>` pelas regras do seu pacote que começam com `/apps` e `/etc`
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

1. Certifique-se de salvar todas as alterações. Agora você pode sincronizar esse novo conteúdo para sua instância do AEM.

1. No painel Servidores, verifique se a conexão foi iniciada e, se não, inicie-a.
1. Clique no ícone **Limpar e publicar**.

Depois de concluído, o pacote deve estar em execução na instância e, ao salvar, qualquer alteração é sincronizada automaticamente com a instância.

Se quiser recriar um pacote de seu projeto, clique com o botão direito do mouse em `PROJECT.ui.apps` ou `PROJECT.ui.content` e escolha **Executar como** > **Instalação do Maven**.

Agora você tem uma pasta de destino criada com seu pacote (chamada, por exemplo, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Resolução de problemas {#troubleshooting}

### Resolvendo Definição de Projeto Inválida {#resolving-invalid-project-definition}

Para resolver dependências inválidas e a definição do projeto, proceda da seguinte maneira:

1. Selecione todos os projetos criados.
1. Clique com o botão direito do mouse em.
1. No menu de contexto, selecione **Maven** > **Atualizar projetos**.
1. Verificar **Forçar Atualizações de Instantâneos/Versões**.
1. Clique em **OK**.

O Eclipse baixa as dependências necessárias. Isso pode demorar um pouco.

## Mais informações {#more-information}

A ferramenta oficial do Apache Sling IDE para o site do Eclipse fornece informações úteis:

* A [**Ferramenta Apache Sling IDE para Eclipse** Guia do Usuário](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentação orienta você pelos conceitos gerais, integração de servidor e recursos de implantação compatíveis com as Ferramentas de Desenvolvimento do AEM.
* A [seção Solução de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* A [lista de problemas conhecidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

A documentação oficial [Eclipse](https://www.eclipse.org/) a seguir pode ajudar a configurar seu ambiente:

* [Introdução ao Eclipse](https://eclipseide.org/getting-started/)
* [Sistema de Ajuda do Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integração do Maven (m2eclipse)](https://www.eclipse.org/m2e/)
