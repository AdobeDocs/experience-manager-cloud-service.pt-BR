---
title: Noções básicas sobre solicitações de conteúdo Cloud Service
description: Se você adquiriu licenças de solicitação de conteúdo do Adobe, saiba mais sobre os tipos de solicitações de conteúdo que o Adobe Experience Cloud as a Service mede e as variações com as ferramentas de relatório de análise de uma organização.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 9%

---

# Solicitações de conteúdo Cloud Service

## Variações de solicitações de conteúdo Cloud Service{#content-requests-variances}

As solicitações de conteúdo podem ter variações entre as ferramentas de relatório de Analytics de uma organização, conforme resumido na tabela a seguir. Em geral, as ferramentas do Analytics que reúnem dados por meio de instrumentação do lado do cliente <b>não deve ser usado</b> relatar o número de solicitações de conteúdo para um determinado site, simplesmente porque elas geralmente dependem do consentimento do usuário final para serem acionadas, perdendo uma fração significativa do tráfego. As ferramentas do Analytics que reúnem dados do lado do servidor em arquivos de log ou relatórios CDN para clientes que adicionam seu próprio CDN além do AEM as a Cloud Service fornecerão contagens melhores. Para relatórios sobre Exibições de página, bem como seu desempenho associado, o Serviço de dados de Adobe RUM é a opção recomendada de Adobe.

| Motivo da variação | Explicação |
|---|---|
| Consentimento do usuário final | As ferramentas do Analytics que dependem da instrumentação do lado do cliente geralmente dependem do consentimento do usuário final para serem acionadas. Isso pode representar a maioria do tráfego que não está sendo rastreado. Para clientes que desejam medir solicitações de conteúdo por conta própria, é recomendável confiar nas ferramentas de análise que coletam relatórios do lado do servidor de dados ou CDN. |
| Marcação com tags | Todas as páginas ou chamadas de API que são rastreadas como solicitações de conteúdo do Adobe Experience Manager (AEM) podem não ser marcadas com o rastreamento do Analytics. |
| Regras de gerenciamento de tags | As configurações das regras de gerenciamento de tags podem resultar em várias configurações de coleta de dados em uma página, resultando em alguma combinação de discrepâncias com o rastreamento de solicitação de conteúdo. |
| Bots | Os bots desconhecidos que não foram pré-identificados e removidos pelo AEM podem causar discrepâncias no rastreamento. |
| Report Suites | As páginas que fazem parte de uma mesma instância e domínio do AEM podem enviar dados para diferentes conjuntos de relatórios de Analytics. |
| Ferramentas de segurança e monitoramento de terceiros | Ferramentas de verificação para monitoramento e segurança podem gerar solicitações de conteúdo para o AEM que não são rastreadas nos relatórios de Analytics. |
| Acesso à API | O acesso programático a páginas ou APIs do Adobe Experience Manager pode gerar solicitações de conteúdo para AEM que não são rastreadas nos relatórios do Analytics. |
| Solicitações de pré-busca | Usar um serviço de pré-busca para pré-carregar páginas a fim de aumentar a velocidade pode causar um aumento significativo no tráfego de solicitações de conteúdo. |
| DDOS | Enquanto o Adobe faz tentativas de detectar e filtrar automaticamente o tráfego de ataques de DDOS, não há garantia de que todos os possíveis ataques de DDOS sejam detectados. |
| Bloqueadores de tráfego | O uso de um bloqueador de rastreadores em um navegador pode impedir o rastreamento de algumas solicitações. |
| Firewalls | Os firewalls podem bloquear o rastreamento do Analytics. Esse cenário é mais frequente com firewalls corporativos. |

Consulte também [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md).

## Noções básicas sobre solicitações de conteúdo Cloud Service {#about-content-request}

As solicitações de conteúdo são rastreadas automaticamente na borda do Adobe Experience Manager (AEM) as a Cloud Service AEM, por meio da análise automatizada dos arquivos de log originados do CDN as a Cloud Service, isolando as solicitações que retornam o conteúdo HTML (text/html) ou JSON (application/json) do CDN e com base em várias regras de inclusão e exclusão detalhadas abaixo. Uma solicitação de conteúdo acontece independentemente do conteúdo retornado que está sendo veiculado a partir dos caches CDN ou retornando à origem do CDN (despachantes AEM).

Para clientes que trazem seu próprio CDN além do AEM as a Cloud Service, esse rastreamento resultará em números que não podem ser usados para comparação com as solicitações de conteúdo licenciadas, que terão de ser medidos pelo cliente na borda do CDN externo.

Há regras em vigor para excluir bots conhecidos, incluindo serviços conhecidos que acessam o site regularmente para atualizar seu índice de pesquisa ou serviço.

### Tipos de solicitações de conteúdo incluídas{#included-content-requests}

