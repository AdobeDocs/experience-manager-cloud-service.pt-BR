---
title: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.8.0
description: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.8.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.8.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager em AEM como Cloud Service 2020.8.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.8.0 é 6 de agosto de 2020.

## Novidades {#whats-new-cloud-manager}

* A Auditoria de conteúdo é um recurso ativado nos Pipelines de Produção de Sites do Cloud Manager. A configuração do pipeline de produção para programas com Sites agora inclui uma terceira guia chamada Auditoria **de** conteúdo. Sempre que um pipeline de produção for executado, uma nova etapa de Auditoria de conteúdo será incluída no pipeline após um teste funcional personalizado que avaliará o site em relação a várias dimensões, incluindo desempenho, SEO (Search Engine Otimization), acessibilidade, práticas recomendadas e PWA (Progressive Web App).


   >[!NOTE]
   >A Auditoria de conteúdo foi renomeada para Auditoria de experiência.

   Consulte Teste [de auditoria de](/help/implementing/cloud-manager/experience-audit-testing.md) experiência para obter mais detalhes.

* Ambientes recém-criados em programas do Assets agora serão configurados automaticamente com o Smart Content Services.

* Ambientes hibernados podem ser removidos da hibernação na página **Visão geral** do Gerenciador de nuvem.

* Capacidade de executar verificações de experiência em páginas, acionadas pelo Google Lighthouse. Como parte do pipeline do Cloud Manager, até 25 páginas podem ser verificadas e validadas em relação aos KPIs de experiência, e as pontuações são exibidas na interface do usuário do Cloud Manager.

### Correções de erros {#bug-fixes-cm}

* Alguns plug-ins SonarQube desnecessários e indesejados estavam sendo executados como parte da verificação de qualidade de código.

* Na página de execução de pipeline, o nome da ramificação estava formatado incorretamente.

* Em alguns casos, as execuções de pipeline concluídas não foram registradas com êxito como tendo sido concluídas, impedindo assim novas execuções do pipeline.

* Ocasionalmente, as execuções de pipeline ficariam *presas* devido a problemas de comunicação interna.

* Ao provisionar uma nova organização, alguns usuários com funções administrativas diferentes dos administradores de sistema receberam erroneamente acesso ao Cloud Manager.

* Em determinadas condições, o trabalho de índices de atualização foi iniciado várias vezes em paralelo, resultando em uma falha de implantação.

* A dica de ferramenta nos cartões de programa não estava consistentemente correta.

* A interface do usuário permitia erroneamente que as operações fossem tentadas em um ambiente durante sua exclusão.

* Ocorreu uma incompatibilidade de cores na página **Visão geral** do Gerenciador de nuvem.

### Problemas conhecidos {#known-issues-cm}

* As páginas inválidas são incluídas, colocando a Pontuação média de auditoria de conteúdo abaixo do que deveriam ser.

* A guia Auditoria de conteúdo exibe incorretamente o URL base usando o domínio do autor em vez do domínio de publicação.

* Para ativar a etapa Auditoria de conteúdo, os usuários devem editar o pipeline e, opcionalmente, adicionar páginas. Se nenhuma página for adicionada, a página inicial será auditada.