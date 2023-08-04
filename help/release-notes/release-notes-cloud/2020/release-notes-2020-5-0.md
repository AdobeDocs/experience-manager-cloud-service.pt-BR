---
title: Notas de versão do Adobe Experience Manager as a Cloud Service 2020.5.0
description: "[!DNL Adobe Experience Manager] Notas de versão as a Cloud Service para 2020.5.0."
exl-id: 8570d2c3-6d55-4914-94b2-f5d162e0c285
source-git-commit: 9ceec0401b91bba2408bda89d4f2c486e2d51eec
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 98%

---

# Notas de versão do AEM as a Cloud Service 2020.5.0 {#release-notes}

Esta página descreve as Notas de versão gerais do Experience Manager as a Cloud Service 2020.5.0.

## Data de lançamento {#release-date}

A data de lançamento do [!DNL Experience Manager] as a Cloud Service 2020.5.0 é quinta-feira, 7 de maio de 2020.

## Novidades no AEM Sites {#aem-sites}

Consulte esta seção para saber mais sobre as novidades e atualizações do AEM Sites no AEM as a Cloud Service, versão 2020.5.0.

* Informações detalhadas sobre trabalhos agora estão disponíveis após o processamento de movimentações e implantações de página em massa como trabalhos assíncronos.
* Ao copiar/colar uma árvore de páginas, agora é possível optar entre colar somente a página raiz ou também as subpáginas da árvore.
* Fragmentos de experiência do AEM exportados para espaços de trabalho do Adobe Target agora aparecem como tipos de ofertas exclusivos e fontes de ofertas no Target.
* MSM - o uso do acionador *publicar* agora implanta com êxito eventos de exclusão para componentes na origem da cópia ativa, ou seja, excluindo componentes em uma cópia ativa que foram excluídos nessa origem de cópia ativa.
* MSM - componentes de cópia ativa agora são renomeados para *_msm_moved* após a implantação do mesmo componente a partir da origem de cópia ativa.


## Novidades do Cloud Manager {#cloud-manager}

Consulte esta seção para saber mais sobre as novidades e atualizações do Cloud Manager no AEM as a Cloud Service, versão 2020.5.0.

### Novidades {#what-is-new}

* Seis regras adicionais de qualidade de código foram adicionadas para ajudar os clientes a identificar possíveis problemas ao planejar uma migração para o Cloud Service.
* Foi adicionada uma nova métrica *Compatibilidade com o Cloud Service* para resumir o número de problemas relacionados à compatibilidade.
* Ambientes com falha de criação agora serão excluídos automaticamente cerca de 24 horas após o evento de falha, a não ser que já tenham sido excluídos.
* O desempenho da página Atividade e da API de Lista de execuções de pipeline foi aprimorado.
* O log de qualidade do código agora contém rastreamentos completos de pilha para exceções.

### Correções de erros  {#bug-fixes}

* Um cartão enganoso era exibido na página de visão geral enquanto o pipeline de produção estava em execução.
* A regra de qualidade de código *DontImplementOrExtendProviderTypesPomCheck* pode, às vezes, produzir uma Exceção de ponteiro nulo.
* Alguns links de documentação da página de visão geral não funcionavam corretamente.
* A caixa de diálogo Criar ambiente não era renderizada corretamente no Safari.
* Determinados cartões na página de visão geral não exibiam os nomes de entidades corretamente.
* Em alguns casos, a etapa Criar imagem não baixava pacotes de clientes com êxito.