| Tipo de solicitação | Solicitação de conteúdo | Descrição |
| --- | --- | --- |
| Código HTTP 100-299 | Incluído | Essas são solicitações regulares que fornecem conteúdo total ou parcial. |
| Bibliotecas HTTP para automação | Incluído | Exemplos:<br>· Amazon CloudFront<br>· Apache Http Client<br>· Cliente Http Assíncrono<br>· Axios<br>Azureus<br>· Curl<br>· Busca de nó no GitHub<br>· Quebra-cabeça<br>· Go-http-client<br>· Chrome Headless<br>· Cliente Java™<br>· Jersey<br>· Oembed de nó<br>· okhttp<br>· Solicitações Python<br>· Reator Netty<br>· Wget<br>WinHTTP |
| Ferramentas de monitoramento e verificação de integridade | Incluído | Elas são configuradas pelo cliente para monitorar um determinado aspecto do site. Por exemplo, disponibilidade ou desempenho real do usuário. Uso `/system/probes/health` e não as páginas de HTML reais do site.<br>Exemplos:<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatível; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>Mil Olhos-Libélula-x1<br>· OmtrBot/1.0<br>WebMon/2.0.0 |
| `<link rel="prefetch">` solicitações | Incluído | Para aumentar a velocidade de carregamento da próxima página, os clientes podem fazer com que o navegador carregue um conjunto de páginas antes que o usuário clique no link, de modo que já estejam no cache. *Mente: Isso está aumentando significativamente o tráfego*—dependendo de quantas dessas páginas são buscadas previamente. |
| Tráfego que bloqueia relatórios do Adobe Analytics ou Google Analytics | Incluído | É mais comum que os visitantes de sites tenham software de privacidade instalado (bloqueadores de anúncios e assim por diante) que afetam a precisão do Google Analytics ou do Adobe Analytics. O AEM as a Cloud Service conta as solicitações no primeiro ponto de entrada na infraestrutura operada pelo Adobe e não no lado do cliente. |

Consulte também [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md).

### Tipos de solicitações de conteúdo excluídas{#excluded-content-request}

| Tipo de solicitação | Solicitação de conteúdo | Descrição |
| --- | --- | --- |
| Código HTTP 500+ | Excluído | Os erros retornam ao visitante quando algo dá errado no AEM as a Cloud Service ou no código personalizado do cliente. |
| Código HTTP 400-499 | Excluído | Erros retornados ao visitante quando o conteúdo não existe (404) ou há outros problemas relacionados ao conteúdo ou à solicitação. |
| Código HTTP 300-399 | Excluído | Essas são boas solicitações que verificam se algo foi alterado no servidor ou redirecionam a solicitação para outro recurso. Elas não têm conteúdo em si, portanto, não são faturáveis. |
| Solicitações em /libs/* | Excluído | Solicitações JSON internas de AEM, como o token CSRF que não é faturável. |
| Tráfego de ataques de DDOS | Excluído | Proteção DDOS. O AEM detecta automaticamente alguns dos ataques de DDOS e os bloqueia. Ataques de DDOS, se detectados, não são faturáveis. |
| Monitoramento as a Cloud Service do AEM na NewRelic | Excluído | Monitoramento global as a Cloud Service do AEM. |
| URL para clientes monitorarem o programa Cloud Service | Excluído | URL recomendado para monitorar externamente a disponibilidade.<br><br>`/system/probes/health` |
| Serviço de aquecimento de pod as a Cloud Service AEM | Excluído | Agente do usuário: skyline-service-warmup/1.* |
| Mecanismos de pesquisa, redes sociais e bibliotecas HTTP conhecidos (marcados pelo Fastly) | Excluído | Serviços conhecidos acessam o site regularmente para atualizar seu índice de pesquisa ou serviço:<br><br>Exemplos:<br>· AddSearchBot<br>AhrefsBot<br>· Applebot<br>· Pergunte a Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· Criado com<br>· Bytespider<br>CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsBot<br>· Google AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>LucidWorks<br>· MJ12bot<br>· PKingdom<br>· Pinterest<br>· SemrushBot<br>· SiteImprove<br>· StashBot<br>· StatusCake<br>· YandexBot |
| Excluir chamadas de Commerce integration framework | Excluído | Essas são solicitações feitas ao AEM que são encaminhadas ao Commerce integration framework — o URL começa com `/api/graphql`—para evitar dupla contagem, não são faturáveis por Cloud Service. |
| Excluir `manifest.json` | Excluído | O manifesto não é uma chamada de API, ele está aqui para fornecer informações sobre como instalar sites da Web em um desktop ou celular. O Adobe não deve contar a solicitação JSON para `/etc.clientlibs/*/manifest.json` |
| Excluir `favicon.ico` | Excluído | Embora o conteúdo retornado não deva ser HTML ou JSON, estamos observando que em alguns cenários, como fluxos de autenticação SAML, favicons podem ser retornados como HTML, portanto, são explicitamente excluídos da contagem. |
