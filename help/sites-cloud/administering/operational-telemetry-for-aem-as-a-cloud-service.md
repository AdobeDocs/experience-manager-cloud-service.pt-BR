---
title: Telemetria operacional do AEM as a Cloud Service
description: Saiba mais sobre a Telemetria operacional, um serviço automatizado que permite monitorar a coleção de dados do lado do cliente.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 100a8cd1a27cd8f0677ed001def0b1e0e7b20ed3
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 0%

---

# Serviço de Telemetria Operacional para o AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>O serviço de Telemetria Operacional, a coleção de dados do lado do cliente, é um serviço automatizado. Nenhuma configuração de cliente é necessária.

>[!INFO]
>
>O monitoramento do lado do cliente só funciona para clientes com o AEM (Adobe Experience Manager) Cloud Service versão **2024.5.16461** e superior.

## Visão geral {#overview}

O serviço de Telemetria Operacional é uma tecnologia de monitoramento de desempenho que monitora o tráfego do lado do cliente em um site ou aplicativo em tempo real. Esse serviço se concentra em coletar métricas e dados essenciais para otimizar o desempenho, monitorando os envolvimentos do site, em vez dos próprios usuários. Com a Telemetria Operacional, as métricas principais de desempenho são rastreadas desde o início do URL até que a solicitação seja enviada de volta ao navegador.

## Quem pode se beneficiar do serviço de Telemetria Operacional? {#who-can-benefit-from-operational-telemetry-service}

A Telemetria operacional ajuda os clientes e a Adobe a entender como os usuários finais interagem com os sites do AEM. A telemetria operacional preserva a privacidade dos visitantes por meio da coleta e amostragem limitadas de dados. Somente uma pequena parte de todas as exibições de página é monitorada.

## Amostragem de dados do serviço de telemetria operacional {#operational-telemetry-service-data-sampling}

As soluções tradicionais de análise da Web tentam coletar dados em cada visitante. O serviço de Telemetria operacional da AEM captura apenas informações de uma pequena fração de visualizações de página. O serviço deve ser amostrado e anonimizado em vez de ser um substituto para o Analytics. Por padrão, as páginas têm uma taxa de amostragem de 1:100. Os operadores do site não podem aumentar ou diminuir a taxa de amostragem neste momento. Para estimar o tráfego total com precisão, para cada 100 exibições de página, os dados são coletados de 1, fornecendo uma aproximação confiável do tráfego geral.

Como a decisão sobre se os dados serão coletados, ela é feita em uma base de exibição de página por exibição de página, e se torna praticamente impossível rastrear interações em várias páginas. Por design, a Telemetria Operacional não tem conceito de visitantes ou sessões, apenas de exibições de página.

## Quais dados são coletados? {#what-data-is-being-collected}

O serviço de Telemetria Operacional foi projetado para minimizar a coleta de dados. O conjunto completo de informações coletadas pela Telemetria Operacional está listado abaixo:

