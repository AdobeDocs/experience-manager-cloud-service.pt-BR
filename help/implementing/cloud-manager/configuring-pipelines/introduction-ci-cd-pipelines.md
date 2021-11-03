---
title: Pipelines de CI-CD
description: Pipelines de CI-CD
index: false
source-git-commit: 6d2f4aa11b3d23343b985b4871b6d7202e3181c7
workflow-type: tm+mt
source-wordcount: '805'
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

## Como entender os pipeline de CI-CD no Cloud Manager {#understand-pipelines}

A tabela a seguir resume todos os pipelines no Cloud Manager, juntamente com seu uso.

| Tipo de pipeline | Implantação ou qualidade do código | Código fonte | Quando usar | Quando ou Por que devo usar? |
|--- |--- |--- |---|---|---|
| Produção ou não produção | Implantação | Front-End | Para implantar o código front-end. O código front-end é qualquer código que é servido como um arquivo estático. É separado do código da interface do usuário fornecido pelo AEM. Inclui Temas do Sites, SPA definidas pelo Cliente, SPA do Firefly e quaisquer outras soluções. Deve estar AEM versão. | Tempos de implantação rápidos.<br> Vários pipelines de front-end podem ser configurados e executados simultaneamente por ambiente. |
|  | Implantação | Pilha completa | Para implantar configurações de back-end, front-end e HTTPD/dispatcher simultaneamente. Observação: Algumas restrições se aplicam. | Quando os pipelines de configuração do front-end ou da camada da Web ainda não foram adotados. |
|  | Implantação | Configuração da camada da Web | Para implantar exclusivamente a configuração HTTPD/dispatcher em uma questão de minutos.  Esse pipeline simplificado fornece aos usuários que desejam implantar apenas as alterações de configuração do dispatcher, um meio acelerado de fazê-lo. Observação: Deve estar em AEM versão [version] | Tempos de implantação rápidos. |


## Pipelines de Front-End do Cloud Manager {#front-end}

Os pipelines front-end ajudam suas equipes a simplificar seu processo de design e desenvolvimento, permitindo pipelines front-end acelerados para a implantação do código front-end. Esse pipeline diferenciado implanta JavaScript e CSS na camada de distribuição de AEM como um tema, resultando em uma nova versão de tema que pode ser referenciada das páginas entregues do tempo de execução de AEM. O código front-end é qualquer código que é servido como um arquivo estático. É separado do código da interface do usuário fornecido pelo AEM. Inclui Temas do Sites, SPA definidas pelo Cliente, SPA do Firefly e quaisquer outras soluções.

>[!NOTE]
>Um usuário conectado como função do Gerenciador de implantação pode criar e executar vários pipelines do front-end simultaneamente. Existe, no entanto, um limite máximo de 300 gasodutos por programa (em todos os tipos).

Há dois tipos de pipeline front-end:

* Qualidade do código front-end
* Implantação de front-end

### Antes de configurar os pipelines do Front-End {#before-start}

Antes de começar a configurar os pipelines do Front-End, consulte AEM Quick Site Creation Jornada para um workflow completo por meio da ferramenta fácil de usar AEM Quick Site Creation. Este site de documentação ajudará você a simplificar o desenvolvimento de front-end do seu site de AEM e personalizar rapidamente seu site sem conhecimento AEM de back-end.

### Configurar o pipeline de front-end {#configure-front-end}

Para saber como configurar o pipeline front-end, consulte:

* Adicionar um pipeline de produção
* Adicionar um pipeline de não produção

## Pipelines de pilha completa {#full-stack-pipeline}

O pipeline de Pilha cheia oferece ao usuário a opção de implantar configurações de back-end, front-end e HTTPD/dispatcher simultaneamente.  Ele implanta código e conteúdo no tempo de execução AEM incluindo código front-end (JavaScript/CSS) empacotado como Bibliotecas AEM clientes. Ele pode implantar a configuração da camada da Web se um pipeline da camada da Web não estiver configurado. Isso representa o pipeline &quot;uber&quot;, enquanto fornece aos usuários as opções para implantar exclusivamente seu código Front-End ou a configuração do dispatcher por meio do pipeline Front-End e do pipeline de Configuração de camada da Web, respectivamente.

As seguintes restrições serão aplicáveis:

1. Um usuário deve estar conectado como Gerenciador de Implantação para configurar ou executar pipelines.

1. A qualquer momento, só pode haver um pipeline de Pilha completa por ambiente.

1. O usuário pode configurar o pipeline de Pilha cheia para um ambiente para ignorar ou não ignorar a configuração do dispatcher. Se o pipeline de Configuração de camada da Web correspondente para o ambiente não existir.

1. O pipeline de Pilha completa para um ambiente ignorará a configuração do dispatcher se o pipeline de Configuração de camada da Web correspondente para o ambiente existir.

Há dois tipos de pipeline de pilha completa:

* Pipeline de qualidade do código de pilha completo
* Pipeline de implantação de pilha completa

### Configurar o pipeline de pilha completa {#configure-full-stack}

Para saber como configurar o pipeline de pilha completa, consulte:

* Adicionar um pipeline de produção
* Adicionar um pipeline de não produção