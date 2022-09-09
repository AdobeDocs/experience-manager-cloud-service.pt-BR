---
title: Como ativar seu aplicativo sem periféricos
description: Nesta parte do AEM Headless Developer Jornada, saiba como implantar um aplicativo sem periféricos, colocando seu código local no Git e movendo-o para o Cloud Manager Git para o pipeline de CI/CD.
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
source-git-commit: 270eb35023e34eed2cd17674372794c6c2cc7757
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 0%

---

# Como ativar seu aplicativo sem periféricos {#go-live}

Nesta parte do [jornada do desenvolvedor sem periféricos do AEM](overview.md), saiba como implantar um aplicativo sem periféricos, colocando seu código local no Git e movendo-o para o Git do Cloud Manager para o pipeline de CI/CD.

## A história até agora {#story-so-far}

No documento anterior da jornada sem cabeçalho AEM, [Como unir tudo - seu aplicativo e seu conteúdo em AEM](put-it-all-together.md) você aprendeu a usar as ferramentas de desenvolvimento de AEM para unir todas as facetas do seu projeto.

Este artigo se baseia nesses fundamentos para que você entenda como preparar seu próprio projeto sem periféricos AEM para entrar em funcionamento.

## Objetivo {#objective}

Este documento ajuda você a entender o pipeline de publicação sem periféricos AEM e as considerações de desempenho que você deve conhecer antes de entrar em contato com seu aplicativo.

* Proteger e dimensionar o aplicativo antes do Launch
* Monitorar problemas de desempenho e depuração

<!-- Alexandru: this is a bit redundant, to review again later

## Prepare your AEM Headless Application for Go-Live {#prepare-your-aem-headless-application-for-golive}

-->
Para preparar o aplicativo sem periféricos de AEM para o lançamento, siga as práticas recomendadas descritas abaixo.

## Proteger e dimensionar seu aplicativo sem cabeçalho antes do lançamento {#secure-and-scale-before-launch}

1. Configurar [Autenticação baseada em token](/help/headless/security/authentication.md) com suas solicitações GraphQL
1. Configurar [Armazenamento em cache](/help/implementing/dispatcher/caching.md).

## Estrutura do modelo x saída GraphQL {#structure-vs-output}

* Evite criar queries que produzem mais de 15 kb de JSON (gzip compactado). Arquivos JSON longos consomem muitos recursos para que o aplicativo cliente analise.
* Evite mais de cinco níveis aninhados de hierarquias de fragmentos. Níveis adicionais dificultam para os autores de conteúdo considerar o impacto de suas alterações.
* Use consultas de vários objetos em vez de modelar consultas com hierarquias de dependência nos modelos. Isso permite maior flexibilidade a longo prazo para reestruturar a saída JSON sem precisar fazer muitas alterações de conteúdo.

## Maximizar a taxa de ocorrências do cache CDN {#maximize-cdn}

* Não use consultas GraphQL diretas, a menos que esteja solicitando conteúdo ao vivo da superfície.
   * Use consultas persistentes sempre que possível.
   * Forneça TTL CDN acima de 600 segundos para que a CDN armazene em cache.
   * AEM pode calcular o impacto de uma alteração de modelo em consultas existentes.
* Divida arquivos JSON/consultas GraphQL entre taxas de alteração de conteúdo baixas e altas para reduzir o tráfego de clientes para CDN e atribuir TTL maior. Isso minimiza a revalidação do CDN no JSON com o servidor de origem.
* Para invalidar ativamente o conteúdo da CDN, use a limpeza suave. Isso permite que a CDN faça o download novamente do conteúdo sem causar a perda de um cache.

## Melhore o tempo de download de conteúdo headless {#improve-download-time}

* Certifique-se de que os clientes HTTP usam HTTP/2.
* Certifique-se de que os clientes HTTP aceitem a solicitação de cabeçalhos para gzip.
* Minimize o número de domínios usados para hospedar JSON e artefatos referenciados.
* Aproveitamento `Last-modified-since` para atualizar recursos.
* Use `_reference` saída no arquivo JSON para iniciar o download de ativos sem precisar analisar os arquivos JSON completos.

## Implantar na produção {#deploy-to-production}

Depois de verificar se tudo foi testado e está funcionando corretamente, você está pronto para enviar as atualizações de código para um [repositório Git centralizado no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

Depois que as atualizações forem carregadas no Cloud Manager, elas poderão ser implantadas em AEM as a Cloud Service usando [pipeline de CI/CD do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

Você pode começar a implantar seu código aproveitando o pipeline de CI/CD do Cloud Manager, que é coberto extensivamente [here](/help/implementing/deploying/overview.md).

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
   * Quando o servidor estiver ativo, verifique se as métricas gerais estão verde/laranja/vermelho, e identifique problemas específicos do aplicativo
   * Abra os mesmos relatórios acima filtrados para o aplicativo ou espaço (por exemplo, desktop do Photoshop, paywall)
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

## A Jornada Termina - Ou Será? {#journey-ends}

Parabéns. Você concluiu a Jornada do desenvolvedor sem cabeçalho AEM! Agora você deve conhecer:

* A diferença entre a entrega de conteúdo sem periféricos e com periféricos.
* AEM recursos sem periféricos.
* Como organizar e AEM um projeto autônomo.
* Como criar conteúdo sem periféricos no AEM.
* Como recuperar e atualizar o conteúdo sem periféricos no AEM.
* Como participar de um projeto sem cabeçalho AEM.
* O que fazer depois do lançamento.

Você já lançou seu primeiro projeto AEM Headless ou agora tem todo o conhecimento necessário para isso. Excelente trabalho!

### Explorar aplicativos de página única {#explore-spa}

As lojas sem cabeça no AEM não precisam parar aqui. Você deve se lembrar do [Parte Introdução da jornada](getting-started.md#integration-levels) discutimos brevemente como o AEM não só suporta o delivery sem interface e os modelos de pilha completa tradicionais, como também pode suportar modelos híbridos que combinam as vantagens de ambos.

Se esse tipo de flexibilidade é algo que você precisa para o seu projeto, continue para a parte adicional opcional da jornada, [Como criar aplicativos de página única (SPA) com AEM.](create-spa.md)

## Recursos adicionais {#additional-resources}

* [Uma visão geral da implantação no AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [Use o Cloud Manager para implantar seu código](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)
* [Integre o Repositório Git do Cloud Manager a um Repositório Git Externo e Implante um Projeto para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html)
