---
title: Backup e restauração no AEM como um serviço em nuvem
description: 'Backup e restauração no AEM como um serviço em nuvem '
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 1%

---


# Backup e restauração no AEM como um serviço em nuvem

Caso ocorra corrupção de conteúdo ou dados, o AEM como um serviço em nuvem pode restaurar o aplicativo completo (código e conteúdo) de um cliente para horários específicos e predeterminados nos últimos sete dias, substituindo o que estava em produção.
Se a implantação de um cliente, o que significa que o código do aplicativo implantado está quebrado ou com problemas, é preferível corrigi-lo e encaminhá-lo para uma nova versão em vez de restaurá-lo a partir do backup.

>[!CAUTION]
>
>Esse recurso deve ser usado somente quando houver problemas graves com o código ou o conteúdo. Os dados recentes entre o momento do backup restaurado e o atual serão perdidos. O armazenamento temporário também será restaurado para a versão antiga.

## Como usar

Os clientes devem registrar um ticket de suporte, descrevendo o problema que está sendo enfrentado. Isso levará a uma investigação por parte do suporte da Adobe que determinará se uma restauração é necessária.

O AEM como serviço de nuvem oferece suporte a:

* Recuperação de 24 horas por ponto, o que significa que o sistema pode ser restaurado para qualquer ponto nas últimas 24 horas.
* Restaure a partir de um carimbo de data e hora específico e definido pela Adobe, retirado uma vez por dia nos últimos 7 dias.  Todas as mensagens de replicação (excluir, atualizar, criar) serão preservadas.

Em todos os casos, a versão do código personalizado será a retirada da última implantação bem-sucedida antes do ponto de restauração.

O RTO (Recovery Time Objetive, objetivo de tempo de recuperação) varia com base no tamanho do repositório, mas como orientação geral, uma vez iniciada a sequência de restauração, deve levar cerca de 30 minutos.

Após uma restauração, a versão do AEM será atualizada para a mais recente.

**Os dados de ambientes excluídos são perdidos permanentemente e não podem ser recuperados.**
