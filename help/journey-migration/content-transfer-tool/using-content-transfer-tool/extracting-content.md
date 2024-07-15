---
title: Extrair conteúdo da origem
description: Saiba como extrair conteúdo de uma instância do Adobe Experience Manager (AEM) de origem para transferi-lo posteriormente para uma instância do Cloud Service AEM.
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 19%

---

# Extrair conteúdo da origem {#extracting-content}

## Processo de extração da ferramenta de transferência de conteúdo {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extração de conteúdo"
>abstract="Extração refere-se ao processo de extrair conteúdo da instância do Adobe Experience Manager (AEM) de origem para uma área temporária chamada de “conjunto de migração”. Um conjunto de migração é uma área de armazenamento na nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância do AEM de origem e a instância do AEM Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=pt-BR#top-up-extraction-process" text="Extração complementar"


Siga as etapas abaixo para extrair seu conjunto de migração da ferramenta Transferência de conteúdo:

>[!NOTE]
>Se o Amazon S3, o Azure Data Store ou o File Data Store for usado como o tipo de armazenamento de dados, você poderá executar a etapa opcional de pré-cópia para aumentar a velocidade da fase de extração. A etapa de pré-cópia é mais eficaz para a primeira extração e assimilação completas. Consulte [Lidar com grandes repositórios de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para obter mais detalhes.

1. Selecione um conjunto de migração no assistente de **Transferência de conteúdo** e clique em **Extrair** para iniciar a extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!TIP]
   >Uma assimilação agora pode ser agendada para iniciar automaticamente imediatamente após uma extração ser bem-sucedida. Consulte [Assimilar conteúdo no Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para obter mais informações.

   >[!IMPORTANT]
   >
   >Verifique se a chave de extração é válida e se não está próxima de expirar. Se estiver próximo da data de expiração, você poderá renovar a chave de Extração selecionando o conjunto de migração e clicando em Propriedades. Clique em **Renovar**. Você será direcionado para a Cloud Acceleration Manager onde pode clicar em **Copiar Chave de Extração**. Toda vez que você clica em **Copiar chave de extração**, é gerada uma nova chave de extração que é válida por 14 dias a partir da data de criação.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. Isso exibe a caixa de diálogo Extração. Clique em **Extrair** para iniciar a fase de extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14b.png)

   >[!NOTE]
   >Opcionalmente, é possível substituir o container de preparo durante a fase de extração. Se o **contêiner de preparação de substituição** estiver desabilitado, ele poderá acelerar as extrações para migrações subsequentes em que os caminhos de conteúdo ou as configurações de inclusão de versões não tenham sido alterados. No entanto, se os caminhos de conteúdo ou as configurações de inclusão de versões tiverem sido alterados, o **contêiner de preparação de substituição** deverá ser habilitado.

1. O campo **Extração** agora exibe o status **RUNNING** para indicar que a extração está em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Você pode clicar em **Exibir andamento** para obter uma exibição granular da extração em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   Você também pode monitorar o progresso da fase de Extração no Cloud Acceleration Manager visitando a página Transferência de Conteúdo e vê-lo com mais detalhes clicando em **...** > **Exibir detalhes**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. Quando a extração for concluída, revise as outras colunas como **Source** e **Caminhos** para obter detalhes do conjunto de migração preenchido. Clique em **...** > **Exibir detalhes** para ver os detalhes, incluindo a duração de cada etapa da extração. Visualize essa caixa de diálogo durante a extração para que você possa ver o andamento das etapas.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service. Se você tiver usado a etapa de pré-cópia para a primeira extração completa, poderá ignorar a pré-cópia para as extrações complementares subsequentes (se o tamanho do conjunto de migração complementar for menor que 200 GB). O motivo é que isso pode adicionar tempo a todo o processo.
>Além disso, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada desde o momento em que a extração inicial é realizada até o momento em que a extração complementar é executada. Os complementos não podem ser executados em um conteúdo cuja estrutura foi alterada desde a extração inicial. Restrinja isso durante o processo de migração.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração complementar.

Siga as etapas abaixo:

1. Navegue até o assistente de **Transferência de conteúdo** e selecione o conjunto de migração para o qual você deseja realizar a extração complementar. Clique em **Extrair** para iniciar a extração complementar.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. A caixa de diálogo **Extração do conjunto de migração** é exibida. Clique em **Extrair**.

   >[!IMPORTANT]
   >Você deve desativar a opção **Substituir containercontêiner de preparação durante a extração**.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## O que vem a seguir {#whats-next}

Depois de aprender a Extrair conteúdo do Source na ferramenta Transferência de conteúdo, agora você está pronto para aprender o Processo de assimilação na ferramenta Transferência de conteúdo. Consulte [Assimilar conteúdo no Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md), onde você pode aprender a assimilar seu conjunto de migração na Ferramenta de transferência de conteúdo.
