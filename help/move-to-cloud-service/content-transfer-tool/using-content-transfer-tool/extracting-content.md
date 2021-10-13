---
title: Extrair conteúdo da origem na ferramenta Transferência de conteúdo
description: Extrair conteúdo da origem na ferramenta Transferência de conteúdo
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 53%

---


# Extrair conteúdo da origem na ferramenta Transferência de conteúdo {#extracting-content}

## Processo de extração na ferramenta Transferência de conteúdo {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="Extração de conteúdo"
>abstract="Extração refere-se à extração de conteúdo da instância de AEM de origem em uma área temporária chamada de conjunto de migração. Um conjunto de migração é uma área de armazenamento em nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância do AEM de origem e a instância do AEM Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="Extração complementar"

Siga as etapas abaixo para extrair seu conjunto de migração da ferramenta Transferência de conteúdo:
>[!NOTE]
>Se o Amazon S3 ou o Azure Data Store for usado como o tipo de armazenamento de dados, você poderá executar a etapa opcional de pré-cópia para acelerar significativamente a fase de extração. Para fazer isso, será necessário configurar um arquivo `azcopy.config` antes de executar a extração. Consulte [Manuseio de repositórios de conteúdo grandes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para obter mais detalhes.

1. Selecione um conjunto de migração na página *Visão geral* e clique em **Extrair** para iniciar a extração. A caixa de diálogo **Extração do conjunto de migração** é exibida e clique em **Extrair** para iniciar a fase de extração.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >Você tem a opção de substituir o containercontêiner de preparação durante a fase de extração.


1. O campo **EXTRAÇÃO** agora exibe o status **EXECUÇÃO** para indicar que a extração está em andamento.

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   Quando a extração for concluída, o status do conjunto de migração será atualizado para **CONCLUÍDO**, e um ícone de nuvem *verde sólido* será exibido abaixo do campo **INFO** .

   ![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >A interface do usuário tem um recurso de recarregamento automático que recarrega a página de visão geral a cada 30 segundos.
   >Quando a fase de extração for iniciada, o bloqueio de gravação é criado e liberado após *60 segundos*. Em seguida, se uma extração for interrompida, você precisará esperar um minuto até que o bloqueio seja liberado antes de reiniciar a extração.

## Extração complementar {#top-up-extraction-process}

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.
>Além disso, é essencial que a estrutura de conteúdo do conteúdo existente não seja alterada do momento em que a extração inicial é levada ao momento em que a extração complementar é executada. Os complementos não podem ser executados em conteúdo cuja estrutura foi alterada desde a extração inicial. Certifique-se de restringir isso durante o processo de migração.

Quando o processo de extração estiver concluído, você poderá transferir o conteúdo delta usando o método de extração complementar. Siga as etapas abaixo:

1. Navegue até a página *Visão geral* e selecione o conjunto de migração para o qual você deseja realizar a extração complementar. Clique em **Extrair** para iniciar a extração complementar. A caixa de diálogo **Extração do conjunto de migração** é exibida.

   >[!IMPORTANT]
   >
   >Você deve desativar a opção **Substituir containercontêiner de preparação durante a extração**.
   >
   >![imagem](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)
