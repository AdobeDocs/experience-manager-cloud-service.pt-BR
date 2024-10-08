---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2907a3b2-e28c-4194-afa8-47eadec6e39a
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html) |
| AEM as a Cloud Service | Este artigo |

Um usuário com acesso de administrador no [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] instala o conector aprimorado. Antes de instalar, verifique o suporte à plataforma e outros [pré-requisitos para o conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>A partir de junho de 2022, o Adobe lançou uma nova integração nativa para conectar o Workfront ao Adobe Experience Manager Assets as a Cloud Service. Essa integração se tornou o método necessário para conectar essas duas soluções. Qualquer nova implementação futura do conector aprimorado (1.9.8 e posterior) para conectar o Workfront com o AEM Assets as a Cloud Service está bloqueada. Para obter mais informações sobre como configurar essa integração, consulte [Configurar a integração as a Cloud Service do Experience Manager Assets](workfront-connector-configure.md).

>[!IMPORTANT]
>
>* O Adobe exige a implantação e a configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por meio de parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], não é suportado pelo Adobe.
>
>* O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam este conector redundante; se isso ocorrer, pode ser necessário que os clientes façam a transição do uso deste conector.
>
>* O Adobe suporta o conector aprimorado versões 1.7.4 e superiores. As versões anteriores de pré-lançamento e personalizadas não são compatíveis. Para verificar a versão aprimorada do conector, consulte a etapa 5(a) de [instruções de instalação do conector aprimorado](workfront-connector-install.md).
>
>* Consulte [Exame de certificação de parceiro para o conector aprimorado do Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte o [Guia do Exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Antes de instalar o conector, siga estas etapas de pré-instalação:

1. Se seu programa AEM as a Cloud Service tiver configurado a Rede avançada e ativado a lista de permissões de IP, será necessário adicionar os IPs da Workfront a essa lista de permissões para permitir Assinaturas de eventos e várias chamadas de API para passar para o AEM.

   * [IPs de Cluster do Workfront](https://experienceleague.adobe.com/docs/workfront/using/administration-and-setup/get-started-administration/configure-your-firewall.html?lang=en#ip-addresses-to-allow-for-clusters-1-2-3-5-7-8-and-9). Para conhecer o cluster IP em [!DNL Workfront], navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Sistema]** > **[!UICONTROL Informações do cliente]**.

   * [APIs de Assinatura de Eventos da Workfront](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-api/event-subscriptions/event-subs-api.html)

   >[!IMPORTANT]
   >
   >* Se você tiver a rede avançada configurada para seu programa e estiver usando a Lista de permissões de IP, devido a uma limitação com a arquitetura do Enhanced Workfront Connector, também será necessário adicionar o IP de saída do programa à lista de permissões no Cloud Manager.
   >
   >* p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >* Para encontrar o IP do seu programa, abra uma janela de terminal e execute um comando, como:
   >
   >    ```
   >    dscacheutil -q host -a name p{PROGRAM_ID}.external.adobeaemcloud.com
   >
   >    ```

1. Verifique se as sobreposições a seguir não existem no repositório [!DNL Experience Manager]. Se você tiver sobreposições pré-existentes nesses caminhos, será necessário remover as sobreposições ou mesclar o delta de alterações entre os dois:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`
   * `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

1. Esta instalação requer que o conhecimento defina um projeto Maven em [!DNL Experience Manager] como [!DNL Cloud Service]. Use os seguintes recursos para entender como incluir um pacote de terceiros em seu projeto Maven:

   * [Incluir pacote de terceiros em seu projeto Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#including-third-party).
   * [Implantar com [!DNL Cloud Manager]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html).

Para instalar o complemento no [!DNL Experience Manager] como [!DNL Cloud Service], siga estas etapas:

1. Baixe o conector aprimorado da [Distribuição de Software Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).

1. [Acesse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) e clone seu repositório do AEM as a Cloud Service da Cloud Manager.

1. Abra o repositório do AEM as a Cloud Service clonado usando um IDE de sua escolha.

1. Coloque o arquivo zip do conector aprimorado baixado na Etapa 1 no seguinte caminho:

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >Se a pasta `resources` não existir, crie a pasta.


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
      >Atualize o número de versão do conector aprimorado antes de copiar a dependência para o pai `pom.xml`.

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


1. Adicionar `pom.xml` incorporações. Adicione os pacotes [!DNL Workfront for Experience Manager enhanced connector] à seção `embeddeds` de `pom.xml` de todos os subprojetos. Precisa inserida no módulo `pom.xml` completo.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   O destino da seção incorporada está definido como `/apps/<path-to-project-install-folder>/install`. Este caminho JCR `/apps/<path-to-project-install-folder>` deve ser incluído nas regras de filtro no arquivo `all/src/main/content/META-INF/vault/filter.xml`. As regras de filtro do repositório geralmente são derivadas do nome do programa. Use o nome da pasta como destino nas regras existentes.

1. Enviar as alterações para o repositório.

1. Execute o pipeline para [implantar as alterações no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

1. Para criar uma configuração de usuário do sistema, crie `wf-workfront-users` no Grupo de Usuários [!DNL Experience Manager] e atribua a permissão `jcr:all` a `/content/dam`. Um usuário do sistema `workfront-tools` é criado automaticamente e as permissões necessárias são gerenciadas automaticamente. Todos os usuários de [!DNL Workfront] que usam o conector aprimorado são adicionados automaticamente como parte desse grupo.

Para obter informações sobre como atualizar o [!DNL Workfront for Experience Manager enhanced connector] de uma versão anterior para a versão mais recente, clique [aqui](update-workfront-enhanced-connector.md).

## Configurar a conexão entre [!DNL Experience Manager] como [!DNL Cloud Service] e [!DNL Workfront] {#configure-connection}

Para criar uma conexão com [!DNL Workfront], siga estas etapas:

1. Em [!DNL Experience Manager], selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuração de Ferramentas do Workfront]**.

1. Selecione `workfront-tools` no painel esquerdo e selecione a opção **[!UICONTROL Criar]** na área superior direita da página.

1. Na caixa de diálogo **[!UICONTROL Conexão Workfront]**, forneça os detalhes necessários da sua implantação do [!DNL Workfront] e selecione a opção **[!UICONTROL Conectar-se ao Workfront]**. Depois de conectada com êxito, a integração personalizada do documento [!DNL Workfront] é criada automaticamente no ambiente [!DNL Workfront].

   ![Conectar [!DNL Experience Manager] e [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Navegue até a guia **[!UICONTROL Avançado]** e selecione a opção **[!UICONTROL É o AEM as a Cloud Service do Servidor]**.
