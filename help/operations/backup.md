---
title: Backup e restauração no AEM as a Cloud Service
description: Backup e restauração no AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 17%

---


# Backup e restauração no AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e restauração"
>abstract="O AEM as a Cloud Service pode restaurar o aplicativo completo (código e conteúdo) de um cliente para uma hora específica e predeterminada nos últimos sete dias, substituindo o que estava em produção. Esse recurso deve ser usado somente quando houver problemas graves com código ou conteúdo. Os dados recentes entre o momento do backup restaurado e o presente são perdidos. O armazenamento temporário também será restaurado para a versão antiga."

Caso ocorra corrupção de conteúdo ou dados, o AEM as a Cloud Service pode restaurar o aplicativo completo de um cliente (código e conteúdo) para horários específicos e predeterminados nos últimos sete dias, substituindo o que estava em produção.
Se a implantação de um cliente, o que significa que o código do aplicativo implantado está corrompido ou com problemas, é preferível corrigi-lo e avançar para uma nova versão em vez de restaurá-lo a partir do backup. O backup é executado de forma que não afete o desempenho de tempo de execução de um aplicativo.

>[!CAUTION]
>
>Esse recurso deve ser usado somente quando houver problemas graves com código ou conteúdo. Os dados recentes entre o momento do backup restaurado e o presente são perdidos. O armazenamento temporário também é restaurado para a versão antiga.

## Como usar {#how-to-use}

Os clientes devem registrar um tíquete de suporte, descrevendo o problema enfrentado. Isso levará a uma investigação do suporte do Adobe, que determinará se uma restauração é necessária.

O AEM as a Cloud Service suporta:

* Backup e restauração para ambientes de preparo, produção e desenvolvimento.
* Recuperação em 24 horas, o que significa que o sistema pode ser restaurado para qualquer ponto nas últimas 24 horas.
* Restaurar a partir de um carimbo de data e hora específico definido por Adobe, tirado duas vezes por dia nos últimos sete dias.  Todas as mensagens de replicação (exclusões, atualizações, criações) são preservadas.

Em todos os casos, a versão do código personalizado é a retirada da última implantação bem-sucedida antes do ponto de restauração.

O RTO (Recovery Time Objetive, objetivo de tempo de recuperação) pode variar, mas como diretriz geral, a sequência de recuperação leva entre 60 e 90 minutos em média, dependendo de vários fatores, como o tamanho do repositório. Ambientes de visualização e editores de várias regiões podem estender o objetivo de tempo de restauração.

Após uma restauração, a versão do AEM é atualizada para a mais recente.

>[!CAUTION]
>
>Os dados de ambientes excluídos são perdidos permanentemente e não podem ser recuperados.

## Backup externo {#offsite-backup}

Embora os backups regulares cubram o risco de exclusões acidentais ou falhas técnicas nos serviços em nuvem do AEM, os riscos que podem surgir da falha de uma região também devem ser cobertos. Além da disponibilidade, o maior risco em interrupções nessa região de dados é principalmente a perda de dados.
A AEM as a Cloud Service cobre esse risco como padrão para todos os ambientes de produção de AEM copiando continuamente todo o conteúdo de AEM para uma região remota e disponibilizando-o para recuperação por um período de três meses. Chamamos esse recurso de Backup Externo.
A restauração dos serviços em nuvem do AEM para ambientes de preparo e produção é realizada pelo Serviço de engenharia de confiabilidade do AEM em caso de interrupções da região de dados.
