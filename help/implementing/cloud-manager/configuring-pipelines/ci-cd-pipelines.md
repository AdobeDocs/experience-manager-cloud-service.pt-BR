---
title: Pipelines de CI-CD
description: Pipelines de CI-CD
index: false
source-git-commit: b8b4d0b9e7e1dfc6809d2e193a2c2fd2438ecdb6
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Pipelines CI-CD do Cloud Manager {#intro-cicd}

No Cloud Manager, há dois tipos de pipeline:

* [Pipeline de produção](#prod-pipeline)
* [Pipeline de não produção](#non-prod-pipeline)

## Pipeline de produção {#prod-pipeline}

Um pipeline de produção é um pipeline criado para a finalidade que inclui uma série de etapas orquestradas para levar o código fonte até a produção. As etapas incluem a criação, o empacotamento, o teste, a validação e a implantação em todos os ambientes de Preparo primeiro. Escusado será dizer que um Pipeline de produção só poderá ser adicionado depois que um conjunto de ambientes de produção e preparo for criado.

>[!NOTE]
>Consulte Configuração do pipeline de produção para obter mais detalhes.


## Pipeline de não produção {#non-prod-pipeline}

Um pipeline de não-produção tem como objetivo executar verificações de qualidade de código ou implantar o código-fonte em um ambiente de desenvolvimento.

>[!NOTE]
>Consulte Pipelines de não produção e de qualidade de código somente para obter mais detalhes.

A implantação e a qualidade do código suportadas no pipeline de Produção e Não Produção no Cloud Manager são categorizadas em dois tipos diferentes:

* Front-End
* Pilha completa

A tabela a seguir resume os pipelines:


>[!NOTE]
>Um pipeline de CI/CD no Cloud Manager é acionado por um evento, como uma solicitação de pull de um repositório de código-fonte, ou seja, uma alteração de código ou um agendamento regular para corresponder a uma cadência de lançamento.
>
>Para configurar o pipeline, você deve:
>* defina o acionador que iniciará o pipeline
>* defina os parâmetros que controlam a implantação de produção
>* configurar os parâmetros de teste de desempenho