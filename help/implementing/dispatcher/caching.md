---
title: Armazenamento em cache no AEM as a Cloud Service
description: Saiba mais sobre as noções básicas de armazenamento em cache no AEM as a Cloud Service
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '2775'
ht-degree: 1%

---

# Introdução {#intro}

O tráfego passa pela CDN para uma camada de servidor Web Apache, que oferece suporte a módulos, incluindo o Dispatcher. Para aumentar o desempenho, o Dispatcher é usado principalmente como cache para limitar o processamento nos nós de publicação.
As regras podem ser aplicadas à configuração do Dispatcher para modificar qualquer configuração padrão de expiração de cache, resultando em cache na CDN. O Dispatcher também respeita os cabeçalhos de expiração de cache resultantes se `enableTTL` O é ativado na configuração do Dispatcher, o que significa que ele atualiza conteúdo específico mesmo fora do conteúdo que está sendo republicado.

Esta página também descreve como o cache do Dispatcher é invalidado e como o cache funciona no nível do navegador em relação às bibliotecas do lado do cliente.

## Armazenamento em cache {#caching}

### HTML/Texto {#html-text}

* por padrão, armazenado em cache pelo navegador por cinco minutos, com base na variável `cache-control` cabeçalho emitido pela camada do Apache. A CDN também respeita esse valor.
* a configuração padrão de cache de HTML/Texto pode ser desativada definindo o `DISABLE_DEFAULT_CACHING` variável em `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Esse método é útil, por exemplo, quando a lógica de negócios exige o ajuste fino do cabeçalho age (com um valor com base no dia do calendário), pois, por padrão, o cabeçalho age é definido como 0. Dito isto, **tenha cuidado ao desativar o cache padrão.**

* pode ser substituído para todo o conteúdo de HTML/Texto definindo o `EXPIRATION_TIME` variável em `global.vars` uso das ferramentas do Dispatcher do SDK as a Cloud Service do AEM.
* O pode ser substituído em um nível mais fino, incluindo o controle independente de CDN e cache do navegador, com o seguinte Apache `mod_headers` diretivas:

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header set Cache-Control "max-age=200"
       Header set Surrogate-Control "max-age=3600"
       Header set Age 0
  </LocationMatch>
  ```

  >[!NOTE]
  >O cabeçalho Surrogate-Control se aplica ao CDN gerenciado por Adobe. Se estiver usando um [CDN gerenciada pelo cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html#point-to-point-CDN), um cabeçalho diferente pode ser necessário, dependendo do provedor de CDN.

  Tenha cuidado ao definir cabeçalhos de controle de cache global ou cabeçalhos de cache semelhantes que correspondam a um regex amplo para que não sejam aplicados a conteúdo que você deve manter privado. Considere o uso de várias diretivas para garantir que as regras sejam aplicadas de maneira granular. Dito isso, o AEM as a Cloud Service remove o cabeçalho do cache se detectar que ele foi aplicado ao que ele detecta como não armazenável em cache pelo Dispatcher, conforme descrito na Documentação do Dispatcher. Para forçar o AEM a sempre aplicar os cabeçalhos de cache, é possível adicionar o **`always`** opção, como segue:

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header unset Cache-Control
       Header unset Expires
       Header always set Cache-Control "max-age=200"
       Header set Age 0
  </LocationMatch>
  ```

  Certifique-se de que um arquivo em `src/conf.dispatcher.d/cache` O tem a seguinte regra (que está na configuração padrão):

  ```
  /0000
  { /glob "*" /type "allow" }
  ```

* Para evitar que conteúdo específico seja armazenado em cache **na CDN**, defina o cabeçalho Cache-Control como *privado*. Por exemplo, o seguinte impediria o conteúdo html em um diretório chamado **seguro** de ser armazenado em cache na CDN:

  ```
     <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
     Header unset Cache-Control
     Header unset Expires
     Header always set Cache-Control "private"
    </LocationMatch>
  ```

* Embora o conteúdo HTML definido como privado não seja armazenado em cache no CDN, ele pode ser armazenado em cache no Dispatcher se [Armazenamento em cache sensível a permissões](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR) O está configurado, garantindo que somente usuários autorizados possam receber o conteúdo.

  >[!NOTE]
  >Os outros métodos, incluindo o [Projeto Dispatcher-ttl AEM ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), não substitui valores com êxito.

  >[!NOTE]
  >O Dispatcher ainda pode armazenar conteúdo em cache de acordo com sua própria configuração [regras de armazenamento em cache](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). Para tornar o conteúdo realmente privado, verifique se ele não está armazenado em cache pelo Dispatcher.

### Bibliotecas do lado do cliente (js,css) {#client-side-libraries}

* Ao usar a estrutura da biblioteca do lado do cliente AEM, o código JavaScript e CSS é gerado de forma que os navegadores podem armazená-lo em cache indefinidamente, já que qualquer alteração se manifesta como novos arquivos com um caminho exclusivo. Em outras palavras, o HTML que faz referência às bibliotecas de clientes é produzido conforme necessário, para que os clientes possam experimentar novo conteúdo conforme ele é publicado. O controle de cache é definido como &quot;imutável&quot; ou 30 dias para navegadores mais antigos que não respeitam o valor &quot;imutável&quot;.
* consulte a seção [Bibliotecas do lado do cliente e consistência de versão](#content-consistency) para obter detalhes adicionais.

### Imagens e qualquer conteúdo grande o suficiente para ser armazenado no armazenamento de blobs {#images}

O comportamento padrão para programas criados após meados de maio de 2022 (especificamente para ids de programa maiores que 65000) é armazenar em cache por padrão, respeitando também o contexto de autenticação da solicitação. Programas mais antigos (ids de programa iguais ou inferiores a 65000) não armazenam em cache conteúdo de blob por padrão.

Em ambos os casos, os cabeçalhos de cache podem ser substituídos em um nível mais fino na camada do Apache/Dispatcher usando o Apache `mod_headers` diretivas, por exemplo:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Ao modificar os cabeçalhos de cache na camada do Dispatcher, tenha cuidado para não armazenar em cache muito. Consulte a discussão na seção HTML/texto [acima](#html-text). Além disso, verifique se os ativos que devem ser mantidos privados (em vez de em cache) não fazem parte do `LocationMatch` filtros de diretiva.

Os recursos JCR (maiores que 16 KB) armazenados no armazenamento de blob normalmente são servidos como redirecionamentos 302 pelo AEM. Esses redirecionamentos são interceptados e seguidos pelo CDN e o conteúdo é entregue diretamente do armazenamento de blob. Somente um conjunto limitado de cabeçalhos pode ser personalizado nessas respostas. Por exemplo, para personalizar `Content-Disposition` você deve usar as diretivas do dispatcher da seguinte maneira:

```
<LocationMatch "\.(?i:pdf)$">
  ForceType application/pdf
  Header set Content-Disposition inline
  </LocationMatch>
```

A lista de cabeçalhos que podem ser personalizados em respostas de blob é:

```
content-security-policy
x-frame-options
x-xss-protection
x-content-type-options
x-robots-tag
access-control-allow-origin
content-disposition
permissions-policy
referrer-policy
x-vhost
content-disposition
cache-control
vary
```

#### Novo comportamento de cache padrão {#new-caching-behavior}

A camada AEM define cabeçalhos de cache dependendo se o cabeçalho de cache já foi definido e o valor do tipo de solicitação. Se nenhum cabeçalho de controle de cache for definido, o conteúdo público será armazenado em cache e o tráfego autenticado será definido como privado. Se um cabeçalho de controle de cache for definido, os cabeçalhos de cache serão deixados intocados.

| O cabeçalho de controle de cache existe? | Tipo de solicitação | AEM define cabeçalhos de cache como |
|------------------------------|---------------|------------------------------------------------|
| Não | público | Controle de cache: público, max-age=600, imutável |
| Não | autenticado | Cache-Control: private, max-age=600, imutável |
| Sim | qualquer | inalterado |

Embora não seja recomendado, é possível alterar o novo comportamento padrão para seguir o comportamento mais antigo (IDs de programa iguais ou inferiores a 65000) definindo a variável de ambiente do Cloud Manager `AEM_BLOB_ENABLE_CACHING_HEADERS` para falso.

#### Comportamento de cache padrão mais antigo {#old-caching-behavior}

A camada de AEM não armazena em cache conteúdo de blob por padrão.

>[!NOTE]
>Altere o comportamento padrão mais antigo para que seja consistente com o novo comportamento (IDs de programa maiores que 65000), definindo a variável de ambiente do Cloud Manager AEM_BLOB_ENABLE_CACHING_HEADERS como true. Se o programa já estiver ativo, verifique se, após as alterações, o conteúdo se comporta conforme esperado.

Agora, as imagens no armazenamento de blob marcadas como privadas não podem ser armazenadas em cache no Dispatcher usando [Armazenamento em cache sensível a permissões](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR). A imagem é sempre solicitada a partir da origem AEM e veiculada se o usuário estiver autorizado.

>[!NOTE]
>Os outros métodos, incluindo o [dispatcher-ttl projeto AEM ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), não substitua os valores com êxito.

### Outros tipos de arquivo de conteúdo no armazenamento de nós {#other-content}

* sem armazenamento em cache padrão
* o padrão não pode ser definido com o `EXPIRATION_TIME` variável usada para tipos de arquivo html/texto
* a expiração do cache pode ser definida com a mesma estratégia LocationMatch descrita na seção html/text especificando o regex apropriado

### Mais otimizações {#further-optimizations}

* Evite usar `User-Agent` como parte da `Vary` cabeçalho. As versões anteriores da configuração padrão do Dispatcher (antes da versão 28 do arquétipo) o incluíam e o Adobe recomenda que você o remova usando as etapas abaixo.
   * Localize os arquivos vhost em `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * Remova ou comente a linha: `Header append Vary User-Agent env=!dont-vary` de todos os arquivos vhost, exceto default.vhost, que é somente leitura
* Use o `Surrogate-Control` cabeçalho para controlar o cache do CDN independentemente do cache do navegador
* Considere aplicar [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) e [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) diretivas para permitir a atualização em segundo plano e evitar erros de cache, mantendo seu conteúdo rápido e atualizado para os usuários.
   * Há muitas maneiras de aplicar essas diretivas, mas é possível adicionar um intervalo de 30 minutos `stale-while-revalidate` para todos os cabeçalhos de controle de cache é um bom ponto de partida.
* Alguns exemplos seguem para vários tipos de conteúdo, que podem ser usados como guia ao configurar suas próprias regras de armazenamento em cache. Considere e teste cuidadosamente sua configuração e requisitos específicos:

   * Armazene em cache recursos mutáveis da biblioteca do cliente por 12 horas e atualize em segundo plano após 12 horas.

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Armazenar em cache recursos imutáveis da biblioteca do cliente a longo prazo (30 dias) com atualização em segundo plano para evitar o MISS.

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Armazene em cache páginas de HTML por cinco minutos com atualização em segundo plano uma hora no navegador e 12 horas no CDN. Os cabeçalhos de controle de cache são sempre adicionados, portanto, é importante garantir que as páginas html correspondentes em /content/* sejam destinadas a serem públicas. Caso contrário, considere usar um regex mais específico.

     ```
     <LocationMatch "^/content/.*\.html$">
        Header unset Cache-Control
        Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Armazene em cache as respostas json do exportador de modelo de Sling/Content Services por cinco minutos com atualização em segundo plano de uma hora no navegador e 12 horas no CDN.

     ```
     <LocationMatch "^/content/.*\.model\.json$">
        Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Armazene em cache URLs imutáveis do componente de imagem principal a longo prazo (30 dias) com atualização em segundo plano para evitar o MISS.

     ```
     <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Armazene em cache recursos mutáveis do DAM, como imagens e vídeos, por 24 horas e atualize em segundo plano após 12 horas para evitar o MISS.

     ```
     <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

### comportamento da solicitação HEAD {#request-behavior}

Quando uma solicitação HEAD é recebida na CDN Adobe para um recurso que é **não** Em cache, a solicitação é transformada e recebida pelo Dispatcher e/ou pela instância do AEM como uma solicitação do GET. Se a resposta for armazenável em cache, as solicitações de HEAD subsequentes serão enviadas pelo CDN. Se a resposta não puder ser armazenada em cache, as solicitações de HEAD subsequentes serão passadas para o Dispatcher, a instância do AEM ou ambas por um tempo que dependa do `Cache-Control` TTL

### Parâmetros da campanha de marketing {#marketing-parameters}

Os URLs do site frequentemente incluem parâmetros de campanha de marketing que são usados para rastrear o sucesso de uma campanha.

Para ambientes criados em outubro de 2023 ou posteriormente, para melhores solicitações de cache, a CDN removerá parâmetros de consulta comuns relacionados a marketing, especificamente aqueles que correspondem ao seguinte padrão regex:

```
^(utm_.*|gclid|gdftrk|_ga|mc_.*|trk_.*|dm_i|_ke|sc_.*|fbclid)$
```

Envie um tíquete de suporte se quiser que esse comportamento seja desativado.

Para ambientes criados antes de outubro de 2023, é recomendável definir as configurações do Dispatcher `ignoreUrlParams` propriedade como [documentado aqui](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters).


## Invalidação de cache do Dispatcher {#disp}

Em geral, não é necessário invalidar o cache do Dispatcher. Em vez disso, você deve confiar no Dispatcher atualizando seu cache quando o conteúdo estiver sendo republicado e o CDN respeitando os cabeçalhos de expiração de cache.

### Invalidação do cache do Dispatcher durante ativação/desativação {#cache-activation-deactivation}

Assim como as versões anteriores do AEM, publicar ou desfazer a publicação de páginas limpa o conteúdo do cache do Dispatcher. Se houver suspeita de um problema de armazenamento em cache, você deverá republicar as páginas em questão e garantir que um host virtual que corresponda à `ServerAlias` localhost, que é necessário para a invalidação do cache do Dispatcher.

>[!NOTE]
>Para a invalidação adequada do Dispatcher, verifique se as solicitações de &quot;127.0.0.1&quot;, &quot;localhost&quot;, &quot;.local&quot;, &quot;.adobeaemcloud.com&quot; e &quot;.adobeaemcloud.net&quot; são todas correspondidas e tratadas por uma configuração vhost para que a solicitação possa ser atendida. Você pode fazer essa tarefa ao fazer a correspondência global &quot;*&quot; em uma configuração do vhost &quot;catch-all&quot; seguindo o padrão na referência [Arquétipo de AEM](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost). Ou você pode garantir que a lista mencionada anteriormente seja capturada por um dos vhosts.

Quando a instância de publicação recebe uma nova versão de uma página ou ativo do autor, ela usa o agente de limpeza para invalidar caminhos apropriados em seu Dispatcher. O caminho atualizado é removido do cache do Dispatcher, junto com seus pais, até um nível (você pode configurar esse nível com o [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

## Invalidação explícita do cache do Dispatcher {#explicit-invalidation}

A Adobe recomenda que você confie nos cabeçalhos de cache padrão para controlar o ciclo de vida da entrega de conteúdo. No entanto, se necessário, é possível invalidar o conteúdo diretamente no Dispatcher.

A lista a seguir contém cenários em que talvez você queira invalidar explicitamente o cache (enquanto escuta, opcionalmente, a conclusão da invalidação):

* Após a publicação do conteúdo, como fragmentos de experiência ou fragmentos de conteúdo, a invalidação do conteúdo publicado e em cache que faz referência a esses elementos.
* Notificar um sistema externo quando as páginas referenciadas tiverem sido invalidadas com êxito.

Há duas abordagens para invalidar explicitamente o cache:

* A abordagem preferida é usar a Distribuição de conteúdo de sling (SCD) do autor.
* A outra abordagem é usar a API de replicação para chamar o agente de replicação de limpeza do Dispatcher de publicação.

As abordagens diferem em termos de disponibilidade de nível, capacidade de desduplicação de eventos e garantia de processamento de eventos. A tabela abaixo resume essas opções:

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
    <td>API de distribuição de conteúdo do Sling (SCD)</td>
    <td>Autor</td>
    <td>Possível usar a API de descoberta ou ativar o <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">modo de desduplicação</a>.</td>
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
       <li>Nível Hierárquico/Estat</li>
       <li>Nível Hierárquico/Estat</li>
       <li>Nivelar Somente Recurso</li>
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
       <li>Nível Hierárquico/Estat</li>
       <li>Nível Hierárquico/Estat</li>
       <li>Nível Hierárquico/Estat</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Publica conteúdo e invalida o cache.</li>
       <li>Da camada Autor/Publicação - Remove o conteúdo e invalida o cache.</li>
       <li><p><strong>Da camada de autor</strong> - Remove o conteúdo e invalida o cache (se acionado a partir da camada de autor do AEM no agente de Publicação).</p>
           <p><strong>Da camada de publicação</strong> - Invalida somente o cache (se acionado a partir da camada de publicação do AEM no agente de limpeza Flush ou Resource-only-flush ).</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

As duas ações diretamente relacionadas à invalidação de cache são Invalidação da API de distribuição de conteúdo do Sling (SCD) e Desativação da API de replicação.

Além disso, na tabela, você pode observar que:

* A API SCD é necessária quando cada evento deve ser garantido, por exemplo, sincronização com um sistema externo que requer conhecimento preciso. Se houver um evento de upscaling do nível de publicação no momento da chamada de invalidação, um evento extra será gerado quando cada nova publicação processar a invalidação.

* O uso da API de replicação não é um caso de uso comum, mas pode ser usado nos casos em que o acionador para invalidar o cache vem do nível de publicação e não do nível de criação. Esse método pode ser útil se o TTL do Dispatcher estiver configurado.

Concluindo, se você deseja invalidar o cache do Dispatcher, a opção recomendada é usar a ação Invalidar da API SCD do Author. Além disso, você também pode acompanhar o evento para acionar mais ações downstream.

### Distribuição de conteúdo de sling (SCD) {#sling-distribution}

>[!NOTE]
>Ao usar as instruções apresentadas abaixo, teste o código personalizado em um ambiente de Desenvolvimento do AEM Cloud Service e não localmente.

Ao usar a ação SCD do autor, o padrão de implementação é o seguinte:

1. No Autor, escreva o código personalizado para invocar a distribuição de conteúdo do sling [API](https://sling.apache.org/documentation/bundles/content-distribution.html), transmitindo a ação de invalidação com uma lista de caminhos:

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* (Opcionalmente) Acompanhe um evento que reflete o recurso que está sendo invalidado para todas as instâncias do Dispatcher:


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

* (Opcionalmente) Execute a lógica de negócios no `invalidated(String[] paths, String packageId)` acima.

>[!NOTE]
>
>O CDN do Adobe não é liberado quando o Dispatcher é invalidado. O CDN gerenciado por Adobe respeita TTLs e, portanto, não há necessidade de ele ser liberado.

### API de replicação {#replication-api}

Veja abaixo o padrão de implementação ao usar a ação Desativar da API de replicação:

1. No nível de publicação, chame a API de replicação para acionar o agente de replicação de limpeza do Dispatcher de publicação.

O ponto de extremidade do agente de limpeza não é configurável, mas pré-configurado para apontar para o Dispatcher, correspondente ao serviço de publicação em execução junto com o agente de limpeza.

O agente de limpeza geralmente pode ser acionado por um código personalizado com base em eventos OSGi ou workflows.

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals("flush");
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

If there is a concern that the dispatcher cache is not clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## Bibliotecas do lado do cliente e consistência de versão {#content-consistency}

As páginas são compostas por HTML, JavaScript, CSS e imagens. Os clientes são incentivados a usar o [Estrutura de bibliotecas do lado do cliente (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) para importar recursos JavaScript e CSS para páginas HTML, levando em conta as dependências entre as bibliotecas JS.

A estrutura clientlibs fornece gerenciamento automático de versões. Isso significa que os desenvolvedores podem fazer check-in das alterações nas bibliotecas JS no controle de origem e a versão mais recente é disponibilizada quando um cliente envia o lançamento. Sem esse fluxo de trabalho, os desenvolvedores devem alterar manualmente o HTML com referências à nova versão da biblioteca, o que é especialmente oneroso se a mesma biblioteca compartilhar muitos modelos de HTML.

Quando as novas versões das bibliotecas são lançadas para produção, as páginas de HTML de referência são atualizadas com novos links para essas versões atualizadas da biblioteca. Depois que o cache do navegador expira para uma determinada página de HTML, não há preocupação de que as bibliotecas antigas sejam carregadas do cache do navegador. O motivo é que a página atualizada (do AEM) agora garante a referência às novas versões das bibliotecas. Ou seja, uma página de HTML atualizada inclui todas as versões mais recentes da biblioteca.

O mecanismo por trás dessa capacidade é um hash serializado, que é anexado ao link da biblioteca do cliente. Ele garante um URL exclusivo com versão para que o navegador armazene em cache o CSS/JS. O hash serializado é atualizado somente quando o conteúdo da biblioteca do cliente é alterado. O que significa que, se ocorrerem atualizações não relacionadas (ou seja, sem alterações no css/js subjacente da biblioteca do cliente), mesmo com uma nova implantação, a referência permanecerá a mesma. Por sua vez, garante menos interrupções no cache do navegador.

### Ativação de versões de Longcache de bibliotecas do lado do cliente - Início rápido do SDK as a Cloud Service do AEM {#enabling-longcache}

As inclusões padrão de clientlib em uma página de HTML são semelhantes ao seguinte exemplo:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Quando o controle de versão estrito da clientlib é ativado, uma chave de hash de longo prazo é adicionada como seletor à biblioteca do cliente. Como resultado, a referência clientlib tem esta aparência:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

O controle de versão estrito do clientlib é ativado por padrão em todos os ambientes as a Cloud Service do AEM.

Para ativar o controle de versão estrito das bibliotecas de clientes no Quickstart do SDK local, faça o seguinte:

1. Navegue até o gerenciador de configurações do OSGi `<host>/system/console/configMgr`
1. Encontre a configuração OSGi para o gerenciador de biblioteca de HTML do Adobe Granite:
   * Marque a caixa de seleção para ativar o Controle de versão estrito
   * No campo rotulado **Chave de cache de longo prazo do cliente**, insira o valor de /.*;hash
1. Salve as alterações. Não é necessário salvar essa configuração no controle do código-fonte, pois o AEM as a Cloud Service ativa automaticamente essa configuração em ambientes de desenvolvimento, preparo e produção.
1. Sempre que o conteúdo da biblioteca do cliente é alterado, uma nova chave de hash é gerada e a referência de HTML é atualizada.
