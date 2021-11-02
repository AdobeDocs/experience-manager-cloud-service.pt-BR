---
title: Pipelines de CI-CD
description: Pipelines de CI-CD
index: false
source-git-commit: 1887cc7374ece840b2dcca4482924b14c4793567
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Pipelines CI-CD do Cloud Manager {#intro-cicd}

## Introdução {#introduction}

Um pipeline de CI/CD no Cloud Manager pode ser acionado por algum tipo de evento, como uma solicitação de pull de um repositório de código fonte, ou seja, uma alteração de código ou algum tipo de agendamento regular para corresponder a uma cadência de lançamento.

>[!NOTE]
>Para configurar o pipeline, você deve:
>* defina o acionador que iniciará o pipeline
>* defina os parâmetros que controlam a implantação de produção
>* configurar os parâmetros de teste de desempenho


No Cloud Manager, há dois tipos de pipeline:

* [Pipeline de produção](#prod-pipeline)
* [Pipeline de não produção](#non-prod-pipeline)

## Pipeline de produção {#prod-pipeline}

Um pipeline de produção é um pipeline criado para a finalidade que inclui uma série de etapas orquestradas para levar o código fonte até a produção. As etapas incluem a criação, o empacotamento, o teste, a validação e a implantação em todos os ambientes de Preparo primeiro. Escusado será dizer que um Pipeline de produção só poderá ser adicionado depois que um conjunto de ambientes de produção e preparo for criado.

Consulte Configuração do pipeline de produção para obter mais detalhes.


## Pipeline de não produção {#non-prod-pipeline}

Um pipeline de não-produção tem como objetivo executar verificações de qualidade de código ou implantar o código-fonte em um ambiente de desenvolvimento.

Consulte Pipelines de não produção e de qualidade de código somente para obter mais detalhes.
