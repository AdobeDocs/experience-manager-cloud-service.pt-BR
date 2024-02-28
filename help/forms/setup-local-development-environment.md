---
title: Como configurar um ambiente de desenvolvimento local para o AEM Forms?
description: Configurar um ambiente de desenvolvimento local para o Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 12877a77-094f-492a-af58-cffafecf79ae
source-git-commit: 1ec17aebe4eb003b24f5036288a8836aabddb77a
workflow-type: tm+mt
source-wordcount: '2724'
ht-degree: 1%

---

# Configurar ambiente de desenvolvimento local para o AEM Forms {#overview}

Ao instalar e configurar um [!DNL  Adobe Experience Manager Forms] as a [!DNL  Cloud Service] , você configura ambientes de desenvolvimento, de preparo e de produção na nuvem. Além disso, também é possível definir e configurar um ambiente de desenvolvimento local.

Você pode usar o ambiente de desenvolvimento local para executar as seguintes ações sem fazer logon no ambiente de desenvolvimento da nuvem:

* [Criar formulários](creating-adaptive-form.md) e ativos relacionados (temas, modelos, ações enviar personalizadas e muito mais)
* [Converter PDF forms em Forms adaptável](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=pt-BR)
* Criar aplicativos para gerar [Comunicações do cliente](aem-forms-cloud-service-communications-introduction.md) por demanda ou em modos de lote.

Depois que um Formulário adaptável ou ativos relacionados estiverem prontos na instância de desenvolvimento local ou em um aplicativo para gerar [Comunicações do cliente] estiver pronto, você poderá exportar o formulário adaptável ou o aplicativo de comunicações do cliente do ambiente de desenvolvimento local para um ambiente Cloud Service para testes adicionais ou migração para ambientes de produção.

Você também pode desenvolver e testar o código personalizado, como componentes personalizados e preencher o serviço no ambiente de desenvolvimento local. Quando o código personalizado for testado e estiver pronto, você poderá usar o repositório Git do seu ambiente de desenvolvimento de Cloud Service para implantar o código personalizado.

Para configurar um novo ambiente de desenvolvimento local e usá-lo para desenvolver atividades do, execute as seguintes ações na ordem listada:

