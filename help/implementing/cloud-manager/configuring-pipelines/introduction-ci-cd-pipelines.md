---
title: Pipelines de CI/CD
description: Saiba mais sobre os pipelines de CI/CD do Cloud Manager e como eles podem ser usados para implantar seu código com eficiência.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 3348662e3da4dad75b851d7af7251d456321a3ec
workflow-type: tm+mt
source-wordcount: '1368'
ht-degree: 100%

---


# Pipelines de CI/CD do Cloud Manager {#intro-cicd}

Saiba mais sobre os pipelines de CI/CD do Cloud Manager e como eles podem ser usados para implantar seu código com eficiência.

## Introdução {#introduction}

Um pipeline de CI/CD no Cloud Manager é um mecanismo para criar código a partir de um repositório de origem e implantá-lo em um ambiente. Um pipeline pode ser acionado por um evento, como uma solicitação pull de um repositório de código-fonte (ou seja, uma alteração de código), ou em um cronograma regular para corresponder a uma cadência de lançamento.

Para configurar um pipeline, você deve:

* Definir o acionador que iniciará o pipeline.
* Definir os parâmetros que controlam a implantação em produção.
* Configurar os parâmetros do teste de desempenho.

O Cloud Manager oferece dois tipos de pipelines:

* [Pipelines de produção](#prod-pipeline)
* [Pipelines de não produção](#non-prod-pipeline)

![Tipos de pipelines](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Visão geral do vídeo {#video}

Para obter uma visão geral rápida dos tipos de pipelines, assista a este vídeo curto.

>[!VIDEO](https://video.tv.adobe.com/v/342363)

## Pipelines de produção {#prod-pipeline}

Um pipeline de produção é um pipeline criado para fins específicos que inclui uma série de etapas orquestradas para implantar código-fonte para uso de produção. As etapas incluem a primeira compilação, empacotamento, teste, validação e implantação em todos os ambientes de preparo. Portanto, um pipeline de produção somente pode ser adicionado após a criação de um conjunto de ambientes de produção e de preparo.

>[!TIP]
>
>Consulte o documento [Configuração de um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) para obter mais detalhes.

## Pipelines de não produção {#non-prod-pipeline}

Um pipeline de não produção serve principalmente para executar verificações de qualidade do código ou implantar código-fonte em um ambiente de desenvolvimento.

>[!TIP]
>
>Consulte o documento [Configuração de um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para obter mais detalhes.

## Fontes de código {#code-sources}

Além de produção e não produção, os pipelines podem ser diferenciados pelo tipo de código que implantam.

* **[Pipelines de pilha completa](#full-stack-pipeline)** - Implanta simultaneamente compilações de código de back-end e front-end contendo um ou mais aplicativos de servidor do AEM, juntamente com configurações HTTPD/Dispatcher.
* **[Pipelines de front-end](#front-end)** - Implantam compilações de código de front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente.
* **[Pipelines de configuração no nível da Web](#web-tier-config-pipelines)** - Implanta configurações HTTPD/Dispatcher.

Elas são descritas em detalhes mais adiante neste documento.

### Noções básicas sobre os pipelines de CI-CD no Cloud Manager {#understand-pipelines}

A tabela a seguir resume todos os pipelines disponíveis no Cloud Manager e seus usos.

| Tipo de pipeline | Implantação ou qualidade do código | Código-fonte | Propósito | Notas |
|--- |--- |--- |---|---|
| Produção ou não produção | Implantação | Pilha completa | Implanta simultaneamente compilações de código back-end e front-end, juntamente com configurações HTTPD/Dispatcher | Quando o código de front-end deve ser implantado simultaneamente com o código de servidor do AEM.<br>Quando os pipelines de front-end ou de configuração no nível da Web ainda não tiverem sido adotados. |
| Produção ou não produção | Implantação | Front-end | Implanta a compilação do código de front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente | Suporta vários pipelines de front-end simultâneos <br>com muito mais rapidez do que implantações de pilha completa |
| Produção ou não produção | Implantação | Configuração no nível da Web | Implanta configurações HTTPD/Dispatcher | Implantações em minutos |
| Não produção | Qualidade do código | Pilha completa | Executa verificações de qualidade do código de pilha completa sem uma implantação | Oferece suporte a vários pipelines |
| Não produção | Qualidade do código | Front-end | Executa verificações de qualidade do código de front-end sem uma implantação | Oferece suporte a vários pipelines |
| Não produção | Qualidade do código | Configuração no nível da Web | Executa verificações de qualidade do código em configurações de dispatcher sem uma implantação | Oferece suporte a vários pipelines |

O diagrama a seguir ilustra as configurações de pipeline do Cloud Manager com o repositório de front-end único tradicional ou configurações de repositório de front-end independente.

![Configurações de pipeline do Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipelines de pilha completa {#full-stack-pipeline}

Os pipelines de pilha completa implantam código de back-end, código de front-end e configurações no nível da Web simultaneamente no tempo de execução do AEM.

* Código de back-end - Conteúdo imutável, como código Java, configurações OSGi, inicialização do repositório, bem como conteúdo mutável
* Código de front-end - Recursos da interface do usuário do aplicativo, como JavaScript, CSS, fontes
* Configuração no nível da Web - Configurações HTTPD/Dispatcher

O pipeline de pilha completa representa um pipeline “uber”, que faz tudo de uma vez, enquanto fornece aos usuários as opções para implantar exclusivamente seu código de front-end ou configurações do Dispatcher por meio do pipeline de front-end e dos pipelines de configuração no nível da Web, respectivamente.

Código de front-end do pacote de pipelines de pilha completa (JavaScript/CSS) como [bibliotecas de cliente do AEM.](/help/implementing/developing/introduction/clientlibs.md)

Os pipelines de pilha completa podem implantar configurações no nível da Web se um [pipeline de configuração no nível da Web](#web-tier-config-pipelines) não está configurado.

As restrições a seguir se aplicam.

* O usuário deve estar conectado na função **Gerente de implantação** para configurar ou executar pipelines.
* Em um dado momento, somente pode haver um pipeline de pilha completa por ambiente.

Além disso, saiba como o pipeline de pilha completa se comportará se você optar por introduzir um [pipeline de configuração no nível da Web.](#web-tier-config-pipelines)

* O pipeline de pilha completa para um ambiente ignorará a configuração do Dispatcher se existir um pipeline de configuração no nível da Web correspondente.
* Se não existir um pipeline de configuração no nível da Web correspondente para o ambiente, o usuário poderá configurar o pipeline de pilha completa para incluir ou ignorar a configuração do Dispatcher.

Os pipelines de pilha completa podem ser pipelines de qualidade do código ou de implantação.

## Pipelines de front-end {#front-end}

O código de front-end é qualquer código que é servido como arquivos estáticos. Ele é separado do código de interface do usuário fornecido pelo AEM e pode incluir temas de site, SPA definidas pelo cliente, SPAs Firefly e outras soluções.

Os pipelines de front-end ajudam as equipes a agilizar o processo de design e desenvolvimento, permitindo uma implantação mais rápida do código de front-end de forma assíncrona ao desenvolvimento de back-end. Esse pipeline dedicado implanta JavaScript e CSS na camada de distribuição do AEM como um tema, resultando em uma nova versão de tema que pode ser referenciada a partir de páginas entregues pelo AEM.

>[!IMPORTANT]
>
>Você deve usar o AEM versão `2021.10.5933.20211012T154732Z ` ou posterior com o AEM Sites habilitado para utilizar pipelines de front-end.

>[!NOTE]
>
>Um usuário com a função **Gerente de implantação** pode criar e executar vários pipelines de front-end simultaneamente.
>
>Existe, no entanto, um limite máximo de 300 pipelines por programa (entre todos os tipos).

Os pipelines de front-end podem ser pipelines de implantação ou de qualidade de código. 

### Antes de configurar os pipelines de front-end {#before-start}

Antes de configurar pipelines de front-end, revise a [Jornada de criação rápida de sites do AEM](/help/journey-sites/quick-site/overview.md) para obter um guia completo sobre a ferramenta simples de Criação rápida de sites do AEM. Essa jornada ajudará você a simplificar seu desenvolvimento de front-end e permitirá que você personalize rapidamente seu site sem conhecimento de back-end no AEM.

### Configurar um pipeline de front-end {#configure-front-end}

Para saber como configurar pipelines de front-end, consulte os documentos a seguir.

* [Adição de um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Configuração de um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### Desenvolvimento de Sites com o pipeline front-end {#developing-with-front-end-pipeline}

Com os pipelines de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ser acelerado.

Consulte o documento [Desenvolvimento de Sites com o pipeline de front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber como esse processo funciona, além de algumas considerações a serem feitas a fim de aproveitar ao máximo o potencial desse processo.

### Configuração de pipelines de pilha completa {#configure-full-stack}

Para saber como configurar pipelines de pilha completa, consulte os documentos a seguir.

* [Adição de um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Configuração de um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Pipelines de configuração no nível da Web {#web-tier-config-pipelines}

Os pipelines de configuração no nível da Web permitem a implantação exclusiva da configuração HTTPD/Dispatcher no tempo de execução do AEM, desvinculando-a de outras alterações de código. É um pipeline simplificado que fornece aos usuários que desejam implantar apenas as alterações de configuração do dispatcher um meio mais rápido de fazê-lo em apenas alguns minutos.

>[!TIP]
>
>Com os pipelines de configuração no nível da Web, você pode escolher entre armazenar a configuração da Web no mesmo local de origem do pipeline de pilha completa ou em um local diferente, dependendo de qual estrutura se adapta melhor ao seu projeto.

As restrições a seguir se aplicam.

* Você deve usar o AEM versão `2021.12.6151.20211217T120950Z` ou posterior para aproveitar os novos pipelines de front-end.
* Você deve [aceitar o modo flexível das ferramentas do dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para aproveitar os pipelines de configuração no nível da Web.
* O usuário deve estar conectado na função **Gerente de implantação** para configurar ou executar pipelines.
* Em um dado momento, somente pode haver um pipeline de configuração no nível da Web por ambiente.
* O usuário não pode definir um pipeline de configuração no nível da Web quando um pipeline de pilha completa correspondente está em execução.
* A estrutura de nível da Web deve seguir a estrutura do modo flexível, conforme definido no documento [Dispatcher na nuvem.](/help/implementing/dispatcher/disp-overview.md#validation-debug)

Além disso, esteja ciente de como o [pipeline de pilha completa](#full-stack-pipeline) se comportará ao introduzir um pipeline no nível da Web.

* Se um pipeline de configuração no nível da Web não tiver sido configurado para um ambiente, o usuário poderá fazer uma seleção ao configurar seu pipeline de pilha completa correspondente para incluir ou ignorar a configuração de Dispatcher durante a execução e a implantação.
* Depois que um pipeline de configuração no nível da Web é configurado para um ambiente, seu pipeline de pilha completa correspondente (se existir) ignorará a configuração do dispatcher durante a execução e a implantação.
* Depois que um pipeline de configuração no nível da Web é excluído, seu pipeline de pilha completa correspondente será redefinido para implantar configurações do Dispatcher durante a execução.

Os pipelines de configuração no nível da Web podem ser do tipo qualidade do código ou de implantação.

### Definição de pipelines de configuração no nível da Web {#configure-web-tier-config-pipelines}

Para saber como configurar pipelines de configuração no nível da Web, consulte os documentos a seguir.

* [Adição de um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Configuração de um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
