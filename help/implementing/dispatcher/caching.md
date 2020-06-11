---
title: Armazenamento em cache no AEM como um serviço em nuvem
description: 'Armazenamento em cache no AEM como um serviço em nuvem '
translation-type: tm+mt
source-git-commit: 18c2f70acd33c83a0d98ccb658d3e9be18b34c8b
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---


# Introdução {#intro}

O tráfego passa pelo CDN para uma camada do servidor da Web apache, que suporta módulos incluindo o dispatcher. Para aumentar o desempenho, o dispatcher é usado principalmente como cache para limitar o processamento nos nós de publicação.
As regras podem ser aplicadas à configuração do despachante para modificar qualquer configuração de expiração de cache padrão, resultando em cache no CDN. Observe que o dispatcher também respeita os cabeçalhos de expiração do cache resultante se `enableTTL` estiverem ativados na configuração do dispatcher, o que significa que ele atualizará conteúdo específico mesmo fora do conteúdo que está sendo republicado.

Esta página também descreve como o cache do dispatcher é invalidado, bem como como o cache funciona no nível do navegador em relação às bibliotecas do lado do cliente.

## Cache {#caching}

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

* Para impedir que o conteúdo específico seja armazenado em cache, defina o cabeçalho Cache-Control como &quot;particular&quot;. Por exemplo, o seguinte impediria que o conteúdo html em um diretório chamado &quot;myfolder&quot; fosse armazenado em cache:

```
<LocationMatch "\/myfolder\/.*\.(html)$">.  // replace with the right regex
    Header set Cache-Control “private”
</LocationMatch>
```

* Observe que outros métodos, incluindo o projeto [](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)dispatcher-ttl AEM ACS Commons, não substituirão valores com êxito.

### Bibliotecas do lado do cliente (js,css) {#client-side-libraries}

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

## Invalidação do Cache do Dispatcher {#disp}

Em geral, não será necessário invalidar o cache do dispatcher. Em vez disso, você deve confiar no dispatcher atualizando seu cache quando o conteúdo estiver sendo republicado e o CDN respeitar os cabeçalhos de expiração do cache.

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
