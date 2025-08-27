---
title: Marque e ative os Componentes principais do Adaptive Forms no AEM Forms as a Cloud Service
description: Saiba como verificar se os Componentes principais do Forms adaptável estão ativados e como ativá-los, se necessário, no AEM Forms as a Cloud Service.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: 32a574e2-faa9-4724-a833-1e4c584582cf
hide: true
hidefromtoc: true
source-git-commit: 3c1931d67e69d155e777c8761fe2bbbd21461ddf
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 1%

---

# Marque e ative os componentes principais adaptáveis do Forms {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

Os Componentes principais adaptáveis do Forms e o Forms adaptável headless já estão habilitados para a maioria dos clientes do AEM Forms as a Cloud Service. Isso permite criar, publicar e fornecer Forms adaptável e Forms headless baseados em componentes principais usando suas instâncias do AEM Forms Cloud Service para vários canais.

## Verifique se os Componentes principais adaptáveis do Forms estão ativados {#check-if-enabled}

Antes de seguir qualquer etapa de ativação, verifique se os Componentes principais adaptáveis do Forms já estão ativados para o seu ambiente:

### Para novos programas do AEM Forms as a Cloud Service

Ao criar um novo programa AEM Forms as a Cloud Service, os Componentes principais do Adaptive Forms e o Headless Adaptive Forms já estão ativados para o seu ambiente.

### Para ambientes Cloud Service existentes

Se seu ambiente Cloud Service existente fornecer a opção de [criar Forms adaptável baseado em Componentes principais](creating-adaptive-form-core-components.md), os Componentes principais do Adaptive Forms e o Forms adaptável headless já estarão habilitados para o seu ambiente.

### Verificar verificando o repositório

Para confirmar se os Componentes principais do Adaptive Forms estão ativados para o seu ambiente:

1. Clonar o repositório do AEM Forms as a Cloud Service.

1. Abra o arquivo `[AEM Repository Folder]/all/pom.xml` do Repositório Git do AEM Forms Cloud Service.

