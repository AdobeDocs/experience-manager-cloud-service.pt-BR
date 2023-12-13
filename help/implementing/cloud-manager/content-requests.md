---
title: Noções básicas sobre solicitações de conteúdo Cloud Service
description: Se você adquiriu licenças de solicitação de conteúdo do Adobe, saiba mais sobre os tipos de solicitações de conteúdo que o Adobe Experience Cloud as a Service mede e as variações com as ferramentas de relatório de análise de uma organização.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: e31b05f0cef6c5ca3a1c00b757eac013aa43bb90
workflow-type: tm+mt
source-wordcount: '2690'
ht-degree: 4%

---

# Solicitações de conteúdo Cloud Service

## Introdução {#introduction}

As solicitações de conteúdo Cloud Service são medidas por meio da coleção de dados do lado do servidor. A coleção é habilitada por meio da análise de log da CDN.

>[!NOTE]
>Além disso, para um número [Clientes anteriores do Adobe](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter), a coleção do lado do cliente também será ativada por meio da medição RUM (Monitoramento de usuário real). Você pode saber mais consultando a documentação em [este artigo](#real-user-monitoring-for-aem-as-a-cloud-service).

## Noções básicas sobre solicitações de conteúdo Cloud Service {#understaing-cloud-service-content-requests}

As solicitações de conteúdo são coletadas automaticamente no lado do servidor, na borda do Adobe Experience Manager as a Cloud Service, por meio da análise automatizada dos arquivos de log originados do AEM as a Cloud Service CDN. Isso é feito isolando as solicitações que retornam o HTML `(text/html)` ou JSON `(application /Json)` conteúdo da CDN e com base em várias regras de inclusão e exclusão detalhadas abaixo. Uma solicitação de conteúdo ocorre independentemente do conteúdo retornado que está sendo veiculado a partir dos caches CDN ou do conteúdo que retorna à origem do CDN (despachantes AEM).

O Serviço de dados de monitoramento de usuário real (RUM) , a coleção no lado do cliente, oferece um reflexo mais preciso das interações do usuário, garantindo uma medida confiável do engajamento do site. Isso fornece aos clientes insights avançados sobre o tráfego e o desempenho da página. Embora isso seja benéfico para clientes que usam a CDN gerenciada por Adobe ou uma CDN não gerenciada por Adobe. Além disso, o relatório de tráfego automático agora pode ser ativado para clientes que usam um CDN não gerenciado por Adobe, eliminando a necessidade de compartilhar relatórios de tráfego com o Adobe.

Para clientes que acrescentam sua própria CDN ao AEM as a Cloud Service, os relatórios do lado do servidor resultarão em números que não podem ser usados para comparação com as solicitações de conteúdo licenciadas. Esses números terão de ser medidos pelo cliente na borda da CDN externa. Para esses clientes, relatórios do lado do cliente e desempenho associado, a variável [Serviço de Dados Adobe RUM](#real-user-monitoring-for-aem-as-a-cloud-service) é a opção Adobe recomendada. Consulte a [notas de versão](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter) para obter mais informações sobre como aceitar o.

## Coleção do lado do servidor {#serverside-collection}

Há regras em vigor para excluir bots conhecidos, incluindo serviços conhecidos que acessam o site regularmente para atualizar seu índice de pesquisa ou serviço.

### Variações de solicitações de conteúdo Cloud Service {#content-requests-variances}

As solicitações de conteúdo podem ter variações entre as ferramentas de relatório de Analytics de uma organização, conforme resumido na tabela a seguir. Em geral, *não* use ferramentas de análise que reúnem dados por meio de instrumentação do lado do cliente para relatar o número de solicitações de conteúdo para um determinado site, simplesmente porque elas geralmente dependem do consentimento do usuário para serem acionadas, perdendo uma fração significativa do tráfego. As ferramentas do Analytics que reúnem dados do lado do servidor em arquivos de log ou relatórios CDN para clientes que adicionam seu próprio CDN além do AEM as a Cloud Service fornecerão contagens melhores. Para gerar relatórios sobre Exibições de página e seu desempenho associado, o Serviço de dados de Adobe RUM é a opção recomendada de Adobe.

| Motivo da variação | Explicação |
|---|---|
| Consentimento do usuário final | As ferramentas do Analytics que dependem da instrumentação do lado do cliente geralmente dependem do consentimento do usuário para serem acionadas. Isso pode representar a maioria do tráfego que não está sendo rastreado. Para clientes que desejam medir solicitações de conteúdo por conta própria, é recomendável confiar nas ferramentas de análise que coletam relatórios do lado do servidor de dados ou CDN. |
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

### Tipos de solicitações de conteúdo incluídas {#included-content-requests}

| Tipo de solicitação | Solicitação de conteúdo | Descrição |
| --- | --- | --- |
| Código HTTP 100-299 | Incluído | Essas são solicitações regulares que fornecem conteúdo total ou parcial. |
| Bibliotecas HTTP para automação | Incluído | Exemplos:<br>· Amazon CloudFront<br>· Apache Http Client<br>· Cliente Http Assíncrono<br>· Axios<br>Azureus<br>· Curl<br>· Busca de nó no GitHub<br>· Quebra-cabeça<br>· Go-http-client<br>· Chrome Headless<br>· Cliente Java™<br>· Jersey<br>· Oembed de nó<br>· okhttp<br>· Solicitações Python<br>· Reator Netty<br>· Wget<br>WinHTTP |
| Ferramentas de monitoramento e verificação de integridade | Incluído | Elas são configuradas pelo cliente para monitorar um determinado aspecto do site. Por exemplo, disponibilidade ou desempenho real do usuário. Uso `/system/probes/health` e não as páginas de HTML reais do site.<br>Exemplos:<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatível; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>Mil Olhos-Libélula-x1<br>· OmtrBot/1.0<br>WebMon/2.0.0 |
| `<link rel="prefetch">` solicitações | Incluído | Para aumentar a velocidade de carregamento da próxima página, os clientes podem fazer com que o navegador carregue um conjunto de páginas antes que o usuário clique no link, de modo que já estejam no cache. *Mente: Isso está aumentando significativamente o tráfego*—dependendo de quantas dessas páginas são buscadas previamente. |
| Tráfego que bloqueia relatórios do Adobe Analytics ou Google Analytics | Incluído | É mais comum que os visitantes de sites tenham software de privacidade instalado (bloqueadores de anúncios e assim por diante) que afetam a precisão do Google Analytics ou do Adobe Analytics. O AEM as a Cloud Service conta as solicitações no primeiro ponto de entrada na infraestrutura operada pelo Adobe e não no lado do cliente. |

Consulte também [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md).

### Tipos de solicitações de conteúdo excluídas {#excluded-content-request}

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

## Coleção do cliente {#cliendside-collection}

### Monitoramento de usuário real (RUM) para AEM as a Cloud Service {#real-user-monitoring-for-aem-as-a-cloud-service}

>[!INFO]
>
>Esse recurso só está disponível para o programa de adoção antecipada.
>É necessário usar a versão do AEM Cloud Service **2023.11.14227** e superiores para habilitar o serviço de dados RUM.

### Visão geral {#overview}

O Monitoramento de usuário real (RUM) é um tipo de tecnologia de monitoramento de desempenho que captura e analisa as experiências de usuário digital de um site ou aplicativo em tempo real. Ele oferece visibilidade do desempenho em tempo real de uma aplicação web e fornece informações precisas sobre a experiência do usuário final.

O Monitoramento de usuário real (RUM) fornece informações detalhadas sobre as principais métricas de desempenho desde o início do URL até que a solicitação seja enviada de volta ao navegador, o que ajuda os desenvolvedores a aprimorar o aplicativo para facilitar o uso para os usuários finais.

### Quem pode se beneficiar do serviço de monitoramento de dados RUM? {#who-can-benefit-from-rum-data-monitoring-service}

O Serviço de dados de RUM é benéfico para quem utiliza a CDN de Adobe, pois oferece um reflexo mais preciso das interações do usuário, garantindo uma medida confiável do engajamento do site ao refletir o número de Exibições de página no lado do cliente que podem ser comparadas com as Exibições de página de log de CDN existentes no lado do servidor. Além disso, para clientes que usam seu próprio CDN, o Adobe agora pode simplificar os relatórios de tráfego automático que incluem Exibições de página para eles, o que significa que eles não precisam compartilhar nenhum relatório de tráfego com o Adobe.

Também é uma ótima oportunidade para obter insights avançados sobre o desempenho da sua página para os clientes que estão usando o CDN do Adobe e para aqueles que estão usando seu próprio CDN.

### Entender como funciona o serviço de dados do Real User Monitoring (RUM) {#understand-how-the-rum-data-service-works}

O Adobe Experience Manager usa o Monitoramento de usuário real (RUM) para ajudar os clientes e o Adobe a entender como os visitantes estão interagindo com sites alimentados pela Adobe Experience Manager, diagnosticar problemas de desempenho e medir a eficiência dos experimentos. O RUM preserva a privacidade dos visitantes por meio de amostragem — somente uma pequena parte de todas as exibições de página será monitorada — e da exclusão criteriosa de todas as informações de identificação pessoal (PII).

### Monitoramento do usuário real (RUM) e privacidade {#rum-and-privacy}

O monitoramento de usuário real no Adobe Experience Manager foi projetado para preservar a privacidade do visitante e minimizar a coleta de dados. Como visitante, isso significa que nenhuma informação pessoal será coletada pelo site que você está visitando ou disponibilizada para o Adobe.

Como operador de site, isso significa que não é necessária nenhuma aceitação adicional para ativar o monitoramento por meio desse recurso. Portanto, não haverá nenhum pop-up adicional para os usuários finais aceitarem para ativar o monitoramento de RUM.

### Amostragem de dados RUM {#rum-data-sampling}

As soluções tradicionais de análise da Web tentam coletar dados em cada visitante. O monitoramento de usuário real da Adobe Experience Manager captura apenas informações de uma pequena fração de visualizações de página. O Monitoramento de usuário real (RUM) deve ser amostrado e anonimizado em vez de um substituto para a análise. Por padrão, as páginas terão uma proporção de amostragem de 1:100. Os operadores do site não podem configurar esse número para aumentar ou diminuir a taxa de amostragem a partir de hoje. Para estimar com precisão o tráfego total, para cada 100 exibições de página, coletamos dados detalhados de uma, fornecendo uma aproximação confiável do tráfego geral.&quot;

Como a decisão sobre se os dados serão coletados é tomada em uma base de exibição de página por exibição de página, torna-se praticamente impossível rastrear interações em várias páginas. O RUM não tem conceito de visitas, visitantes ou sessões, apenas de exibições de página. Isto é por design.

### Quais dados estão sendo coletados {#what-data-is-being-collected}

O RUM (Real User Monitoring, monitoramento do usuário real) foi projetado para impedir a coleta de informações de identificação pessoal. O conjunto completo de informações que podem ser coletadas pelo Monitoramento de usuário real da Adobe Experience Manager está listado abaixo:

* O nome do host do site que está sendo visitado, por exemplo: `experienceleague.adobe.com`
* O tipo amplo de agente do usuário usado para exibir a página, como: desktop ou dispositivo móvel
* O horário da coleta de dados, como: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* O URL da página que está sendo visitada, por exemplo: `https://experienceleague.adobe.com/docs`
* O URL referenciador (o URL da página que se vinculou à página atual, se o usuário seguiu um link)
* Uma ID gerada aleatoriamente da exibição de página, em um formato semelhante a: `2Ac6`
* O peso ou o inverso da taxa de amostragem, por exemplo: `100`. Isso significa que somente uma em cada cem exibições de página será registrada
* O ponto de verificação ou nome de um evento específico na sequência de carregamento da página ou interação com ela como visitante
* A origem ou o identificador do elemento DOM com o qual o usuário interage para o ponto de verificação mencionado acima. Por exemplo, pode ser uma imagem
* O target ou link para uma página externa ou recurso com o qual o usuário interage para o ponto de verificação mencionado acima. Por exemplo: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* As métricas de desempenho dos Componentes principais da Web (CWV), o Maior renderizador de conteúdo (LCP), o Primeiro atraso de entrada (FID) e o Deslocamento de layout cumulativo (CLS) que descrevem a qualidade da experiência do visitante.

### Como configurar o serviço de dados de monitoramento de usuário real (RUM) {#how-to-set-up-them-rum-data-service}

* Se você deseja fazer parte de nosso programa de Primeiros usuários, envie um email para `aemcs-rum-adopter@adobe.com`, junto com o nome de domínio para o ambiente de produção, preparo e desenvolvimento a partir do endereço de email associado à Adobe ID. A equipe de produtos do Adobe habilitará o Serviço de dados de monitoramento de usuário real (RUM) para você.
* Depois de concluído, a equipe de produtos de colaboração do Adobe criará um Canal do cliente.
* A equipe de produtos do Adobe entrará em contato com você para fornecer a chave de domínio e o URL do painel de dados, onde é possível visualizar as Exibições de página e [Vídeos virtuais principais da Web (CWV)](https://web.dev/vitals/) métricas coletadas pela coleção Monitoramento de usuário real (RUM) do lado do cliente.
* Em seguida, você será orientado sobre como usar a chave de domínio para acessar o url do painel de dados e visualizar as métricas.

### Como os dados de RUM (Monitoramento de usuário real) estão sendo usados {#how-rum-data-is-being-used}

Os dados de RUM são benéficos para os seguintes propósitos:

* Identificar e corrigir gargalos de desempenho para locais de clientes
* Relatórios de tráfego simplificados e automáticos que incluem Exibições de página para clientes que usam seu próprio CDN, o que significa que eles não precisam compartilhar nenhum relatório de tráfego com o Adobe.
* Para entender como o Adobe Experience Manager interage com outros scripts (como análises, direcionamento ou bibliotecas externas) na mesma página, a fim de aumentar a compatibilidade.

### Limitações e noções básicas sobre a variação em exibições de página e métricas de desempenho {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Como você analisará esses dados, pode ou não haver variações nas exibições de página e outras métricas de desempenho relatadas pelo Monitoramento de usuário real (RUM). Essas variações podem ser atribuídas a vários fatores inerentes ao monitoramento em tempo real no lado do cliente. Estas são as principais considerações que os clientes devem ter em mente ao interpretar os dados de RUM:

1. **Bloqueadores de rastreadores**

   * Os usuários finais que utilizam bloqueadores de rastreadores ou extensões de privacidade podem impedir a coleta de dados do Real User Monitoring (RUM), pois essas ferramentas restringem a execução dos scripts de rastreamento. Essa restrição pode resultar em exibições de página e interações do usuário não relatadas, criando uma discrepância entre a atividade real do site e os dados capturados pelo RUM.

1. **Limitações na captura de chamadas API/JSON**

   * O serviço de dados RUM se concentra na experiência do lado do cliente e não captura a API de back-end ou as chamadas JSON no momento. A exclusão dessas chamadas dos dados de Monitoramento de usuário real (RUM) criará variações das solicitações de conteúdo medidas pelo CDN Analytics.

### Perguntas frequentes {#faq}

1. **Como posso configurar caminhos para incluir ou excluir no monitoramento?**

   Os clientes poderão definir caminhos para incluir ou excluir os URLs para monitoramento ao definir as variáveis de Ambiente na configuração no Cloud Manager usando estas variáveis: `AEM_WEBVITALS_EXCLUDE` e `AEM_WEBVITALS_INCLUDE_PATHS`

   Observe que, por padrão, a configuração &quot;incluir&quot; está definida como target &quot;/content&quot;. É importante lembrar que os caminhos que você precisa configurar aqui são caminhos de conteúdo no sistema, não os caminhos de URL que você vê no navegador. Essa distinção é fundamental para definir e personalizar com precisão sua configuração de acordo com suas necessidades específicas.

1. **O Adobe seria capaz de rastrear todas as exibições de página antes que a interação atinja o CDN gerenciado pelo cliente ou no ponto em que a interação atinja o CDN gerenciado pelo cliente?**

   Sim.

1. **Os clientes poderão integrar os scripts do serviço de dados RUM a sistemas de terceiros, como o Dynatrace?**

   Sim.

1. **As métricas de &quot;Interação com a próxima pintura&quot;, &quot;Tempo até o primeiro byte&quot; e &quot;Primeira pintura com conteúdo&quot; estão sendo coletadas?**

   A interação com a próxima tinta (INP) e o Time to first byte (TTFB) são coletados.  A primeira tinta cheia de conteúdo não é coletada no momento.
