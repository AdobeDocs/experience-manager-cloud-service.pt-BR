---
title: Monitoramento de uso real do AEM as a Cloud Service
description: Saiba mais sobre o Real Use Monitoring (RUM) , um serviço automatizado que permite monitorar a coleta de dados do lado do cliente.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: f3091a3868ac57150afd6f1640709ce3e9566bac
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Serviço de monitoramento de uso real para AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>O serviço de monitoramento de uso real, a coleta de dados no lado do cliente, é um serviço automatizado. Nenhuma configuração de cliente é necessária.

>[!INFO]
>
>O monitoramento do lado do cliente só funciona para clientes com o AEM (Adobe Experience Manager) Cloud Service versão **2024.5.16461** e superior.

## Visão geral {#overview}

O serviço RUM (Real Use Monitoring) é uma tecnologia de monitoramento de desempenho que monitora o tráfego do lado do cliente em um site ou aplicativo em tempo real. Esse serviço se concentra em coletar métricas e dados essenciais para otimizar o desempenho, monitorando os envolvimentos do site, em vez dos próprios usuários. Com o RUM, as métricas principais de desempenho são rastreadas desde o início do URL até que a solicitação seja enviada de volta ao navegador.

## Quem pode se beneficiar de um serviço de monitoramento de uso real? {#who-can-benefit-from-rum-service}

O Monitoramento de uso real ajuda os clientes e a Adobe a entender como os usuários finais interagem com os sites da AEM. O Monitoramento de uso real preserva a privacidade dos visitantes por meio de coleta e amostragem limitadas de dados - apenas uma pequena parte de todas as exibições de página é monitorada.

## Amostragem de dados do serviço de monitoramento de uso real {#rum-service-data-sampling}

As soluções tradicionais de análise da Web tentam coletar dados em cada visitante. O serviço de Monitoramento de uso real (RUM) da AEM captura apenas informações de uma pequena fração de exibições de página. O serviço deve ser amostrado e anonimizado em vez de ser um substituto para o Analytics. Por padrão, as páginas têm uma proporção de amostragem de 1:100. Os operadores do site não podem aumentar ou diminuir a taxa de amostragem neste momento. Para estimar o tráfego total com precisão, para cada 100 exibições de página, os dados são coletados de 1, fornecendo uma aproximação confiável do tráfego geral.

Como a decisão sobre se os dados serão coletados, ela é feita em uma base de exibição de página por exibição de página, e se torna praticamente impossível rastrear interações em várias páginas. Por design, o RUM não tem conceito de visitantes ou sessões, apenas de exibições de página.

## Quais dados são coletados? {#what-data-is-being-collected}

O serviço de monitoramento de uso real foi projetado para minimizar a coleta de dados. O conjunto completo de informações coletadas pelo RUM está listado abaixo:

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

## Como o Monitoramento de uso real funciona para um cliente {#how-rum-works-for-a-customer}

O Monitoramento de uso real monitora automaticamente o tráfego do lado do cliente. Como cliente do Adobe, você não precisa realizar nenhuma etapa adicional, pois esse serviço é perfeitamente integrado à sua configuração existente. Com o serviço de Monitoramento de uso real (RUM) disponível no mercado, você se beneficia automaticamente desse novo recurso. O serviço Monitoramento de uso real não expõe nenhuma métrica voltada para o cliente para monitoramento atualmente. Estamos trabalhando para fornecer essa funcionalidade a você o mais rápido possível.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Como o Adobe usa o monitoramento de uso real {#how-rum-data-is-being-used}

Os dados de Monitoramento de uso real são usados para os seguintes propósitos:

* Identificar e corrigir gargalos de desempenho para locais de clientes
* Para entender como o AEM interage com outros scripts (como análises, direcionamento ou bibliotecas externas) na mesma página, para aumentar a compatibilidade.
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their RUM data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede RUM data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by RUM.

1. **Limitations in capturing headless API/JSON calls**

   * RUM data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from RUM service data creates variances from the content requests measured by CDN Analytics.
-->

## Perguntas frequentes {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the RUM service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **As métricas &quot;Interação com a próxima pintura&quot;, &quot;Tempo até o primeiro byte&quot; e &quot;Primeira pintura com conteúdo&quot; estão sendo coletadas?**

   A interação com a próxima pintura (INP) e o Tempo até o Primeiro Byte (TTFB) são coletados.  A primeira tinta cheia de conteúdo não é coletada no momento.

1. **O caminho `/.rum` está bloqueado no meu site, como devo corrigir?**

   O caminho `/.rum` é necessário para que a coleção RUM funcione. Se você usar um CDN na frente do AEM as a Cloud Service do Adobe, certifique-se de que o caminho `/.rum` seja encaminhado para a mesma origem do AEM que o outro conteúdo do AEM. E certifique-se de que ele não seja ajustado de forma alguma.

1. **A coleção de RUM conta para solicitações de conteúdo para fins contratuais?**

   A biblioteca RUM e a coleção RUM não contam como solicitações de conteúdo e não aumentam o número relatado de exibições de página ou chamadas de API. Além disso, para clientes que usam CDN pronta para uso com o AEM as a Cloud Service, a [coleção do lado do servidor](#serverside-collection) é a base para solicitações de conteúdo.

1. **Como posso desabilitar o RUM?**

   A Adobe recomenda usar o Monitoramento de uso real (RUM) devido a seus benefícios significativos e que permitirá que a Adobe o ajude a otimizar suas experiências digitais melhorando o desempenho do site. O serviço foi projetado para ser ininterrupto e não tem impacto no desempenho do site.

   Recusar pode significar perder uma chance de melhorar o engajamento no tráfego do seu site. No entanto, se encontrar problemas, entre em contato com o Suporte da Adobe.