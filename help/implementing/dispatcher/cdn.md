---
title: CDN no AEM as a Cloud Service
description: Saiba como usar a CDN gerenciada pelo AEM e como apontar sua própria CDN para a CDN gerenciada pelo AEM.
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
role: Admin
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 9%

---


# CDN no AEM as a Cloud Service {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="CDN no AEM as a Cloud Service"
>abstract="O AEM as Cloud Service é enviado com uma CDN pré-criada. Seu principal objetivo é reduzir a latência, fornecendo conteúdo que pode ser armazenado em cache a partir dos nós CDN na borda, perto do navegador. Ele é totalmente gerenciado e configurado para obter o desempenho ideal dos aplicativos AEM."

O AEM as a Cloud Service vem com uma CDN integrada, projetada para reduzir a latência, fornecendo conteúdo que pode ser armazenado em cache a partir de nós de borda próximos ao navegador do usuário. Essa CDN totalmente gerenciada é otimizada para o desempenho de aplicativos AEM.

A CDN gerenciada por AEM atende à maioria das necessidades de desempenho e segurança dos clientes. Para o nível de publicação, os clientes podem optar por rotear o tráfego por meio de sua própria CDN, que devem gerenciar. Essa opção está disponível caso a caso, principalmente quando os clientes têm integrações herdadas existentes com um provedor de CDN que são difíceis de substituir.

