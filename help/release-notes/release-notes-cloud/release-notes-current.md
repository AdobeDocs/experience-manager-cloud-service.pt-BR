---
title: Notas de versão do Adobe Experience Manager as a Cloud Service para 2020.5.0
description: Notas de versão do Experience Manager para 2020.5.0
translation-type: tm+mt
source-git-commit: 94a732f56929ad4af23855152e258f82ad61ee2c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 29%

---


# Notas de versão para AEM as a Cloud Service 2020.5.0{#release-notes}

A seção a seguir descreve as Notas de versão gerais para Experience Manager as a Cloud Service 2020.5.0.

## Cloud Manager {#cloud-manager}

Siga esta seção para saber mais sobre as novidades e atualizações do Cloud Manager no AEM as a Cloud Service versão 2020.5.0.

### Novidades {#what-is-new}

* Seis regras adicionais de qualidade de código foram adicionadas para ajudar os clientes a identificar possíveis problemas ao planejar uma migração para o Serviço da nuvem.
* Uma nova métrica de Compatibilidade *do serviço da* Cloud foi adicionada para resumir o número de problemas relacionados à compatibilidade.
* Ambientes que não foram criados serão excluídos automaticamente aproximadamente 24 horas após a criação falhar, a menos que já tenham sido excluídos.
* O desempenho da página de Atividade e da API de Lista de execuções de pipeline foi aprimorado.
* O log de qualidade do código agora contém rastreamentos completos de pilha para exceções.

### Correções de erros {#bug-fixes}

* Um cartão enganoso foi exibido na página de visão geral enquanto o pipeline de produção estava em execução.
* A regra de qualidade do código *DontImplantaçãoOrExtendProviderTypesPomCheck* pode, às vezes, produzir uma Exceção de Ponteiro Nulo.
* Alguns links de documentação da página de visão geral não funcionavam corretamente.
* A caixa de diálogo Criar Ambiente não foi renderizada corretamente no Safari.
* Determinados cartões na página de visão geral não exibiam os nomes das entidades corretamente.
* Em alguns casos, a Imagem de compilação falhava ao baixar os pacotes do cliente com êxito.

