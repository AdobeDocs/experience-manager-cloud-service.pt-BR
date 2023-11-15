---
title: Backup e restauração no AEM as a Cloud Service
description: Saiba mais sobre backup e restauração no AEM as a Cloud Service
exl-id: 469fb1a1-7426-4379-9fe3-f5b0ebf64d74
source-git-commit: 83b5d9a3ff0e9a3c69e36a97a3f733b05f827d3b
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 27%

---


# Backup e restauração no AEM as a Cloud Service {#backup-aemaacs}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_backuprestore"
>title="Backup e restauração"
>abstract="O AEM as a Cloud Service pode restaurar o aplicativo completo (código e conteúdo) de um cliente para uma hora específica e predeterminada nos últimos sete dias, substituindo o que estava em produção. Esse recurso deve ser usado somente quando houver problemas graves com código ou conteúdo. Os dados recentes entre o momento do backup restaurado e o presente foram perdidos. O preparo também é restaurado para a versão antiga."

Caso ocorra corrupção de conteúdo ou dados, o AEM as a Cloud Service pode restaurar o aplicativo completo de um cliente (código e conteúdo). Ele é restaurado para horários específicos e predeterminados nos últimos sete dias, substituindo o que estava em produção.
Se a implantação de um cliente, o que significa que o código do aplicativo implantado está corrompido ou com problemas, é preferível corrigi-lo e avançar para uma nova versão em vez de restaurá-lo a partir do backup. O backup é executado de forma que não afete o desempenho de tempo de execução de um aplicativo.

>[!CAUTION]
>
>Esse recurso deve ser usado somente quando houver problemas graves com código ou conteúdo. Os dados recentes entre o momento do backup restaurado e o presente foram perdidos. O preparo também é restaurado para a versão antiga.

## Como usar {#how-to-use}

Os clientes devem registrar um tíquete de suporte, descrevendo o problema enfrentado. O tíquete de suporte geralmente leva a uma investigação pelo suporte de Adobe, que pode determinar se uma restauração é necessária.

O AEM as a Cloud Service suporta:

* Backup e restauração para ambientes de preparo, produção e desenvolvimento.
* Recuperação pontual em 24 horas, o que significa que o sistema pode ser restaurado para qualquer ponto nas últimas 24 horas.
* Restaurar a partir de um carimbo de data e hora específico definido por Adobe, tirado duas vezes por dia nos últimos sete dias. Todas as mensagens de replicação (exclusões, atualizações, criações) são preservadas.

Em todos os casos, a versão do código personalizado é a retirada da última implantação bem-sucedida antes do ponto de restauração.

O RTO (Recovery Time Objetive, objetivo de tempo de recuperação) pode variar, mas como diretriz geral, a sequência de recuperação leva de 60 a 90 minutos em média, dependendo de vários fatores, como o tamanho do repositório. Ambientes de visualização e editores de várias regiões podem estender o objetivo de tempo de restauração.

Após uma restauração, a versão do AEM é atualizada para a mais recente.

>[!CAUTION]
>
>Os dados de ambientes excluídos são perdidos permanentemente e não podem ser recuperados.

## Backup externo {#offsite-backup}

Embora os backups regulares cubram o risco de exclusões acidentais ou falhas técnicas nos Cloud Service AEM, os riscos que podem surgir da falha de uma região também devem ser cobertos. Além da disponibilidade, o maior risco em interrupções nessa região de dados é principalmente a perda de dados.
O AEM as a Cloud Service cobre esse risco como padrão para todos os ambientes de produção do AEM. Ele copia continuamente todo o conteúdo do AEM para uma região remota e o disponibiliza para recuperação por três meses. O Adobe chama esse recurso de Backup Externo.
A restauração dos Cloud Service de AEM para ambientes de preparo e produção é realizada pelo Serviço de Engenharia de Confiabilidade do AEM se houver interrupções na região de dados.