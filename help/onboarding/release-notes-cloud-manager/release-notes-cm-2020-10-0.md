---
title: Notas de versão para 2020.10.0
description: Notas de versão para 2020.10.0
translation-type: tm+mt
source-git-commit: 9ed52fb3a9971bcaede71613774f653273a86530
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 60%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.10.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager em AEM como Cloud Service 2020.10.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.10.0 é 1 de outubro de 2020.

## Cloud Manager {#cloud-manager}

### Novidades {#what-is-new}

* A página Ambientes foi reprojetada.

* A página de ambientes hibernados agora mostra um status discreto no Cloud Manager.

* O container de build do Cloud Manager agora é compatível com Java 8 e Java 11.

* O número de variáveis por ambiente aumentou para 200.

* A placa de Ambiente na página Visão geral agora lista até três ambientes. Os usuários podem selecionar o botão **Mostrar tudo** para navegar até a página de resumo do Ambiente para visualização de uma tabela com uma lista completa de ambientes.
Consulte [Visualização de Ambientes](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obter mais detalhes.


### Correções de erros {#bug-fixes-cloud-manager}

* Devido a um erro, o link do Cloud Manager para o Console do desenvolvedor estava ativo antes dos ambientes serem totalmente criados.

* O link direto do Cloud Manager para o Console do desenvolvedor não exibia a opção de desibernar/hibernar para ambientes do Programa de sandbox.

* Os botões Cancelar e Salvar na página Edição de Pipeline de Não Produção nem sempre estavam visíveis.

* Certas falhas no processo de qualidade do código podiam resultar na geração incorreta do arquivo de log.

* Às vezes, o nome sugerido na criação de um novo programa retornava um duplicado de um nome de programa existente.

* Grandes logs de etapas de pipeline não podiam ser baixados consistentemente pela interface do usuário.

* A validação de nomes de ambientes apresentava um erro off-by-one.

* A página Ambientes às vezes mostrava segmentos do Publish e do Dispatcher sem que estivessem presentes.