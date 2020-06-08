---
title: CDN no AEM como um serviço em nuvem
description: CDN no AEM como um serviço em nuvem
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 2%

---


# CDN no AEM como um serviço em nuvem {#cdn}

O AEM como Cloud Service é enviado com um CDN integrado. O principal objetivo é reduzir a latência, fornecendo conteúdo armazenável nos nós CDN na borda, perto do navegador. Ele é totalmente gerenciado e configurado para obter o desempenho ideal dos aplicativos AEM.

No total, o AEM oferta duas opções:

1. CDN gerenciado pelo AEM - CDN predefinido do AEM. É uma opção totalmente integrada e não exige um grande investimento do cliente no suporte à integração do CDN com o AEM.
1. A CDN gerenciada pelo cliente aponta para a CDN gerenciada pelo AEM - o cliente aponta seu próprio CDN para a CDN predefinida do AEM. O cliente ainda precisará gerenciar seu próprio CDN, mas o investimento na integração com o AEM é moderado.

A primeira opção deve atender à maioria dos requisitos de desempenho e segurança do cliente. Além disso, requer um mínimo de esforço do cliente.

A segunda opção será permitida caso a caso. A decisão se baseia em atender a determinados pré-requisitos, incluindo, mas não se limitando a, o cliente que possui uma integração herdada com seu fornecedor de CDN que é difícil de abandonar.

Apresentada abaixo é uma matriz de decisão para comparar as duas opções. Informações mais detalhadas podem ser encontradas nas seções a seguir.

| Detalhes | CDN gerenciado pelo AEM | O CDN gerenciado pelo cliente aponta para o AEM CDN |
|---|---|---|
| **Esforço do cliente** | Nenhum, está totalmente integrado. Somente é necessário apontar CNAME para o CDN gerenciado pelo AEM. | Modere o investimento do cliente. O cliente deve gerenciar seu próprio CDN. |
| **Pré-requisitos** | Nenhum | CDN existente que é oneroso substituir. Deve demonstrar um teste de carga bem-sucedido antes de entrar em funcionamento. |
| **Conhecimento do CDN** | Nenhum | Requer pelo menos um recurso de engenharia parcial com conhecimento detalhado de CDN capaz de configurar o CDN do cliente. |
| **Segurança** | Administrado pela Adobe. | Gerenciado pela Adobe (e opcionalmente pelo cliente em seu próprio CDN). |
| **Show** | Otimizado pela Adobe. | Se beneficiará de alguns recursos de CDN do AEM, mas possivelmente de uma pequena ocorrência de desempenho devido ao salto extra. **Observação**: Hops da CDN do cliente para a CDN da Adobe pronta para uso (provavelmente será eficiente). |
| **Cache** | Suporta cabeçalhos de cache aplicados ao dispatcher. | Suporta cabeçalhos de cache aplicados ao dispatcher. |
| **Recursos de compactação de imagem e vídeo** | Pode trabalhar com o Adobe Dynamic Media. | Pode trabalhar com o Adobe Dynamic Media ou com a solução de imagem/vídeo CDN gerenciada pelo cliente. |

## CDN gerenciado pelo AEM  {#aem-managed-cdn}

A preparação para o delivery de conteúdo usando o CDN predefinido da Adobe é simples, como descrito abaixo:

1. Você fornecerá o certificado SSL assinado e a chave secreta para a Adobe compartilhando um link para um formulário seguro contendo essas informações. Coordene-se com o suporte ao cliente nesta tarefa.
   **Observação:** O Aem como um serviço em nuvem não oferece suporte a certificados DV (Domain Validated, Domínio validado).
1. Você deve informar o suporte ao cliente:
   * qual domínio personalizado deve ser associado a um determinado ambiente, conforme definido pela ID do programa e pela ID do ambiente.
   * se for necessária alguma listagem de IP para restringir o tráfego a um determinado ambiente.
1. O suporte ao cliente coordenará com você o tempo de um registro DNS CNAME, apontando para o FQDN `cdn.adobeaemcloud.com`.
1. Você será notificado quando os certificados SSL estiverem expirando, para que possa reenviar os novos certificados SSL.

**Restrição de tráfego**

Por padrão, para uma configuração de CDN gerenciada da Adobe, todo o tráfego público pode chegar ao serviço de publicação, tanto para ambientes de produção quanto de não produção (desenvolvimento e estágio). Se você deseja limitar o tráfego ao serviço de publicação de um determinado ambiente (por exemplo, limitando o armazenamento temporário por uma faixa de endereços IP), é necessário trabalhar com o suporte ao cliente para configurar essas restrições.

## CDN do cliente aponta para o CDN gerenciado pelo AEM {#point-to-point-CDN}

Suportado se você quiser usar seu CDN existente, mas não puder atender aos requisitos de um CDN gerenciado pelo cliente. Nesse caso, você gerencia seu próprio CDN, mas aponta para o CDN gerenciado da Adobe.

Esteja ciente de que:

1. Você deve ter um CDN existente.
1. Você deve gerenciá-la.
1. Você deve ser capaz de configurar o CDN para trabalhar com o Aem como um serviço de nuvem - consulte as instruções de configuração abaixo.
1. Você deve ter especialistas em engenharia de CDN que estejam em contato caso surjam problemas relacionados.
1. Você deve executar e passar com êxito em um teste de carga antes de ir para a produção.

Instruções de configuração:

1. Defina o `X-Forwarded-Host` cabeçalho com o nome do domínio.
1. Defina o cabeçalho Host com o domínio de origem, que é a entrada do CDN da Adobe. O valor deve vir da Adobe.
1. Envie o cabeçalho SNI para a origem. Como o cabeçalho Host, o cabeçalho sni deve ser o domínio de origem.
1. Defina o `X-Edge-Key`, que é necessário para rotear o tráfego corretamente para os servidores AEM. O valor deve vir da Adobe.

Antes de aceitar o tráfego ao vivo, você deve validar com o suporte ao cliente da Adobe que o roteamento de tráfego completo está funcionando corretamente.
