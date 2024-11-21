---
title: Entender as solicitações de conteúdo do Cloud Service
description: Se você adquiriu licenças de solicitação de conteúdo do Adobe, saiba mais sobre os tipos de solicitações de conteúdo que o Adobe Experience Cloud as a Service mede e as variações com as ferramentas de relatório de análise de uma organização.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f24b2672431ecf7b7b0ed11b6dc9b09344946239
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 9%

---

# Entender as solicitações de conteúdo Cloud Service

## Introdução {#introduction}

As solicitações de conteúdo se referem às solicitações feitas ao AEM Sites, incluindo as solicitações relacionadas aos Edge Delivery Services ou aos sistemas de cache fornecidos pelo cliente, como uma Rede de entrega de conteúdo. Essas solicitações entregam conteúdo ou dados no formato HTML por meio de exibições de página (por exemplo, páginas e Fragmentos de experiência) ou no formato JSON por meio de chamadas de API de maneira headless. As solicitações de conteúdo são contadas como uma exibição de página ou cinco chamadas de API e são medidas na entrada do primeiro sistema de cache a receber uma solicitação de conteúdo. Certas solicitações HTTP são incluídas ou excluídas para fins de contagem de solicitações de conteúdo. A lista completa dessas solicitações HTTP incluídas e excluídas e suas definições técnicas estão disponíveis na documentação.

## Sobre solicitações de conteúdo Cloud Service {#understanding-cloud-service-content-requests}

