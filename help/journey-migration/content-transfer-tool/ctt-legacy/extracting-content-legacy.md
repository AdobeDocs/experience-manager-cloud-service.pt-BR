---
title: Extrair conteúdo da origem (herdado)
description: Extrair conteúdo da origem
hide: true
hidefromtoc: true
exl-id: 9f43356c-ba51-48bc-97f5-f1f5db81e7f3
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 34%

---

# Extrair conteúdo da origem (herdado) {#extracting-content}

## Processo de extração na ferramenta Transferência de conteúdo {#extraction-process}

Siga as etapas abaixo para extrair seu conjunto de migração da ferramenta Transferência de conteúdo:
>[!NOTE]
>Se o Amazon S3 ou o Azure Data Store for usado como o tipo de armazenamento de dados, você poderá executar a etapa opcional de pré-cópia para acelerar significativamente a fase de extração. Para fazer isso, você precisa configurar um `azcopy.config` arquivo antes de executar a extração. Consulte [Lidar com grandes repositórios de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para obter mais detalhes.

>[!IMPORTANT]
>Você deve executar a ferramenta Mapeamento de usuários antes de extrair o conteúdo da origem. Consulte [Utilização da Ferramenta de mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en) para obter mais detalhes.

1. Selecione um conjunto de migração em **Transferência de conteúdo** e clique em **Extract** para iniciar a extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. A variável **Extração do conjunto de migrações** é exibida e clique em **Extract** para iniciar a fase de extração.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >Opcionalmente, é possível substituir o container de preparo durante a fase de extração.

   >[!IMPORTANT]
   >Se o Mapeamento de usuários não tiver sido executado nesse conjunto de migração antes da extração do conteúdo da origem, você verá um aviso indicando que a etapa de Mapeamento de usuários está pendente, como mostrado na figura abaixo. Selecionar **Mapear usuários** para executar a ferramenta Mapeamento de usuários.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. A variável **Extração** O campo agora exibe a variável **EM EXECUÇÃO** status para indicar que a extração está em andamento.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   Quando a extração for concluída, o status do conjunto de migração será atualizado para **CONCLUÍDO**, e um ícone de nuvem *verde sólido* será exibido abaixo do campo **INFO** .

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >A interface do usuário do tem um recurso de recarregamento automático que recarrega o **Transferência de conteúdo** a cada 30 segundos.
   >Quando a fase de extração for iniciada, o bloqueio de gravação é criado e liberado após *60 segundos*. Em seguida, se uma extração for interrompida, você precisará esperar um minuto até que o bloqueio seja liberado antes de reiniciar a extração.

## Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.
>Além disso, certifique-se de que a estrutura de conteúdo do conteúdo existente não seja alterada desde o momento em que a extração inicial é realizada até o momento em que a extração complementar é executada. Os complementos não podem ser executados em um conteúdo cuja estrutura foi alterada desde a extração inicial. Restrinja isso durante o processo de migração.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração complementar.

Siga as etapas abaixo:

1. Navegue até a **Transferência de conteúdo** e selecione o conjunto de migração para o qual você deseja executar a extração complementar. Clique em **Extrair** para iniciar a extração complementar.

   ![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. A variável **Extração do conjunto de migrações** é exibida. Clique em **Extract**.

   >[!IMPORTANT]
   >Você deve desativar a opção **Substituir containercontêiner de preparação durante a extração**.
   >![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## O que vem a seguir {#whats-next}

Depois de saber mais sobre &quot;Extração de conteúdo da origem&quot; na Ferramenta de transferência de conteúdo, agora você está pronto para aprender o Processo de assimilação na Ferramenta de transferência de conteúdo. Consulte [Assimilar conteúdo no Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para saber como assimilar seu conjunto de migração da ferramenta Transferência de conteúdo.
