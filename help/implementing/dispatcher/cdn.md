---
title: CDN no AEM as a Cloud Service
description: CDN no AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: 8ca8944d37c1a10782597ec30c16b0151b5cd717
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 5%

---


# CDN no AEM as a Cloud Service {#cdn}

AEM como Cloud Service é fornecido com um CDN integrado. O principal objetivo é reduzir a latência, fornecendo conteúdo armazenável nos nós CDN na borda, perto do navegador. Ele é totalmente gerenciado e configurado para obter o desempenho ideal dos aplicativos AEM.

A CDN gerenciada AEM atenderá aos requisitos de desempenho e segurança da maioria dos clientes. Para a camada de publicação, os clientes podem, opcionalmente, apontar para ela a partir de seu próprio CDN, que precisarão gerenciar. Isso será permitido caso a caso, com base no atendimento de determinados pré-requisitos, incluindo, mas não se limitando a, o cliente que possui uma integração herdada com seu fornecedor de CDN difícil de abandonar.

## AEM Managed CDN {#aem-managed-cdn}

Siga as seções abaixo para usar a interface do usuário de autoatendimento do Cloud Manager para se preparar para o delivery de conteúdo usando a CDN predefinida do Adobe:

1. [Gerenciamento de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Gerenciamento de nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Restrição de tráfego**

Por padrão, para uma configuração de CDN gerenciada pelo Adobe, todo o tráfego público pode chegar ao serviço de publicação, tanto para ambientes de produção quanto de não produção (desenvolvimento e estágio). Se você deseja limitar o tráfego ao serviço de publicação de um determinado ambiente (por exemplo, limitar o armazenamento temporário por um intervalo de endereços IP), é possível fazer isso de uma forma de autoatendimento por meio da interface do usuário do Cloud Manager.

Consulte [Gerenciando Listas de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) para saber mais.

## O CDN do cliente aponta para AEM CDN gerenciada {#point-to-point-CDN}

Se um cliente precisar usar o CDN existente, ele poderá gerenciá-lo e apontá-lo para o CDN gerenciado pela Adobe, desde que:

* O cliente deve ter um CDN existente que seria oneroso substituí-lo.
* O cliente deve gerenciá-lo.
* O cliente deve ser capaz de configurar o CDN para trabalhar com o AEM como um Cloud Service - consulte as instruções de configuração abaixo.
* O cliente deve ter especialistas em engenharia de CDN que estejam em contato caso surjam problemas relacionados.
* O cliente deve executar e passar com êxito em um teste de carga antes de ir para a produção.

Instruções de configuração:

1. Defina o cabeçalho `X-Forwarded-Host` com o nome do domínio.
1. Defina o cabeçalho do host com o domínio da origem, que é a entrada do Adobe CDN. O valor deve vir do Adobe.
1. Envie o cabeçalho SNI para a origem. Como o cabeçalho Host, o cabeçalho sni deve ser o domínio de origem.
1. Defina `X-Edge-Key`, que é necessário para rotear o tráfego corretamente para os servidores AEM. O valor deve vir do Adobe.

Antes de aceitar o tráfego ao vivo, você deve validar com o suporte ao cliente Adobe que o roteamento de tráfego completo está funcionando corretamente.

Existe um potencial pequeno impacto no desempenho devido ao lúpulo extra, embora o salto da CDN do cliente para a CDN gerenciada pela Adobe provavelmente seja eficiente.

Observe que essa configuração de CDN do cliente é compatível com a camada de publicação, mas não na frente da camada do autor.

## Cabeçalhos de localização geográfica {#geo-headers}

A CDN gerenciada pelo Adobe adicionará cabeçalhos a cada solicitação com:

* código do país: `x-aem-client-country`
* código do continente: `x-aem-client-continent`

Os valores para os códigos de país são os códigos alfa-2 descritos [here](https://en.wikipedia.org/wiki/ISO_3166-1).

Os valores dos códigos do continente são:

* AF África
* AN Antártica
* AS Ásia
* Europa da UE
* NA América do Norte
* OC Oceania
* América do Sul SA

Essas informações podem ser úteis para casos de uso, como redirecionamento para um url diferente com base na origem (país) da solicitação. Embora, neste caso de utilização específica, o redirecionamento não deva ser armazenado em cache, uma vez que varia. Se necessário, você pode usar `Cache-Control: private` para impedir o armazenamento em cache. Consulte também [Cache](/help/implementing/dispatcher/caching.md#html-text).
