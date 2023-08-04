---
title: Extrair conteúdo da origem
description: Saiba como extrair conteúdo de uma instância de AEM de origem para transferi-lo posteriormente para uma instância de Cloud Service AEM.
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 26%

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
>Se o Amazon S3, Azure Data Store ou File Data Store for usado como o tipo de armazenamento de dados, você poderá executar a etapa opcional de pré-cópia para acelerar significativamente a fase de extração. A etapa de pré-cópia é mais eficaz para a primeira extração e assimilação completas. Consulte [Lidar com grandes repositórios de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para obter mais detalhes.

1. Selecione um conjunto de migração em **Transferência de conteúdo** e clique em **Extract** para iniciar a extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >Verifique se a chave de extração é válida e não está próxima de sua expiração. Se estiver próximo da data de expiração, você poderá renovar a chave de Extração selecionando o conjunto de migração e clicando em Propriedades. Clique em **Renovar**. Isso o levará ao Cloud Acceleration Manager, onde você pode clicar em **Copiar chave de extração**. Sempre que você clicar em **Copiar chave de extração**, uma nova chave de Extração é gerada e é válida por 14 dias a partir do momento da criação.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. Isso exibirá a caixa de diálogo Extração. Clique em **Extract** para iniciar a fase de extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
   >Você tem a opção de substituir o container de preparo durante a fase de extração. Se **Substituir container de preparo** O está desativado e pode acelerar extrações para migrações subsequentes em que os caminhos de conteúdo ou as configurações de inclusão de versões não foram alterados. No entanto, se os caminhos de conteúdo ou as configurações de inclusão de versões tiverem sido alterados, **Substituir container de preparo** deve ser ativado.

1. A variável **Extração** O campo agora exibe a variável **EM EXECUÇÃO** status para indicar que a extração está em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   Você pode clicar em **Visualizar progresso** para obter uma visualização granular da extração em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   Você também pode monitorar o progresso da fase de Extração no Cloud Acceleration Manager visitando a página Transferência de conteúdo, e vê-lo com mais detalhes clicando em **..** e depois em **Exibir detalhes**.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. Depois que a extração for concluída, revise as outras colunas como **Origem** e **Caminhos** para obter detalhes sobre o conjunto de migração preenchido clicando em **..** e depois em **Exibir detalhes** para ver detalhes, incluindo a duração de cada etapa da extração. Visualize essa caixa de diálogo durante a extração para ver como as etapas estão progredindo.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service. Se você tiver usado a etapa de pré-cópia para a primeira extração completa, poderá ignorar a pré-cópia para extrações complementares subsequentes (se o tamanho do conjunto de migração complementar for menor que 200 GB), pois pode adicionar tempo a todo o processo.
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

Depois de aprender a Extrair conteúdo da origem na ferramenta Transferência de conteúdo, você está pronto para aprender o Processo de assimilação na ferramenta Transferência de conteúdo. Consulte [Assimilar conteúdo no Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para saber como assimilar seu conjunto de migração da ferramenta Transferência de conteúdo.
