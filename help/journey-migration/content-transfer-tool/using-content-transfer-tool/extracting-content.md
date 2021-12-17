---
title: Extrair conteúdo da origem
description: Extrair conteúdo da origem
source-git-commit: bcbf4e4ba1330bef9f2c8c473419903e40ac0e58
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 36%

---


# Extrair conteúdo da origem {#extracting-content}

## Processo de extração na ferramenta Transferência de conteúdo {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extração de conteúdo"
>abstract="Extração refere-se à extração de conteúdo da instância de AEM de origem em uma área temporária chamada de conjunto de migração. Um conjunto de migração é uma área de armazenamento em nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância do AEM de origem e a instância do AEM Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extração complementar"


Siga as etapas abaixo para extrair seu conjunto de migração da ferramenta Transferência de conteúdo:
>[!NOTE]
>Se o Amazon S3 ou o Azure Data Store for usado como o tipo de armazenamento de dados, você poderá executar a etapa opcional de pré-cópia para acelerar significativamente a fase de extração. Para fazer isso, será necessário configurar um `azcopy.config` arquivo antes de executar a extração. Consulte [Lidar com grandes repositórios de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para obter mais detalhes.

>[!IMPORTANT]
>Você deve executar a ferramenta Mapeamento de usuários antes de extrair o conteúdo da origem. Consulte [Usar a ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) para obter mais detalhes.

1. Selecione um conjunto de migração de **Transferência de conteúdo** e clique em **Extract** para iniciar a extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. O **Extração do conjunto de migração** é exibida e clique em **Extract** para iniciar a fase de extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >Você tem a opção de substituir o containercontêiner de preparação durante a fase de extração.

   >[!IMPORTANT]
   >Se o Mapeamento de usuários não tiver sido executado nesse conjunto de migração antes da extração de conteúdo da origem, você verá um aviso exibindo se a etapa Mapeamento de usuários está pendente, como mostrado na figura abaixo. Clique em **Mapear usuários** para executar a ferramenta Mapeamento de usuários.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. O **Extração** agora exibe a variável **EM EXECUÇÃO** status para indicar que a extração está em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   Quando a extração for concluída, o status do conjunto de migração será atualizado para **CONCLUÍDO**, e um ícone de nuvem *verde sólido* será exibido abaixo do campo **INFO** .

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >A interface do usuário tem um recurso de recarregamento automático que recarrega o **Transferência de conteúdo** assistente a cada 30 segundos.
   >Quando a fase de extração for iniciada, o bloqueio de gravação é criado e liberado após *60 segundos*. Em seguida, se uma extração for interrompida, você precisará esperar um minuto até que o bloqueio seja liberado antes de reiniciar a extração.

## Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.
>Além disso, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada do momento em que a extração inicial é levada ao momento em que a extração complementar é executada. Os complementos não podem ser executados em conteúdo cuja estrutura foi alterada desde a extração inicial. Certifique-se de restringir isso durante o processo de migração.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração complementar.

Siga as etapas abaixo:

1. Navegue até o **Transferência de conteúdo** e selecione o conjunto de migração para o qual deseja executar a extração complementar. Clique em **Extrair** para iniciar a extração complementar.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. O **Extração do conjunto de migração** será exibida. Clique em **Extract**.

   >[!IMPORTANT]
   >Você deve desativar a opção **Substituir containercontêiner de preparação durante a extração**.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## O que vem a seguir {#whats-next}

Depois de aprender a extrair conteúdo da origem na ferramenta Transferência de conteúdo, você estará pronto para aprender o Processo de assimilação na ferramenta Transferência de conteúdo. Consulte [Inserção de conteúdo ao Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para saber como assimilar seu conjunto de migração na ferramenta Transferência de conteúdo.
