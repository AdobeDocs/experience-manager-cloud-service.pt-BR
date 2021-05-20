---
title: Como ativar seu aplicativo autônomo
description: Nesta parte do AEM Headless Developer Jornada, saiba como implantar um aplicativo headless, colocando seu código local no Git e movendo-o para o Cloud Manager Git para o pipeline de CI/CD.
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
source-git-commit: bc717c544bd4f0449d358b831a5132f85fa85e86
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 0%

---

# Como ativar seu aplicativo headless {#go-live}

>[!CAUTION]
>
>DESATUALIZADO - Esse conteúdo de rascunho foi substituído pela nova [Documentação de Jornada do desenvolvedor sem cabeçalho.](/help/journey-headless/developer/overview.md)

Nesta parte do [AEM Headless Developer Jornada](overview.md), saiba como implantar um aplicativo headless, colocando seu código local no Git e movendo-o para o Cloud Manager Git para o pipeline de CI/CD.

## A história até agora {#story-so-far}

No documento anterior da jornada sem cabeçalho AEM, [Como atualizar seu conteúdo por meio das APIs do AEM Assets](update-your-content.md) você aprendeu a atualizar seu conteúdo sem cabeçalho existente no AEM por meio da API e agora deve:

* Entenda a API HTTP do AEM Assets.

Este artigo se baseia nesses fundamentos para que você entenda como preparar seu próprio projeto sem periféricos AEM para entrar em funcionamento.

## Objetivo {#objective}

Este documento ajuda você a entender o pipeline de publicação sem periféricos AEM e as considerações de desempenho que você precisa ter em mente antes de entrar em contato com seu aplicativo.

* Saiba mais sobre o SDK do AEM e a ferramenta de desenvolvimento necessária
* Configure um tempo de execução de desenvolvimento local para simular seu conteúdo antes de entrar no ar
* Noções básicas sobre replicação e cache de conteúdo AEM
* Proteger e dimensionar o aplicativo antes do Launch
* Monitorar problemas de desempenho e depuração

## O SDK do AEM {#the-aem-sdk}

O SDK do AEM é usado para criar e implantar código personalizado. É a principal ferramenta necessária para desenvolver e testar seu aplicativo sem periféricos antes de entrar online. Ele contém os seguintes artefatos:

* O Quickstart jar - um arquivo jar executável que pode ser usado para configurar um autor e uma instância de publicação
* Ferramentas do Dispatcher - o módulo Dispatcher e suas dependências para sistemas baseados em Windows e UNIX
* Java API Jar - A dependência Java Jar/Maven que expõe todas as APIs Java permitidas que podem ser usadas para desenvolvimento em relação a AEM
* Javadoc jar - o javadocs para o jar da API Java

## Ferramentas adicionais de desenvolvimento {#additional-development-tools}

Além do SDK AEM, você precisará de ferramentas adicionais que facilitem o desenvolvimento e o teste do código e conteúdo localmente:

* Java
* Git
* Apache Maven
* A biblioteca Node.js
* O IDE de sua escolha

Como o AEM é um aplicativo Java, é necessário instalar o Java e o SDK Java para dar suporte ao desenvolvimento do AEM como Cloud Service.

O Git é o que você usará para gerenciar o controle do código-fonte, bem como para verificar as alterações no Cloud Manager e, em seguida, implantá-las em uma instância de produção.

AEM usa o Apache Maven para criar projetos gerados a partir do arquétipo de projeto AEM Maven. Todos os principais IDEs fornecem suporte de integração para Maven.

Node.js é um ambiente de tempo de execução JavaScript usado para trabalhar com os ativos de front-end de um subprojeto `ui.frontend` de um projeto AEM. O Node.js é distribuído com npm, é o gerenciador de pacotes Node.js de fato, usado para gerenciar dependências do JavaScript.

## Componentes de um sistema de AEM em um resumo {#components-of-an-aem-system-at-a-glance}

Em seguida, vamos dar uma olhada nas partes constituintes de um ambiente AEM.

Um ambiente AEM completo é composto de um Autor, Publicação e Dispatcher. Esses mesmos componentes serão disponibilizados no tempo de execução de desenvolvimento local para facilitar a visualização do código e conteúdo antes de entrar no ar.

* **O serviço Autor** é onde usuários internos criam, gerenciam e visualizam conteúdo.

* **O** serviço de Publicação é considerado o ambiente &quot;Ao vivo&quot; e normalmente é com o que os usuários finais interagem. O conteúdo, após ser editado e o aplicativo criado no serviço Autor, é distribuído ao serviço de Publicação. O padrão de implantação mais comum com AEM aplicativos sem cabeçalho é ter a versão de produção do aplicativo conectada a um serviço de publicação do AEM.

