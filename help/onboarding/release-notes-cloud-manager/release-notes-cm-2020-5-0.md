---
title: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.5.0
description: Notas de versão do Cloud Manager no AEM como Cloud Service versão 2020.5.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 71%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.5.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager em AEM como Cloud Service 2020.5.0.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM como Cloud Service 2020.5.0 é 7 de maio de 2020.

## Novidades {#whats-new-cloud-manager}

* Seis regras adicionais de qualidade de código foram adicionadas para ajudar os clientes a identificar possíveis problemas ao planejar uma migração para o Cloud Service.
* Foi adicionada uma nova métrica *Compatibilidade com o Cloud Service* para resumir o número de problemas relacionados à compatibilidade.
* Ambientes com falha de criação agora serão excluídos automaticamente cerca de 24 horas após o evento de falha, a não ser que já tenham sido excluídos.
* O desempenho da página Atividade e da API de Lista de execuções de pipeline foi aprimorado.
* O log de qualidade do código agora contém rastreamentos completos de pilha para exceções.

### Correções de erros {#bug-fixes}

* Um cartão enganoso era exibido na página de visão geral enquanto o pipeline de produção estava em execução.
* A regra de qualidade de código *DontImplementOrExtendProviderTypesPomCheck* pode, às vezes, produzir uma Exceção de ponteiro nulo.
* Alguns links de documentação da página de visão geral não funcionavam corretamente.
* A caixa de diálogo Criar ambiente não era renderizada corretamente no Safari.
* Determinados cartões na página de visão geral não exibiam os nomes de entidades corretamente.
* Em alguns casos, a etapa Criar imagem não baixava pacotes de clientes com êxito.
