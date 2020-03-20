---
title: Entrega de conteúdo
description: 'Entrega de conteúdo '
translation-type: tm+mt
source-git-commit: d1c953e1caf440f18e488f07a32bcf5bc3880f67

---


# Entrega de conteúdo no AEM como um serviço em nuvem {#content-delivery}

A entrega de conteúdo do serviço de publicação inclui:

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

As seções abaixo fornecem mais detalhes sobre a entrega de conteúdo, incluindo configuração CDN e cache do dispatcher.

Informações sobre replicação do serviço de autor para o serviço de publicação estão disponíveis [aqui](/help/operations/replication.md).

>[!NOTE]
>O tráfego passa por um servidor da Web apache, que suporta módulos incluindo o dispatcher. O dispatcher é usado principalmente como cache para limitar o processamento nos nós de publicação, a fim de aumentar o desempenho.

## CDN {#cdn}

O AEM oferece três opções:

1. Adobe Managed CDN - CDN predefinido do AEM. Essa é a opção recomendada, pois está completamente integrada.
1. A CDN do cliente aponta para a CDN gerenciada da Adobe - o cliente aponta seu próprio CDN para a CDN predefinida do AEM. Se a primeira opção não for viável, essa será a próxima opção preferencial, pois ainda potencializa a integração do AEM com seu CDN padrão. Os clientes ainda serão responsáveis pelo gerenciamento de seu próprio CDN.
1. CDN gerenciada pelo cliente - o cliente traz seu próprio CDN e é inteiramente responsável por gerenciá-lo.

>[!CAUTION]
>A primeira opção é altamente recomendada. A Adobe não pode ser responsabilizada pelo resultado de qualquer configuração incorreta se você escolher a segunda opção.

A segunda e a terceira opções serão permitidas caso a caso. Isso envolve atender a determinados pré-requisitos, incluindo, mas não se limitando a, o cliente ter uma integração herdada com seu fornecedor de CDN, o que é difícil de desfazer.

### CDN gerenciada da Adobe {#adobe-managed-cdn}

A preparação para a entrega de conteúdo usando a CDN predefinida da Adobe é simples, como descrito abaixo:

1. Você fornecerá o certificado SSL assinado e a chave secreta para a Adobe compartilhando um link para um formulário seguro contendo essas informações. Coordene-se com o suporte ao cliente nesta tarefa.
Observação: O Aem como um serviço em nuvem não oferece suporte a certificados DV (Domain Validated, Domínio validado).
1. O suporte ao cliente coordenará com você o tempo de um registro DNS CNAME, apontando para o FQDN `adobe-aem.map.fastly.net`.
1. Você será notificado quando os certificados SSL estiverem expirando, para que possa reenviar os novos certificados SSL.

Por padrão, para uma configuração de CDN gerenciada da Adobe, todo o tráfego público pode chegar ao serviço de publicação, tanto para ambientes de produção quanto de não produção (desenvolvimento e estágio). Se você deseja limitar o tráfego ao serviço de publicação para um determinado ambiente (por exemplo, limitar o armazenamento temporário por uma faixa de endereços IP), é necessário trabalhar com o suporte ao cliente para configurar essas restrições.

### O CDN do cliente aponta para o CDN gerenciado da Adobe {#point-to-point-CDN}

Suportado se você quiser usar seu CDN existente, mas não puder atender aos requisitos de um CDN gerenciado pelo cliente. Nesse caso, você gerencia seu próprio CDN, mas aponta para o CDN gerenciado da Adobe.

Esteja ciente de que você deve:

1. Você deve ter um CDN existente.
1. Você vai lidar com isso.
1. Você deve ser capaz de configurar o CDN para trabalhar com o Aem como um serviço de nuvem - consulte as instruções de configuração abaixo.
1. Você tem especialistas em engenharia de CDN que estão em contato caso surjam problemas relacionados.
1. Você deve executar e passar com êxito em um teste de carga antes de ir para a produção.

Instruções de configuração:

1. Defina o `X-Forwarded-Host` cabeçalho com o nome do domínio.
1. Defina o cabeçalho Host com o domínio de origem, que é a entrada do CDN da Adobe. O valor deve vir da Adobe.
1. Envie o cabeçalho SNI para a origem. Como o cabeçalho Host, o cabeçalho sni deve ser o domínio de origem.
1. Defina o `X-Edge-Key`, que é necessário para rotear o tráfego corretamente para os servidores AEM. O valor deve vir da Adobe.

