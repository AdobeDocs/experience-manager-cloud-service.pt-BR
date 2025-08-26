---
title: Introdução aos pipelines de CI/CD
description: Saiba mais sobre os pipelines de CI/CD do Cloud Manager e como eles podem ser usados para implantar seu código com eficiência.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d065397b874cc24fb7af53e1258520f3e8270c55
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 33%

---


# Pipelines de CI/CD do Cloud Manager {#intro-cicd}

Saiba mais sobre os pipelines de CI/CD (Integração contínua/entrega contínua) do Cloud Manager e como eles podem ser usados para implantar seu código com eficiência.

## Introdução aos pipelines de CI/CD {#introduction}

Um pipeline de CI/CD no Cloud Manager é um mecanismo para criar código a partir de um repositório de origem e implantá-lo em um ambiente. Um evento aciona um pipeline, como uma solicitação pull de um repositório de código-fonte, como o Git (ou seja, uma alteração de código). Ou pode ser acionado em uma programação regular para corresponder a uma cadência de lançamento.

Para configurar um pipeline, você deve fazer o seguinte:

* Defina o acionador que inicia o pipeline.
* Defina os parâmetros que controlam a implantação de produção.
* Configurar os parâmetros do teste de desempenho.

O Cloud Manager oferece dois tipos de pipelines:

