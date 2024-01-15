---
title: Perguntas frequentes sobre o AEM Forms as a Cloud Service
description: Perguntas frequentes as a Cloud Service sobre o Forms
contentOwner: khsingh
role: User
feature: Adaptive Forms, FAQ
index: false
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 2%

---

# Perguntas frequentes {#frequently-asked-questions}

* **Posso usar o Editor de código para criar regras?**
Você pode usar o Editor visual para criar as regras. O Editor de códigos não está disponível em [!DNL Forms] as a Cloud Service. Se o formulário adaptável usar scripts de regras desenvolvidos com o editor de código, use o [Utilitário de migração](migrate-to-forms-as-a-cloud-service.md) para converter seus scripts de código em funções personalizadas. Você pode usar funções personalizadas com o Editor visual para continuar obtendo os resultados obtidos com o Editor de códigos.

* **Posso criar um formulário adaptável baseado em XFA em instâncias do Cloud Service?**
Sim, você pode criar um formulário adaptável baseado em XFA na instância do Cloud Service. No entanto, o suporte para o Adaptive Forms baseado em XFA não está disponível para o SDK as a Cloud Service do AEM Forms (Ambiente de desenvolvimento local). Se você pretende usar o Adaptive Forms baseado em XFA com o SDK as a Cloud Service do AEM Forms, entre em contato com o Suporte do Adobe com detalhes do caso de uso e requisitos específicos.

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **Posso migrar o conteúdo de um repositório no local ou [!DNL Adobe-Managed Services] ambientes para [!DNL Forms] as a Cloud Service ambiente?**
Sim, você pode migrar seu código personalizado, conteúdo e ativos do no local ou [!DNL Adobe-Managed Services] ambientes para [!DNL Forms] ambiente as a Cloud Service. Para obter instruções detalhadas, consulte [Migrar para o Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **Onde posso obter AEM? [!DNL Forms] as a Cloud Service [!DNL Java™] Documentação de referência da API?**
Você pode baixar a documentação de referência da API Java™ em [!DNL Maven Central Repository]. Para baixar:
   1. Ir para [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Localizar e abrir uma página contendo a versão mais recente do [!DNL Experience Manager Forms] SDK.
   1. Clique na opção Exibir tudo para exibir todos os arquivos.
   1. Baixe e extraia o `aem-forms-sdk-api-<version>-javadocs`.jar
   1. Abra o arquivo index.html para exibir a documentação de referência da API.

* **Onde posso obter [!DNL JavaScript™] Referência de API do Adaptive Forms?**
Você pode baixar [!DNL JavaScript™] Documentação de referência da API de[!DNL  Maven Central Repository]. Para baixar:
   1. Abertura [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Localizar e abrir uma página contendo a versão mais recente do [!DNL Experience Manager Forms] SDK.
   1. Clique na opção Exibir tudo para exibir todos os arquivos.
   1. Baixe e extraia o `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. Abra o arquivo index.html para exibir a documentação de referência da API.

* **Posso continuar usando temas e modelos existentes?**
Sim, você pode continuar usando os temas criados com o AEM 6.4 Forms e o AEM 6.5 Forms depois de usar o [Utilitário de migração](migrate-to-forms-as-a-cloud-service.md) para movê-los para [!DNL AEM Forms] as a Cloud Service.

  Você também pode criar um projeto com base em [!DNL AEM Forms] as a Cloud Service [Arquétipo](setup-local-development-environment.md#forms-cloud-service-local-development-environment) e use temas de amostra e modelos incluídos.

* **Posso produzir dados compatíveis com o esquema?**
Sim, você pode criar o Adaptive Forms para produzir dados compatíveis com o esquema.

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **Posso armazenar em cache o conteúdo protegido?**
O armazenamento em cache de recursos de conteúdo protegido está desativado, por padrão. Para ativar o recurso, execute as instruções fornecidas em [Armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR).

* **Eu tenho um Formulário adaptável localizado; ele não está renderizando a versão localizada? Qual pode ser a causa e como resolvê-la?**

  A convenção de URL do Adaptive Forms localizado agora permite especificar um local no URL. A nova convenção de URL permite o armazenamento em cache de formulários localizados em um Dispatcher ou CDN. No ambiente Cloud Service, use o formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um Formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. O Adobe recomenda usar o armazenamento em cache do Dispatcher ou CDN. Isso ajuda a melhorar a velocidade de renderização de formulários pré-preenchidos.

* **Atualizei um Formulário adaptável; a versão atualizada não está disponível para uso pelos clientes?**
Por padrão, a CDN atualiza o cache a cada 5 minutos, aguarda 5 minutos e verifica a versão atualizada.

* **Posso usar a etapa Assinatura em um Formulário adaptável para criar uma experiência de assinatura no navegador?**
Não, a etapa Assinatura não está disponível para [!DNL Forms] as a Cloud Service. Remova a etapa Assinatura do Adaptive Forms. Em vez da etapa Assinatura, permita que os usuários assinem um formulário adaptável após o envio. Ele ajuda você a continuar fornecendo uma experiência de assinatura no navegador.

* **Posso usar a etapa Verificar em um Formulário adaptável?**
Não, a etapa Verificar não está disponível para [!DNL Forms] as a Cloud Service. Remova a etapa de verificação do seu Forms adaptável existente antes de mover esses formulários para um ambiente Cloud Service.

* **Posso adicionar gráficos a um Formulário adaptável?**
Sim, você pode adicionar gráficos ao Forms adaptável. O Forms adaptável fornece um componente de gráfico. Você pode usá-lo para adicionar gráficos a um Formulário adaptável.

* **Posso conectar um modelo de dados de formulário a um modelo de banco de dados relacional?**
Você pode conectar um modelo de dados de formulário a [!DNL RESTful web services], [!DNL SOAP-based web services], [!DNL OData services]e o perfil de usuário Experience Manager como fontes de dados. Não há suporte disponível para conectar um modelo de dados de formulário a um banco de dados relacional.

* **Posso usar certificados personalizados com o Modelo de dados de formulário para autenticação?**
O modelo de dados de formulário não fornece um método para usar certificados personalizados para autenticação. Portanto, os certificados personalizados como x509 e SSL bidirecional não são compatíveis.

* **Posso usar a ação enviar do Forms Portal no Adaptive Forms?**

  Você pode modificar seu Forms adaptável existente para usar [Enviar para endpoint REST](configuring-submit-actions.md#submit-to-rest-endpoint), [Enviar e-mail](configuring-submit-actions.md#send-email), [Enviar usando modelo de dados do formulário](configuring-submit-actions.md#submit-using-form-data-model), e [Chamar um fluxo de trabalho de AEM](configuring-submit-actions.md#invoke-an-aem-workflow) Enviar ações. As ações de envio do Portal do Forms e do Portal do Forms ainda não estão disponíveis. Fique de olho nas notas de versão mensais para a disponibilidade dos recursos.

* **Posso usar [!DNL AEM Forms] aplicativo com [!DNL AEM Forms] as a Cloud Service?**

  Os formulários adaptáveis oferecem um design responsivo. Esses formulários alteram a aparência, o design e a interatividade com base no dispositivo subjacente. Você pode continuar usando o Adaptive Forms no dispositivo móvel enquanto acompanha as notas de versão mensais da disponibilidade dos recursos.

* **Quais recursos não fazem parte da versão inicial do GA?**
Forms Portal, [!DNL AEM Forms] aplicativo, integração com o Adobe Analytics e integração com o Adobe Target não fazem parte da versão inicial do GA. Verifique as notas de versão mensais para obter informações sobre novos recursos.

* **Eu criei um [Esquema JSON para criar um formulário adaptável](adaptive-form-json-schema-form-model.md). O esquema JSON define eventos para alguns componentes de formulários adaptáveis. O AEM Forms as a Cloud Service é compatível com eventos?**
Crie o Formulário adaptável com base no esquema JSON no ambiente Experience Manager 6.5 Forms e use o [Utilitário de migração](migrate-to-forms-as-a-cloud-service.md) para migrar o Adaptive Forms para o AEM Forms as a Cloud Service. O utilitário converte esses eventos em bibliotecas de clientes e você pode continuar usando o Forms adaptável com eventos em um ambiente Cloud Service.

<!-- 

* **Is there any AEM Forms as a Cloud Service connector for Microsoft Power Automate?**

  Yes, Adobe provides an Adobe Experience Manager connector to access [Adobe Experience Manager Forms - Communication capabilities](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) through Microsoft Power Automate. You can create a PDF document that is based on a form design and XML form data or create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) and other Printer Definition Language documents. 

  You can get started with Adobe Experience Manager easily with just a few steps:

  1. Generate the Service credentials: Use Adobe Experience Manager Developer Console to [generate](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?#generate-service-credentials) the service credentials.  
  
  1. Setup your connection: Add your service credentials to the Adobe Experience Manager Connector. You can get crdential from service credential JSON and copy these credential details to your one-time connection setup:

    * AEM Server
    * Organization ID 
    * Client ID
    * Client Secret
    * Technical Account ID
    * Meta Scopes
    * Private Key - base64 encoded keys are accepted
    * Adobe IMS Host URL

    <br> 
    
    ![Use your Service Credential JSON for credential details](assets/forms-aem-pa-connector-connection.png)

    A sample Service Credential JSON file fields mapped to Adobe Experience Manager connector for Microsoft Power Automate.

    -->


