---
title: Monitoramento de uso real para AEM as a Cloud Service
description: Saiba como usar o Monitoramento de uso real (RUM) para capturar e analisar a experiência do usuário digital de um site ou aplicativo em tempo real.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
source-git-commit: 0514d56fb65245b1919969a60f6d4c2b719deaa6
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 0%

---

# Serviço de monitoramento de uso real para AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Adobe está animado para anunciar o [Implantação do GA](/help/release-notes/release-notes-cloud/release-notes-current.md#real-use-monitoring) para o serviço de monitoramento de uso real, a coleta de dados do lado do cliente. É um serviço automatizado e não requer configuração do cliente.

>[!INFO]
>
>O monitoramento no lado do cliente funciona somente para clientes com a versão do AEM Cloud Service **2024.5.16461** e acima.

## Visão geral {#overview}

O serviço de Monitoramento de uso real (RUM) é uma tecnologia de monitoramento de desempenho que captura e analisa as experiências do usuário digital de um site ou aplicativo em tempo real. Ele oferece visibilidade do desempenho em tempo real de uma aplicação web e fornece informações mais detalhadas sobre a experiência do usuário final. &quot;Monitoramento de usuário real&quot; foi reformulado para &quot;Monitoramento de uso real&quot; porque reflete melhor a verdadeira essência do serviço. O serviço se concentra em otimizar o desempenho monitorando os envolvimentos do site, em vez dos próprios usuários.

Com o RUM, as métricas principais de desempenho são rastreadas desde o início do URL até que a solicitação seja enviada de volta ao navegador. Ele ajuda os desenvolvedores a aprimorar o aplicativo para facilitar o uso para os usuários finais.

## Quem pode se beneficiar de um serviço de monitoramento de uso real? {#who-can-benefit-from-rum-service}

O serviço de Monitoramento de uso real é benéfico para todos os clientes. Ele oferece uma reflexão representativa das interações do usuário, garantindo uma medida confiável de envolvimento do site ao capturar o número de exibições de página do lado do cliente.

Para todos os clientes do Adobe, esse serviço fornece informações valiosas sobre as interações do usuário. Os clientes que empregam seu próprio CDN podem se beneficiar de relatórios de tráfego simplificados, já que o Adobe agora integra diretamente a coleta de dados, eliminando a necessidade de relatórios separados durante os ciclos de renovação.

Deseja desbloquear todo o potencial do seu site, usando a ferramenta de visualização Adobe Early Adoter RUM Explorer para obter insights úteis sobre o envolvimento do site? Essa ferramenta pode fornecer insights sobre o desempenho da página, incluindo métricas sobre o número de cliques, Core Web Vitals (CWV), conversões e mapas de jornada do cliente. Ao usar esses insights avançados, você pode ajustar as experiências digitais para atender às necessidades dos usuários com mais eficiência. Se quiser saber mais e obter acesso, envie um email para `rum-explorer@adobe.com`.

## Entender como funciona o serviço de monitoramento de uso real {#understand-how-the-rum-service-works}

O Adobe Experience Manager (AEM) usa o Monitoramento de uso real (RUM) para ajudar os clientes e o Adobe a entender como os visitantes interagem com os sites do AEM. Ele os ajuda a diagnosticar problemas de desempenho e medir a eficácia dos experimentos. O RUM preserva a privacidade dos visitantes por meio da amostragem — somente uma pequena parte de todas as exibições de página é monitorada — e nenhuma informação de identificação pessoal (PII) é coletada.

## Serviço de monitoramento e privacidade em uso real {#rum-service-and-privacy}

O serviço de monitoramento de uso real no AEM foi projetado para preservar a privacidade do visitante e minimizar a coleta de dados. Como visitante, significa que o site que você está visitando ou disponibilizado para o Adobe não coleta informações pessoais.

Como operador de site, não é necessária nenhuma aceitação adicional para habilitar o monitoramento por meio desse recurso. Não há nenhum pop-up ou formulário de consentimento adicional para os usuários finais aceitarem para ativar o RUM.

## Amostragem de dados do Real Use Monitoring Service {#rum-service-data-sampling}

As soluções tradicionais de análise da Web tentam coletar dados em cada visitante. O serviço AEM RUM captura apenas informações de uma pequena fração de visualizações de página. O serviço deve ser amostrado e anonimizado em vez de ser um substituto para o Analytics. Por padrão, as páginas têm uma proporção de amostragem de 1:100. Os operadores do site não podem aumentar ou diminuir a taxa de amostragem neste momento. Para estimar o tráfego total com precisão, para cada 100 exibições de página, os dados são coletados de 1, fornecendo uma aproximação confiável do tráfego geral.

Como a decisão sobre se os dados serão coletados, ela é feita em uma base de exibição de página por exibição de página, e se torna praticamente impossível rastrear interações em várias páginas. Por design, o RUM não tem conceito de visitantes ou sessões, apenas de exibições de página.

## Quais dados estão sendo coletados {#what-data-is-being-collected}

O serviço de monitoramento de uso real foi projetado para impedir a coleta de informações de identificação pessoal. O conjunto completo de informações coletadas pelo RUM está listado abaixo:

