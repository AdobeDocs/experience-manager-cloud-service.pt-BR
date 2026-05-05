---
title: Trechos de configuração da CDN para cenários comuns
description: Padrões YAML prontos para cópia para as configurações de CDN gerenciado pela Adobe e CDN gerenciado pelo cliente, incluindo autenticação de borda, redirecionamentos, variação de cache, modelagem de tráfego e limites de taxa.
feature: Dispatcher
role: Admin
source-git-commit: ab43facbd4c34c92878e303acf2fef9cc127e28a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# Trechos de configuração da CDN para cenários comuns {#cdn-configuration-snippets}

Este artigo coleta padrões práticos de `cdn.yaml` para o AEM as a Cloud Service. Use-as junto com a documentação de recursos para [regras de tráfego da CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), [credenciais da CDN gerenciadas pelo cliente](/help/implementing/dispatcher/cdn-credentials-authentication.md) e [regras de filtro de tráfego, incluindo a WAF](/help/security/traffic-filter-rules-including-waf.md). Implante trechos com um [pipeline de configuração](/help/operations/config-pipeline.md) do Cloud Manager.

>[!NOTE]
>
>Substitua nomes de host, caminhos, intervalos de IP, chaves e limites por valores que correspondam ao seu programa. Teste as alterações em um ambiente de não produção antes de promovê-las.

## CDN gerenciada pelo cliente {#customer-managed-cdn}

### Configuração da autenticação de chave do Edge somente para alguns domínios {#edge-auth-selected-hosts}

Problema: Em uma [CDN gerenciada pelo cliente](/help/implementing/dispatcher/cdn.md#point-to-point-cdn), você deve impor a autenticação para alguns nomes de host do cliente, enquanto outros nomes de host que atingem a publicação devem permanecer disponíveis sem esse cabeçalho (por exemplo, durante a implantação ou quando apenas um domínio de marca está atrás da sua CDN).

Solução: exija a autenticação `X-AEM-Edge-Key` apenas quando o primeiro nome de host de `X-Forwarded-Host` for igual ao seu nome de host de destino (por exemplo, `example.com`). A regra usa a propriedade de solicitação `forwardedDomain` para executar essa correspondência e executa a ação `authenticate` no autenticador de borda. Substitua nomes de host, nomes de autenticador e espaços reservados de chave para o seu programa.

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: forwardedDomain, equals: "example.com" }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

### Configurando a Autenticação de Chave do Edge para Solicitações que Não Vêm de IPs VPN {#edge-auth-trusted-ips}

Problema: configurar autenticação de chave de borda para BYOCDN, mas permitir acesso direto ao domínio de publicação somente para IPs VPN

Solução: exige autenticação X-AEM-Edge-Key somente quando o IP do cliente não está na lista de IPs VPN

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: clientIp, notIn: ["10.0.0.1", "11.0.0.0/24", "<other VPN IPs>"] }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

## Redirecionamentos {#redirects}

### Redirecionando do domínio APEX para www {#apex-to-www}

```yaml
kind: "CDN"
version: "1"
data:
 redirects:
   rules:
     - name: non-www-to-www-redirect
       when:
         reqProperty: domain
         doesNotMatch: '^www\.'
       action:
         type: redirect
         status: 301
         location:
           join:
             format: 'https://www.%s%s'
             args:
               - reqProperty: domain
               - reqProperty: url
```

### Modificando a Chave do Cache {#cache-key}

A CDN não expõe um campo &quot;chave de cache&quot; separado. Como a URL participa do cache, você pode dividir entradas de cache alterando a URL, por exemplo, adicionando um parâmetro de consulta por meio de uma [transformação de solicitação](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations).

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: set-request-different-cache-curl
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqHeader: user-agent
              matches: curl
        actions:
          - type: set
            queryParam: cache
            value: 'curl'
```

### Redirecionando para um caminho normalizado {#trailing-slash}

Envie um redirecionamento permanente quando um navegador solicitar uma barra à direita na publicação, por exemplo, de `https://www.example.com/path/` para `https://www.example.com/path`.

```yaml
kind: "CDN"
version: "1"
data:
  redirects:
    rules:
      - name: remove-trailing-slash
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: www.example.com
            - reqProperty: originalPath
              matches: ^/(.+)/$
        action:
          type: redirect
          status: 301
          location:
            reqProperty: originalPath
            transform:
              - op: replace
                match: ^/(.+)/$
                replacement: https://www.example.com/\1
```

### Extração de informações de um cookie JSON {#json-cookie}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when: { reqProperty: tier, equals: publish }
        actions:
        - type: set
          reqHeader: x-mycookie-info
          value:
            reqCookie: mycookie
            transform: 
            - 'base64decode'
            - { op: 'replace', match: '"info":\s*"([^"]*)"', replacement: '\1'} 
```

## Configuração de Origem Cruzada {#cross-origin}

### Atendimento de solicitações do OPTIONS a partir da CDN {#options-from-cdn}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when:
          allOf: 
            - { reqProperty: path, like: /mypathi*  }
            - { reqProperty: method, equals: "OPTIONS" }
            - { reqHeader: Origin, equals: "https://example.com" }
        actions:
          - type: respond
            status: 200
            reason: "OK"
            headers:
              content-type: 'text/plain'
              access-control-allow-origin: { reqHeader: Origin }
              access-control-allow-methods: "*"
              access-control-allow-headers: "*"
```

## Filtros de tráfego {#traffic-filters}

### ASN de Limite de Taxa {#rate-limit-asn}

Problema: Os limites de taxa por IP podem perder um padrão de DDoS (negação de serviço distribuído): cada endereço permanece abaixo do limite, portanto, o tráfego legítimo e abusivo é semelhante na camada IP.

Solução: conte solicitações por nome de sistema autônomo (`clientAsName`) para que o limitador agregue hosts que compartilham o mesmo nome de rede. O trecho grava `clientAsName` em uma propriedade de log em cada solicitação e, em seguida, aplica um limite de taxa ao autor e à publicação agrupados por esse valor. Muitos usuários podem compartilhar um ASN (por exemplo, um grande ISP ou uma saída de VPN corporativa), portanto, o ajuste limita cuidadosamente e monitora logs de CDN para falsos positivos.

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: client_as_name
            value:
              reqProperty: clientAsName
  trafficFilters:
    rules:
    - name: limit-requests-client-as-name
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        count: all
        groupBy:
          - reqProperty: clientAsName
      action: block
```
