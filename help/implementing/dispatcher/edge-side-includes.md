---
title: Edge Side Includes
description: O CDN do Adobe Managed agora é compatível com o Edge Side Includes (ESI), uma linguagem de marcação para a montagem de conteúdo dinâmico da Web no nível da borda.
feature: Dispatcher
exl-id: 35093477-2788-4f69-80a9-899f43567cae
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 2%

---

# Edge Side Includes {#edge-side-includes}

>[!NOTE]
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada, envie um email para `aemcs-cdn-config-adopter@adobe.com` e descreva seu caso de uso.

A velocidade de entrega de conteúdo se beneficia do armazenamento de páginas em cache de forma agressiva, obtida por meio da configuração de cabeçalhos de cache com valores de TTL (high time to live). Isso pode ser desafiador quando as páginas incluem conteúdo dinâmico, que precisa ser atualizado com frequência ou potencialmente não pode ser armazenado em cache. Felizmente, há estratégias em que a página de HTML pode ser armazenada em cache com um TTL alto, adiando a busca dos trechos de conteúdo mais dinâmicos para um momento posterior, por meio do Javascript do lado do cliente ou no CDN. A última abordagem é um padrão chamado Edge Side Includes (ESI), que é compatível com sites renderizados com a publicação do AEM. O HTML inclui tags ESI instruindo o CDN a adiar a veiculação da página no navegador até que ele avalie essas tags, recuperando conteúdo adicional e mais dinâmico (TTL mais baixo) da origem (ou cache CDN se o TTL não tiver expirado).

Alguns casos de uso em que as Inclusões do Edge Side podem ser úteis:

* Exibir o nome de um usuário final ou outras informações exclusivas de um usuário final.
* Exibir uma lista de informações recentes, como artigos de notícias ou preços de ações.

## Sintaxe ESI {#esi-syntax}

A sintaxe ESI é a seguinte se uma página pai `/content/page.html` incluir um trecho `content/snippets/mysnippet.html`.

```
<html>
  <head>
      <title>My Site</title>
  </head>
  <body>
    <div id="content">
      <esi:include src="/content/snippets/mysnippet.html" />
    </div>
  </body>
</html>
```

Consulte a [especificação ESI](https://www.w3.org/TR/esi-lang/) para obter detalhes.

### Considerações {#esi-syntax-considerations}

* As seguintes tags ESI são compatíveis: include, comment, remove.
* As tags ESI são processadas na CDN sequencialmente em vez de simultaneamente, portanto, muitas tags ESI em uma página com TTLs baixos podem adicionar latência à experiência do usuário final.
* A profundidade máxima de ESI: processamento de inclusão é 5.
* O total máximo de ESI: incluir fragmentos de processamento é 256.


## Configuração do Apache {#esi-apache}

Se você tiver páginas com tags ESI, deve declarar as seguintes propriedades na configuração do Apache:

```
<LocationMatch "/parent-pages/*content/page.html">
   # disable dispatcher compression
   SetEnv no-gzip 1
   # enable esi processing 
   Header set x-aem-esi "on"
   # enable edgeCDN compression
   Header set x-aem-compress "on"

   # typically the main page is cached at the CDN
   Header always set Cache-Control "max-age=300"
 </LocationMatch>


<LocationMatch "/content/snippets/mysnippet.html">
  SetEnv no-gzip 1

  # typically the included page is either set to a lower TTL than the parent page, or not cached at all, as these 2 commented declarations show, respectively:
  #Header always set Cache-Control "no-cache"
  #Header always set Cache-Control "max-age=50"
 </LocationMatch> 
```

As propriedades configuradas têm o seguinte comportamento:

| Propriedade | Comportamento |
|-----------|--------------------------|
| **no-gzip** | Se definida como 1, a página de HTML será transmitida do Apache para o CDN descompactado. Isso é necessário para a ESI, pois o conteúdo deve ser enviado para o CDN descompactado para que o CDN possa visualizar e avaliar as tags ESI.<br/><br/>A página pai e os trechos incluídos devem definir no-gzip como 1.<br/><br/>Essa configuração substitui qualquer configuração de compactação que o Apache tenha usado de outra forma, com base nos valores `Accept-Encoding` da solicitação. |
| **x-aem-esi** | Se definido como &quot;ativado&quot;, o CDN avaliará as tags ESI da página de HTML principal.  Por padrão, o cabeçalho não está definido. |
| **x-aem-compress** | Se definido como &quot;ativado&quot;, o CDN compactará o conteúdo do CDN para o navegador. Como a transmissão da página pai do Apache para o CDN deve ser descompactada para que o ESI funcione (`no-gzip` definido como 1), isso pode reduzir a latência.<br/><br/>Se esse cabeçalho não estiver definido, quando o CDN recuperar o conteúdo da origem descompactada, ele também fornecerá conteúdo ao cliente descompactado. Portanto, é necessário definir esse cabeçalho se `no-gzip` estiver definido como 1 (necessário para ESI) e se desejar veicular conteúdo compactado da CDN para o navegador. |

## Sling Dynamic Include {#esi-sdi}

Embora não seja obrigatório, o [Sling Dynamic Include](https://sling.apache.org/documentation/bundles/dynamic-includes.html) (SDI) pode ser usado para gerar trechos ESI que são interpretados na CDN.
