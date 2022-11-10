---
title: Assimilar conteúdo no Target
description: Assimilar conteúdo no Target
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: e8b4fe047c9656aa592fc851279dc6a189144023
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 13%

---

# Assimilar conteúdo no Target {#ingesting-content}

## Processo de assimilação na ferramenta Transferência de conteúdo {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="Assimilação de conteúdo"
>abstract="Assimilação refere-se à assimilação de conteúdo do conjunto de migração na instância do Cloud Service de destino. A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="Ingestão complementar"

Siga as etapas abaixo para assimilar seu conjunto de migração da ferramenta Transferência de conteúdo:
>[!NOTE]
>Você pode executar a etapa opcional de pré-cópia para acelerar significativamente a fase de assimilação. A etapa de pré-cópia é mais eficaz para a primeira extração e ingestão completas. Consulte [Integração com o AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obter mais detalhes.

1. Vá para Cloud Acceleration Manager. Clique no cartão do projeto e clique no cartão Transferência de conteúdo . Navegar para **Trabalhos de assimilação** e clique em **Nova Assimilação**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. Forneça as informações necessárias para criar uma nova assimilação.

   * Selecione o conjunto de migração que você acabou de extrair como a Fonte
   * Selecione o ambiente de destino. É aqui que o conteúdo do conjunto de migração será assimilado. Selecione a camada. (Autor/Publicação).

   >[!NOTE]
   >
   >Se a origem foi Autor, é recomendável assimilá-la no nível Autor no destino. Da mesma forma, se a origem foi Publicar, o destino também deve ser Publicar.

   >[!NOTE]
   >
   >Você pode executar a etapa opcional de pré-cópia para acelerar significativamente a fase de assimilação. Consulte [Integração com o AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) para obter mais detalhes.
   > 
   >Se a assimilação com pré-cópia for usada (para S3 ou Azure Data Store), é recomendável executar a assimilação do autor primeiro sozinho. Isso irá acelerar a assimilação de Publicação quando for executada mais tarde.

   >[!IMPORTANT]
   >
   >Você poderá iniciar uma assimilação no ambiente de destino somente se pertencer ao local **Administradores de AEM** no serviço de criação do Cloud Service de destino. Se não conseguir iniciar uma assimilação, consulte [Não é possível iniciar a assimilação](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) para obter mais detalhes.

   >[!IMPORTANT]
   >
   >Se a configuração **Varrer** estiver habilitado antes da assimilação, ele excluirá todo o repositório existente e criará um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Isso também é verdadeiro para um usuário administrador adicionado ao **administradores** grupo. Você precisará ser adicionado novamente ao grupo de administradores para iniciar uma assimilação.

1. Clique em **Assimilar**

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. Em seguida, você pode monitorar a fase de assimilação na exibição da lista Trabalhos de assimilação e usar o menu de ação da assimilação para exibir o log conforme a assimilação avança.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. Quando a assimilação estiver concluída, clique no botão (i) no canto superior direito da tela para obter mais informações sobre o trabalho de assimilação.

<!-- Alexandru: hiding temporarily, until it's reviewed 

1. The **Migration Set ingestion** dialog box displays. Content can be ingested to either Author instance or Publish instance at a time. Select the instance to ingest content to. Click on **Ingest** to start the ingestion phase. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >If ingesting with pre-copy is used (for S3 or Azure Data Store), it is recommended to run Author ingestion first alone. This will speed up the Publish ingestion when it is run later. 

   >[!IMPORTANT]
   >When the **Wipe existing content on Cloud instance before ingestion** option is enabled, it deletes the entire existing repository and creates a new repository to ingest content into. This means that it resets all settings including permissions on the target Cloud Service instance. This is also true for an admin user added to the **administrators** group.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Additionally, click on **Customer Care** to log a ticket, as shown in the figure below. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## Ingestão complementar {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup" title="Top Up Ingestion"
>abstract="Use o recurso de cima para mover o conteúdo modificado desde a atividade de transferência de conteúdo anterior. Após a conclusão da assimilação, verifique os logs em busca de erros/avisos. Todos os erros devem ser resolvidos imediatamente, lidando com os problemas relatados ou entrando em contato com o Atendimento ao Cliente do Adobe."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="Visualização de logs"

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a *atualizações complementares* de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service. Se tiver usado a etapa de pré-cópia para a primeira assimilação completa, você pode ignorar a pré-cópia para as assimilações adicionais subsequentes (se o tamanho do conjunto de migração complementar for menor que 200 GB), pois isso pode adicionar tempo ao processo inteiro.

Quando o processo de ingestão estiver concluído, para assimilar o conteúdo delta, será necessário executar uma [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) e, em seguida, use o método de ingestão complementar.

Você pode fazer isso criando um novo trabalho de assimilação e garantir que **Varrer** estiver desativado durante a fase de assimilação, conforme mostrado abaixo:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## Resolução de problemas {#troubleshooting}

### O CAM não pode recuperar o token de migração {#cam-unable-to-retrieve-the-migration-token}

A recuperação automática do token de migração pode falhar por motivos diferentes, incluindo você [configuração de uma lista de permissões IP via Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) no ambiente Cloud Service do target.  Nesses cenários, você verá a seguinte caixa de diálogo ao tentar iniciar uma assimilação:

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

Você precisará recuperar o token de migração manualmente clicando no link &quot;Obter token&quot; na caixa de diálogo. Isso abrirá outra guia que exibe o token. Em seguida, você pode copiar o token e colá-lo no **Entrada do token de migração** campo. Agora, você deve ser capaz de iniciar a ingestão.

>[!NOTE]
>
>O token estará disponível para usuários que pertencem ao local **Administradores de AEM** no serviço de criação do Cloud Service de destino.

### Não é possível iniciar a assimilação {#unable-to-start-ingestion}

Você poderá iniciar uma assimilação no ambiente de destino somente se pertencer ao local **Administradores de AEM** no serviço de criação do Cloud Service de destino. Se você não pertencer ao grupo de administradores AEM, verá um erro como mostrado abaixo ao tentar iniciar uma assimilação. Você pode solicitar que o administrador o adicione ao local **Administradores de AEM** ou peça o token em si, que pode ser colado no **Entrada do token de migração** campo.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

## O que vem a seguir {#whats-next}

Depois de concluir a Inserção de conteúdo no Target, você pode visualizar os logs de cada etapa (extração e assimilação) e procurar erros. Consulte [Visualização de logs para um conjunto de migração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) para saber mais.
