---
title: Como ativar seu aplicativo sem periféricos
description: Nesta parte do AEM Headless Developer Jornada, saiba como implantar um aplicativo headless, colocando seu código local no Git e movendo-o para o Cloud Manager Git para o pipeline de CI/CD.
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
source-git-commit: 309fae113f98111e8dc548226a7fba1b72f16248
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 0%

---

# Como ativar seu aplicativo sem cabeçalho {#go-live}

>[!CAUTION]
>
>TRABALHO EM ANDAMENTO - A criação deste documento está em curso e não deve ser entendida como completa ou definitiva, nem deve ser usada para fins de produção.

Nesta parte do [AEM Headless Developer Jornada,](overview.md) saiba como implantar um aplicativo headless, colocando seu código local no Git e movendo-o para o Cloud Manager Git para o pipeline de CI/CD.

## A história até agora {#story-so-far}

No documento anterior da jornada sem periféricos AEM, [Como colocar tudo junto - Seu aplicativo e seu conteúdo em AEM sem periféricos](put-it-all-together.md) você aprendeu a preparar seu próprio projeto AEM sem periféricos para entrar em funcionamento e agora deveria:

* Entenda os requisitos para entrar no ar.

Este artigo se baseia nesses fundamentos para que você entenda como colocar seu projeto sem cabeçalho AEM em execução.

## Objetivo {#objective}

Este documento ajuda você a entender o pipeline de publicação sem periféricos AEM e as considerações de desempenho que você precisa ter em mente antes de entrar em contato com seu aplicativo.

* Saiba mais sobre o SDK do AEM e a ferramenta de desenvolvimento necessária
* Configure um tempo de execução de desenvolvimento local para simular seu conteúdo antes de entrar no ar
* Noções básicas sobre replicação e cache de conteúdo AEM
* Proteger e dimensionar o aplicativo antes do Launch
* Monitorar problemas de desempenho e depuração

## O SDK do AEM {#the-aem-sdk}

Ele contém os seguintes artefatos:

* O Quickstart jar - um arquivo jar executável que pode ser usado para configurar um autor e uma instância de publicação
* Ferramentas do Dispatcher - o módulo Dispatcher e suas dependências para sistemas baseados em Windows e UNIX
* Java API Jar - A dependência Java Jar/Maven que expõe todas as APIs Java permitidas que podem ser usadas para desenvolvimento em relação a AEM
* Javadoc jar - o javadocs para o jar da API Java

## Ferramentas de desenvolvimento {#development-tools}

Além do SDK AEM, você precisará de ferramentas adicionais que facilitem o desenvolvimento e o teste do código e conteúdo localmente:

* Java
* O SDK AEM
* Git
* Apache Maven
* A biblioteca Node.js
* O IDE de sua escolha

Como o AEM é um aplicativo Java, é necessário instalar o Java e o SDK Java para dar suporte ao desenvolvimento do AEM como Cloud Service.

O SDK do AEM é usado para criar e implantar código personalizado. É a principal ferramenta necessária para testar seu aplicativo sem periféricos antes de entrar online.

O Git é o que você usará para gerenciar o controle do código-fonte, bem como para verificar as alterações no Cloud Manager e, em seguida, implantá-las em uma instância de produção.

AEM usa o Apache Maven para criar projetos gerados a partir do arquétipo de projeto AEM Maven. Todos os principais IDEs fornecem suporte de integração para Maven.

Node.js é um ambiente de tempo de execução JavaScript usado para trabalhar com os ativos de front-end de um subprojeto ui.frontend de um projeto AEM. O Node.js é distribuído com npm, é o gerenciador de pacotes Node.js de fato, usado para gerenciar dependências do JavaScript.

## Componentes de um sistema de AEM em um resumo {#components-of-an-aem-system-at-a-glance}

Um ambiente AEM completo é composto de um Autor, Publicação e Dispatcher. Esses mesmos componentes serão disponibilizados no tempo de execução de desenvolvimento local para facilitar a visualização do código e conteúdo antes de entrar no ar.

* **O serviço Autor** é onde usuários internos criam, gerenciam e visualizam conteúdo.

* **O** serviço de Publicação é considerado o ambiente &quot;Ao vivo&quot; e normalmente é com o que os usuários finais interagem. O conteúdo, após ser editado e aprovado no serviço Autor, é distribuído ao serviço de Publicação. O padrão de implantação mais comum com AEM aplicativos sem cabeçalho é ter a versão de produção do aplicativo conectada a um serviço de publicação do AEM.