* **O** Dispatcher é um servidor da Web estático aumentado com o módulo Dispatcher de AEM. Armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

## O Fluxo de Trabalho de Desenvolvimento Local {#the-local-development-workflow}

O projeto de desenvolvimento local é construído no Apache Maven e está usando o Git para controle de origem. Para atualizar o projeto, os desenvolvedores podem usar seu ambiente de desenvolvimento integrado preferido, como Eclipse, Visual Studio Code ou IntelliJ, entre outros.

Para testar atualizações de código ou conteúdo que serão assimiladas pelo aplicativo sem periféricos, é necessário implantar as atualizações no tempo de execução do AEM local, que inclui instâncias locais dos serviços de criação e publicação do AEM.

Anote as distinções entre cada componente no tempo de execução do AEM local, pois é importante testar suas atualizações onde elas são mais importantes. Por exemplo, teste as atualizações de conteúdo no autor ou teste o novo código na instância de publicação.

Em um sistema de produção, um dispatcher e um servidor http Apache sempre se sentarão na frente de uma instância de publicação de AEM. Eles fornecem serviços de armazenamento em cache e de segurança para o sistema de AEM, portanto, é fundamental testar atualizações de código e conteúdo em relação ao dispatcher também.

## Visualização do código e conteúdo localmente com o ambiente de desenvolvimento local {#previewing-your-code-and-content-locally-with-the-local-development-environment}

Para preparar o seu projeto sem periféricos AEM para lançamento, você precisa garantir que todas as partes constituintes do seu projeto estejam funcionando bem.

Para fazer isso, você precisa juntar tudo: código, conteúdo e configuração e teste-os em um ambiente de desenvolvimento local para estar em prontidão.

O ambiente de desenvolvimento local compreende três áreas principais:

1. O AEM Project - isso conterá todos os códigos personalizados, configurações e conteúdo em que os desenvolvedores AEM trabalharão
1. O Local AEM Runtime - versões locais dos serviços de criação e publicação do AEM que serão usados para implantar o código do AEM projeto
1. O Local Dispatcher Runtime - uma versão local do servidor Web Apache httpd que inclui o módulo Dispatcher

Depois que o ambiente de desenvolvimento local for configurado, é possível simular o conteúdo que serve ao aplicativo React ao implantar um servidor Node estático localmente.

