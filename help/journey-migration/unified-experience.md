---
title: Experiência unificada para ferramentas de refatoração de código
description: Saiba mais sobre a experiência unificada para ferramentas de refatoração de código.
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# Experiência unificada para ferramentas de refatoração de código {#unified-experience}

O Adobe desenvolveu ferramentas para automatizar algumas das tarefas de refatoração de código necessárias para ser compatível com o Adobe Experience Manager (AEM) as a Cloud Service. Para reduzir a complexidade associada à instalação e configuração de diferentes ferramentas de refatoração de código, o Adobe desenvolveu um plug-in para unificar ferramentas que operam em código e repositórios.

## Benefícios {#benefits}

O plug-in de Experiência unificada oferece os seguintes benefícios:

* Unifica ferramentas que funcionam no código-fonte em uma só `node.js` aplicativo exposto como `aio-cli ` para fornecer uma experiência consistente ao usuário.

* Executa todas as ferramentas por meio de um único comando, ao mesmo tempo em que fornece a flexibilidade para executar ferramentas específicas conforme necessário.

* Simplifica a adição de novas ferramentas, mantendo a experiência consistente.

## Compreender o plug-in {#understanding-plugin}

A variável `aio-cli-plugin-aem-cloud-service-migration` O plug-in do consiste em duas partes principais:

* **Interface do usuário**

   * `aio-cli` comandos para executar uma ou mais ferramentas de refatoração de código (por meio do encadeamento das ferramentas a serem executadas sequencialmente).
   * `config.yaml` que assume os parâmetros de entrada necessários.

* **Conjunto de ferramentas de refatoração de código subjacente**

  As ferramentas de refatoração de código executam suas funcionalidades ao:

   * Digitalizar a respectiva seção do código do cliente e manipular o código (com base na implementação do código para práticas recomendadas) para produzir a saída que pode ser validada e implantada.

   * Produzir um relatório de resumo para registrar as operações realizadas durante a execução.

## Disponibilidade {#availability}

Consulte [Recurso do Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) onde você pode saber mais sobre o uso e como contribuir para esse código de plug-in de código aberto no GitHub.

>[!NOTE]
>Atualmente, o plug-in está integrado ao AEM Dispatcher Converter e ao Repository Modernizer.
