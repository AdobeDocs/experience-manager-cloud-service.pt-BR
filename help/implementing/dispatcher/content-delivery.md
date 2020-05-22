---
title: Delivery de conteúdo
description: 'Delivery de conteúdo '
translation-type: tm+mt
source-git-commit: a07de761dd9aedb3469f256e08ecf05b2102889d
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 1%

---


# Entrega de conteúdo no AEM as a Cloud Service {#content-delivery}

Os detalhes da página atual publicam o delivery de conteúdo do serviço no AEM como um serviço em nuvem. O delivery de conteúdo do serviço de publicação inclui:

* CDN (normalmente gerenciado pela Adobe)
* Despachante do AEM
* Publicar AEM

O fluxo de dados é o seguinte:

1. O URL é adicionado no navegador
1. Solicitação feita ao CDN mapeada no DNS para esse domínio
1. Se o conteúdo for totalmente armazenado em cache no CDN, o CDN o enviará para o navegador
1. Se o conteúdo não estiver totalmente armazenado em cache, a CDN chamará (proxy reverso) o dispatcher
1. Se o conteúdo for totalmente armazenado em cache no dispatcher, o dispatcher o enviará para a CDN
1. Se o conteúdo não estiver totalmente armazenado em cache, o dispatcher chamará (proxy reverso) para a publicação do AEM
1. O conteúdo é renderizado pelo navegador, que também pode armazená-lo em cache, dependendo dos cabeçalhos

O tipo de conteúdo HTML/texto é definido para expirar após 300s (5 minutos) na camada do dispatcher, um limite que tanto o cache do dispatcher quanto o CDN respeitam. Durante as reimplantações do serviço de publicação, o cache do dispatcher é limpo e aquecido posteriormente antes que os novos nós de publicação aceitem o tráfego.

As seções abaixo fornecem mais detalhes sobre o delivery de conteúdo, incluindo configuração e cache de CDN.

Informações sobre replicação do serviço de autor para o serviço de publicação estão disponíveis [aqui](/help/operations/replication.md).

## CDN {#cdn}

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

### CDN gerenciado pelo AEM  {#aem-managed-cdn}

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

### CDN do cliente aponta para o CDN gerenciado pelo AEM {#point-to-point-CDN}

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

## Cache {#caching}

O armazenamento em cache no CDN pode ser configurado usando as regras do dispatcher. Observe que o dispatcher também respeita os cabeçalhos de expiração do cache resultante se `enableTTL` estiverem ativados na configuração do dispatcher, o que significa que ele atualizará conteúdo específico mesmo fora do conteúdo que está sendo republicado.

### HTML/Texto {#html-text}

* por padrão, armazenado em cache pelo navegador por cinco minutos, com base no cabeçalho de controle de cache emitido pela camada de cache. O CDN também respeita esse valor.
* pode ser substituída para todo o conteúdo HTML/Texto definindo a `EXPIRATION_TIME` variável em `global.vars` usando o AEM como ferramentas do Dispatcher do SDK do serviço em nuvem.
* pode ser substituído em um nível de granulado mais fino pelas seguintes diretivas apache mod_headers:

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
</LocationMatch>
```

Você deve garantir que um arquivo em `src/conf.dispatcher.d/cache` tem a seguinte regra (que está na configuração padrão):

```
/0000
{ /glob "*" /type "allow" }
```

* Observe que outros métodos, incluindo o projeto [](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)dispatcher-ttl AEM ACS Commons, não substituirão valores com êxito.

### Bibliotecas do lado do cliente (js, css) {#client-side-libraries}

* ao usar a estrutura da biblioteca do lado do cliente do AEM, o JavaScript e o código CSS são gerados de tal forma que os navegadores podem armazená-los em cache indefinidamente, já que qualquer alteração é manifestada como novos arquivos com um caminho exclusivo.  Em outras palavras, o HTML que faz referência às bibliotecas do cliente será produzido conforme necessário para que os clientes possam experimentar novo conteúdo conforme ele é publicado. O controle de cache é definido como &quot;imutável&quot; ou 30 dias para navegadores mais antigos que não respeitam o valor &quot;imutável&quot;.
* consulte a seção Bibliotecas do lado do [cliente e consistência](#content-consistency) da versão para obter mais detalhes.

### Imagens e qualquer conteúdo grande o suficiente armazenado no armazenamento blob {#images}

* por padrão, não armazenado em cache
* pode ser definido em um nível de granulado mais fino pelas seguintes `mod_headers` diretivas de cache:

```
<LocationMatch "^.*.jpeg$">
    Header set Cache-Control "max-age=222"
