---
title: Monitoramento de uso real para AEM como Cloud Service
description: Aprenda a usar o Monitoramento de uso real (RUM) para capturar e analisar as experiência do usuário digitais de um site ou aplicativo em tempo real.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 9a8adf777008b7a601abc8760cee67ec3c1816c6
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---

# Serviço de monitoramento de uso real para AEM como Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>O serviço de Monitoramento de uso real, o lado do cliente coleção dos dados, é um serviço automatizado. Nenhuma configuração de cliente é necessária.

>[!INFO]
>
>O monitoramento do lado do cliente funciona apenas para clientes com AEM Cloud Service versão **2024.5.16461** e superior.

## Visão geral {#overview}

O serviço monitoramento de uso real (RUM) é uma tecnologia de monitoramento de desempenho que captura e analisa as experiências de usuário digitais de um site ou aplicativo em tempo real. Ela proporciona visibilidade para o desempenho em tempo real de uma aplicativo web e fornece uma insight mais profunda no final experiência do usuário. O serviço foca na otimização do desempenho monitorando os envolvimentos do site, e não os próprios usuários.

Com o RUM, as principais métricas de desempenho são rastreadas desde o início da URL até que a solicitação seja servida de volta ao navegador. Isso ajuda os desenvolvedores a aprimorar as aplicativo para facilitar o uso para os usuários finais.

>[!INFO]
>
>O &quot;Monitoramento real de usuários&quot; foi reformulado para &quot;Monitoramento de uso real&quot;, pois reflete melhor a verdadeira essência do serviço.

## Quem pode se beneficiar de um serviço de monitoramento de uso real? {#who-can-benefit-from-rum-service}

O serviço de Monitoramento de uso real é benéfico para todos os clientes. Oferece um reflexo representativo das interações usuário, garantindo uma medir confiável dos envolvimento do site capturando o número de visualizações lado do cliente página.

Para todos os Adobe Systems clientes, esse serviço fornece insights valiosos sobre interações usuário. Os clientes que empregam suas próprias CDN podem se beneficiar de tráfego relatórios simplificadas, uma vez que Adobe Systems integra diretamente o coleção de dados, eliminando a necessidade de relatórios separados durante os ciclos de renovação.

## Entenda como funciona o serviço de monitoramento de uso real {#understand-how-the-rum-service-works}

Adobe Experience Manager (AEM) usa o Monitoramento de uso real (RUM) para ajudar os clientes e os Adobe Systems a entender como os visitantes interagem com sites AEM. Ajuda a diagnosticar problemas de desempenho e medir a eficácia dos experimentos. O RUM preserva a privacidade dos visitantes por meio de amostragem - apenas uma pequena parte de todas as página exibições é monitorada - e nenhuma informação pessoalmente identificável (PII) é coletada.

## Serviço de monitoramento de uso real e privacidade {#rum-service-and-privacy}

O serviço de Monitoramento de uso real no AEM foi projetado para preservar visitante privacidade e minimizar coleção de dados. Como visitante, significa que o site que você está visitando ou disponibilizado para Adobe Systems não coleta nenhuma informação pessoal.

Como operador de site, não é necessário aceitar adicionais para permitir o monitoramento através desse recurso. Não há pop-up adicional ou formulário de consentimento para os usuários finais aceitarem para ativar o RUM.

## Amostra de dados do serviço de monitoramento de uso real {#rum-service-data-sampling}

As soluções tradicionais do análise da web tentam coletar dados em cada visitante. O serviço RUM da AEM captura apenas informações de uma pequena fração de exibições do página. O serviço deve ser amostrado e anônimo, em vez de um substituto para análise. Por padrão, as páginas têm uma taxa de 1:100 amostragem. Os operadores de site não podem aumentar ou diminuir a taxa de amostragem neste momento. Para estimar o total tráfego com precisão, a cada 100 visualizações página, os dados são coletados a partir de 1, fornecendo uma aproximação confiável de tráfego geral.

Como a decisão de se os dados são coletados, eles são feitos em um exibição de página exibição de página base, e torna-se virtualmente impossível faixa interações em várias páginas. Por design, o RUM não tem o conceito de visitantes ou sessões, somente de visualizações página.

## Quais dados estão sendo coletados {#what-data-is-being-collected}

O serviço de Monitoramento de uso real foi projetado para impedir o coleção de informações pessoalmente identificáveis. O conjunto completo de informações coletadas pelo RUM está listado abaixo:

