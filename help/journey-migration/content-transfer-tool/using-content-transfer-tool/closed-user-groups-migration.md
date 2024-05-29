---
title: Migrar grupos de usuários fechados
description: Saiba mais sobre as considerações especiais necessárias para habilitar Grupos de usuários fechados após a migração do conteúdo para o Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
source-git-commit: 29ffb48d23b4a2fe4973b005c98c5720b4196367
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 10%

---

# Migrar grupos de usuários fechados {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migração de grupos de usuários fechados"
>abstract="Atualmente, a migração de grupos de usuários fechados (CUG, sigla em inglês) requer algumas verificações e etapas para garantir a operação após a migração."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=pt-BR" text="Grupos de Usuários Fechados no AEM"

Atualmente, os Grupos de usuários fechados (CUG) precisam de algumas etapas adicionais para funcionarem no ambiente de destino de uma migração. Este documento explica o cenário e as etapas necessárias para protegê-los da maneira desejada.

## Migração de grupos

As principais (incluindo grupos) são incluídas automaticamente em uma migração para o Adobe Experience Manager as a Cloud Service se estiverem associadas ao conteúdo migrado por meio da ACL desse conteúdo, e também são incluídas se forem referenciadas em uma política CUG sobre esse conteúdo.

## Grupos de usuários fechados na migração

A verificação da existência do grupo e de seus membros deve ser feita antes da ativação. O Relatório principal, baixado por meio da visualização de Tarefa de assimilação, pode ser usado para ver se o grupo em questão foi incluído ou não porque não estava em uma ACL ou em uma política CUG.

Em seguida, os processos devem ser acionados e as propriedades devem ser definidas para ativar CUGs. Para fazer isso, publique novamente todas as páginas associadas a uma política CUG. Isso calibra a instância de Publicação para rastrear as políticas.

Isso ativa as políticas CUG em Publicar, e o conteúdo só é acessível aos usuários autenticados que são membros do grupo associado às políticas.

## Resumo

Em resumo, estas são as etapas para habilitar o CUG após uma migração:

1. Verifique se cada grupo usado nas políticas CUG existe em Publicar após a migração.
   - Um grupo pode existir se for incluído em uma política CUG de conteúdo migrado ou na ACL desse conteúdo.
   - Caso contrário, use Pacotes para instalá-lo na instância de destino (ou criá-lo manualmente) e ativá-lo e seus membros. Em seguida, verifique se ele existe em Publicar.
1. Republicar todas as páginas associadas a uma política CUG, garantindo que ela seja publicada, por exemplo, editando a página primeiro. É importante republicar todos eles.
   - Depois que todas as páginas forem republicadas, verifique a funcionalidade de cada página protegida por CUG.