* **O** Dispatcher é um servidor da Web estático aumentado com o módulo Dispatcher de AEM. Armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

## O Fluxo de Trabalho de Desenvolvimento Local {#the-local-development-workflow}

O projeto de desenvolvimento local é construído no Apache Maven e está usando o Git para controle de origem. Para atualizar o projeto, os desenvolvedores podem usar seu ambiente de desenvolvimento integrado preferido, como Eclipse, Visual Studio Code ou IntelliJ, entre outros.

Para testar atualizações de código ou conteúdo que serão assimiladas pelo aplicativo sem periféricos, é necessário implantar as atualizações no tempo de execução do AEM local, que inclui instâncias locais dos serviços de criação e publicação do AEM.

Anote as distinções entre cada componente no tempo de execução do AEM local, pois é importante testar suas atualizações onde elas são mais importantes. Por exemplo, teste as atualizações de conteúdo no autor ou teste o novo código na instância de publicação.

Em um sistema de produção, um dispatcher e um servidor http Apache sempre se sentarão na frente de uma instância de publicação de AEM. Eles fornecem serviços de armazenamento em cache e de segurança para o sistema de AEM, portanto, é fundamental testar atualizações de código e conteúdo em relação ao dispatcher também.

Depois de verificar se tudo foi testado e está funcionando corretamente, você está pronto para enviar suas atualizações de código para um repositório Git centralizado no Cloud Manager.

Depois que as atualizações forem carregadas no Cloud Manager, elas poderão ser implantadas no AEM como um Cloud Service usando o pipeline de CI/CD do Cloud Manager.

## Visualização do código e conteúdo localmente com o ambiente de desenvolvimento local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar o seu projeto sem periféricos AEM para lançamento, você precisa garantir que todas as partes constituintes do seu projeto estejam funcionando bem.

Para fazer isso, você precisa juntar tudo: código, conteúdo e configuração e teste-os em um ambiente de desenvolvimento local para estar em prontidão.

O ambiente de desenvolvimento local compreende três áreas principais:

1. O AEM Project - isso conterá todos os códigos personalizados, configurações e conteúdo em que os desenvolvedores AEM trabalharão
1. O Local AEM Runtime - versões locais dos serviços de criação e publicação do AEM que serão usados para implantar o código do AEM projeto
1. O Local Dispatcher Runtime - uma versão local do servidor Web Apache httpd que inclui o módulo Dispatcher

Depois que o ambiente de desenvolvimento local for configurado, é possível simular o conteúdo que serve para o aplicativo React ao implantar um servidor Node estático localmente.

