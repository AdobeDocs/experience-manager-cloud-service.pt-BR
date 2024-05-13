---
title: Introdução ao Adaptive Forms.
description: Saiba como criar formulários adaptáveis compatíveis com dispositivos móveis com nosso tutorial passo a passo. Esses formulários se adaptam perfeitamente em todos os dispositivos, garantindo uma experiência perfeita.
keywords: Forms adaptável, Forms responsivo, HTML5 Forms
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
source-git-commit: 3eb2a7ce311f9e738a95ea5fcf6876f4df1fa648
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 2%

---


# Criar um formulário adaptável (componentes principais) - Tutorial

Atualmente, os usuários esperam uma experiência móvel em todas as suas interações, e os formulários não são exceção. Os formulários adaptáveis podem ajudá-lo a criar formulários que não são apenas amigáveis para dispositivos móveis, mas também melhorar o engajamento do usuário e reduzir o tempo que leva para concluí-los.

Este tutorial fornece um guia passo a passo para a criação de um formulário adaptável. Ele está dividido em um caso de uso e vários guias, cada um deles ensinando a adicionar um novo recurso ao formulário adaptável.

Ao final do tutorial, você será capaz de:

* Criar um formulário adaptável e seu modelo de dados
* Estilizar o formulário adaptável
* Criar regras de negócios usando o editor de regras de formulário adaptável
* Preencher previamente campos de formulário adaptáveis
* Adicionar assinaturas eletrônicas ao formulário
* Protect seu formulário de bots usando o Google reCAPTCHA
* Localize seu formulário adaptável para diferentes idiomas
* Configurar o formulário para produzir dados estruturados
* Configurar o formulário para enviar dados a um terminal REST
* Publicar seu formulário adaptável


## Por que criar formulários baseados nos Componentes principais?

O AEM Forms fornece os Componentes de base e os Componentes principais para criar experiências de formulários. Os Componentes principais são a abordagem moderna e recomendada para criar qualquer nova experiência de formulários. Por que usar os Componentes principais? Esses componentes são leves e de código aberto (disponíveis no github), oferecem excelente pontuação no Google Lighthouse e na Web, são compatíveis com acessibilidade e oferecem todos os recursos familiares do AEM Sites (como controle de versão e localização). Além disso, esses componentes são mais fáceis de estilizar, e você pode personalizar facilmente a aparência de acordo com as diretrizes de marca da sua organização. Eles não têm dependências de terceiros. Qualquer desenvolvedor com conhecimento em JavaScript e CSS pode personalizar facilmente esses componentes.

![Por que criar Componentes principais baseados no Forms adaptável? Esses componentes são leves, mais fáceis de estilizar, oferecem alta pontuação mínima, padrões de acessibilidade de suporte, facilmente personalizáveis, de código aberto, disponíveis no github, sem dependência de bibliotecas de terceiros e quase não têm curva de aprendizado para desenvolvedores do AEM e autores do AEM. Além disso, os Componentes principais do AEM Forms têm todos os recursos dos Componentes principais do AEM WCM.](/help/forms/assets/cc-core-components-benefits.png)

## Caso de uso: pré-qualificação de empréstimo residencial simplificada com o Forms adaptável

Neste tutorial, você cria um formulário adaptável para um banco grande. O caso de uso é:

Os possíveis compradores de casas visitam o site ou a agência do banco para explorar as opções de empréstimo para residências. O processo de aplicativo tradicional é demorado e sobrecarregado, exigindo, muitas vezes, documentação prévia. Isso dissuade alguns compradores de iniciar o processo, dificultando tanto a geração de leads do banco quanto a capacidade do comprador de procurar com confiança por sua casa dos sonhos.

Você tem a tarefa de desenvolver um formulário interativo de pré-qualificação de empréstimo à casa. Este formulário reunirá informações básicas, pré-qualificará o mutuário com base em suas informações, oferecendo quantias estimadas de empréstimo, possíveis necessidades de entrada de pagamento e taxas de juros com base em diferentes tipos de empréstimo. Os usuários pré-qualificados poderiam iniciar um aplicativo de empréstimo completo diretamente do formulário de pré-qualificação.

O formulário seria criado usando formulários adaptáveis. Isso permite uma experiência personalizada enquanto coleta os dados financeiros necessários para uma pré-qualificação precisa do empréstimo para residências.

Na conclusão do tutorial, seu formulário seria semelhante ao seguinte formulário:

![Adicione um formulário de trabalho aqui](/help/forms/assets/cc-tutorial-final-form.png)

## Configurar um ambiente de desenvolvimento

Você pode criar e testar o formulário adaptável diretamente no computador local antes de implantá-lo em um ambiente Cloud Service. O Adobe fornece um AEM SDK para o desenvolvimento local que permite

* Crie, personalize e teste formulários localmente.
* Projetar temas de formulários e criar configurações localmente,
* Implante facilmente os ativos concluídos na nuvem.

O desenvolvimento local com o SDK do AEM economiza tempo e simplifica o processo de desenvolvimento


**Pronto para começar?**

