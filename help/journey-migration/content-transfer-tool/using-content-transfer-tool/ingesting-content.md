---
title: Assimilar conteúdo no Target
description: Assimilar conteúdo no Target
source-git-commit: 80e148aa5533963bcd6354e2117a4619bcf5b27f
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 31%

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
>Você pode executar a etapa opcional de pré-cópia para acelerar significativamente a fase de assimilação. Consulte [Integração com o AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) para obter mais detalhes.

1. Selecione um conjunto de migração de **Transferência de conteúdo** e clique em **Assimilar** para iniciar a ingestão.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. A caixa de diálogo **Assimilação do conjunto de migração** é exibida. O conteúdo pode ser assimilado na instância do autor ou na instância de publicação de cada vez. Selecione a instância para a qual assimilar conteúdo. Clique em **Assimilar** para iniciar a fase de ingestão.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >Se a assimilação com pré-cópia for usada (para S3 ou Azure Data Store), é recomendável executar a assimilação do autor primeiro sozinho. Isso irá acelerar a assimilação de Publicação quando for executada mais tarde.

   >[!IMPORTANT]
   >Quando a variável **Limpar o conteúdo existente na instância do Cloud antes da assimilação** estiver ativada, ela excluirá todo o repositório existente e criará um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Isso também é verdadeiro para um usuário administrador adicionado ao **administradores** grupo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Além disso, clique em **Atendimento ao cliente** para registrar um tíquete, como mostrado na figura abaixo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   Além disso, consulte [Considerações importantes sobre o uso da ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) para saber mais.

1. Uma vez concluída a assimilação, o status em **Ingestão de autor** atualizações a **CONCLUÍDO**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## Ingestão complementar {#top-up-ingestion-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a *atualizações complementares* de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Quando o processo de assimilação estiver concluído, você poderá usar o conteúdo delta por meio do método de ingestão complementar. Siga as etapas abaixo:

1. Navegue até o **Transferência de conteúdo** e selecione o conjunto de migração para o qual deseja executar a assimilação complementar. Clique em **Assimilar** para iniciar a extração complementar.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. A caixa de diálogo **Assimilação do conjunto de migração** é exibida.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >Você deve desativar o **Limpar o conteúdo existente na instância do Cloud antes da assimilação** , para evitar que o conteúdo existente seja excluído da atividade de assimilação anterior. Além disso, clique em **Atendimento ao cliente** para registrar um tíquete, conforme mostrado na figura anterior.

## O que vem a seguir {#whats-next}

Depois de aprender a Inserir conteúdo no Target na ferramenta Transferência de conteúdo, você pode visualizar logs ao concluir cada etapa (extração e assimilação) e procurar erros. Consulte [Visualização de logs para um conjunto de migração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) para saber mais.