* O nome de host do site que está sendo visitado, por exemplo: `experienceleague.adobe.com`
* O tipo amplo de agente de usuário e sistema operacional que é usado para exibir a página, como: `desktop:windows` ou `mobile:ios`
* A hora da coleta de dados, como: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* A URL da página que está sendo visitada, por exemplo: `https://experienceleague.adobe.com/docs`
* O URL referenciador (o URL da página que se vinculou à página atual, se o usuário seguiu um link)
* Uma ID gerada aleatoriamente da exibição de página, em um formato semelhante a: `2Ac6`
* O peso ou o inverso da taxa de amostragem, como: `100`. Significa que somente uma em cada cem exibições de página é registrada
* O ponto de verificação ou nome de um evento específico na sequência de carregamento da página. Ou, interagindo com ele como visitante
* A origem ou o identificador do elemento DOM com o qual o usuário interage para o ponto de verificação mencionado acima. Por exemplo, pode ser uma imagem
* O target ou link para uma página externa ou recurso com o qual o usuário interage para o ponto de verificação mencionado acima. Por exemplo: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* As [Métricas de desempenho do Core Web Vitals (CWV)](https://web.dev/articles/lcp) [LCP (Largest Contentful Paint)](https://web.dev/articles/lcp), [INP (Interaction to Next Paint)](https://web.dev/articles/inp) e [CLS (Cumulative Layout Shift)](https://web.dev/articles/cls) que descrevem a qualidade de experiência do visitante.

## Como a telemetria operacional funciona para um cliente {#how-operational-telemetry-works-for-a-customer}

A Telemetria Operacional monitora automaticamente o tráfego do lado do cliente. Como cliente do Adobe, você não precisa realizar nenhuma etapa adicional, pois esse serviço é perfeitamente integrado à sua configuração existente. Com o serviço de Telemetria Operacional disponível no mercado, você se beneficia automaticamente desse novo recurso. O serviço de Telemetria Operacional não expõe nenhuma métrica voltada para o cliente para monitoramento atualmente. Estamos trabalhando para fornecer essa funcionalidade a você o mais rápido possível.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Como o Adobe usa a Telemetria Operacional {#how-operational-telemetry-data-is-being-used}

Os dados de Telemetria Operacional são usados para os seguintes propósitos:

* Identificar e corrigir gargalos de desempenho para locais de clientes
* Para entender como o AEM interage com outros scripts (como análises, direcionamento ou bibliotecas externas) na mesma página, para aumentar a compatibilidade.
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their Operational Telemetry data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede Operational Telemetry data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by Operational Telemetry.

1. **Limitations in capturing headless API/JSON calls**

   * Operational Telemetry data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from Operational Telemetry service data creates variances from the content requests measured by CDN Analytics.
-->

## Perguntas frequentes {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the Operational Telemetry service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **As métricas &quot;Interação com a próxima pintura&quot;, &quot;Tempo até o primeiro byte&quot; e &quot;Primeira pintura com conteúdo&quot; estão sendo coletadas?**

   A interação com a próxima pintura (INP) e o Tempo até o Primeiro Byte (TTFB) são coletados.  A primeira tinta cheia de conteúdo não é coletada no momento.

1. **O caminho `/.rum` está bloqueado no meu site, como devo corrigir?**

   O caminho `/.rum` é necessário para que a coleção de Telemetria Operacional funcione. Se você usar um CDN na frente do AEM as a Cloud Service do Adobe, certifique-se de que o caminho `/.rum` seja encaminhado para a mesma origem do AEM que o outro conteúdo do AEM. E certifique-se de que ele não seja ajustado de forma alguma. Como alternativa, você pode alterar o host a ser usado para a Telemetria Operacional `rum.hlx.page`, [definindo uma variável de ambiente no Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables) chamada `AEM_OPTEL_EXTERNAL` para o valor `true`. Se você quiser voltar para as mesmas solicitações de domínio posteriormente, basta remover essa variável de ambiente novamente.

1. **A coleção de Telemetria Operacional conta para solicitações de conteúdo para fins contratuais?**

   A biblioteca de Telemetria operacional e a coleção de Telemetria operacional não contam como solicitações de conteúdo e não aumentam o número relatado de exibições de página ou chamadas de API. Além disso, para clientes que usam CDN pronta para uso com o AEM as a Cloud Service, a [coleção do lado do servidor](#serverside-collection) é a base para solicitações de conteúdo.

1. **Como posso desabilitar a Telemetria Operacional?**

   A Adobe recomenda usar a Telemetria operacional devido aos seus benefícios significativos e que permitirá que a Adobe o ajude a otimizar suas experiências digitais melhorando o desempenho do site. O serviço foi projetado para ser ininterrupto e não tem impacto no desempenho do site.

   Recusar pode significar perder uma chance de melhorar o engajamento no tráfego do seu site. No entanto, se você encontrar problemas, poderá desabilitar a Telemetria Operacional [definindo uma variável de ambiente no Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables) chamada `AEM_OPTEL_DISABLED` para o valor `true`. Se você quiser ativar a Telemetria operacional novamente em um ponto posterior, basta remover essa variável de ambiente novamente.

1. **Posso usar uma Política de Segurança de Conteúdo com um Nonce?**

   O suporte para Telemetria Operacional contém um recurso experimental para dar suporte a uma Política de Segurança de Conteúdo com um nonce. Este recurso pode ser habilitado por [configuração de uma variável de ambiente no Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables) chamada `AEM_OPTEL_NONCE` para o valor `true`. Se quiser desabilitar novamente em um ponto posterior, basta remover essa variável de ambiente novamente.

   Se você encontrar problemas com esse recurso, entre em contato com o Suporte da Adobe.

1. **Como posso habilitar a Telemetria Operacional apenas para determinadas páginas?**

   Por padrão, a Telemetria Operacional está habilitada para todas as páginas abaixo da pasta `/content` no repositório. Ao [definir uma variável de ambiente no Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables) chamada `AEM_OPTEL_INCLUDED_PATHS` para uma lista de caminhos separados por vírgula no repositório, a Telemetria Operacional só será habilitada para essas páginas. Além disso, você pode definir `AEM_OPTEL_EXCLUDED_PATHS` para uma lista de caminhos no repositório que serão excluídos. Com a combinação dessas duas configurações, você pode ajustar a inclusão da Telemetria Operacional de acordo com seus requisitos.

