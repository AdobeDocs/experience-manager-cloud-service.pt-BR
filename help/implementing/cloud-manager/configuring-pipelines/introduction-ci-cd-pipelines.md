---
title: Pipelines de CI/CD
description: Saiba mais sobre os pipelines de CI/CD do Cloud Manager e como eles podem ser usados para implantar seu código com eficiência.
index: true
source-git-commit: d1fe713f0c35a96cf6ba3172ea11986fd9d42fd6
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 1%

---


# Pipelines de CI/CD do Cloud Manager {#intro-cicd}

Saiba mais sobre os pipelines de CI/CD do Cloud Manager e como eles podem ser usados para implantar seu código com eficiência.

## Introdução {#introduction}

Um pipeline de CI/CD no Cloud Manager é um mecanismo para criar código a partir de um repositório de origem e implantá-lo em um ambiente. Um pipeline pode ser acionado por um evento, como uma solicitação de pull de um repositório de código-fonte (ou seja, uma alteração de código), ou em um agendamento regular para corresponder a uma cadência de lançamento.

Para configurar um pipeline, você deve:

* Defina o acionador que iniciará o pipeline.
* Defina os parâmetros que controlam a implantação de produção.
* Configure os parâmetros do teste de desempenho.

O Cloud Manager oferece dois tipos de pipelines:

* [Pipelines de produção](#prod-pipeline)
* [Pipelines de não produção](#non-prod-pipeline)

![Tipos de gasodutos](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Pipelines de produção {#prod-pipeline}

Um pipeline de produção é um pipeline criado para fins específicos que inclui uma série de etapas orquestradas para implantar código fonte para uso de produção. As etapas incluem a primeira criação, empacotamento, teste, validação e implantação em todos os ambientes de preparo temporário. Portanto, um pipeline de produção só pode ser adicionado depois que um conjunto de ambientes de produção e de preparo é criado.

>[!TIP]
>
>Consulte o documento [Configuração de um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) para obter mais detalhes.

## Pipeline de não produção {#non-prod-pipeline}

Um pipeline de não produção serve principalmente para executar verificações de qualidade de código ou implantar o código fonte em um ambiente de desenvolvimento.

>[!TIP]
>
>Consulte o documento [Configurar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para obter mais detalhes.

## Fontes de código {#code-sources}

Além da produção e da não produção, os pipelines podem ser diferenciados pelo tipo de código que implantam.

* **[Pipelines de pilha completa](#full-stack-pipeline)** - Implante simultaneamente builds de código back-end e front-end contendo um ou mais aplicativos de servidor AEM juntamente com configurações HTTPD/Dispatcher
* **[Pipelines de front-end](#front-end)** - Implantar builds de código front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente
* **[Pipelines de configuração de camada da Web](#web-tier-config-pipelines)** - Implanta configurações HTTPD/Dispatcher

Elas são descritas detalhadamente mais adiante neste documento.

### Como entender os pipeline de CI-CD no Cloud Manager {#understand-pipelines}

A tabela a seguir resume todos os pipelines disponíveis no Cloud Manager e seus usos.

| Tipo de pipeline | Implantação ou qualidade do código | Código fonte | Propósito | Notas |
|--- |--- |--- |---|---|
| Produção ou não produção | Implantação | Pilha completa | Implanta simultaneamente builds de código back-end e front-end juntamente com configurações HTTPD/Dispatcher | Quando o código front-end deve ser implantado simultaneamente com AEM código de servidor.<br>Quando os pipelines de front-end ou os pipelines de configuração da camada da Web ainda não tiverem sido adotados. |
| Produção ou não produção | Implantação | Front-End | Implanta a build de código front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente | Suporta vários pipelines front-end simultâneos<br>Muito mais rápido que implantações em pilha completa |
| Produção ou não produção | Implantação | Configuração da camada da Web | Implanta configurações HTTPD/Dispatcher | Implantações em minutos |
| Não produção | Qualidade do código | Pilha completa | Executa verificações de qualidade de código no código de pilha completa sem uma implantação | Suporta vários pipelines |
| Não produção | Qualidade do código | Front-End | Executa verificações de qualidade de código no código front-end sem uma implantação | Suporta vários pipelines |
| Não produção | Qualidade do código | Configuração da camada da Web | Executa verificações de qualidade de código em configurações do dispatcher sem uma implantação | Suporta vários pipelines |

O diagrama a seguir ilustra as configurações de pipeline do Cloud Manager com o repositório front-end tradicional e único ou configurações de repositório front-end independente.

![Configurações do pipeline do Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipelines de pilha completa {#full-stack-pipeline}

Os pipelines de pilha completa implantam código back-end, código front-end e configurações de camada da Web para AEM o tempo de execução simultaneamente.

* Código de back-end - conteúdo imutável, como código Java, configurações OSGi, reponteiro, bem como conteúdo mutável
* Código front-end - recursos da interface do usuário do aplicativo, como JavaScript, CSS, fontes
* Configuração de camada da Web - Configurações HTTPD/Dispatcher

O pipeline de pilha completa representa um pipeline &quot;uber&quot;, fazendo tudo de uma vez, enquanto fornece aos usuários as opções para implantar exclusivamente seu código front-end ou configurações do Dispatcher por meio do pipeline front-end e dos pipelines de configuração da camada da Web, respectivamente.

Código front-end do pacote de pipelines de pilha completa (JavaScript/CSS) como [AEM bibliotecas de clientes.](/help/implementing/developing/introduction/clientlibs.md)

pipelines de pilha completa podem implantar configurações de camada da Web se um [pipeline de configuração de camada da web](#web-tier-config-pipelines) não está configurado.

As restrições a seguir se aplicam.

* Um usuário deve estar conectado com a variável **Gerenciador de implantação** para configurar ou executar pipelines.
* A qualquer momento, só pode haver um pipeline de pilha completa por ambiente.

Além disso, esteja ciente de como o pipeline de pilha completa se comportará se você optar por introduzir um [pipeline de configuração de camada da web.](#web-tier-config-pipelines)

* O pipeline de pilha completa para um ambiente ignorará a configuração do Dispatcher se o pipeline de configuração de camada da Web correspondente existir.
* Se o pipeline de configuração de camada da Web correspondente para o ambiente não existir, o usuário pode configurar o pipeline de pilha completa para incluir ou ignorar a configuração do Dispatcher.

Os pipelines de pilha completa podem ser pipelines ou implantação de qualidade do código.

## Pipelines de front-end {#front-end}

O código front-end é qualquer código que é servido como arquivos estáticos. Ele é separado do código da interface fornecido pelo AEM e pode incluir temas do site, SPA definidas pelo cliente, Firefly SPA e outras soluções.

Os pipelines de front-end ajudam as equipes a agilizar o processo de design e desenvolvimento, permitindo a implantação acelerada do código front-end assíncrono do desenvolvimento de back-end. Esse pipeline dedicado implanta JavaScript e CSS na camada de distribuição de AEM como um tema, resultando em uma nova versão de tema que pode ser referenciada a partir de páginas entregues pela AEM.

>[!IMPORTANT]
>
>Você deve estar AEM versão `2021.10.5933.20211012T154732Z ` ou superior com o AEM Sites habilitado para utilizar pipelines de front-end.

>[!NOTE]
>
>Um usuário com a **Gerenciador de implantação** pode criar e executar vários pipelines de front-end simultaneamente.
>
>Existe, no entanto, um limite máximo de 300 gasodutos por programa (em todos os tipos). Eles podem ser de qualidade de código front-end ou pipelines de implantação front-end.

Os pipelines de front-end podem ser pipelines ou implantação de qualidade do código.

### Antes de configurar os pipeline de front-end {#before-start}

Antes de configurar os pipelines de front-end, reveja o [AEM Jornada de criação rápida de site](/help/journey-sites/quick-site/overview.md) para obter um guia completo por meio da ferramenta fácil de usar AEM Quick Site Creation. Essa jornada ajudará você a simplificar seu desenvolvimento de front-end e permitirá que você personalize rapidamente seu site sem conhecimento AEM de back-end.

### Configurar um pipeline front-end {#configure-front-end}

Para saber como configurar pipelines de front-end, consulte os seguintes documentos.

* [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### Desenvolvimento de sites com o pipeline front-end {#developing-with-front-end-pipeline}

Com os pipelines de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ser acelerado.

Consulte o documento [Desenvolvimento de sites com o pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber como esse processo funciona, além de algumas considerações a serem levadas em conta, a fim de tirar todo o potencial desse processo.

### Configuração de pipeline de pilha completa {#configure-full-stack}

Para saber como configurar pipelines de pilha completa, consulte os seguintes documentos.

* [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Pipelines de configuração de camada da Web {#web-tier-config-pipelines}

Os pipelines de configuração da camada da Web permitem a implantação exclusiva da configuração HTTPD/Dispatcher no tempo de execução do AEM, dissociando-a de outras alterações de código. É um pipeline simplificado que fornece aos usuários que desejam implantar apenas as alterações de configuração do dispatcher, um meio acelerado de fazê-lo em apenas alguns minutos.

>[!TIP]
>
>Com os pipelines de configuração da camada da Web, você pode escolher entre armazenar a configuração da Web no mesmo local de origem do pipeline de pilha completo ou em um local diferente, dependendo de qual estrutura se adapta melhor ao seu projeto.

As restrições a seguir se aplicam.

* Você deve estar AEM versão `2021.12.6151.20211217T120950Z` ou mais recente para aproveitar os pipelines de configuração da camada da Web.
* Você deve [aceitar o modo flexível das ferramentas do dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para aproveitar os pipelines de configuração da camada da Web.
* Um usuário deve estar conectado com a variável **Gerenciador de implantação** para configurar ou executar pipelines.
* A qualquer momento, só pode haver um pipeline de configuração de camada da Web por ambiente.
* O usuário não pode configurar um pipeline de configuração de camada da Web quando seu pipeline de pilha completa correspondente está em execução.
* A estrutura da camada da Web deve aderir à estrutura do modo flexível, conforme definido no documento [Dispatcher na nuvem.](/help/implementing/dispatcher/disp-overview.md#validation-debug)

Além disso, esteja ciente de como a variável [pipeline de pilha completo](#full-stack-pipeline) se comportará ao introduzir um pipeline de camada da Web.

* Se um pipeline de configuração de camada da Web não tiver sido configurado para um ambiente, o usuário pode fazer uma seleção ao configurar seu pipeline de pilha completa correspondente para incluir ou ignorar a configuração do Dispatcher durante a execução e implantação.
* Depois que um pipeline de configuração de camada da Web é configurado para um ambiente, seu pipeline de pilha completa correspondente (se existir) ignorará a configuração do dispatcher durante a execução e implantação.
* Depois que um pipeline de configuração de camada da Web é excluído, seu pipeline de pilha completa correspondente será redefinido para implantar configurações do Dispatcher durante sua execução.

Os pipelines de configuração da camada da Web podem ser da qualidade do código do tipo ou da implantação.

### Configuração de pipeline de configuração de camada da Web {#configure-web-tier-config-pipelines}

Para saber como configurar pipelines de configuração da camada da Web, consulte os seguintes documentos.

* [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
