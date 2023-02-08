---
title: Armazenamento em cache no AEM as a Cloud Service
description: Armazenamento em cache no AEM as a Cloud Service
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: b0db2224e3dd7af01bf61fe29e8e24793ab33c5b
workflow-type: tm+mt
source-wordcount: '2832'
ht-degree: 2%

---

# Introdução {#intro}

O tráfego passa pelo CDN para uma camada de servidor da Web Apache, que oferece suporte a módulos, incluindo o Dispatcher. Para aumentar o desempenho, o Dispatcher é usado principalmente como cache para limitar o processamento nos nós de publicação.
As regras podem ser aplicadas à configuração do Dispatcher para modificar qualquer configuração padrão de expiração do cache, resultando no armazenamento em cache no CDN. Observe que o Dispatcher também respeita os cabeçalhos de expiração do cache resultante se `enableTTL` estiver ativado na configuração do Dispatcher, o que implica que ele atualizará o conteúdo específico mesmo fora do conteúdo que está sendo republicado.

Esta página também descreve como o cache do Dispatcher é invalidado e como o cache funciona no nível do navegador em relação às bibliotecas do lado do cliente.

## Armazenamento em cache {#caching}

### HTML/Texto {#html-text}

* por padrão, armazenado em cache pelo navegador por cinco minutos, com base na variável `cache-control` cabeçalho emitido pela camada do Apache. A CDN também respeita esse valor.
* A configuração padrão de armazenamento em cache de HTML/Texto pode ser desativada ao definir a variável `DISABLE_DEFAULT_CACHING` em `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Isso pode ser útil, por exemplo, quando sua lógica comercial requer o ajuste fino do cabeçalho da idade (com um valor com base no dia do calendário), já que, por padrão, o cabeçalho da idade é definido como 0. Dito isto, **tenha cuidado ao desativar o cache padrão.**

* pode ser substituído para todo o conteúdo de HTML/Texto definindo a variável `EXPIRATION_TIME` em `global.vars` usando as ferramentas AEM as a Cloud Service do SDK Dispatcher.
* pode ser substituído em um nível com granularidade mais fina, incluindo o controle independente do CDN e do cache do navegador, com o seguinte Apache `mod_headers` diretivas:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >O cabeçalho Controle de Substituição se aplica à CDN gerenciada pelo Adobe. Se estiver usando um [CDN gerenciada pelo cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN), um cabeçalho diferente pode ser necessário, dependendo do provedor CDN.

   Tenha cuidado ao definir cabeçalhos de controle de cache global ou aqueles que correspondem a um amplo regex, de modo que eles não sejam aplicados ao conteúdo que você precisa manter privado. Considere o uso de várias diretivas para garantir que as regras sejam aplicadas de forma refinada. Dito isso, AEM as a Cloud Service removerá o cabeçalho do cache se detectar que ele foi aplicado ao que detecta como não armazenável em cache pelo Dispatcher, conforme descrito na documentação do Dispatcher. Para forçar o AEM a sempre aplicar os cabeçalhos de cache, é possível adicionar o **always** da seguinte forma:

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

* Embora o conteúdo de HTML definido como privado não seja armazenado em cache no CDN, ele pode ser armazenado em cache no dispatcher se [Cache sensível a permissão](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR) estiver configurado, garantindo que somente usuários autorizados possam receber o conteúdo.

   >[!NOTE]
   >Os outros métodos, incluindo o [dispatcher-ttl AEM projeto ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), não substituirá os valores com êxito.

   >[!NOTE]
   >Observe que o Dispatcher ainda pode armazenar o conteúdo em cache de acordo com seu próprio [regras de armazenamento em cache](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). Para tornar o conteúdo realmente privado, você deve garantir que ele não seja armazenado em cache pelo Dispatcher.

### Bibliotecas do lado do cliente (js, css) {#client-side-libraries}

* Ao usar AEM estrutura de biblioteca do lado do cliente, o JavaScript e o código CSS são gerados de forma que os navegadores possam armazená-los em cache indefinidamente, já que qualquer alteração se manifesta como novos arquivos com um caminho exclusivo.  Em outras palavras, o HTML que faz referência às bibliotecas de clientes será produzido conforme necessário para que os clientes possam ter novo conteúdo conforme ele é publicado. O controle de cache é definido como &quot;imutável&quot; ou 30 dias para navegadores mais antigos que não respeitam o valor &quot;imutável&quot;.
* consulte a seção [Bibliotecas do lado do cliente e consistência da versão](#content-consistency) para obter mais detalhes.

### Imagens e qualquer conteúdo grande o suficiente para ser armazenado no armazenamento de blobs {#images}

O comportamento padrão dos programas criados após meados de maio de 2022 (especificamente, para ids de programa maiores que 65000) é armazenar em cache por padrão, respeitando também o contexto de autenticação da solicitação. Os programas mais antigos (ids de programa iguais ou inferiores a 65000) não armazenam em cache o conteúdo do blob por padrão.

Em ambos os casos, os cabeçalhos de armazenamento em cache podem ser substituídos em um nível de granularidade mais fina na camada do Apache/Dispatcher usando o Apache `mod_headers` diretivas, por exemplo:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Ao modificar os cabeçalhos de cache na camada do Dispatcher, tenha cuidado para não armazenar em cache muito, consulte a discussão na seção HTML/texto [above](#html-text). Além disso, verifique se os ativos destinados a serem mantidos privados (em vez de armazenados em cache) não fazem parte do `LocationMatch` filtros de diretiva.

#### Novo comportamento padrão de armazenamento em cache {#new-caching-behavior}

A camada de AEM definirá cabeçalhos de cache dependendo se o cabeçalho do cache já foi definido e do valor do tipo de solicitação. Observe que, se nenhum cabeçalho de controle de cache tiver sido definido, o conteúdo público será armazenado em cache e o tráfego autenticado será definido como privado. Se um cabeçalho de controle de cache tiver sido definido, os cabeçalhos de cache ficarão inalterados.

| O cabeçalho de controle de cache existe? | Tipo de solicitação | AEM define cabeçalhos de cache como |
|------------------------------|---------------|------------------------------------------------|
| Não | público | Controle de cache: público, max-age=600, imutável |
| Não | autenticado | Controle de cache: private, max-age=600, imutável |
| Sim | qualquer | inalterado |

Embora não seja recomendado, é possível alterar o novo comportamento padrão para seguir o comportamento mais antigo (ids de programa iguais ou inferiores a 65000), definindo a variável de ambiente do Cloud Manager `AEM_BLOB_ENABLE_CACHING_HEADERS` como falso.

#### Comportamento de armazenamento em cache padrão mais antigo {#old-caching-behavior}

A camada de AEM não armazenará em cache o conteúdo do blob por padrão.

>[!NOTE]
>É recomendável alterar o comportamento padrão mais antigo para que seja consistente com o novo comportamento (ids de programa mais altas que 65000), definindo a variável de ambiente do Cloud Manager AEM_BLOB_ENABLE_CACHING_HEADERS como true. Se o programa já estiver ativo, verifique se, depois das alterações, o conteúdo se comporta conforme o esperado.

No momento, as imagens no armazenamento de blob marcadas como privadas não podem ser armazenadas em cache no dispatcher usando [Cache sensível a permissão](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR). A imagem é sempre solicitada da origem da AEM e servida se o usuário estiver autorizado.

>[!NOTE]
>Os outros métodos, incluindo o [dispatcher-ttl AEM projeto ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), não substituirá os valores com êxito.

### Outros tipos de arquivos de conteúdo no armazenamento de nós {#other-content}

* sem armazenamento em cache padrão
* O padrão não pode ser definido com a variável `EXPIRATION_TIME` variável usada para tipos de arquivo html/text
* a expiração do cache pode ser definida com a mesma estratégia LocationMatch descrita na seção html/text especificando o regex apropriado

### Outras otimizações {#further-optimizations}

* Evite usar `User-Agent` como parte da `Vary` cabeçalho. Versões anteriores da configuração padrão do Dispatcher (antes do arquétipo versão 28) incluíam isso e recomendamos que você a removesse usando as etapas abaixo.
   * Localize os arquivos vhost em `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * Remova ou comente a linha: `Header append Vary User-Agent env=!dont-vary` de todos os arquivos vhost, com exceção do default.vhost, que é somente leitura
