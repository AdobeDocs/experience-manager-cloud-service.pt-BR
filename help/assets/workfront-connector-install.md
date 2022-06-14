---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 109f07c7273cc9a4890e41bf29a1509f738d130b
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

Um usuário com acesso de administrador em [!DNL Adobe Experience Manager] como [!DNL Cloud Service] instala o conector aprimorado. Antes de instalar, revise o suporte à plataforma e outros [pré-requisitos para o conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* O Adobe requer implantação e configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], ele não é compatível com o Adobe.
>
>* O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam redundante este conector; se isso ocorrer, os clientes podem ser solicitados a fazer a transição do uso desse conector.
>
>* O Adobe oferece suporte ao conector avançado versões 1.7.4 e superior. Não há suporte para pré-lançamento e versões personalizadas anteriores. Para verificar a versão do conector aprimorado, consulte a etapa 5(a) de [instruções de instalação do conector avançado](workfront-connector-install.md).
>
>* Consulte [Exame de certificação de parceiro para Workfront para conector aprimorado Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte [Guia de exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


Antes de instalar o conector, siga estas etapas de pré-instalação:

1. [Configurar o firewall](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html). Para conhecer o cluster IP em [!DNL Workfront], navegue até [!UICONTROL Configuração] > [!UICONTROL Sistema] > [!UICONTROL Informações do cliente].

1. No dispatcher, permita cabeçalhos HTTP nomeados `authorization`, `username`e `apikey`. Permitir `GET`, `POST`e `PUT` solicitações para `/bin/workfront-tools`.

1. Verifique se os seguintes caminhos não existem em [!DNL Experience Manager] repositório:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Esta instalação requer conhecimento para definir um projeto Maven em [!DNL Experience Manager] como [!DNL Cloud Service]. Use os seguintes recursos para entender como incluir um pacote de terceiros em seu projeto Maven:

   * [Incluir pacote de terceiros em seu projeto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Implantar com [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=pt-BR).

Para instalar o complemento em [!DNL Experience Manager] como [!DNL Cloud Service]siga estas etapas:

1. Baixe o conector aprimorado de [Distribuição de software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [Acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) e clonar seu repositório as a Cloud Service AEM do Cloud Manager.

1. Abra o repositório clonado AEM as a Cloud Service usando um IDE de sua escolha.

1. Coloque o arquivo zip do conector aprimorado baixado na Etapa 1 no seguinte caminho:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se a variável `resources` não existe, crie a pasta.


1. Adicionar `pom.xml` dependências:

   1. Adicionar uma dependência no principal `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
      ```

      >[!NOTE]
      >
      >Certifique-se de atualizar o número de versão do conector aprimorado antes de copiar a dependência para o pai `pom.xml`.

   1. Adicionar uma dependência em `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. Adicionar `pom.xml` incorporados. Adicione o [!DNL Workfront for Experience Manager enhanced connector] pacotes para `embeddeds` da seção `pom.xml` de todo o seu subprojeto. Precisa de incorporado no módulo all `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   O target da seção incorporada é definido como `/apps/<path-to-project-install-folder>/install`. Este caminho JCR `/apps/<path-to-project-install-folder>` deve ser incluído nas regras de filtro no `all/src/main/content/META-INF/vault/filter.xml` arquivo. As regras de filtro do repositório geralmente são derivadas do nome do programa. Use o nome da pasta como destino nas regras existentes.

1. Encaminhe as alterações para o repositório.

1. Execute o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. Para criar uma configuração de usuário do sistema, crie `wf-workfront-users` em [!DNL Experience Manager] Grupo de usuários e atribua a permissão `jcr:all` para `/content/dam`. Um usuário do sistema `workfront-tools` O é criado automaticamente e as permissões necessárias são gerenciadas automaticamente. Todos os usuários de [!DNL Workfront] os usuários do conector aprimorado são adicionados automaticamente como parte desse grupo.

Para obter informações sobre como atualizar o [!DNL Workfront for Experience Manager enhanced connector] de uma versão anterior para a versão mais recente, clique em [here](update-workfront-enhanced-connector.md).

## Configure a conexão entre [!DNL Experience Manager] como [!DNL Cloud Service] e [!DNL Workfront] {#configure-connection}

Para criar uma conexão com o [!DNL Workfront]siga estas etapas:

1. Em [!DNL Experience Manager], selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração das ferramentas do Workfront]**.

1. Selecionar `workfront-tools` no painel esquerdo e selecione **[!UICONTROL Criar]** na área superior direita da página.

1. No **[!UICONTROL Conexão Workfront]** , forneça os detalhes necessários de sua [!DNL Workfront] e selecione **[!UICONTROL Conectar-se ao Workfront]** opção. Depois de conectado com êxito, a variável [!DNL Workfront] a integração personalizada do documento é criada automaticamente no [!DNL Workfront] ambiente.

   ![Connect [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Navegue até o **[!UICONTROL Avançado]** e selecione a opção **[!UICONTROL O servidor AEM as a Cloud Service]**.
