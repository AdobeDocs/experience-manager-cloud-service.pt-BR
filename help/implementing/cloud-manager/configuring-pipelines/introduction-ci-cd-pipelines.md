---
title: Pipelines de CI-CD
description: Siga esta página para saber mais sobre os pipeline de CI-CD do Cloud Manager
index: true
source-git-commit: 471924b2edd5e0bccd7c1eb9d6dd36ad2bd89f88
workflow-type: tm+mt
source-wordcount: '955'
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

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)


## Pipeline de produção {#prod-pipeline}

Um pipeline de produção é um pipeline criado para a finalidade que inclui uma série de etapas orquestradas para levar o código fonte até a produção. As etapas incluem a criação, o empacotamento, o teste, a validação e a implantação em todos os ambientes de Preparo primeiro. Escusado será dizer que um Pipeline de produção só poderá ser adicionado depois que um conjunto de ambientes de produção e preparo for criado.

Consulte [Configuração de um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) para obter mais detalhes.


## Pipeline de não produção {#non-prod-pipeline}

Um pipeline de não-produção tem como objetivo executar verificações de qualidade de código ou implantar o código-fonte em um ambiente de desenvolvimento.

Consulte [Configurar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para obter mais detalhes.

## Como entender os pipeline de CI-CD no Cloud Manager {#understand-pipelines}

A tabela a seguir resume todos os pipelines no Cloud Manager, juntamente com seu uso.

| Tipo de pipeline | Implantação ou qualidade do código | Código fonte | Quando usar | Quando ou Por que devo usar? |
|--- |--- |--- |---|---|
| Produção ou não produção | Implantação | Front-End | Tempos de implantação rápidos.<br>Vários pipelines de front-end podem ser configurados e executados simultaneamente por ambiente.<br>A build do pipeline Front-End envia a build para um armazenamento. Quando uma página html é disponibilizada, ela pode fazer referência a arquivos estáticos do Código do Front, que serão fornecidos pela CDN usando esse armazenamento como uma origem. | Para implantar exclusivamente o código front-end contendo um ou mais aplicativos da interface do usuário do cliente. O código front-end é qualquer código que é servido como um arquivo estático. É separado do código da interface do usuário fornecido pelo AEM. Inclui Temas do Sites, SPA definidas pelo Cliente, SPA do Firefly e quaisquer outras soluções.<br>Deve estar na AEM versão 2021.10.5933.20211012T154732Z |
| Produção ou não produção | Implantação | Pilha completa | Quando os gasodutos de front-end ainda não foram adotados.<br>Para casos em que o código Front-End deve ser implantado exatamente ao mesmo tempo que o código do Servidor de AEM. | Para implantar AEM código do Servidor (conteúdo imutável, código Java, configurações OSGi, configuração HTTPD/dispatcher, repontar, conteúdo mutável, fontes) - contendo um ou mais aplicativos AEM do servidor, todos ao mesmo tempo. |
| Não produção | Qualidade do código | Front-End | Para que o Cloud Manager seja avaliado. sucesso da build e qualidade do código sem fazer uma implantação.<br>Vários pipelines podem ser configurados e executados. | Execute verificações de qualidade de código no código front-end. |
| Não produção | Qualidade do código | Pilha completa | Para que o Cloud Manager seja avaliado. sucesso da build e qualidade do código sem fazer uma implantação.<br>Vários pipelines podem ser configurados e executados. | Execute a verificação de qualidade do código no código de pilha completo. |


O diagrama a seguir ilustra as configurações de pipeline do Cloud Manager com um repositório front-end único ou uma configuração de repositório front-end independente tradicional:

![](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipelines de Front-End do Cloud Manager {#front-end}

Os pipelines front-end ajudam suas equipes a simplificar seu processo de design e desenvolvimento, permitindo pipelines front-end acelerados para a implantação do código front-end. Esse pipeline diferenciado implanta JavaScript e CSS na camada de distribuição de AEM como um tema, resultando em uma nova versão de tema que pode ser referenciada das páginas entregues do tempo de execução de AEM. O código front-end é qualquer código que é servido como um arquivo estático. É separado do código da interface do usuário fornecido pelo AEM. Inclui Temas do Sites, SPA definidas pelo Cliente, SPA do Firefly e quaisquer outras soluções.

>[!IMPORTANT]
>Você deve estar AEM versão `2021.10.5933.20211012T154732Z ` para utilizar pipelines Front-End.

>[!NOTE]
>Um usuário conectado como função do Gerenciador de implantação pode criar e executar vários pipelines do front-end simultaneamente. Existe, no entanto, um limite máximo de 300 gasodutos por programa (em todos os tipos).

Elas podem ser do tipo Qualidade do código front-end ou pipelines de implantação front-end.

### Antes de configurar os pipelines do Front-End {#before-start}

Antes de começar a configurar os pipelines do Front-End, consulte [AEM Jornada de criação rápida de site](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) para um fluxo de trabalho completo por meio da ferramenta de criação rápida de sites AEM fácil de usar. Este site de documentação ajudará você a simplificar o desenvolvimento de front-end do seu site de AEM e personalizar rapidamente seu site sem conhecimento AEM de back-end.

### Configurar um pipeline front-end {#configure-front-end}

Para saber como configurar o pipeline front-end, consulte:

* [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

## Pipelines de pilha completa {#full-stack-pipeline}

O pipeline de Pilha cheia oferece ao usuário a opção de implantar configurações de back-end, front-end e HTTPD/dispatcher simultaneamente.  Ele implanta código e conteúdo no tempo de execução AEM incluindo código front-end (JavaScript/CSS) empacotado como Bibliotecas AEM clientes. Ele pode implantar a configuração da camada da Web se um pipeline da camada da Web não estiver configurado. Isso representa o pipeline &quot;uber&quot;, enquanto fornece aos usuários as opções para implantar exclusivamente seu código Front-End ou a configuração do dispatcher por meio do pipeline Front-End e do pipeline de Configuração de camada da Web, respectivamente.
Eles podem ser do tipo Pilha cheia - Qualidade do código ou Pilha cheia - pipeline de implantação.

As seguintes restrições serão aplicáveis:

1. Um usuário deve estar conectado como Gerenciador de Implantação para configurar ou executar pipelines.

1. A qualquer momento, só pode haver um pipeline de Pilha completa por ambiente.

1. O usuário pode configurar o pipeline de Pilha cheia para um ambiente para ignorar ou não ignorar a configuração do dispatcher. Se o pipeline de Configuração de camada da Web correspondente para o ambiente não existir.

1. O pipeline de Pilha completa para um ambiente ignorará a configuração do dispatcher se o pipeline de Configuração de camada da Web correspondente para o ambiente existir.


### Configurar um pipeline de pilha completo {#configure-full-stack}

Para saber como configurar o pipeline de pilha completa, consulte:

* [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)