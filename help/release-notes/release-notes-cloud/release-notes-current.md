---
title: Notas de versão do Adobe Experience Manager as a Cloud Service para 2020.5.0
description: Notas de versão do Experience Manager para 2020.5.0
translation-type: tm+mt
source-git-commit: 8fe1f6f1c7c6a608ee1ca42836ee91e83487428d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 18%

---


# Notas de versão para AEM as a Cloud Service 2020.5.0{#release-notes}

A seção a seguir descreve as Notas de versão gerais para Experience Manager as a Cloud Service 2020.5.0.

## Data de lançamento {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.5.0 is May 07, 2020.

## What&#39;s New in AEM Sites {#aem-sites}

Siga esta seção para saber mais sobre as novidades e as atualizações do AEM Sites no AEM como uma versão 2020.5.0 do serviço de nuvem.

* As informações detalhadas sobre a tarefa agora estão disponíveis após o processamento de movimentações e roll-outs de página em massa como trabalhos assíncronos.
* Ao copiar/colar uma árvore de página, agora você se oferece para escolher entre colar somente a página raiz ou também as subpáginas da árvore.
* Os Fragmentos de experiência do AEM exportados para espaços de trabalho do Adobe Público alvo agora aparecem como tipos de oferta exclusivos e fontes de oferta no Público alvo.
* MSM - o uso do acionador de *publicação* agora encerra com êxito eventos de exclusão para componentes na fonte de cópia ativa, ou seja, a exclusão de componentes em uma live copy que foram excluídos na fonte de live copy.
* MSM - componentes de live copy estão sendo renomeados para *_msm_movidos* após a mesma implementação de componente da fonte de live copy.


## Novidades do Cloud Manager {#cloud-manager}

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

