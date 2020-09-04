---
title: CDN no AEM as a Cloud Service
description: CDN no AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: 50c5be6adf265eac9c9c7a7b36d03cb30ba4e5d2
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 4%

---


# CDN no AEM as a Cloud Service {#cdn}

AEM como Cloud Service é fornecido com um CDN integrado. O principal objetivo é reduzir a latência, fornecendo conteúdo armazenável nos nós CDN na borda, perto do navegador. Ele é totalmente gerenciado e configurado para obter o desempenho ideal dos aplicativos AEM.

A CDN gerenciada AEM atenderá aos requisitos de desempenho e segurança da maioria dos clientes. Para a camada de publicação, os clientes podem, opcionalmente, apontar para ela a partir de seu próprio CDN, que precisarão gerenciar. Isso será permitido caso a caso, com base no atendimento de determinados pré-requisitos, incluindo, mas não se limitando a, o cliente que possui uma integração herdada com seu fornecedor de CDN difícil de abandonar.

## CDN gerenciado AEM  {#aem-managed-cdn}

Siga estas etapas para preparar o delivery do conteúdo usando o Adobe Offline CDN:

1. Forneça o certificado SSL assinado e a chave secreta para o Adobe, compartilhando um link para um formulário seguro contendo essas informações. Coordene-se com o suporte ao cliente nesta tarefa.
   **Observação:** O Aem como Cloud Service não oferece suporte a certificados de Domínio Validado (DV). Além disso, deve ser um certificado TLS X.509 de uma autoridade de certificação (CA) confiável com uma chave privada RSA de 2048 bits correspondente.
1. Informe o suporte ao cliente:
   * qual domínio personalizado deve ser associado a um determinado ambiente, conforme definido pela ID do programa e pela ID do ambiente. Observe que domínios personalizados no lado do autor não são suportados.
   * se for necessário algum incluir na lista de permissões IP para restringir o tráfego a um determinado ambiente.
1. Coordene com o suporte ao cliente a temporização das alterações necessárias nos registros DNS. As instruções são diferentes com base na necessidade ou não de um registro de ápice:
   * se um registro de ápice não for necessário, os clientes devem definir o registro de DNS CNAME para apontar para o FQDN `cdn.adobeaemcloud.com`.
   * se for necessário um registro anexado, crie um registro A apontando para os seguintes IPs: 151.101.3.10, 151.101.67.10, 151.101.131.10, 151.101.195.10. Os clientes precisam de um registro de vértice se o FQDN desejado corresponder à Zona DNS. Isso pode ser testado usando o comando Unix dig para verificar se o valor SOA da saída corresponde ao domínio. Por exemplo, o comando `dig anything.dev.adobeaemcloud.com` retorna um SOA (Start de Autoridade, ou seja, a zona) de `dev.adobeaemcloud.com` modo que não seja um registro APEX, enquanto `dig dev.adobeaemcloud.com` retorna um SOA de `dev.adobeaemcloud.com` modo que seja um registro anexado.
1. Você será notificado quando os certificados SSL estiverem expirando, para que possa reenviar os novos certificados SSL.

**Restrição de tráfego**

Por padrão, para uma configuração de CDN gerenciada pelo Adobe, todo o tráfego público pode chegar ao serviço de publicação, tanto para ambientes de produção quanto de não produção (desenvolvimento e estágio). Se você deseja limitar o tráfego ao serviço de publicação de um determinado ambiente (por exemplo, limitando o armazenamento temporário por uma faixa de endereços IP), é necessário trabalhar com o suporte ao cliente para configurar essas restrições.

## CDN do cliente aponta para AEM CDN gerenciada {#point-to-point-CDN}

Se um cliente precisar usar o CDN existente, ele poderá gerenciá-lo e apontá-lo para o CDN gerenciado pela Adobe, desde que:

* O cliente deve ter um CDN existente que seria oneroso substituí-lo.
* O cliente deve gerenciá-lo.
* O cliente deve ser capaz de configurar o CDN para trabalhar com o AEM como um Cloud Service - consulte as instruções de configuração abaixo.
* O cliente deve ter especialistas em engenharia de CDN que estejam em contato caso surjam problemas relacionados.
* O cliente deve executar e passar com êxito em um teste de carga antes de ir para a produção.

Instruções de configuração:

1. Defina o `X-Forwarded-Host` cabeçalho com o nome do domínio.
1. Defina o cabeçalho do host com o domínio da origem, que é a entrada do Adobe CDN. O valor deve vir do Adobe.
1. Envie o cabeçalho SNI para a origem. Como o cabeçalho Host, o cabeçalho sni deve ser o domínio de origem.
1. Defina o `X-Edge-Key`, que é necessário para direcionar o tráfego corretamente para os servidores AEM. O valor deve vir do Adobe.

Antes de aceitar o tráfego ao vivo, você deve validar com o suporte ao cliente Adobe que o roteamento de tráfego completo está funcionando corretamente.

Existe um potencial pequeno impacto no desempenho devido ao lúpulo extra, embora o salto da CDN do cliente para a CDN gerenciada pela Adobe provavelmente seja eficiente.

Observe que essa configuração de CDN do cliente é compatível com a camada de publicação, mas não na frente da camada do autor.
