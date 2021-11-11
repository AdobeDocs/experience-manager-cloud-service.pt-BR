---
title: Armazenamento em cache no AEM as a Cloud Service
description: 'Armazenamento em cache no AEM as a Cloud Service '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: b9829a033b99da10217ede18b1591e4bb04762c0
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 1%

---

# Introdução {#intro}

O tráfego passa pelo CDN para uma camada de servidor da Web apache, que suporta módulos, incluindo o dispatcher. Para aumentar o desempenho, o dispatcher é usado principalmente como um cache para limitar o processamento nos nós de publicação.
As regras podem ser aplicadas à configuração do dispatcher para modificar qualquer configuração padrão de expiração do cache, resultando no armazenamento em cache no CDN. Observe que o dispatcher também respeita os cabeçalhos de expiração do cache resultante se `enableTTL` estiver ativado na configuração do dispatcher, o que implica que ele atualizará o conteúdo específico mesmo fora do conteúdo que está sendo republicado.

Esta página também descreve como o cache do dispatcher é invalidado, bem como como como o cache funciona no nível do navegador em relação às bibliotecas do lado do cliente.

## Armazenamento em cache {#caching}

### HTML/Texto {#html-text}

* por padrão, armazenado em cache pelo navegador por cinco minutos, com base na variável `cache-control` cabeçalho emitido pela camada apache. A CDN também respeita esse valor.
* A configuração padrão de armazenamento em cache de HTML/Texto pode ser desativada ao definir a variável `DISABLE_DEFAULT_CACHING` em `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Isso pode ser útil, por exemplo, quando sua lógica comercial requer o ajuste fino do cabeçalho da idade (com um valor com base no dia do calendário), já que, por padrão, o cabeçalho da idade é definido como 0. Dito isto, **tenha cuidado ao desativar o cache padrão.**

* pode ser substituído para todo o conteúdo de HTML/Texto definindo a variável `EXPIRATION_TIME` em `global.vars` usando as ferramentas AEM as a Cloud Service do SDK Dispatcher.
* pode ser substituído em um nível de granulado mais fino pelas seguintes diretivas apache mod_headers:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Tenha cuidado ao definir cabeçalhos de controle de cache global ou aqueles que correspondem a um grande regex, de modo que eles não sejam aplicados ao conteúdo que você pretende manter privado. Considere o uso de várias diretivas para garantir que as regras sejam aplicadas de forma refinada. Dito isso, AEM as a Cloud Service removerá o cabeçalho do cache se detectar que ele foi aplicado ao que detecta como não armazenável em cache pelo dispatcher, conforme descrito na documentação do dispatcher. Para forçar o AEM a sempre aplicar os cabeçalhos de cache, é possível adicionar o **always** da seguinte forma:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Você deve garantir que um arquivo de `src/conf.dispatcher.d/cache` tem a seguinte regra (que está na configuração padrão):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* Para evitar que conteúdo específico seja armazenado em cache **na CDN**, defina o cabeçalho Controle de Cache como *private*. Por exemplo, o seguinte impediria o conteúdo html em um diretório chamado **seguro** de ser armazenado em cache no CDN:

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >Os outros métodos, incluindo o [dispatcher-ttl AEM projeto ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), não substituirá os valores com êxito.

   >[!NOTE]
   >Observe que o dispatcher ainda pode armazenar o conteúdo em cache de acordo com seu próprio [regras de armazenamento em cache](https://helpx.adobe.com/experience-manager/kb/find-out-which-requests-does-aem-dispatcher-cache.html). Para tornar o conteúdo realmente privado, você deve garantir que ele não seja armazenado em cache pelo dispatcher.

### Bibliotecas do lado do cliente (js, css) {#client-side-libraries}

* ao usar AEM estrutura de biblioteca do lado do cliente, o JavaScript e o código CSS são gerados de forma que os navegadores possam armazená-los em cache indefinidamente, já que qualquer alteração se manifesta como novos arquivos com um caminho exclusivo.  Em outras palavras, o HTML que faz referência às bibliotecas de clientes será produzido conforme necessário para que os clientes possam ter novo conteúdo conforme ele é publicado. O controle de cache é definido como &quot;imutável&quot; ou 30 dias para navegadores mais antigos que não respeitam o valor &quot;imutável&quot;.
* consulte a seção [Bibliotecas do lado do cliente e consistência da versão](#content-consistency) para obter mais detalhes.

### Imagens e qualquer conteúdo grande o suficiente armazenado no armazenamento de blob {#images}

* por padrão, não armazenado em cache
* pode ser definido em um nível mais fino pelo seguinte apache `mod_headers` diretivas:

   ```
      <LocationMatch "^/content/.*\.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   Consulte a discussão na seção html/texto acima para ter cuidado para não armazenar em cache muito amplamente e também para forçar o AEM a sempre aplicar o armazenamento em cache com a opção &quot;sempre&quot;.

   É necessário assegurar que um processo `src/conf.dispatcher.d/`o cache tem a seguinte regra (que está na configuração padrão):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   Certifique-se de que os ativos destinados a serem mantidos privados em vez de armazenados em cache não façam parte dos filtros de diretiva LocationMatch .

   >[!NOTE]
   >Os outros métodos, incluindo o [dispatcher-ttl AEM projeto ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), não substituirá os valores com êxito.

