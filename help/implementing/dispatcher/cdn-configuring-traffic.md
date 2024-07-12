---
title: Configuração do tráfego no CDN
description: Saiba como configurar o tráfego CDN declarando regras e filtros em um arquivo de configuração e implantando-os no CDN usando o Pipeline de configuração do Cloud Manager.
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: c34aa4ad34d3d22e1e09e9026e471244ca36e260
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 1%

---

# Configuração do tráfego no CDN {#cdn-configuring-cloud}

O AEM as a Cloud Service oferece uma coleção de recursos configuráveis na camada [CDN gerenciado por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) que modificam a natureza das solicitações de entrada ou respostas de saída. As seguintes regras, descritas em detalhes nesta página, podem ser declaradas para alcançar o seguinte comportamento:

* [Solicitar transformações](#request-transformations) - modifique aspectos de solicitações de entrada, incluindo cabeçalhos, caminhos e parâmetros.
* [Transformações de resposta](#response-transformations) - modifique cabeçalhos que estão no caminho de volta para o cliente (por exemplo, um navegador da Web).
* [Redirecionamentos do lado do cliente](#client-side-redirectors) - acione um redirecionamento de navegador. Esse recurso ainda não está disponível para disponibilidade geral, mas para os participantes iniciais.
* [Seletores de origem](#origin-selectors) - proxy para um back-end de origem diferente.

Também podem ser configuradas na CDN as Regras de filtro de tráfego (incluindo o WAF), que controlam qual tráfego é permitido ou negado pela CDN. Este recurso já foi lançado e você pode saber mais sobre ele na página [Regras de filtro de tráfego, incluindo regras WAF](/help/security/traffic-filter-rules-including-waf.md).

Além disso, se a CDN não puder entrar em contato com sua origem, você poderá escrever uma regra que faça referência a uma página de erro personalizada auto-hospedada (que é renderizada). Saiba mais sobre isso lendo o artigo [Configurando páginas de erro de CDN](/help/implementing/dispatcher/cdn-error-pages.md).

Todas essas regras, declaradas em um arquivo de configuração no controle do código-fonte, são implantadas usando o [Pipeline de Configuração do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Observe que o tamanho cumulativo do arquivo de configuração, incluindo as regras de filtro de tráfego, não pode exceder 100 KB.

## Ordem de avaliação {#order-of-evaluation}

Funcionalmente, os vários recursos mencionados anteriormente são avaliados na seguinte sequência:

![imagem](/help/implementing/dispatcher/assets/order.png)

## Configurar {#initial-setup}

Antes de configurar o tráfego na CDN, é necessário fazer o seguinte:

* Crie esta pasta e estrutura de arquivo na pasta de nível superior do seu projeto Git:

```
config/
     cdn.yaml
```

* O arquivo de configuração `cdn.yaml` deve conter metadados e as regras descritas nos exemplos abaixo. O parâmetro `kind` deve ser definido como `CDN` e a versão deve ser definida como a versão do esquema, que atualmente é `1`.

* Crie um pipeline de configuração de implantação direcionada no Cloud Manager. Consulte [configuração de pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e [configuração de pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

**Notas**

* Atualmente, os RDEs não oferecem suporte ao pipeline de configuração.
* Você pode usar `yq` para validar localmente a formatação YAML do seu arquivo de configuração (por exemplo, `yq cdn.yaml`).

## Sintaxe {#configuration-syntax}

Os tipos de regra nas seções abaixo compartilham uma sintaxe comum.

Uma regra é referenciada por um nome, uma &quot;cláusula when&quot; condicional e ações.

A cláusula when determina se uma regra será avaliada com base nas propriedades, incluindo domínio, caminho, sequências de consulta, cabeçalhos e cookies. A sintaxe é a mesma nos tipos de regras; para obter detalhes, consulte a [seção Estrutura de condição](/help/security/traffic-filter-rules-including-waf.md#condition-structure), no artigo Regras de filtro de tráfego.

Os detalhes do nó de ações diferem por tipo de regra e são descritos nas seções individuais abaixo.

## Solicitar transformações {#request-transformations}

As regras de transformação de solicitação permitem modificar solicitações recebidas. As regras oferecem suporte para a configuração, remoção e alteração de caminhos, parâmetros de consulta e cabeçalhos (incluindo cookies) com base em várias condições correspondentes, incluindo expressões regulares. Também é possível definir variáveis, que podem ser referenciadas posteriormente na sequência de avaliação.

Os casos de uso são variados e incluem regravações de URL para simplificação de aplicativos ou mapeamento de URLs herdados.

Como mencionado anteriormente, há um limite de tamanho para o arquivo de configuração, portanto, as organizações com requisitos maiores devem definir regras na camada `apache/dispatcher`.

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

As ações disponíveis são explicadas na tabela abaixo.

| Nome | Propriedades | Significado |
|-----------|--------------------------|-------------|
| **conjunto** | (reqProperty ou reqHeader ou queryParam ou reqCookie), valor | Define um parâmetro de solicitação especificado (somente a propriedade &quot;path&quot; é compatível), ou o cabeçalho de solicitação, parâmetro de consulta ou cookie, para um determinado valor. |
|     | var, value | Define uma propriedade de solicitação especificada para um determinado valor. |
| **não definido** | reqProperty | Remove um parâmetro de solicitação especificado (somente a propriedade &quot;path&quot; é suportada), ou o cabeçalho de solicitação, parâmetro de consulta, ou cookie, para um determinado valor. |
|         | var | Remove uma variável especificada. |
|         | queryParamMatch | Remove todos os parâmetros de consulta que correspondem a uma expressão regular especificada. |
| **transformar** | op:replace, (reqProperty ou reqHeader ou queryParam ou reqCookie), match, replacement | Substitui parte do parâmetro de solicitação (somente a propriedade &quot;caminho&quot; é compatível) ou o cabeçalho de solicitação, parâmetro de consulta ou cookie por um novo valor. |
|              | op:tolower, (reqProperty ou reqHeader ou queryParam ou reqCookie) | Define o parâmetro de solicitação (somente a propriedade &quot;path&quot; é suportada), ou o cabeçalho de solicitação, parâmetro de consulta, ou cookie para seu valor em minúsculas. |

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

É possível definir variáveis durante a transformação da solicitação e, em seguida, referenciá-las posteriormente na sequência de avaliação. Consulte o diagrama [ordem da avaliação](#order-of-evaluation) para obter mais detalhes.

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

As regras de transformação de resposta permitem definir e não definir cabeçalhos das respostas de saída do CDN. Além disso, consulte o exemplo acima para fazer referência a uma variável previamente definida em uma regra de transformação de solicitação.

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
```

**Ações**

As ações disponíveis são explicadas na tabela abaixo.

| Nome | Propriedades | Significado |
|-----------|--------------------------|-------------|
| **conjunto** | reqHeader, valor | Define um cabeçalho especificado para um determinado valor na resposta. |
| **não definido** | respHeader | Remove um cabeçalho especificado da resposta. |

## Seletores de origem {#origin-selectors}

Você pode aproveitar a CDN do AEM para rotear o tráfego para diferentes back-ends, incluindo aplicativos que não sejam Adobe (talvez por caminho ou subdomínio).

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
        when: { reqProperty: path, like: /proxy-me* }
        action:
          type: selectOrigin
          originName: example-com
          # skpCache: true
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
|     | skipCache (opcional, o padrão é falso) | Sinalizar se o armazenamento em cache deve ser usado para solicitações correspondentes a esta regra. Por padrão, as respostas serão armazenadas em cache de acordo com o cabeçalho de cache de resposta (por exemplo, Cache-Control ou Expires) |

**Origens**

As conexões com as origens são somente SSL e usam a porta 443.

| Propriedade | Significado |
|------------------|--------------------------------------|
| **nome** | Nome que pode ser referenciado por &quot;action.originName&quot;. |
| **domínio** | Nome do domínio usado para conectar ao back-end personalizado. Ele também é usado para SNI e validação SSL. |
| **ip** (opcional, com suporte para iv4 e ipv6) | Se fornecido, ele será usado para se conectar ao back-end em vez de ao &quot;domínio&quot;. O &quot;domínio&quot; ainda é usado para SNI e validação SSL. |
| **forwardHost** (opcional, o padrão é falso) | Se definido como true, o cabeçalho &quot;Host&quot; da solicitação do cliente será passado para o back-end; caso contrário, o valor &quot;domínio&quot; será passado no cabeçalho &quot;Host&quot;. |
| **forwardCookie** (opcional, o padrão é falso) | Se definido como verdadeiro, o cabeçalho &quot;Cookie&quot; da solicitação do cliente será passado para o back-end; caso contrário, o cabeçalho Cookie será removido. |
| **forwardAuthorization** (opcional, o padrão é falso) | Se definido como verdadeiro, o cabeçalho &quot;Autorização&quot; da solicitação do cliente será passado para o backend; caso contrário, o cabeçalho de Autorização será removido. |
| **tempo limite** (opcional, em segundos, o padrão é 60) | Número de segundos que o CDN deve aguardar até que um servidor de back-end forneça o primeiro byte de um corpo de resposta HTTP. Esse valor também é usado como um tempo limite entre bytes para o servidor de back-end. |

### Utilização de proxy para o Edge Delivery Services {#proxying-to-edge-delivery}

Há cenários em que os seletores de origem devem ser usados para direcionar o tráfego pelo AEM Publish para o AEM Edge Delivery Services:

* Parte do conteúdo é entregue por um domínio gerenciado pelo AEM Publish, enquanto outros conteúdos do mesmo domínio são entregues por Edge Delivery Services
* O conteúdo entregue pelos Edge Delivery Services se beneficiaria das regras implantadas por meio do Pipeline de configuração, incluindo regras de filtro de tráfego ou transformações de solicitação/resposta

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
              matches: "^^(/scripts/.*|/styles/.*|/fonts/.*|/blocks/.*|/icons/.*|.*/media_.*|/favicon.ico)"
        action:
          type: selectOrigin
          originName: aem-live
    origins:
      - name: aem-live
        domain: main--repo--owner.aem.live
```

>[!NOTE]
> Como o CDN Gerenciado por Adobe é usado, certifique-se de configurar a invalidação por push no modo **gerenciado**, seguindo a [documentação de invalidação por push da Instalação](https://www.aem.live/docs/byo-dns#setup-push-invalidation) dos Edge Delivery Services.


## Redirecionamentos do lado do cliente {#client-side-redirectors}

>[!NOTE]
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada, envie um email para `aemcs-cdn-config-adopter@adobe.com` e descreva seu caso de uso.

Você pode usar as regras de redirecionamento do lado do cliente para 301, 302 e redirecionamentos semelhantes do lado do cliente. Se uma regra for correspondente, o CDN responderá com uma linha de status que inclui o código de status e a mensagem (por exemplo, HTTP/1.1 301 Movido Permanentemente), bem como o conjunto de cabeçalhos do local.

São permitidas localizações absolutas e relativas com valores fixos.

Observe que o tamanho cumulativo do arquivo de configuração, incluindo as regras de filtro de tráfego, não pode exceder 100 KB.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_redirects:
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
| **redirecionar** | localização | Valor para o cabeçalho &quot;Local&quot;. |
|     | Status (opcional, o padrão é 301) | Status HTTP a ser usado na mensagem de redirecionamento, 301 por padrão, os valores permitidos são: 301, 302, 303, 307, 308. |
