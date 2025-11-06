---
title: 'Como unir tudo: seu aplicativo e seu conteúdo no AEM headless'
description: Nesta parte da Jornada de desenvolvedores headless do AEM, saiba como participar do Projeto do AEM, incluindo Fragmentos de conteúdo, chamadas de GraphQL, chamadas de API REST e aplicativo, e prepará-lo para entrar em funcionamento.
exl-id: bece84ad-4c8c-410c-847e-9ef3f79970cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 97%

---

# Como unir tudo: seu aplicativo e seu conteúdo no AEM headless {#put-it-all-together}

Nesta parte da [Jornada de desenvolvedores headless do AEM](overview.md), você se familiariza com o uso das ferramentas de desenvolvimento do AEM e do SDK headless para montar seu aplicativo.

## A história até agora {#story-so-far}

No documento anterior da jornada headless do AEM, [Como atualizar seu conteúdo por meio das APIs do AEM Assets](update-your-content.md) você aprendeu a atualizar o conteúdo headless existente no AEM por meio da API e agora deve:

* Entender a API HTTP do AEM Assets.

## Objetivo {#objective}

Este artigo tem como objetivo ajudar você a entender como montar seu aplicativo AEM headless:

* Saiba mais sobre o SDK headless do AEM e a ferramenta de desenvolvimento necessária
* Configurar um tempo de execução de desenvolvimento local para simular seu conteúdo antes de entrar no ar
* Compreensão dos fundamentos da replicação de conteúdo do AEM

## O SDK do AEM {#the-aem-sdk}

O SDK do AEM é usado para criar e implantar código personalizado. Esta é a principal ferramenta necessária para desenvolver e testar seu aplicativo headless antes de colocá-lo em funcionamento. Ele contém os seguintes artefatos:

* O Quickstart jar: um arquivo jar executável que pode ser usado para configurar um autor e uma instância de publicação
* Ferramentas do Dispatcher: o módulo Dispatcher e suas dependências para sistemas baseados em Windows e UNIX®
* Java™ API Jar: a dependência Java™ Jar/Maven que expõe todas as APIs Java™ permitidas que podem ser usadas para desenvolvimento no AEM
* Javadoc jar: o javadocs para o jar da API Java™

## O SDK headless do AEM {#the-aem-headless-sdk}

Diferente do SDK do AEM, o **SDK headless** do AEM é um conjunto de bibliotecas que podem ser usadas pelos clientes para interagir rápida e facilmente com APIs headless do AEM por HTTP.

Para obter mais informações, consulte [AEM Headless SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=pt-BR).

## Ferramentas de desenvolvimento adicionais {#additional-development-tools}

Além do SDK do AEM, você precisa de ferramentas adicionais que facilitem o desenvolvimento e o teste do código e conteúdo localmente:

* Java™
* Git
* Apache Maven
* A biblioteca Node.js
* O IDE de sua escolha

Uma vez que o AEM é um aplicativo Java™, é necessário instalar o Java™ e o SDK do Java™ para dar suporte ao desenvolvimento do AEM as a Cloud Service.

O Git é o que você usa para gerenciar o controle de origem e verificar as alterações no Cloud Manager e, em seguida, implantá-las em uma instância de produção.

O AEM usa o Apache Maven para criar projetos gerados a partir do arquétipo de projeto Maven do AEM. Todos os principais IDEs fornecem suporte de integração para Maven.

Node.js é um ambiente de tempo de execução JavaScript usado para trabalhar com os ativos de front-end de um subprojeto de `ui.frontend` do projeto do AEM. O Node.js é distribuído com npm, é o Gerenciador de Pacotes Node.js de fato, usado para gerenciar dependências do JavaScript.

## Principais características de componentes de um sistema do AEM {#components-of-an-aem-system-at-a-glance}

Em seguida, vamos analisar as partes constituintes de um ambiente do AEM.

Um ambiente do AEM completo é composto de um Autor, Publicação e Dispatcher. Esses mesmos componentes são disponibilizados no tempo de execução de desenvolvimento local para facilitar a visualização do código e do conteúdo antes de colocá-lo em funcionamento.

