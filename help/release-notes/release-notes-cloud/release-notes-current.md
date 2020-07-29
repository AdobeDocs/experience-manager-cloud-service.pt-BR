---
title: Notas de versão do Adobe Experience Manager as a Cloud Service 2020.7.0
description: Notas de versão do Experience Manager para 2020.7.0
translation-type: tm+mt
source-git-commit: 9e27ff9510fda5ed238a25b2d63d1d9a3099a8b5
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 87%

---


# Notas de versão do AEM as a Cloud Service 2020.7.0 {#release-notes}

A seção a seguir descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.7.0.

## Novidades do Cloud Manager {#cloud-manager}

Consulte esta seção para saber mais sobre as novidades e atualizações do Cloud Manager no AEM as a Cloud Service, versão 2020.7.0.

### Data de lançamento {#release-date}

A data de lançamento da versão 2020.7.0 do [!UICONTROL Cloud Manager] é 9 de julho de 2020.

### Novidades {#what-is-new-cloud-manager}

* A página de ambientes foi renovada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O número de variáveis por ambiente aumentou para 200.

* Os pipelines do Cloud Manager agora oferecem suporte a variáveis e segredos definidos pelo cliente.
Consulte Variáveis [de](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) pipeline para obter mais detalhes.

### Correções de erros {#bug-fixes-cm}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de desibernar/hibernar para ambientes do Programa de sandbox.

* As opções **Cancelar** e **Salvar** nem sempre estavam visíveis na página de edição do pipeline de não produção.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Às vezes, o nome sugerido na criação de um novo programa retornava um duplicado de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e do Dispatcher sem que estivessem presentes.

### Problemas conhecidos {#known-issues}

* Devido a uma mudança na forma como a cobertura de código é calculada, a versão _mínima_ do plug-in Jacoco agora é 0.7.5.201505241946 (lançado em maio de 2015). Os clientes que referenciarem explicitamente uma versão mais antiga receberão uma mensagem de erro no processo de qualidade do código.

## Novidades do Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Siga esta seção para saber mais sobre as novidades e as atualizações do Cloud Readiness Analyzer versão v1.0.2.

### Correções de erros {#cra-bug-fixes}

* Não foi possível executar a versão anterior do CRA no Adobe Experience Manager (AEM) 6.1. Foi adicionado suporte direto para permitir usuários no grupo de administradores.

   Consulte [Instalação do CRA no AEM 6.1](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) para obter mais detalhes.

* O carimbo de data e hora de expiração exibido no relatório de resumo estava incorreto.

* O CRA estava detectando componentes personalizados duplicados.

* No AEM 6.1, a inspeção de conteúdo era encerrada antes de concluir a inspeção completa. Adição de um gerenciamento de exceções para permitir que o inspetor pule e continue até que a inspeção completa seja concluída.

