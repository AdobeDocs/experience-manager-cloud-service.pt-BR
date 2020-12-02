---
title: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.7.0
description: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.7.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 73%

---


# Notas de versão do Cloud Manager no Adobe Experience Manager como Cloud Service 2020.7.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager em AEM como Cloud Service 2020.7.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.7.0 é 9 de julho de 2020.

## Novidades {#whats-new-cloud-manager}

* A página de ambientes foi renovada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O número de variáveis por ambiente aumentou para 200.

* Os pipelines do Cloud Manager agora oferecem suporte a variáveis e segredos definidos pelo cliente.

   Consulte [Variáveis de pipeline](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables) para saber mais.

* Agora há suporte para Repositórios de Maven Privado com vínculo de autenticação.

* O container de build do Cloud Manager agora é compatível com Java 8 e Java 11.
Consulte [Usando o suporte Java 11](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support) para obter mais detalhes.

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

* Devido a uma mudança na forma como a cobertura de código é calculada, a versão *mínima* do plug-in Jacoco agora é a 0.7.5.201505241946 (lançada em maio de 2015). Os clientes que indicarem uma versão mais antiga receberão uma mensagem de erro no processo de qualidade do código.