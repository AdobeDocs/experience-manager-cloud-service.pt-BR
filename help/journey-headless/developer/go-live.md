---
title: Como executar o aplicativo headless
description: Nesta parte da Jornada do desenvolvedor headless do AEM, saiba como implantar um aplicativo headless, colocando seu código local no Git e movendo-o para o Git do Cloud Manager para o pipeline de CI/CD.
exl-id: 81616e31-764b-44b0-94a6-3ae24ce56bf6
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 2ccca86a0e611b93c273e37abb6e0fd7870421d4
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 88%

---

# Como executar o aplicativo headless {#go-live}

Nesta parte da [Jornada do desenvolvedor headless do AEM](overview.md), saiba como implantar um aplicativo headless, colocando seu código local no Git e movendo-o para o Git do Cloud Manager para o pipeline de CI/CD.

## A história até agora {#story-so-far}

No documento anterior da jornada headless do AEM, [Como unir tudo: seu aplicativo e seu conteúdo no AEM headless](put-it-all-together.md), você aprendeu a usar as ferramentas de desenvolvimento do AEM para unir todas as facetas de seu projeto.

Este artigo se baseia nesses fundamentos para que você entenda como preparar seu próprio projeto headless do AEM.

## Objetivo {#objective}

Este documento ajuda você a entender o pipeline de publicação headless do AEM e as considerações de desempenho que você deve conhecer antes de executar seu aplicativo.

* Proteger e dimensionar o aplicativo antes do lançamento
* Monitorar o desempenho e depurar problemas

Para preparar o aplicativo headless do AEM para o lançamento, siga as práticas recomendadas descritas abaixo.

## Proteger e dimensionar o aplicativo headless antes do lançamento {#secure-and-scale-before-launch}

1. Configurar a [Autenticação baseada em token](/help/headless/security/authentication.md) com suas solicitações da GraphQL
1. Configurar [Armazenamento em cache](/help/implementing/dispatcher/caching.md).

## Estrutura do modelo vs Saída da GraphQL {#structure-vs-output}

* Evite criar consultas que produzem mais de 15 kb de JSON (gzip compactado). Arquivos JSON longos consomem muitos recursos para análise do aplicativo cliente.
* Evite mais de cinco níveis aninhados de hierarquias de fragmentos. Níveis adicionais tornam difícil para os autores de conteúdo considerar o impacto de suas alterações.
* Use consultas de vários objetos em vez de modelar consultas com hierarquias de dependência nos modelos. Isso permite maior flexibilidade a longo prazo para reestruturar a saída JSON sem precisar fazer muitas alterações de conteúdo.

## Maximizar a taxa de ocorrências do cache CDN {#maximize-cdn}

* Não use consultas diretas da GraphQL, a menos que esteja solicitando conteúdo ao vivo a partir da superfície.
   * Use consultas persistentes sempre que possível.
   * Forneça TTL CDN acima de 600 segundos para que a CDN armazene em cache.
   * O AEM pode calcular o impacto de uma alteração de modelo em consultas existentes.
* Separe arquivos JSON/consultas GraphQL que possuem altas taxas de alteração de conteúdo dos que possuem baixas taxas para reduzir o tráfego de clientes para a CDN e gerar mais TTL. Isso minimiza a revalidação do CDN no JSON com o servidor de origem.
* Para invalidar ativamente o conteúdo da CDN, use a limpeza suave. Isso permite que a CDN faça o download novamente do conteúdo sem causar a perda de um cache.

## Melhore o tempo de download de conteúdo headless {#improve-download-time}

* Verifique se os clientes HTTP usam HTTP/2.
* Verifique se os clientes HTTP aceitam a solicitação de cabeçalhos para gzip.
* Minimize o número de domínios usados para hospedar JSON e artefatos referenciados.
* Aproveite o `Last-modified-since` para atualizar recursos.
* Use a saída `_reference` no arquivo JSON para iniciar o download de ativos sem precisar analisar os arquivos JSON completos.

## Implantar para produção {#deploy-to-production}

Depois de verificar se tudo foi testado e está funcionando corretamente, você está pronto para enviar as atualizações de código para um [repositório Git centralizado no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=pt-BR).

Depois que as atualizações forem carregadas no Cloud Manager, elas poderão ser implantadas no AEM as a Cloud Service usando o [pipeline de CI/CD do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=pt-BR).