* **O serviço do Autor** é onde os usuários internos criam, gerenciam e visualizam conteúdo.

* **O serviço de Publicação** é considerado o ambiente “ativo” e é, normalmente, com o que os usuários finais interagem. O conteúdo, após ser editado e aprovado no serviço do Autor, é distribuído ao serviço de Publicação. O padrão de implantação mais comum com aplicativos headless do AEM é ter uma versão de produção do aplicativo conectada a um serviço de publicação do AEM.

* **O Dispatcher** é um servidor Web estático aumentado com o módulo AEM Dispatcher. Ele armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

## O fluxo de trabalho de desenvolvimento local {#the-local-development-workflow}

O projeto de desenvolvimento local é construído no Apache Maven e usa o Git para controle de origem. Para atualizar o projeto, a equipe de desenvolvimento pode usar seu ambiente integrado preferido, como Eclipse, Visual Studio Code, IntelliJ, entre outros.

Para testar atualizações de código ou conteúdo assimiladas pelo aplicativo headless, você deve implantar as atualizações no tempo de execução do AEM local, que inclui instâncias locais dos serviços de criação e publicação do AEM.

Anote as distinções entre cada componente no tempo de execução do AEM local, pois é importante testar as atualizações onde elas são mais importantes. Por exemplo, teste as atualizações de conteúdo no autor ou teste o novo código na instância de publicação.

Em um sistema de produção, um Dispatcher e um servidor http Apache sempre estarão na frente de uma instância de publicação do AEM. Eles fornecem serviços de armazenamento em cache e de segurança para o sistema do AEM, portanto, é fundamental testar atualizações de código e conteúdo em relação ao Dispatcher também.

## Visualização do código e conteúdo localmente com o ambiente de desenvolvimento local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar o projeto do AEM headless para o lançamento, você precisa garantir que todas as partes constituintes do seu projeto estejam funcionando bem.

Para fazer isso, você deve juntar tudo: código, conteúdo e configuração, além de testá-los em um ambiente de desenvolvimento local para prepará-los para entrar em operação.

O ambiente de desenvolvimento local compreende três áreas principais:

1. O projeto do AEM: este projeto contém todo o código personalizado, a configuração e o conteúdo em que os desenvolvedores do AEM trabalharão
1. O tempo de execução do AEM local: versões locais dos serviços de criação e publicação do AEM usados para implantar o código do projeto do AEM
1. O tempo de execução do Dispatcher local: uma versão local do servidor Web Apache httpd que inclui o módulo Dispatcher

Depois que o ambiente do desenvolvimento local estiver configurado, você pode simular a exibição de conteúdo para o aplicativo React implantando um servidor Node estático localmente.

<!-- THIS TOPIC IS 404. IT DOES NOT APPEAR IN THE TOC OR ANYWHERE ELSE To get a more in-depth look at setting up a local development environment and all dependencies needed for content preview, see [Production Deployment documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/headless-tutorial/graphql/multi-step/production-deployment.html). -->

## O que vem a seguir {#whats-next}

Agora que concluiu esta parte da jornada de desenvolvedores headless do AEM, você deve:

* Familiarize-se com as ferramentas de desenvolvimento do AEM
* Compreensão do fluxo de trabalho de desenvolvimento local

Continue sua jornada headless do AEM revisando o documento [Como ativar seu aplicativo headless](/help/journey-headless/developer/go-live.md) por meio do qual você coloca seu projeto headless do AEM em funcionamento.

## Recursos adicionais {#additional-resources}

* [O SDK do AEM as a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Configurar um Ambiente do AEM local](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=pt-BR)
* [SDK headless do AEM para navegadores do lado do cliente (JavaScript)](https://github.com/adobe/aem-headless-client-js)
* [SDK headless do AEM para lado do servidor/Node.js (JavaScript)](https://github.com/adobe/aem-headless-client-nodejs)
* [SDK headless do AEM para Java™](https://github.com/adobe/aem-headless-client-java)
* [Introdução ao AEM as a Headless CMS](/help/headless/introduction.md)
* [Portal do Desenvolvedor do AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
* [Tutoriais do Headless no AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/getting-started-with-aem-headless/overview)
