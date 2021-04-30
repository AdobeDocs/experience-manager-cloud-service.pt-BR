---
title: Como ativar seu aplicativo sem periféricos
description: Nesta parte do AEM Headless Developer Jornada, saiba como implantar um aplicativo headless, colocando seu código local no Git e movendo-o para o Cloud Manager Git para o pipeline de CI/CD.
hide: true
hidefromtoc: true
index: false
exl-id: f79b5ada-8f59-4706-9f90-bc63301b2b7d
translation-type: tm+mt
source-git-commit: dc4f1e916620127ebf068fdcc6359041b49891cf
workflow-type: tm+mt
source-wordcount: '1039'
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

* Noções básicas sobre replicação e cache de conteúdo AEM
* Configure as ferramentas necessárias para simular ficar ativa no aplicativo sem periféricos
* Proteger e dimensionar o aplicativo antes do Launch
* Monitorar problemas de desempenho e depuração

## Noções básicas sobre replicação e cache de conteúdo {#content-replication-and-caching}

Um ambiente AEM completo é composto de um Autor, Publicação e Dispatcher.

* **O serviço Autor** é onde usuários internos criam, gerenciam e visualizam conteúdo.

* **O** serviço de Publicação é considerado o ambiente &quot;Ao vivo&quot; e normalmente é com o que os usuários finais interagem. O conteúdo, após ser editado e aprovado no serviço Autor, é distribuído ao serviço de Publicação.

* **O** Dispatcher é um servidor da Web estático aumentado com o módulo Dispatcher de AEM. Armazena em cache as páginas da Web produzidas pela instância de publicação para melhorar o desempenho.

O padrão de implantação mais comum com AEM aplicativos sem cabeçalho é ter a versão de produção do aplicativo conectada a um serviço de publicação do AEM.

## Requisitos e configuração {#requirements-and-configuration}

1. Configurar um [Tempo de Execução Local](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/aem-runtime.html#install-java) usando o [AEM as a Cloud service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)
2. Instale o [conteúdo de amostra WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) e os pontos de extremidade GraphQL subsequentes
3. Implante e configure um [Servidor de nós estático](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/production-deployment.html?lang=en#static-server).

## Proteja e dimensione seu aplicativo sem cabeçalho antes de iniciar {#secure-and-scale-before-launch}

1. Configurar [Autenticação Baseada em Token](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
2. Webhooks seguros
3. Configurar armazenamento em cache e escalabilidade

## Implantar na produção {#deploy-to-production}

Depois de testar todo o código e conteúdo localmente, você está pronto para iniciar uma implantação de produção com o AEM.

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

## Monitoramento {#monitoring}

### Como verificar o desempenho geral {#check-overall-performance}

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

Para garantir que seu aplicativo funcione corretamente antes da inicialização, é recomendável seguir essas etapas como uma abordagem geral para a depuração:

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
