---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 8ca25f86a8d0d61b40deaff0af85e56e438efbdc
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

Um usuário com acesso de administrador em [!DNL Adobe Experience Manager] como [!DNL Cloud Service] instala o conector aprimorado. Antes de instalar, revise o suporte à plataforma e outros [pré-requisitos para o conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>O Adobe requer implantação e configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], ele não é compatível com o Adobe.
>
>O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam redundante este conector; se isso ocorrer, os clientes podem ser solicitados a fazer a transição do uso desse conector.

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
   * [Implantar com [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

Para instalar o complemento em [!DNL Experience Manager] como [!DNL Cloud Service]siga estas etapas:

1. Adicionar `pom.xml` dependências:

   1. Adicionar uma dependência no principal `pom.xml`.

      ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version>1.7.4</version>
      </dependency>
      ```

   1. Adicionar uma dependência em todos os módulos [!DNL pom.xml].

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
         </dependency>
      ```

1. Adicionar `pom.xml` autenticação.

   1. Inclua a configuração de repositório abaixo no pom.xml no perfil adobe-public, para que as dependências do conector (acima) possam ser resolvidas no momento da criação (localmente e pelo Cloud Manager). As credenciais para acesso ao repositório serão fornecidas após a compra de uma licença. As credenciais precisarão ser adicionadas ao arquivo settings.xml na seção servidores.

      ```XML
      <repository>
         <id>hoodoo-maven</id>
         <name>Hoodoo Repository</name>
         <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
      </repository>
      ```

   1. Crie um arquivo com o nome `./cloudmanager/maven/settings.xml` na raiz do projeto. Para oferecer suporte a um repositório Maven protegido por senha, consulte [como configurar seu projeto](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md). Além disso, um exemplo `settings.xml` para referência. Por fim, atualize seu local `settings.xml` para compilar localmente.

      ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
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

1. Para criar uma configuração de usuário do sistema, crie `wf-workfront-users` em [!DNL Experience Manager] Grupo de usuários e atribua a permissão `jcr:all` para `/content/dam`. Um usuário do sistema `workfront-tools` O é criado automaticamente e as permissões necessárias são gerenciadas automaticamente. Todos os usuários de [!DNL Workfront] os usuários do conector aprimorado são adicionados automaticamente como parte desse grupo.

## Configure a conexão entre [!DNL Experience Manager] como [!DNL Cloud Service] e [!DNL Workfront] {#configure-connection}

Para criar uma conexão com o [!DNL Workfront]siga estas etapas:

1. Em [!DNL Experience Manager], selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração das ferramentas do Workfront]**.

1. Selecionar `workfront-tools` no painel esquerdo e selecione **[!UICONTROL Criar]** na área superior direita da página.

1. No **[!UICONTROL Conexão Workfront]** , forneça os detalhes necessários de sua [!DNL Workfront] e selecione **[!UICONTROL Conectar-se ao Workfront]** opção. Depois de conectado com êxito, a variável [!DNL Workfront] a integração personalizada do documento é criada automaticamente no [!DNL Workfront] ambiente.

   ![Connect [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Navegue até o **[!UICONTROL Avançado]** e selecione a opção **[!UICONTROL O servidor AEM as a Cloud Service]**.