### CDN gerenciada pelo cliente {#customer-managed-cdn}

Suportado se precisar usar o CDN existente.  Nesse caso, você gerencia seu próprio CDN, apontando para o AEM.

Você pode gerenciar seu próprio CDN, desde que:

1. Você tem um CDN existente.
1. Deve ser um CDN suportado. Atualmente, o Akamai é compatível. Se sua organização quiser gerenciar um CDN não suportado no momento, entre em contato com o suporte ao cliente.
1. Você vai lidar com isso.
1. Você deve ser capaz de configurar o CDN para trabalhar com o Aem como um serviço de nuvem - consulte as instruções de configuração abaixo.
1. Você tem especialistas em engenharia de CDN que estão em contato caso surjam problemas relacionados.
1. É necessário fornecer listas de permissões de nós CDN para o Gerenciador de nuvem, conforme descrito nas instruções de configuração.
1. Você deve executar e passar com êxito em um teste de carga antes de ir para a produção.

Instruções de configuração:

1. Forneça a lista de permissões do fornecedor de CDN para a Adobe chamando a API de criação/atualização do ambiente com uma lista de CIDRs para a lista de permissões.
1. Defina o `X-Forwarded-Host` cabeçalho com o nome do domínio.
1. Defina o cabeçalho Host com o domínio de origem, que é o Aem como uma entrada do serviço em nuvem. O valor deve vir da Adobe.
1. Envie o cabeçalho SNI para a origem. O cabeçalho SNI deve ser o domínio de origem.
1. Defina o `X-Edge-Key` que é necessário para rotear o tráfego corretamente para os servidores AEM. O valor deve vir da Adobe.

Antes de aceitar o tráfego ao vivo, você deve validar com o suporte ao cliente da Adobe que o roteamento de tráfego completo está funcionando corretamente.

### Cache {#caching}

O processo de cache segue as regras apresentadas abaixo.

### HTML/Texto {#html-text}

* por padrão, armazenado em cache pelo navegador por 5 minutos, com base no cabeçalho de controle de cache emitido pela camada de cache. O CDN também respeita esse valor.
* pode ser substituída para todo o conteúdo HTML/Texto definindo a `EXPIRATION_TIME` variável em `global.vars` usando o AEM como ferramentas do Dispatcher do SDK do serviço em nuvem.

Você deve garantir que um arquivo em `src/conf.dispatcher.d/cache` que tenha a seguinte regra:

```
/0000
{ /glob "*" /type "allow" }
```

* pode ser substituído em um nível de granulado mais fino por diretivas apache mod_headers. Por exemplo:

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200 s-maxage=200"
</LocationMatch>
```

Você deve garantir que um arquivo em `src/conf.dispatcher.d/cache` que tenha a seguinte regra:

```
/0000
{ /glob "*" /type "allow" }
```

* Observe que outros métodos, incluindo o projeto [](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)dispatcher-ttl AEM ACS Commons, não substituirão valores com êxito.

### Bibliotecas do lado do cliente (js, css) {#client-side-libraries}

* ao usar a estrutura da biblioteca do lado do cliente do AEM, o JavaScript e o código CSS são gerados de tal forma que os navegadores podem armazená-los em cache indefinidamente, já que qualquer alteração é manifestada como novos arquivos com um caminho exclusivo.  Em outras palavras, o HTML que faz referência às bibliotecas do cliente será produzido conforme necessário para que os clientes possam experimentar novo conteúdo conforme ele é publicado. O controle de cache é definido como &quot;imutável&quot; ou 30 dias para navegadores mais antigos que não respeitam o valor &quot;imutável&quot;.
* consulte a seção Bibliotecas do lado do [cliente e consistência](#content-consistency) da versão para obter mais detalhes.

### Imagens {#images}

* não armazenado em cache

### Outros tipos de conteúdo {#other-content}

* sem cache padrão
* pode ser substituído por apache `mod_headers`. Por exemplo:

```
<LocationMatch "\.(css|js)$">
    Header set Cache-Control "max-age=500 s-maxage=500"