Para clientes que usam o CDN pronto para uso, as solicitações de conteúdo de Cloud Service são medidas por meio da coleção de dados do lado do servidor. Essa coleção é habilitada por meio da análise de log da CDN. O AEM (Adobe Experience Manager) coleta as a Cloud Service automaticamente solicitações de conteúdo do lado do servidor na borda do. Ele analisa arquivos de log gerados pelo AEM as a Cloud Service CDN. Esse processo é feito isolando as solicitações que retornam o conteúdo HTML `(text/html)` ou JSON `(application/json)` da CDN e é baseado em várias regras de inclusão e exclusão detalhadas abaixo. Uma solicitação de conteúdo ocorre independentemente de o conteúdo ser veiculado a partir dos caches CDN ou retornado à origem CDN (despachantes do AEM).

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Variações de solicitações de conteúdo Cloud Service {#content-requests-variances}

As solicitações de conteúdo podem ter variações nas ferramentas de relatório do Analytics de uma organização, conforme resumido na tabela a seguir. Em geral, evite usar ferramentas de análise que dependam de instrumentação do lado do cliente para relatar o número de solicitações de conteúdo para um site. Essas ferramentas geralmente perdem uma grande parte do tráfego porque dependem do consentimento do usuário para serem ativadas. As ferramentas do Analytics que reúnem dados do lado do servidor em arquivos de log ou relatórios CDN para clientes que adicionam seu próprio CDN sobre o AEM as a Cloud Service fornecem contagens melhores.

| Motivo da variação | Explicação |
|---|---|
| Consentimento do usuário final | As ferramentas do Analytics que dependem da instrumentação do lado do cliente geralmente dependem do consentimento do usuário para serem acionadas. Esse workflow pode representar a maioria do tráfego que não está sendo rastreado. Para clientes que desejam medir solicitações de conteúdo por conta própria, é recomendável confiar nas ferramentas de análise que coletam relatórios do lado do servidor de dados ou CDN. |
| Marcação com tags | Todas as páginas ou chamadas de API que são rastreadas como solicitações de conteúdo do Adobe Experience Manager não podem ser marcadas com o rastreamento do Analytics. |
| Regras de gerenciamento de tags | As configurações das regras de gerenciamento de tags podem resultar em várias configurações de coleta de dados em uma página, resultando em alguma combinação de discrepâncias com o rastreamento de solicitação de conteúdo. |
| Bots | Os bots desconhecidos cujo AEM não foi pré-identificado e removido podem causar discrepâncias no rastreamento. |
| Report Suites | As páginas que fazem parte de uma mesma instância e domínio do AEM podem enviar dados para diferentes conjuntos de relatórios de Analytics. |
| Ferramentas de segurança e monitoramento de terceiros | Ferramentas de verificação para monitoramento e segurança podem gerar solicitações de conteúdo para o AEM que não são rastreadas nos relatórios de Analytics. |
| Acesso à API | O acesso programático a páginas ou APIs do Adobe Experience Manager pode gerar solicitações de conteúdo para AEM que não são rastreadas nos relatórios do Analytics. |
| Solicitações de pré-busca | Usar um serviço de pré-busca para pré-carregar páginas a fim de aumentar a velocidade pode causar um aumento significativo no tráfego de solicitações de conteúdo. |
| DDOS | Enquanto o Adobe faz tentativas de detectar e filtrar automaticamente o tráfego de ataques de DDOS, não há garantia de que todos os possíveis ataques de DDOS sejam detectados. |
| Bloqueadores de tráfego | O uso de um bloqueador de rastreadores em um navegador pode impedir o rastreamento de algumas solicitações. |
| Firewalls | Os firewalls podem bloquear o rastreamento do Analytics. Esse cenário é mais frequente com firewalls corporativos. |

Consulte também [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md).

## Regras de coleção do lado do servidor {#serverside-collection}

Há regras em vigor para excluir bots conhecidos, incluindo serviços conhecidos que acessam o site regularmente para atualizar seu índice de pesquisa ou serviço.

### Tipos de solicitações de conteúdo incluídas {#included-content-requests}

| Tipo de solicitação | Solicitação de conteúdo | Descrição |
| --- | --- | --- |
| Código HTTP 100-299 | Incluído | Solicitações regulares que entregam todo o conteúdo ou parte dele. |
| Bibliotecas HTTP para automação | Incluído | Exemplos:<br>· Amazon CloudFront<br>· Apache Http Client<br>· Cliente HTTP Assíncrono<br>· Axios<br>· Azureus<br>· Curl<br>· Busca de Nó GitHub<br>· Guzzle<br>· Go-http-client<br>· Chrome Headless<br>· Cliente Java™<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· Solicitações Python<br>· Rede do Reator<br>6}· Wget<br>· WinHTTP<br>· HTTP<br>· Busca de Nós do GitHub<br>· Netty do Reator |
| Ferramentas de monitoramento e verificação de integridade | Incluído | Configurado pelo cliente para monitorar um determinado aspecto do site. Por exemplo, disponibilidade ou desempenho real do usuário. Se eles estiverem direcionando pontos de extremidade específicos como `/system/probes/health` para verificações de integridade, o Adobe recomenda usar o ponto de extremidade `/system/probes/health` e não as páginas de HTML reais do site. [Veja abaixo](#excluded-content-request)<br>Exemplos:<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatível; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` solicitações | Incluído | Para aumentar a velocidade de carregamento da próxima página, os clientes podem fazer com que o navegador carregue um conjunto de páginas antes que o usuário clique no link, de modo que já estejam no cache. *Mente: essa abordagem aumenta significativamente o tráfego*, dependendo de quantas dessas páginas são buscadas previamente. |
| Tráfego que bloqueia relatórios do Adobe Analytics ou Google Analytics | Incluído | É mais comum que os visitantes de sites tenham software de privacidade instalado (bloqueadores de anúncios e assim por diante) que afetam a precisão do Google Analytics ou do Adobe Analytics. O AEM as a Cloud Service conta as solicitações no primeiro ponto de entrada na infraestrutura operada pelo Adobe e não no lado do cliente. |

Consulte também [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md).

### Tipos de solicitações de conteúdo excluídas {#excluded-content-request}

| Tipo de solicitação | Solicitação de conteúdo | Descrição |
| --- | --- | --- |
| Código HTTP 500+ | Excluído | Erros retornados ao visitante quando algo dá errado no AEM as a Cloud Service ou no código personalizado do cliente. |
| Código HTTP 400-499 | Excluído | Erros retornados ao visitante quando o conteúdo não existe (404) ou há outros problemas relacionados ao conteúdo ou à solicitação. |
| Código HTTP 300-399 | Excluído | Solicitações válidas que verificam se algo foi alterado no servidor ou redirecionam a solicitação para outro recurso. Elas não têm conteúdo em si, portanto, não são faturáveis. |
| Solicitações em /libs/* | Excluído | Solicitações JSON internas de AEM, como o token CSRF que não é faturável. |
| Tráfego de ataques de DDOS | Excluído | Proteção DDOS. O AEM detecta automaticamente alguns dos ataques de DDOS e os bloqueia. Ataques de DDOS, se detectados, não são faturáveis. |
| Monitoramento do AEM as a Cloud Service New Relic | Excluído | Monitoramento global da AEM as a Cloud Service. |
| URL para clientes monitorarem o programa Cloud Service | Excluído | A Adobe recomenda que você use a URL para monitorar a disponibilidade ou a verificação de integridade externamente.<br><br>`/system/probes/health` |
| Serviço de aquecimento do pod do AEM as a Cloud Service | Excluído |
| Agente: skyline-service-warmup/1.* |
| Mecanismos de pesquisa, redes sociais e bibliotecas HTTP conhecidos (marcados pelo Fastly) | Excluído | Serviços conhecidos que visitam o site regularmente para atualizar seu índice de pesquisa ou serviço:<br><br>Exemplos:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Ask Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuiltWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsBot Google<br>· AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteImprove<br>· StashBot<br>· StatusCake<br>· YandexBot<br>· Claudebot |
| Excluir chamadas de Commerce integration framework | Excluído | As solicitações feitas ao AEM que são encaminhadas para o Commerce integration framework—a URL começa com `/api/graphql`—para evitar dupla contagem, elas não são faturáveis para o Cloud Service. |
| Excluir `manifest.json` | Excluído | O manifesto não é uma chamada de API. Está aqui para fornecer informações sobre como instalar sites da Web em um desktop ou telefone celular. O Adobe não deve contar a solicitação JSON para `/etc.clientlibs/*/manifest.json` |
| Excluir `favicon.ico` | Excluído | Embora o conteúdo retornado não deva ser HTML ou JSON, alguns cenários, como fluxos de autenticação SAML, foram observados para retornar favicons como HTML. Como resultado, os favicons são explicitamente excluídos da contagem. |
| Proxy CDN para um back-end diferente | Excluído | As solicitações roteadas para diferentes back-ends não AEM usando a técnica [Seletores de Origem CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) são excluídas, pois não atingem AEM. |
