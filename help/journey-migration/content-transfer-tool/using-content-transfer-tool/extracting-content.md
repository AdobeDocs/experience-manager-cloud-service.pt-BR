---
title: Extrair conteúdo da origem
description: Extrair conteúdo da origem
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: b31fe77cd43362b6ad768e8a2b258c23ae84466c
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 27%

---

# Extrair conteúdo da origem {#extracting-content}

## Processo de extração na ferramenta Transferência de conteúdo {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extração de conteúdo"
>abstract="Extração refere-se à extração de conteúdo da instância do AEM de origem em uma área temporária chamada de conjunto de migração. Um conjunto de migração é uma área de armazenamento em nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância do AEM de origem e a instância do AEM Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-extraction-process" text="Extração complementar"


Siga as etapas abaixo para extrair seu conjunto de migração da ferramenta Transferência de conteúdo:

>[!NOTE]
>Se o Amazon S3, o Azure Data Store ou o File Data Store for usado como o tipo de armazenamento de dados, você poderá executar a etapa opcional de pré-cópia para acelerar significativamente a fase de extração. A etapa de pré-cópia é mais eficaz para a primeira extração e ingestão completas. Consulte [Lidar com grandes repositórios de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para obter mais detalhes.

1. Selecione um conjunto de migração de **Transferência de conteúdo** e clique em **Extract** para iniciar a extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >Certifique-se de que a chave de Extração seja válida e não esteja próxima da expiração. Se estiver próximo da data de expiração, é possível renovar a chave de Extração selecionando o conjunto de migração e clicando em Propriedades. Clique em **Renovar**. Isso o levará ao Cloud Acceleration Manager, onde você pode clicar em **Copiar chave de extração**. Toda vez que você clicar em **Copiar chave de extração**, uma nova chave de Extração é gerada e é válida por 14 dias a partir do momento da criação.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. Isso exibirá a caixa de diálogo Extração. Clique em **Extract** para iniciar a fase de extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
   >Você tem a opção de substituir o contêiner de preparação durante a fase de extração. If **Substituir contêiner de preparação** estiver desativado, pode acelerar as extrações para migrações subsequentes, onde os caminhos de conteúdo ou as configurações de incluir versões não foram alteradas. No entanto, se os caminhos de conteúdo ou as configurações de versões de inclusão tiverem sido alterados, então **Substituir contêiner de preparação** deve estar ativada.

1. O **Extração** agora exibe a variável **EM EXECUÇÃO** status para indicar que a extração está em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Você pode clicar em **Visualizar progresso** para obter uma visualização granular da extração em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   Você também pode monitorar o progresso da fase de extração no Cloud Acceleration Manager acessando a página Transferência de conteúdo e visualizá-la com mais detalhes clicando em **...** e depois **Exibir detalhes**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. Quando a Extração estiver concluída, analise as outras colunas como **Origem** e **Caminhos** para obter detalhes sobre o conjunto de migração que você preencheu, clicando em **...** e depois **Exibir detalhes** para ver detalhes, incluindo a duração de cada etapa da extração. Visualize essa caixa de diálogo durante a extração para ver como as etapas estão progredindo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service. Se você tiver usado a etapa de pré-cópia para a primeira extração completa, poderá ignorar a pré-cópia para as extrações adicionais subsequentes (se o tamanho do conjunto de migração complementar for menor que 200 GB), pois isso poderá adicionar tempo ao processo inteiro.
>Além disso, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada do momento em que a extração inicial é levada ao momento em que a extração complementar é executada. Os complementos não podem ser executados em conteúdo cuja estrutura foi alterada desde a extração inicial. Certifique-se de restringir isso durante o processo de migração.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração complementar.

Siga as etapas abaixo:

1. Navegue até o **Transferência de conteúdo** e selecione o conjunto de migração para o qual deseja executar a extração complementar. Clique em **Extrair** para iniciar a extração complementar.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. O **Extração do conjunto de migração** será exibida. Clique em **Extract**.

   >[!IMPORTANT]
   >Você deve desativar a opção **Substituir containercontêiner de preparação durante a extração**.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## O que vem a seguir {#whats-next}

Depois de aprender a extrair conteúdo da origem na ferramenta Transferência de conteúdo, você estará pronto para aprender o Processo de assimilação na ferramenta Transferência de conteúdo. Consulte [Inserção de conteúdo ao Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para saber como assimilar seu conjunto de migração na ferramenta Transferência de conteúdo.
