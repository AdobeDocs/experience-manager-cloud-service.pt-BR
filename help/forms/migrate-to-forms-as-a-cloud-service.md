---
title: Como migrar de um Forms AEM 6.5 e Forms AEM 6.4 para [!DNL AEM Forms] Ambiente as a Cloud Service?
description: Migrar de um [!DNL AEM Forms] Ambiente local para [!DNL AEM Forms] Ambiente as a Cloud Service
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: b11979acc23efe5f1af690443180a6b456d589ed
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 5%

---

# Migrar para o [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

Você pode migrar sua Forms adaptativa, temas, modelos e configurações de nuvem do <!-- AEM 6.3 Forms--> AEM 6.4 Forms em OSGi e AEM 6.5 Forms em OSGi para [!DNL AEM] as a Cloud Service. Antes de migrar esses ativos, use o Utilitário de migração para converter o formato usado nas versões anteriores para o formato usado em [!DNL AEM] as a Cloud Service. Ao executar o Utilitário de migração, os seguintes ativos são atualizados:

* Componentes personalizados para o Adaptive Forms
* Modelos e temas adaptáveis do Forms
* Configurações da nuvem
* Os scripts do editor de código são convertidos em funções reutilizáveis e aplicados a regras visuais.

## Considerações {#consideration}

* O serviço ajuda a migrar o conteúdo somente do [!DNL AEM Forms] em ambientes OSGi. Migrar conteúdo de [!DNL AEM Forms] no JEE para um ambiente Cloud Service não é suportado.

* (Somente para o AEM 6.3 Forms ou um ambiente de versão anterior atualizado para AEM 6.4 Forms ou AEM 6.5 Forms) O Adaptive Forms baseado em modelos e temas prontos para uso no AEM 6.3 Forms ou versão anterior não são suportados em [!DNL AEM Forms] as a Cloud Service.

* A etapa Verificar não está disponível. Remova a etapa de verificação do seu Adaptive Forms existente antes de movê-los para um ambiente Cloud Service.

* A etapa de assinatura do Adaptive Forms não está disponível. Remova a etapa Assinatura de um formulário adaptável existente. Configurar o formulário adaptável para usar a experiência de assinatura no navegador. Ele exibe o contrato do Adobe Acrobat Sign para assinar o contrato dentro do navegador no envio de um formulário adaptável. A experiência de assinatura no navegador ajuda a fornecer uma experiência de assinatura mais rápida e economiza tempo para o signatário.

## Diferença com o AEM 6.5 Forms

