---
title: Como podemos migrar do AEM 6.5 Forms para o AEM Forms as a Cloud Service?
description: Introdução à Jornada de migração para o AEM as a Cloud Service | Adobe Experience Manager. Migrar de um(a) [!DNL AEM Forms] (ambientes no local e AMS) para o(a) [!DNL AEM Forms] ambiente(a) as a Cloud Service.
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, migrate 6.5 forms to CS, migrate 6.5 forms to cloud service, upgrade 6.5 forms to CS, move 6.5 forms to CS, upgrade AEM 6.5 to CS, AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Migration Journey to AEM as a Cloud Service | Adobe Experience Manager.
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 1%

---

# Migração de um [!DNL AEM Forms] (ambientes no local e AMS) para um ambiente [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/upgrade.html) |
| AEM as a Cloud Service | Este artigo |

Você pode migrar ou atualizar seu Forms adaptável, temas, modelos e configurações de nuvem do <!-- AEM 6.3 Forms AEM 6.4 Forms on OSGi and --> AEM 6.5 Forms no OSGi para o [!DNL AEM] as a Cloud Service. Antes de migrar esses ativos, use o Utilitário de Migração para converter o formato usado nas versões anteriores no formato usado em [!DNL AEM] as a Cloud Service.
Vamos começar com a jornada de migração para o AEM as a Cloud Service | Adobe Experience Manager. Quando você executa o Utilitário de Migração, os seguintes ativos são atualizados:

* Componentes personalizados para o Adaptive Forms
* Modelos e temas adaptáveis do Forms
* Configurações de nuvem
* Os scripts do editor de código são convertidos em funções reutilizáveis e aplicados a regras visuais.

## Considerações sobre a migração para o Forms as a Cloud Service {#consideration}

Para migrar do AEM 6.5 Forms para o AEM Cloud Service, é importante considerar os seguintes pontos:

* O serviço ajuda a migrar o conteúdo somente de [!DNL AEM Forms] em ambientes OSGi. Não há suporte para a migração de conteúdo de [!DNL AEM Forms] no JEE para um ambiente Cloud Service.

* (Somente para versões anteriores ao AEM 6.5 Forms) O Adaptive Forms AEM com base em modelos e temas prontos para uso disponíveis no 6.3 Forms ou na versão anterior não são compatíveis com o [!DNL AEM Forms] as a Cloud Service.

* O Adobe Experience Manager Forms as a Cloud Service traz algumas alterações notáveis para os recursos existentes em comparação aos ambientes Adobe Experience Manager 6.5 Forms (On-Premise and Adobe-Managed Service). Antes de continuar com a migração para o serviço, [saiba mais sobre essas alterações importantes](notable-changes.md) e as [diferenças no nível de recursos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report) para decidir migrar com base nos recursos exigidos pela sua organização.




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

Para garantir uma transição sem problemas do ambiente do AEM Forms 6.5 para o AEM as a Cloud Service, é importante considerar os seguintes pré-requisitos:

* Habilite a opção [Forms - Inscrição Digital](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) para o seu programa Cloud Service do Forms e [execute o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=pt-BR).

  ![Resultado do teste](assets/enable-add-on.png)

* Em um ambiente de Cloud Service, o Utilitário de migração funciona em conjunto com a Ferramenta de mapeamento de usuários e a Ferramenta de transferência de conteúdo. O Utilitário de migração torna os ativos do [!DNL AEM Forms] compatíveis com o Cloud Service e a ferramenta de transferência de conteúdo migra o conteúdo do seu ambiente [!DNL AEM Forms] para um ambiente as a Cloud Service [!DNL AEM]. Antes de usar o Utilitário de Migração, saiba mais sobre o processo de [migração para o AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html). O processo tem duas ferramentas:
   * [Ferramenta de mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration): a Ferramenta de mapeamento de usuários ajuda a mapear seus usuários com as contas de usuário do Adobe IMS correspondentes.
   * [Ferramenta de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration): a ferramenta de transferência de conteúdo ajuda a preparar e transferir conteúdo de um ambiente existente para um ambiente Cloud Service. Ele ajuda os usuários a atualizar facilmente do AEM Forms para o ambiente de nuvem.
* Contas com privilégios de administrador em [!DNL AEM Forms] as a Cloud Service e seu ambiente [!DNL AEM Forms] local.
* Baixe e instale o Analisador de Práticas Recomendadas, a Ferramenta de Transferência de Conteúdo e o Utilitário de Migração do [!DNL AEM Forms] do [Portal de Distribuição de Software.](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)

