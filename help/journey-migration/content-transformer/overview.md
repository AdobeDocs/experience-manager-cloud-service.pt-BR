---
title: Visão geral do transformador de conteúdo
description: Saiba como detectar e corrigir problemas relacionados ao conteúdo relatados pelo BPA usando o Transformador de conteúdo.
exl-id: aa3397ff-3dd6-4c67-9064-cb9b19bf1c73
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Visão geral {#overview-ct}

O CT (Transformador de Conteúdo) é uma ferramenta desenvolvida pelo Adobe que pode ser usada para detectar e corrigir automaticamente problemas relacionados ao conteúdo relatados pelo [Analisador de Práticas Recomendadas (BPA)](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) antes de migrar o conteúdo da sua implementação de AEM atual (No local ou Managed Services) para o AEM as a Cloud Service.

O Transformador de Conteúdo pode ajudar a resolver problemas que se enquadram nas [categorias de padrão BPA](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=pt-BR) a seguir (mostradas na tabela abaixo), permitindo que os usuários executem ações em massa, como mover ou excluir. Isso pode reduzir significativamente o tempo e a complexidade associados a um projeto de migração.

## Categorias de padrões cobertas pelo Transformador de conteúdo e soluções sugeridas {#pattern-categories-and-benefits}

| Código do padrão | Tipo/Subtipo de suspeita | Possível correção antes de migrar o conteúdo para o AEM as a Cloud Service |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendants.route | Mova esses ativos para um local diferente ou exclua-os para garantir que não sejam migrados para o AEM as a Cloud Service. |
| CAV | content.area.violation | Mova os caminhos temporariamente para `/etc/packages/content-transformation/paths` para garantir que eles não sejam migrados para o AEM as a Cloud Service. |
| DOPI | deprecated.ordered.index | Remova os índices obsoletos. |
| OAUI | non.migrated.oauth.users | Remova esses usuários para garantir que eles não sejam migrados para o AEM as a Cloud Service. |
| PCX | page.complex.medium <br> page.complex.high | Exclua as páginas/filhos ou mova-os para um local diferente para garantir que eles não sejam migrados para o AEM as a Cloud Service. |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modify <br> custom.replication.agent.detection | Remova os agentes de replicação criados. <br> OU <br> Remova as propriedades modificadas/adicionadas. |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | Mova para o local correto para evitar problemas durante a migração. |
| URS | node.size | Mova os nós temporariamente para `/etc/packages/content-transformation/paths` para garantir que eles não sejam migrados para o AEM as a Cloud Service. |

## Benefícios fornecidos pelo transformador de conteúdo {#benefits}

O transformador de conteúdo oferece os seguintes benefícios:

* À prova de falhas: um pacote é criado pelo Transformador de conteúdo sempre que ele faz qualquer modificação no repositório para corrigir problemas. Se necessário, é possível reverter para o estado anterior instalando o pacote.
* Fácil de usar: o transformador de conteúdo foi integrado à ferramenta de transferência de conteúdo e vem com uma interface de usuário simples e intuitiva.
* Economiza tempo: quando você tem um alto número de problemas de conteúdo que se enquadram em uma categoria de padrão, é possível resolver todos com vários cliques usando o Transformador de conteúdo.
