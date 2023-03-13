---
title: Como migrar de um Forms AEM 6.5 Forms e AEM 6.4 para o [!DNL AEM Forms] as a Cloud Service ambiente?
description: Migrar de um [!DNL AEM Forms] (Ambientes no local e AMS) para [!DNL AEM Forms] ambiente as a Cloud Service
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: d9c19d0b567a9a97973c4c4e25e64722da109dbb
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 3%

---

# Migrar de um [!DNL AEM Forms] (Ambientes no local e AMS) para [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

Você pode migrar suas configurações adaptáveis do Forms, temas, modelos e nuvem do <!-- AEM 6.3 Forms--> AEM 6.4 Forms no OSGi e AEM 6.5 Forms no OSGi para [!DNL AEM] as a Cloud Service. Antes de migrar esses ativos, use o Utilitário de migração para converter o formato usado nas versões anteriores no formato usado no [!DNL AEM] as a Cloud Service. Quando você executa o Utilitário de Migração, os seguintes ativos são atualizados:

* Componentes personalizados para o Adaptive Forms
* Modelos e temas adaptáveis do Forms
* Configurações de nuvem
* Os scripts do editor de código são convertidos em funções reutilizáveis e aplicados a regras visuais.

## Considerações {#consideration}

* O serviço ajuda a migrar o conteúdo somente de [!DNL AEM Forms] em ambientes OSGi. Migrar conteúdo de [!DNL AEM Forms] no JEE para um ambiente Cloud Service não é compatível.

* (Somente para AEM 6.3 Forms ou um ambiente de versão anterior atualizado para AEM 6.4 Forms ou AEM 6.5 Forms) Forms adaptável com base em modelos prontos para uso e temas disponíveis no 6.3 AEM Forms ou versão anterior não são compatíveis com o [!DNL AEM Forms] as a Cloud Service.

* O Adobe Experience Manager Forms as a Cloud Service traz algumas alterações notáveis para os recursos existentes em comparação aos ambientes Adobe Experience Manager 6.5 Forms (On-Premise and Adobe-Managed Service). Antes de prosseguir com a migração para o serviço, [saiba mais sobre essas alterações importantes](notable-changes.md) e a variável [diferenças no nível de recurso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report) para decidir migrar com base nos recursos de que sua organização precisa.




<!-- 
## Difference with AEM 6.5 Forms 

| Feature         | Difference with AEM 6.5 Forms    |
|--------------|-----------|
| HTML5 Forms (Mobile Forms)     | The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. |
| Adaptive Forms     | <li><b>XSD-Based Adaptive Forms:</b> The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. </li> <li><b> Adaptive Form templates:</b> Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. </li><li><b>Rule editor:</b> AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor. </li> <li><b>Drafts and submissions:</b> The service does not retain metadata for drafts and submitted Adaptive Forms. </li> <li><b> Prefill Service:</b> By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. </li><li><b>Submit actions:</b> The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. </li>|
| Form Data Model | <li>Forms data model supports only HTTP and HTTPs endpoints to submit data. </li><li>Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores. The service does not support JDBC connector, Mutual SSL for Rest connector, and x509 certificate-based authentication for SOAP data sources. </li>|
| Automated Forms Conversion Service     | The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).|
|Configurations|<li>Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment. </li> <li>If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service.</li> |
| Document Manipulation APIs (Assembler Service)| The service does not support operations dependent on other services or applications: <li>Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported</li><li>Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF</li><li>Forms Service-based conversions are not supported. For example, XDP to PDF Forms.</li><li>The service does not support converting a Signed PDF or Transparent PDF to another PDF format.</li>| -->

## Pré-requisitos {#prerequisites}

* [Habilitar Forms - Inscrição digital](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) para o seu programa Forms Cloud Service e [executar o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=pt-BR).

   ![Resultado do teste](assets/enable-add-on.png)

