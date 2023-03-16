---
title: Backup e restauração em AEM as a Cloud Service
description: Backup e restauração em AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: eec03acf5d208236ddac338134f95fb3aaa5ee26
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---


# Backup e restauração em AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e restauração"
>abstract="AEM as a Cloud Service pode restaurar o aplicativo completo (código e conteúdo) de um cliente para horários específicos e predeterminados nos últimos sete dias, substituindo o que estava em produção. Esse recurso deve ser usado somente quando houver problemas graves com código ou conteúdo. Os dados recentes entre o momento do backup restaurado e o presente serão perdidos. O armazenamento temporário também será restaurado para a versão antiga."

Caso ocorra corrupção de conteúdo ou dados, AEM as a Cloud Service pode restaurar o aplicativo completo (código e conteúdo) de um cliente para horários específicos e predeterminados nos últimos sete dias, substituindo o que estava em produção.
Se a implantação de um cliente, o que significa que o código de aplicativo implantado está corrompido ou corrompido, é preferível corrigi-lo e implantá-lo em uma nova versão em vez de restaurá-lo a partir do backup. O backup é executado de uma maneira que não afeta o desempenho de tempo de execução de um aplicativo.

>[!CAUTION]
>
>Esse recurso deve ser usado somente quando houver problemas graves com código ou conteúdo. Os dados recentes entre o momento do backup restaurado e o presente serão perdidos. O armazenamento temporário também será restaurado para a versão antiga.

## Como usar {#how-to-use}

Os clientes devem registrar um tíquete de suporte, descrevendo o problema que está sendo enfrentado. Isso levará a uma investigação por parte do suporte Adobe, que determinará se uma restauração é necessária.

AEM suporte as a Cloud Service:

* Backup e restauração para ambientes de estágio, produção e desenvolvimento.
* Recuperação de 24 horas, o que significa que o sistema pode ser restaurado para qualquer ponto nas últimas 24 horas.
* Restaure a partir de um carimbo de data e hora específico e definido por Adobe, coletado duas vezes por dia nos últimos 7 dias.  Todas as mensagens de replicação (excluir, atualizar, criar) serão preservadas.

Em todos os casos, a versão do código personalizado será a retirada da última implantação bem-sucedida antes do ponto de restauração.

O RTO (Recovery Time Objetive, objetivo de tempo de recuperação) pode variar, mas como diretriz geral, a sequência de recuperação leva entre 60 e 90 minutos em média, dependendo de vários fatores, como o tamanho do repositório. Ambientes de visualização e editores de várias regiões podem estender o objetivo de tempo de restauração.

Após uma restauração, a versão do AEM será atualizada para a mais recente.

>[!CAUTION]
>
>Os dados de ambientes excluídos são perdidos permanentemente e não podem ser recuperados.

## Backup externo {#offsite-backup}

Embora os backups regulares cubram o risco de exclusões acidentais ou falhas técnicas nos Serviços em Nuvem do AEM, os riscos que podem surgir da falha de uma região também devem ser cobertos. Além da disponibilidade, o maior risco de paralisação dessas regiões de dados é principalmente a perda de dados.
AEM as a Cloud Service cobre esse risco como padrão para todos os ambientes de produção AEM copiando continuamente todo o conteúdo AEM para uma região remota e disponibilizando-o para recuperação por um período de três meses. Chamamos esse recurso de backup externo.
A restauração dos Serviços em Nuvem do AEM para ambientes de estágio e produção é realizada pela AEM Service Reliability Engineering em caso de paralisação da região de dados.
