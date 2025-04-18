---
title: Configuração do tráfego no CDN
description: Saiba como configurar o tráfego CDN declarando regras e filtros em um arquivo de configuração e implantando-os no CDN usando um pipeline de configuração do Cloud Manager.
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: a43fdc3f9b9ef502eb0af232b1c6aedbab159f1f
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 1%

---


# Configuração do tráfego no CDN {#cdn-configuring-cloud}

AEM como um Cloud Service oferece uma coleção de recursos configuráveis na [camada de CDN gerenciada Adobe Systems](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) que modifica a natureza de solicitações recebidas ou respostas de saída. As seguintes regras, descritas detalhadamente nesta página, podem ser declaradas para alcançar o seguinte comportamento:

* [Transformações de solicitação](#request-transformations) : modifique aspectos de solicitações recebidas, incluindo cabeçalhos, caminhos e parâmetros.
* [Transformações de resposta](#response-transformations) - modifique cabeçalhos que estão no caminho de volta para o cliente (por exemplo, um navegador da Web).
* [Redirecionamentos do lado do servidor](#server-side-redirectors) - acione um redirecionamento do navegador.
* [Seletores de origem](#origin-selectors) - proxy para um back-end de origem diferente.

Também podem ser configuradas na CDN as Regras de filtro de tráfego (incluindo o WAF), que controlam qual tráfego é permitido ou negado pela CDN. Esse recurso já foi lançado e você pode saber mais sobre ele nas [Regras de Filtrar de Tráfego, incluindo regras](/help/security/traffic-filter-rules-including-waf.md) de WAF página.

Além disso, se o CDN não puder entrar em contato com sua origem, você pode escrever uma regra que referencie um erro personalizado auto-hospedado página (que é então renderizado). Saiba mais sobre isso lendo o artigo de páginas](/help/implementing/dispatcher/cdn-error-pages.md) de erro de [configuração CDN.

Todas essas regras, declaradas em um arquivo de configuração no controle de origem, são implantadas usando o pipeline](/help/operations/config-pipeline.md) de configuração do Cloud Manager[. Esteja ciente de que o tamanho cumulativo do arquivo de configuração, incluindo tráfego regras de filtro, não pode exceder 100 KB.

## Ordem de avaliação {#order-of-evaluation}

Funcionalmente, os vários recursos mencionados anteriormente são avaliados na seguinte sequência:

![Ordem de avaliação](/help/implementing/dispatcher/assets/order.png)

## Configurar {#initial-setup}

Antes de configurar tráfego no CDN é necessário fazer o seguinte:

1. Criar um arquivo nomeado `cdn.yaml` ou similar, fazendo referência aos vários trechos de configuração nas seções abaixo.

   Todos os trechos têm essas propriedades comuns, que são descritas em [Pipeline de configuração](/help/operations/config-pipeline.md#common-syntax). O `kind` valor propriedade deve ser *CDN* e o `version` propriedade deve ser definido como *1*.

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   ```

1. Coloque o arquivo em algum lugar em uma pasta de nível superior chamada *config* ou similar, conforme descrito em [Pipeline de configuração](/help/operations/config-pipeline.md#folder-structure).

1. Crie um Pipeline de configuração no Cloud Manager, conforme descrito em [Pipeline de configuração](/help/operations/config-pipeline.md#managing-in-cloud-manager).

1. Implante a configuração.

## Sintaxe de regras {#configuration-syntax}

Os tipos de regra nas seções abaixo compartilham uma sintaxe comum.

Uma regra é referenciada por um nome, uma &quot;cláusula when&quot; condicional e ações.

A cláusula when determina se uma regra será avaliada com base nas propriedades, incluindo domínio, caminho, sequências de consulta, cabeçalhos e cookies. A sintaxe é a mesma nos tipos de regras; para obter detalhes, consulte a [seção Estrutura de condição](/help/security/traffic-filter-rules-including-waf.md#condition-structure), no artigo Regras de filtro de tráfego.

Os detalhes do nó de ações diferem por tipo de regra e são descritos nas seções individuais abaixo.

## Solicitar transformações {#request-transformations}

As regras de transformação de solicitação permitem modificar solicitações recebidas. As regras oferecem suporte para a configuração, remoção e alteração de caminhos, parâmetros de consulta e cabeçalhos (incluindo cookies) com base em várias condições correspondentes, incluindo expressões regulares. Também é possível definir variáveis, que podem ser referenciadas posteriormente na sequência de avaliação.

Os casos de uso são variados e incluem reescritas URL para aplicativo simplificação ou mapeamento de URLs herdados.

Como mencionado anteriormente, há um limite de tamanho para o arquivo de configuração, de modo que organizações com requisitos maiores definam regras na `apache/dispatcher` camada.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  requestTransformations:
    removeMarketingParams: true
    rules:
      - name: set-header-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: some value
      - name: set-header-with-reqproperty-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: {reqProperty: path}
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header

      - name: unset-matching-query-params-rule
        when:
          reqProperty: path
          equals: /unset-matching-query-params
        actions:
          - type: unset
            queryParamMatch: ^removeMe_.*$

      - name: unset-all-query-params-except-exact-two-rule
        when:
          reqProperty: path
          equals: /unset-all-query-params-except-exact-two
        actions:
          - type: unset
            queryParamMatch: ^(?!leaveMe$|leaveMeToo$).*$

      - name: multi-action
        when:
          reqProperty: path
          like: /multi-action
        actions:
          - type: set
            reqHeader: x-header1
            value: body set by transformation rule
          - type: set
            reqHeader: x-header2
            value: '201'

      - name: replace-html
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: \.html$
            replacement: ""
```

**Ações**

Explicadas na tabela abaixo estão as ações disponíveis.

| Nome | Propriedades | Significado |
|-----------|--------------------------|-------------|
| **conjunto** | (reqProperty ou reqHeader ou queryParam ou reqCookie), valor | Define um parâmetro de solicitação especificado (somente a propriedade &quot;path&quot; é compatível), ou o cabeçalho de solicitação, parâmetro de consulta ou cookie, para um determinado valor, que pode ser um literal de cadeia de caracteres ou parâmetro de solicitação. |
|     | var, value | Define uma propriedade de solicitação especificada para um determinado valor. |
| **não definido** | reqProperty | Remove um parâmetro de solicitação especificado (somente &quot;path&quot; propriedade suportado), ou solicitação cabeçalho, query parâmetro ou cookie, para um determinado valor, que pode ser um parâmetro literal de string ou solicitação. |
|         | var | Remove um variável especificado. |
|         | queryParamMatch | Remove todos os parâmetros query que correspondem a um expressão regular especificado. |
|         | queryParamDoesNotMatch | Remove todos os parâmetros de consulta que não correspondem a uma expressão regular especificada. |
| **transformar** | op:replace, (reqProperty ou reqHeader ou queryParam ou reqCookie ou var), match, replacement | Substitui parte do parâmetro de solicitação (somente a propriedade &quot;path&quot; é compatível), o cabeçalho de solicitação, o parâmetro de consulta, o cookie ou a variável por um novo valor. |
|              | op:tolower, (reqProperty ou reqHeader ou queryParam ou reqCookie ou var) | Define o parâmetro de solicitação (somente a propriedade &quot;path&quot; é compatível), o cabeçalho de solicitação, o parâmetro de consulta, o cookie ou a variável com seu valor em minúsculas. |

As ações de substituição oferecem suporte aos grupos de captura, conforme ilustrado abaixo:

```
      - name: extract-country-code-from-path
        when:
          reqProperty: path
          matches: ^/([a-zA-Z]{2})(/.*|$)
        actions:
          - type: set
            var: country-code
            value:
              reqProperty: path
          - type: transform
            var: country-code
            op: replace
            match: ^/([a-zA-Z]{2})(/.*|$)
            replacement: \1
      - name: replace-jpg-with-jpeg
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: (.*)(\.jpg)$
            replacement: "\1\.jpeg"
```

As ações podem ser encadeadas. Por exemplo:

```
actions:
    - type: transform
      reqProperty: path
      op: replace
      match: \.html$
      replacement: ""
    - type: transform
      reqProperty: path
      op: tolower
```

### Variáveis {#variables}

É possível definir variáveis durante a transformação da solicitação e, em seguida, referenciá-las posteriormente na sequência de avaliação. Consulte o [solicitar do diagrama de avaliação](#order-of-evaluation) para obter mais detalhes.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value

  responseTransformations:
    rules:
      - name: set-response-header-while-variable
        when:
          var: some_var_name
          equals: some_value
        actions:
          - type: set
            respHeader: x-some-header
            value: some header value
```

## Transformações de resposta {#response-transformations}

As regras de transformação de resposta permitem definir e não definir cabeçalhos das respostas de saída do CDN. Além disso, consulte o exemplo acima para fazer referência a uma variável previamente definida em uma regra de transformação de solicitação. O código de status da resposta também pode ser definido.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  responseTransformations:
    rules:
      - name: set-response-header-rule
        when:
          reqProperty: path
          like: /set-response-header
        actions:
          - type: set
            value: value-set-by-resp-rule
            respHeader: x-resp-header

      - name: unset-response-header-rule
        when:
          reqProperty: path
          like: /unset-response-header
        actions:
          - type: unset
            respHeader: x-header1

      # Example: Multi-action on response header
      - name: multi-action-response-header-rule
        when:
          reqProperty: path
          like: /multi-action-response-header
        actions:
          - type: set
            respHeader: x-resp-header-1
            value: value-set-by-resp-rule-1
          - type: set
            respHeader: x-resp-header-2
            value: value-set-by-resp-rule-2
      # Example: setting status code
      - name: status-code-rule
        when:
          reqProperty: path
          like: status-code
        actions:
          - type: set
            respProperty: status
            value: '410'        
```

**Ações**

Explicadas na tabela abaixo estão as ações disponíveis.

| Nome | Propriedades | Significado |
|-----------|--------------------------|-------------|
| **conjunto** | reqHeader, valor | Define um cabeçalho especificado para um determinado valor na resposta. |
|          | respProperty, valor | Define uma propriedade de resposta. Suporta apenas o propriedade &quot;status&quot; no solicitar para definir o código do status. |
| **Unset** | respHeader | Remove um cabeçalho especificado da resposta. |

## Seletores de origem {#origin-selectors}

Você pode aproveitar a CDN da AEM para rotear o tráfego para diferentes back-ends, incluindo aplicativos que não sejam da Adobe (talvez por caminho ou subdomínio).

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy* }
        action:
          type: selectOrigin
          originName: example-com
          # skipCache: true
    origins:
      - name: example-com
        domain: www.example.com
        # ip: '1.1.1.1'
        # forwardHost: true
        # forwardCookie: true
        # forwardAuthorization: true
        # timeout: 20
```

**Ações**

A ação disponível é explicada na tabela abaixo.

| Nome | Propriedades | Significado |
|-----------|--------------------------|-------------|
| **selectOrigin** | originName | Nome de uma das origens definidas. |
|     | skipCache (opcional, o padrão é falso) | Sinalize se deve usar armazenamento em cache para solicitações que correspondam a esse regra. Por padrão, as respostas serão armazenadas em cache de acordo com a resposta armazenamento em cache cabeçalho (por exemplo, Cache-Control ou Expires) |

**Origens**

As conexões com as origens são somente SSL e usam a porta 443.

| Propriedade | Significado |
|------------------|--------------------------------------|
| **nome** | Nome que pode ser referenciado por &quot;action.originName&quot;. |
| **domínio** | Nome do domínio usado para conectar ao back-end personalizado. Ele também é usado para SNI e validação SSL. |
| **ip** (opcional, com suporte para iv4 e ipv6) | Se fornecido, ele será usado para se conectar ao back-end em vez de ao &quot;domínio&quot;. O &quot;domínio&quot; ainda é usado para SNI e validação SSL. |
| **forwardHost** (opcional, o padrão é falso) | Se estiver definido como true, o cabeçalho &quot;Host&quot; do cliente solicitação será passado para o backend, caso contrário, o valor &quot;domínio&quot; será passado no cabeçalho &quot;Host&quot;. |
| **forwardCookie** (opcional, o padrão é false) | Se estiver definido como true, o cabeçalho &quot;Cookie&quot; do cliente solicitação será passado para o backend, caso contrário, o cabeçalho cookie será removido. |
| **forwardAuthorization** (opcional, o padrão é false) | Se estiver definido como true, o cabeçalho &quot;Autorização&quot; do cliente solicitação será passado para o backend, caso contrário, o cabeçalho de Autorização será removido. |
| **tempo limite** (opcional, em segundos, o padrão é 60) | Número de segundos que o CDN deve aguardar até que um servidor de back-end forneça o primeiro byte de um corpo de resposta HTTP. Esse valor também é usado como um tempo limite entre bytes para o servidor de back-end. |

### Utilização de proxy para o Edge Delivery Services {#proxying-to-edge-delivery}

Há cenários em que os seletores de origem devem ser usados para rotear o tráfego por meio da Publicação do AEM para o AEM Edge Delivery Services:

* Parte do conteúdo é entregue por um domínio gerenciado pela AEM Publish, enquanto outro conteúdo do mesmo domínio é entregue pela Edge Delivery Services
* O conteúdo entregue pelo Edge Delivery Services se beneficiaria das regras implantadas por meio do pipeline de configuração, incluindo regras de filtro de tráfego ou transformações de solicitação/resposta

Este é um exemplo de uma regra de seletor de origem que pode fazer isso:

```
kind: CDN
version: '1'
data:
  originSelectors:
    rules:
      - name: select-edge-delivery-services-origin
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: <Production Host>
            - reqProperty: path
              matches: "^(/scripts/.*|/styles/.*|/fonts/.*|/blocks/.*|/icons/.*|.*/media_.*|/favicon.ico)"
        action:
          type: selectOrigin
          originName: aem-live
    origins:
      - name: aem-live
        domain: main--repo--owner.aem.live
```

>[!NOTE]
> Como a CDN Gerenciada pela Adobe é usada, certifique-se de configurar a invalidação por push no modo **gerenciado**, seguindo a [documentação de invalidação por push da Instalação](https://www.aem.live/docs/byo-dns#setup-push-invalidation) do Edge Delivery Services.


## Redirecionamentos do lado do servidor {#server-side-redirectors}

Você pode usar as regras de redirecionamento do lado do cliente para 301, 302 e redirecionamentos semelhantes do lado do cliente. Se um regra corresponder, o CDN responderá com uma linha de status que inclui o código do status e a mensagem (por exemplo, HTTP/1.1 301 Movido permanentemente), bem como o conjunto do cabeçalho da localização.

Os locais absolutos e relativos com valores fixos são permitidos.

Esteja ciente de que o tamanho cumulativo do arquivo de configuração, incluindo tráfego regras de filtro, não pode exceder 100 KB.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  redirects:
    rules:
      - name: redirect-absolute
        when: { reqProperty: path, equals: "/page.html" }
        action:
          type: redirect
          status: 301
          location: https://example.com/page
      - name: redirect-relative
        when: { reqProperty: path, equals: "/anotherpage.html" }
        action:
          type: redirect
          location: /anotherpage
```

| Nome | Propriedades | Significado |
|-----------|--------------------------|-------------|
| **redirecionar** | localização | Valor para o cabeçalho &quot;Localização&quot;. |
|     | Status (opcional, o padrão é 301) | Status HTTP a ser usado na mensagem de redirecionamento, 301 por padrão, os valores permitidos são: 301, 302, 303, 307, 308. |

Os locais de um redirecionamento podem ser literais de cadeia de caracteres (por exemplo, https://www.example.com/page) ou o resultado de uma propriedade (por exemplo, caminho) que é transformada opcionalmente, com a seguinte sintaxe:

```
redirects:
  rules:
    - name: country-code-redirect
      when: { reqProperty: path, like: "/" }
      action:
        type: redirect
        location:
          reqProperty: clientCountry
          transform:
            - op: replace
              match: '^(.*)$'
              replacement: 'https://www.example.com/\1/home'
            - op: tolower
    - name: www-redirect
      when: { reqProperty: domain, equals: "example.com" }
      action:
        type: redirect
        location:
          reqProperty: url
          transform:
            - op: replace
              match: '^/(.*)$'
              replacement: 'https://www.example.com/\1'
```