1. Procure as seguintes dependências:

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![localize o artefato core-forms-components-af-core em all/pom.xml](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   Se essas dependências existirem, os Componentes principais adaptáveis do Forms serão ativados para o seu ambiente.

## Quando a ativação manual é necessária {#when-manual-enablement-needed}

Somente se você tiver um programa mais antigo do Forms as a Cloud Service em que os Componentes principais não estejam ativados (confirmado pela verificação acima), será necessário adicionar manualmente as dependências dos Componentes principais do Adaptive Forms ao repositório do AEM as a Cloud Service e implantar o repositório nos ambientes do Cloud Service.

+++ Etapas de ativação manual 

>[!WARNING]
>
>Siga estas etapas somente se a verificação acima confirmar que os componentes principais adaptáveis do Forms NÃO estão ativados para o seu ambiente.

Execute as seguintes etapas, na ordem listada, para ativar os Componentes principais adaptáveis do Forms e o Forms adaptável headless para um ambiente do AEM Forms as a Cloud Service:

![Habilitar componentes principais e formulários adaptáveis headless](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## &#x200B;1. Clonar o repositório Git do AEM Forms as a Cloud Service {#clone-git-repository}

1. Faça logon no [Cloud Manager](https://my.cloudmanager.adobe.com/) e selecione sua organização e programa.

1. Navegue até o cartão **Pipelines** na página **Visão geral do programa**, clique no botão **Acessar informações do repositório** para acessar e gerenciar o Repositório Git. A página inclui as seguintes informações:

   * URL do Repositório Git da Cloud Manager.
   * Credenciais do nome de usuário do Git do Repositório Git (nome de usuário e senha).

   Clique em **Gerar senha** para exibir ou gerar a senha.

1. Abra o terminal ou o prompt de comando no computador local e execute o seguinte comando:

   ```Shell
   git clone [Git Repository URL]
   ```

   Quando solicitado, forneça as credenciais. O repositório é clonado no computador local.


## &#x200B;2. Adicione as dependências dos Componentes principais do Forms adaptável ao Repositório Git {#add-adaptive-forms-core-components-dependencies}

1. Abra a pasta Repositório Git em um editor de código de texto simples. Por exemplo, Código VS.
1. Abra o arquivo `[AEM Repository Folder]\pom.xml` para edição.
1. Substitua as versões dos componentes `core.forms.components.version`, `core.forms.components.af.version` e `core.wcm.components.version` pelas versões especificadas na [documentação dos componentes principais](https://github.com/adobe/aem-core-forms-components). Se o componente não existir, adicione esses componentes.

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.wcm.components.version>2.22.10</core.wcm.components.version>
       <core.forms.components.version>2.0.18</core.forms.components.version>
       <core.forms.components.af.version>2.0.18</core.forms.components.af.version>
   </properties>
   ```

   ![Mencione a versão mais recente dos Componentes principais do Forms](/help/forms/assets/latest-forms-component-version.png)

1. Na seção de dependências do arquivo `[AEM Repository Folder]\pom.xml`, adicione as seguintes dependências e salve o arquivo.

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

1. Abra o arquivo `[AEM Repository Folder]/all/pom.xml` para edição. Adicione as seguintes dependências na seção `<embeddeds>` e salve o arquivo.

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
   >  Substitua `${appId}` com sua appId.
   >
   >  Para encontrar seu `${appId}`, no arquivo `[AEM Repository Folder]/all/pom.xml`, pesquise o termo `-packages/application/install`. O texto antes do termo `-packages/application/install` é o seu `${appId}`. Por exemplo, o código a seguir, `myheadlessform` é `${appId}`.
   >
   >   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. Na seção `<dependencies>` do arquivo `[AEM Repository Folder]/all/pom.xml`, adicione as seguintes dependências e salve o arquivo:

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

1. Abra o `[AEM Repository Folder]/ui.apps/pom.xml` para edição. Adicione a dependência `af-core bundle` e salve o arquivo.

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

## &#x200B;3. Criar e implantar o código atualizado

Implante o código atualizado em seus ambientes de desenvolvimento local e do Cloud Service para ativar os Componentes principais nos dois ambientes:

* [Criar e implantar código atualizado em um ambiente de desenvolvimento local (AEM as a Cloud Service SDK)](#core-components-on-aem-forms-local-sdk)

* [Criar e implantar código atualizado em um ambiente do AEM Forms as a Cloud Service](#core-components-on-aem-forms-cs)

### Criar e implantar código atualizado em um ambiente de desenvolvimento local {#core-components-on-aem-forms-local-sdk}

1. Abra o prompt de comando ou o terminal.

1. Navegue até o diretório raiz do seu projeto do Repositório Git.

1. Execute o seguinte comando para criar o pacote para o seu ambiente:

   ```Shell
       mvn clean install
   ```



   Depois que o pacote for criado com êxito, você poderá encontrá-lo na [Pasta do Repositório Git]\all\target\[appid].all-[version].zip

1. Use o [Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR) para implantar o [pacote de Pasta de Projeto do Arquétipo do AEM]\all\target\[appid].all-[version].zip no ambiente de desenvolvimento local.


### Criar e implantar código atualizado em um ambiente do AEM Forms as a Cloud Service {#core-components-on-aem-forms-cs}

1. Abra o terminal ou o prompt de comando.
1. Navegue até `[AEM Repository Folder]` e execute os seguintes comandos na ordem listada

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. Depois que os arquivos forem confirmados no Repositório Git, [Execute o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=pt-BR).

   Depois que a execução do pipeline for bem-sucedida, os Componentes principais adaptáveis do Forms serão ativados para o ambiente correspondente. Além disso, um modelo de Forms adaptável (Componentes principais) e o tema do Canvas 3.0 são adicionados ao ambiente do Forms as a Cloud Service, fornecendo opções para personalizar e criar Componentes principais com base no Adaptive Forms.

+++

## Perguntas frequentes {#faq}

### Quais são os componentes principais? {#core-components}

Os [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) são um conjunto de componentes padronizados de Gerenciamento de Conteúdo Online (WCM) para que o AEM acelere o tempo de desenvolvimento e reduza o custo de manutenção de seus sites.

### Quais são todos os recursos adicionados na ativação dos componentes principais? {#core-components-capabilities}

Quando os Componentes principais do Forms adaptável estiverem ativados para seu ambiente, um modelo de Formulário adaptável baseado em Componentes principais em branco e o tema do Canvas 3.0 serão adicionados ao seu ambiente. Depois de ativar os Componentes principais adaptáveis do Forms no seu ambiente, você pode:

* [Criar Componentes Principais com base no Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md).
* [Criar Componentes Principais com base em modelos de Formulário Adaptável](/help/forms/template-editor.md).
* [Criar temas personalizados para os Componentes principais com base em modelos de Formulário adaptável](/help/forms/using-themes-in-core-components.md).
* [Servir representações JSON do Formulário adaptável com base no Componente principal para canais como dispositivos móveis, Web, aplicativos nativos e serviços que exigem a representação headless de um formulário](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=pt-BR).

### Como sei se preciso ativar manualmente os Componentes principais do Adaptive Forms? {#manual-enablement-needed-faq}

A maioria dos clientes já tem os Componentes principais adaptáveis do Forms ativados. Você só precisará ativá-los manualmente se:

1. Você tem um programa mais antigo do Forms as a Cloud Service criado antes dos Componentes principais serem incluídos automaticamente
1. A verificação na seção [Verificar se os Componentes principais adaptáveis do Forms estão habilitados](#check-if-enabled) confirma que as dependências necessárias estão ausentes do repositório

Se não tiver certeza, siga as etapas de verificação na seção [Verificar se os Componentes principais adaptáveis do Forms estão habilitados](#check-if-enabled) acima.

### Por que os formulários baseados nos Componentes principais não são renderizados no projeto?

Os formulários baseados nos Componentes principais podem deixar de ser renderizados devido a uma incompatibilidade de versões entre o pacote dos Componentes principais do Forms e a versão incluída no arquétipo de projeto. Normalmente, esse problema ocorre quando a versão especificada no arquétipo do projeto é igual ou superior à versão fornecida com o pacote dos Componentes principais do Forms. Para resolver esse problema, siga um destes procedimentos:

* Use uma versão inferior do pacote dos Componentes principais do Forms no arquétipo de projeto.
* Remova a dependência dos Componentes principais do Forms do arquétipo de projeto, pois a versão necessária já está incluída no AEM as a Cloud Service. O pacote dos Componentes principais do Forms é fornecido com o AEM as a Cloud SDK a partir da versão 20133, por exemplo, `AEM SDK v2025.3.20133.20250325T063357Z-250300`.

>[!MORELIKETHIS]
>
>* [Criar um Formulário Adaptável](/help/forms/creating-adaptive-form-core-components.md)