* O nome do host do site que está sendo visitado, por exemplo: `experienceleague.adobe.com`
* O tipo amplo de agente do usuário e o sistema operacional usados para exibir a página, como: `desktop:windows` ou `mobile:ios`
* O horário da coleta de dados, como: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* O URL da página que está sendo visitada, por exemplo: `https://experienceleague.adobe.com/docs`
* O URL referenciador (o URL da página que se vinculou à página atual, se o usuário seguiu um link)
* Uma ID gerada aleatoriamente da exibição de página, em um formato semelhante a: `2Ac6`
* O peso ou o inverso da taxa de amostragem, por exemplo: `100`. Significa que somente uma em cada cem exibições de página é registrada
* O ponto de verificação ou nome de um evento específico na sequência de carregamento da página. Ou, interagindo com ele como visitante
* A origem ou o identificador do elemento DOM com o qual o usuário interage para o ponto de verificação mencionado acima. Por exemplo, pode ser uma imagem
* O target ou link para uma página externa ou recurso com o qual o usuário interage para o ponto de verificação mencionado acima. Por exemplo: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* As métricas de desempenho dos Componentes principais da Web (CWV), incluindo o Maior Conteúdo de Pintura (LCP), o Primeiro Atraso de Entrada (FID), o Cumulative Layout Shift (CLS) e o Tempo para o Primeiro Byte (TTFB) que descrevem a qualidade da experiência do visitante.

## Como funciona o monitoramento de uso real para um cliente {#how-rum-works-for-a-customer}

O Monitoramento de uso real monitora automaticamente o tráfego do lado do cliente para fornecer insights valiosos. Como cliente Adobe, não é necessário executar nenhuma etapa adicional, pois esse serviço é perfeitamente integrado à sua configuração existente. Com a implantação da Disponibilidade Geral (GA), você se beneficia automaticamente desse novo recurso.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Como os dados do serviço de monitoramento de uso real estão sendo usados {#how-rum-service-data-is-being-used}

Os dados de RUM são benéficos para os seguintes propósitos:

* Identificar e corrigir gargalos de desempenho para locais de clientes
* Para simplificar a pesquisa de tráfego automatizada que inclui exibições de página.
* Para entender como o AEM interage com outros scripts (como análises, direcionamento ou bibliotecas externas) na mesma página, para aumentar a compatibilidade.

## Limitações e noções básicas sobre a variação em exibições de página e métricas de desempenho {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

À medida que você analisa os dados de RUM, pode haver variações nas exibições de página e outras métricas de desempenho. Essas variações podem ser atribuídas a vários fatores inerentes ao monitoramento em tempo real no lado do cliente. Estas são as principais considerações que os clientes devem ter em mente ao interpretar os dados de RUM:

1. **Bloqueadores do rastreador**

   * Os usuários finais que utilizam bloqueadores de rastreadores ou extensões de privacidade podem impedir a coleta de dados do RUM, pois essas ferramentas restringem a execução dos scripts de rastreamento. Essa restrição pode resultar em exibições de página e interações do usuário não relatadas, criando uma discrepância entre a atividade real do site e os dados capturados pelo RUM.

1. **Limitações na captura de chamadas de API/JSON headless**

   * O serviço de dados RUM se concentra na experiência do lado do cliente e não captura as chamadas de API de back-end ou JSON feitas de um aplicativo headless não AEM no momento. A exclusão dessas chamadas dos dados de serviço do RUM cria variações das solicitações de conteúdo medidas pelo CDN Analytics.

## Perguntas frequentes {#faq}


1. **Os clientes podem integrar os scripts de serviço RUM a sistemas de terceiros, como o Dynatrace?**

   Sim.

1. **As métricas de &quot;Interação com a próxima pintura&quot;, &quot;Tempo até o primeiro byte&quot; e &quot;Primeira pintura cheia de conteúdo&quot; estão sendo coletadas?**

   A interação com a próxima pintura (INP) e o Tempo até o Primeiro Byte (TTFB) são coletados.  A primeira tinta cheia de conteúdo não é coletada no momento.

1. **A variável `/.rum` O caminho da Web está bloqueado no meu site. Como devo corrigir?**

   A variável `/.rum` o caminho é necessário para que a coleção RUM funcione. Se você tiver uma CDN na frente do que o Adobe oferece como parte do AEM as a Cloud Service, verifique se `/.rum` o caminho segue para a mesma origem de AEM que o restante do conteúdo de AEM. E certifique-se de que ele não seja ajustado de forma alguma.

1. **A coleção de RUM conta para solicitações de conteúdo para fins contratuais?**

   A biblioteca RUM e a coleção RUM não contam como solicitações de conteúdo e não aumentam o número relatado de exibições de página ou chamadas de API. Além disso, para clientes que usam CDN pronto para uso com AEM as a Cloud Service, [coleção do lado do servidor](#serverside-collection) O é a base para solicitações de conteúdo.

1. **Como posso recusar?**

   A Adobe recomenda usar o Monitoramento de uso real (RUM) devido a seus benefícios significativos e que ele pode permitir a otimização de suas experiências digitais. Ele pode oferecer insights valiosos que podem ajudar a melhorar o desempenho do site. O serviço foi projetado para ser ininterrupto e não tem impacto no desempenho do site.

   Recusar significa perder esses insights. No entanto, se encontrar problemas, entre em contato com o Suporte da Adobe.
