---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: 393ec79e820632e879a377e697ecd09f4571c0b7
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 2%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html) |
| AEM as a Cloud Service | Este artigo |

Um usuário com acesso de administrador no [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] instala o conector aprimorado. Antes de instalar, consulte o suporte à plataforma e outros [pré-requisitos para o conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>A partir de junho de 2022, o Adobe lançou uma nova integração nativa para conectar o Workfront ao Adobe Experience Manager Assets as a Cloud Service. Essa integração se tornou o método necessário para conectar essas duas soluções. Qualquer nova implementação futura do conector aprimorado (1.9.8 e posterior) para conectar o Workfront com o AEM Assets as a Cloud Service será bloqueada. Para obter mais informações sobre como configurar essa integração, consulte [Configurar a integração as a Cloud Service do Experience Manager Assets](workfront-connector-configure.md).

>[!IMPORTANT]
>
>* O Adobe exige a implantação e a configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por meio de parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], não é compatível com o Adobe.
>
>* O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam esse conector redundante; se isso ocorrer, pode ser necessário que os clientes façam a transição do uso desse conector.
>
>* O Adobe suporta o conector aprimorado versões 1.7.4 e superiores. As versões anteriores de pré-lançamento e personalizadas não são compatíveis. Para verificar a versão aprimorada do conector, consulte a etapa 5(a) do [instruções de instalação do conector aprimorado](workfront-connector-install.md).
>
>* Consulte [Exame de certificação de parceiros para o conector aprimorado do Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte [Guia do exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Antes de instalar o conector, siga estas etapas de pré-instalação:

1. Se o seu programa AEM as a Cloud Service tiver configurado a Rede avançada e ativado a lista de permissões de IP, será necessário adicionar os IPs da Workfront AEM a essa lista de permissões para permitir Assinaturas de eventos e várias chamadas de API para passar para o.

   * [IPs de cluster do Workfront](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=en#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9). Para conhecer o cluster IP em [!DNL Workfront], navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Sistema]** > **[!UICONTROL Informações do cliente]**.

   * [IPs da API de assinatura de evento do Workfront](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html)

   >[!IMPORTANT]
   >
   >* Se você tiver a Rede avançada configurada para seu programa e estiver usando a Lista de permissões de IP, devido a uma limitação com a arquitetura do Conector aprimorado do Workfront, também será necessário adicionar o IP de saída do programa à lista de permissões no Cloud Manager.
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* Para encontrar o IP do seu programa, abra uma janela de terminal e execute um comando, como:
   >
   >    ```
   >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >    ```

1. Verifique se as seguintes sobreposições não existem no [!DNL Experience Manager] repositório. Se você tiver sobreposições pré-existentes nesses caminhos, será necessário remover as sobreposições ou mesclar o delta de alterações entre os dois:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. Esta instalação requer conhecimento para definir um projeto Maven em [!DNL Experience Manager] as a [!DNL Cloud Service]. Use os seguintes recursos para entender como incluir um pacote de terceiros em seu projeto Maven:

   * [Incluir pacote de terceiros em seu projeto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Implantar com [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=pt-BR).

Para instalar o complemento no [!DNL Experience Manager] as a [!DNL Cloud Service], siga estas etapas:

1. Baixe o conector aprimorado de [Distribuição de software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Access](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) e clonar seu repositório do AEM as a Cloud Service no Cloud Manager.

1. Abra o repositório as a Cloud Service AEM clonado usando um IDE de sua escolha.

1. Coloque o arquivo zip do conector aprimorado baixado na Etapa 1 no seguinte caminho:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se a variável `resources` pasta não existe, crie a pasta.


1. Adicionar `pom.xml` dependências:

   1. Adicionar uma dependência no pai `pom.xml`.

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

   1. Adicionar uma dependência no `all module pom.xml`.

      ```XML
         <dependency>
            <groupId>digital.hoodoo</groupId>
            <artifactId>workfront-tools.ui.apps</artifactId>
            <type>zip</type>
            <scope>system</scope>
            <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
         </dependency>
      ```


1. Adicionar `pom.xml` incorpora. Adicione o [!DNL Workfront for Experience Manager enhanced connector] pacotes para `embeddeds` seção do `pom.xml` de todo o subprojeto. Precisa ser incorporado no módulo all `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   O target da seção incorporada é definido como `/apps/<path-to-project-install-folder>/install`. Este caminho JCR `/apps/<path-to-project-install-folder>` deve ser incluído nas regras de filtro na `all/src/main/content/META-INF/vault/filter.xml` arquivo. As regras de filtro do repositório geralmente são derivadas do nome do programa. Use o nome da pasta como destino nas regras existentes.

1. Enviar as alterações para o repositório.

1. Executar o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. Para criar uma configuração de usuário do sistema, crie `wf-workfront-users` in [!DNL Experience Manager] Grupo de usuários e atribuir a permissão `jcr:all` para `/content/dam`. Um usuário do sistema `workfront-tools` O é criado automaticamente e as permissões necessárias são gerenciadas automaticamente. Todos os usuários de [!DNL Workfront] que usam o conector aprimorado são adicionados automaticamente como parte desse grupo.

Para obter informações sobre como atualizar o [!DNL Workfront for Experience Manager enhanced connector] de uma versão anterior para a versão mais recente, clique em [aqui](update-workfront-enhanced-connector.md).

## Configurar a conexão entre [!DNL Experience Manager] as a [!DNL Cloud Service] e [!DNL Workfront] {#configure-connection}

Para criar uma conexão com [!DNL Workfront], siga estas etapas:

1. Entrada [!DNL Experience Manager], selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração de ferramentas do Workfront]**.

1. Selecionar `workfront-tools` no painel esquerdo e selecione **[!UICONTROL Criar]** na área superior direita da página.

1. No **[!UICONTROL Conexão Workfront]** , forneça os detalhes necessários do seu [!DNL Workfront] e selecione **[!UICONTROL Conectar-se ao Workfront]** opção. Depois de conectado com êxito, o [!DNL Workfront] a integração personalizada de documentos é criada automaticamente na [!DNL Workfront] ambiente.

   ![Conectar [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Navegue até a **[!UICONTROL Avançado]** e selecione a opção **[!UICONTROL O servidor AEM está as a Cloud Service]**.