Os clientes que desejam publicar no nível do Edge Delivery Services podem aproveitar a CDN gerenciada pelo Adobe. Consulte [CDN gerenciada por Adobe](#aem-managed-cdn). <!-- CQDOC-21758, 5b -->


<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## CDN gerenciada pela Adobe {#aem-managed-cdn}

<!-- CQDOC-21758, 5a -->

Para se preparar para a entrega de conteúdo usando o CDN integrado do AEM por meio da interface de usuário de autoatendimento do Cloud Manager, você pode aproveitar os recursos de CDN gerenciados pelo Adobe. Essa funcionalidade permite manipular o gerenciamento de CDN de autoatendimento, incluindo a configuração e instalação de certificados SSL, como certificados DV (Validação de domínio) ou EV/OV (Validação estendida/organização). Para obter mais detalhes sobre esses métodos, consulte o seguinte:

* [Edge Delivery Services no Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)
* [Introdução a nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
* [Introdução aos certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)
* [Adicionar uma configuração de CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)

**Restringindo o tráfego**

Por padrão, para uma configuração de CDN gerenciada pelo AEM, todo o tráfego público pode chegar ao serviço de publicação para ambientes de produção e não produção (desenvolvimento e preparo). É possível limitar o tráfego para o serviço de publicação de um determinado ambiente (por exemplo, limitação de preparo por um intervalo de endereços IP) por meio da interface do usuário do Cloud Manager.

Consulte [Gerenciamento de listas de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) para saber mais.

>[!CAUTION]
>
>A CDN gerenciada do AEM serve solicitações somente de IPs permitidos. Se você apontar seu próprio CDN para o CDN gerenciado pelo AEM, verifique se os IPs do seu CDN estão incluídos na Lista de permissões de IP.

### Configurar o tráfego na CDN {#cdn-configuring-cloud}

Você pode configurar o tráfego na CDN de várias maneiras, incluindo:

* bloqueando tráfego mal-intencionado com [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md) (incluindo regras WAF avançadas opcionalmente licenciáveis)
* modificando a natureza da [solicitação e resposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)
* aplicando [redirecionamentos do lado do cliente](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) do 301/302
* declarando [seletores de origem](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) para reverter uma solicitação de proxy para back-ends não-AEM

Use arquivos YAML no Git para configurar esses recursos. E use o [Pipeline de configuração](/help/implementing/dispatcher/cdn-configuring-traffic.md) do Cloud Manager para implantá-los.

### Configurar páginas de erro do CDN {#cdn-error-pages}

Você pode configurar uma página de erro CDN para substituir a página padrão, sem marca. Essa página personalizada é exibida no raro evento de o AEM não estar disponível. Para obter mais detalhes, consulte [Configurando páginas de erro da CDN](/help/implementing/dispatcher/cdn-error-pages.md).

### Limpar conteúdo em cache na CDN {#purge-cdn}

A definição do TTL usando o cabeçalho HTTP Cache-Control é uma abordagem eficaz para equilibrar o desempenho da entrega de conteúdo e a atualização de conteúdo. No entanto, em cenários em que é essencial fornecer conteúdo atualizado imediatamente, pode ser útil limpar o cache do CDN diretamente.

Leia sobre [configuração de um token de API de limpeza](/help/implementing/dispatcher/cdn-credentials-authentication.md/#purge-API-token) e [limpeza do conteúdo CDN em cache](/help/implementing/dispatcher/cdn-cache-purge.md).

### Autenticação básica na CDN {#basic-auth}

Para casos de uso de autenticação simples, incluindo participantes de negócios que revisam o conteúdo, proteja o conteúdo exibindo uma caixa de diálogo de autenticação básica que requer um nome de usuário e senha. [Saiba mais](/help/implementing/dispatcher/cdn-credentials-authentication.md) e participe do programa de adoção antecipada.

## O CDN gerenciado pelo cliente aponta para o CDN gerenciado pelo AEM {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="A CDN do cliente aponta para a CDN gerenciada pelo AEM"
>abstract="O AEM as a Cloud Service oferece uma opção para os clientes usarem sua CDN existente. Para o nível de publicação, os clientes têm a opção de apontar para ela a partir de sua própria CDN, a qual precisarão gerenciar. Isso será permitido caso a caso, com base no cumprimento de certos pré-requisitos, incluindo, entre outros, uma integração herdada do cliente com seu fornecedor de CDN que seja difícil de abandonar."

Se um cliente precisar usar sua CDN existente, ele poderá gerenciá-la e apontá-la para a CDN gerenciada pelo AEM, desde que:

* O cliente deve ter uma CDN existente que seria onerosa para substituir.
* O cliente deve gerenciá-lo.
* O cliente deve ser capaz de configurar o CDN para funcionar com o AEM as a Cloud Service - consulte as instruções de configuração apresentadas abaixo.
* O cliente deve ter especialistas em CDN de engenharia que estejam disponíveis para resolver problemas relacionados ao caso.
* O cliente deve executar e passar com êxito em um teste de carga antes de ir para a produção.

Instruções de configuração:

1. Aponte seu CDN para o ingresso do CDN do Adobe como seu domínio de origem. Por exemplo, `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Defina SNI para o ingresso do CDN do Adobe.
1. Defina o cabeçalho Host para o domínio de origem. Por exemplo: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Defina o cabeçalho `X-Forwarded-Host` com o nome de domínio para que o AEM possa determinar o cabeçalho do host. Por exemplo: `X-Forwarded-Host:example.com`.
1. Defina `X-AEM-Edge-Key`. O valor deve ser configurado usando um pipeline de configuração do Cloud Manager, conforme descrito em [este artigo](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

   * Necessário para que o CDN do Adobe possa validar a origem das solicitações e transmitir os cabeçalhos `X-Forwarded-*` para o aplicativo AEM. Por exemplo, `X-Forwarded-For` é usado para determinar o IP do cliente. Portanto, torna-se responsabilidade do chamador confiável (ou seja, a CDN gerenciada pelo cliente) garantir a exatidão dos cabeçalhos `X-Forwarded-*` (consulte a observação abaixo).
   * Opcionalmente, o acesso ao ingresso da CDN do Adobe pode ser bloqueado quando um `X-AEM-Edge-Key` não estiver presente. Informe o Adobe se precisar de acesso direto ao ingresso do CDN do Adobe (para ser bloqueado).

Consulte a seção [Configurações de exemplo de fornecedor de CDN](#sample-configurations) para obter exemplos de configuração dos principais fornecedores de CDN.

Antes de aceitar o tráfego ativo, você deve validar com o suporte ao cliente do Adobe se o roteamento de tráfego de ponta a ponta está funcionando corretamente.

Depois de configurar o `X-AEM-Edge-Key`, você pode testar se a solicitação é roteada corretamente da seguinte maneira.

No Linux®:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

No Windows:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

>[!NOTE]
>
>Ao usar seu próprio CDN, não é necessário instalar domínios e certificados no Cloud Manager. O roteamento no CDN Adobe é feito usando o domínio padrão `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`, que deve ser enviado no cabeçalho da solicitação `Host`. Substituir o cabeçalho da solicitação `Host` por um nome de domínio personalizado pode rotear a solicitação incorretamente por meio da CDN Adobe.

>[!NOTE]
>
>Os clientes que gerenciam seu próprio CDN devem garantir a integridade dos cabeçalhos enviados para o CDN do AEM. Por exemplo, é recomendável que os clientes limpem todos os cabeçalhos `X-Forwarded-*` e os definam como valores conhecidos e controlados. Por exemplo, `X-Forwarded-For` deve conter o endereço IP do cliente, enquanto `X-Forwarded-Host` deve conter o host do site.

>[!NOTE]
>
>Os ambientes dos programas de sandbox não são compatíveis com um CDN fornecido pelo cliente.

O salto extra entre o CDN do cliente e o CDN AEM só será necessário se houver uma falha de cache. Ao usar as estratégias de otimização de cache descritas neste artigo, a adição de uma CDN do cliente deve apresentar apenas uma latência insignificante.

Essa configuração de CDN do cliente tem suporte para o nível de publicação, mas não na frente do nível de criação.

### Configurações de exemplo de fornecedor de CDN {#sample-configurations}

Veja abaixo vários exemplos de configuração de vários dos principais fornecedores de CDN.

**Akamai**

![Akamai1](assets/akamai1.png "Akamai")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon CloudFront**

![CloudFront1](assets/cloudfront1.png "Amazon CloudFront")
![CloudFront2](assets/cloudfront2.png "Amazon CloudFront")

**Cloudflare**

![Cloudflare1](assets/cloudflare1.png "Cloudflare")
![Cloudflare2](assets/cloudflare2.png "Cloudflare")

### Erros comuns {#common-errors}

As configurações de exemplo fornecidas mostram as configurações básicas necessárias. No entanto, uma configuração de cliente pode ter outras regras de impacto que removem, editam ou reorganizam os cabeçalhos necessários para que o AEM as a Cloud Service disponibilize o tráfego. Abaixo estão erros comuns que ocorrem ao configurar um CDN gerenciado pelo cliente para apontar para o AEM as a Cloud Service.

**Redirecionamento para o ponto de extremidade do serviço de publicação**

Quando uma solicitação recebe uma resposta 403 proibida, significa que alguns cabeçalhos obrigatórios estão ausentes na solicitação. Uma causa comum para isso é que a CDN está gerenciando o tráfego de domínio apex e `www`, mas não está adicionando o cabeçalho correto para o domínio `www`. Esse problema pode ser solucionado verificando os logs de CDN do AEM as a Cloud Service e os cabeçalhos de solicitação necessários.

**Muitos redirecionamentos Loop**

Quando uma página recebe um loop &quot;Muitos redirecionamentos&quot;, algum cabeçalho de solicitação é adicionado ao CDN que corresponde a um redirecionamento que o força de volta a si mesmo. Como exemplo:

* Uma regra CDN é criada para corresponder ao domínio apex ou ao domínio www e adiciona o cabeçalho X-Forwarded-Host somente do domínio apex.
* Uma solicitação de um domínio apex corresponde a essa regra CDN, que adiciona o domínio apex como o cabeçalho X-Forwarded-Host.
* Uma solicitação é enviada para a origem em que um redirecionamento corresponde explicitamente ao cabeçalho do host para o domínio apex (por exemplo, ^example.com).
* Uma regra de regravação é acionada, o que regrava a solicitação do domínio apex para https com o subdomínio www.
* Esse redirecionamento é então enviado para a borda do cliente, onde a regra CDN é acionada novamente, adicionando novamente o cabeçalho X-Forwarded-Host para o domínio apex, não para o subdomínio www. Em seguida, o processo é reiniciado até que a solicitação falhe.

Para resolver esse problema, avalie sua estratégia de redirecionamento SSL, regras CDN, redirecionamento e reescreva combinações de regras.

## Cabeçalhos de geolocalização {#geo-headers}

O CDN gerenciado pelo AEM adiciona cabeçalhos a cada solicitação com:

* código do país: `x-aem-client-country`
* código do continente: `x-aem-client-continent`

>[!NOTE]
>
>Se houver uma CDN gerenciada pelo cliente, esses cabeçalhos refletirão a localização do servidor proxy CDN do cliente em vez do cliente real. Os clientes devem gerenciar os cabeçalhos de geolocalização por meio de sua própria CDN ao usar uma CDN gerenciada pelo cliente.

Os valores para os códigos de país são os códigos Alpha-2 descritos em [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1).

Os valores para os códigos de continente são:

* AF África
* AN Antártida
* AS Ásia
* UE Europa
* NA América do Norte
* Oceânia OC
* SA América do Sul

Essas informações são úteis para redirecionar para um URL diferente com base no país de origem da solicitação. Use o cabeçalho Vary para armazenar em cache respostas que dependem das informações geográficas. Por exemplo, os redirecionamentos para uma página de aterrissagem de país específico sempre devem conter `Vary: x-aem-client-country`. Se necessário, você pode usar `Cache-Control: private` para impedir o armazenamento em cache. Consulte também [Cache](/help/implementing/dispatcher/caching.md#html-text).
