---
title: O que mudou entre o AEM 6.5 Forms e o AEM Cloud Services
description: Você é um usuário do Experience Manager Forms e deseja atualizar para o Adobe Experience Manager Forms as a Cloud Service? Conheça as alterações mais importantes antes de atualizar ou migrar para o Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: fa8629fefe3ad29f70213b15bb31623a2f7d5420
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# Alterações importantes para usuários existentes do Adobe Experience Manager 6.5 Forms  {#notable-changes-for-existing-AEM-Forms-users}

O Adobe Experience Manager Forms as a Cloud Service traz algumas alterações notáveis para os recursos existentes em comparação com o Adobe Experience Manager Forms no local e [!DNL Adobe-Managed Service] ambientes. As principais diferenças estão listadas abaixo:

| Recurso/capacidade | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms |
|---|---|---|
| Arquitetura nativa em nuvem | ✅ | ⛌ |
| Dimensionamento automático com base na carga | ✅ | ⛌ |
| Nenhum tempo de inatividade para upgrades | ✅ | ⛌ |
| Frequência de implantação do recurso | Agile* | Trimestral |
| CDN (content delivery network) incluída | ✅ | ⛌ |
| Topologias otimizadas para máxima resiliência e eficiência | ✅ | ⛌ |
| Ambiente de desenvolvimento nativo em nuvem | ✅ | ⛌ |
| Autoatendimento via Cloud Manager | ✅ | ⛌ |
| Upgrades automatizados com integração contínua e entrega contínua (CI/CD) | ✅ | ⛌ |
| Integração com o [!DNL Micosoft Power Automate] | ✅ | ⛌ |
| Integração com o [!DNL DocuSign] | ✅ | ⛌ |
| Fácil conectividade com o Microsoft Dynamics e o Salesforce | ✅ | ⛌ |
| Fácil conectividade com armazenamentos de dados do Microsoft Azure | ✅ | ⛌ |
| Editor de regras reforçadas | ✅ | ⛌ |
| Assistente de criação de formulário | ✅ | ⛌ |
| Suporte XCI personalizado para documento de registro | ✅ | ⛌ |
| Forms adaptável <sup>1</sup> | ✅ | ✅ |
| APIs de comunicações (serviços de documentos) <sup>2,3</sup> | ✅ | ✅ |
| Serviço Automated forms conversion <sup>4</sup> | ✅ | ✅ |
| Portal Forms <sup>5</sup> | ✅ | ✅ |
| Modelo de dados do Forms <sup>6</sup> | ✅ | ✅ |
| HTML5 FORMS <sup>7</sup> | ⛌ | ✅ |
| Segurança de documentos | ⛌ | ✅ |

Antes de continuar com o serviço, considere os seguintes casos excepcionais:

+++ 1. Forms adaptável