* Execute a ferramenta [Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) e corrija o problema relatado. Para os possíveis problemas relacionados à migração do Adobe Experience Manager Forms para o Adobe Experience Manager Forms as a Cloud Service AEM, consulte [Detecção de padrão do para Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report).


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->




## Migrar [!DNL AEM 6.5 Forms] ativos para o AEM Cloud Service {#use-the-migration-utility}

Execute as etapas a seguir para tornar seus ativos do [!DNL AEM Forms] compatíveis com o Cloud Service e transferi-los para um ambiente as a Cloud Service do [!DNL AEM].

1. Crie um [clone](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) de seu ambiente [!DNL AEM Forms] existente.

   >[!NOTE]
   >
   > Ao migrar do 6.5 para o Cloud Service, é recomendável usar o ambiente clonado para executar a ferramenta Transferência de conteúdo e o Migration Utility. A Ferramenta de transferência de conteúdo e o Utilitário de migração fazem algumas alterações no conteúdo e nos ativos. Portanto, não execute a ferramenta Transferência de conteúdo e o Migration Utility em um ambiente de produção.

1. Faça logon no ambiente clonado com privilégios administrativos.

1. Execute a [Ferramenta de Mapeamento de Usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) para mapear seus usuários com as contas de usuário do Adobe IMS correspondentes. Você precisa de contas de usuário do Adobe IMS para fazer logon em uma instância as a Cloud Service do [!DNL AEM Forms].

1. Baixe e instale o [Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) e o [!DNL AEM Forms] as a Cloud Service Migration Utility do [Portal de Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) no ambiente clonado. Você pode usar o Gerenciador de pacotes AEM para instalar a ferramenta e o utilitário.

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Migração de Conteúdo]**.

1. Abra o cartão **[!UICONTROL Preparar o Forms para migração]**. O navegador exibe cinco opções:
   * **[!UICONTROL Migração do AEM Forms Assets]**
   * **[!UICONTROL Migração de componentes personalizados adaptáveis do Forms]**
   * **[!UICONTROL Migração de Modelos Adaptáveis do Forms]**
   * **[!UICONTROL Migração de configurações de nuvem do AEM Forms]**
   * **[!UICONTROL Migração de Scripts do Editor de Códigos]**

1. Use a opção um após o outro para tornar os ativos do [!DNL AEM Forms] compatíveis com o [!DNL AEM] as a Cloud Service:

   1. Selecione **[!UICONTROL Migração do AEM Forms Assets]** e, na próxima tela, selecione **[!UICONTROL Iniciar Migração]**. Isso torna o Adaptive Forms e temas em seu ambiente [!DNL AEM Forms] compatíveis com o [!DNL AEM] as a Cloud Service.

   1. Selecione **[!UICONTROL Migração de componentes personalizados adaptáveis do Forms]** e, na página Migração de componentes personalizados, selecione **[!UICONTROL Iniciar Migração]**. Ele torna qualquer componente personalizado desenvolvido para o Forms adaptável e as sobreposições de componentes no ambiente [!DNL AEM Forms] compatíveis com o [!DNL AEM] as a Cloud Service.

   1. Selecione **[!UICONTROL Migração de modelo de Forms adaptável]** e, na página Migração de componentes personalizados, selecione **[!UICONTROL Iniciar Migração]**. Ele torna os modelos de Formulário Adaptável em `/apps` ou `/conf` e criados usando o Editor de Modelos AEM compatíveis com o [!DNL AEM] as a Cloud Service.

   1. Selecione **[!UICONTROL Migração de Configurações de Nuvem do AEM Forms]** e, na página Migração de Configurações, selecione **[!UICONTROL Iniciar Migração]**. Ele atualiza e move os seguintes Cloud Service para um novo local:

      * Cloud Service do modelo de dados de formulário
      * Cloud Service Google reCAPTCHA
      * Cloud Service [!DNL Adobe Sign]
      * Cloud Service Adobe Fonts

   1. Selecione **[!UICONTROL Migração de Scripts do Editor de Códigos]**, especifique um local para salvar funções reutilizáveis e selecione **[!UICONTROL Iniciar Migração].

   O Cloud Service não é compatível com scripts do editor de regras. A ferramenta **[!UICONTROL Migração de scripts do editor de códigos]** converte todos os scripts de regras no seu ambiente em funções reutilizáveis e aplica as funções reutilizáveis ao editor visual no local apropriado. Essas funções reutilizáveis são salvas na forma de bibliotecas de clientes e ajudam a manter a funcionalidade existente intacta. A ferramenta aplica automaticamente as funções reutilizáveis geradas ao Forms adaptável correspondente.

   Migração de formulário AEM para Cloud Service, use o [Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) para exportar as funções reutilizáveis (Bibliotecas de Clientes) para um pacote.