Você pode começar a implantar seu código usando o pipeline CI/CD do Cloud Manager, que é amplamente abordado em [Implantação de Pacotes de Conteúdo por meio do Cloud Manager e do Gerenciador de Pacotes](/help/implementing/deploying/overview.md).

## Monitoramento de desempenho {#performance-monitoring}

Para que os usuários tenham a melhor experiência possível ao usar o aplicativo headless do AEM, é importante monitorar as principais métricas de desempenho, conforme detalhado abaixo:

* Validar versões de visualização e produção do aplicativo
* Verificar as páginas de status do AEM para obter o status atual de disponibilidade do serviço
* Acessar relatórios de desempenho
   * Desempenho da entrega
      * Desempenho de CDN (Rapidamente): verifique o número de chamadas, a taxa de cache, as taxas de erro e o tráfego de conteúdo
      * Servidores de origem: número de chamadas, taxas de erro, cargas da CPU, tráfego de conteúdo
   * Desempenho do autor
      * Verificar o número de usuários, solicitações e carga
* Acessar relatórios de desempenho específicos do aplicativo e do espaço
   * Quando o servidor estiver ativo, verifique se as métricas gerais estão verdes/laranjas/vermelhas, então identifique problemas específicos do aplicativo
   * Abra os mesmos relatórios acima filtrados para o aplicativo ou espaço (por exemplo, desktop Photoshop, paywall)
   * Use APIs de log do Splunk para acessar o desempenho do serviço e do aplicativo
   * Entre em contato com o Suporte ao cliente em caso de outros problemas.

## Resolução de problemas {#troubleshooting}

### Depuração {#debugging}

Siga essas práticas recomendadas como uma abordagem geral para depurar:

* Valide a funcionalidade e o desempenho com a versão de visualização do aplicativo
* Valide a funcionalidade e o desempenho com a versão de produção do aplicativo
* Valide com a visualização JSON do Editor de fragmento de conteúdo
* Inspecione o JSON no aplicativo cliente para verificar a presença de problemas nele ou na entrega
* Inspecione o JSON usando o GraphQL para verificar a presença de problemas relacionados ao conteúdo em cache ou ao AEM 

### Registro de um erro com o suporte {#logging-a-bug-with-support}

Para informar um erro ao suporte com eficiência caso precise de mais assistência, faça o seguinte:

* Tire capturas de tela do problema, se necessário
* Documente uma maneira de reproduzir o problema
* Documente o conteúdo com o qual o é possível reproduz o problema
* Registre o problema por meio do portal de suporte do AEM com a prioridade apropriada

## A jornada termina - Será? {#journey-ends}

Parabéns! Você concluiu a Jornada do desenvolvedor headless do AEM! Agora você deve ter uma compreensão básica sobre:

* A diferença entre a entrega de conteúdo headless e headful.
* Recursos headless do AEM.
* Como organizar um projeto do AEM Headless.
* Como criar conteúdo headless no AEM.
* Como recuperar e atualizar conteúdo headless no AEM.
* Como ativar um projeto do AEM Headless.
* O que fazer depois da ativação.

Ou você já lançou seu primeiro projeto Headless do AEM ou agora tem todo o conhecimento necessário para tal. Excelente trabalho!

### Explore os Aplicativos de página única {#explore-spa}

No entanto, isso não é tudo que o armazenamento headless do AEM oferece. Talvez você se lembre na [Parte de introdução da jornada](getting-started.md#integration-levels), discutimos brevemente como o AEM não só oferece suporte a entrega headless e modelos tradicionais de pilha completa, como também pode oferecer suporte a modelos híbridos que combinam as vantagens de ambos.

Se esse tipo de flexibilidade for algo que você precisa para seu projeto, continue para a parte adicional opcional da jornada, [Como criar aplicativos de página única (SPAs) com o AEM](create-spa.md).

## Recursos adicionais {#additional-resources}

* [Introdução ao AEM as a Headless CMS](/help/headless/introduction.md)
* [Portal do Desenvolvedor do AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
* [Tutoriais do Headless no AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/getting-started-with-aem-headless/overview)
* [Uma visão geral da implantação do AEM as a Cloud Service](/help/implementing/deploying/overview.md)
* [Use o Cloud Manager para implantar seu código](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=pt-BR)
* [Integre o repositório Git do Cloud Manager a um repositório Git externo e implante um projeto para o AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=pt-BR)