Para obter uma análise mais detalhada da configuração de um ambiente de desenvolvimento local e todas as dependências necessárias para a visualização de conteúdo, consulte [Implantação de produção com um serviço de publicação do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## Implantar na produção {#deploy-to-production}

Depois de testar todo o código e conteúdo localmente, você estará pronto para iniciar uma implantação de produção com o AEM.

Você pode começar a implantar seu código aproveitando o pipeline de CI/CD do Cloud Manager, que é coberto extensivamente [aqui](/help/implementing/deploying/overview.md).

## Prepare seu aplicativo sem cabeçalho AEM para ativação {#prepare-your-aem-headless-application-for-golive}

Agora é hora de preparar seu aplicativo sem periféricos AEM para o lançamento, seguindo as práticas recomendadas descritas abaixo.

### Proteja e dimensione seu aplicativo sem cabeçalho antes de iniciar {#secure-and-scale-before-launch}

1. Configurar [Autenticação Baseada em Token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
1. Webhooks seguros
1. Configurar armazenamento em cache e escalabilidade

### Estrutura do modelo vs Saída GraphQL {#structure-vs-output}

* Evite criar queries que produzem mais de 15 kb de JSON (gzip compactado). Arquivos JSON longos consomem muitos recursos para que o aplicativo cliente analise.
* Evite mais de cinco níveis aninhados de hierarquias de fragmentos. Níveis adicionais dificultam para os autores de conteúdo considerar o impacto de suas alterações.
* Use consultas de vários objetos em vez de modelar consultas com hierarquias de dependência nos modelos. Isso permite maior flexibilidade a longo prazo para reestruturar a saída JSON sem precisar fazer muitas alterações de conteúdo.

### Maximizar a taxa de ocorrências do cache CDN {#maximize-cdn}

* Não use consultas GraphQL diretas, a menos que esteja solicitando conteúdo ao vivo da superfície.
   * Em vez disso, use consultas persistentes.
   * Forneça TTL CDN acima de 600 segundos para que a CDN possa armazená-los em cache.
   * AEM pode calcular o impacto de uma alteração de modelo em consultas existentes.
* Divida arquivos JSON/consultas GraphQL entre taxas de alteração de conteúdo baixas e altas para reduzir o tráfego de clientes para CDN e atribuir TTL maior. Isso minimiza a revalidação do CDN no JSON com o servidor de origem.
* Para invalidar ativamente o conteúdo da CDN, use a limpeza suave. Isso permite que a CDN baixe novamente o conteúdo sem causar a perda de um cache.

### Melhore o tempo para baixar conteúdo headless {#improve-download-time}

* Certifique-se de que os clientes HTTP usam HTTP/2.
* Certifique-se de que os clientes HTTP aceitem a solicitação de cabeçalhos para gzip.
* Minimize o número de domínios usados para hospedar JSON e artefatos referenciados.
* Utilize `Last-modified-since` para atualizar recursos.
* Use a saída `_reference` no arquivo JSON para iniciar o download de ativos sem precisar analisar os arquivos JSON completos.

## Monitoramento de desempenho {#performance-monitoring}

Para que os usuários tenham a melhor experiência possível ao usar o aplicativo sem periféricos AEM, é importante monitorar as principais métricas de desempenho, conforme detalhado abaixo:

* Validar versões de visualização e produção do aplicativo
* Verificar AEM páginas de status para o status de disponibilidade de serviço atual
* Acessar relatórios de desempenho
   * Desempenho do delivery
      * Fastly (CDN) - verifique o número de chamadas, a taxa de cache, as taxas de erro, o tráfego de carga
      * Servidores de origem - número de chamadas, taxas de erro, cargas da CPU, tráfego de carga
   * Desempenho do autor
      * Verificar o número de usuários, solicitações e carregamento
* Acessar relatórios de desempenho específicos do aplicativo e do espaço
   * Quando o servidor estiver ativo, verifique se as métricas gerais estão verde/laranja/vermelho, e identifique problemas específicos do aplicativo
   * Abra os mesmos relatórios acima filtrados para o aplicativo/espaço (ou seja, desktop do Photoshop, paywall etc.)
   * Use APIs de log do Splunk para acessar o desempenho do serviço e do aplicativo
   * Entre em contato com o Suporte ao cliente em caso de outros problemas.

## Resolução de problemas {#troubleshooting}

### Depuração {#debugging}

Siga essas práticas recomendadas como uma abordagem geral para depurar:

* Validar a funcionalidade e o desempenho com a versão de visualização do aplicativo
* Validar a funcionalidade e o desempenho com a versão de produção do aplicativo
* Validar com a visualização JSON do Editor de fragmento de conteúdo
* Inspect o JSON no aplicativo cliente para verificar a presença de problemas no aplicativo cliente ou no delivery
* Inspect o JSON usando GraphQL para verificar a presença de problemas relacionados ao conteúdo ou AEM em cache

### Registro de um bug com suporte {#logging-a-bug-with-support}

Para registrar um bug com suporte com eficiência, caso precise de assistência adicional, siga as etapas abaixo:

* Tire capturas de tela do problema, se necessário
* Documente uma maneira de reproduzir o problema
* Documente o conteúdo com o qual o problema reproduz
* Registre um problema por meio do portal de suporte AEM com a prioridade apropriada

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da Jornada de Desenvolvedores sem Cabeça da AEM, você deve:

* Entenda AEM conceitos básicos sobre replicação e cache de conteúdo.
* Saiba como configurar as ferramentas necessárias para simular o início do aplicativo sem periféricos.
* Saiba como proteger e dimensionar seu aplicativo antes do Launch.
* Entenda como monitorar problemas de desempenho e depuração.

Você deve continuar sua jornada sem periféricos de AEM revisando o documento [Pós-lançamento](post-launch.md) onde você aprende a manter sua experiência sem periféricos.

## Recursos adicionais {#additional-resources}

* [Configurar Um Ambiente De AEM Local](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [O AEM como um SDK do Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Uma visão geral da implantação do no AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [Use o Cloud Manager para implantar seu código](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Integre o Repositório Git do Cloud Manager a um Repositório Git Externo e Implante um Projeto para AEM como Cloud Service](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/master/help/implementing/developing/headless-journey/access-your-content.md)