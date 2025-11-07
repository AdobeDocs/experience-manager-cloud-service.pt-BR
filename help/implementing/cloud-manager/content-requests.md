---
title: Entender as solicitações de conteúdo do Cloud Service
description: Se você adquiriu licenças de solicitação de conteúdo do Adobe, saiba mais sobre os tipos de solicitações de conteúdo que o Adobe Experience Cloud as a Service mede e as variações com as ferramentas de relatório de análise de uma organização.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 2%

---

# Entender as solicitações de conteúdo do Cloud Service

## Introdução {#introduction}

As solicitações de conteúdo incluem solicitações enviadas ao AEM Sites. Essas solicitações podem ser roteadas por meio do Edge Delivery Services ou de sistemas de cache fornecidos pelo cliente, como uma Rede de entrega de conteúdo (CDN). Essas solicitações fornecem dados estruturados no formato HTML ou JSON e oferecem suporte a exibições de página (por exemplo, páginas e Fragmentos de experiência) ou retornos JSON por meio de APIs de forma headless.

O sistema conta as solicitações de conteúdo quando um usuário visualiza uma página usando o HTML ou JSON. Ele mede a solicitação no ponto em que o primeiro sistema de cache a recebe. Certas solicitações HTTP são incluídas ou excluídas para fins de contagem de solicitações de conteúdo. Veja a lista completa de HTTP [solicitações de conteúdo incluídas](#included-content-requests) e [solicitações de conteúdo excluídas](#excluded-content-request).

>[!NOTE]
>
>Os dados mostrados na exibição Solicitações de conteúdo são atualizados a cada 24 horas.

## Sobre solicitações de conteúdo do Cloud Service {#understanding-cloud-service-content-requests}

Uma *solicitação de página* refere-se a uma solicitação HTTP que recupera o conteúdo estruturado principal (por exemplo, HTML ou JSON) necessário para renderizar a experiência da página principal. Ela não inclui solicitações de ativos, como imagens ou scripts.

Para clientes que usam o CDN pronto para uso, o AEM as a Cloud Service conta as solicitações de conteúdo conforme medido no nível do servidor. Essa medição ocorre automaticamente e não depende do rastreamento de análises do cliente.

O AEM (Adobe Experience Manager) as a Cloud Service identifica solicitações de conteúdo com base nos tipos de resposta gerados pela instância do AEM e recebidas na CDN. Especificamente, as solicitações que retornam HTML (`text/html`) ou JSON (`application/json`) são contadas. Esses formatos normalmente fornecem conteúdo principal da página para renderização tradicional do site ou entrega headless.

As solicitações de ativos estáticos, como arquivos JavaScript, folhas de estilos CSS e imagens, não são contadas como solicitações de conteúdo.

>[!NOTE]
>Se uma solicitação de API retornar HTML ou JSON que sirva como conteúdo no nível da página (por exemplo, no delivery headless), ela ainda poderá ser contada como uma solicitação de conteúdo, dependendo de seu contexto.

As solicitações de conteúdo são medidas independentemente de a resposta ter sido fornecida pelo cache do CDN ou encaminhada para o ambiente de origem do AEM.

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Variações de solicitações de conteúdo do Cloud Service {#content-requests-variances}

As solicitações de conteúdo podem ter variações nas ferramentas de relatório de análise de uma organização, conforme resumido na tabela a seguir. Em geral, evite usar ferramentas de análise que dependam de instrumentação do lado do cliente para relatar o número de solicitações de conteúdo para um site. Essas ferramentas geralmente perdem uma grande parte do tráfego porque dependem do consentimento do usuário para serem ativadas. As ferramentas do Analytics que reúnem dados do lado do servidor em arquivos de log ou relatórios CDN para clientes que adicionam seu próprio CDN sobre o AEM as a Cloud Service fornecem contagens melhores.

| Motivo da variação | Explicação |
|---|---|
| Consentimento do usuário final | As ferramentas do Analytics que dependem da instrumentação do lado do cliente geralmente dependem do consentimento do usuário para serem acionadas. Esse workflow pode representar a maioria do tráfego que não está sendo rastreado. Para clientes que desejam medir solicitações de conteúdo por conta própria, a Adobe recomenda que você confie nas ferramentas de análise para coletar dados de relatórios do lado do servidor ou de CDN. |
| Marcação com tags | Todas as páginas ou chamadas de API que são rastreadas como solicitações de conteúdo do Adobe Experience Manager não podem ser marcadas com o rastreamento do Analytics. |
| Regras de gerenciamento de tags | As configurações das regras de gerenciamento de tags podem resultar em várias configurações de coleta de dados em uma página, resultando em alguma combinação de discrepâncias com o rastreamento de solicitação de conteúdo. |
| Bots | Os bots desconhecidos que o AEM não identificou previamente e removeu podem causar discrepâncias no rastreamento. |
| Report Suites | As páginas na mesma instância do AEM podem se reportar a diferentes conjuntos de relatórios do Analytics. Esse processo pode dividir dados em vários conjuntos, dependendo da configuração. |
| Ferramentas de segurança e monitoramento de terceiros | As ferramentas de verificação de monitoramento e segurança (por exemplo, verificadores de tempo de atividade ou verificadores de vulnerabilidade) podem solicitar páginas, gerando solicitações de conteúdo do lado do servidor não visíveis nos relatórios de análise. |
| Acesso à API | As solicitações para páginas ou conteúdo do AEM por meio de APIs (por exemplo, por meio do Adobe Experience Manager as a Headless CMS) ainda contam como solicitações de conteúdo, mas não acionam o rastreamento de análise. |
| Solicitações de pré-busca | A pré-busca (por exemplo, usando um service worker ou uma função de borda) pode aumentar os volumes de tráfego, solicitando páginas antecipadamente. Essas solicitações são contadas no lado do servidor, mas não executam o código de análise do lado do cliente. |
| DDOS | O Adobe usa a filtragem para detectar e bloquear muitos ataques de DDoS. No entanto, algumas solicitações de ataque ainda podem ser contadas como solicitações de conteúdo antes da aplicação dos filtros. |
| Bloqueadores de tráfego | Os recursos de privacidade no navegador ou firewalls corporativos podem bloquear o carregamento de scripts de análise. Esses usuários ainda geram solicitações de conteúdo do lado do servidor. |
| Firewalls | Os firewalls corporativos ou regionais podem impedir que as chamadas do Analytics cheguem aos servidores da Adobe, causando a subgeração de relatórios no Analytics enquanto as contagens do lado do servidor permanecem inalteradas. |

Consulte o [Painel de Licenças](/help/implementing/cloud-manager/license-dashboard.md) para obter informações sobre como visualizar e rastrear o uso de solicitações de conteúdo em relação aos limites da sua licença.

## Regras de coleção do lado do servidor {#serverside-collection}

O AEM as a Cloud Service aplica regras de coleção do lado do servidor para contar solicitações de conteúdo. Essas regras excluem bots conhecidos (como rastreadores de mecanismo de pesquisa) e um conjunto de serviços de monitoramento que fazem ping regular no site. Outro tráfego do tipo sintético ou de monitoramento que não esteja nessa lista de exclusão é contado como solicitações de conteúdo faturável.

As tabelas a seguir listam os tipos de solicitações de conteúdo incluídas e excluídas, com breves descrições de cada uma.

### Tipos de solicitações de conteúdo incluídas {#included-content-requests}

>[!NOTE]
>Se uma solicitação de API retornar uma resposta do HTML, ela poderá ser classificada como uma solicitação de conteúdo, dependendo de seu contexto de uso. As solicitações de API que retornam dados que não são da interface do usuário normalmente são excluídas.

| Tipo de solicitação | Solicitação de conteúdo | Descrição |
| --- | --- | --- |
| Código HTTP 100-299 | Incluído | Inclui solicitações bem-sucedidas que retornam conteúdo completo ou parcial do HTML ou JSON.<br>Código HTTP 206: essas solicitações fornecem apenas uma parte do conteúdo completo. Por exemplo, um vídeo ou uma imagem grande. As solicitações de conteúdo parcial são incluídas quando entregam parte de uma resposta HTML ou JSON usada na renderização do conteúdo da página. |
| Bibliotecas HTTP para automação | Incluído | Solicitações feitas por ferramentas ou bibliotecas que recuperam o conteúdo da página. Exemplos incluem o seguinte: <br>· Amazon CloudFront<br>· Apache Http Client<br>· Axios<br>· Azureus<br>· Curl<br>· Busca de Nó GitHub<br>· Guzzle<br>· Go-http-client<br>· Headless Chrome<br>· Java™ Client<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· Solicitações Python<br>· Reator Netty<br>· Wget<br>· WinHTTP<br>· HTTP<br>· Busca de Nó GitHub<br>· Netty de Reator<br> |
| Ferramentas de monitoramento e verificação de integridade | Incluído | Solicitações usadas para monitorar a integridade ou a disponibilidade de páginas.<br>Consulte [Tipos de solicitações de conteúdo excluídas](#excluded-content-request).<br>Os exemplos incluem o seguinte:<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatível; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` solicitações | Incluído | Quando os clientes fazem pré-carregamento ou pré-busca de conteúdo (por exemplo, com `<link rel="prefetch">`), o sistema conta essas solicitações do lado do servidor. Observe que essa abordagem pode aumentar o tráfego, dependendo de quantas dessas páginas são buscadas previamente. |
| Tráfego que bloqueia os relatórios do Adobe Analytics ou do Google Analytics | Incluído | É mais comum que os visitantes de sites tenham software de privacidade instalado (bloqueadores de anúncios e assim por diante) que afetam a precisão do Google Analytics ou do Adobe Analytics. O AEM as a Cloud Service conta as solicitações no primeiro ponto de entrada na infraestrutura operada pela Adobe e não no lado do cliente. |

Consulte também [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md).

### Tipos de solicitações de conteúdo excluídas {#excluded-content-request}

| Tipo de solicitação | Solicitação de conteúdo | Descrição |
| --- | --- | --- |
| Código HTTP 500+ | Excluído | Erros retornados ao visitante quando algo dá errado no AEM as a Cloud Service ou no código personalizado do cliente. |
| Código HTTP 400-499 | Excluído | Erros retornados ao visitante quando o conteúdo não existe (404) ou há outros problemas relacionados ao conteúdo ou à solicitação. |
| Código HTTP 300-399 | Excluído | Solicitações válidas que verificam se algo foi alterado no servidor ou redirecionam a solicitação para outro recurso. Elas não têm conteúdo em si, portanto, não são faturáveis. |
| Solicitações indo para `/libs/`* | Excluído | Solicitações JSON internas do AEM, como o token CSRF que não é faturável. |
| Tráfego de ataques de DDOS | Excluído | Proteção DDOS. O AEM detecta automaticamente alguns dos ataques de DDOS e os bloqueia. Ataques de DDOS, se detectados, não são faturáveis. |
| Monitoramento do AEM as a Cloud Service New Relic | Excluído | Monitoramento global da AEM as a Cloud Service. |
| URL para os clientes monitorarem o programa Cloud Service | Excluído | A Adobe recomenda que você use a URL para monitorar a disponibilidade ou a verificação de integridade externamente.<br><br>`/system/probes/health` |
| Serviço de aquecimento do pod do AEM as a Cloud Service | Excluído | Agente: skyline-service-warmup/1.* |
| Mecanismos de pesquisa, redes sociais e bibliotecas HTTP conhecidos (marcados pelo Fastly) | Excluído | Serviços conhecidos que visitam o site regularmente para atualizar seu índice de pesquisa ou serviço:<br><br>Exemplos:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Ask Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuiltWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsBot Google<br>· AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteImprove<br>· StashBot<br>· StatusCake<br>· YandexBot<br>· ContentKing<br>· Claudebot |
| Excluir chamadas do Commerce integration framework | Excluído | As solicitações feitas ao AEM que são encaminhadas para o Commerce integration framework — a URL começa com `/api/graphql` — para evitar dupla contagem, elas não são faturáveis para o Cloud Service. |
| Excluir `manifest.json` | Excluído | O manifesto não é uma chamada de API. Está aqui para fornecer informações sobre como instalar sites da Web em um desktop ou telefone celular. O Adobe não deve contar a solicitação JSON para `/etc.clientlibs/*/manifest.json` |
| Excluir `favicon.ico` | Excluído | Embora o conteúdo retornado não deva ser HTML ou JSON, alguns cenários, como fluxos de autenticação SAML, foram observados para retornar favicons como HTML. Como resultado, os favicons são explicitamente excluídos da contagem. |
| Fragmento de experiência (XF) - Reutilização do mesmo domínio | Excluído | Solicitações feitas a caminhos XF (como `/content/experience-fragments/...`) de páginas hospedadas no mesmo domínio (conforme identificado pelo cabeçalho Referenciador correspondente ao host da solicitação).<br><br> Exemplo: uma página inicial em `aem.customer.com` que obtém um XF para um banner ou cartão do mesmo domínio.<br><br>· A URL corresponde a /content/experience-fragments/...<br>· O domínio referenciador corresponde a `request_x_forwarded_host`<br><br>**Observação:** Se o caminho do Fragmento de Experiência for personalizado (por exemplo, usando `/XFrags/...` ou qualquer caminho fora de `/content/experience-fragments/`), a solicitação não será excluída e poderá ser contada, mesmo que seja do mesmo domínio. Recomendamos usar a estrutura de caminho XF padrão do Adobe para garantir que a lógica de exclusão se aplique corretamente. |

## Gerenciamento de solicitações de conteúdo {#managing-content-requests}

Conforme mencionado na seção [Variações de solicitações de conteúdo do Cloud Service](#content-requests-variances), as solicitações de conteúdo podem ser maiores do que o esperado devido a vários motivos, com um thread comum sendo direcionado ao tráfego na CDN.  Como cliente do AEM, você pode monitorar e gerenciar suas solicitações de conteúdo para que se ajustem ao orçamento de licença.  O gerenciamento de solicitações de conteúdo geralmente é uma combinação de técnicas de implementação e [regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md).

### Técnicas de implementação para gerenciar solicitações de conteúdo {#implementation-techniques-to-manage-crs}

* Certifique-se de que todas as respostas de Página não encontrada sejam entregues com o status HTTP 404.  Se forem retornados com um status 200, eles serão contabilizados nas solicitações de conteúdo.
* Rotear a verificação de integridade ou as ferramentas de monitoramento para o URL /systems/probes/health, ou usar o método HEAD em vez do GET para evitar a ocorrência de solicitações de conteúdo.
* Equilibre suas necessidades de atualização de conteúdo com o custo de licença da AEM para qualquer rastreador de pesquisa personalizado que você integrou ao seu site.  Um rastreador excessivamente agressivo pode consumir muitas solicitações de conteúdo.
* Procure qualquer redirecionamento no lado do servidor (status 301 ou 302) em vez de no lado do cliente (status 200 com redirecionamento do javascript) para evitar duas solicitações de conteúdo separadas.
* Combine ou reduza chamadas de API, que são respostas JSON do AEM que podem ser carregadas para renderizar a página.

### Regras de filtro de tráfego para gerenciar solicitações de conteúdo {#traffic-filter-rules-to-manage-crs}

* Um padrão de bot comum é usar um agente de usuário vazio.  Será necessário analisar os padrões de implementação e tráfego para ver se o agente de usuário vazio é útil ou não.  Se você quiser bloquear esse tráfego, a [sintaxe](/help/security/traffic-filter-rules-including-waf.md#rules-syntax) recomendada é:

```
trafficFilters:
  rules:
    - name: block-missing-user-agent
      when:
        anyOf:
          - { reqHeader: user-agent, exists: false }
          - { reqHeader: user-agent, equals: '' }
      action: block
```

* Alguns bots atingem um site muito fortemente um dia e desaparecem no seguinte.  Isso pode frustrar qualquer tentativa de bloquear um endereço IP ou agente do usuário específico.  Uma abordagem genérica é introduzir uma [regra de limite de taxa](/help/security/traffic-filter-rules-including-waf.md#rate-limit-rules).  Revise os [exemplos](/help/security/traffic-filter-rules-including-waf.md#ratelimiting-examples) e crie uma regra que corresponda à sua tolerância para uma taxa rápida de solicitações.  Revise a sintaxe [Estrutura de Condição](/help/security/traffic-filter-rules-including-waf.md#condition-structure) para quaisquer exceções que você queira permitir para um limite de taxa genérico.
