---
title: Migração de grupos de usuários fechados
description: Esta página fornece as considerações especiais necessárias para habilitar Grupos de usuários fechados após a migração do conteúdo para o Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
source-git-commit: 9da813d39d154e81da5b9814aa86b8318dc0bb3a
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 8%

---

# Migração de grupos de usuários fechados {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migração de Grupos de Usuários Fechados"
>abstract="Atualmente, a migração de grupos de usuários fechados (CUG, sigla em inglês) requer algumas verificações e etapas para garantir a operação após a migração."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=pt-BR" text="Grupos de Usuários Fechados no AEM"

Atualmente, os Grupos de usuários fechados (CUG) precisam de algumas etapas adicionais para funcionarem no ambiente de destino de uma migração.  Este documento explica o cenário e as etapas necessárias para protegê-los da maneira desejada.

## Migração de grupos

As entidades principais (incluindo grupos) são incluídas automaticamente em uma migração para o Adobe Experience Manager as a Cloud Service se estiverem associadas ao conteúdo migrado por meio da ACL desse conteúdo.

## Grupos de usuários fechados na migração

Atualmente, os grupos associados *somente* com uma política de Grupo de usuários fechado (CUG) são *não* incluído automaticamente na assimilação. Como dito acima, eles serão migrados se estiverem associados a qualquer conteúdo por meio de uma ACL. A verificação da existência do grupo e de seus membros deve ser feita antes da ativação. O Relatório principal, baixado por meio da visualização Trabalho de assimilação, pode ser usado para ver se o grupo em questão foi incluído ou não porque não estava em uma ACL. Se o grupo não existir, ele deverá ser criado na instância do Autor, incluindo a adição de membros apropriados, e ativado para que exista na instância de Publicação. Isso pode ser feito usando pacotes criados na origem.

Por fim, os processos devem ser acionados e as propriedades devem ser definidas para habilitar os CUGs. Para fazer isso, publique novamente todas as páginas associadas a uma política CUG. Isso calibrará a instância de publicação para rastrear as políticas.

Isso ativará as políticas CUG em Publicar, e o conteúdo só estará acessível aos usuários autenticados que são membros do grupo associado às políticas.

## Desenvolvimento ativo

A equipe de migração está trabalhando para que as políticas do CUG migrem e funcionem automaticamente, sem etapas adicionais após assimilar o conteúdo.
É aconselhável incluir a funcionalidade CUG em qualquer processo de teste antes de tentar entrar em funcionamento.

## Resumo

Em resumo, estas são as etapas para habilitar o CUG após uma migração:

1. Verifique se cada grupo usado nas políticas CUG existe em Publicar após a migração.
   - Um grupo já pode existir se for incluído na ACL de um conteúdo migrado.
   - Caso contrário, use pacotes para instalá-lo na instância de destino (ou criá-lo manualmente) e ativá-lo e seus membros. Em seguida, verifique se ele existe em Publicar.
1. Republicar todas as páginas associadas a uma política CUG, garantindo que ela seja publicada, por exemplo, editando a página primeiro. É importante republicar todas elas.
   - Depois que todas as páginas forem publicadas novamente, verifique a funcionalidade de cada página protegida por CUG.

