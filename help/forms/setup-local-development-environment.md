---
title: Configurar um ambiente de desenvolvimento local para o Adobe Experience Manager Forms as a Cloud Service
description: Configurar um ambiente de desenvolvimento local para o Adobe Experience Manager Forms as a Cloud Service
exl-id: 12877a77-094f-492a-af58-cffafecf79ae
source-git-commit: a1b186fec2d6de0934ffebc96967d36a967c044e
workflow-type: tm+mt
source-wordcount: '3042'
ht-degree: 4%

---

# Configurar um ambiente de desenvolvimento local e um projeto de desenvolvimento inicial {#overview}

Ao configurar e configurar um [!DNL  Adobe Experience Manager Forms] como [!DNL  Cloud Service] , você configura ambientes de desenvolvimento, armazenamento temporário e produção na nuvem. Além disso, também é possível configurar e configurar um ambiente de desenvolvimento local.

Você pode usar o ambiente de desenvolvimento local para executar as seguintes ações sem fazer logon no ambiente de desenvolvimento de nuvem:

* [Criar formulários](creating-adaptive-form.md) e ativos relacionados (temas, modelos, ações de envio personalizadas e muito mais)
* [Converter formulários PDF em formulários adaptáveis](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html?lang=pt-BR)
* Criar aplicativos para gerar [Comunicações do cliente](aem-forms-cloud-service-communications-introduction.md) sob demanda ou em modos de lote.

Depois que um formulário adaptável ou ativos relacionados estiverem prontos na instância de desenvolvimento local ou em um aplicativo para gerar [Comunicações do cliente] estiver pronto, você pode exportar o aplicativo Adaptive Form ou Customer Communications do ambiente de desenvolvimento local para um ambiente Cloud Service para testes adicionais ou para ambientes de produção.

Você também pode desenvolver e testar código personalizado, como componentes personalizados e serviços de preenchimento prévio no ambiente de desenvolvimento local. Quando o código personalizado é testado e pronto, você pode usar o repositório Git do ambiente de desenvolvimento do Cloud Service para implantar o código personalizado.

Para configurar um novo ambiente de desenvolvimento local e usá-lo para desenvolver atividades, execute as seguintes ações na ordem listada:

* [Configurar ferramentas de desenvolvimento](#setup-development-tools-for-AEM-projects)

* [Configurar instâncias locais de Autor e Publicação](#set-up-local-experience-manager-environment-for-development)

* [Adicionar o arquivo Forms às instâncias de desenvolvimento local e configurar usuários](#add-forms-archive-configure-users)

* [Configurar o ambiente de desenvolvimento local para microsserviços](#docker-microservices)

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

Você precisa do seguinte software para configurar um ambiente de desenvolvimento local. Baixe antes de começar a configurar o ambiente de desenvolvimento local:

| Software | Descrição | Links de download |
|---|---|---|
| Adobe Experience Manager as a Cloud Service SDK | O SDK inclui [!DNL Adobe Experience Manager] Ferramentas do QuickStart e do Dispatcher | Baixe o SDK mais recente em [Distribuição de software](#software-distribution) |  |
| Arquivo de recursos do Adobe Experience Manager Forms (complemento AEM Forms) | Ferramentas para criar, estilizar e otimizar o Adaptive Forms e outros recursos do Adobe Experience Manager Forms | Baixar de [Distribuição de software](#software-distribution) |
| (Opcional) Conteúdo de referência do Adobe Experience Manager Forms | Ferramentas para criar, estilizar e otimizar o Adaptive Forms e outros recursos do Adobe Experience Manager Forms | Baixar de [Distribuição de software](#software-distribution) |
| (Opcional) Adobe Experience Manager Forms Designer | Ferramentas para criar, estilizar e otimizar o Adaptive Forms e outros recursos do Adobe Experience Manager Forms | Baixar de [Distribuição de software](#software-distribution) |

### Faça o download da versão mais recente do software na Distribuição de software {#software-distribution}

Para baixar a versão mais recente do SDK do Adobe Experience Manager as a Cloud Service, o arquivo de recursos do Experience Manager Forms (complemento AEM Forms), os ativos de referência de formulários ou o Forms Designer de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html):

1. Faça logon em <https://experience.adobe.com/#/downloads> com sua Adobe ID

   >[!NOTE]
   >
   > Sua organização do Adobe deve ser provisionada para AEM as a Cloud Service baixar o SDK as a Cloud Service AEM.

1. Navegue até o **[!UICONTROL AEM as a Cloud Service]** guia .
1. Classifique por data publicada em ordem decrescente.
1. Clique no SDK do Adobe Experience Manager as a Cloud Service mais recente, no arquivo de recursos do Experience Manager Forms (complemento AEM Forms), nos ativos de referência de formulários ou no Forms Designer.
1. Revise e aceite o EULA. Toque no **[!UICONTROL Baixar]** botão.

## Configurar ferramentas de desenvolvimento para Projetos AEM {#setup-development-tools-for-AEM-projects}

O projeto do Adobe Experience Manager Forms é uma base de código personalizada. Ele contém código, configurações e conteúdo que são implantados via Cloud Manager no [!DNL Adobe Experience Manager] as a Cloud Service. O [Arquétipo de Maven do Projeto AEM](https://github.com/adobe/aem-project-archetype) fornece a estrutura de base do projeto.

Configure as seguintes ferramentas de desenvolvimento para usar em seu [!DNL Adobe Experience Manager] projeto de desenvolvimento:

* [Java™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up)
* [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git)
* [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js)
* [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven)

Para obter instruções detalhadas para configurar as ferramentas de desenvolvimento mencionadas anteriormente, consulte [Configurar ferramentas de desenvolvimento](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html).

## Configurar o ambiente Experience Manager local para desenvolvimento

O SDK do Cloud Service fornece um arquivo QuickStart . Ela executa uma versão local do Experience Manager. Você pode executar as instâncias Autor ou Publicação localmente.

Embora o QuickStart forneça uma experiência de desenvolvimento local, ele não tem todos os recursos disponíveis em [!DNL Adobe Experience Manager] as a Cloud Service. Portanto, sempre teste seus recursos e código com [!DNL Adobe Experience Manager] Ambiente de desenvolvimento as a Cloud Service antes de mover os recursos para o estágio ou produção.

Para instalar e configurar o ambiente Experience Manager local, execute as seguintes etapas:

* [Baixar e extrair](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) o [!DNL Adobe Experience Manager] SDK as a Cloud Service
* [Configurar uma instância do autor](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-author-service)
* [Configurar uma instância de publicação](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#set-up-local-aem-publish-service)

## Adicione o arquivo Forms às instâncias de Autor e Publicação locais e configure usuários específicos do Forms {#add-forms-archive-configure-users}

Execute as seguintes etapas na ordem listada para adicionar o arquivo Forms às instâncias do Experience Manager e configurar usuários específicos de formulários:

### Instale o arquivo de recursos complementares mais recente do Forms {#add-forms-archive}

O arquivo as a Cloud Service de recursos do Adobe Experience Manager Forms fornece ferramentas para criar, estilizar e otimizar o Adaptive Forms no ambiente de desenvolvimento local. Instale o pacote para criar um formulário adaptável e usar vários outros recursos do [!DNL AEM Forms]. Para instalar o pacote:

1. Baixe e extraia a versão mais recente [!DNL AEM Forms] arquivar para seu sistema operacional a partir de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

1. Navegue até o diretório crx-quickstart/install. Se a pasta não existir, crie-a.

1. Pare a instância do AEM, coloque a variável [!DNL AEM Forms] arquivo de recursos complementares, `aem-forms-addon-<version>.far`, na pasta install e reinicie a instância.

### Configurar usuários e permissões {#configure-users-and-permissions}

Crie usuários como o desenvolvedor de formulários e o profissional de formulários e [adicionar esses usuários a grupos de formulários predefinidos](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=en#accessing) para fornecer as permissões necessárias. A tabela abaixo lista todos os tipos de usuários e grupos predefinidos para cada tipo de usuário de formulários:

| Tipo de usuário | Grupo AEM |
|---|---|
| Administrador de formulários / | [!DNL forms-users] (Usuários do AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors]e [!DNL fdm-authors] |
| Desenvolvedor de formulários | [!DNL forms-users] (Usuários do AEM Forms), [!DNL template-authors], [!DNL workflow-users], [!DNL workflow-editors]e [!DNL fdm-authors] |
| Cliente Experience Lead ou UX Designer | [!DNL forms-users], [!DNL template-authors] |
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

O AEM Forms as a Cloud Services fornece um ambiente SDK baseado em docker para facilitar o desenvolvimento do Documento de registro e o uso de outros microsserviços. Ele libera a configuração manual de binários e adaptações específicas da plataforma. Para configurar o ambiente:

1. Instalar e configurar o Docker:

   * Instalação (para Microsoft® Windows) [Desktop Docker](https://www.docker.com/products/docker-desktop). Ele configura `Docker Engine` e `docker-compose` na sua máquina.

   * Instalação do (Apple macOS) [Desktop Docker para Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac). Ele inclui o Docker Engine, o cliente da CLI Docker, o Docker Compose, a Docker Content Trust, os Kubernetes e o Credential Helper.

   * Instalação (para Linux®) [Mecanismo de docking station](https://docs.docker.com/engine/install/#server) e [Composição do Docker](https://docs.docker.com/compose/install/) na sua máquina.
   >[!NOTE]
   >
   > * Para o Apple macOS, lista de permissões pastas de  contendo instâncias locais do AEM Author.
   >
   > * O Docker Desktop para Windows suporta dois backends, Hyper-V
      > (herdado) e WSL2 (moderno). O compartilhamento de arquivos é automático
      > gerenciado pela Docker ao usar o WSL2 (moderno). Você tem que
      > configure explicitamente o compartilhamento de arquivos ao usar o Hyper-V (herdado).


1. Crie uma pasta, por exemplo, aem-sdk, em paralelo às instâncias de autor e publicação. Por exemplo C:\aem-sdk.

1. Extraia o `aem-forms-addon-<version>.zip\aem-forms-addon-native-<version>.zip` arquivo.

   ![o aem forms extraído adiciona nativo](assets/microservice-docker.png)

1. Crie uma variável de ambiente AEM_HOME e aponte para a instalação local do AEM Author. Por exemplo C:\aem\author\.

1. Abra o sdk.bat ou sdk.sh para edição. Defina o AEM_HOME para apontar para a instalação local do AEM Author. Por exemplo C:\aem\author\.

1. Abra o prompt de comando e navegue até o `aem-forms-addon-native-<version>` pasta.

1. Certifique-se de que a instância local do autor do AEM esteja ativa e em execução. Execute o seguinte comando para iniciar o SDK:

   * (no Microsoft® Windows) `sdk.bat start`
   * (no Linux® ou Apple macOS) `AEM_HOME=[local AEM Author installation] ./sdk.sh start`

   >[!NOTE]
   >
   > Se você tiver definido a variável de ambiente no arquivo sdk.sh , é opcional especificar na linha de comando. A opção para definir a variável de ambiente na linha de comando é fornecida para executar o comando sem atualizar o script de shell.

   ![start-sdk-command](assets/start-sdk.png)

Agora você pode usar o ambiente de desenvolvimento local para renderizar Documento de registro. Para testar, faça upload de um arquivo XDP no seu ambiente e renderize-o. Por exemplo, <http://localhost:4502/libs/xfaforms/profiles/default.print.pdf?template=crx:///content/dam/formsanddocuments/cheque-request.xdp> converte o arquivo XDP no documento PDF.

## Configurar um projeto de desenvolvimento para o Forms com base no arquétipo do Experience Manager {#forms-cloud-service-local-development-environment}

Use este projeto para criar o Adaptive Forms, implantar atualizações de configuração, sobreposições, criar componentes personalizados do Formulário adaptável, testar e código personalizado no local [!DNL Experience Manager Forms] SDK. Após testar localmente, você pode implantar o projeto no  [!DNL Experience Manager Forms] Ambientes as a Cloud Service de produção e não de produção. Ao implantar o projeto, os seguintes ativos da AEM Forms também são implantados:

| Temas | Modelos | Modelos de dados de formulário |
---------|----------|---------
| Tela 3.0 | Básico | Microsoft® Dynamics 365 |
| Tranquilo | Em branco | Salesforce |
| Urbane |  |  |
| Ultramarina |  |  |
| Beril |  |  |

>[!NOTE]
>
> Configure AEM projeto baseado no Archetype versão 30 ou posterior para obter e usar os Modelos de dados de formulário do Microsoft® Dynamics 365 e Salesforce com o AEM Forms as a Cloud Service.
Configure AEM projeto baseado no Archetype versão 32 ou posterior para obter e usar os temas Tranquil, Urbane e Ultramarine com o AEM Forms as a Cloud Service.

Para configurar o projeto:

1. **Repositório Git do Clone Cloud Manager na instância de desenvolvimento local:**  O repositório Git do Cloud Manager contém um projeto de AEM padrão. É baseado em [Arquétipo de AEM](https://github.com/adobe/aem-project-archetype/). Clone seu Repositório Git do Cloud Manager usando o Gerenciamento de conta Git de autoatendimento da interface do usuário do Cloud Manager para trazer o projeto para o ambiente de desenvolvimento local. Para obter detalhes sobre como acessar o repositório, consulte [Acessar repositórios](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

<!-- 1. 
After the repository is cloned, [integrate your Git repo with Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html)

**Make cloned AEM project compatible with [!DNL AEM Forms] as a Cloud Service:** Remove uber-jar and other non-cloud dependencies from the pom.xml files of the project. You can refer the pom.xml files of the [sample AEM project](assets/FaaCSample.zip) for the list of required dependencies and update your AEM project accordingly. You can also refer [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html) to learn changes required to make an AEM project compatible with AEM as a Cloud Service.  -->

1. **Crie um [!DNL Experience Manager Forms] como [Cloud Service] projeto:** Crie um [!DNL Experience Manager Forms] como [Cloud Service] projeto com base no mais recente [Arquétipo de AEM](https://github.com/adobe/aem-project-archetype) ou posterior. O arquétipo ajuda os desenvolvedores a começarem facilmente a desenvolver [!DNL AEM Forms] as a Cloud Service. Também inclui alguns temas e modelos de exemplo para ajudar você a começar rapidamente.

   Abra o prompt de comando e execute o comando abaixo para criar um [!DNL Experience Manager Forms] Projeto as a Cloud Service.

   ```shell
   mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="41" -D appTitle=mysite -D appId=mysite -D groupId=com.mysite -D includeFormsenrollment="y" -D aemVersion="cloud"
   ```

   Altere o `appTitle`, `appId`e `groupId` no comando acima para refletir seu ambiente. Além disso, defina o valor para includeFormsenrollment, includeFormscommunications e includeFormsheadless para `y` ou `n` dependendo da sua licença e das suas necessidades. O includeFormsheadless é obrigatório para criar o Adaptive Forms com base nos Componentes principais.

   * Use o `includeFormsenrollment=y` opção para incluir configurações, temas, modelos, Componentes principais e dependências específicas do Forms necessárias para criar o Adaptive Forms. Se você usar o Forms Portal, defina a variável `includeExamples=y` opção. Também adiciona os componentes principais do Forms Portal ao projeto.

   * Use o `includeFormscommunications=y` para incluir os Componentes principais do Forms e as dependências necessárias para incluir a funcionalidade de Comunicações do cliente.

1. Implante o projeto no ambiente de desenvolvimento local. Você pode usar o seguinte comando para implantar em seu ambiente de desenvolvimento local

   `mvn -PautoInstallPackage clean install`

   Para obter a lista completa de comandos, consulte [Criação e instalação](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Implante o código no [!DNL AEM Forms] Ambiente as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Configurar ferramentas locais do Dispatcher {#setup-local-dispatcher-tools}

O Dispatcher é um módulo de servidor Web Apache HTTP que fornece uma camada de segurança e desempenho entre a camada CDN e AEM Publish. O Dispatcher é parte integrante da arquitetura de Experience Manager geral e deve fazer parte do ambiente de desenvolvimento local.

Execute as seguintes etapas para configurar o Dispatcher local e, em seguida, adicionar regras específicas do Forms a ele:

### Configurar Dispatcher local {#setup-local-dispatcher}

O [!DNL Experience Manager] O SDK as a Cloud Service inclui a versão recomendada das Ferramentas do Dispatcher, que facilita a configuração, validação e simulação do Dispatcher localmente. As Ferramentas do Dispatcher são baseadas em Docker e fornecem ferramentas de linha de comando para transpor os arquivos de configuração do Apache HTTP Web Server e do Dispatcher em um formato compatível e implantá-los no Dispatcher em execução no container Docker.

O armazenamento em cache no Dispatcher permite [!DNL AEM Forms] para preencher previamente o Adaptive Forms em um cliente. Ele melhora a velocidade de renderização de formulários pré-preenchidos.

Para obter instruções detalhadas sobre como configurar o Dispatcher, consulte [Configurar ferramentas locais do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#local-development-environment-set-up)

### Adicionar regras específicas do Forms ao Dispatcher {#forms-specific-rules-to-dispatcher}

Execute as seguintes etapas para configurar o cache do Dispatcher para o Experience Manager Forms as a Cloud Service:

1. Abra o AEM Project e acesse `\src\conf.dispatcher.d\available_farms`
1. Crie uma cópia do `default.farm` arquivo. Por exemplo, `forms.farm`.
1. Abra o arquivo recém-criado `forms.farm` para editar e substituir o seguinte código:

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
1. Ir para `conf.d/enabled_farms` e criar um link simbólico para a `forms.farm` arquivo.
1. Compile e implante o projeto no seu [!DNL AEM Forms] Ambiente as a Cloud Service.

### Considerações sobre o armazenamento em cache {#considerations-about-caching}

* O armazenamento em cache do Dispatcher permite [!DNL AEM Forms] para preencher previamente o Adaptive Forms em um cliente. Ele melhora a velocidade de renderização de formulários pré-preenchidos.
* O armazenamento em cache de recursos de conteúdo protegido está desativado, por padrão. Para ativar o recurso, você pode executar as instruções fornecidas no [Armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=en) artigo
* O Dispatcher pode não conseguir invalidar algum Adaptive Forms e o Adaptive Forms relacionado. Para resolver esses problemas, consulte [[!DNL AEM Forms] Armazenamento em cache](troubleshooting-caching-performance.md) na seção solução de problemas.
* Armazenamento em cache do Forms adaptável localizado:
   * Usar formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Por padrão, a opção Localidade do navegador está desativada. Para alterar a configuração de local do navegador,
* Ao usar o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`e Usar Localidade do Navegador no gerenciador de configuração estiver desativado, a versão não localizada do Formulário Adaptável será exibida. O idioma não localizado é o idioma usado durante o desenvolvimento do Formulário adaptável. A localidade configurada para o seu navegador (localidade do navegador) não é considerada e uma versão não localizada do Formulário adaptável é disponibilizada.
* Ao usar o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`e Usar local do navegador no gerenciador de configuração estiver ativado, uma versão localizada do Formulário adaptável será exibida, se disponível. O idioma do formulário adaptável localizado é baseado na localidade configurada para seu navegador (localidade do navegador). Pode levar a [armazenamento em cache somente da primeira instância de um formulário adaptável]. Para evitar que o problema ocorra em sua instância, consulte [somente a primeira instância de um formulário adaptável é armazenada em cache](troubleshooting-caching-performance.md) na seção solução de problemas.

Seu ambiente de desenvolvimento local está pronto.

## Ativar os Componentes principais adaptáveis do Forms para um projeto existente baseado no arquétipo de AEM {#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project}

Se você estiver usando AEM programa baseado no Archetype versão 40 ou posterior para o AEM Forms as a Cloud Service, os Componentes principais serão ativados automaticamente para seu ambiente. Ao habilitar os componentes principais no seu ambiente, o modelo **Formulários adaptáveis (Componente principal)** e o tema da tela são adicionados ao seu ambiente. Se sua versão do SDK do AEM for anterior à 2023.02.0, [certifique-se de que`prerelease` o sinalizador esteja habilitado em seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=pt-BR#new-features), pois os componentes principais dos formulários adaptáveis faziam parte do pré-lançamento antes da versão 2023.02.0.

Para ativar os Componentes principais adaptáveis do Forms para o seu ambiente as a Cloud Service do AEM Forms com base em versões anteriores do Archetype, incorpore artefatos de Componentes principais do WCM e artefatos do Componente principal do Forms (incluindo exemplos) no seu projeto:

1. Abra a pasta do projeto AEM Archetype em um editor de código de texto simples. Por exemplo, Código VS.

1. Abrir nível superior `.pom` arquivo (pom pai) do projeto Arquétipo de AEM no ambiente local, adicione as seguintes propriedades ao arquivo e salve-o.

   ```XML
   <properties>
       <core.forms.components.version>2.0.4</core.forms.components.version> <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
       <core.wcm.components.version>2.21.2</core.wcm.components.version>
   </properties>
   ```

   Para obter a versão mais recente de `core.forms.components` e `core.wcm.components`, verificar [documentação dos componentes principais](https://github.com/adobe/aem-core-forms-components).

1. Na seção de dependências do nível superior (pai) `pom.xml` adicione as seguintes dependências:

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

1. Abra o `all/pom.xml` e adicione as seguintes dependências no `embedded` seção para adicionar artefatos dos Componentes principais adaptáveis do Forms ao seu projeto do Arquétipo de AEM:

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
   Substitua ${appId} pelo appId do seu arquétipo.

1. Na seção de dependências do `all/pom.xml` adicione as seguintes dependências:

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

1. Incluir `af-core bundle` dependência na `ui.apps/pom.xml`

   ```XML
        <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   Certifique-se de que os seguintes artefatos dos Componentes principais do Adaptive Forms não estejam incluídos em seu projeto.
   `<dependency>`
   `<groupId>com.adobe.aem</groupId>`
   `<artifactId>core-forms-components-apps</artifactId>`
   `</dependency>`
   e
   `<dependency>`
   `<groupId>com.adobe.aem</groupId>`
   `<artifactId>core-forms-components-core</artifactId>`
   `</dependency>`

1. [Executar o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=pt-BR). Após a execução bem-sucedida do pipeline, os Componentes principais adaptáveis do Forms são ativados para seu ambiente. Além disso, o modelo Adaptive Forms (Componentes principais) e o tema Canvas são adicionados ao ambiente as a Cloud Service do Forms.


## Atualizar seu ambiente de desenvolvimento local {#upgrade-your-local-development-environment}

Atualizar o SDK para uma nova versão requer a substituição de todo o ambiente de desenvolvimento local, resultando na perda de todo o código, configuração e conteúdo nos repositórios locais. Certifique-se de que qualquer código, configuração ou conteúdo que não deve ser destruído esteja comprometido com o Git ou seja exportado das instâncias do Experience Manager local como Pacotes CRX.

### Como evitar perda de conteúdo ao atualizar o SDK {#avoid-content-loss-when-upgrading--SDK}

A atualização do SDK está criando uma nova instância de Autor e Publicação, incluindo um novo repositório ([Configurar AEM projeto](#forms-cloud-service-local-development-environment)), o que significa que as alterações feitas em um repositório anterior do SDK são perdidas. Para obter estratégias viáveis para ajudar no conteúdo persistente entre atualizações de SDK, consulte [Como evitar perda de conteúdo ao atualizar o SDK do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html?lang=en#optional-local-aem-runtime-set-up-tasks)

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

### Faça backup e importe conteúdo específico do Forms para um novo ambiente SDK {#backup-and-import-Forms-specific-content-to-new-SDK-environment}

Para fazer backup e mover ativos do SDK existente para um novo ambiente do SDK:

* Crie um backup do seu conteúdo existente.

* Configure um novo ambiente do SDK.

* Importe o backup para o novo ambiente SDK.

### Crie um backup do seu conteúdo existente {#create-backup-of-your-existing-content}

Faça o backup do Adaptive Forms, modelos, modelo de dados de formulário, tema, configurações e código personalizado. Você pode executar a seguinte ação para criar o backup:

1. [Baixar](import-export-forms-templates.md#manage-forms-and-related-assets) Forms adaptável, temas e PDF forms.
1. Exportar modelos de formulário adaptável.

1. Baixar modelos de dados de formulário

1. Exportar modelos editáveis, configurações de nuvem e modelo de fluxo de trabalho. Para exportar todos os itens mencionados anteriormente do SDK existente, crie um [Pacote CRX](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=pt-BR) com os seguintes filtros:

   * /conf/ReferenceEditableTemplates
   * /conf/global/settings/cloudconfigs
   * /conf/global/settings/wcm
   * /var/workflow/models
   * /conf/global/settings/workflow
1. Exporte configurações de email, envie e preencha previamente o código de ações do seu ambiente de desenvolvimento local. Para exportar essas configurações e configurações, crie uma cópia das seguintes pastas e arquivos no ambiente de desenvolvimento local:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

### Importe o backup para o novo ambiente do SDK {#import-the-backup-to-your-new-SDK-environment}

Importe Forms adaptáveis, modelos, modelo de dados de formulário, tema, configurações e código personalizado para seu novo ambiente. Você pode executar a seguinte ação para importar o backup:

1. [Importar](import-export-forms-templates.md#manage-forms-and-related-assets) Adaptável Forms, temas e PDF forms para novos ambientes SDK.
1. Importe modelos de formulário adaptável para o novo ambiente SDK.

1. Faça upload de Modelos de dados de formulário para o novo ambiente SDK.

1. Importe modelos editáveis, configurações de nuvem e modelo de fluxo de trabalho. Para importar todos os itens mencionados anteriormente no novo ambiente do SDK, importe o Pacote CRX contendo esses itens para o novo ambiente do SDK.

1. Importe configurações de email, envio e código de ações de preenchimento prévio de seu ambiente de desenvolvimento local. Para importar essas configurações e configurações, coloque os seguintes arquivos do seu antigo projeto do Archetype no novo projeto do Archetype:

   * `[Archetype Project in Cloud Service Git]/core/src/main/java/com/<program name>/core/service`
   * `[Archetype Project in Cloud Service Git] /core/src/main/java/com/<program name>/core/servlets/FileAttachmentServlet.java`
   * `[Archetype Project in Cloud Service Git]/ui.apps/src/main/content/jcr_root/apps/<program name>/config`

O novo ambiente agora tem formulários e ativos relacionados do ambiente antigo.
