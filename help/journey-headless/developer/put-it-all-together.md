---
title: Como unir tudo - seu aplicativo e seu conteúdo em AEM
description: Nesta parte da Jornada de desenvolvedores sem cabeçalho do AEM, saiba como participar do Projeto de AEM, incluindo Fragmentos de conteúdo, suas chamadas GraphQL, suas chamadas de API REST e seu aplicativo, e prepará-lo para entrar em funcionamento.
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 9%

---

# Como unir tudo - seu aplicativo e seu conteúdo em AEM {#put-it-all-together}

Nesta parte do [jornada do desenvolvedor sem periféricos do AEM](overview.md), você se familiariza com o uso das ferramentas de desenvolvimento AEM e do SDK sem cabeçalho para unir seu aplicativo.

## A história até agora {#story-so-far}

No documento anterior da jornada sem cabeçalho AEM, [Como atualizar seu conteúdo por meio das APIs do AEM Assets](update-your-content.md) você aprendeu a atualizar o conteúdo sem cabeçalho existente no AEM por meio da API e agora deve:

* Entenda a API HTTP do AEM Assets.

## Objetivo {#objective}

Este artigo tem como objetivo ajudá-lo a entender como colocar seu aplicativo sem periféricos de AEM junto por:

* Saiba mais sobre o SDK sem cabeçalho do AEM e a ferramenta de desenvolvimento necessária
* Configurar um tempo de execução de desenvolvimento local para simular seu conteúdo antes de entrar no ar
* Noções básicas AEM replicação de conteúdo

## O SDK AEM {#the-aem-sdk}

O SDK do AEM é usado para criar e implantar código personalizado. É a principal ferramenta necessária para desenvolver e testar seu aplicativo sem periféricos antes de entrar online. Ele contém os seguintes artefatos:

* O Quickstart jar - um arquivo jar executável que pode ser usado para configurar um autor e uma instância de publicação
* Ferramentas do Dispatcher - o módulo Dispatcher e suas dependências para sistemas baseados em Windows e UNIX®
* Java™ API Jar - A dependência Java™ Jar/Maven que expõe todas as APIs Java™ permitidas que podem ser usadas para desenvolvimento em relação a AEM
* Javadoc jar - o javadocs para o jar da API do Java™

## O SDK sem cabeçalho do AEM {#the-aem-headless-sdk}

Diferente do SDK AEM, o AEM **SDK sem periféricos** O é um conjunto de bibliotecas que podem ser usadas pelos clientes para interagir rápida e facilmente com AEM APIs headless por HTTP.

Para obter mais informações sobre o SDK sem cabeçalho AEM, consulte o [documentação aqui](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html).

## Ferramentas de desenvolvimento adicionais {#additional-development-tools}

Além do SDK AEM, você precisa de ferramentas adicionais que facilitem o desenvolvimento e o teste do código e conteúdo localmente:

* Java™
* Git
* Apache Maven
* A biblioteca Node.js
* O IDE de sua escolha

Como AEM é um aplicativo Java™, é necessário instalar o Java™ e o Java™ SDK para dar suporte ao desenvolvimento AEM as a Cloud Service.

O Git é o que você usa para gerenciar o controle de origem e verificar as alterações no Cloud Manager e, em seguida, implantá-las em uma instância de produção.

AEM usa o Apache Maven para criar projetos gerados a partir do arquétipo de projeto AEM Maven. Todos os principais IDEs fornecem suporte de integração para Maven.

Node.js é um ambiente de tempo de execução JavaScript usado para trabalhar com os ativos de front-end de um projeto de AEM `ui.frontend` subprojeto. O Node.js é distribuído com npm, é o Gerenciador de Pacotes Node.js de fato, usado para gerenciar dependências do JavaScript.

## Principais componentes de um sistema AEM {#components-of-an-aem-system-at-a-glance}

Em seguida, vamos olhar para as partes constituintes de um ambiente AEM.

Um ambiente AEM completo é composto de um Autor, Publicação e Dispatcher. Esses mesmos componentes são disponibilizados no tempo de execução de desenvolvimento local para facilitar a visualização do código e conteúdo antes de entrar no ar.

* **O serviço do Autor** é onde os usuários internos criam, gerenciam e visualizam conteúdo.

* **O serviço de Publicação** é considerado o ambiente &quot;ativo&quot; e é, normalmente, com o que os usuários finais interagem. O conteúdo, após ser editado e aprovado no serviço do Autor, é distribuído ao serviço de Publicação. O padrão de implantação mais comum com aplicativos headless do AEM é ter uma versão de produção do aplicativo conectada a um serviço de publicação do AEM.

* **O Dispatcher** é um servidor Web estático aumentado com o módulo Dispatcher do AEM. Armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

## O fluxo de trabalho de desenvolvimento local {#the-local-development-workflow}

O projeto de desenvolvimento local é construído no Apache Maven e está usando o Git para controle de origem. Para atualizar o projeto, os desenvolvedores podem usar seu ambiente de desenvolvimento integrado preferido, como Eclipse, Visual Studio Code ou IntelliJ, entre outros.

Para testar atualizações de código ou conteúdo assimiladas pelo seu aplicativo sem periféricos, você deve implantar as atualizações no tempo de execução do AEM local, que inclui instâncias locais dos serviços de criação e publicação do AEM.

Anote as distinções entre cada componente no tempo de execução do AEM local, pois é importante testar suas atualizações onde elas são mais importantes. Por exemplo, teste as atualizações de conteúdo no autor ou teste o novo código na instância de publicação.

Em um sistema de produção, um Dispatcher e um servidor http Apache sempre estarão na frente de uma instância de publicação de AEM. Eles fornecem serviços de armazenamento em cache e de segurança para o sistema de AEM, portanto, é fundamental testar atualizações de código e conteúdo em relação ao Dispatcher também.

## Visualização do código e conteúdo localmente com o ambiente de desenvolvimento local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar o seu projeto AEM sem cabeça para lançamento, você precisa garantir que todas as partes constituintes do seu projeto estejam funcionando bem.

Para fazer isso, você deve juntar tudo: código, conteúdo e configuração, além de testá-los em um ambiente de desenvolvimento local para estar em prontidão.

O ambiente de desenvolvimento local compreende três áreas principais:

1. Projeto AEM - este projeto contém todo o código personalizado, configuração e conteúdo em que os desenvolvedores AEM trabalharão
1. O Local AEM Runtime - versões locais dos serviços de criação e publicação do AEM usados para implantar o código do AEM projeto
1. O Local Dispatcher Runtime - uma versão local do servidor Web Apache httpd que inclui o módulo Dispatcher

Depois que o ambiente de desenvolvimento local for configurado, é possível simular o conteúdo que serve para o aplicativo React ao implantar um servidor Node estático localmente.

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## O que vem a seguir {#whats-next}

Agora que você concluiu esta parte da Jornada de Desenvolvedores sem Cabeça da AEM, você deve:

* Familiarize-se com as ferramentas de desenvolvimento de AEM
* Entender o fluxo de trabalho de desenvolvimento local

Continue sua jornada sem periféricos de AEM revisando o documento [Como ativar seu aplicativo sem periféricos](/help/journey-headless/developer/go-live.md) onde você leva seu AEM projeto Headless ao vivo!

## Recursos adicionais {#additional-resources}

* [O SDK AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Configurar Um Ambiente De AEM Local](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=pt-BR)
* [AEM SDK sem cabeçalho para navegadores do lado do cliente (JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [SDK sem cabeçalho AEM para server-side/Node.js (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [SDK sem periféricos AEM para Java™](https://github.com/adobe/aem-headless-client-java)