1. [Implante](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) o pacote de funções reutilizáveis (Bibliotecas de Clientes), [código personalizado, componentes, configurações](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager), bibliotecas personalizadas específicas da localidade para seu ambiente as a Cloud Service [!DNL AEM].

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Execute a [Ferramenta de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). Ao especificar parâmetros na tela **[!UICONTROL Criar Conjunto de Migração]**, especifique o caminho do Forms Adaptável, temas, modelos, Modelo de Dados de Formulário (FDM), Cloud Service, Componentes Personalizados e outros ativos específicos do AEM Forms para a opção **[!UICONTROL Caminhos a serem incluídos]**. Ele adiciona os [!DNL AEM Forms] ativos especificados ao conjunto de migração.

## Caminhos de vários ativos específicos do AEM Forms

Ao migrar do AEM Forms 6.5 para o Cloud Service, você pode localizar os ativos específicos do AEM Forms em:

* **Forms adaptável**: você pode encontrar formulários adaptáveis em `/content/dam/formsanddocuments/`e `/content/forms/af`. Por exemplo, para um formulário adaptável chamado Registro WKND, adicione os caminhos `/content/dam/formsanddocuments/wknd-registration` e `/content/forms/af/wknd-registration`.
* **Modelo de dados de formulário**: você pode encontrar todo o Modelo de dados de formulário (FDM) em `/content/dam/formsanddocuments-fdm`. Por exemplo, `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Bibliotecas de clientes**: o caminho padrão das bibliotecas de clientes é `/etc/clientlibs/fd/theme`.

* **Modelos de formulário adaptável**: o caminho padrão dos modelos é `/conf/<template folder>`. Por exemplo, para um modelo intitulado caminho de adição básico `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Temas de formulários adaptáveis e bibliotecas de clientes**: o caminho padrão de temas é ` /content/dam/formsanddocuments-themes/` e o caminho padrão de bibliotecas de clientes é `/etc/clientlibs/fd/theme`. Por exemplo, para um modelo intitulado Tema WKND, adicione o caminho ` /content/dam/formsanddocuments-themes/wkndtheme` e as bibliotecas de clientes para o tema em `/etc/clientlibs/reference-themes/wkndtheme-3-0`. Você também pode ter temas e bibliotecas de clientes em outros caminhos personalizados.

* **Configurações de Nuvem**: você pode encontrar Configurações de Nuvem em `/conf/`. Por exemplo, a configuração de nuvem do Modelo de dados de formulário (FDM) está em `/conf/global/settings/cloudconfigs/fdm`.

* **Modelo de Fluxo de Trabalho**: você pode encontrar modelos de Fluxo de Trabalho do AEM em `/conf/global/settings/workflow/models/`. Por exemplo, para um modelo de fluxo de trabalho chamado Registro WKND, adicione o caminho `/conf/global/settings/workflow/models/wknd-registration`

Você pode adicionar os caminhos de pasta de nível superior listados abaixo ou caminhos de pasta específicos, conforme descrito abaixo. Ela permite migrar um determinado ativo e todos os ativos e formulários de uma só vez, ao atualizar do AEM Forms 6.5 para o Cloud Service.

* `/content/dam/formsanddocuments-fdm`
* `/content/dam/formsanddocuments/themes`
* `/content/forms/af`
* `/etc/clientlibs/fd/theme`

Ao migrar modelos de fluxo de trabalho do AEM do AEM Forms 6.5 para o Cloud Service, especifique os seguintes caminhos:

* `/conf/global/settings/workflow/models/`
* `/conf/global/settings/workflow/launcher`
* `/var/workflow/models`

## Ver próximo

* [Alterações importantes para usuários existentes do Adobe Experience Manager 6.5 Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/notable-changes.html)
* [Integrar ao AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service.html)
* [Criar o primeiro formulário adaptável no Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=pt-br)

## Informações adicionais

O utilitário de migração ajuda a migrar o Adaptive Forms com base em componentes de base. Além disso, o Forms as a Cloud Service suporta os Componentes principais adaptáveis do Forms. Assim, você pode:

* [Criar Forms adaptável independente baseado em Componente principal](/help/forms/creating-adaptive-form-core-components.md)
* [Criar formulário adaptável baseado em Componente principal diretamente em uma página do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

Para saber mais sobre o AEM Forms as a Cloud Service, consulte:

* [Introdução ao Cloud Service AEM Forms](/help/forms/home.md)
* [Inovações no Cloud Service AEM Forms](/help/forms/latest-innovations.md)