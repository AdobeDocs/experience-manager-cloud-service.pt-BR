---
title: Como unir tudo - seu aplicativo e seu conteúdo em AEM
description: Nesta parte da Jornada de desenvolvedores sem cabeçalho do AEM, saiba como participar do Projeto de AEM, incluindo Fragmentos de conteúdo, suas chamadas GraphQL, suas chamadas de API REST e seu aplicativo, e prepará-lo para entrar em funcionamento.
hide: true
hidefromtoc: true
index: false
exl-id: 254fb9dd-36c8-43ce-aaea-ceb4d079503d
translation-type: tm+mt
source-git-commit: e8eb9d2c96d24601e50c48f6846a8c8bac8b0252
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 0%

---

# Como unir tudo - seu aplicativo e seu conteúdo em AEM autônomo {#put-it-all-together}

>[!CAUTION]
>
>TRABALHO EM ANDAMENTO - A criação deste documento está em curso e não deve ser entendida como completa ou definitiva, nem deve ser usada para fins de produção.

Nesta parte da [AEM Jornada de desenvolvedores headless,](overview.md) saiba como participar do AEM Project, incluindo Fragmentos de conteúdo, suas chamadas GraphQL, suas chamadas REST API e seu aplicativo, e prepará-lo para entrar em vigor.

## A história até agora {#story-so-far}

No documento anterior da jornada sem cabeçalho AEM, [Como atualizar seu conteúdo por meio das APIs do AEM Assets](update-your-content.md) você aprendeu a atualizar seu conteúdo sem cabeçalho existente no AEM por meio da API e agora deve:

* Entenda a API HTTP do AEM Assets.

Este artigo se baseia nesses fundamentos para que você entenda como preparar seu próprio projeto sem periféricos AEM para entrar em funcionamento.

## Objetivo {#objective}

* Entenda qual é o fluxo de trabalho de desenvolvimento local do AEM
* Instale o SDK do AEM para obter um tempo de execução de desenvolvimento local em que você pode usar para testar seu conteúdo
* Saiba mais sobre as ferramentas de desenvolvimento necessárias para trabalhar ao lado do tempo de execução de desenvolvimento local

## O Fluxo de Trabalho de Desenvolvimento Local {#the-local-development-workflow}

O projeto de desenvolvimento local é construído no Apache Maven e está usando o Git para controle de origem. Para atualizar o projeto, os desenvolvedores podem usar seu ambiente de desenvolvimento integrado preferido, como Eclipse, Visual Studio Code ou IntelliJ, entre outros.

Para testar atualizações de código ou conteúdo que serão assimiladas pelo seu aplicativo sem periféricos, é necessário implantar as atualizações em um tempo de execução de AEM local, que inclui instâncias locais das instâncias de autor e publicação do AEM.

Anote as distinções entre cada componente no tempo de execução do AEM local, pois é importante testar suas atualizações onde elas são mais importantes - por exemplo, testar atualizações de conteúdo no autor ou testar novo código na instância de publicação.

Em um sistema de produção, um dispatcher e um servidor http Apache sempre se sentarão na frente de uma instância de publicação de AEM. Eles fornecem serviços de armazenamento em cache e de segurança para o sistema de AEM, portanto, é fundamental testar atualizações de código e conteúdo em relação ao dispatcher também.

Depois de verificar se tudo foi testado e está funcionando corretamente, você está pronto para enviar suas atualizações de código para um repositório Git centralizado no Cloud Manager.

Depois que as atualizações forem carregadas no Cloud Manager, elas poderão ser implantadas no AEM como um Cloud Service usando o pipeline de CI/CD do Cloud Manager.


## O SDK do AEM {#the-aem-sdk}

O SDK do AEM é usado para criar e implantar código personalizado. Ele contém os seguintes artefatos:

* O Quickstart jar - um arquivo jar executável que pode ser usado para configurar um autor e uma instância de publicação
* Ferramentas do Dispatcher - o módulo Dispatcher e suas dependências para sistemas baseados em Windows e UNIX
* Java API Jar - A dependência Java Jar/Maven que expõe todas as APIs Java permitidas que podem ser usadas para desenvolvimento em relação a AEM
* Javadoc jar - o javadocs para o jar da API Java

## Configuração do Ambiente de Desenvolvimento Local {#local-development-environment}

Para preparar o seu projeto sem periféricos AEM para lançamento, você precisa garantir que todas as partes constituintes do seu projeto estejam funcionando bem.

Para fazer isso, é necessário reunir tudo - código, conteúdo e configuração e testá-lo em um ambiente de desenvolvimento local para estar em preparação.

O ambiente de desenvolvimento local compreende três áreas principais:

1. O AEM Project - isso conterá todos os códigos personalizados, configurações e conteúdo em que os desenvolvedores AEM trabalharão
1. O Local AEM Runtime - versões locais dos serviços de criação e publicação do AEM que serão usados para implantar o código do AEM projeto
1. O Local Dispatcher Runtime - uma versão local do servidor Web Apache httpd que inclui o módulo Dispatcher

## Ferramentas de desenvolvimento {#development-tools}

Além do SDK AEM, você precisará de ferramentas adicionais que facilitem o desenvolvimento e o teste do código e conteúdo localmente:

* Java
* Git
* Apache Maven
* A biblioteca Node.js
* O IDE de sua escolha

Como o AEM é um aplicativo Java, é necessário instalar o Java e o SDK Java para dar suporte ao desenvolvimento do AEM como Cloud Service.

O Git é a ferramenta que você usará para gerenciar o controle do código-fonte, bem como para verificar as alterações no Cloud Manager e, em seguida, implantá-las em uma instância de produção.

AEM usa o Apache Maven para criar projetos gerados a partir do arquétipo de projeto AEM Maven. Todos os principais IDEs fornecem suporte de integração para Maven.

Node.js é um ambiente de tempo de execução JavaScript usado para trabalhar com os ativos de front-end de um subprojeto ui.frontend de um projeto AEM. O Node.js é distribuído com npm, é o gerenciador de pacotes Node.js de fato, usado para gerenciar dependências do JavaScript.

## O que vem a seguir {#what-is-next}

Você deve continuar sua jornada sem periféricos de AEM revisando o documento [Como entrar em vigor com seu aplicativo sem periféricos](go-live.md), onde você realmente leva seu AEM projeto sem periféricos em tempo real!

## Recursos adicionais {#additional-resources}

* [Configuração do ambiente de desenvolvimento local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-dispatcher-runtime)  - saiba como instalar as ferramentas necessárias para começar a desenvolver para o AEM
* [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)  - Analise detalhadamente o SDK AEM