---
title: Experiência unificada para ferramentas de refatoração de código
description: Experiência unificada para ferramentas de refatoração de código
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Experiência unificada para ferramentas de refatoração de código {#unified-experience}

Desenvolvemos ferramentas para automatizar algumas das tarefas de refatoração de código necessárias para serem compatíveis com AEM as a Cloud Service. Para reduzir a complexidade associada à instalação e configuração de diferentes ferramentas de refatoração de código, desenvolvemos um plug-in para unificar ferramentas que operam em código e repositórios.

## Benefícios {#benefits}

O plug-in Unified Experience oferece os seguintes benefícios:

* Unifica ferramentas que funcionam no código-fonte em um `node.js` aplicativo exposto como `aio-cli ` para fornecer uma experiência do usuário consistente ao usuário.

* Fornece a capacidade de executar todas as ferramentas por meio de um único comando, além de fornecer a flexibilidade para executar ferramentas específicas, conforme necessário.

* Fornece extensibilidade para simplificar a adição de novas ferramentas, além de manter a experiência consistente.

## Como entender o plug-in {#understanding-plugin}

O `aio-cli-plugin-aem-cloud-service-migration` O plug-in consiste em duas partes principais:

* **Interface do usuário**

   * `aio-cli` comandos para executar uma ou mais ferramentas de refatoração de código (por meio do encadeamento das ferramentas a serem executadas sequencialmente).
   * `config.yaml` que utiliza os parâmetros de entrada necessários.

* **Conjunto de ferramentas de refatoração de código subjacente**

   As ferramentas de refatoração de código executam suas funcionalidades ao:

   * Analisar a respectiva seção do código do cliente e manipular o código (com base na implementação do código para práticas recomendadas) para produzir a saída que pode ser validada e implantada.

   * Produzir um relatório de resumo para registrar as operações executadas durante a execução.

## Disponibilidade {#availability}

Consulte [Recurso Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para saber mais sobre o uso e como você pode contribuir com esse código de plug-in de código aberto no GitHub.

>[!NOTE]
>Atualmente, o plug-in é integrado ao AEM Dispatcher Converter e ao Repository Modernizer.