| Recurso | Diferença com o AEM 6.5 Forms |
|--------------|-----------|
| HTML5 Forms (Mobile Forms) | O serviço não é compatível com o HTML5 Forms (Mobile Forms). Se você renderizar os formulários baseados em XDP como HTML5 Forms, poderá continuar usando o recurso no AEM 6.5 Forms. |
| Formulários adaptáveis | <li><b>Forms adaptável baseado em XSD:</b> O serviço não é compatível com o HTML5 Forms (Mobile Forms). Se você renderizar os formulários baseados em XDP como HTML5 Forms, poderá continuar usando o recurso no AEM 6.5 Forms. </li> <li><b> Modelos de formulário adaptável:</b> Use o pipeline de criação e o repositório Git correspondente do seu programa para importar modelos de Formulário adaptável existentes. </li><li><b>Editor de regras:</b> O AEM Forms as a Cloud Service oferece uma [Editor de regras](rule-editor.md#visual-rule-editor). O editor de código não está disponível no Forms as a Cloud Service. O utilitário de migração ajuda a migrar os formulários que têm regras personalizadas (criadas no editor de códigos). O utilitário converte essas regras em funções personalizadas compatíveis com o Forms as a Cloud Service. Você pode usar as funções reutilizáveis com o Editor de regras para continuar a obter resultados obtidos com os scripts de regras `onSubmitError` ou `onSubmitSuccess` agora estão disponíveis como ações no Editor de regras. </li> <li><b>Rascunhos e envios:</b> O serviço não retém metadados para rascunhos e Forms adaptável enviado. </li> <li><b> Serviço de preenchimento prévio:</b> Por padrão, o serviço de preenchimento prévio mescla dados com um formulário adaptável no cliente em vez de mesclar dados no servidor no AEM 6.5 Forms. O recurso ajuda a melhorar o tempo necessário para preencher previamente um formulário adaptável. Você sempre pode configurar para executar a ação de mesclagem no Adobe Experience Manager Forms Server. </li><li><b>Enviar ações:</b> O **Enviar email como PDF** não está disponível. O **Email** a ação enviar fornece opções para enviar anexos e anexar Documento de registro (DoR) com email. </li> |
| Modelo de dados do formulário | <li>O modelo de dados Forms oferece suporte somente a pontos de extremidade HTTP e HTTP para o envio de dados. </li><li>O Forms as a Cloud Service permite usar o Microsoft Azure Blob, o Microsoft Sharepoint, o Microsoft OneDrive e serviços compatíveis com operações CRUD gerais (Criar, Ler, Atualizar e Excluir) como armazenamentos de dados. O serviço não é compatível com o conector JDBC, o SSL Mútuo para o conector Rest e a autenticação baseada em certificado x509 para fontes de dados SOAP. </li> |
| Serviço Automated forms conversion | O serviço não fornece metamodelo para o Automated forms conversion Service. Você pode [baixe-o na documentação do Automated forms conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model). |
| Configurações | <li>Por padrão, o suporte a email é compatível somente com protocolos HTTP e HTTPs. [Entre em contato com a equipe de suporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) para habilitar as portas para enviar emails e habilitar o protocolo SMTP para seu ambiente. </li> <li>Se você usar pacotes personalizados, recompile seu código com a versão mais recente do adobe-aemfd-docmanager antes de usar esses pacotes com o Forms as a Cloud Service.</li> |
| APIs de Manipulação de Documento (Serviço Assembler) | O serviço não suporta operações dependentes de outros serviços ou aplicações: <li>Não há suporte para a conversão de documentos em um formato que não seja PDF para um formato PDF. Por exemplo, o Microsoft Word para o PDF, o Microsoft Excel para o PDF e o HTML para o PDF não são suportados</li><li>Não há suporte para conversões baseadas em Distiller do Adobe. Por exemplo, PostScript(PS) para PDF</li><li>Não há suporte para conversões baseadas no Forms Service. Por exemplo, XDP para PDF forms.</li><li>O serviço não oferece suporte à conversão de PDF assinado ou PDF transparente para outro formato PDF.</li> |

## Pré-requisitos {#prerequisites}

* [Ativar o Forms - Inscrição digital](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) para seu programa Forms Cloud Service e [executar o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

   ![Resultado do teste](assets/enable-add-on.png)

* Em um ambiente Cloud Service, o Utilitário de migração funciona em conjunto com a Ferramenta de mapeamento de usuários e a Ferramenta de transferência de conteúdo. O Utilitário de migração faz [!DNL AEM Forms] ativos compatíveis com o Cloud Service e a ferramenta de transferência de conteúdo migram o conteúdo do [!DNL AEM Forms] ambiente a um [!DNL AEM] Ambiente as a Cloud Service. Antes de usar o Utilitário de migração, aprenda o processo de [mudança para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html). O processo tem duas ferramentas:
   * [Ferramenta de mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration): A Ferramenta de mapeamento de usuários ajuda a mapear seus usuários com as contas de usuário correspondentes do Adobe IMS.
   * [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration): A ferramenta Transferência de conteúdo ajuda você a preparar e transferir o conteúdo do ambiente existente para um ambiente Cloud Service.
* Contas com privilégios de administrador em [!DNL AEM Forms] as a Cloud Service e local [!DNL AEM Forms] ambiente.
* Baixe e instale o Analisador de práticas recomendadas, a ferramenta Transferência de conteúdo e [!DNL AEM Forms] Utilitário de migração de [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)

* Execute o [Analisador de práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) e corrija o problema reportado.

<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## Migrar [!DNL AEM Forms] ativos  {#use-the-migration-utility}

Execute as etapas a seguir para criar [!DNL AEM Forms] ativos compatíveis com o Cloud Service e transferi-los para um [!DNL AEM] Ambiente as a Cloud Service.

1. Crie um [clone](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) do seu [!DNL AEM Forms] ambiente.

   Sempre use o ambiente clonado para executar a ferramenta Transferência de conteúdo e o utilitário de migração. A ferramenta Transferência de conteúdo e o utilitário de migração fazem algumas alterações no conteúdo e nos ativos. Portanto, não execute a ferramenta Transferência de conteúdo e o utilitário de migração em um ambiente de produção.

1. Faça logon no ambiente clonado com privilégios administrativos.

1. Execute o [Ferramenta de mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) para mapear os usuários com as contas de usuário correspondentes do Adobe IMS. Você precisa de contas de usuário do Adobe IMS para fazer logon em um [!DNL AEM Forms] Instância as a Cloud Service.

1. Baixe e instale o [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) e [!DNL AEM Forms] Utilitário de migração as a Cloud Service de [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) sobre o ambiente clonado. Você pode usar AEM Gerenciador de pacotes para instalar a ferramenta e o utilitário.

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Migração de conteúdo]**.

1. Abra o **[!UICONTROL Preparar o Forms para migração]** cartão. O navegador exibe cinco opções:
   * **[!UICONTROL Migração de ativos de AEM Forms]**
   * **[!UICONTROL Migração de componentes personalizados adaptáveis do Forms]**
   * **[!UICONTROL Migração de modelos adaptáveis do Forms]**
   * **[!UICONTROL Migração das configurações de nuvem de AEM Forms]**
   * **[!UICONTROL Migração de script do editor de código]**

1. Use a opção um após o outro para tornar sua [!DNL AEM Forms] ativos compatíveis com [!DNL AEM] as a Cloud Service:

   1. Toque **[!UICONTROL Migração de ativos do AEM Forms]** e na próxima tela, toque em **[!UICONTROL Iniciar migração]**. Torna a Adaptive Forms e os temas em seu [!DNL AEM Forms] compatível com o ambiente [!DNL AEM] as a Cloud Service .

   1. Toque **[!UICONTROL Migração de componentes personalizados adaptáveis do Forms]** e, na página Migração de componentes personalizados, toque em **[!UICONTROL Iniciar migração]**. Ele torna qualquer componente personalizado desenvolvido para o Adaptive Forms e as sobreposições de componentes em seu [!DNL AEM Forms] compatível com o ambiente [!DNL AEM] as a Cloud Service .

   1. Toque **[!UICONTROL Migração de modelo adaptável do Forms]** e, na página Migração de componentes personalizados, toque em **[!UICONTROL Iniciar migração]**. Ele torna os modelos de formulário adaptável em /apps ou /conf e é criado usando AEM Editor de modelo compatível com [!DNL AEM] as a Cloud Service .

   1. Toque **[!UICONTROL Migração de configurações da AEM Forms Cloud]** e, em seguida, na página Migração de configuração , toque em **[!UICONTROL Iniciar migração]**. Ele atualiza e move os seguintes Cloud Services para um novo local:

      * Cloud Service de Modelo de dados de formulário
      * Cloud Service Google reCAPTCHA
      * [!DNL Adobe Sign] Serviço em nuvem
      * Cloud Service Adobe Fonts
   1. Toque **[!UICONTROL Migração de script do editor de código]**, especifique um local para salvar funções reutilizáveis e toque em **[!UICONTROL Iniciar migração].

   O Cloud Service não suporta scripts do editor de regras. O **[!UICONTROL Migração de script do editor de códigos]** A ferramenta converte todos os scripts de regras em seu ambiente para funções reutilizáveis e aplica as funções reutilizáveis ao editor visual no local apropriado. Essas funções reutilizáveis são salvas no formato de bibliotecas de clientes e ajudam a manter a funcionalidade existente intacta. A ferramenta aplica automaticamente as funções reutilizáveis geradas ao Adaptive Forms correspondente.

   Use o [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) para exportar as funções reutilizáveis (bibliotecas de clientes) para um pacote.

1. [Implantar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) o pacote de funções reutilizáveis (bibliotecas de clientes), [código personalizado, componentes, configurações](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager), bibliotecas específicas do local personalizadas para o [!DNL AEM] Ambiente as a Cloud Service.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Execute o [Ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). Ao especificar parâmetros na variável **[!UICONTROL Criar conjunto de migração]** , especifique o caminho da Adaptive Forms, temas, modelos, Modelos de dados de formulário, Cloud Services, Componentes personalizados e outros ativos específicos da AEM Forms para a **[!UICONTROL Caminhos a incluir]** opção. Ele adiciona especificado [!DNL AEM Forms] ativos para o conjunto de migração.

## Caminhos de vários ativos específicos do AEM Forms

* **Forms adaptável**: Você pode encontrar formulários adaptáveis em `/content/dam/formsanddocuments/`e /content/forms/af. Por exemplo, para um formulário adaptável chamado Registro de WKND, adicione caminhos `/content/dam/formsanddocuments/wknd-registration` e `/content/forms/af/wknd-registration`.
* **Modo de dados do formulário**: Você pode encontrar todos os Modelos de dados de formulário em `/content/dam/formsanddocuments-fdm`. Por exemplo, `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Bibliotecas do cliente**: O caminho padrão das bibliotecas do cliente é `/etc/clientlibs/fd/theme`.

* **Modelos de formulário adaptável**: O caminho padrão dos modelos é `/conf/<template folder>`. Por exemplo, para um modelo chamado caminho de adição básico `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Temas de formulário adaptável e bibliotecas de clientes**: O caminho padrão dos temas é ` /content/dam/formsanddocuments-themes/` e o caminho padrão das bibliotecas do cliente é `/etc/clientlibs/fd/theme`. Por exemplo, para um modelo chamado Tema WKND, adicione caminho ` /content/dam/formsanddocuments-themes/wkndtheme` e bibliotecas de clientes para o tema em `/etc/clientlibs/reference-themes/wkndtheme-3-0`. Também é possível ter temas e bibliotecas de clientes em outros caminhos personalizados.

* **Configurações da nuvem**: Você pode encontrar as configurações da nuvem em `/conf/`. Por exemplo, a configuração de nuvem do Modelo de dados de formulário está em `/conf/global/settings/cloudconfigs/fdm`.

* **Modelo de fluxo de trabalho**: Você pode encontrar AEM modelos de fluxo de trabalho em `/conf/global/settings/workflow/models/`. Por exemplo, para um modelo de fluxo de trabalho denominado Caminho de adição do Registro WKND `/conf/global/settings/workflow/models/wknd-registration`

Você pode adicionar caminhos de pastas de nível superior listados abaixo ou caminhos de pastas específicos, conforme descrito abaixo. Ela permite migrar determinados ativos e todos os ativos e formulários de uma só vez.

* /content/dam/formsanddocuments-fdm
* /content/dam/formsanddocuments/themes
* /content/forms/af
* /etc/clientlibs/fd/theme

Para migrar AEM modelos de Fluxo de trabalho, especifique os seguintes caminhos:

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/models
