---
title: Arquitetura AEM Forms as a Cloud Service para APIs de Forms adaptável e comunicação
description: Entenda a arquitetura do  [!DNL AEM Forms] as a Cloud Service para saber mais sobre os aspectos de escalabilidade, resiliência e desempenho da plataforma.
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 9d677bee-50ca-460e-b503-6b7799900735
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 2%

---

# Arquitetura do Forms as a Cloud Service [!DNL AEM] {#architecture}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/aem-forms-architecture-deployment.html) |
| AEM as a Cloud Service | Este artigo |

O [!DNL Adobe Experience Manager Forms] as a Cloud Service é uma solução nativa em nuvem para que as empresas criem, gerenciem, publiquem e atualizem formulários digitais complexos e comunicações enquanto integram dados enviados a processos de back-end, regras de negócios e salvam dados em um armazenamento de dados externo. Estende [!DNL Adobe Experience Manager as a Cloud Service]. Para saber mais sobre dimensionamento, implantação, ambientes e outras infraestruturas, consulte [Uma Introdução à Arquitetura de [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html).

A AEM Forms as a Cloud Service oferece suporte a dois casos de uso importantes: Inscrição digital e Comunicações ao cliente. As ilustrações a seguir descrevem a arquitetura para ambos os casos de uso.

## Inscrição digital Forms

![Inscrição Forms-Digital](assets/forms-cloud-service-architecture-forms-digital-enrollment.svg)

## Comunicações da Forms

![Comunicação-Forms](assets/forms-cloud-service-architecture-forms-communications.svg)

## Aplicabilidade e casos de uso

### Seguros

## O AEM Forms pode lidar com operações de seguro em escala?

Sim. Quando implantada usando arquiteturas recomendadas no Adobe Managed Services ou na nuvem privada, a AEM Forms oferece suporte a envios de formulários de alto volume e a cargas de trabalho de escala empresarial.

## O AEM Forms é seguro para dados de seguros?

Sim. O AEM Forms oferece suporte a mecanismos seguros de transmissão de dados, acesso controlado e autenticação corporativa, tornando-o adequado para lidar com dados confidenciais de seguros.

## Componentes

O Forms as a Cloud Service inclui vários componentes:

### CDN (Content Delivery Network)

Todos os programas do AEM Forms as a Cloud Service têm acesso ao [serviço CDN interno](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn). Está incluído na licença do Forms as a Cloud Services.

### Autor

Um Autor é uma instância do AEM Forms as a Cloud Service em execução no modo de execução padrão do Autor. Destina-se a usuários internos, designers de formulários e desenvolvedores. Um ambiente de Autor habilita as seguintes funcionalidades:

* Criação e gerenciamento de formulários.
* Conexão com o serviço de conversão automatizada de formulários para converter um formulário PDF ou XDP em um formulário adaptável.
* Criar e executar workflows centrados no Forms.
* Gerenciamento de ativos de formulários adaptáveis.
* Gerenciamento de ativos de comunicações.
* APIs RESTful síncronas (APIs em tempo real) e APIs em lote para criar, montar e fornecer comunicações personalizadas e orientadas pela marca.
* APIs síncronas para combinar, reorganizar e validar documentos do PDF.

### Publicação

Uma instância de Publicação é um AEM Forms as a Cloud Service executado no modo de execução padrão Publicação. As instâncias de publicação destinam-se aos usuários finais de aplicativos baseados em formulário, por exemplo, usuários que acessam um site público e enviam formulários. Ela permite as seguintes funcionalidades:

* Renderização e envio de formulários para usuários finais.
* Transporte de dados brutos de formulário enviados para processamento posterior e armazenamento no sistema de registro final.
* Conectando-se ao Armazenamento gerenciado pelo cliente para armazenar dados.
* Conexão com o Adobe Sign para assinar eletronicamente um registro de envio de formulário adaptável.
* Sincronizar APIs para criar, montar e fornecer comunicações personalizadas e orientadas pela marca.
* Sincronizar APIs para combinar, reorganizar e validar documentos do PDF.

A Replicação reversa não está disponível no AEM as a Cloud Service para enviar conteúdo/dados do Serviço de publicação para o Serviço do autor. No entanto, é possível configurar um Forms adaptável em execução em Publicar para enviar dados a um Fluxo de trabalho em um Autor (os fluxos de trabalho só podem ser executados no Autor). Isso é útil em casos de uso de aprovação.

#### Dispatcher

O [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=pt-BR) é uma ferramenta de armazenamento em cache e/ou balanceamento de carga do Adobe Experience Manager que pode ser usada com um servidor Web de classe empresarial.

### Serviços da Adobe

**Serviço de conversão automática de formulários**

O [Serviço de conversão automática de formulários](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=pt-BR) converte automaticamente seus formulários PDF e XFA em formulários adaptáveis compatíveis com dispositivos responsivos e baseados em HTML5.

**Adobe Sign**

O Adobe Sign é um serviço de assinatura eletrônica baseado em nuvem que permite ao usuário enviar, assinar, rastrear e gerenciar processos de assinatura usando um navegador ou dispositivo móvel. É possível integrar o Adobe Sign a um formulário adaptável para automatizar fluxos de trabalho de assinatura, simplificar processos de assinatura única e multiassinatura e assinar eletronicamente formulários adaptáveis.

<!-- **PDF Service API**
Adobe’s PDF Services API lets create, combine, export, and extract data from PDFs through powerful and flexible cloud-based APIs. -->

### Armazenamento gerenciado pelo cliente

O Forms as a Cloud Service fornece opções para armazenar conteúdo em um sistema de armazenamento externo, como o Blob Store, o banco de dados ou um serviço de armazenamento. Você também pode armazenar dados de fluxos de trabalho em andamento (dados de variáveis de fluxos de trabalho do AEM) que contêm elementos de Dados pessoais sensíveis (SPD) em um repositório gerenciado pelo cliente para processamento seguro. A Adobe recomenda armazenar dados confidenciais apenas em armazenamentos gerenciados pelo cliente.

Você pode usar o **Conector de Armazenamento Unificado** para se conectar ao Armazenamento de Blob e o **Modelo de Dados de Formulário (FDM)** para se conectar a bancos de dados ou serviços de back-end (RESTful, SOAP, Armazenamento de Blob do Azure e muito mais).

### Serviços de documento

Os serviços de documentos são os seguintes:

* **O Serviço de Saída (Comunicações - APIs de Geração de Documentos)** ajuda a criar documentos personalizados e padronizados, aprovados pela marca, como correspondências comerciais, declarações, cartas de processamento de solicitações, avisos de benefícios, faturas mensais ou kits de boas-vindas.

* O **Serviço de Assembler (Comunicações - APIs de Manipulação de Documentos)** ajuda a combinar, reorganizar e validar documentos do PDF.

* O **Serviço do Documento de Registro (DoR)** ajuda a gerar o Documento de Registro (DoR). O serviço é executado em seus próprios pods, separados das instâncias Autor e Publicar do Forms as a Cloud Service. Ele ajuda a fornecer um melhor desempenho e dimensionar os pods independentemente, dependendo da carga.

### Cloud Manager

O Cloud Manager é um componente essencial do [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html). É o ponto de entrada único para as operações e a persona de desenvolvedor de nossos clientes. É o local onde os programas e ambientes do AEM podem ser gerenciados. O Cloud Manager evoluiu como um portal de autoatendimento, em que os principais componentes do AEM as a Cloud Service podem ser criados e configurados:

* Criação e gerenciamento de programas
* Criação e gerenciamento dos ambientes do AEM nos programas
* Criação e gerenciamento de pipelines para implantação do código e configuração do cliente em um ambiente específico
* Ser notificado sobre eventos importantes do ciclo de vida desses componentes (por exemplo, atualizações de produtos)
Para obter mais informações sobre o Cloud Manager, consulte [Entender o Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) e [Introdução ao Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=pt-BR).

### Console do desenvolvedor

Um Developer Console fornece vários detalhes de cada ambiente do Forms as a Cloud Service em execução. Esses detalhes são úteis na depuração do ambiente. Para obter detalhes, consulte [Depurando o AEM as a Cloud Service com a Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html).

<!--

+++CDN (Content Delivery Network):

Every AEM Forms as a Cloud Service program has access to Fastly CDN service. It is included in the licence of Forms as a Cloud Services.

+++

+++Adaptive Forms
Adaptive Forms enable customers to author web-friendly reflowable web forms and fragments that are used by the customers for their data capture needs. This feature enables customers to manage their complex data capture needs easily, by using multiple integrations with Adobe Sign, Document Services, Form Data Model (FDM), Automated Forms Conversion service, and more.

+++

+++Automated Forms Conversion Service (AFCS)
Automated Forms Conversion service helps accelerate digitization and modernization of data capture experience through automated conversion of PDF forms to adaptive forms. The service, powered by Adobe Sensei, automatically converts your PDF forms to device-friendly, responsive, and HTML5-based adaptive forms. While using the existing investments in PDF Forms and XFA, the service also applies appropriate validations, styling, and layout to adaptive form fields during conversion.

+++

+++Form Data Model (FDM)
The Form Data Model (FDM) feature is the standard way of creating data integrations with external/internal data sources and using them across the different Forms as a Cloud Service features. FDM provides a rich editor for customers to integrate, define, and manage relationships between the different entities and data sources and perform operations on them. Form data is stored in a data store hosted on the customer premises. Organizations can also use blob store hosted by the cloud provider and Adobe Experince Platform to store data.

+++

+++Forms Workflows
Forms-centric workflows is an extension to the default AEM Workflow and provides our customers with additional workflow capabilities like Form Data review, task assignment, and document services invocation.

+++

+++Communications
Forms as a Cloud Service offering consists of multiple services tailored specifically for document processing.

+++

+++Document of Record
A Document of Record is a PDF version of a form. It provides an ability to keep a record of the information  that you provide and submit in an Adaptive Form in PDF fromat. The service provides a default DoR template and tools to develop a custom template.

+++

## Terminologies

<!-- ## Cloud Manager{#cloud-manager}

Cloud Manager is an essential component to [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Each new tenant of the [!DNL AEM Forms] as a Cloud Service is first provisioned for Cloud Manager access. Cloud Manager is the single-entry point for the operations and developer persona of our customers. It is the place from where the AEM programs and environments can be managed. Cloud Manager has evolved as a self-service portal where the main components of the AEM as a Cloud Service can be created and configured:

* Creating and managing programs
* Creating and managing the AEM environments within the programs
* Creating and managing the pipelines for deploying the customer code and configuration to a particular environment
* Getting notified of important lifecycle events for these components (for example, product updates)
For more information about Cloud Manager, see [Understand Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) and [Introduction to Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Users and Authentication {#users-and-authentication}

AEM as a Cloud Service includes Admin Console support for AEM instances and Adobe Identity Management System (IMS) based authentication. The Admin Console allows administrators to centrally manage all Experience Cloud users. Users and Groups can be assigned to product profiles associated with AEM as a Cloud Service instances, allowing them to log in to that instance. For more information about users, authentication, and, and accessing an instance of AEM as a Cloud Service, see [IMS Support for [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Various personas are involved in a typical [!DNL AEM Forms] project. After you log in to your [!DNL AEM Forms] as a Cloud Service instance, you can [add users in admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) for personas applicable to your organization or project and [assign users to built-in groups](forms-groups-privileges-tasks.md) to provide them required privileges.

To learn various in-built [!DNL AEM Forms] specific user groups and privileges available on [!DNL AEM Forms] as a Cloud Services instance, see [Configure, user, roles and groups](forms-groups-privileges-tasks.md). 

## Developer Experience {#developer-experience}

The new architecture supporting AEM as a Cloud Service brings some key changes to the overall developer experience. One of the major goals for the changes to developer experience is to allow migration to AEM as a Cloud Service as quickly as possible, with little modifications to existing custom code.

## Cloud development {#cloud-development}

Here are the guidelines to run your existing code smoothly on AEM as a Cloud Service environment:

* Store your code and configurations to the Git repository of the associated Cloud Manager program. It makes managing and integrating code with CI/CD a breeze.  
* Make application code and configuration compatible with the baseline [!DNL AEM Forms] images. Using the latest APIs helps to build faster and secure applications.
* Use the Cloud Manager pipeline associated with the Cloud Manager environment to build and deploy applications. It helps you bring the latest features and bug fixed for [!DNL AEM Forms] as a Cloud Service to your environment.
* Try that your custom applications pass all the code quality, security, and performance gates enforced in the pipeline. It helps build secure and better performing applications which leads to better customer experience. You can always use Cloud Manager UI to skip some checks.
This process is commonly referred to as cloud-first development. [!DNL AEM Forms] as a Cloud Service also provides an SDK to support rapid development before the pending code and configuration changes are attempted in the cloud.
Some interfaces that were previously part of the AEM QuickStart are no longer available to the users of the AEM as a Cloud Service environment. For instance, the Web Console where OSGI bundles and their associated configuration are managed. The CRXDE Lite content repository browser becomes only accessible on non-production environment types. A subset of the Web Console functionalities that developers require, especially when it comes to diagnostics and status purposes, is made available via a new developer console.
Also, one of the most common requirements for developers is quick access to the log files of the various environments. With [!DNL AEM Cloud Service], the log files of the different nodes in the Author, Publish are made available via the Cloud Manager, either in the form of files that can be downloaded or via APIs for tailing the logs. Due to the clear separation of code and content, developers can use a particular process for updating content as part of a deployment. The typical use cases for mutable content are:
* Standard “default” content that is part of the customer project (for example, folders, templates, workflows...)
* Search index definitions
* ACLs and permissions
* Service users and user groups
Set up your development environment, [Configure your CI/CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html), and learn to [deploy your code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) on the environment. -->

### Criação de formulário adaptável {#local-development}

Ao instalar e configurar um ambiente do as a Cloud Service [!DNL AEM Forms], você configura ambientes de desenvolvimento, de preparo e de produção. Além disso, configure um ambiente de desenvolvimento local para iterações e desenvolvimento rápidos. Você pode baixar e configurar o AEM SDK e o arquivo de recursos complementares do [!DNL AEM Forms] para configurar um ambiente de desenvolvimento do as a Cloud Service [!DNL Forms] local.  Para obter instruções detalhadas, consulte [Configurar um ambiente de desenvolvimento local](setup-local-development-environment.md).

## Depuração {#debugging}

O AEM as a Cloud Service é executado em infraestruturas de nuvem dimensionáveis e de autoatendimento. Ele requer que os desenvolvedores do AEM entendam e depurem vários aspectos do AEM as a Cloud Service, desde a criação e implantação até a obtenção de detalhes sobre a execução de aplicativos do AEM. Para obter informações detalhadas, consulte [Depuração do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html).


>[!MORELIKETHIS]
>
>* [Introdução às Comunicações do AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Processamento em Lote de Comunicações do AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Processamento da comunicação - APIs síncronas](/help/forms/aem-forms-cloud-service-communications.md)