* **Forms adaptável baseado em XSD:** O serviço não oferece suporte ao HTML5 Forms (Mobile Forms). Se você renderizar seus formulários baseados em XDP como HTML5 Forms, poderá continuar usando o recurso no AEM 6.5 Forms. Você pode usar o modelo XDP para projetar um modelo para documento para registro. O serviço não é compatível com o Adaptive Forms baseado em XFA
* **Importação de modelos de formulário adaptável:** Use o pipeline de build e o repositório Git correspondente do seu programa para importar modelos de Formulário adaptável existentes.
* **Editor de regras:** O AEM Forms as a Cloud Service oferece uma [Editor de regras](rule-editor.md#visual-rule-editor). O editor de código não está disponível no Forms as a Cloud Service. O utilitário de migração ajuda a migrar os formulários que têm regras personalizadas (criadas no editor de código). O utilitário converte essas regras em funções personalizadas compatíveis com o Forms as a Cloud Service. Você pode usar as funções reutilizáveis com o Editor de regras para continuar obtendo os resultados obtidos com scripts de regras. A `onSubmitError` ou `onSubmitSuccess` As funções do agora estão disponíveis como ações no Editor de regras.
* **Rascunhos e envios:** O serviço não retém metadados para rascunhos e Forms adaptável enviado.
* **Preencher Serviço:** Por padrão, o serviço de preenchimento prévio mescla dados com um formulário adaptável no cliente em vez de mesclar dados no servidor no AEM 6.5 Forms. O recurso ajuda a melhorar o tempo necessário para preencher previamente um Formulário adaptável. Você sempre pode configurar o para executar a ação de mesclagem no servidor do Adobe Experience Manager Forms.
* **Enviar ações:** A variável **Enviar por e-mail como PDF** ação não disponível. A variável **E-mail** ação enviar fornecer opções para enviar anexos e anexar Documento de registro (DoR) com o email.
* **Componentes**: o serviço não oferece suporte à experiência de assinatura no formulário e não inclui os componentes Resumo e Verificação para o Adaptive Forms.



+++


+++ 2. Serviços de documento: APIs de manipulação de documentos (Serviço do Assembler)


O serviço não oferece suporte a operações dependentes de outros serviços ou aplicativos:

* Não há suporte para a conversão de documentos em formato não PDF em PDF. Por exemplo, Microsoft Word para PDF, Microsoft Excel para PDF e HTML para PDF não são compatíveis. Se os documentos não estiverem em formato PDF. Converta esses documentos no formato PDF antes de usá-los com APIs de manipulação de documentos de comunicações. Por exemplo, se seus documentos estiverem no Microsoft Office, HTML, PostScript (PS), formato XDP, converta esses documentos para o formato PDF antes de usá-los com documentos PDF.
* Não há suporte para conversões baseadas em Distiller do Adobe. Por exemplo, PostScript(PS) para PDF
* Não há suporte para conversões baseadas em serviços do Forms. Por exemplo, XDP para PDF forms.
* O serviço não oferece suporte à conversão de um PDF assinado ou PDF transparente para outro formato PDF.
* Não está disponível a aplicação de direitos de uso usando o Serviço de Extensões do Reader.
* O serviço não oferece a capacidade de converter documentos de PDF assinados ou transparentes para o formato PDF/A.

+++


+++ 3. Serviços de documento: APIs de geração de documento (serviço de saída)

Em uma única chamada de API ou em um lote, você pode usar apenas um modelo com vários arquivos DATA XML. Não há suporte para o uso de vários modelos com vários arquivos de dados em uma única chamada de API.

+++

+++ 4. Serviço Automated forms conversion

O serviço não fornece um metamodelo para o Serviço do Automated forms conversion. Você pode [baixe-o na documentação do Automated forms conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

+++

+++ 5. Portal Forms

O suporte para uso anônimo do Forms Portal não está disponível imediatamente (OOTB). Você pode personalizar o Forms Portal para permitir a exibição de formulários para usuários não conectados.

+++

+++ 6. Modelo de dados do formulário

* O modelo de dados do Forms oferece suporte somente a endpoints HTTP e HTTPs para enviar dados. O serviço não oferece suporte a SSL mútuo para conector REST e autenticação baseada em certificado x509 para fontes de dados SOAP.

* O Forms as a Cloud Service permite usar o Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive e serviços que oferecem suporte a operações CRUD (Create, Read, Update, and Delete, Criar, Ler, Atualizar e Excluir) gerais como armazenamentos de dados. As especificações Open API 2.0 e Open API são compatíveis. O serviço também oferece suporte ao conector JDBC.

+++


+++ 7. HTML5 Forms

* O serviço não oferece suporte ao HTML5 Forms (Mobile Forms). Se você renderizar seus formulários baseados em XDP como HTML5 Forms, poderá continuar usando o recurso no AEM 6.5 Forms.

* Se você tiver um caso de uso para capturar dados offline e sincronizá-los na próxima vez que voltar online, poderá continuar usando o [Espaço de trabalho AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) recurso no AEM 6.5 Forms.

+++





+++ 8. Ambiente do desenvolvedor

* Um ambiente nativo em nuvem não tem o console da Web (gerenciador de configurações). Você pode usar [[!DNL AEM Forms] SDK as a Cloud Service para gerar configurações](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) e pipeline de CI/CD para [implantar a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) para a instância do Cloud Service.
* Por padrão, o email suporta somente os protocolos HTTP e HTTPs. [Contate a equipe de suporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) para habilitar portas para enviar emails e para habilitar o protocolo SMTP para o seu ambiente.
* O serviço não oferece suporte à conversão de um PDF assinado ou PDF transparente para outro formato PDF. Antes de usar seus pacotes de clientes com o Forms as a Cloud Service, recompile seu código personalizado com a versão mais recente da convenção de URL do adobe-aemfd-docmanager* da Adaptive Forms localizada, que agora suporta a especificação de um local no URL. A nova convenção de URL permite o armazenamento em cache de formulários localizados em um Dispatcher ou CDN. No ambiente Cloud Service, use o formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um Formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. O Adobe recomenda usar o armazenamento em cache do Dispatcher ou CDN. Ajuda a melhorar a velocidade de renderização de formulários pré-preenchidos
* O Adobe Experience Manager Forms as a Cloud Service traz muitos novos recursos e possibilidades para seus projetos do AEM. No entanto, há algumas alterações necessárias para que os projetos do Adobe Experience Manager Maven sejam compatíveis com o AEM Cloud Service. Em um alto nível, o AEM requer uma separação de conteúdo e código em subpacotes discretos para respeitar a divisão entre conteúdo mutável e imutável. Use o [Modernizador de repositório](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) ferramenta para reestruturar pacotes de projetos existentes separando o conteúdo e o código em pacotes discretos para serem compatíveis com a estrutura do projeto definida para o Adobe Experience Manager as a Cloud Service.


+++

<!-- 

### HTML5 Forms (Mobile Forms)

The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms.

### Adaptive Forms 

* **XSD-Based Adaptive Forms:** The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. You can use XDP-template to design a template for Document for Record. The service does not support XFA based Adaptive Forms  
* **Importing Adaptive Form templates:** Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. 
*  **Rule editor:** AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor.  
* **Drafts and submissions:** The service does not retain metadata for drafts and submitted Adaptive Forms.  
* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. 
* **Submit actions:** The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. 
* **Components**:  The service does not support in-form signing experience and does not include the Summary and Verify components for Adaptive Forms.  
* **Forms portal**: Support for anonymous use of Forms portal is not available out of the box (OOTB). You can customize the forms portal to enable displaying forms for non-logged in users.

### Form Data Model

* Forms data model supports only HTTP and HTTPs endpoints to submit data. The service does not support Mutual SSL for REST connector and x509 certificate-based authentication for SOAP data sources. * Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores, both Open API specification 2.0 and Open API specification are supported. The service also provides support for JDBC connector.


### Automated Forms Conversion Service     

The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).


### Configurations

* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.  
* If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service. 


### Document Services: Document Manipulation APIs (Assembler Service)

The service does not support operations dependent on other services or applications:  

* Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported. If your documents are in a non-PDF format. Convert such documents to PDF format before using those with Communications Document Manipulation APIs. For example, if your documents are in Microsoft Office, HTML, PostScript (PS), XDP format, convert these documents to PDF format before using those with PDF documents. 
* Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF
* Forms Service-based conversions are not supported. For example, XDP to PDF Forms.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.
* Applying usage rights using Reader Extensions Service is not available. 
* The service does not provide the ability to convert signed or transparent PDF Documents to PDF/A format. 

### Document Services: Document Generation APIs (Output Service)

* In a single API call or batch, you can use one template with multiple DATA XML files. Using mutiple templates with multiple data files in a single API call is not supported. 

### Other differences

* A cloud-native environment does not have web console (configuration manager). You can use [[!DNL AEM Forms] as a Cloud Service SDK to generate configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) and CI/CD pipeline to [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) to your Cloud Service instance.
* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.* Before using your customer bundles with Forms as a Cloud Service, recompile your custom code with the latest version of adobe-aemfd-docmanager* URL convention of localized Adaptive Forms now supports specifying a locale in the URL. New URL convention enables caching localized forms on a Dispatcher or CDN. On Cloud Service environment, use the URL format `http://host:port/content/forms/af/<afName>.<locale>.html` to request a localized version of an Adaptive Form instead of `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recommends using Dispatcher or CDN caching. It helps improve rendering speed of prefilled forms 
* Adobe Experience Manager Forms as a Cloud Service brings many new features and possibilities into your AEM Projects. However, there are some changes required to Adobe Experience Manager Maven projects to be compatible with AEM Cloud Service. At a high-level, AEM requires a separation of content and code into discrete subpackages to respect the split between mutable and immutable content. Use the [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) tool to restructure existing project packages by separating content and code into discrete packages to be compatible with the project structure defined for Adobe Experience Manager as a Cloud Service.
-->