* Em um ambiente de Cloud Service, o Utilitário de migração funciona em conjunto com a Ferramenta de mapeamento de usuários e a Ferramenta de transferência de conteúdo. O Migration Utility faz [!DNL AEM Forms] ativos compatíveis com o Cloud Service e a ferramenta de transferência de conteúdo migra o conteúdo do [!DNL AEM Forms] ambiente para um [!DNL AEM] ambiente as a Cloud Service. Antes de usar o Migration Utility, saiba mais sobre o processo de [migração para o AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html). O processo tem duas ferramentas:
   * [Ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration): a Ferramenta de mapeamento de usuários ajuda a mapear seus usuários com as contas de usuário do Adobe IMS correspondentes.
   * [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration): a ferramenta Transferência de conteúdo ajuda a preparar e transferir conteúdo de um ambiente existente para um ambiente Cloud Service.
* Contas com privilégios de administrador ativadas [!DNL AEM Forms] as a Cloud Service e seu local [!DNL AEM Forms] ambiente.
* Baixar e instalar o Analisador de práticas recomendadas, a Ferramenta de transferência de conteúdo e [!DNL AEM Forms] Utilitário de migração de [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)

* Execute o [Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) e corrija o problema relatado. Para os possíveis problemas relacionados à migração do Adobe Experience Manager Forms para o Adobe Experience Manager Forms as a Cloud Service, consulte [Detecção de padrão AEM para Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report).


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## Migrar [!DNL AEM Forms] ativos  {#use-the-migration-utility}

Execute as seguintes etapas para tornar seus [!DNL AEM Forms] ativos compatíveis com o Cloud Service e transferi-los para um [!DNL AEM] ambiente as a Cloud Service.

1. Criar um [clone](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) do seu existente [!DNL AEM Forms] ambiente.

   Sempre use o ambiente clonado para executar a Ferramenta de transferência de conteúdo e o Utilitário de migração. A Ferramenta de transferência de conteúdo e o Utilitário de migração fazem algumas alterações no conteúdo e nos ativos. Portanto, não execute a ferramenta Transferência de conteúdo e o Migration Utility em um ambiente de produção.

1. Faça logon no ambiente clonado com privilégios administrativos.

1. Execute o [Ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) para mapear seus usuários com as contas de usuário do Adobe IMS correspondentes. Você precisa de contas de usuário do Adobe IMS para fazer logon em um [!DNL AEM Forms] instância as a Cloud Service.

1. Baixe e instale o [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) e [!DNL AEM Forms] Utilitário de migração as a Cloud Service do [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) no ambiente clonado. Você pode usar o Gerenciador de pacotes AEM para instalar a ferramenta e o utilitário.

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Migração de conteúdo]**.

1. Abra o **[!UICONTROL Preparar o Forms para migração]** cartão. O navegador exibe cinco opções:
   * **[!UICONTROL Migração de ativos de AEM Forms]**
   * **[!UICONTROL Migração adaptável de componentes personalizados do Forms]**
   * **[!UICONTROL Migração adaptável de modelos do Forms]**
   * **[!UICONTROL Migração das configurações de nuvem de AEM Forms]**
   * **[!UICONTROL Migração de script do editor de código]**

1. Use a opção um após o outro para tornar seus [!DNL AEM Forms] ativos compatíveis com [!DNL AEM] as a Cloud Service:

   1. Toque **[!UICONTROL Migração de ativos do AEM Forms]** e, na próxima tela, toque em **[!UICONTROL Iniciar migração]**. Ele coloca o Forms adaptável e temas em seu [!DNL AEM Forms] ambiente compatível com [!DNL AEM] as a Cloud Service.

   1. Toque **[!UICONTROL Migração adaptável de componentes personalizados do Forms]** e na página Migração de componentes personalizados, toque em **[!UICONTROL Iniciar migração]**. Ele faz com que qualquer componente personalizado desenvolvido para Forms adaptável e sobreposições de componentes no seu [!DNL AEM Forms] ambiente compatível com [!DNL AEM] as a Cloud Service.

   1. Toque **[!UICONTROL Migração de modelo adaptável do Forms]** e na página Migração de componentes personalizados, toque em **[!UICONTROL Iniciar migração]**. Ele torna os modelos de Formulário adaptável em /apps ou /conf e criados usando o Editor de modelo AEM compatíveis com [!DNL AEM] as a Cloud Service.

   1. Toque **[!UICONTROL Migração de configurações da AEM Forms Cloud]** e, na página Migração de configuração, toque em **[!UICONTROL Iniciar migração]**. Ele atualiza e move os seguintes Cloud Services para um novo local:

      * Cloud Service do modelo de dados de formulário
      * Cloud Service Google reCAPTCHA
      * [!DNL Adobe Sign] Serviço em nuvem
      * Cloud Service Adobe Fonts
   1. Toque **[!UICONTROL Migração de script do editor de código]**, especifique um local para salvar funções reutilizáveis e toque em **[!UICONTROL Iniciar migração].

   O Cloud Service não é compatível com scripts do editor de regras. A variável **[!UICONTROL Migração de script do editor de código]** a ferramenta converte todos os scripts de regras em seu ambiente em funções reutilizáveis e aplica as funções reutilizáveis ao editor visual no local apropriado. Essas funções reutilizáveis são salvas na forma de bibliotecas de clientes e ajudam a manter a funcionalidade existente intacta. A ferramenta aplica automaticamente as funções reutilizáveis geradas ao Forms adaptável correspondente.

   Use o [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) para exportar as funções reutilizáveis (Bibliotecas de clientes) para um pacote.