### Outros tipos de arquivos de conteúdo no armazenamento de nós {#other-content}

* sem armazenamento em cache padrão
* O padrão não pode ser definido com a variável `EXPIRATION_TIME` variável usada para tipos de arquivo html/text
* a expiração do cache pode ser definida com a mesma estratégia LocationMatch descrita na seção html/text especificando o regex apropriado

## Invalidação de cache do Dispatcher {#disp}

Em geral, não será necessário invalidar o cache do dispatcher. Em vez disso, você deve confiar no dispatcher atualizando seu cache quando o conteúdo estiver sendo republicado e o CDN respeitar os cabeçalhos de expiração do cache.

### Invalidação de cache do Dispatcher durante a ativação/desativação {#cache-activation-deactivation}

Como nas versões anteriores do AEM, a publicação ou o cancelamento da publicação de páginas limpará o conteúdo do cache do dispatcher. Se houver suspeita de um problema de cache, os clientes devem republicar as páginas em questão.

Quando a instância de publicação recebe uma nova versão de uma página ou ativo do autor, ela usa o agente de limpeza para invalidar os caminhos apropriados em seu dispatcher. O caminho atualizado é removido do cache do dispatcher, juntamente com seus pais, até um nível (você pode configurar isso com a variável [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level).

### Invalidação do cache do dispatcher explícito {#explicit-invalidation}

Em geral, não será necessário invalidar manualmente o conteúdo no dispatcher, mas é possível, se necessário.

>[!NOTE]
>Antes de AEM as a Cloud Service, havia duas maneiras de invalidar o cache do dispatcher.
>
>1. Chame o agente de replicação, especificando o agente de liberação do dispatcher de publicação
>2. Chamar diretamente a `invalidate.cache` API (por exemplo, `POST /dispatcher/invalidate.cache`)

>
>O do dispatcher `invalidate.cache` A abordagem da API não será mais suportada, pois aborda apenas um nó específico do dispatcher. AEM as a Cloud Service opera no nível de serviço, não no nível de nó individual e, portanto, as instruções de invalidação no [Invalidar páginas em cache do AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) não são mais válidas para AEM as a Cloud Service.

O agente de limpeza de replicação deve ser usado. Isso pode ser feito usando o [API de replicação](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). O endpoint do agente de limpeza não é configurável, mas pré-configurado para apontar para o dispatcher, correspondente ao serviço de publicação que executa o agente de limpeza. O agente de limpeza normalmente pode ser acionado por eventos ou fluxos de trabalho OSGi.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 
-->

O diagrama apresentado abaixo ilustra isso.

![CDN](assets/cdnd.png "CDN")

Se houver uma preocupação de que o cache do dispatcher não esteja sendo limpo, entre em contato com o [suporte ao cliente](https://helpx.adobe.com/support.ec.html) que pode liberar o cache do dispatcher, se necessário.

A CDN gerenciada por Adobe respeita os TTLs e, portanto, não há necessidade de liberá-la. Se houver suspeita de um problema, [entre em contato com o suporte ao cliente](https://helpx.adobe.com/support.ec.html) suporte que pode liberar um cache CDN gerenciado por Adobe, conforme necessário.

## Bibliotecas do lado do cliente e consistência da versão {#content-consistency}

As páginas são compostas por HTML, Javascript, CSS e imagens. Os clientes são incentivados a aproveitar o [Estrutura de bibliotecas do lado do cliente (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) para importar recursos Javascript e CSS para páginas HTML, levando em conta as dependências entre as bibliotecas JS.

A estrutura clientlibs fornece gerenciamento automático de versão, o que significa que os desenvolvedores podem fazer check-in de alterações nas bibliotecas JS no controle de origem e a versão mais recente será disponibilizada quando um cliente enviar o lançamento. Sem isso, os desenvolvedores precisariam alterar manualmente o HTML com referências à nova versão da biblioteca, que é especialmente onerosa se muitos templates de HTML compartilharem a mesma biblioteca.

Quando as novas versões das bibliotecas são lançadas para produção, as páginas de HTML de referência são atualizadas com novos links para essas versões atualizadas da biblioteca. Depois que o cache do navegador expirar para uma determinada HTML page, não há preocupação de que as bibliotecas antigas sejam carregadas do cache do navegador, pois a página atualizada (de AEM) agora é garantida para fazer referência às novas versões das bibliotecas. Em outras palavras, uma página de HTML atualizada incluirá todas as versões mais recentes da biblioteca.

O mecanismo para isso é um hash serializado, que é anexado ao link da biblioteca do cliente, garantindo um url exclusivo com versão para o navegador armazenar em cache o CSS/JS. O hash serializado só é atualizado quando o conteúdo da biblioteca do cliente muda. Isso significa que, se ocorrerem atualizações não relacionadas (ou seja, sem alterações no css/js subjacente da biblioteca do cliente), mesmo com uma nova implantação, a referência permanecerá a mesma, garantindo menos interrupção do cache do navegador.

### Ativação das versões do Longcache das bibliotecas do lado do cliente - AEM Início rápido do SDK as a Cloud Service {#enabling-longcache}

As inclusões padrão de clientlib em uma página HTML são semelhantes ao seguinte exemplo:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Quando o controle de versão restrito da clientlib é ativado, uma chave de hash de longo prazo é adicionada como seletor à biblioteca do cliente. Como resultado, a referência clientlib tem esta aparência:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

O controle de versão clientlib restrito é ativado por padrão em todos os ambientes AEM as a Cloud Service.

Para ativar o controle de versão restrito do clientlib no Quickstart do SDK local, execute as seguintes ações:

1. Navegue até o Gerenciador de Configuração do OSGi `<host>/system/console/configMgr`
1. Encontre a Configuração OSGi para o Gerenciador da Biblioteca de HTML do Adobe Granite:
   * Marque a caixa de seleção para ativar o controle de versão restrito
   * No campo rotulado Chave de cache do lado do cliente de longo prazo, insira o valor de /.*;hash
1. Salve as alterações. Observe que não é necessário salvar essa configuração no controle de origem, pois AEM as a Cloud Service habilitará automaticamente essa configuração em ambientes de desenvolvimento, estágio e produção.
1. Sempre que o conteúdo da biblioteca do cliente for alterado, uma nova chave de hash será gerada e a referência de HTML será atualizada.
