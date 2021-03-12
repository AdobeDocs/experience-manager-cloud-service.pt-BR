---
title: CDN no AEM as a Cloud Service
description: CDN no AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: 6c9a0779cfb9c3c2088a17e67437c76b589276f0
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 4%

---


# CDN no AEM as a Cloud Service {#cdn}

AEM como Cloud Service é enviado com um CDN integrado. Seu principal objetivo é reduzir a latência, fornecendo conteúdo armazenável em cache a partir dos nós CDN na borda, perto do navegador. Ele é totalmente gerenciado e configurado para obter o desempenho ideal dos aplicativos AEM.

A CDN gerenciada AEM atenderá aos requisitos de desempenho e segurança da maioria dos clientes. Para o nível de publicação, os clientes podem apontar para ele opcionalmente a partir de sua própria CDN, que precisarão gerenciar. Isso será permitido caso a caso, com base no atendimento a determinados pré-requisitos, incluindo, mas não limitado a, o cliente que tem uma integração herdada com seu fornecedor de CDN que é difícil de abandonar.

## AEM CDN gerenciada {#aem-managed-cdn}

Siga as seções abaixo para usar a interface do usuário de autoatendimento do Cloud Manager para preparar a entrega de conteúdo usando a CDN predefinida do AEM:

1. [Gerenciar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Restrição de tráfego**

Por padrão, para uma configuração de CDN gerenciada AEM, todo o tráfego público pode chegar ao serviço de publicação, para ambientes de produção e não produção (desenvolvimento e estágio). Se quiser limitar o tráfego para o serviço de publicação de um determinado ambiente (por exemplo, limitando o armazenamento temporário por um intervalo de endereços IP), faça isso de uma maneira automatizada por meio da interface do usuário do Cloud Manager.

Consulte [Gerenciando Listas de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) para saber mais.

>[!CAUTION]
>
>Somente as solicitações dos IPs permitidos serão atendidas pelo CDN gerenciado do AEM. Se você apontar seu próprio CDN para o CDN gerenciado AEM, verifique se os IPs do seu CDN estão incluídos na lista de permissões de .

## A CDN do cliente aponta para AEM CDN gerenciada {#point-to-point-CDN}

Se um cliente precisar usar sua CDN existente, ele poderá gerenciá-la e apontá-la para a CDN gerenciada AEM, desde que:

* O cliente deve ter uma CDN existente que seria onerosa para substituir.
* O cliente deve gerenciá-lo.
* O cliente deve ser capaz de configurar a CDN para funcionar com o AEM como um Cloud Service - consulte as instruções de configuração abaixo.
* O cliente deve ter especialistas em CDN de engenharia que estejam em contato caso surjam problemas relacionados.
* O cliente deve executar e passar com sucesso em um teste de carga antes de ir para a produção.

Instruções de configuração:

1. Defina o cabeçalho `X-Forwarded-Host` com o nome de domínio.
1. Defina o cabeçalho Host com o domínio de origem, que é a entrada do CDN AEM. O valor deve vir do Adobe.
1. Envie o cabeçalho SNI para a origem. Como o cabeçalho Host, o cabeçalho sni deve ser o domínio de origem.
1. Defina o `X-Edge-Key` ou o `X-AEM-Edge-Key` (se sua CDN retirar o X-Edge-*), que é necessário para rotear o tráfego corretamente para os servidores de AEM. O valor deve vir do Adobe. Informe o Adobe se quiser acesso direto à entrada do Adobe CDN (a ser bloqueado quando `X-Edge-Key` não estiver presente).

Antes de aceitar o tráfego em tempo real, você deve validar com o suporte ao cliente do Adobe que o roteamento de tráfego completo está funcionando corretamente.

>[!NOTE]
>
>Os clientes que gerenciam sua própria CDN devem garantir a integridade dos cabeçalhos enviados para AEM CDN. Por exemplo, é recomendável que os clientes limpem todos os cabeçalhos `X-Forwarded-*` e os definam como valores conhecidos e controlados. Por exemplo, `X-Forwarded-For` deve conter o endereço IP do cliente, enquanto `X-Forwarded-Host` deve conter o host do site.

Há um pequeno impacto no desempenho devido ao salto extra, embora o salto da CDN do cliente para a CDN gerenciada AEM provavelmente seja eficiente.

Observe que essa configuração de CDN do cliente é compatível com o nível de publicação, mas não na frente do nível de criação.

## Cabeçalhos de geolocalização {#geo-headers}

A CDN gerenciada AEM adicionará cabeçalhos a cada solicitação com:

* Código do país: `x-aem-client-country`
* Código do continente: `x-aem-client-continent`

Os valores para os códigos de país são os códigos Alfa-2 descritos [aqui](https://en.wikipedia.org/wiki/ISO_3166-1).

Os valores dos códigos continentais são:

* AF África
* AN Antártica
* AS Ásia
* Europa da UE
* NA América do Norte
* OC Oceânia
* América do Sul

Essas informações podem ser úteis para casos de uso, como redirecionamento para um url diferente com base na origem (país) da solicitação. Use o cabeçalho Vary para armazenar respostas em cache que dependem de informações geográficas. Por exemplo, os redirecionamentos para uma página de aterrissagem de um país específico devem sempre conter `Vary: x-aem-client-country`. Se necessário, você pode usar `Cache-Control: private` para evitar o armazenamento em cache. Consulte também [Cache](/help/implementing/dispatcher/caching.md#html-text).
