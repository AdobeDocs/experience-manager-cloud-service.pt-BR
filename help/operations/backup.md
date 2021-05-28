---
title: Backup e restauração no AEM como Cloud Service
description: Backup e restauração no AEM como Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Backup e restauração no AEM como Cloud Service


>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e restauração"
>abstract="O AEM como Cloud Service pode restaurar o aplicativo completo (código e conteúdo) de um cliente para horários específicos e predeterminados nos últimos sete dias, substituindo o que estava em produção. Esse recurso deve ser usado somente quando houver problemas graves com código ou conteúdo. Os dados recentes entre o momento do backup restaurado e o presente serão perdidos. O armazenamento temporário também será restaurado para a versão antiga."

Caso ocorra corrupção de conteúdo ou dados, o AEM como Cloud Service pode restaurar o aplicativo completo (código e conteúdo) de um cliente para horários específicos e predeterminados nos últimos sete dias, substituindo o que estava em produção.
Se a implantação de um cliente, o que significa que o código de aplicativo implantado está corrompido ou corrompido, é preferível corrigi-lo e implantá-lo em uma nova versão em vez de restaurá-lo a partir do backup. O backup é executado de uma maneira que não afeta o desempenho de tempo de execução de um aplicativo.

>[!CAUTION]
>
>Esse recurso deve ser usado somente quando houver problemas graves com código ou conteúdo. Os dados recentes entre o momento do backup restaurado e o presente serão perdidos. O armazenamento temporário também será restaurado para a versão antiga.

## Como usar

Os clientes devem registrar um tíquete de suporte, descrevendo o problema que está sendo enfrentado. Isso levará a uma investigação por parte do suporte Adobe, que determinará se uma restauração é necessária.

O AEM as a Cloud Service suporta:

* Recuperação de 24 horas, o que significa que o sistema pode ser restaurado para qualquer ponto nas últimas 24 horas.
* Restaure a partir de um carimbo de data e hora específico e definido por Adobe, coletado uma vez por dia nos últimos 7 dias.  Todas as mensagens de replicação (excluir, atualizar, criar) serão preservadas.

Em todos os casos, a versão do código personalizado será a retirada da última implantação bem-sucedida antes do ponto de restauração.

O RTO (Recovery Time Objetive, objetivo de tempo de recuperação) varia de acordo com o tamanho do repositório, mas como diretriz geral, uma vez que a sequência de restauração começa, deve levar cerca de 30 minutos.

Após uma restauração, a versão do AEM será atualizada para a mais recente.

**Os dados de ambientes excluídos são perdidos permanentemente e não podem ser recuperados.**
