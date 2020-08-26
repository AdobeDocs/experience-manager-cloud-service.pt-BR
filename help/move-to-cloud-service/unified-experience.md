---
title: Experiência unificada para ferramentas de refatoração de código
description: Experiência unificada para ferramentas de refatoração de código
translation-type: tm+mt
source-git-commit: 03434343829e1a1fb95256a607619b55626c6afc
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 1%

---


# Experiência unificada para ferramentas de refatoração de código {#unified-experience}

Desenvolvemos ferramentas para automatizar algumas das tarefas de refatoração de código necessárias para serem compatíveis com AEM como Cloud Service. Para reduzir a complexidade associada à instalação e configuração de diferentes ferramentas de refatoração de código, desenvolvemos um plug-in para unificar as ferramentas que operam em código e repositórios.

## Benefits {#benefits}

O plug-in Experiência unificada oferece os seguintes benefícios:

* Unifica as ferramentas que funcionam no código fonte em um `node.js` aplicativo exposto como `aio-cli ` plug-in para fornecer uma experiência do usuário consistente ao usuário.

* Fornece a capacidade de executar todas as ferramentas por meio de um único comando, além de fornecer a flexibilidade para executar ferramentas específicas, conforme necessário.

* Fornece extensibilidade para simplificar a adição de novas ferramentas, além de manter a experiência consistente.

## Como entender o plug-in {#understanding-plugin}

O `aio-cli-plugin-aem-cloud-service-migration` plug-in consiste em duas partes principais:

* **Interface do usuário**

   * `aio-cli` comandos para executar uma ou mais ferramentas de refatoração de código (por meio do encadeamento das ferramentas a serem executadas sequencialmente)
   * `config.yaml` que utiliza os parâmetros de entrada necessários

* **Conjunto de ferramentas de refatoração de código subjacente**

   As ferramentas de refatoração de código executam suas funcionalidades:

   * Analisar a seção respectiva do código do cliente e manipular o código (com base na implementação do código para as práticas recomendadas) para produzir a saída que pode ser validada e implantada.

   * Produzir um relatório de resumo para registrar as operações executadas durante a execução.

## Disponibilidade {#availability}

Consulte Recurso [Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para saber mais sobre o uso e como você pode contribuir para esse código de plug-in que é open-source no GitHub.

>[!NOTE]
>Atualmente, apenas o Dispatcher Converter está integrado ao plug-in.
