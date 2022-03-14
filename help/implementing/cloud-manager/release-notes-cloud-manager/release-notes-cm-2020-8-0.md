---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2020.8.0
description: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2020.8.0
feature: Release Information
exl-id: 70674e16-f9ba-4777-98fe-34161e90a481
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2020.8.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2020.8.0.

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager AEM as a Cloud Service 2020.8.0 é 6 de agosto de 2020.

## Novidades {#whats-new-cloud-manager}

* A Auditoria de conteúdo é um recurso ativado nos Pipelines de produção de sites do Cloud Manager. A configuração Pipeline de produção para programas com Sites agora inclui uma terceira guia chamada **Auditoria de conteúdo**. Sempre que um pipeline de produção for executado, uma nova etapa de Auditoria de conteúdo será incluída no pipeline após um teste funcional personalizado que avaliará o site em relação a várias dimensões, incluindo desempenho, SEO (Otimização de mecanismo de pesquisa), acessibilidade, práticas recomendadas e PWA (Aplicativo web progressivo).


   >[!NOTE]
   >A Auditoria de conteúdo foi renomeada para Auditoria de experiência.

   Consulte [Teste de auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md) para obter mais detalhes.

* Os ambientes recém-criados nos programas do Assets agora serão configurados automaticamente com os Serviços de conteúdo inteligente.

* Ambientes hibernados podem ser removidos da hibernação no do Cloud Manager **Visão geral** página.

* Capacidade de executar verificações de experiência em páginas, acionadas pelo Google Lighthouse. Como parte do pipeline do Cloud Manager , até 25 páginas podem ser verificadas e validadas em relação aos KPIs de experiência, e as pontuações são exibidas na interface do usuário do Cloud Manager.

### Correções de erros {#bug-fixes-cm}

* Alguns plug-ins desnecessários e indesejados do SonarQube estavam sendo executados como parte da verificação de qualidade do código.

* Na página de execução do pipeline, o nome da ramificação estava formatado incorretamente.

* Em alguns casos, as execuções de pipeline concluídas não foram registradas com êxito como tendo sido concluídas, impedindo assim novas execuções do pipeline.

* Ocasionalmente, as execuções de pipeline receberiam *preso* devido a problemas de comunicação interna.

* Ao provisionar uma nova organização, alguns usuários com funções administrativas diferentes dos administradores de sistema receberam erroneamente acesso ao Cloud Manager.

* Sob determinadas condições, o trabalho de índices de atualização foi iniciado várias vezes em paralelo, resultando em uma falha de implantação.

* A dica de ferramenta nos cartões de programa não estava consistentemente correta.

* A interface do usuário permitiu erroneamente que as operações fossem tentadas em um ambiente enquanto eram excluídas.

* Havia uma incompatibilidade de cores no Cloud Manager **Visão geral** página.

### Problemas conhecidos {#known-issues-cm}

* Páginas inválidas são incluídas, trazendo a Pontuação média de auditoria de conteúdo abaixo do que deveriam ser.

* A guia Auditoria de conteúdo exibe incorretamente o URL base usando o domínio do autor em vez do domínio de publicação.

* Para ativar a etapa Auditoria de conteúdo , os usuários devem editar o pipeline e, opcionalmente, adicionar páginas. Se nenhuma página for adicionada, a página inicial será auditada.