Para obter uma análise mais detalhada da configuração de um ambiente de desenvolvimento local e todas as dependências necessárias para a visualização de conteúdo, consulte a [documentação de Implantação de produção](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## Prepare seu aplicativo AEM Headless para o Go-Live {#prepare-your-aem-headless-application-for-golive}

Agora, é hora de preparar seu aplicativo sem periféricos AEM para o lançamento, seguindo as práticas recomendadas descritas abaixo.

### Proteja e dimensione seu aplicativo sem cabeçalho antes de iniciar {#secure-and-scale-before-launch}

1. Configure [Autenticação Baseada em Token](/help/assets/content-fragments/graphql-authentication-content-fragments.md) com suas solicitações GraphQL
1. Configure [Cache](/help/implementing/dispatcher/caching.md).

### Estrutura do modelo vs Saída GraphQL {#structure-vs-output}

* Evite criar queries que produzem mais de 15 kb de JSON (gzip compactado). Arquivos JSON longos consomem muitos recursos para que o aplicativo cliente analise.
* Evite mais de cinco níveis aninhados de hierarquias de fragmentos. Níveis adicionais dificultam para os autores de conteúdo considerar o impacto de suas alterações.
* Use consultas de vários objetos em vez de modelar consultas com hierarquias de dependência nos modelos. Isso permite maior flexibilidade a longo prazo para reestruturar a saída JSON sem precisar fazer muitas alterações de conteúdo.

### Maximizar a taxa de ocorrências do cache CDN {#maximize-cdn}

* Não use consultas GraphQL diretas, a menos que esteja solicitando conteúdo ao vivo da superfície.
   * Use consultas persistentes sempre que possível.
   * Forneça TTL CDN acima de 600 segundos para que a CDN armazene em cache.
   * AEM pode calcular o impacto de uma alteração de modelo em consultas existentes.
* Divida arquivos JSON/consultas GraphQL entre taxas de alteração de conteúdo baixas e altas para reduzir o tráfego de clientes para CDN e atribuir TTL maior. Isso minimiza a revalidação do CDN no JSON com o servidor de origem.
* Para invalidar ativamente o conteúdo da CDN, use a limpeza suave. Isso permite que a CDN baixe novamente o conteúdo sem causar a perda de um cache.

### Melhore o tempo para baixar conteúdo headless {#improve-download-time}

* Certifique-se de que os clientes HTTP usam HTTP/2.
* Certifique-se de que os clientes HTTP aceitem a solicitação de cabeçalhos para gzip.
* Minimize o número de domínios usados para hospedar JSON e artefatos referenciados.
* Utilize `Last-modified-since` para atualizar recursos.
* Use a saída `_reference` no arquivo JSON para iniciar o download de ativos sem precisar analisar os arquivos JSON completos.

## Implantar na produção {#deploy-to-production}

Depois de verificar se tudo foi testado e está funcionando corretamente, você está pronto para enviar suas atualizações de código para um [repositório Git centralizado no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

Depois que as atualizações forem carregadas no Cloud Manager, elas poderão ser implantadas no AEM como um Cloud Service usando o [pipeline CI/CD do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

Você pode começar a implantar seu código aproveitando o pipeline de CI/CD do Cloud Manager, que é coberto extensivamente [aqui](/help/implementing/deploying/overview.md).

## Monitoramento de desempenho {#performance-monitoring}

Para que os usuários tenham a melhor experiência possível ao usar o aplicativo sem periféricos AEM, é importante monitorar as principais métricas de desempenho, conforme detalhado abaixo:

* Validar versões de visualização e produção do aplicativo
* Verificar AEM páginas de status para o status de disponibilidade de serviço atual
* Acessar relatórios de desempenho
   * Desempenho do delivery
      * Desempenho de CDN (Fastly) - verifique o número de chamadas, a taxa de cache, as taxas de erro e o tráfego de carga
      * Servidores de origem - número de chamadas, taxas de erro, cargas da CPU, tráfego de carga
   * Desempenho do autor
      * Verificar o número de usuários, solicitações e carregamento
* Acessar relatórios de desempenho específicos do aplicativo e do espaço
   * Quando o servidor estiver ativo, verifique se as métricas gerais estão verde/laranja/vermelho e identifique problemas específicos do aplicativo
   * Abra os relatórios mencionados acima, mas filtre-os para o aplicativo ou espaço (por exemplo, desktop do Photoshop, paywall)
   * [Use ](/help/implementing/developing/introduction/logging.md#splunk-logs) APIs de log do Splunk para acessar o desempenho do serviço e do aplicativo
   * Entre em contato com o Suporte ao cliente em caso de outros problemas.

## Resolução de problemas {#troubleshooting}

### Depuração {#debugging}

Siga essas práticas recomendadas como uma abordagem geral para depurar:

* Validar a funcionalidade e o desempenho com a versão de visualização do aplicativo
* Validar a funcionalidade e o desempenho com a versão de produção do aplicativo
* Validar com a [visualização JSON](/help/assets/content-fragments/content-fragments-json-preview.md) do Editor de fragmento de conteúdo
* Inspect o JSON no aplicativo cliente para verificar a presença de problemas no aplicativo cliente ou no delivery
* Inspect o JSON usando GraphQL para verificar a presença de problemas relacionados ao conteúdo ou AEM em cache

### Registro de um bug com suporte {#logging-a-bug-with-support}

Para registrar um bug com suporte com eficiência, caso precise de assistência adicional, siga as etapas abaixo:

* Tire capturas de tela do problema, se necessário
* Documente uma maneira de reproduzir o problema
* Documente o conteúdo com o qual o problema reproduz
* Registre um problema por meio do portal de suporte AEM com a prioridade do aplicativo

## A Jornada Termina - Ou Será? {#journey-ends}

Parabéns! Você concluiu a Jornada do desenvolvedor sem cabeçalho AEM! Agora você deve conhecer:

* A diferença entre a entrega de conteúdo sem periféricos e com periféricos.
* AEM recursos sem periféricos.
* Como organizar e AEM um projeto autônomo.
* Como criar conteúdo sem periféricos no AEM.
* Como recuperar e atualizar o conteúdo sem periféricos no AEM.
* Como participar de um projeto sem cabeçalho AEM.
* O que fazer depois do lançamento?

## Recursos adicionais {#additional-resources}

* [Uma visão geral da implantação do no AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [O AEM como um SDK do Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
* [Configurar Um Ambiente De AEM Local](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)
* [Use o Cloud Manager para implantar seu código](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Integre o Repositório Git do Cloud Manager a um Repositório Git Externo e Implante um Projeto para AEM como Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)