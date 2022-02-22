---
title: Programas e tipos de programas
description: Saiba mais sobre a hierarquia do Cloud Manager e como os diferentes tipos de programas se encaixam em sua estrutura e como são diferentes.
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: 74e17ccb93c97dd6881c9b63d9a2d784d3add430
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# Programas e tipos de programas {#understanding-programs}

O Cloud Manager é construído em torno de uma hierarquia de entidades. Os detalhes disso não são essenciais para o seu trabalho diário no Cloud Manager, mas uma visão geral ajudará você a entender os programas e configurar os seus próprios.

![Hierarquia do Cloud Manager](assets/program-types1.png)

* **CONTENTOR** - Este é o topo da hierarquia. Todos os clientes são provisionados com um locatário.
* **PROGRAMAS** - Cada locatário tem um ou mais programas, [que refletem frequentemente as soluções licenciadas do cliente.](introduction-production-programs.md)
* **AMBIENTES** - Cada programa tem vários ambientes, como produção para conteúdo ao vivo, um para preparo e outro para fins de desenvolvimento.
   * Cada programa pode ter apenas um ambiente de produção, mas vários ambientes não relacionados à produção.
* **REPOSITÓRIO** - Os programas têm repositórios git, onde o aplicativo e o código front-end são mantidos para os ambientes.
* **FERRAMENTAS E FLUXOS DE TRABALHO** - Pipelines gerencia a implantação do código dos repositórios para os ambientes, enquanto outras ferramentas permitem acesso a logs, monitoramento e gerenciamento de ambiente.

Um exemplo geralmente é útil na contextualização dessa hierarquia.

* A WKND Travel and Adventure Enterprise pode ser uma **inquilino** que se concentra em mídia relacionada a viagens.
* O locatário da WKND Travel and Adventure Enterprises pode ter dois **programas**: programa one Sites para a WKND Magazine e um programa Assets para a WKND Media.
* Os programas WKND Magazine e WKND Media teriam desenvolvimento, estágio e produção **ambientes**.

## Repositório de código-fonte {#source-code-repository}

Um programa do Cloud Manager será fornecido automaticamente com seu próprio repositório Git.

Para acessar o repositório Git do Cloud Manager, os usuários precisarão usar um cliente Git com uma ferramenta de linha de comando, um cliente Git visual independente ou o IDE do usuário preferido, como Eclipse, IntelliJ ou NetBeans.

Depois que um cliente Git é configurado, você pode gerenciar seu repositório Git na interface do usuário do Cloud Manager. Para saber mais sobre como gerenciar o git usando a interface do usuário do Cloud Manager, consulte o documento [Acesso ao Git.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

Para começar a desenvolver o aplicativo AEM Cloud, uma cópia local do código do aplicativo deve ser feita verificando-o do repositório do Cloud Manager para um local no computador local.

```java
$ git clone {URL}
```

O workflow é, portanto, um workflow git padrão.

1. Um usuário clona uma cópia local do repositório Git.
1. O usuário faz alterações no repositório de código local.
1. Quando pronto, o usuário confirma as alterações no repositório Git remoto.

A única diferença é que o repositório Git remoto faz parte do Cloud Manager, que é transparente para o desenvolvedor.

## Tipos de programas {#program-types}

Um usuário pode criar um **produção** ou **sandbox** programa.

* A **programa de produção** é criado para ativar o tráfego ao vivo em seu site.
   * Consulte o documento [Introdução aos programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) para obter mais detalhes.
* A **programa sandbox** O é normalmente criado para servir os propósitos de treinamento, execução de demonstrações, ativação, POCs ou documentação.
   * Um ambiente de caixa de proteção não é destinado a transportar tráfego ao vivo e terá restrições que um programa de produção não irá.
   * Ele incluirá Sites e Ativos e será fornecido automaticamente com uma ramificação git que inclui código de amostra, um ambiente de desenvolvimento e um pipeline de não produção.
   * Consulte o documento [Introdução aos programas de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) para obter mais detalhes.
