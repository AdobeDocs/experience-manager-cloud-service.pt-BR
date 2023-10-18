---
title: Como ativar os Componentes principais do Adaptive Forms no ambiente de desenvolvimento as a Cloud Service e local do AEM Forms?
description: Saiba como ativar os Componentes principais do Adaptive Forms no AEM Forms as a Cloud Service.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin
exl-id: 32a574e2-faa9-4724-a833-1e4c584582cf
source-git-commit: 0f8aed76af4d2640094a76f2805f73a0a619e33f
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 6%

---

# Ativar os Componentes principais adaptáveis do Forms {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

A ativação dos componentes principais adaptáveis do Forms no AEM Forms as a Cloud Service permite que você comece a criar, publicar e fornecer componentes principais com base no Adaptive Forms e no Headless Forms, usando as instâncias do Cloud Service da AEM Forms para vários canais. Você precisa do ambiente habilitado dos Componentes principais adaptáveis do Forms para usar o Forms adaptável headless.

## Considerações

* Ao criar um novo programa AEM Forms as a Cloud Service, [Os componentes principais adaptáveis do Forms e o Forms adaptável headless já estão ativados para o seu ambiente](#are-adaptive-forms-core-components-enabled-for-my-environment).

* Se você tiver um programa as a Cloud Service mais antigo do Forms, em que os Componentes principais estão [não ativado](#enable-components), você pode [adicionar dependências dos Componentes principais do Forms adaptável](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment) no repositório do AEM as a Cloud Service e implante o repositório nos ambientes Cloud Service para ativar o Forms adaptável headless.

* Se o ambiente de Cloud Service existente fornecer a opção de [criar Forms adaptável com base em Componentes principais](creating-adaptive-form-core-components.md), os Componentes principais do Adaptive Forms e o Headless Adaptive Forms já estão habilitados para o seu ambiente e você pode usar o Adaptive Forms baseado em Componentes principais como formulários headless para canais como dispositivos móveis, Web, aplicativos nativos e serviços que exigem uma representação headless do Adaptive Forms.


## Ativar os Componentes principais adaptáveis do Forms e o Forms adaptável headless {#enable-headless-forms}

Execute as seguintes etapas, na ordem listada, para ativar os Componentes principais adaptáveis do Forms e o Forms adaptável headless para um ambiente as a Cloud Service do AEM Forms


![Habilitar componentes principais e formulários adaptáveis headless](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## 1. Clonar o repositório Git as a Cloud Service do AEM Forms {#clone-git-repository}

1. Efetue logon no [Cloud Manager](https://my.cloudmanager.adobe.com/) e selecione sua organização e programa.

1. Navegue até a **Pipelines** do seu **Visão geral do programa** clique no link **Acessar informações do repositório** botão para acessar e gerenciar o Repositório Git. A página inclui as seguintes informações:

   * URL do Repositório Git do Cloud Manager.
   * Credenciais do nome de usuário do Git do Repositório Git (nome de usuário e senha).

   Clique em **Gerar senha** para exibir ou gerar a senha.

1. Abra o terminal ou o prompt de comando no computador local e execute o seguinte comando:

   ```Shell
   git clone [Git Repository URL]
   ```

   Quando solicitado, forneça as credenciais. O repositório é clonado no computador local.


## 2. Adicione as dependências dos Componentes principais do Forms adaptável ao Repositório Git {#add-adaptive-forms-core-components-dependencies}

1. Abra a pasta Repositório Git em um editor de código de texto simples. Por exemplo, Código VS.
1. Abra o `[AEM Repository Folder]\pom.xml` arquivo para edição.
1. Substituir versões do `core.forms.components.version`, `core.forms.components.af.version` e `core.wcm.components.version` componentes com versões especificadas em [documentação dos Componentes principais](https://github.com/adobe/aem-core-forms-components). Se o componente não existir, adicione esses componentes.

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.wcm.components.version>2.22.10</core.wcm.components.version>
       <core.forms.components.version>2.0.18</core.forms.components.version>
       <core.forms.components.af.version>2.0.18</core.forms.components.af.version>
   </properties>
   ```

   ![Mencione a versão mais recente dos Componentes principais do Forms](/help/forms/assets/latest-forms-component-version.png)

1. Na seção de dependências do `[AEM Repository Folder]\pom.xml` adicione as seguintes dependências e salve o arquivo.

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <version>${core.wcm.components.version}</version>
               <type>zip</type>
           </dependency>    
           <!-- End of WCM Core Component Examples Dependencies -->
           <!-- Forms Core Component Dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
   <!-- End of AEM Forms Core Component Dependencies -->
   ```

1. Abra o `[AEM Repository Folder]/all/pom.xml` arquivo para edição. Adicione as seguintes dependências no `<embeddeds>` e salve o arquivo.

   ```XML
   <!-- WCM Core Component Examples Dependencies -->
   
   <!-- inside plugin config of filevault-package-maven-plugin -->  
   <!-- embed wcm core components examples artifacts -->
   
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.config</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <!-- embed forms core components artifacts -->
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   ```

   >[!NOTE]
   >
   >
   >  Substituir `${appId}` com sua appId.
   >
   >  Para encontrar o `${appId}`, no `[AEM Repository Folder]/all/pom.xml` arquivo, pesquise o `-packages/application/install` termo. O texto antes da `-packages/application/install` o termo é seu `${appId}`. Por exemplo, o código a seguir, `myheadlessform` é `${appId}`.
   >
   >   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. No `<dependencies>` seção do `[AEM Repository Folder]/all/pom.xml` adicione as seguintes dependências e salve o arquivo:

   ```XML
           <!-- Other existing dependencies -->
           <!-- wcm core components examples dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <type>zip</type>
               </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
           </dependency>
               <!-- forms core components dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
           </dependency>
               <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
           </dependency>
   ```

1. Abra o `[AEM Repository Folder]/ui.apps/pom.xml` para edição. Adicione o `af-core bundle` e salve o arquivo.

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >Verifique se os seguintes artefatos dos Componentes principais adaptáveis do Forms não estão incluídos em seu projeto.
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-apps</artifactId>`
   >
   > `</dependency>`
   >
   > e
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-core</artifactId>`
   >
   > `</dependency>`


1. Salvar e fechar o arquivo.

## 3. Criar e implantar o código atualizado

Implante o código atualizado em seus ambientes de desenvolvimento e Cloud Service locais para ativar os Componentes principais em ambos os ambientes:

* [Criar e implantar código atualizado em um ambiente de desenvolvimento local (SDK do AEM as a Cloud Service)](#core-components-on-aem-forms-local-sdk)

* [Criar e implantar código atualizado em um ambiente as a Cloud Service do AEM Forms](#core-components-on-aem-forms-cs)

### Criar e implantar código atualizado em um ambiente de desenvolvimento local {#core-components-on-aem-forms-local-sdk}

1. Abra o prompt de comando ou o terminal.

1. Navegue até o diretório raiz do seu projeto do Repositório Git.

1. Execute o seguinte comando para criar o pacote para o seu ambiente:

   ```Shell
       mvn clean install
   ```



   Depois que o pacote for criado com êxito, você poderá encontrá-lo em [Pasta do repositório Git]\all\target\[appid].all-[version].zip

1. Use o [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR) para implantar o [Pasta de projeto do arquétipo AEM]\all\target\[appid].all-[version]pacote .zip no ambiente de desenvolvimento local.


### Criar e implantar código atualizado em um ambiente as a Cloud Service do AEM Forms {#core-components-on-aem-forms-cs}

1. Abra o terminal ou o prompt de comando.
1. Navegue até o `[AEM Repository Folder]` e execute os seguintes comandos na ordem listada

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. Depois que os arquivos forem confirmados no Repositório Git, [Executar o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=pt-BR).

   Depois que a execução do pipeline for bem-sucedida, os Componentes principais adaptáveis do Forms serão ativados para o ambiente correspondente. Além disso, um modelo de Forms adaptável (Componentes principais) e o tema do Canvas 3.0 são adicionados ao ambiente as a Cloud Service do Forms, fornecendo opções para personalizar e criar Componentes principais com base no Forms adaptável.


## Perguntas frequentes {#faq}

### Quais são os componentes principais? {#core-components}

A variável [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) são um conjunto de componentes padronizados de Gerenciamento de Conteúdo na Web (WCM, na sigla em inglês) para o AEM a fim de acelerar o tempo de desenvolvimento e reduzir o custo de manutenção de seus sites.

### Quais são todos os recursos adicionados na ativação dos componentes principais? {#core-components-capabilities}

Quando os Componentes principais do Forms adaptável estiverem ativados para seu ambiente, um modelo de Formulário adaptável baseado em Componentes principais em branco e o tema do Canvas 3.0 serão adicionados ao seu ambiente. Depois de ativar os Componentes principais adaptáveis do Forms no seu ambiente, você pode:

* [Criar componentes principais com base no Forms adaptável](/help/forms/creating-adaptive-form-core-components.md).
* [Criar componentes principais com base em modelos de formulário adaptável](/help/forms/template-editor.md).
* [Criar temas personalizados para os Componentes principais com base em modelos de formulário adaptável](/help/forms/using-themes-in-core-components.md).
* [Servir representações JSON do Formulário adaptável com base nos Componentes principais para canais como dispositivos móveis, Web, aplicativos nativos e serviços que exigem a representação headless de um formulário](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-BR).

### Os Componentes principais adaptáveis do Forms estão habilitados para meu ambiente? {#enable-components}

Para verificar se os Componentes principais do Adaptive Forms estão ativados para o seu ambiente:

1. [Clonar o repositório as a Cloud Service do AEM Forms](#1-clone-your-aem-forms-as-a-cloud-service-git-repository).

1. Abra o `[AEM Repository Folder]/all/pom.xml` arquivo do Repositório Git do AEM Forms Cloud Service.

1. Procure as seguintes dependências:

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![localize o artefato core-forms-components-af-core em all/pom.xml](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   Se as dependências existirem, os Componentes principais adaptáveis do Forms serão ativados para o seu ambiente.

>[!MORELIKETHIS]
>
>* [Criar um formulário adaptável](/help/forms/creating-adaptive-form-core-components.md)