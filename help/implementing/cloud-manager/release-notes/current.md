---
title: Notas de versão do Cloud Manager 2023.9.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2023.9.0 no AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 8bf2ffe8b1d3780f4ad3f6972fea4f8281945abb
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 23%

---


# Notas de versão do Cloud Manager 2023.9.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2023.9.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2023.9.0 no AEM as a Cloud Service é 14 de setembro de 2023. A próxima versão está planejada para 5 de outubro de 2023.

## Novidades {#what-is-new}

* Os logs CDN, quando disponíveis, podem ser baixados por meio da interface do usuário do Cloud Manager.
* Os usuários agora podem optar por incluir o teste de Auditoria de experiência viabilizado pelo Google LightHouse em pipelines de pilha completa e não produção.

## Programa de adoção antecipada {#early-adoption}

Faça parte do nosso programa de adoção antecipada e tenha a chance de testar alguns recursos futuros.

### Restauração de conteúdo de autoatendimento {#content-restore}

[Um novo recurso de restauração de conteúdo de autoatendimento](/help/operations/restore.md) O agora oferece restauração de backup por até sete dias e está disponível para usuários iniciais para fins de avaliação, apresentando:

* Restauração de backup point-in-time nas últimas 24 horas
* Restaurações por tempo fixo de até sete dias

Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para `aemcs-restorefrombackup-adopter@adobe.com` do email associado à Adobe ID. Observação:

* O programa de adoção antecipada está limitado apenas a ambientes de desenvolvimento.
* A disponibilidade do programa de adoção antecipada deste recurso é limitada.
* Esse recurso é para recuperação de conteúdo excluído acidentalmente e não se destina à recuperação de desastres.

### Painel de auditoria de experiência {#experience-audit-dashboard}

[O painel de Auditoria de experiência do Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) O inclui uma exibição de tendências das pontuações de desempenho da página, juntamente com insights e recomendações para ajudar você a melhorá-las. A Auditoria de experiência está incluída como uma etapa no pipeline de produção do Cloud Manager.

O painel usa o Google Lighthouse, uma ferramenta de código aberto e automatizada para melhorar a qualidade dos seus aplicativos Web. Você pode executá-la em qualquer página da Web, pública ou que exija autenticação. Ele tem auditorias de desempenho, acessibilidade, aplicativos web progressivos, SEO e muito mais.

Interessado em testar o novo painel? Envie um email para `aem-lighthouse-pilot@adobe.com` do email associado à sua Adobe ID e podemos começar.

## Correções de erros {#bug-fixes}

* Quando um programa é excluído, qualquer pipeline associado em execução também é excluído, garantindo que o pipeline não seja designado incorretamente como status de falha.
* O botão Ativação concluída está desativado e informa ao usuário o motivo pelo qual um pipeline está em andamento.
* Ocasionalmente, quando todas as etapas de uma execução de pipeline são &#39;concluídas&#39;, o status do pipeline é visto como &quot;em execução&quot;, fazendo parecer que está em um estado travado. Agora é visto como &#39;Concluído&#39;.
