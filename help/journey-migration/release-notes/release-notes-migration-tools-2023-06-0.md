---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.06.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.06.0
feature: Release Information
exl-id: 021b7472-d1e4-4ef6-a040-c612fed8d3c3
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 3%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.06.0 {#release-notes}

Esta página descreve as Notas de versão das Ferramentas de migração no AEM as a Cloud Service 2023.06.0.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v2.0.20 é 8 de junho de 2023.

### Novidades {#what-is-new-ctt}

* Uma nova ferramenta de migração - o Transformador de conteúdo (CT) foi integrada à Ferramenta de transferência de conteúdo (CTT) com esta versão. O Transformador de Conteúdo pode detectar e corrigir automaticamente problemas relacionados ao conteúdo relatados pelo [Analisador de Práticas Recomendadas (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=pt-BR) antes de migrar o conteúdo da sua implementação de AEM atual (No local ou Managed Services) para o AEM as a Cloud Service.
Os benefícios fornecidos pelo transformador de conteúdo são:
   * À prova de falhas: um pacote é criado pelo Transformador de conteúdo sempre que ele faz qualquer modificação no repositório para corrigir problemas. Se necessário, é possível reverter para o estado anterior instalando o pacote.
   * Fácil de usar: o transformador de conteúdo foi integrado à ferramenta de transferência de conteúdo e vem com uma interface de usuário simples e intuitiva.
   * Economiza tempo: quando você tem um alto número de problemas de conteúdo que se enquadram em uma categoria de padrão, é possível resolver todos com vários cliques usando o Transformador de conteúdo, o que reduz significativamente o tempo e a complexidade da migração.