1. [Implantar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) o pacote de funções reutilizáveis (bibliotecas de clientes), [código personalizado, componentes, configurações](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager), bibliotecas personalizadas específicas do local para o seu [!DNL AEM] ambiente as a Cloud Service.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Execute o [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). Ao especificar parâmetros na variável **[!UICONTROL Criar conjunto de migração]** , especifique o caminho do Forms adaptável, temas, modelos, Modelos de dados de formulário, Cloud Services, Componentes personalizados e outros ativos específicos do AEM Forms para o **[!UICONTROL Caminhos a serem incluídos]** opção. Ele adiciona informações [!DNL AEM Forms] ativos para o conjunto de migração.

## Caminhos de vários ativos específicos do AEM Forms

* **Forms adaptável**: você pode encontrar formulários adaptáveis em `/content/dam/formsanddocuments/`e /content/forms/af. Por exemplo, para um formulário adaptável chamado Registro WKND, adicione caminhos `/content/dam/formsanddocuments/wknd-registration` e `/content/forms/af/wknd-registration`.
* **Modo de dados de formulário**: todos os modelos de dados de formulário estão disponíveis em `/content/dam/formsanddocuments-fdm`. Por exemplo, `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Bibliotecas de clientes**: o caminho padrão das bibliotecas de clientes é `/etc/clientlibs/fd/theme`.

* **Modelos de formulário adaptável**: o caminho padrão dos modelos é `/conf/<template folder>`. Por exemplo, para um modelo chamado caminho de adição básico `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Temas do formulário adaptável e bibliotecas de clientes**: o caminho padrão dos temas é ` /content/dam/formsanddocuments-themes/` e o caminho padrão das bibliotecas de clientes é `/etc/clientlibs/fd/theme`. Por exemplo, para um modelo chamado Tema WKND, adicione o caminho ` /content/dam/formsanddocuments-themes/wkndtheme` e bibliotecas de clientes para o tema em `/etc/clientlibs/reference-themes/wkndtheme-3-0`. Você também pode ter temas e bibliotecas de clientes em outros caminhos personalizados.

* **Configurações da nuvem**: você pode encontrar as Configurações de nuvem em `/conf/`. Por exemplo, a configuração da nuvem do modelo de dados de formulário está em `/conf/global/settings/cloudconfigs/fdm`.

* **Modelo de fluxo de trabalho**: você pode encontrar modelos de fluxo de trabalho do AEM em `/conf/global/settings/workflow/models/`. Por exemplo, para um modelo de fluxo de trabalho chamado Registro WKND, adicione o caminho `/conf/global/settings/workflow/models/wknd-registration`

Você pode adicionar os caminhos de pasta de nível superior listados abaixo ou caminhos de pasta específicos, conforme descrito abaixo. Ela permite migrar um determinado ativo e todos os ativos e formulários de uma só vez.

* /content/dam/formsanddocuments-fdm
* /content/dam/formsanddocuments/themes
* /content/forms/af
* /etc/clientlibs/fd/theme

Para migrar modelos de fluxo de trabalho do AEM, especifique os seguintes caminhos:

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/models
