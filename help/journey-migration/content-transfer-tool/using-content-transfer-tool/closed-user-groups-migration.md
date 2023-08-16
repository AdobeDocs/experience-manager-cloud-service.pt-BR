---
title: Migração de grupos de usuários fechados
description: Esta página fornece as considerações especiais necessárias para habilitar Grupos de usuários fechados após a migração do conteúdo para o Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
source-git-commit: ca3c4bae2e652d75190d68c76b1dd4e09239f16c
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 7%

---

# Migração de grupos de usuários fechados {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migração de Grupos de Usuários Fechados"
>abstract="Atualmente, a migração de Grupos de Usuários Fechados (CUG, sigla em inglês) requer algumas verificações e etapas para se tornar operacional após uma migração."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=pt-BR" text="Grupos de Usuários Fechados no AEM"

Atualmente, os Grupos de usuários fechados (CUG) precisam de algumas etapas adicionais para funcionarem no ambiente de destino de uma migração.  Este documento explica o cenário e as etapas necessárias para protegê-los da maneira desejada.

## Migração de grupos

As entidades principais (incluindo grupos) são incluídas automaticamente em uma migração para o Adobe Experience Manager as a Cloud Service se estiverem associadas ao conteúdo migrado por meio da ACL desse conteúdo.

## Grupos de usuários fechados na migração

Atualmente, os grupos associados *somente* com uma política de Grupo de usuários fechado (CUG) são *não* incluído automaticamente na assimilação. Se estiverem associados a qualquer conteúdo por meio de uma ACL, como dito acima, eles serão migrados. A verificação de que o grupo existe deve ser feita antes da ativação. O Relatório principal, baixado por meio da visualização Trabalho de assimilação, pode ser usado para ver se o grupo em questão foi incluído ou não porque não estava em uma ACL. Se o grupo não existir, ele deverá ser criado na instância do Autor, incluindo a adição de membros apropriados, e ativado para que exista na instância de Publicação.

Finalmente, os processos devem ser acionados para habilitar o CUG. Para fazer isso, publique novamente qualquer conteúdo que contenha a política CUG. Portanto, em seus processos normais de teste, se for descoberto que o CUG não funciona, publique novamente esse conteúdo (garantindo que ele seja publicado mesmo se não for modificado).

Isso deve ativar as políticas CUG em Publicar, e o conteúdo só estará acessível aos usuários autenticados que são membros do grupo associado às políticas.

## Desenvolvimento ativo

A equipe de migração está trabalhando para que as políticas do CUG migrem e funcionem automaticamente, sem etapas adicionais após assimilar o conteúdo.
É aconselhável incluir a funcionalidade CUG em qualquer processo de teste antes de tentar entrar em funcionamento.

## Resumo

Em resumo, estas são as etapas para habilitar o CUG após uma migração:

1. Verifique se cada grupo usado nas políticas CUG existe em Publicar após a migração.
   - Um grupo já pode existir se for incluído na ACL de um conteúdo migrado.
   - Caso contrário, use pacotes para instalá-lo na instância de destino (ou criá-lo manualmente) e ativá-lo e seus membros. Em seguida, verifique se ele existe em Publicar.
1. Se a política CUG ainda não proteger o nó, publique novamente a página (garantindo que ela seja publicada mesmo que nenhuma alteração seja feita nessa página).
   - Verifique para cada nó protegido por CUG.