* Use o `Surrogate-Control` cabeçalho para controlar o armazenamento em cache CDN independentemente do armazenamento em cache do navegador
* Considere aplicar [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) e [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) diretivas para permitir a atualização em segundo plano e evitar falhas no cache, mantendo o conteúdo rápido e atualizado para os usuários.
   * Existem muitas formas de aplicar estas diretivas, mas acrescentando 30 minutos `stale-while-revalidate` para todos os cabeçalhos de controle de cache é um bom ponto de partida.
* Alguns exemplos se seguem para vários tipos de conteúdo, que podem ser usados como guia ao configurar suas próprias regras de cache. Considere e teste cuidadosamente a configuração e os requisitos específicos:

   * Armazene em cache os recursos da biblioteca do cliente mutável para 12h e atualize em segundo plano após 12h.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Armazene em cache recursos imutáveis da biblioteca do cliente a longo prazo (30 dias) com atualização em segundo plano para evitar o MISS.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Armazene em cache HTML pages por 5 minutos com a atualização em segundo plano 1 h no navegador e 12 h no CDN. Os cabeçalhos de controle de cache sempre serão adicionados, portanto, é importante garantir que as páginas html correspondentes em /content/* sejam destinadas ao público. Caso contrário, considere usar um regex mais específico.

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Armazene em cache as respostas json dos serviços de conteúdo/exportador de modelo Sling por 5 minutos com atualização em segundo plano em 1h no navegador e 12h no CDN.

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Armazene em cache URLs imutáveis do componente de imagem principal a longo prazo (30 dias) com a atualização em segundo plano para evitar o MISS.

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Armazene em cache recursos mutáveis do DAM como imagens e vídeos para 24 horas e atualize o plano de fundo após 12 horas para evitar o MISS

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### Comportamento da solicitação de HEAD {#request-behavior}

Quando uma solicitação de HEAD é recebida na CDN do Adobe para um recurso que é **not** em cache, a solicitação é transformada e recebida pelo Dispatcher e/ou AEM instância como uma solicitação do GET. Se a resposta for armazenável em cache, as solicitações de HEAD subsequentes serão atendidas no CDN. Se a resposta não puder ser armazenada em cache, as solicitações de HEAD subsequentes serão passadas para a instância do Dispatcher e/ou AEM por um período de tempo que depende do `Cache-Control` TTL.

### Parâmetros da campanha de marketing {#marketing-parameters}

Os URLs do site frequentemente incluem parâmetros de campanha de marketing usados para rastrear o sucesso de uma campanha. Para usar o cache do dispatcher de maneira eficaz, é recomendável configurar o `ignoreUrlParams` propriedade como [documentado aqui](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters).

O `ignoreUrlParams` deve estar sem comentários e deve fazer referência ao arquivo `conf.dispatcher.d/cache/marketing_query_parameters.any`. O arquivo pode ser modificado ao descomentar as linhas correspondentes aos parâmetros relevantes para seus canais de marketing. Você também pode adicionar outros parâmetros.

```
/ignoreUrlParams {
{{ /0001 { /glob "*" /type "deny" }}}
{{ $include "../cache/marketing_query_parameters.any"}}
}
```

## Invalidação de cache do Dispatcher {#disp}

Em geral, não será necessário invalidar o cache do Dispatcher. Em vez disso, você deve confiar no Dispatcher atualizando seu cache quando o conteúdo estiver sendo republicado e o CDN respeitar os cabeçalhos de expiração do cache.

### Invalidação de cache do Dispatcher durante a ativação/desativação {#cache-activation-deactivation}

Como nas versões anteriores do AEM, a publicação ou o cancelamento da publicação de páginas limpa o conteúdo do cache do Dispatcher. Se houver suspeita de um problema de armazenamento em cache, você deve republicar as páginas em questão e garantir que um host virtual esteja disponível e corresponda à variável `ServerAlias` localhost, que é necessário para a invalidação do cache do Dispatcher.

>[!NOTE]
>Para invalidação adequada do dispatcher, verifique se as solicitações de &quot;127.0.0.1&quot;, &quot;localhost&quot;, &quot;.local&quot;, &quot;.adobeaemcloud.com&quot; e &quot;.adobeaemcloud.net&quot; são correspondidas e tratadas por uma configuração de vhost para que essa solicitação possa ser atendida. Você pode fazer isso fazendo a correspondência global &quot;*&quot; em uma configuração vhost catch-all seguindo o padrão na referência [AEM arquétipo](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost) ou assegurando que a lista anteriormente mencionada seja capturada por um dos vhosts.

Quando a instância de publicação recebe uma nova versão de uma página ou ativo do autor, ela usa o agente de limpeza para invalidar os caminhos apropriados em seu Dispatcher. O caminho atualizado é removido do cache do Dispatcher, junto com seus pais, até um nível (você pode configurar isso com o [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

## Invalidação explícita do cache do Dispatcher {#explicit-invalidation}

O Adobe recomenda confiar em cabeçalhos de cache padrão para controlar o ciclo de vida da entrega de conteúdo. No entanto, se necessário, é possível invalidar o conteúdo diretamente no Dispatcher.

A lista a seguir contém cenários em que você pode querer invalidar explicitamente o cache (enquanto, opcionalmente, escuta a conclusão da invalidação):

* Após publicar o conteúdo, como fragmentos de experiência ou fragmentos de conteúdo, invalidar o conteúdo publicado e armazenado em cache que faz referência a esses elementos.
* Notificar um sistema externo quando as páginas referenciadas tiverem sido invalidadas com êxito.

Há duas abordagens para invalidar explicitamente o cache:

* A abordagem preferencial é usar a Distribuição de conteúdo de sling (SCD) do autor.
* Ao usar a API Replicação para chamar o agente de replicação de liberação do Dispatcher de publicação.

As abordagens diferem em termos de disponibilidade de camada, da capacidade de desduplicar eventos e da garantia de processamento de eventos. A tabela abaixo resume essas opções:

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>N/A</th>
    <th>Disponibilidade de nível</th>
    <th>Desduplicação </th>
    <th>Garantia </th>
    <th>Ação </th>
    <th>Impacto </th>
    <th>Descrição </th>
  </tr>  
  <tr>
    <td>API Sling Content Distribution (SCD)</td>
    <td>Autor</td>
    <td>Possível usando a API de descoberta ou habilitando a variável <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">modo de desduplicação</a>.</td>
    <td>Pelo menos uma vez.</td>
    <td>
     <ol>
       <li>ADICIONAR</li>
       <li>EXCLUIR</li>
       <li>INVALIDAR</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Hierárquico/Nível de Estado</li>
       <li>Hierárquico/Nível de Estado</li>
       <li>Nível Somente Recurso</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Publica conteúdo e invalida o cache.</li>
       <li>Remove o conteúdo e invalida o cache.</li>
       <li>Invalida o conteúdo sem publicá-lo.</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>API de replicação</td>
    <td>Publicação</td>
    <td>Não possível, evento gerado em cada instância de publicação.</td>
    <td>Melhor esforço.</td>
    <td>
     <ol>
       <li>ATIVAR</li>
       <li>DESATIVAR</li>
       <li>EXCLUIR</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Hierárquico/Nível de Estado</li>
       <li>Hierárquico/Nível de Estado</li>
       <li>Hierárquico/Nível de Estado</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Publica conteúdo e invalida o cache.</li>
       <li>Da camada Autor/Publicação - Remove o conteúdo e invalida o cache.</li>
       <li><p><strong>Da camada do autor</strong> - Remove o conteúdo e invalida o cache (se acionado do nível de Autor do AEM no agente de Publicação).</p>
           <p><strong>Da camada de publicação</strong> - Invalida somente o cache (se disparado do nível de Publicação do AEM no agente de Liberação ou de Liberação Somente Recurso).</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

Observe que as duas ações diretamente relacionadas à invalidação do cache são Invalidar a API da Distribuição de conteúdo de sling (SCD) e Desativar a API de replicação.

Além disso, a partir da tabela, observamos que:

* A API SCD é necessária quando todos os eventos devem ser garantidos, por exemplo, sincronização com um sistema externo que requer conhecimento preciso. Se houver um evento de aumento do nível de publicação no momento da chamada de invalidação, um evento adicional será gerado quando cada nova publicação processar a invalidação.

* O uso da API de replicação não é um caso de uso comum, mas deve ser usado nos casos em que o acionador para invalidar o cache vem do nível de publicação e não do nível de criação. Isso pode ser útil se o TTL do dispatcher estiver configurado.

Em conclusão, se você estiver procurando invalidar o cache do Dispatcher, a opção recomendada é usar a ação Invalidar API SCD do Autor. Além disso, você também pode acompanhar o evento para depois acionar outras ações de downstream.

### Distribuição de conteúdo de sling (SCD) {#sling-distribution}

>[!NOTE]
>Ao usar as instruções apresentadas abaixo, esteja ciente de que você deve testar o código personalizado em um ambiente de desenvolvimento AEM Cloud Service e não localmente.

Ao usar a ação SCD do Autor, o padrão de implementação é o seguinte:

1. Do autor, escreva o código personalizado para chamar a distribuição de conteúdo do sling [API](https://sling.apache.org/documentation/bundles/content-distribution.html), transmitindo a ação de invalidação com uma lista de caminhos:

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* (Opcionalmente) Analise um evento que reflita o recurso que está sendo invalidado para todas as instâncias do Dispatcher:


```
package org.apache.sling.distribution.journal.shared;

import org.apache.sling.discovery.DiscoveryService;
import org.apache.sling.distribution.journal.impl.event.DistributionEvent;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import static org.apache.sling.distribution.DistributionRequestType.INVALIDATE;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_PATHS;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_TYPE;
import static org.apache.sling.distribution.event.DistributionEventTopics.AGENT_PACKAGE_DISTRIBUTED;
import static org.osgi.service.event.EventConstants.EVENT_TOPIC;

@Component(immediate = true, service = EventHandler.class, property = {
        EVENT_TOPIC + "=" + AGENT_PACKAGE_DISTRIBUTED
})
public class InvalidatedHandler implements EventHandler {
    private static final Logger LOG = LoggerFactory.getLogger(InvalidatedHandler.class);

    @Reference
    private DiscoveryService discoveryService;

    @Override
    public void handleEvent(Event event) {

        String distributionType = (String) event.getProperty(DISTRIBUTION_TYPE);

        if (INVALIDATE.name().equals(distributionType)) {
            boolean isLeader = discoveryService.getTopology().getLocalInstance().isLeader();
            // process the OSGi event on the leader author instance
            if (isLeader) {
                String[] paths = (String[]) event.getProperty(DISTRIBUTION_PATHS);
                String packageId = (String) event.getProperty(DistributionEvent.PACKAGE_ID);
                invalidated(paths, packageId);
            }
        }
    }

    private void invalidated(String[] paths, String packageId) {
        // custom logic
        LOG.info("Successfully applied package with id {}, paths {}", packageId, paths);
    }
}
```

<!-- Optionally, instead of using the isLeader approach, one could add an OSGi configuration for the PID org.apache.sling.distribution.journal.impl.publisher.DistributedEventNotifierManager and property deduplicateEvent=true. But we'll stick with just one strategy and not mention it (double-check this).**review this**-->

* (Opcionalmente) Execute a lógica comercial no `invalidated(String[] paths, String packageId)` acima.

>[!NOTE]
>
>O Adobe CDN não é liberado quando o Dispatcher é invalidado. A CDN gerenciada por Adobe respeita os TTLs e, portanto, não há necessidade de liberá-la.

### API de replicação {#replication-api}

Apresentado abaixo é o padrão de implementação ao usar a ação de desativação da API de replicação:

1. No nível de publicação, chame a API Replicação para acionar o agente de replicação de liberação do Dispatcher de publicação.

O endpoint do agente de limpeza não é configurável, mas sim pré-configurado para apontar para o Dispatcher, correspondente ao serviço de publicação em execução junto com o agente de limpeza.

O agente de limpeza geralmente pode ser acionado por código personalizado com base em eventos ou fluxos de trabalho OSGi.

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals(“flush”);
  }
});

Replicator.replicate (session,ReplicationActionType.DELETE,paths, options);
```

<!-- In general, it will not be necessary to manually invalidate content in the dispatcher, but it is possible if needed.

>[!NOTE]
>Prior to AEM as a Cloud Service, there were two ways of invalidating the dispatcher cache.
>
>1. Invoke the replication agent, specifying the publish dispatcher flush agent
>2. Directly calling the `invalidate.cache` API (for example, `POST /dispatcher/invalidate.cache`)
>
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache isn't clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

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
1. Salve as alterações. Não é necessário salvar essa configuração no controle de origem, pois AEM as a Cloud Service ativa automaticamente essa configuração em ambientes de desenvolvimento, estágio e produção.
1. Sempre que o conteúdo da biblioteca do cliente for alterado, uma nova chave de hash será gerada e a referência de HTML será atualizada.
