---
title: Perguntas frequentes as a Cloud Service da Forms
description: Perguntas frequentes as a Cloud Service da Forms
contentOwner: khsingh
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
source-git-commit: a5cd8a49a74eb8372d1d363ff859e1aef921859b
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 2%

---

# Perguntas frequentes {#frequently-asked-questions}

* **Posso usar o Editor de códigos para criar regras?**
Você pode usar o Editor visual para criar as regras. O Editor de códigos não está disponível em [!DNL Forms] as a Cloud Service. Se o Formulário adaptável usar scripts de regras desenvolvidos com o editor de códigos, use a [Utilitário de migração](migrate-to-forms-as-a-cloud-service.md) para converter seus scripts de código em funções personalizadas. Você pode usar funções personalizadas com o Visual Editor para continuar obtendo os resultados obtidos com o Editor de códigos.

* **Posso criar um formulário adaptável baseado em XFA em instâncias do Cloud Service?**
Sim, você pode criar um Formulário adaptável baseado em XFA na instância do Cloud Service. No entanto, o suporte para Forms adaptável baseado em XFA não está disponível para o SDK as a Cloud Service da AEM Forms (ambiente de desenvolvimento local). Se você pretende usar o Forms adaptável baseado em XFA com o SDK as a Cloud Service da AEM Forms, entre em contato com o Suporte do Adobe com detalhes do caso de uso e requisitos específicos.

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **Posso migrar o conteúdo de um No local ou [!DNL Adobe-Managed Services] ambientes para [!DNL Forms] Ambiente as a Cloud Service?**
Sim, você pode migrar o código, o conteúdo e os ativos personalizados do local ou [!DNL Adobe-Managed Services] ambientes para [!DNL Forms] Ambiente as a Cloud Service. Para obter instruções detalhadas, consulte [Migrar para o Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **Onde posso obter AEM [!DNL Forms] as a Cloud Service [!DNL Java™] Documentação de referência da API?**
Você pode baixar a documentação de referência da API Java™ em [!DNL Maven Central Repository]. Para baixar:
   1. Ir para [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Localize e abra a página que contém a versão mais recente de [!DNL Experience Manager Forms] SDK.
   1. Clique na opção Exibir todos para exibir todos os arquivos.
   1. Baixe e extraia o `aem-forms-sdk-api-<version>-javadocs`.jar.
   1. Abra o arquivo index.html para exibir a documentação de referência da API.

* **Onde posso chegar [!DNL JavaScript™] Referência de API para Adaptive Forms?**
Você pode baixar [!DNL JavaScript™] Documentação de referência da API de[!DNL  Maven Central Repository]. Para baixar:
   1. Abrir [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Localize e abra a página que contém a versão mais recente de [!DNL Experience Manager Forms] SDK.
   1. Clique na opção Exibir todos para exibir todos os arquivos.
   1. Baixe e extraia o `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. Abra o arquivo index.html para exibir a documentação de referência da API.

* **Posso continuar usando temas e modelos existentes?**
Sim, você pode continuar usando os temas criados com AEM 6.4 Forms e AEM 6.5 Forms depois de usar a variável [Utilitário de migração](migrate-to-forms-as-a-cloud-service.md) para movê-los para [!DNL AEM Forms] as a Cloud Service.

   Você também pode criar um projeto com base em [!DNL AEM Forms] as a Cloud Service [Arquétipo](setup-local-development-environment.md#forms-cloud-service-local-development-environment) e use temas e modelos de amostra incluídos.

* **Posso produzir dados compatíveis com o esquema?**
Sim, você pode criar o Adaptive Forms para produzir dados compatíveis com o esquema.

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **Posso armazenar em cache o conteúdo protegido?**
O armazenamento em cache de recursos de conteúdo protegido está desativado, por padrão. Para ativar o recurso, você pode executar as instruções fornecidas em [Armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

* **Tenho um formulário adaptável localizado; não está renderizando a versão localizada? Qual poderia ser a causa e como resolvê-la?**

   A convenção de URL do Adaptive Forms localizado agora é compatível com a especificação de um local no URL. A nova convenção de URL permite o armazenamento em cache de formulários localizados em um Dispatcher ou CDN. No ambiente Cloud Service , use o formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. O Adobe recomenda usar o armazenamento em cache do Dispatcher ou CDN. Ajuda a melhorar a velocidade de renderização dos formulários pré-preenchidos.

* **Atualizei um formulário adaptável; a versão atualizada não está disponível para uso pelos clientes?**
Por padrão, o CDN atualiza o cache a cada 5 minutos, espera por 5 minutos e verifica a versão atualizada.

* **Posso usar a etapa Assinatura em um formulário adaptável para criar uma experiência de assinatura no navegador?**
Não, a etapa Assinatura não está disponível para [!DNL Forms] as a Cloud Service. Remova a etapa Assinatura no Adaptive Forms. Em vez da etapa Assinatura, permita que os usuários assinem um formulário adaptável após o envio. Ajuda a continuar fornecendo uma experiência de assinatura no navegador.

* **Posso usar a etapa Verificar em um formulário adaptável?**
Não, a etapa Verificar não está disponível para [!DNL Forms] as a Cloud Service. Remova a etapa de verificação do seu Adaptive Forms existente antes de movê-los para um ambiente Cloud Service.

* **Posso adicionar gráficos a um formulário adaptável?**
Sim, você pode adicionar gráficos ao Adaptive Forms. O Adaptive Forms fornece um componente gráfico. Você pode usá-lo para adicionar gráficos a um Formulário adaptável.

* **Posso conectar um Modelo de Dados de Formulário a um modelo de banco de dados relacional?**
Você pode conectar um Modelo de dados de formulário a [!DNL RESTful web services], [!DNL SOAP-based web services], [!DNL OData services]e perfil de usuário do Experience Manager como fontes de dados. Não há suporte para conectar um Modelo de dados de formulário a um banco de dados relacional.

* **Posso usar certificados personalizados com o Modelo de dados de formulário para autenticação?**
O Modelo de dados de formulário não fornece um método para usar certificados personalizados para autenticação. Portanto, os certificados personalizados, como x509 e SSL bidirecional, não são compatíveis.

* **Posso usar a ação de envio do Forms Portal no Adaptive Forms?**

   Você pode modificar seu Adaptive Forms existente para usar [Enviar para ponto de extremidade REST](configuring-submit-actions.md#submit-to-rest-endpoint), [Enviar email](configuring-submit-actions.md#send-email), [Enviar usando o Modelo de dados de formulário](configuring-submit-actions.md#submit-using-form-data-model)e [Chamar um fluxo de trabalho AEM](configuring-submit-actions.md#invoke-an-aem-workflow) Enviar ações. A ação de envio do Portal Forms e do Forms Portal ainda não está disponível. Fique de olho nas notas de versão mensais para ver a disponibilidade dos recursos.

* **Posso usar [!DNL AEM Forms] aplicativo com [!DNL AEM Forms] as a Cloud Service?**

   Os formulários adaptáveis oferecem um design responsivo. Esses formulários alteram a aparência, o design e a interatividade com base no dispositivo subjacente. Você pode continuar usando o Adaptive Forms em dispositivos móveis e, ao mesmo tempo, acompanhar as notas de versão mensais da disponibilidade dos recursos.

* **Quais recursos não fazem parte da versão inicial do GA?**
Portal Forms, [!DNL AEM Forms] aplicativos, integração com o Adobe Analytics e integração com o Adobe Target não fazem parte da versão inicial do GA. Procure notas de versão mensais para obter informações sobre novos recursos.

* **Eu criei um [Esquema JSON para criar um formulário adaptável](adaptive-form-json-schema-form-model.md). O esquema JSON define eventos para alguns componentes de formulários adaptáveis. O AEM Forms as a Cloud Service é compatível com eventos?**
Crie o Formulário adaptável com base no esquema JSON no ambiente Experience Manager 6.5 Forms e use o [Utilitário de migração](migrate-to-forms-as-a-cloud-service.md) para migrar o Adaptive Forms para o AEM Forms as a Cloud Service. O utilitário converte esses eventos em bibliotecas do cliente e você pode continuar usando o Adaptive Forms com eventos em um ambiente Cloud Service.