* O host nome do site que está sendo visitado, por exemplo: `experienceleague.adobe.com`
* O amplo tipo de agente usuário e o sistema operacional usado para exibir as página, como: `desktop:windows` ou `mobile:ios`
* A hora do coleção de dados, como: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* A URL da página visitada instância: `https://experienceleague.adobe.com/docs`
* A URL do Referenciador (a URL do página vinculado ao página atual, se o usuário seguido de uma link)
* Uma ID gerada aleatoriamente do exibição de página, em um formato semelhante a: `2Ac6`
* A peso ou o inverso da taxa de amostragem, como: `100`. Significa que apenas uma em cada cem página visualizações é registrada
* A ponto de verificação ou nome de uma determinada evento na sequência de carregamento da página. Ou interagir com ela como uma visitante
* A origem ou identificador do elemento DOM com o qual o usuário interage para o ponto de verificação mencionado acima. Por instância, pode ser uma imagem
* A Direcionamento ou link a um página ou recurso externo com o qual a usuário interage para o ponto de verificação mencionado acima. Por exemplo: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* As principais métricas de desempenho de Vital da Web (CWV), incluindo o Maior Contentful Paint (LCP), First Input Delay (FID), Cumulative Layout Shift (CLS) e Time To First Byte (TTFB) que descrevem a qualidade do visitante de experiência.

## Como o monitoramento de uso real funciona para um cliente {#how-rum-works-for-a-customer}

O Monitoramento de uso real monitora automaticamente os lado do cliente tráfego para fornecer insights valiosos. Como um cliente Adobe Systems, você não precisa tomar etapas adicionais, pois este serviço é perfeitamente integrado à sua configuração existente. Com a disponibilidade geral (GA) implantação, você se beneficia automaticamente desse novo recurso.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Como os dados do serviço de monitoramento de uso real estão sendo usados {#how-rum-service-data-is-being-used}

Os dados RUM são benéficos para os seguintes fins:

* Para identificar e corrigir afunilamentos de desempenho para sites de clientes
* Para simplificar a pesquisa de tráfego automatizada que inclui exibições página.
* Para entender como AEM interage com outros scripts (como análise, direcionamento ou bibliotecas externos) no mesmo página, para aumentar a compatibilidade.

## Limitações e no entendimento da variação em Página exibições e métricas de desempenho {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

À medida que você analisa os dados do RUM, pode haver variações nas exibições de página e outras métricas de desempenho. Essas variações podem ser atribuídas a vários fatores inerentes ao monitoramento lado do cliente tempo real. Veja a seguir as principais considerações que os clientes devem ter em mente ao interpretar seus dados de RUM:

1. **Bloqueadores do rastreador**

   * Os usuários finais que empregam bloqueadores de rastreadores ou extensões de privacidade podem impedir o RUM coleção de dados, uma vez que essas ferramentas restringem a execução rastreamento scripts de rastreamento. Essa restrição pode cliente potencial a exibições página subnotificadas e interações usuário, criando uma discrepância entre o atividade do site real e os dados capturados pelo RUM.

1. **Limitações na captura de chamadas de API/JSON sem cabeça**

   * O serviço de dados RUM se concentra no lado do cliente experiência e não captura as chamadas de API de back-end ou JSON feitas de um aplicativo sem AEM sem cabeça no momento. A exclusão dessas chamadas dos dados do serviço RUM cria variações a partir das solicitações de conteúdo medidas por CDN Analytics.

## Perguntas frequentes {#faq}


1. **Os clientes podem integrar os scripts do serviço RUM a sistemas de terceiros curtir o Dynatrace?**

   Sim.

1. **A &quot;Interação para a próxima pintura&quot;, &quot;Hora do primeiro byte&quot; e &quot;Primeira tinta contentful&quot; é vital para as métricas da Web que estão sendo coletadas?**

   Interação à próxima pintura (INP) e Tempo para byte primeiro (TTFB) são coletadas.  A primeira tinta contentful não é coletada no momento.

1. **O `/.rum` caminho está bloqueado no meu site, como devo corrigir?**

   O `/.rum` caminho é necessário para que o RUM coleção funcione. Se você tiver uma CDN à frente do que Adobe Systems fornece como parte da AEM como uma Cloud Service, certifique-se de que o `/.rum` caminho avança para o mesmo AEM origem que o resto de seus AEM conteúdo. E, certifique-se de que não esteja ajustado de forma alguma.

1. **A RUM coleção conta para conteúdo solicitações para fins contratuais?**

   O biblioteca RUM e o RUM coleção não contam como solicitações de conteúdo e não aumentam o número relatado de exibições de página ou chamadas à API. Além disso, para clientes que usam CDN prontos para uso com AEM como Cloud Service, [lado do servidor coleção](#serverside-collection) é a base para solicitações conteúdo.

1. **Como posso opt out?**

   Adobe Systems recomenda o uso do Monitoramento de uso real (RUM) devido a seus benefícios significativos e que possa permitir otimizar suas experiências digitais. Ele pode oferta informações valiosas que podem ajudar a melhorar o desempenho do site. O serviço foi projetado para ser contínuo e não afeta o desempenho do seu site.

   Recusar significa que essas informações não foram encontradas. No entanto, se encontrar problemas, entre em contato com o Adobe Systems Suporte.