</LocationMatch>
```

*Outros métodos de configuração de cabeçalhos de cache também podem funcionar

Antes de aceitar o tráfego ao vivo, os clientes devem validar com o suporte ao cliente da Adobe que o roteamento de tráfego completo está funcionando corretamente.

## Dispatcher {#disp}

O tráfego passa por um servidor da Web apache, que suporta módulos incluindo o dispatcher. O dispatcher é usado principalmente como cache para limitar o processamento nos nós de publicação, a fim de aumentar o desempenho.

O conteúdo do tipo HTML/texto é definido com cabeçalhos de cache correspondentes a uma expiração de 300 s (5 minutos).

O restante desta seção descreve as considerações relacionadas à invalidação do cache do dispatcher.

### Invalidação do Cache do Dispatcher durante Ativação/Desativação {#cache-activation-deactivation}

Como nas versões anteriores do AEM, publicar ou desfazer a publicação de páginas limpará o conteúdo do cache do dispatcher. Se houver suspeita de um problema de armazenamento em cache, os clientes devem republicar as páginas em questão.

Quando a instância de publicação recebe uma nova versão de uma página ou ativo do autor, ela usa o agente de liberação para invalidar os caminhos apropriados em seu dispatcher. O caminho atualizado é removido do cache do dispatcher, juntamente com seus pais, até um nível mais alto (você pode configurar isso com o [nível](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)de statfileslevel.

### Invalidação explícita do cache do dispatcher {#explicit-invalidation}

Em geral, não será necessário invalidar manualmente o conteúdo no dispatcher, mas é possível se necessário, conforme descrito abaixo.

Antes do AEM como um serviço em nuvem, havia duas maneiras de invalidar o cache do dispatcher.

1. Chame o agente de replicação, especificando o agente de liberação do dispatcher de publicação
2. Chamando diretamente a `invalidate.cache` API (por exemplo, `POST /dispatcher/invalidate.cache`)

A `invalidate.cache` abordagem não será mais suportada, pois ela aborda somente um nó de dispatcher específico.
O AEM como um serviço em nuvem opera no nível de serviço, não no nível de nó individual e, portanto, as instruções de invalidação na página [Invalidar páginas em cache do AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) não são válidas para o AEM como um serviço em nuvem.
Em vez disso, o agente de liberação de replicação deve ser usado. Isso pode ser feito usando a API de replicação. A documentação da API de replicação está disponível [aqui](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) e, para obter um exemplo de como limpar o cache, consulte a página [de exemplo da](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) API especificamente o `CustomStep` exemplo que emite uma ação de replicação do tipo ATIVATE para todos os agentes disponíveis. O ponto de extremidade do agente de liberação não é configurável, mas pré-configurado para apontar para o dispatcher, correspondente ao serviço de publicação que executa o agente de liberação. O agente de descarga normalmente pode ser acionado por eventos ou fluxos de trabalho OSGi.

O diagrama abaixo ilustra isso.

![](assets/cdnc.png "CDN")

Se houver uma preocupação de que o cache do dispatcher não esteja sendo apagado, entre em contato com o suporte ao cliente que pode liberar o cache do dispatcher, se necessário.

O CDN gerenciado pela Adobe respeita os TTLs e, portanto, não é necessário liberá-lo. Se houver suspeita de um problema, entre em contato com o suporte ao cliente que pode liberar um cache CDN gerenciado pela Adobe, conforme necessário.

## Bibliotecas do lado do cliente e consistência da versão {#content-consistency}

As páginas são, claro, feitas de HTML, Javascript, CSS e imagens. Os clientes são incentivados a aproveitar a estrutura de Bibliotecas do lado do cliente (clientlibs) para importar recursos do Javascript e CSS para páginas HTML, levando em conta as dependências entre as bibliotecas do JS.

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

Por padrão, o controle de versão restrito do clientlib é ativado em todos os ambientes AEM como um serviço em nuvem.

Para ativar o controle de versão restrito do clientlib no Início rápido do SDK local, execute as seguintes ações:

1. Navegue até o Gerenciador de configuração do OSGi <host>/system/console/configMgr
1. Localize o Gerenciador de biblioteca HTML da configuração OSGi para o Adobe Granite:
   * Marque a caixa de seleção para ativar o Controle de versão restrito
   * No campo rotulado Chave de cache do lado do cliente de longo prazo, digite o valor de /.*;hash
1. Salve as alterações. Observe que não é necessário salvar essa configuração no controle de origem, pois o AEM como um serviço de nuvem ativará automaticamente essa configuração em ambientes de desenvolvimento, estágio e produção.
1. Sempre que o conteúdo da biblioteca do cliente for alterado, uma nova chave hash será gerada e a referência HTML será atualizada.
