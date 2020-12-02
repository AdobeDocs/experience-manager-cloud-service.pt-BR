---
title: Ferramentas de desenvolvedor AEM para Eclipse
description: Ferramentas de desenvolvedor AEM para Eclipse
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 1%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## Visão geral {#overview}

As Ferramentas do desenvolvedor do AEM para Eclipse são um plug-in do Eclipse com base no [plug-in do Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lançado sob a licença do Apache 2.

Ele oferta vários recursos que facilitam AEM desenvolvimento:

* Integração perfeita com instâncias AEM por meio do Eclipse Server Connector
* Sincronização de pacotes de conteúdo e OSGi
* Suporte à depuração com recurso de troca a quente de código
* Inicialização simples de projetos AEM por meio de um Assistente de criação de projeto específico
* Edição fácil das propriedades do JCR

## Requisitos {#requirements}

Antes de usar as ferramentas do desenvolvedor AEM, é necessário:

* Baixe e instale o [Eclipse IDE para desenvolvedores de Java Enterprise](https://www.eclipse.org/downloads/packages/).
* Configure a instalação do eclipse para garantir que você tenha pelo menos 1 gigabyte de memória heap editando o arquivo de configuração `eclipse.ini` conforme descrito em [Perguntas frequentes do Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>No macOS, você precisa clicar com o botão direito do mouse em **Eclipse.app** e selecionar **Mostrar conteúdo do pacote** para encontrar seu `eclipse.ini`**.**

## Como instalar as ferramentas do desenvolvedor AEM para o Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Depois de atender aos [requisitos](#requirements) acima, você pode instalar o plug-in da seguinte maneira:

1. Abra o [Site de ferramentas do desenvolvedor AEM.](https://eclipse.adobe.com/aem/dev-tools/)

1. Copie o **Link de Instalação**.

   Observe que, como alternativa, você pode baixar um arquivo em vez de usar o link de instalação. Isso permite a instalação offline, mas você perderá notificações automáticas de atualização dessa forma.

1. No Eclipse, abra o menu **Ajuda**.
1. Clique em **Instalar novo software**.
1. Clique em **Adicionar...**.
1. Em **Nome**, digite `AEM Developer Tools`.
1. Em **Location** copie o URL de instalação.
1. Clique em **Adicionar**.
1. Verifique os plug-ins **AEM** e **Sling**.
1. Clique em **Avançar**.
1. Na janela **Instalar Detalhes**, clique novamente em **Avançar**.
1. Aceite os contratos de licença e clique em **Finish**.
1. Clique em **ReiniciarAgora** para reiniciar o Eclipse.

## A Perspectiva AEM {#the-aem-perspective}

No Eclipse, uma Perspectiva determina as ações e visualizações disponíveis em uma janela e permite a interação orientada por tarefa com recursos no Eclipse. Para obter mais detalhes sobre Perspectiva, consulte a documentação do [Eclipse.](https://help.eclipse.org)

As Ferramentas de Desenvolvimento de AEM para Eclipse fornecem uma Perspectiva AEM que oferta o controle total sobre seus projetos e instâncias de AEM. Para abrir a AEM Perspectiva:

1. Na barra de menus do Eclipse, selecione **Janela** -> **Perspectiva** -> **Abrir Perspectiva** -> **Outro**.
1. Selecione **AEM** na caixa de diálogo e clique em **Abrir**.

![A perspectiva AEM no Eclipse](assets/eclipse-aem-perspective.png)

## Amostra de projeto de vários módulos {#sample-multi-module-project}

As ferramentas de desenvolvedor AEM para Eclipse vêm com uma amostra de projeto de vários módulos que ajudam você a se familiarizar rapidamente com a configuração de um projeto no Eclipse, além de servir como um guia de práticas recomendadas para vários recursos de AEM. [Saiba mais sobre o Tipo de Arquivo](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype) do Projeto.

Siga estas etapas para criar o projeto de amostra:

1. No menu **Arquivo** > **Novo** > **Projeto**, navegue até a seção **AEM** e selecione **AEM Amostra de Projeto Multimódulo**.

   ![AEM Amostra de projeto de vários módulos](assets/aem-sample-project.png)

1. Clique em **Avançar**.

   >[!NOTE]
   >
   >Essa etapa pode levar algum tempo, pois m2eclipse precisa verificar os catálogos de arquétipos.

1. Escolha `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` no menu e clique em **Avançar**.

   ![Selecionar versão de tipo de arquivo](assets/select-archetype.png)

1. Forneça os seguintes campos para o projeto de amostra:

   * **Nome**
   * **ID do grupo**
   * **Id de artefato**
   * **appId** - Talvez seja necessário expandir as  **** opções avançadas para definir esse valor.
   * **appTitle** - Talvez seja necessário expandir as  **** opções avançadas para definir esse valor.
   * **Package** - Talvez seja necessário expandir as  **** Advancedotions para definir esse valor.

   ![Definir propriedades de arquétipo](assets/archetype-properties.png)

1. Clique em **Avançar**.

1. Em seguida, você configura um servidor AEM ao qual o Eclipse se conectará.

   Para usar o recurso do depurador, é necessário ter iniciado o AEM no modo de depuração - o que pode ser obtido, por exemplo, adicionando o seguinte à linha de comando:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Conectar-se ao servidor AEM](assets/connect-server.png)

1. Clique em **Concluir**. A estrutura do projeto é criada.

   >[!NOTE]
   >
   >Em uma nova instalação (mais especificamente, quando as dependências do Mac nunca foram baixadas), você pode criar o projeto com erros. Nesse caso, siga o procedimento descrito em [Resolvendo definição de projeto inválida](#resolving-invalid-project-definition).

## Como importar projetos existentes {#how-to-import-existing-projects}

Você pode usar o recurso **Novo projeto** para criar a estrutura certa para você:

1. Siga as instruções para criar um [Amostra de projeto de vários módulos](#sample-multi-module-project) e você terá os seguintes projetos criados para você, o que permitirá uma saudável separação de preocupações:

   * `PROJECT.ui.apps` para  `/apps` e  `/etc` conteúdo
   * `PROJECT.ui.content` para  `/content` que seja criado
   * `PROJECT.core` para pacotes Java (eles se tornarão interessantes assim que você quiser adicionar o código Java)
   * `PROJECT.it.launcher` e  `PROJECT.it.tests` para testes de integração

1. Substitua o conteúdo do projeto `PROJECT.ui.apps` pelas pastas `apps` e `etc` do pacote:

   1. No painel do Project Explorer, desmonte `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Clique com o botão direito do mouse na pasta `apps` e escolha **Mostrar em** > **Explorador do Sistema**.
   1. Exclua as pastas `apps` e `etc` que devem ser exibidas e coloque aqui as pastas `apps` e `etc` do pacote de conteúdo.
   1. No Eclipse, clique com o botão direito do mouse no projeto `PROJECT.ui.apps` e escolha **Atualizar**.

1. Em seguida, faça o mesmo para `PROJECT.ui.content` e substitua sua pasta de conteúdo por uma de suas embalagens:

   1. No painel do Project Explorer, desmonte `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Clique com o botão direito do mouse na pasta de conteúdo mais profunda e escolha **Mostrar em** -> **Explorador do Sistema**.
   1. Exclua a pasta de conteúdo que deve ser exibida e coloque aqui a pasta de conteúdo do seu pacote de conteúdo.
   1. No Eclipse, clique com o botão direito do mouse no projeto `PROJECT.ui.content` e escolha **Atualizar**.

1. Agora você precisa atualizar os arquivos `filter.xml` desses dois projetos para corresponder ao conteúdo do seu pacote de conteúdo. Para isso, abra o arquivo `META-INF/vault/filter.xml` do seu pacote de conteúdo em um editor de texto/código separado.

   * Este é um exemplo de como seu arquivo `filter.xml` pode parecer:

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

1. Quanto ao conteúdo do pacote que foi dividido em dois projetos, você também terá que dividir essas regras de filtragem em dois e atualizar os arquivos `filter.xml` dos dois projetos.

   1. No Eclipse, abra `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Substitua o conteúdo do elemento `<workspaceFilter>` pelas regras do seu pacote que start com `/apps` e `/etc`
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
   1. Substitua as regras pelas regras do seu pacote que são start por `/content`.
      * Por exemplo:

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. Certifique-se de salvar todas as alterações. Agora você pode sincronizar o novo conteúdo com a sua instância AEM.

1. No painel Servidores, verifique se a conexão foi iniciada e, se não for start.
1. Clique no ícone **Limpar e publicar**.

Depois de concluído, o pacote deve ser executado na instância e, ao salvar, qualquer alteração será automaticamente sincronizada à instância.

Se desejar reconstruir um pacote a partir do seu projeto, clique com o botão direito do mouse em `PROJECT.ui.apps` ou `PROJECT.ui.content` e escolha **Executar como** -> **Maven Install**.

Agora você tem uma pasta de públicos alvos que foi criada com seu pacote dentro (chamada, por exemplo, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Resolução de problemas {#troubleshooting}

### Resolvendo Definição de Projeto Inválida {#resolving-invalid-project-definition}

Para resolver dependências inválidas e definição de projeto, siga estas instruções:

1. Selecione todos os projetos criados.
1. Clique com o botão direito do mouse.
1. No menu de contexto, selecione **Maven** -> **Atualizar projetos**.
1. Verifique **Forçar Atualizações de Instantâneos/Versões**.
1. Clique em **OK**.

O Eclipse baixa as dependências necessárias. Isso pode levar um momento.

## Mais informações {#more-information}

A ferramenta oficial Apache Sling IDE para o site Eclipse fornece informações úteis:

* A [**ferramenta Apache Sling IDE para o Guia do Usuário do Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentação o guiará pelos conceitos gerais, integração de servidor e recursos de implantação suportados pelas Ferramentas de Desenvolvimento AEM.
* A seção [Resolução de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* Os [problemas conhecidos são listas](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

A seguinte documentação oficial do [Eclipse](https://eclipse.org/) pode ajudar a configurar seu ambiente:

* [Introdução ao Eclipse](https://eclipse.org/users/)
* [Sistema de ajuda do Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integração Maven (m2eclipse)](https://www.eclipse.org/m2e/)
