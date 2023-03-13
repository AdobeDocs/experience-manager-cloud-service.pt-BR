---
title: Assimilar conteúdo no Target (herdado)
description: Assimilar conteúdo no Target
hide: true
hidefromtoc: true
exl-id: 326b3e98-5055-49b5-a005-63fd3ca35202
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 27%

---

# Assimilar conteúdo no Target (herdado) {#ingesting-content}

## Processo de assimilação na ferramenta Transferência de conteúdo {#ingestion-process}

Siga as etapas abaixo para assimilar seu conjunto de migração da ferramenta Transferência de conteúdo:
>[!NOTE]
>Você pode executar a etapa opcional de pré-cópia para acelerar significativamente a fase de assimilação. Consulte [Assimilar com AzCopy](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) para obter mais detalhes.

1. Selecione um conjunto de migração em **Transferência de conteúdo** e clique em **Assimilar** para iniciar a assimilação.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. A caixa de diálogo **Assimilação do conjunto de migração** é exibida. O conteúdo pode ser assimilado na instância do Autor ou na instância de Publicação de cada vez. Selecione a instância na qual assimilar conteúdo. Clique em **Assimilar** para iniciar a fase de assimilação.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >Se a assimilação com pré-cópia for usada (para S3 ou Azure Data Store), é recomendável executar a assimilação do autor primeiro sozinha. Isso irá acelerar a Assimilação de publicação quando for executado posteriormente.

   >[!IMPORTANT]
   >Quando a variável **Apagar conteúdo existente na instância da nuvem antes da assimilação** estiver ativada, excluirá todo o repositório existente e criará um novo repositório para assimilar conteúdo. Isso significa que ele redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino. Isso também ocorre para um usuário administrador adicionado à variável **administradores** grupo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Clique em **Atendimento ao cliente** para registrar um tíquete, conforme mostrado na figura abaixo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   Consulte também [Considerações importantes sobre o uso da ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) para saber mais.

1. Quando a assimilação estiver concluída, o status em **Assimilação do autor** atualizações para **CONCLUÍDO**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## Ingestão complementar {#top-up-ingestion-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a *atualizações complementares* de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Quando o processo de assimilação estiver concluído, você poderá usar o conteúdo delta por meio do método de ingestão complementar. Siga as etapas abaixo:

1. Navegue até a **Transferência de conteúdo** e selecione o conjunto de migração para o qual você deseja realizar a assimilação complementar. Clique em **Assimilar** para iniciar a extração complementar.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. A caixa de diálogo **Assimilação do conjunto de migração** é exibida.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >Você deve desativar o **Apagar conteúdo existente na instância da nuvem antes da assimilação** para impedir a exclusão do conteúdo existente da atividade de assimilação anterior. Clique em **Atendimento ao cliente** para registrar um ticket, conforme mostrado na figura anterior.

## O que vem a seguir {#whats-next}

Depois de aprender a Assimilar conteúdo no Target na ferramenta Transferência de conteúdo, você poderá visualizar os logs ao concluir cada etapa (extração e assimilação) e procurar erros. Consulte [Visualização de logs para um conjunto de migração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) para saber mais.