* [Pipelines de produção](#prod-pipeline)
* [Pipelines de não produção](#non-prod-pipeline)

![Tipos de pipelines](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Pipelines de produção {#prod-pipeline}

Um pipeline de produção é um pipeline criado para fins específicos que inclui uma série de etapas orquestradas para implantar código-fonte para uso de produção. As etapas incluem a primeira compilação, empacotamento, teste, validação e implantação em todos os ambientes de preparo. Portanto, um pipeline de produção só pode ser adicionado depois que um conjunto de ambientes de produção e de preparo é criado.

>[!TIP]
>
>Consulte [Configurar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

## Pipelines de não produção {#non-prod-pipeline}

Um pipeline de não produção serve principalmente para executar verificações de qualidade do código ou implantar código-fonte em um ambiente de desenvolvimento.

>[!TIP]
>
>Consulte [Configurar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

## Fontes de código {#code-sources}

Os pipelines também podem diferir pelo tipo de código que implantam, além de ambientes de produção e não produção.

* **[Pipelines de pilha completa](#full-stack-pipeline)** - Implanta simultaneamente compilações de código de back-end e front-end contendo um ou mais aplicativos de servidor do AEM, juntamente com configurações HTTPD/Dispatcher.
* **[Configurar pipelines](#config-deployment-pipeline)** - Você pode implantar configurações rapidamente para recursos como encaminhamento de logs e tarefas de manutenção relacionadas à limpeza. Também inclui várias configurações de CDN (Content Delivery Network), como regras de filtro de tráfego, incluindo regras do Web Application Firewall (WAF). Além disso, você pode gerenciar transformações de solicitação e resposta, seletores de origem, redirecionamentos do lado do cliente, páginas de erro, chaves CDN, chaves de API de limpeza e autenticação básica. Consulte [Usar pipelines de configuração](/help/operations/config-pipeline.md) para obter detalhes.
* **[Pipelines de front-end](#front-end)** - Implante compilações de código de front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente.
* **[Pipelines de configuração no nível da Web](#web-tier-config-pipelines)** - Implanta configurações HTTPD/Dispatcher.

Esses tipos de pipeline são descritos detalhadamente mais adiante neste documento.

### Entender os pipelines de CI-CD no Cloud Manager {#understand-pipelines}

A tabela a seguir resume os pipelines disponíveis no Cloud Manager e seus usos.

| Tipo de pipeline | Implantação ou qualidade do código | código Source | Propósito | Notas |
| --- | --- | --- | --- | ---|
| Produção ou não produção | Implantação | Pilha completa | Implanta simultaneamente compilações de código back-end e front-end, juntamente com configurações HTTPD/Dispatcher | Usado quando o código de front-end deve ser implantado simultaneamente com o código de servidor do AEM. Usado quando os pipelines de front-end ou de configuração no nível da Web ainda não foram adotados. |
| Produção ou não produção | Implantação | Front-end | Implanta a compilação do código de front-end contendo um ou mais aplicativos de interface do usuário do lado do cliente | Suporta vários pipelines de front-end simultâneos<br>Muito mais rápido do que implantações de pilha completa. |
| Produção ou não produção | Implantação | Configuração no nível da Web | Implanta configurações HTTPD/Dispatcher | Implantações em minutos |
| Produção ou não produção | Implantação | Configuração | Implanta a [configuração para vários recursos](/help/operations/config-pipeline.md) relacionados às tarefas de manutenção de CDN, encaminhamento de logs e limpeza | Implantações em minutos |
| Não produção | Qualidade do código | Pilha completa | Executa verificações de qualidade do código de pilha completa sem uma implantação | Oferece suporte a vários pipelines |
| Não produção | Qualidade do código | Front-end | Executa verificações de qualidade do código de front-end sem uma implantação | Oferece suporte a vários pipelines |
| Não produção | Qualidade do código | Configuração no nível da Web | Executa verificações de qualidade do código em configurações do Dispatcher sem uma implantação | Oferece suporte a vários pipelines |

O diagrama a seguir ilustra as configurações de pipeline do Cloud Manager com o repositório de front-end único tradicional ou configurações de repositório de front-end independente.

![Configurações de pipeline do Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipelines de pilha completa {#full-stack-pipeline}

Os pipelines de pilha completa implantam código de back-end, código de front-end e configurações no nível da Web ao tempo de execução do AEM, tudo ao mesmo tempo.

* Código de back-end - Conteúdo imutável, como código Java, configurações OSGi, repoinit e conteúdo mutável
* Código de front-end - Recursos da interface do usuário do aplicativo, como JavaScript, CSS, fontes
* Configuração no nível da Web - Configurações HTTPD/Dispatcher

O pipeline de pilha completa representa um pipeline &quot;uber&quot;. Ela lida com tudo simultaneamente, além de permitir que os usuários implantem seu código de front-end ou configurações de Dispatcher separadamente. Essa implantação é feita por meio do pipeline de front-end e dos pipelines de configuração no nível da Web, respectivamente.

Código de front-end do pacote de pipelines de pilha completa (JavaScript/CSS) como [bibliotecas do cliente do AEM](/help/implementing/developing/introduction/clientlibs.md).

Os pipelines de pilha completa podem implantar configurações no nível da Web se um [pipeline de configuração no nível da Web](#web-tier-config-pipelines) não está configurado.

As restrições a seguir se aplicam.

* O usuário deve estar conectado na função **Gerente de implantação** para configurar ou executar pipelines.
* Somente pode haver um pipeline de pilha completa por ambiente.

Além disso, saiba como o pipeline de pilha completa se comporta se você optar por introduzir um [pipeline de configuração no nível da Web](#web-tier-config-pipelines).

* O pipeline de pilha completa para um ambiente ignora a configuração do Dispatcher se existir um pipeline de configuração no nível da Web correspondente.
* Se não existir um pipeline de configuração no nível da Web correspondente para o ambiente, o usuário poderá configurar o pipeline de pilha completa para incluir ou ignorar a configuração do Dispatcher.

Os pipelines de pilha completa podem ser pipelines de qualidade do código ou de implantação.

### Configurar pipelines de pilha completa {#configure-full-stack}

Consulte [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code).
Consulte [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

## Configuração de pipelines {#config-deployment-pipeline}

Usando um pipeline de configuração, você pode implantar configurações rapidamente para encaminhamento de logs, tarefas de manutenção relacionadas à limpeza e várias configurações de CDN, incluindo regras de filtro de tráfego (como regras do WAF (Firewall do Aplicativo Web)). Além disso, você pode gerenciar transformações de solicitação e resposta, seletores de origem, redirecionamentos do lado do cliente, páginas de erro, chaves CDN gerenciadas pelo cliente, chaves de API de limpeza e autenticação básica.

Consulte [Usar pipelines de configuração](/help/operations/config-pipeline.md) para obter uma lista abrangente de recursos com suporte e saber como gerenciar as configurações no repositório para que elas sejam implantadas corretamente.

### Configurar pipelines de configuração {#configure-config-deployment}

Consulte [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment).
Consulte [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment).

## Pipelines de front-end {#front-end}

O código de front-end é qualquer código que é servido como arquivos estáticos. Ele é separado do código de interface fornecido pelo AEM e pode incluir temas de site, SPAs definidos pelo cliente, SPAs comuns e outras soluções.

Os pipelines de front-end ajudam as equipes a agilizar o processo de design e desenvolvimento, permitindo uma implantação mais rápida do código de front-end, de forma assíncrona ao desenvolvimento de back-end. Esse pipeline dedicado implanta o JavaScript e o CSS na camada de distribuição do AEM como um tema, resultando em uma nova versão de tema, que pode ser referenciada a partir de páginas entregues pelo AEM.

>[!NOTE]
>
>Alguém com a função **Gerente de implantação** pode criar e executar vários pipelines de front-end simultaneamente.
>
>Existe, no entanto, um limite máximo de 300 pipelines por programa (entre todos os tipos).

Os pipelines de front-end podem ser pipelines de implantação ou de qualidade de código. 

### Antes de configurar pipelines de front-end {#before-start}

Antes de configurar os pipelines de front-end, revise a [Jornada de criação rápida de sites do AEM](/help/journey-sites/quick-site/overview.md) para obter um guia completo sobre a ferramenta simples de criação rápida de sites do AEM. Esta jornada ajuda a simplificar o desenvolvimento de front-end e permite personalizar o site rapidamente sem conhecimento de back-end no AEM.

### Configurar um pipeline de front-end {#configure-front-end}

Consulte [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline).
Consulte [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline).

### Desenvolver sites com o pipeline de front-end {#developing-with-front-end-pipeline}

Com os pipelines de front-end, é dada mais independência aos desenvolvedores de front-end e o processo de desenvolvimento pode ser acelerado.

Consulte [Desenvolver sites com o pipeline de front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) para saber como esse processo funciona, além de algumas considerações a serem feitas a fim de aproveitar ao máximo o potencial desse processo.

## Pipelines de configuração no nível da Web {#web-tier-config-pipelines}

Os pipelines de configuração no nível da Web permitem a implantação exclusiva da configuração HTTPD/Dispatcher no tempo de execução do AEM, desvinculando-a de outras alterações de código. É um pipeline simplificado que fornece aos usuários que desejam implantar somente as alterações de configuração do Dispatcher um meio mais rápido de fazê-lo em apenas alguns minutos.

>[!TIP]
>
>Os pipelines de configuração no nível da Web permitem armazenar a configuração da Web no mesmo local de origem ou em um local diferente do pipeline de pilha completa, dependendo do que melhor se adapta à estrutura do projeto.

As restrições a seguir se aplicam.

* Estar na versão `2021.12.6151.20211217T120950Z` ou mais recente do AEM para usar pipelines de configuração no nível da Web.
* [Aceite o modo flexível das ferramentas do Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para usar pipelines de configuração no nível da Web.
* É necessário estar conectado na função **Gerente de implantação** para configurar ou executar pipelines.
* Em um dado momento, somente pode haver um pipeline de configuração no nível da Web por ambiente.
* O usuário não pode configurar um pipeline de configuração no nível da Web quando seu pipeline de pilha completa correspondente está em execução.
* A estrutura de nível da Web deve seguir a estrutura do modo flexível, conforme definido no documento [Dispatcher na nuvem](/help/implementing/dispatcher/disp-overview.md#validation-debug).

Além disso, esteja ciente de como o [pipeline de pilha completa](#full-stack-pipeline) se comporta ao introduzir um pipeline no nível da Web.

* Se um pipeline de configuração no nível da Web não estiver definido para um ambiente, o usuário poderá optar por incluir ou ignorar a configuração do Dispatcher ao configurar o pipeline de pilha completa. Essa seleção é feita durante a execução e a implantação.
* Depois que um pipeline de configuração no nível da Web é configurado para um ambiente, seu pipeline de pilha completa correspondente (se existir) ignora a configuração do Dispatcher durante a execução e a implantação.
* Depois que um pipeline de configuração no nível da Web é excluído, seu pipeline de pilha completa correspondente é redefinido para implantar as configurações do Dispatcher durante a execução.

Os pipelines de configuração no nível da Web podem ser do tipo `Code quality` ou `Deployment`.

### Configurar pipelines no nível da Web {#configure-web-tier}

Consulte [Adicionar um pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment).
Consulte [Adicionar um pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment).

## Visão geral em vídeo dos tipos de pipeline {#video}

Para obter uma visão geral rápida dos tipos de pipelines, assista ao vídeo a seguir (2 minutos, 26 segundos).

>[!VIDEO](https://video.tv.adobe.com/v/342363)
