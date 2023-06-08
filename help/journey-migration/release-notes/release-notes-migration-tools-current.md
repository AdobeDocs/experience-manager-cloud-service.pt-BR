---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.06.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.06.0
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: a1597e4102589dfc9b5bdb8c2a54e8e9ec3392b7
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.06.0 {#release-notes}

Esta página descreve as notas de versão das ferramentas de migração no AEM as a Cloud Service 2022.06.0.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v2.0.20 é 8 de junho de 2023.

### Novidades {#what-is-new-ctt}

* Uma nova ferramenta de migração - o Transformador de conteúdo (CT) foi integrada à Ferramenta de transferência de conteúdo (CTT) com esta versão. O transformador de conteúdo pode detectar e corrigir automaticamente problemas relacionados ao conteúdo relatados pelo [Analisador de práticas recomendadas (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) antes de migrar o conteúdo da sua implementação atual do AEM (no local ou Managed Services) para o AEM as a Cloud Service.
Os benefícios fornecidos pelo transformador de conteúdo são:
   * À prova de falhas: um pacote é criado pelo Transformador de conteúdo sempre que ele faz qualquer modificação no repositório para corrigir problemas. Se necessário, é possível reverter para o estado anterior instalando o pacote.
   * Fácil de usar: o transformador de conteúdo foi integrado à ferramenta de transferência de conteúdo e vem com uma interface de usuário simples e intuitiva.
   * Economiza tempo: quando você tem um alto número de problemas de conteúdo que se enquadram em uma categoria de padrão, é possível resolver todos eles com apenas alguns cliques usando o Transformador de conteúdo, o que reduz significativamente o tempo e a complexidade da migração.
