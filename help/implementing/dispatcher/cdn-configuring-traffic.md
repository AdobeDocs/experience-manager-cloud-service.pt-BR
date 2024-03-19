---
title: Configuração do tráfego no CDN
description: Saiba como configurar o tráfego de CDN declarando regras e filtros em um arquivo de configuração e implantando-os no CDN usando o Pipeline de configuração do Cloud Manager.
feature: Dispatcher
source-git-commit: 0a0c9aa68b192e8e2a612f50a58ba5f9057c862d
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 2%

---


# Configuração do tráfego no CDN {#cdn-configuring-cloud}

>[!NOTE]
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada, envie um email para `aemcs-cdn-config-adopter@adobe.com` e descreva seu caso de uso.

O AEM as a Cloud Service oferece uma coleção de recursos configuráveis no [CDN gerenciada por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) camada que modifica a natureza das solicitações recebidas ou respostas enviadas. As seguintes regras, descritas em detalhes nesta página, podem ser declaradas para alcançar o seguinte comportamento:

* [Solicitar transformações](#request-transformations) - modificar aspectos de solicitações recebidas, incluindo cabeçalhos, caminhos e parâmetros.
* [Transformações de resposta](#response-transformations) - modificar cabeçalhos que estão no caminho de volta para o cliente (por exemplo, um navegador da web).
* [Redirecionadores do lado do cliente](#client-side-redirectors) - acionar um redirecionamento de navegador.
* [Seletores de origem](#origin-selectors) - proxy para um back-end de origem diferente.

Também podem ser configuradas na CDN as Regras de filtro de tráfego (incluindo o WAF), que controlam qual tráfego é permitido ou negado pela CDN. Esse recurso já foi lançado e você pode saber mais sobre ele no [Regras de filtro de tráfego incluindo regras WAF](/help/security/traffic-filter-rules-including-waf.md) página.

Além disso, se a CDN não puder entrar em contato com sua origem, você poderá escrever uma regra que faça referência a uma página de erro personalizada auto-hospedada (que é renderizada). Saiba mais sobre isso lendo o [Configuração de páginas de erro do CDN](/help/implementing/dispatcher/cdn-error-pages.md) artigo.

Todas essas regras, declaradas em um arquivo de configuração no controle do código-fonte, são implantadas usando [Pipeline de configuração do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Esteja ciente de que o tamanho cumulativo do arquivo de configuração não pode exceder 100KB.

## Ordem de avaliação {#order-of-evaluation}

Funcionalmente, os vários recursos mencionados anteriormente são avaliados na seguinte sequência:

![imagem](/help/implementing/dispatcher/assets/order.png)

## Configurar {#initial-setup}

Antes de configurar o tráfego na CDN, é necessário fazer o seguinte:

* Primeiro, crie esta pasta e a estrutura de arquivo na pasta de nível superior do seu projeto Git:

```
config/
     cdn.yaml
```

* Em segundo lugar, a `cdn.yaml` o arquivo de configuração deve conter metadados e as regras descritas nos exemplos abaixo.

## Solicitar transformações {#request-transformations}

As regras de transformação de solicitação permitem modificar solicitações recebidas. As regras oferecem suporte para a configuração, remoção e alteração de caminhos, parâmetros de consulta e cabeçalhos (incluindo cookies) com base em várias condições correspondentes, incluindo expressões regulares. Também é possível definir variáveis, que podem ser referenciadas posteriormente na sequência de avaliação.

Os casos de uso são variados e incluem regravações de URL para simplificação de aplicativos ou mapeamento de URLs herdados.

Como mencionado anteriormente, há um limite de tamanho para o arquivo de configuração, de modo que as organizações com requisitos maiores devem definir regras no `apache/dispatcher` camada.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:  
  experimental_requestTransformations:
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
 
      - name: set-query-param-rule
        when:
          reqProperty: path
          equals: /set-query-param
        actions:
          - type: set
            queryParam: someParam
            value: someValue
 
      - name: unset-query-param-rule
        when:
          reqProperty: path
          equals: /unset-query-param
        actions:
          - type: unset
            queryParam: someParam
 
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
 
      - name: set-req-cookie-rule
        when:
          reqProperty: path
          equals: /set-req-cookie
        actions:
          - type: set
            reqCookie: someParam
            value: someValue
 
      - name: unset-req-cookie-rule
        when:
          reqProperty: path
          equals: /unset-req-cookie
        actions:
          - type: unset
            reqCookie: someParam
 
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some value
 
      - name: unset-variable-rule
        when:
          reqProperty: path
          equals: /unset-variable
        actions:
          - type: unset
            var: some_var_name
 
      - name: replace-segment
        when:
          reqProperty: path
          like: /replace-segment/*
        actions:
          - type: replace
            reqProperty: path
            match: /replace-segment/
            value: /segment-was-replaced/
 
      - name: replace-extension
        when:
          reqProperty: path
          like: /replace-extension/*.html
        actions:
          - type: replace
            reqProperty: path
            match: \.html
            value: ''
 
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
```

**Ações**

As ações disponíveis são explicadas na tabela abaixo.

| Nome | Propriedades | Significado |
|-----------|--------------------------|-------------|
| **set** | reqHeader, valor | Define um cabeçalho especificado para um determinado valor. |
|     | queryParam, valor | Define um parâmetro de consulta especificado para um determinado valor. |
|     | reqCookie, valor | Define um cookie especificado para um determinado valor. |
|     | var, value | Define uma variável especificada para um determinado valor. |
| **unset** | reqHeader | Remove um cabeçalho especificado. |
|         | queryParam | Remove um parâmetro de consulta especificado. |
|         | reqCookie | Remove um cookie especificado. |
|         | var | Remove uma variável especificada. |
|         | queryParamMatch | Remove todos os parâmetros de consulta que correspondem a uma expressão regular especificada. |
| **replace** | reqProperty, correspondência, valor | Substitui parte da propriedade de solicitação por um novo valor. Atualmente, somente a propriedade &quot;path&quot; é compatível. |

### Variáveis {#variables}

É possível definir variáveis durante a transformação da solicitação e, em seguida, referenciá-las posteriormente na sequência de avaliação. Consulte a [ordem de avaliação](#order-of-evaluation) para obter mais detalhes.

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:   
  experimental_requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value
 
  experimental_responseTransformations:
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
  experimental_responseTransformations:
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
| **set** | reqHeader, valor | Define um cabeçalho especificado para um determinado valor na resposta. |
| **unset** | respHeader | Remove um cabeçalho especificado da resposta. |

## Seletores de origem {#origin-selectors}

Você pode aproveitar a CDN do AEM para rotear o tráfego para diferentes back-ends, incluindo aplicativos que não sejam Adobe (talvez por caminho ou subdomínio).

Exemplo de configuração:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy-me* }
        action:
          type: selectOrigin
          originName: example-com
          # useCache: false
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
|     | useCache (opcional, o padrão é verdadeiro) | Sinalizar se o armazenamento em cache deve ser usado para solicitações correspondentes a esta regra. |

**Origens**

As conexões com as origens são somente SSL e usam a porta 443.

| Propriedade | Significado |
|------------------|--------------------------------------|
| **name** | Nome que pode ser referenciado por &quot;action.originName&quot;. |
| **domínio** | Nome do domínio usado para conectar ao back-end personalizado. Ele também é usado para SNI e validação SSL. |
| **ip** (opcional, compatível com iv4 e ipv6) | Se fornecido, ele será usado para se conectar ao back-end em vez de ao &quot;domínio&quot;. O &quot;domínio&quot; ainda é usado para SNI e validação SSL. |
| **forwardHost** (opcional, o padrão é falso) | Se definido como true, o cabeçalho &quot;Host&quot; da solicitação do cliente será passado para o back-end; caso contrário, o valor &quot;domínio&quot; será passado no cabeçalho &quot;Host&quot;. |
| **forwardCookie** (opcional, o padrão é falso) | Se definido como verdadeiro, o cabeçalho &quot;Cookie&quot; da solicitação do cliente será passado para o back-end; caso contrário, o cabeçalho Cookie será removido. |
| **forwardAuthorization** (opcional, o padrão é falso) | Se definido como verdadeiro, o cabeçalho &quot;Autorização&quot; da solicitação do cliente será passado para o backend; caso contrário, o cabeçalho de Autorização será removido. |
| **timeout** (opcional, em segundos, o padrão é 60) | Número de segundos que o CDN deve aguardar até que um servidor de back-end forneça o primeiro byte de um corpo de resposta HTTP. Esse valor também é usado como um tempo limite entre bytes para o servidor de back-end. |

## Redirecionadores do lado do cliente {#client-side-redirectors}

Você pode usar as regras de redirecionamento do lado do cliente para 301, 302 e redirecionamentos semelhantes do lado do cliente. Se uma regra for correspondente, o CDN responderá com uma linha de status que inclui o código de status e a mensagem (por exemplo, HTTP/1.1 301 Movido Permanentemente), bem como o conjunto de cabeçalhos do local.

São permitidas localizações absolutas e relativas com valores fixos.

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
