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

1. Selecione um conjunto de migração na lista **Transferência de conteúdo** e clique em **Extract** para iniciar a extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!TIP]
   >Uma assimilação agora pode ser agendada para iniciar automaticamente imediatamente após uma extração ser bem-sucedida. Consulte [Assimilar conteúdo no Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para obter mais informações.

   >[!IMPORTANT]
   >
   >Verifique se a chave de extração é válida e se não está próxima de expirar. Se estiver próximo da data de expiração, você poderá renovar a chave de Extração selecionando o conjunto de migração e clicando em Propriedades. Clique em **Renovar**. Isso leva você ao Cloud Acceleration Manager, onde é possível clicar em **Copiar chave de extração**. Sempre que você clicar em **Copiar chave de extração**, uma nova chave de Extração é gerada e é válida por 14 dias a partir do momento da criação.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. Isso exibe a caixa de diálogo Extração. Clique em **Extract** para iniciar a fase de extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14b.png)

   >[!NOTE]
   >Opcionalmente, é possível substituir o container de preparo durante a fase de extração. Se **Substituir container de preparo** estiver desativado, poderá acelerar as extrações para migrações subsequentes em que os caminhos de conteúdo ou as configurações de inclusão de versões não tenham sido alterados. No entanto, se os caminhos de conteúdo ou as configurações de inclusão de versões tiverem sido alterados, **Substituir container de preparo** deve ser ativado.

1. A variável **Extração** O campo agora exibe a variável **EM EXECUÇÃO** status para indicar que a extração está em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Você pode clicar em **Visualizar progresso** para obter uma visualização granular da extração em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   Você também pode monitorar o progresso da fase de Extração no Cloud Acceleration Manager visitando a página Transferência de conteúdo e vê-lo com mais detalhes clicando em **..** > **Exibir detalhes**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. Quando a extração for concluída, analise as outras colunas como **Origem** e **Caminhos** para obter detalhes sobre o conjunto de migração preenchido. Clicando **..** > **Exibir detalhes** para ver detalhes, incluindo a duração de cada etapa da extração. Visualize essa caixa de diálogo durante a extração para que você possa ver o andamento das etapas.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service. Se você tiver usado a etapa de pré-cópia para a primeira extração completa, poderá ignorar a pré-cópia para as extrações complementares subsequentes (se o tamanho do conjunto de migração complementar for menor que 200 GB). O motivo é que isso pode adicionar tempo a todo o processo.
>Além disso, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada desde o momento em que a extração inicial é realizada até o momento em que a extração complementar é executada. Os complementos não podem ser executados em um conteúdo cuja estrutura foi alterada desde a extração inicial. Restrinja isso durante o processo de migração.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração complementar.

Siga as etapas abaixo:

1. Navegue até a **Transferência de conteúdo** e selecione o conjunto de migração para o qual você deseja executar a extração complementar. Clique em **Extrair** para iniciar a extração complementar.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. A variável **Extração do conjunto de migrações** é exibida. Clique em **Extract**.

   >[!IMPORTANT]
   >Você deve desativar a opção **Substituir containercontêiner de preparação durante a extração**.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## O que vem a seguir {#whats-next}

Depois de aprender a Extrair conteúdo da origem na ferramenta Transferência de conteúdo, agora você está pronto para aprender o Processo de assimilação na ferramenta Transferência de conteúdo. Consulte [Assimilar conteúdo no Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) onde você pode aprender a assimilar seu conjunto de migração da ferramenta Transferência de conteúdo.
