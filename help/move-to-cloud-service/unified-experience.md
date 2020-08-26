---
title: Experiência unificada para ferramentas de refatoração de código
description: Experiência unificada para ferramentas de refatoração de código
translation-type: tm+mt
source-git-commit: c00b10b4d564e05099740b9ff991624db4f37a3d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Experiência unificada para ferramentas de refatoração de código {#unified-experience}

Várias ferramentas com diferentes pontos de interação para os clientes criam uma experiência desarticulada e aumentam a complexidade do uso de ferramentas, com cada uma tendo diferentes requisitos de execução em termos de instalação, configuração e execução.

## Benefits {#benefits}

A Unified Experience for Code Refactoring Tools chama e executa todas as ferramentas de refatoração de código que funcionam no código-fonte a partir do mesmo local.

A Experiência unificada para ferramentas de refatoração de código junto com os repositórios companheiros permite:

* Unifique todas as ferramentas que funcionam na migração de código-fonte em um único `node.js` aplicativo exposto `aio-cli plugin` para fornecer uma experiência do usuário consistente.

* Provisionamento para executar a migração geral por meio de um único comando, além de oferecer flexibilidade para executar uma ferramenta específica conforme o requisito.

* Simplifique a futura adição de novas ferramentas, como a adição de uma nova ferramenta ao plug-in, deve simplesmente exigir a adição de um novo comando para o desenvolvedor e uma simples atualização do plug-in para o usuário, de modo que a experiência permaneça consistente com mais valor agregado.

### Como entender o design do aplicativo

Essas ferramentas unificam todas as ferramentas de refatoração de código em um aplicativo node.js exposto `aio-cli plugin` para fornecer uma experiência consistente ao usuário.

O plug-in consiste em duas partes principais:

* **Interface do usuário**

   `aio-cli` comandos para executar uma ou mais ferramentas de migração (por meio do encadeamento das ferramentas a serem executadas sequencialmente)`config.yaml` que utilizam os parâmetros de entrada necessários

* **Conjunto de ferramentas de migração subjacente**

   As ferramentas de migração executam suas funcionalidades:

   * Analisar a seção respectiva do código do cliente e executar a migração (com base na implementação do código para práticas recomendadas) para produzir a saída que pode ser validada e implantada.

   * Gravando as operações executadas durante a migração, em uma ordem consistente para produzir um relatório de resumo.

## Uso do plug-in {#using-plugin}

O `aio-cli-plugin-aem-cloud-service-migration` reformata o código do cliente, a estrutura do repositório ou as configurações na máquina local do cliente. Esta página captura os requisitos detalhados e as decisões de design para a experiência unificada.
Está disponível como um código aberto para a comunidade se estender para casos de uso personalizados.

## Disponibilidade {#availability}

Você pode instalar e usar o `aio-cli-plugin-aem-cloud-service-migration` via `aio-cli` (atualmente integrado apenas ao conversor de despachante).

Consulte Recurso [Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para saber mais sobre o uso e como você pode contribuir para essa ferramenta.

O código de plug-in foi aberto e está disponível no Github.