* [Configurar ferramentas de desenvolvimento](#setup-development-tools-for-AEM-projects)

* [Configurar instâncias locais de Autor e Publicação](#set-up-local-experience-manager-environment-for-development)

* [Adicionar arquivo do Forms às instâncias de desenvolvimento locais e configurar usuários](#add-forms-archive-configure-users)

* [Configurar ambiente de desenvolvimento local para microsserviços](#docker-microservices)

* [Configurar um projeto de desenvolvimento](#forms-cloud-service-local-development-environment)

* [Configurar ferramentas locais do Dispatcher](#setup-local-dispatcher-tools)

<!--
You can use the local development environment to create and test Adaptive Forms without connecting to the Cloud Service. [!DNL AEM Forms] provides an SDK to help test all the cloud-ready functionalities on the local development environment. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can also develop and test custom code like custom components and prefill service on the local development environment. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code. 

>[!NOTE]
>
> Pre-pilot release does not support using an [!DNL AEM Forms] as a Cloud Service development instance to create forms. You can create forms, related assets, and custom code only on a local development environment.-->

<!--
You configure two types of development environments:

* **[!DNL AEM Forms] as a Cloud Service development environment:** Use the [[!DNL AEM Forms] as a Cloud Service](setup-forms-cloud-service.md) environment to store, manage, and publish Adaptive Forms and related assets. Do not use an [!DNL AEM Forms] as a Cloud Service environment to create Adaptive Forms and related assets <!--, form-centric workflows, a form data model, or to generate a Document of Record. -->

<!--
* **Local development environment:** You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. 
Use a local development environment:
    
    * To create forms and related assets (themes, templates, custom Submit Actions, and more) and convert PDF forms to Adaptive Forms. After an Adaptive Form or related assets are ready on the local development instance, you can export the Adaptive Form and related assets from the local development environment to an [!DNL AEM Forms] as a Cloud Service development environment for publishing.  
    
    * To update configuration settings and develop and test custom code like custom components and prefill service. When the custom code is tested and ready, you can use the Git repository of your [!DNL AEM Forms] as a Cloud Service development environment to deploy the custom code.  

You can use the local development environment to create and test Adaptive Forms without connecting to the service. Adobe provides a SDK for the local development to help test all the cloud-ready functionalities. When your forms and related assets are ready and tested on the local development environment, you can import these forms and related assets to an [!DNL AEM Forms] as a Cloud Service instance for publishing. 

You can use the [development tools](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/dev-tools.html) to write custom code, customize or create new Adaptive Forms components, create a custom prefill service, or modify default configurations of an [!DNL AEM Forms] as a Cloud Service instance. 

-->

## Pré-requisitos

Você precisa do seguinte software para configurar um ambiente de desenvolvimento local. Baixe-os antes de começar a configurar o ambiente de desenvolvimento local:

| Software | Descrição | Links de download |
|---|---|---|
| ADOBE EXPERIENCE MANAGER AS A CLOUD SERVICE SDK | O SDK inclui [!DNL Adobe Experience Manager] Ferramentas do QuickStart e do Dispatcher | Baixe o SDK mais recente em [Distribuição de software](#software-distribution) |  |
| Arquivo de recursos do Adobe Experience Manager Forms (complemento do AEM Forms) | Ferramentas para criar, estilizar e otimizar o Adaptive Forms e outros recursos do Adobe Experience Manager Forms | Baixar de [Distribuição de software](#software-distribution) |
| (Opcional) Conteúdo de referência do Adobe Experience Manager Forms | Ferramentas para criar, estilizar e otimizar o Adaptive Forms e outros recursos do Adobe Experience Manager Forms | Baixar de [Distribuição de software](#software-distribution) |
| (Opcional) Adobe Experience Manager Forms Designer | Ferramentas para criar, estilizar e otimizar o Adaptive Forms e outros recursos do Adobe Experience Manager Forms | Baixar de [Distribuição de software](#software-distribution) |

### Baixar a versão mais recente do software da Distribuição de software {#software-distribution}

Para baixar a versão mais recente do SDK do Adobe Experience Manager as a Cloud Service, o arquivo de recursos do Experience Manager Forms (complemento do AEM Forms), os ativos de referência de formulários ou o Forms Designer no [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html):

1. Efetue logon no <https://experience.adobe.com/#/downloads> com o seu Adobe ID

   >[!NOTE]
   >
   > Sua organização de Adobe deve ser provisionada para o AEM as a Cloud Service AEM as a Cloud Service baixar o SDK do.

1. Navegue até a **[!UICONTROL AEM as a Cloud Service]** guia.
1. Classifique por data de publicação em ordem decrescente.
1. Clique no Adobe Experience Manager as a Cloud Service SDK mais recente, no arquivo de recursos do Experience Manager Forms (complemento do AEM Forms), nos ativos de referência de formulários ou no Forms Designer.
1. Revise e aceite o EULA. Clique no botão **[!UICONTROL Baixar]**.

## Configurar ferramentas de desenvolvimento para Projetos AEM {#setup-development-tools-for-AEM-projects}

O projeto do Adobe Experience Manager Forms é uma base de código personalizada. Ele contém código, configurações e conteúdo que são implantados por meio do Cloud Manager para [!DNL Adobe Experience Manager] as a Cloud Service. A variável [Arquétipo Maven do projeto AEM](https://github.com/adobe/aem-project-archetype) O fornece a estrutura de linha de base para o projeto.

Configure as seguintes ferramentas de desenvolvimento para usar no [!DNL Adobe Experience Manager] projeto de desenvolvimento:

* [Java™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up)
* [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git)
* [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js)
* [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven)

Para obter instruções detalhadas sobre como configurar as ferramentas de desenvolvimento mencionadas anteriormente, consulte [Configurar ferramentas de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html).

## Configurar o ambiente de Experience Manager local para desenvolvimento

O SDK do Cloud Service fornece um arquivo QuickStart. Ele executa uma versão local do Experience Manager. Execute as instâncias Autor ou Publicar localmente.

Embora o QuickStart forneça uma experiência de desenvolvimento local, ele não tem todos os recursos disponíveis no [!DNL Adobe Experience Manager] as a Cloud Service. Assim, sempre teste seus recursos e código com [!DNL Adobe Experience Manager] Ambiente de desenvolvimento as a Cloud Service antes de mover os recursos para o estágio ou produção.

Para instalar e configurar o ambiente de Experience Manager local, execute as seguintes etapas:

* [Baixar e extrair](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) o [!DNL Adobe Experience Manager] AS A CLOUD SERVICE SDK
* [Configurar uma instância de autor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-author-service)
* [Configurar uma instância de publicação](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-publish-service)

## Adicionar arquivo do Forms às instâncias locais de Autor e Publicação e configurar usuários específicos do Forms {#add-forms-archive-configure-users}

Execute as seguintes etapas na ordem listada para adicionar o arquivo Forms às instâncias Experience Manager e configurar usuários específicos de formulários:

### Instale o arquivo de recursos complementares mais recente do Forms {#add-forms-archive}

O arquivo de recursos as a Cloud Service do Adobe Experience Manager Forms fornece ferramentas para criar, estilizar e otimizar o Adaptive Forms no ambiente de desenvolvimento local. Instale o pacote para criar um Formulário adaptável e usar vários outros recursos do [!DNL AEM Forms]. Para instalar o pacote:

1. Baixe e extraia a versão mais recente [!DNL AEM Forms] arquive para seu sistema operacional em [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

1. Navegue até o diretório crx-quickstart/install. Caso a pasta não exista, crie-a.

1. Interrompa a instância do AEM, coloque o [!DNL AEM Forms] arquivo de recursos complementar, `aem-forms-addon-<version>.far`, na pasta de instalação.
1. Vá para a janela de comando ativa e pressione `Ctrl + C` para reiniciar o SDK.

   >[!NOTE]
   >
   > É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

### Configurar usuários e permissões {#configure-users-and-permissions}

Crie usuários como Desenvolvedor de formulários e Profissional de formulários e [adicionar esses usuários a grupos de formulários predefinidos](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=en#accessing) para fornecer as permissões necessárias. A tabela abaixo lista todos os tipos de usuários e grupos predefinidos para cada tipo de usuários de formulários:

| Tipo de usuário | Grupo AEM |
|---|---|
| Profissional de formulários / | [!DNL forms-users] (Usuários do AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors], e [!DNL fdm-authors] |
| Desenvolvedor de formulários | [!DNL forms-users] (Usuários do AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors], e [!DNL fdm-authors] |
| Líder de experiência do cliente ou designer de UX | [!DNL forms-users], [!DNL template-authors] |
| Administrador do AEM | [!DNL aem-administrators], [!DNL fd-administrators] |
| Usuário final | Quando um usuário precisar fazer logon para exibir e enviar um Formulário adaptável, adicione esses usuários a [!DNL forms-users] grupo. </br> Quando nenhuma autenticação de usuário for necessária para acessar o Adaptive Forms, não atribua nenhum grupo a esses usuários. |

<!--  

## Set up a local AEM instance for development

Perform the following steps in the listed order to set up and configure your local development environment:

1. **Set up an AEM author instance:** You require an author instance to create Adaptive Forms. Download and extract the latest AEM SDK archive. Run the quick start file in author run mode to set up an author instance. For detailed instructions, see [default local instance](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html).  

1. **Install the latest [!DNL AEM Forms] add-on feature archive:** [!DNL AEM Forms] add-on feature archive provides tools to create, style, and optimize Adaptive Forms on the local development environment. Install the package to create an Adaptive Form and use various other features of [!DNL AEM Forms]. To install the package:

    1. Download and extract the latest [!DNL AEM Forms] archive for your operating system from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

    1. Navigate to the crx-quickstart/install directory. If the folder does not exist, create it.

    1. Stop your Cloud ready AEM instance, place the [!DNL AEM Forms] add-on feature archive, `aem-forms-addon-<version>.far`,  in the install folder, and restart the instance.

1. **Configure users and permissions:** Create users like Form Developer and Form Practitioner a nd add these users to pre-defined forms group to provide them required permissions. The table below lists all types of users and pre-defined groups for each type of forms users:
  
    | User Type | AEM Group |
    |---|---|
    | Form Practitioner  | forms-users (AEM Forms Users), template-authors  |
    | Form Developer | forms-users (AEM Forms Users), template-authors |
    | End-User| everyone* |

    `*` When a user should log in to access or submit Adaptive Forms, add such users to the everyone group.  -->

<!--    
### Set up an AEM project for the development tasks related to local AEM 6.5.5 Forms instance

Use this project to update configurations, create overlays, develop custom Adaptive Form components, and custom code using the local development environment. To set up the project:

1. **Install and configure Maven and set up an AEM project based on Apache Maven:** Apache Maven is an open-source tool for managing software projects. It helps automate builds and provides quality project information. It is the recommended build management tool for AEM projects. For detailed instructions to set up an AEM project based on Apache Maven, see [How to Build AEM Projects using Apache Maven](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/ht-projects-maven.html).

1. Configure the project to use [uber-jar](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=en#install-aem-forms-jee-installer) version 6.5.5 or later and [[!DNL AEM Forms] Client SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/) version 6.0.160 or later.  

1. **Set Up an Integrated Development Environment:**  Set up an IDE of your choice for development, see [Set Up an Integrated Development Environment](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) for detailed instructions.
 -->

## Configurar o ambiente de desenvolvimento local para o Documento de registro (DoR){#docker-microservices}

O AEM Forms as a Cloud Service fornece um ambiente de SDK baseado em docker para facilitar o desenvolvimento do Documento de registro e o uso de outros microsserviços. Isso libera você da configuração manual de binários e adaptações específicos da plataforma. Para configurar o ambiente:

1. Instalar e configurar o Docker:

   * (Para Microsoft® Windows) Instalar [Desktop Docker](https://www.docker.com/products/docker-desktop). Ele configura `Docker Engine` e `docker-compose` na sua máquina.

   * Instalação do (Apple macOS) [Desktop Docker para Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac). Ele inclui Docker Engine, cliente Docker CLI, Docker Compose, Docker Content Trust, Kubernetes e Credential Helper.

   * (Para Linux®) Instalar [Mecanismo do Docker](https://docs.docker.com/engine/install/#server) e [Composição do Docker](https://docs.docker.com/compose/install/) na sua máquina.

   >[!NOTE]
   >
   > * Para o Apple macOS, o incluir na lista de permissões AEM pastas que contêm instâncias locais do Autor.
   >
   > * O Docker Desktop para Windows suporta dois back-ends, Hyper-V
   > (herdado) e WSL2 (moderno). O compartilhamento de arquivos é automaticamente
   > gerenciado pelo Docker ao usar o WSL2 (moderno). Você precisa
   > configure explicitamente o compartilhamento de arquivos ao usar o Hyper-V (herdado).

1. Crie uma pasta, digamos o aem-sdk, em paralelo às instâncias de autor e publicação. Por exemplo, C:\aem-sdk.

1. Extraia o `aem-forms-addon-<version>.zip\aem-forms-addon-native-<version>.zip` arquivo.

   ![complemento extraído do aem forms nativo](assets/microservice-docker.png)

1. Crie uma variável de ambiente AEM_HOME e aponte para a instalação local do AEM Author. Por exemplo, C:\aem\author\.

1. Abra sdk.bat ou sdk.sh para edição. Defina AEM_HOME para apontar para a instalação local do AEM Author. Por exemplo, C:\aem\author\.

1. Abra o prompt de comando e navegue até o `aem-forms-addon-native-<version>` pasta.

1. Certifique-se de que a instância local do autor do AEM esteja ativa e em execução. Execute o seguinte comando para iniciar o SDK:

   * (no Microsoft® Windows) `sdk.bat start`
   * (no Linux® ou Apple macOS) `AEM_HOME=[local AEM Author installation] ./sdk.sh start`

   >[!NOTE]
   >
   > Se você tiver definido a variável de ambiente no arquivo sdk.sh, especificá-la na linha de comando é opcional. A opção para definir a variável de ambiente na linha de comando é fornecida para executar o comando sem atualizar o script de shell.

   ![start-sdk-command](assets/start-sdk.png)

Agora você pode usar o ambiente de desenvolvimento local para renderizar o Documento de registro. Para testar, carregue um arquivo XDP no seu ambiente e renderize-o. Por exemplo, <http://localhost:4502/libs/xfaforms/profiles/default.print.pdf?template=crx:///content/dam/formsanddocuments/cheque-request.xdp> converte o arquivo XDP para o documento PDF.

## Configurar um projeto de desenvolvimento para o Forms com base no arquétipo de Experience Manager {#forms-cloud-service-local-development-environment}

Use este projeto para criar o Adaptive Forms, implantar atualizações de configuração, sobreposições, criar componentes de Formulário adaptável personalizados, testar e personalizar código no local [!DNL Experience Manager Forms] SDK. Após os testes locais, é possível implantar o projeto em  [!DNL Experience Manager Forms] Ambientes as a Cloud Service de produção e não produção. Quando você implanta o projeto, os seguintes ativos do AEM Forms também são implantados:

| Temas | Modelos | Modelos de dados de formulário |
---------|----------|---------
| Canvas 3.0 | Básico | Microsoft® Dynamics 365 |
| Tranquilo | Em branco | Salesforce |
| Urbana |   |  |
| Ultramarina |  |  |
| Berilo |  |  |

>[!NOTE]
>
> Configure o projeto baseado no Arquétipo AEM versão 30 ou posterior para obter e usar os modelos de dados de formulário do Microsoft® Dynamics 365 e Salesforce com o AEM Forms as a Cloud Service.
> Configure o Arquétipo AEM versão 32 ou posterior do projeto para obter e usar temas Tranquil, Urbane e Ultramarine com o AEM Forms as a Cloud Service.

Para configurar o projeto:

1. **Clonar o repositório Git do Cloud Manager na instância de desenvolvimento local:**  Seu repositório Git do Cloud Manager contém um projeto AEM padrão. Baseia-se no [Arquétipo AEM](https://github.com/adobe/aem-project-archetype/). Clonar o Repositório Git do Cloud Manager usando o Gerenciamento de conta Git por autoatendimento da interface do usuário do Cloud Manager para trazer o projeto para o ambiente de desenvolvimento local. Para obter detalhes sobre o acesso ao repositório, consulte [Acessar repositórios](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

<!-- 1. 
After the repository is cloned, [integrate your Git repo with Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)

**Make cloned AEM project compatible with [!DNL AEM Forms] as a Cloud Service:** Remove uber-jar and other non-cloud dependencies from the pom.xml files of the project. You can refer the pom.xml files of the [sample AEM project](assets/FaaCSample.zip) for the list of required dependencies and update your AEM project accordingly. You can also refer [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html) to learn changes required to make an AEM project compatible with AEM as a Cloud Service.  -->

1. **Criar um [!DNL Experience Manager Forms] as a [Cloud Service] projeto:** Criar um [!DNL Experience Manager Forms] as a [Cloud Service] projeto com base no mais recente [Arquétipo AEM](https://github.com/adobe/aem-project-archetype) ou posteriormente. O arquétipo ajuda os desenvolvedores a iniciar o desenvolvimento facilmente para [!DNL AEM Forms] as a Cloud Service. Ele também inclui alguns exemplos de temas e modelos para ajudá-lo a começar rapidamente.

   Abra o prompt de comando e execute o comando abaixo para criar uma [!DNL Experience Manager Forms] as a Cloud Service projeto.

   ```shell
   mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="41" -D appTitle=mysite -D appId=mysite -D groupId=com.mysite -D includeFormsenrollment="y" -D aemVersion="cloud"
   ```

   Altere o `appTitle`, `appId`, e `groupId` no comando acima para refletir seu ambiente. Além disso, defina o valor de includeFormsenrollment, includeFormscommunications e includeFormsheadless como `y` ou `n` dependendo da sua licença e dos requisitos. Incluir Formsheadless é obrigatório para criar o Forms adaptável com base nos Componentes principais.

   * Use o `includeFormsenrollment=y` opção para incluir configurações específicas do Forms, temas, modelos, Componentes principais e dependências necessárias para criar o Adaptive Forms. Se você usa o Forms Portal, defina a variável `includeExamples=y` opção. Ele também adiciona os componentes principais do Forms Portal ao projeto.

   * Use o `includeFormscommunications=y` opção para incluir os Componentes principais do Forms e as dependências necessárias para incluir a funcionalidade Comunicações do cliente.

     >[!WARNING]
     >
     >* Ao criar um projeto do Arquétipo com a versão 45, a variável [Pasta de projeto do arquétipo AEM]/pom.xml define inicialmente a versão dos componentes principais de formulários como 2.0.64. Antes de criar ou implantar o projeto Arquétipo, atualize a versão dos componentes principais de formulários para 2.0.62.

1. Implante o projeto no ambiente de desenvolvimento local. Você pode usar o comando a seguir para implantar no ambiente de desenvolvimento local

   `mvn -PautoInstallPackage clean install`

   Para obter a lista completa de comandos, consulte [Criação e instalação](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Implante o código no seu [!DNL AEM Forms] ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Configurar ferramentas locais do Dispatcher {#setup-local-dispatcher-tools}

O Dispatcher é um módulo de servidor Web Apache HTTP que fornece uma camada de segurança e desempenho entre a camada de publicação CDN e AEM. O Dispatcher é parte integral da arquitetura Experience Manager geral e deve fazer parte do ambiente de desenvolvimento local.

Execute as seguintes etapas para configurar o Dispatcher local e, em seguida, adicionar regras específicas do Forms a ele:

### Configurar o Dispatcher local {#setup-local-dispatcher}

A variável [!DNL Experience Manager] O SDK as a Cloud Service inclui a versão recomendada das Ferramentas do Dispatcher que facilita a configuração, validação e simulação do Dispatcher localmente. As Ferramentas do Dispatcher são baseadas em Docker e fornecem ferramentas de linha de comando para transcompilar arquivos de configuração do Apache HTTP Web Server e do Dispatcher em um formato compatível e implantá-los no Dispatcher em execução no contêiner Docker.

O armazenamento em cache no Dispatcher permite [!DNL AEM Forms] para preencher previamente o Adaptive Forms em um cliente. Ele melhora a velocidade de renderização de formulários pré-preenchidos.

Para obter instruções detalhadas sobre como configurar o Dispatcher, consulte [Configurar ferramentas locais do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#local-development-environment-set-up)

### Adicionar regras específicas do Forms ao Dispatcher {#forms-specific-rules-to-dispatcher}

Execute as seguintes etapas para configurar o cache do Dispatcher para o Experience Manager Forms as a Cloud Service:

1. Abra o projeto AEM e acesse `\src\conf.dispatcher.d\available_farms`
1. Crie uma cópia do `default.farm` arquivo. Por exemplo, `forms.farm`.
1. Abra o criado `forms.farm` para editar e substituir o seguinte código:

   ```json
   #/ignoreUrlParams {
   #/0001 { /glob "*" /type "deny" }
   #/0002 { /glob "q" /type "allow" }
   #}
   ```

   com

   ```json
   /ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   /0002 { /glob "dataRef" /type "allow" }
   }
   ```

1. Salve e feche o arquivo.
1. Ir para `conf.d/enabled_farms` e criar um link simbólico para o `forms.farm` arquivo.
1. Compile e implante o projeto em seu [!DNL AEM Forms] ambiente as a Cloud Service.

### Considerações sobre armazenamento em cache {#considerations-about-caching}

* O armazenamento em cache do Dispatcher permite [!DNL AEM Forms] para preencher previamente o Adaptive Forms em um cliente. Ele melhora a velocidade de renderização de formulários pré-preenchidos.
* O armazenamento em cache de recursos de conteúdo protegido está desativado, por padrão. Para ativar o recurso, você pode executar as instruções fornecidas no [Armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=en) artigo
* O Dispatcher pode falhar ao invalidar alguns Forms adaptáveis e Forms adaptáveis relacionados. Para resolver esses problemas, consulte [[!DNL AEM Forms] Armazenamento em cache](troubleshooting-caching-performance.md) na seção solução de problemas.
* Armazenamento em cache do Adaptive Forms localizado:
   * Usar formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um Formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * A opção Local do navegador está desativada, por padrão. Para alterar a configuração do local do navegador,
* Quando você usa o formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`e Usar localidade do navegador no gerenciador de configurações estiver desativado, a versão não localizada do Formulário adaptável será fornecida. O idioma não localizado é o idioma usado ao desenvolver o Formulário adaptável. A localidade configurada para seu navegador (localidade do navegador) não é considerada e uma versão não localizada do Formulário adaptável é fornecida.
* Quando você usa o formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`e Usar localidade do navegador no gerenciador de configurações estiver ativado, uma versão localizada do Formulário adaptável será fornecida, se disponível. O idioma do Formulário adaptável localizado se baseia no local configurado para seu navegador (local do navegador). Pode levar a [armazenamento em cache somente da primeira instância de um Formulário adaptável]. Para evitar que o problema ocorra na sua instância, consulte [somente a primeira instância de um Formulário adaptável é armazenada em cache](troubleshooting-caching-performance.md) na seção solução de problemas.

O ambiente de desenvolvimento local está pronto.

## Habilitar os componentes principais de formulários adaptáveis no AEM Forms as a Cloud Service e no ambiente de desenvolvimento local

A ativação dos componentes principais adaptáveis do Forms no AEM Forms as a Cloud Service permite que você comece a criar, publicar e fornecer componentes principais com base no Adaptive Forms e no Headless Forms, usando as instâncias do Cloud Service da AEM Forms para vários canais. Você precisa do ambiente habilitado dos Componentes principais adaptáveis do Forms para usar o Forms adaptável headless.

Para obter instruções, consulte [Ativar os Componentes principais adaptáveis do Forms no ambiente de desenvolvimento as a Cloud Service e local do AEM Forms](/help/forms/enable-adaptive-forms-core-components.md)


## Atualizar o ambiente de desenvolvimento local {#upgrade-your-local-development-environment}

Atualizar o SDK para uma nova versão requer a substituição de todo o ambiente de desenvolvimento local, resultando na perda de todo o código, configuração e conteúdo nos repositórios locais. Verifique se qualquer código, configuração ou conteúdo que não deve ser destruído foi confirmado com segurança no Git ou exportado das instâncias de Experience Manager locais como Pacotes CRX.

### Como evitar perda de conteúdo ao atualizar o SDK {#avoid-content-loss-when-upgrading--SDK}

A atualização do SDK está efetivamente criando uma nova instância de Autor e Publicação, incluindo um novo repositório ([Configurar projeto do AEM](#forms-cloud-service-local-development-environment)), o que significa que as alterações feitas no repositório de um SDK anterior são perdidas. Para obter estratégias viáveis para ajudar a criar conteúdo persistente entre as atualizações do SDK, consulte [Como evitar perda de conteúdo ao atualizar o SDK do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#optional-local-aem-runtime-set-up-tasks)

<!--When you update any  Forms-specifc configuration, create overlays, develop custom Adaptive Form components, or develop and test any custom code in AEM project for the development tasks related to local development instance, use the AEM project cloned from the Cloud Manager Git repository to [deploy the custom code and other changes to your [!DNL AEM Forms] as a Cloud Service's production or non-production environment](https://video.tv.adobe.com/v/30191?quality=9).

## Upgrade your local development environment {#update-local-setup}

Update the local AEM setup (AEM SDK) to latest version at least monthly on, or shortly after, the last Thursday of each month, which is the release cadence for AEM as a Cloud Service "feature releases". You can download local AEM SDK from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

Updating the AEM SDK to a new version requires replacing the entire local development environment, resulting in a loss of all code, configuration and content in the local AEM repositories. Ensure that any code, config or content that should not be destroyed is safely committed to Git, or exported from the local AEM instance as AEM Packages.

### How to avoid content loss when upgrading the AEM SDK {#avoid-content-loss-when-upgrading--AEM-SDK}

Upgrading the AEM SDK is effectively creating a brand new AEM runtime ([Set up a local AEM instance](setup-forms-cloud-service.md)), including a new repository ([Set up AEM project](#forms-cloud-service-local-development-environment)), meaning any changes made to a prior AEM SDK's repository are lost. The following are viable strategies for aiding in persisting content between AEM SDK upgrades, and can be used discretely or in concert:

1. Create a content package dedicated to containing the sample content to aid in development and maintain it in Git. Any content that should be persisted through AEM SDK upgrades would be persisted into this package and re-deployed after upgrading the AEM SDK.
1. Use [oak-upgrade](https://jackrabbit.apache.org/oak/docs/migration.html) with the `includepaths` directive, to copy content from the prior AEM SDK repository to the new AEM SDK repository.
1. Back up any content using AEM Package Manager and content packages on the prior AEM SDK and re-install them on the new AEM SDK.

Remember, using the above approaches to maintain code between AEM SDK upgrades, indicates a development anti-pattern. Non-disposable code should originate in your Development IDE and flow into AEM SDK via deployments.

For information about troubleshooting, stopping local AEM environment, run modes, and deployment, see [Set up local AEM Runtime](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#local-development-environment-set-up).-->

### Fazer backup e importar conteúdo específico do Forms para um novo ambiente de SDK {#backup-and-import-Forms-specific-content-to-new-SDK-environment}

Para fazer backup e mover ativos do SDK existente para um novo ambiente de SDK:

* Crie um backup do conteúdo existente.

* Configure um novo ambiente do SDK.

* Importe o backup para o novo ambiente do SDK.

### Criar um backup do conteúdo existente {#create-backup-of-your-existing-content}

Faça backup de seu Forms adaptável, modelos, modelo de dados de formulário, tema, configurações e código personalizado. Você pode executar a seguinte ação para criar o backup:

1. [Baixar](import-export-forms-templates.md#manage-forms-and-related-assets) Forms adaptável, temas e PDF forms.
1. Exportar modelos de formulário adaptável.

1. Baixar modelos de dados do formulário

1. Exportar modelos editáveis, configurações de nuvem e modelo de fluxo de trabalho. Para exportar todos os itens mencionados anteriormente do SDK existente, crie um [Pacote CRX](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html) com os seguintes filtros:

   * /conf/ReferenceEditableTemplates
   * /conf/global/settings/cloudconfigs
   * /conf/global/settings/wcm
   * /var/workflow/models
   * /conf/global/settings/workflow
1. Exporte configurações de email, envie e preencha previamente o código de ações de seu ambiente de desenvolvimento local. Para exportar essas configurações, crie uma cópia das seguintes pastas e arquivos no ambiente de desenvolvimento local:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

### Importe o backup para o novo ambiente do SDK {#import-the-backup-to-your-new-SDK-environment}

Importe o Adaptive Forms, modelos, modelo de dados de formulário, tema, configurações e código personalizado para seu ambiente atualizado. Execute a seguinte ação para importar o backup:

1. [Importar](import-export-forms-templates.md#manage-forms-and-related-assets) Forms adaptável, temas e PDF forms para novos ambientes do SDK.
1. Importar modelos de formulário adaptável para o novo ambiente do SDK.

1. Fazer upload de modelos de dados de formulário para o novo ambiente do SDK.

1. Importar modelos editáveis, configurações de nuvem e modelo de fluxo de trabalho. Para importar todos os itens mencionados anteriormente para o novo ambiente do SDK, importe o pacote CRX que contém esses itens para o novo ambiente do SDK.

1. Importe configurações de email, envie e preencha previamente o código de ações do seu ambiente de desenvolvimento local. Para importar essas configurações, coloque os seguintes arquivos do seu antigo projeto do Arquétipo para o seu novo projeto do Arquétipo:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

Seu novo ambiente agora tem formulários e ativos relacionados do ambiente antigo.
