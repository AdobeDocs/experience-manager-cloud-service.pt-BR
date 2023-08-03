---
title: Programas e tipos de programas
description: Saiba mais sobre a hierarquia do Cloud Manager e como os diferentes tipos de programas se encaixam em sua estrutura e a diferença entre eles.
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: fc14675e47e7a61bf36acb9a16756a593189b702
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 88%

---


# Programas e tipos de programas {#understanding-programs}

O Cloud Manager é construído com base em uma hierarquia de entidades. Os detalhes disso não são essenciais para o seu trabalho diário no Cloud Manager, mas ter uma visão geral ajudará você a entender os programas e configurar os seus próprios programas.

![Hierarquia do Cloud Manager](assets/program-types1.png)

* **LOCATÁRIO** - Esse é o topo da hierarquia. Cada cliente recebe um locatário.
* **PROGRAMAS** - cada locatário tem um ou mais programas, [que geralmente refletem as soluções licenciadas do cliente.](introduction-production-programs.md)
* **AMBIENTES** - cada programa tem vários ambientes, um de produção para conteúdo dinâmico, um para preparo e outro para fins de desenvolvimento.
   * Cada programa pode ter apenas um ambiente de produção, mas pode ter vários ambientes de não produção.
* **REPOSITÓRIO** - Os programas têm repositórios Git, nos quais o código do aplicativo e do front-end são mantidos para os ambientes.
* **FERRAMENTAS E FLUXOS DE TRABALHO** - Pipelines gerenciam a implantação de código dos repositórios nos ambientes, enquanto que outras ferramentas permitem o acesso a registros, monitoramento e gerenciamento do ambiente.

Geralmente, um exemplo é útil na contextualização dessa hierarquia.

* A WKND Travel and Adventure Enterprises pode ser um **locatário** que se concentra em mídias relacionadas a viagens.
* O locatário da WKND Travel and Adventure Enterprises pode ter dois **programas**: um programa Sites para a WKND Magazine e um programa Assets para a WKND Media.
* Os programas da WKND Magazine e WKND Media teriam **ambientes** de desenvolvimento, preparação e produção.

## Repositório de código-fonte {#source-code-repository}

Um programa do Cloud Manager será provisionado automaticamente com seu próprio repositório Git.

Para acessar o repositório Git do Cloud Manager, os usuários precisarão usar um cliente Git com uma ferramenta de linha de comando, um cliente Git visual independente ou um IDE de escolha do usuário, como Eclipse, IntelliJ ou NetBeans.

Depois que um cliente Git é configurado, você pode gerenciar seu repositório Git na interface do Cloud Manager. Para saber mais sobre como gerenciar o Git usando a interface do Cloud Manager, consulte [Acesso ao Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

Para começar a desenvolver o aplicativo do AEM Cloud, é necessário fazer uma cópia local do código do aplicativo movendo-o do repositório do Cloud Manager para um local no computador.

```java
$ git clone {URL}
```

Portanto, trata-se de um fluxo de trabalho Git padrão.

1. O usuário clona uma cópia local do repositório Git.
1. O usuário faz alterações no repositório de código local.
1. Quando termina, o usuário confirma as alterações no repositório Git remoto.

A única diferença é que o repositório Git remoto faz parte do Cloud Manager, que é transparente para o desenvolvedor.

## Tipos de programas {#program-types}

Um usuário pode criar um **produção** programa ou um **sandbox** programa.

* Um **programa de produção** é criado para permitir o tráfego direto em seu site.
   * Consulte [Introdução aos programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obter mais detalhes.
* Um **programa de sandbox** é normalmente criado para fins de treinamento, execução de demonstrações, capacitação, POCs ou documentação.
   * Um ambiente de sandbox não se destina a transportar tráfego direto e terá restrições que um programa de produção não terá.
   * Ele inclui Sites e Ativos e é fornecido preenchido automaticamente com uma ramificação Git que inclui código de amostra, um ambiente de desenvolvimento e um pipeline de não produção.
   * Consulte [Introdução aos programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) para obter mais detalhes.
