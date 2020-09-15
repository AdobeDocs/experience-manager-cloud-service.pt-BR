---
title: Backup e restauração em AEM como Cloud Service
description: 'Backup e restauração em AEM como Cloud Service '
translation-type: tm+mt
source-git-commit: c3af507716ef60541ecca8dafb797651e8ece9d3
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Backup e restauração em AEM como Cloud Service

Caso ocorra corrupção de conteúdo ou dados, AEM como Cloud Service pode restaurar o aplicativo completo (código e conteúdo) de um cliente para horários específicos e predeterminados nos últimos sete dias, substituindo o que estava em produção.
Se a implantação de um cliente, o que significa que o código do aplicativo implantado está quebrado ou com problemas, é preferível corrigi-lo e encaminhá-lo para uma nova versão em vez de restaurá-lo a partir do backup. O backup é executado de uma maneira que não afeta o desempenho do tempo de execução de um aplicativo.

>[!CAUTION]
>
>Esse recurso deve ser usado somente quando houver problemas graves com o código ou o conteúdo. Os dados recentes entre o momento do backup restaurado e o atual serão perdidos. O armazenamento temporário também será restaurado para a versão antiga.

## Como usar

Os clientes devem registrar um ticket de suporte, descrevendo o problema que está sendo enfrentado. Isso levará a uma investigação por parte do suporte a Adobe que determinará se uma restauração é necessária.

AEM como Cloud Service suporta:

* Recuperação de 24 horas por ponto, o que significa que o sistema pode ser restaurado para qualquer ponto nas últimas 24 horas.
* Restaure a partir de um carimbo de data e hora específico e definido por Adobe, retirado uma vez por dia nos últimos 7 dias.  Todas as mensagens de replicação (excluir, atualizar, criar) serão preservadas.

Em todos os casos, a versão do código personalizado será a retirada da última implantação bem-sucedida antes do ponto de restauração.

O RTO (Recovery Time Objetive, objetivo de tempo de recuperação) varia com base no tamanho do repositório, mas como orientação geral, uma vez iniciada a sequência de restauração, deve levar cerca de 30 minutos.

Após uma restauração, a versão AEM será atualizada para a mais recente.

**Os dados de ambientes excluídos são perdidos permanentemente e não podem ser recuperados.**