1. [Configurar ferramentas de desenvolvimento para Projetos AEM](/help/forms/setup-local-development-environment.md#set-up-development-tools-for-aem-projects): baixe e instale a versão mais recente do [Java 11™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up), [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git), [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js), e [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven). Além disso, instale um editor de texto simples. Os exemplos deste tutorial são baseados no Visual Studio Code.

1. [Instalar o SDK do AEM](/help/forms/setup-local-development-environment.md#set-up-local-experience-manager-environment-for-development): baixe e instale a versão mais recente do SDK do AEM. Isso fornece as ferramentas essenciais para o desenvolvimento do AEM. Anote a versão do SDK do AEM.

   ![Distribuição de software](/help/forms/assets/software-distribution.png)

   ![instalar o SDK do AEM](/help/forms/assets/start-aem-sdk.png)

1. [Adicionar o complemento do AEM Forms](/help/forms/setup-local-development-environment.md#add-forms-archive-to-local-author-and-publish-instances-and-configure-forms-specific-users): Baixe e instale o complemento AEM Forms correspondente à versão do SDK do AEM na [Distribuição de software](https://experience.adobe.com/#/downloads) Portal.
   ![install-aem-forms-add-on](/help/forms/assets/install-aem-forms-add-on.png)

   +++Instalar complemento do AEM Forms

       Para instalar o complemento do AEM Forms, pare o AEM SDK, adicione o arquivo do complemento (.far) do AEM Forms AEM AEM à pasta &quot;SDK/crx-quickstart/install&quot; e reinicie o SDK.
   
+++

1. [Configurar permissões do usuário](/help/forms/setup-local-development-environment.md#configure-users-and-permissions): crie usuários com permissões de desenvolvimento, criação e outras e adicione esses usuários a grupos de formulários predefinidos.


1. [Adicionar modelos adaptáveis do Forms](/help/forms/setup-local-development-environment.md#set-up-a-development-project-for-forms-based-on-experience-manager-archetype): Use o Arquétipo AEM 48 ou posterior para criar um novo projeto AEM e implantá-lo no SDK do AEM. O projeto adiciona modelos do Adaptive Forms ao AEM SDK.

   +++Adicionar modelos adaptáveis do Forms

   1. Execute o comando abaixo para criar um projeto AEM.

      ```
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="48" -D appTitle=securbank -D appId=securbank -D groupId=com.securbank -D includeFormsenrollment="y" -D aemVersion="cloud"
      ```

      ![AEM-Arquétipo-Projeto](/help/forms/assets/aem-archetype-project.png)

   1. Implante o projeto no ambiente de desenvolvimento local. Você pode usar o comando a seguir para implantar no ambiente de desenvolvimento local

      ```
      cd securbank
      
      mvn -PautoInstallPackage clean install
      ```

+++

   Depois de implantar o projeto AEM, você pode ver os modelos adaptáveis do Forms no seu ambiente.

   ![Modelos de formulário adaptável](/help/forms/assets/adaptive-forms-templates.png)

Para obter um guia passo a passo sobre como configurar o ambiente de desenvolvimento local do AEM Forms, consulte [configurar ambiente de desenvolvimento local para o AEM Forms](/help/forms/setup-local-development-environment.md)



## Próxima etapa

Depois de configurar o ambiente de desenvolvimento, você estará pronto para criar um formulário adaptável. No próximo artigo, você aprenderá a

* Criar um formulário adaptável a partir do modelo em branco
* Campos de layout para exibir e aceitar facilmente informações.
* Visualize o formulário.

<!-- 

### Step 2: Create Form Data Model

A form data model lets you connect an adaptive form to disparate data sources. For example, AEM user profile, RESTful web services, SOAP-based web services, OData services, and relational databases. You can use the form data model with an adaptive form to retrieve, update, delete, and add data to connected data sources.

Goals of article:

* Create the form data model using Rest endpoint.
* Add data model objects so you can form the data model.
* Configure read and write services for the form data model.
* Test form data model and configured services with test data.

### Step 4: Apply rules to adaptive form fields

AEM Forms provide an editor to write rules on adaptive form objects. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps ensure accuracy and speeds up the form-filling experience.

Goals:

* Create and apply rules to adaptive form fields.
* Use rules to trigger form data model services to update the data to database.

### Step 5: Style your adaptive form

Adaptive forms provide OOTB themes and allows you to customize an existing theme to make a brand specific theme. 


A theme contains styling details for components and panels, and you can reuse a theme in different forms. Styles include properties such as background colors, state colors, transparency, alignment, and size. When you apply the theme to your form, the specified style reflects on corresponding components of your form.

Goals:

* Apply an out of the box theme to an adaptive form.
* Create your brand specific theme.


### Step 6: Publish your adaptive form

You can publish adaptive forms as a stand-alone form (single page application), include in AEM Sites page, or include in a non-AEM Sites page.

Goals:

* Publish the adaptive form as an AEM Page.
* Embed the adaptive form in an AEM Sites Page.
* Embed the adaptive form in an external webpage (a non-AEM webpage hosted outside AEM).

-->