---
title: Como migrar de um Forms AEM 6.5 e Forms AEM 6.4 para [!DNL AEM Forms] Ambiente as a Cloud Service?
description: Migrar de um [!DNL AEM Forms] On-Premise environment to [!DNL AEM Forms] Ambiente as a Cloud Service
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 2%

---

# Migrar para [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

Você pode migrar sua Forms adaptativa, temas, modelos e configurações de nuvem do <!-- AEM 6.3 Forms--> AEM 6.4 Forms em OSGi e AEM 6.5 Forms em OSGi para [!DNL AEM] as a Cloud Service. Antes de migrar esses ativos, use o Utilitário de migração para converter o formato usado nas versões anteriores para o formato usado em [!DNL AEM] as a Cloud Service. Ao executar o Utilitário de migração, os seguintes ativos são atualizados:

* Componentes personalizados para o Adaptive Forms
* Modelos e temas adaptáveis do Forms
* Configurações da nuvem
* Os scripts do editor de código são convertidos em funções reutilizáveis e aplicados a regras visuais.

## Considerações {#consideration}

* O serviço ajuda a migrar o conteúdo somente do [!DNL AEM Forms] em ambientes OSGi. Migrar conteúdo de [!DNL AEM Forms] no JEE para um ambiente Cloud Service não é suportado.

* (Somente para AEM 6.3 Forms ou um ambiente de versão anterior atualizado para AEM 6.4 Forms ou AEM 6.5 Forms) A Forms adaptável com base em modelos e temas prontos para uso no AEM 6.3 Forms ou versão anterior não são compatíveis com o [!DNL [!DNL AEM Forms]] as a Cloud Service.

## Pré-requisitos {#prerequisites}

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
