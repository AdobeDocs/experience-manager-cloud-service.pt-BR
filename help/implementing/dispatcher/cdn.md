---
title: CDN no AEM as a Cloud Service
description: CDN no AEM as a Cloud Service
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 8%

---

# CDN no AEM as a Cloud Service {#cdn}


>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="CDN no AEM as a Cloud Service"
>abstract="AEM como Cloud Service é enviado com um CDN integrado. Seu principal objetivo é reduzir a latência, fornecendo conteúdo armazenável em cache a partir dos nós CDN na borda, perto do navegador. Ele é totalmente gerenciado e configurado para obter o desempenho ideal dos aplicativos AEM."

AEM como Cloud Service é enviado com um CDN integrado. Seu principal objetivo é reduzir a latência, fornecendo conteúdo que pode ser armazenado em cache a partir dos nós CDN na borda, perto do navegador. Ele é totalmente gerenciado e configurado para obter o desempenho ideal dos aplicativos AEM.


A CDN gerenciada AEM atenderá aos requisitos de desempenho e segurança da maioria dos clientes. Para o nível de publicação, os clientes podem apontar para ele opcionalmente a partir de sua própria CDN, que precisarão gerenciar. Isso será permitido caso a caso, com base no atendimento a determinados pré-requisitos, incluindo, mas não limitado a, o cliente que tem uma integração herdada com seu fornecedor de CDN que é difícil de abandonar.

## CDN gerenciada AEM  {#aem-managed-cdn}

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

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="A CDN do cliente aponta para AEM CDN gerenciada"
>abstract="AEM como Cloud Service oferece uma opção para os clientes usarem sua CDN existente. Para o nível de publicação, os clientes podem apontar para ele opcionalmente a partir de sua própria CDN, que precisarão gerenciar. Isso será permitido caso a caso, com base no atendimento a determinados pré-requisitos, incluindo, mas não limitado a, o cliente que tem uma integração herdada com seu fornecedor de CDN que é difícil de abandonar."

Se um cliente precisar usar sua CDN existente, ele poderá gerenciá-la e apontá-la para a CDN gerenciada AEM, desde que:

* O cliente deve ter uma CDN existente que seria onerosa para substituir.
* O cliente deve gerenciá-lo.
* O cliente deve ser capaz de configurar a CDN para funcionar com o AEM como um Cloud Service - consulte as instruções de configuração abaixo.
* O cliente deve ter especialistas em CDN de engenharia que estejam em contato caso surjam problemas relacionados.
* O cliente deve executar e passar com sucesso em um teste de carga antes de ir para a produção.

Instruções de configuração:

1. Defina o cabeçalho `X-Forwarded-Host` com o nome de domínio. Por exemplo: `X-Forwarded-Host:example.com`.
1. Defina o cabeçalho Host com o domínio de origem, que é a entrada do CDN AEM. Por exemplo: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Envie o cabeçalho SNI para a origem. Como o cabeçalho Host , o cabeçalho SNI deve ser o domínio de origem.
1. Defina `X-Edge-Key` ou `X-AEM-Edge-Key` (se sua CDN tira `X-Edge-*`). O valor deve vir do Adobe.
   * Isso é necessário para que o Adobe CDN possa validar a origem das solicitações e transmitir os cabeçalhos `X-Forwarded-*` para o aplicativo AEM. Por exemplo, `X-Forwarded-Host` é usado pelo AEM para determinar o cabeçalho do Host e `X-Forwarded-For` é usado para determinar o IP do cliente. Assim, é responsabilidade do chamador confiável (ou seja, o CDN gerenciado pelo cliente) garantir a correção dos cabeçalhos `X-Forwarded-*` (consulte a nota abaixo).
   * Como opção, o acesso à entrada do Adobe CDN pode ser bloqueado quando um `X-Edge-Key` não estiver presente. Informe o Adobe se precisar de acesso direto à entrada do Adobe CDN (para ser bloqueado).

Antes de aceitar o tráfego ao vivo, você deve validar com suporte ao cliente Adobe que o roteamento de tráfego final está funcionando corretamente.

>[!NOTE]
>
>Os clientes que gerenciam sua própria CDN devem garantir a integridade dos cabeçalhos enviados para AEM CDN. Por exemplo, é recomendável que os clientes limpem todos os cabeçalhos `X-Forwarded-*` e os definam como valores conhecidos e controlados. Por exemplo, `X-Forwarded-For` deve conter o endereço IP do cliente, enquanto `X-Forwarded-Host` deve conter o host do site.

>[!NOTE]
>
>Os ambientes de programa de sandbox não oferecem suporte a um CDN fornecido pelo cliente.

Há um pequeno impacto no desempenho devido ao salto extra, embora o salto da CDN do cliente para a CDN gerenciada AEM provavelmente seja eficiente.

Observe que essa configuração de CDN do cliente é compatível com o nível de publicação, mas não na frente do nível do autor.

## Cabeçalhos de geolocalização {#geo-headers}

O CDN gerenciado AEM adiciona cabeçalhos a cada solicitação com:

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