</LocationMatch>
```

É necessário garantir que um arquivo em src/conf.dispatcher.d/cache tenha a seguinte regra (que está na configuração padrão):

```
/0000
{ /glob "*" /type "allow" }
```

Certifique-se de que os ativos destinados a serem mantidos privados em vez de armazenados em cache não façam parte dos filtros da diretiva LocationMatch.

* Observe que outros métodos, incluindo o projeto [](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)dispatcher-ttl AEM ACS Commons, não substituirão valores com êxito.

### Outros tipos de arquivos de conteúdo no armazenamento de nós {#other-content}

* sem cache padrão
* o padrão não pode ser definido com a `EXPIRATION_TIME` variável usada para tipos de arquivos html/text
* a expiração do cache pode ser definida com a mesma estratégia LocationMatch descrita na seção html/texto especificando o regex apropriado

## Dispatcher {#disp}

O tráfego passa por um servidor da Web apache, que suporta módulos incluindo o dispatcher. O dispatcher é usado principalmente como cache para limitar o processamento nos nós de publicação, a fim de aumentar o desempenho.

Conforme descrito na seção de cache do CDN, as regras podem ser aplicadas à configuração do dispatcher para modificar quaisquer configurações padrão de expiração do cache.

O restante desta seção descreve as considerações relacionadas à invalidação do cache do dispatcher. Para a maioria dos clientes, não deve ser necessário invalidar o cache do dispatcher, em vez de confiar na atualização do cache pelo dispatcher após a republicação do conteúdo e no CDN que respeita os cabeçalhos de expiração do cache.

### Invalidação do Cache do Dispatcher durante Ativação/Desativação {#cache-activation-deactivation}

Como nas versões anteriores do AEM, publicar ou desfazer a publicação de páginas limpará o conteúdo do cache do dispatcher. Se houver suspeita de um problema de armazenamento em cache, os clientes devem republicar as páginas em questão.

Quando a instância de publicação recebe uma nova versão de uma página ou ativo do autor, ela usa o agente de liberação para invalidar os caminhos apropriados em seu dispatcher. O caminho atualizado é removido do cache do dispatcher, juntamente com seus pais, até um nível mais alto (você pode configurar isso com o [nível](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)de statfileslevel.

### Invalidação explícita do cache do dispatcher {#explicit-invalidation}

Em geral, não será necessário invalidar manualmente o conteúdo no dispatcher, mas é possível se necessário, conforme descrito abaixo.

Antes do AEM como um serviço em nuvem, havia duas maneiras de invalidar o cache do dispatcher.

1. Chame o agente de replicação, especificando o agente de liberação do dispatcher de publicação
2. Chamando diretamente a `invalidate.cache` API (por exemplo, `POST /dispatcher/invalidate.cache`)

A abordagem da `invalidate.cache` API do dispatcher não será mais suportada, pois ela aborda somente um nó de dispatcher específico. O AEM como um serviço em nuvem opera no nível de serviço, não no nível de nó individual e, portanto, as instruções de invalidação na página [Invalidar páginas em cache do AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) não são mais válidas para o AEM como um serviço em nuvem.
Em vez disso, o agente de liberação de replicação deve ser usado. Isso pode ser feito usando a API de replicação. A documentação da API de replicação está disponível [aqui](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) e, para obter um exemplo de como limpar o cache, consulte a página [de exemplo da](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) API especificamente o `CustomStep` exemplo que emite uma ação de replicação do tipo ATIVATE para todos os agentes disponíveis. O ponto de extremidade do agente de liberação não é configurável, mas pré-configurado para apontar para o dispatcher, correspondente ao serviço de publicação que executa o agente de liberação. O agente de descarga normalmente pode ser acionado por eventos ou workflows OSGi.

O diagrama apresentado abaixo ilustra isso.

![](assets/cdnd.png "CDN")

Se houver uma preocupação de que o cache do dispatcher não esteja sendo apagado, entre em contato com o suporte [ao](https://helpx.adobe.com/support.ec.html) cliente que pode liberar o cache do dispatcher, se necessário.

O CDN gerenciado pela Adobe respeita os TTLs e, portanto, não é necessário liberá-lo. Se houver suspeita de um problema, [entre em contato com o suporte](https://helpx.adobe.com/support.ec.html) ao cliente para obter suporte que possa liberar um cache de CDN gerenciado pela Adobe, conforme necessário.

## Bibliotecas do lado do cliente e consistência da versão {#content-consistency}

As páginas são compostas de HTML, Javascript, CSS e imagens. Os clientes são incentivados a aproveitar a estrutura de Bibliotecas do lado do cliente (clientlibs) para importar recursos do Javascript e CSS para páginas HTML, levando em conta as dependências entre as bibliotecas do JS.

A estrutura clientlibs fornece gerenciamento automático de versões, o que significa que os desenvolvedores podem fazer check-in das alterações nas bibliotecas JS no controle de origem e a versão mais recente será disponibilizada quando um cliente fizer o lançamento. Sem isso, os desenvolvedores precisariam alterar manualmente o HTML com referências à nova versão da biblioteca, que é especialmente onerosa se muitos modelos HTML compartilharem a mesma biblioteca.

Quando as novas versões das bibliotecas são lançadas para produção, as páginas HTML de referência são atualizadas com novos links para essas versões atualizadas da biblioteca. Depois que o cache do navegador expirar para uma determinada página HTML, não há preocupação de que as bibliotecas antigas sejam carregadas do cache do navegador, pois a página atualizada (do AEM) agora é garantida para fazer referência às novas versões das bibliotecas. Em outras palavras, uma página HTML atualizada incluirá todas as versões mais recentes da biblioteca.

O mecanismo para isso é um hash serializado, que é anexado ao link da biblioteca do cliente, garantindo um url exclusivo com versão para que o navegador armazene o CSS/JS em cache. O hash serializado só é atualizado quando o conteúdo da biblioteca do cliente é alterado. Isso significa que se ocorrerem atualizações não relacionadas (ou seja, sem alterações no css/js subjacente da biblioteca do cliente) mesmo com uma nova implantação, a referência permanecerá a mesma, garantindo menos interrupção no cache do navegador.

### Ativação das versões do Longcache das bibliotecas do lado do cliente - Início rápido do AEM como um serviço em nuvem SDK {#enabling-longcache}

A clientlib padrão inclui em uma página HTML como o exemplo a seguir:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Quando o controle de versão restrito do clientlib está ativado, uma chave hash de longo prazo é adicionada como seletor à biblioteca do cliente. Como resultado, a referência clientlib se parece com:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Por padrão, o controle de versão restrito do clientlib é ativado em todo o AEM como ambientes de serviço em nuvem.

Para ativar o controle de versão restrito do clientlib no Início rápido do SDK local, execute as seguintes ações:

1. Navegue até o Gerenciador de configuração do OSGi `<host>/system/console/configMgr`
1. Localize o Gerenciador de biblioteca HTML da configuração OSGi para o Adobe Granite:
   * Marque a caixa de seleção para ativar o Controle de versão restrito
   * No campo rotulado Chave de cache do lado do cliente de longo prazo, digite o valor de /.*;hash
1. Salve as alterações. Observe que não é necessário salvar essa configuração no controle de origem, pois o AEM como um serviço de nuvem ativará automaticamente essa configuração em ambientes de desenvolvimento, estágio e produção.
1. Sempre que o conteúdo da biblioteca do cliente for alterado, uma nova chave hash será gerada e a referência HTML será atualizada.
