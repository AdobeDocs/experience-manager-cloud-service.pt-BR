---
title: Configurar regras de filtro de tráfego (com regras do WAF)
description: Usar regras de filtro de tráfego (com regras WAF) para filtrar o tráfego
source-git-commit: b1b184b63ab6cdeb8a4e0019c31a34db59438a3d
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 2%

---


# Configuração de regras de filtro de tráfego (com regras do WAF) para filtrar o tráfego {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada em andamento, envie um email para **aemcs-waf-adopter@adobe.com**, incluindo o nome da organização e o contexto sobre o interesse no recurso.

O Adobe tenta mitigar os ataques contra sites do cliente, mas pode ser útil filtrar proativamente o tráfego que corresponde a determinados padrões, de modo que o tráfego mal-intencionado não chegue ao seu aplicativo. As possíveis abordagens incluem:

* Módulos de camada do Apache, como `mod_security`
* Configuração das regras de filtro de tráfego implantadas na CDN por meio do pipeline de configuração do Cloud Manager

Este artigo descreve a abordagem das regras de filtro de tráfego. A maioria dessas regras bloqueia ou permite solicitações com base nas propriedades da solicitação e nos cabeçalhos da solicitação, incluindo IP, caminhos e agente do usuário. Essas regras podem ser configuradas por todos os clientes do AEM as a Cloud Service Sites e do Forms.

Os clientes que licenciam o complemento WAF (Web Application Firewall) também podem configurar uma categoria adicional de regras chamada &quot;WAF traffic filter rules&quot; (ou regras WAF de filtro de tráfego). Essas regras do WAF bloqueiam solicitações que correspondem a vários padrões associados ao tráfego mal-intencionado. Entre em contato com a equipe de conta do Adobe para obter detalhes sobre como licenciar esse recurso futuro. Observe que nenhuma licença adicional é necessária durante o programa de adoção antecipada.

As regras de filtro de tráfego podem ser implantadas em todos os tipos de ambiente de nuvem (RDE, desenvolvimento, preparo, produção) em programas de produção (que não sejam de sandbox).

## Configurar {#setup}

1. Primeiro, crie a seguinte pasta e estrutura de arquivo para a pasta de nível superior no Git:

   ```
   config/
        cdn/
           cdn.yaml
   ```

1. `cdn.yaml` deve conter metadados, bem como uma lista de regras de filtros de tráfego e regras do WAF.

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     trafficFilters:
       rules:
         ...
   ```

O parâmetro &quot;kind&quot; deve ser definido como &quot;CDN&quot; e a versão deve ser definida como a versão do schema, que atualmente é &quot;1&quot;. Veja mais exemplos abaixo.


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. Para configurar as regras do WAF, o WAF deve estar ativado no Cloud Manager, conforme descrito abaixo, para os cenários de programa novos e existentes. Observe que uma licença separada deve ser adquirida para o WAF.

   1. Para configurar o WAF em um novo programa, marque a opção **Proteção WAF-DDOS** caixa de seleção na **Segurança** conforme mostrado abaixo. Continue seguindo as etapas descritas em [Adicionar programa de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) para criar seu programa

   1. Para configurar o WAF em um programa existente, selecione o **Editar programa** seguindo as etapas descritas na seção [Programas de edição](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) documentação. Em seguida, no **Segurança** do assistente, você poderá desmarcar ou marcar a opção WAF-DDOS a qualquer momento

1. Para tipos de ambiente diferentes do RDE, execute o pipeline de configuração do Cloud Manager, que pode ser configurado conforme descrito abaixo.

   1. No cartão de pipeline na página inicial do Cloud Manager, selecione **Adicionar pipeline de produção** ou **Adicionar pipeline de não produção** para iniciar o assistente de adição de pipeline
   1. Selecionar **Pipeline de implantação** na guia configuração

      ![Selecione a opção Pipeline de implantação](/help/security/assets/deployment.png)

   1. Dê um nome ao pipeline, selecione acionadores de implantação e selecione **Continuar**
   1. No **Código-fonte** selecione **Implantação direcionada** e selecione **Configuração**

      ![Selecionar implantação direcionada](/help/security/assets/target-deployment.png)

   1. Selecione o repositório e a ramificação conforme necessário. Se existir um pipeline de configuração para o ambiente selecionado, essa seleção será desativada.

      ![Visão geral de um pipeline de configuração](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      > Os usuários devem estar conectados como Gerente de implantação para configurar ou executar esses pipelines.
      > Além disso, você pode configurar e executar apenas um pipeline de configuração por ambiente.

   1. Selecione **Salvar**. Seu novo pipeline aparecerá no cartão de pipeline e poderá ser executado quando estiver pronto.
   1. Para RDEs, a linha de comando será usada, mas RDE não é compatível no momento.

## Sintaxe das regras de filtro de tráfego {#rules-syntax}

Você pode configurar `traffic filter rules` para corresponder a padrões como IPs, agente de usuário, cabeçalhos de solicitação, nome do host, localização geográfica e url.

Os clientes que licenciam a oferta do WAF também podem configurar uma categoria especial de regras de filtro de tráfego chamada `WAF traffic filter rules` (ou regras WAF para abreviar) que fazem referência a um ou mais sinalizadores WAF, que estão listados em sua própria seção abaixo.

Este é um exemplo de um conjunto de regras de filtro de tráfego, que também inclui uma regra do WAF.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

O formato das regras de filtro de tráfego no arquivo cdn.yaml é descrito abaixo. Veja alguns exemplos em uma seção posterior.


| **Propriedade** | **Maioria das regras de filtro de tráfego** | **Regras de filtro de tráfego do WAF** | **Tipo** | **Valor padrão** | **Descrição** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Nome da regra (64 caracteres de comprimento, pode conter apenas alfanuméricos e - ) |
| quando | X | X | `Condition` | - | A estrutura básica é:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>Consulte Sintaxe de estrutura de condição abaixo, que descreve os getters, predicados e como combinar várias condições. |
| ação | X | X | `Action` | log | log, permitir, bloquear, log ou objeto de ação O padrão é log |
| rateLimit | X |   | `RateLimit` | não definido | Configuração de limitação de taxa. A limitação de taxa está desabilitada se não estiver definida.<br><br>Há uma seção separada mais abaixo que descreve a sintaxe rateLimit, juntamente com exemplos. |

### Estrutura de condição {#condition-structure}

Uma Condição pode ser uma Condição simples ou um grupo de Condições.

**Condição simples**

Uma Condição simples é composta por um getter e um predicado.

```
{ <getter>: <value>, <predicate>: <value> }
```

**Agrupar condições**

Um Grupo de condições é composto por várias Condições simples e/ou de grupo.

```
<allOf|anyOf>:
  - { <getter>: <value>, <predicate>: <value> }
  - { <getter>: <value>, <predicate>: <value> }
  - <allOf|anyOf>:
    - { <getter>: <value>, <predicate>: <value> }
```

| **Propriedade** | **Tipo** | **Significado** |
|---|---|---|
| **allOf** | `array[Condition]` | **e** operação. true se todas as condições listadas retornarem true |
| **anyOf** | `array[Condition]` | **ou** operação. true se qualquer uma das condições listadas retornar true |

**Getter**

| **Propriedade** | **Tipo** | **Descrição** |
|---|---|---|
| reqProperty | `string` | Propriedade de solicitação.<br><br>Um de: `path` , `queryString`, `method`, `tier`, `domain`, `clientIp`, `clientCountry`<br><br>A propriedade do domínio é uma transformação em minúsculas do cabeçalho do host da solicitação. É útil para comparações de cadeias de caracteres, para que as correspondências não sejam perdidas devido à diferenciação entre maiúsculas e minúsculas.<br><br>A variável `clientCountry` usa códigos de duas letras exibidos em [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) |
| reqHeader | `string` | Retorna o cabeçalho da solicitação com o nome especificado |
| queryParam | `string` | Retorna o parâmetro de consulta com o nome especificado |
| cookie | `string` | Retorna o cookie com o nome especificado |

**Predicado**

| **Propriedade** | **Tipo** | **Significado** |
|---|---|---|
| **igual** | `string` | true se o resultado de getter for igual ao valor fornecido |
| **doesNotEqual** | `string` | true se o resultado de getter não for igual ao valor fornecido |
| **gostar** | `string` | true se o resultado de getter corresponder ao padrão fornecido |
| **notLike** | `string` | true se o resultado de getter não corresponder ao padrão fornecido |
| **matches** | `string` | true se o resultado de getter corresponder ao regex fornecido |
| **doesNotMatch** | `string` | true se o resultado de getter não corresponder ao regex fornecido |
| **em** | `array[string]` | true se a lista fornecida contiver o resultado getter |
| **notIn** | `array[string]` | true se a lista fornecida não contiver o resultado getter |

### Estrutura de ação {#action-structure}

Especificado por `action` que pode ser uma string especificando o tipo de ação (permitir, bloquear, log) e assumindo valores padrão para todas as outras opções ou um objeto no qual o tipo de regra é definido por meio de `type` campo obrigatório junto com outras opções aplicáveis a esse tipo.

**Tipos de ação**

As ações são priorizadas de acordo com seus tipos na tabela a seguir, que é ordenada para refletir a ordem em que as ações são executadas:

| **Nome** | **Propriedades permitidas** | **Significado** |
|---|---|---|
| **permitir** | `wafFlags` (opcional) | se wafFlags não estiver presente, o interromperá o processamento de regras e continuará a fornecer a resposta. Se wafFlags estiver presente, ele desativará as proteções WAF especificadas e continuará o processamento de regras. |
| **bloco** | `status, wafFlags` (opcional e mutuamente exclusivo) | se wafFlags não estiver presente, retorna o erro HTTP ignorando todas as outras propriedades, o código de erro é definido pela propriedade de status ou o padrão é 406. Se wafFlags estiver presente, ele ativa as proteções WAF especificadas e continua para o processamento de regras. |
| **log** | `wafFlags` (opcional) | registra o fato de que a regra foi acionada, caso contrário, não afeta o processamento. wafFlags não tem efeito |

### Lista de Sinalizadores do WAF {#waf-flags-list}

A variável `wafFlag` propriedade pode incluir o seguinte:

| **ID do sinalizador** | **Nome do sinalizador** | **Descrição** |
|---|---|---|
| SQLI | Injeção de SQL | A Injeção de SQL é a tentativa de obter acesso a um aplicativo ou obter informações privilegiadas executando consultas arbitrárias ao banco de dados. |
| BACKDOOR | Backdoor | Um sinal backdoor é uma solicitação que tenta determinar se um arquivo backdoor comum está presente no sistema. |
| CMDEXE | Execução de comando | Execução de Comando é a tentativa de obter controle ou danificar um sistema alvo através de comandos arbitrários do sistema por meio da entrada do usuário. |
| XSS | Criação de script entre sites | Cross-Site Scripting é a tentativa de sequestrar a conta de um usuário ou a sessão de navegação na Web por meio de um código JavaScript mal-intencionado. |
| PASSAGEM | Diretório de passagem | O Diretory Traversal é a tentativa de navegar pelas pastas privilegiadas em todo o sistema, na esperança de obter informações confidenciais. |
| USERAGENT | Ferramentas de ataque | Ferramentas de ataque é o uso de software automatizado para identificar vulnerabilidades de segurança ou para tentar explorar uma vulnerabilidade detectada. |
| LOG4J-JNDI | Log4J JNDI | Os ataques ao Log4J JNDI tentam explorar a [Vulnerabilidade do Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente nas versões do Log4J anteriores à 2.16.0 |
| AWS SSRF | AWS-SSRF | Server Side Request Forgery (SSRF) é uma solicitação que tenta enviar solicitações feitas pelo aplicativo web para sistemas internos de destino. Os ataques de AWS SSRF usam SSRF para obter chaves do Amazon Web Services (AWS) e obter acesso a buckets do S3 e seus dados. |
| BHH | Cabeçalhos de salto inválidos | Os cabeçalhos de salto inválido indicam uma tentativa de contrabando de HTTP por meio de um cabeçalho TE (Transferir Codificação) ou CL (Conteúdo Comprimento) malformado, ou um cabeçalho TE e CL bem formado |
| ANORMALPATH | Caminho anormal | Caminho anormal indica que o caminho original difere do caminho normalizado (por exemplo, `/foo/./bar` é normalizado para `/foo/bar`) |
| COMPACTADO | Compactação detectada | O corpo da solicitação POST está compactado e não pode ser inspecionado. Por exemplo, se um cabeçalho de solicitação &quot;Content-Encoding: gzip&quot; for especificado e o corpo da POST não for texto simples. |
| CODIFICAÇÃODUPLA | Codificação dupla | A Codificação dupla verifica a técnica de evasão de caracteres html de codificação dupla |
| FORÇAR NAVEGAÇÃO | Navegação forçada | A navegação forçada é a tentativa mal sucedida de acessar as páginas de administração |
| NOTUTF8 | Codificação inválida | Codificação inválida pode fazer com que o servidor traduza caracteres mal-intencionados de uma solicitação em uma resposta, causando uma negação de serviço ou XSS |
| ERRO JSON | Erro de codificação JSON | Um corpo de solicitação POST, PUT ou PATCH especificado como contendo JSON no cabeçalho de solicitação &quot;Content-Type&quot;, mas que contém erros de análise JSON. Isso geralmente está relacionado a um erro de programação ou a uma solicitação automatizada ou mal-intencionada. |
| DADOS MALFORMADOS | Dados malformados no corpo da solicitação | Um corpo de solicitação POST, PUT ou PATCH que está malformado de acordo com o cabeçalho de solicitação &quot;Content-Type&quot;. Por exemplo, se um cabeçalho de solicitação &quot;Content-Type: application/x-www-form-urlencoded&quot; for especificado e contiver um corpo de POST que seja json. Isso geralmente é um erro de programação, uma solicitação automatizada ou mal-intencionada. Exige o agente 3.2 ou superior. |
| SANS | Tráfego IP mal-intencionado | [SANS Internet Storm Center](https://isc.sans.edu/) lista de endereços IP relatados como envolvidos em atividades mal-intencionadas |
| SIGSCI-IP | Efeito de rede | IP sinalizado por SignalSciences: sempre que um IP é sinalizado devido a um sinal mal-intencionado pelo mecanismo de decisão, esse IP é propagado para todos os clientes. As solicitações subsequentes desses endereços IP que contêm qualquer sinal adicional durante o sinalizador são registradas |
| NO-CONTENT-TYPE | Cabeçalho da solicitação &quot;Content-Type&quot; ausente | Uma solicitação POST, PUT ou PATCH que não tem um cabeçalho de solicitação &quot;Content-Type&quot;. Por padrão, os servidores de aplicativos devem assumir &quot;Content-Type: text/plain; charset=us-ascii&quot; neste caso. Muitas solicitações automatizadas e mal-intencionadas podem estar sem &quot;Tipo de conteúdo&quot;. |
| NOUA | Nenhum agente de usuário | Muitas solicitações automatizadas e mal-intencionadas usam User-Agents falsos ou ausentes para dificultar a identificação do tipo de dispositivo que faz as solicitações. |
| TORNODE | Tráfego Tor | Tor é um software que oculta a identidade de um usuário. Um pico no tráfego Tor pode indicar um invasor tentando mascarar sua localização. |
| DATA CENTER | Tráfego de data center | Tráfego de data center é o tráfego não orgânico originado de provedores de hospedagem identificados. Esse tipo de tráfego geralmente não é associado a um usuário final real. |
| NULLBYTE | Byte nulo | Bytes nulos normalmente não aparecem em uma solicitação e indicam que a solicitação está malformada e é potencialmente maliciosa. |
| IMPOSTOR | SearchBot Impostor | O impostor de bot de pesquisa é alguém que finge ser um bot de pesquisa do Google ou do Bing, mas que não é legítimo. Observe que não depende de uma resposta sozinha, mas deve ser resolvida na nuvem primeiro, portanto, não deve ser usada em uma regra prévia. |
| ARQUIVOPRIVADO | Arquivos privados | Os arquivos privados geralmente têm natureza confidencial, como um Apache `.htaccess` ou um arquivo de configuração que poderia vazar informações confidenciais |
| SCANNER | Scanner | Identifica ferramentas e serviços de digitalização populares |
| RESPONSESPLIT | Divisão de resposta HTTP | Identifica quando os caracteres CRLF são enviados como entrada para o aplicativo para inserir cabeçalhos na resposta HTTP |
| XML-ERROR | Erro de codificação de XML | Um corpo de solicitação POST, PUT ou PATCH especificado como contendo XML dentro do cabeçalho de solicitação &quot;Content-Type&quot;, mas que contém erros de análise XML. Isso geralmente está relacionado a um erro de programação ou a uma solicitação automatizada ou mal-intencionada. |

## Considerações {#considerations}

* Quando duas regras conflitantes são criadas, as regras de permissão sempre têm prioridade sobre as regras de bloqueio. Por exemplo, se você criar uma regra para bloquear um caminho específico e uma regra para permitir um endereço IP específico, as solicitações desse endereço IP no caminho bloqueado serão permitidas.

* Se uma regra for correspondente e bloqueada, a CDN responderá com uma `406` código de retorno.

* Os arquivos de configuração não devem conter segredos, pois eles podem ser lidos por qualquer pessoa com acesso ao repositório Git.

## Exemplos de regras {#examples}

Alguns exemplos de regras se seguem. Consulte a [seção limite de taxa](#rules-with-rate-limits) mais abaixo para exemplos de limitação de taxa.

**Exemplo 1**

Esta regra bloqueia solicitações provenientes do IP 192.168.1.1:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**Exemplo 2**

Essa regra bloqueia solicitações no caminho `/helloworld` ao publicar com um usuário-agente que contenha o Chrome:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
           allOf:
            - { reqProperty: path, equals: /helloworld }
            - { reqProperty: tier, equals: publish }
            - { reqHeader: user-agent, matches: '.*Chrome.*'  }
           action:
             type: block
```

**Exemplo 3**

Essa regra bloqueia solicitações que contêm o parâmetro de consulta `foo`, mas permite todas as solicitações provenientes do IP 192.168.1.1:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when: { queryParam: url-param, equals: foo }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**Exemplo 4**

Essa regra bloqueia solicitações para o caminho /block-me e bloqueia todas as solicitações que correspondam a um padrão SQLI ou XSS:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**Exemplo 4**

Essa regra bloqueia o acesso a países OFAC:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: block-ofac-countries
        when:
          allOf:
            - { reqProperty: tier, equals: publish }
            - reqProperty: clientCountry
              in:
                - SY
                - BY
                - MM
                - KP
                - IQ
                - CD
                - SD
                - IR
                - LR
                - ZW
                - CU
                - CI
        action: block
```

## Regras com Limites de Taxa {#rules-with-rate-limits}

Às vezes, é desejável bloquear o tráfego correspondente a uma regra somente se a correspondência exceder uma determinada taxa ao longo do tempo. Definir um valor para o `rateLimit` A propriedade limita a taxa dessas solicitações que correspondem à condição da regra.

### Estrutura rateLimit {#ratelimit-structure}

| **Propriedade** | **Tipo** | **Padrão** | **SIGNIFICADO** |
|---|---|---|---|
| limite | número inteiro de 10 a 10000 | obrigatório | Taxa de solicitações em solicitações por segundo para as quais a regra é acionada. |
| janela | enumeração de inteiros: 1, 10 ou 60 | 10 | Janela de amostragem em segundos para a qual a taxa de solicitação é calculada. |
| penalidade | número inteiro de 60 a 3600 | 300 (5 minutos) | Um período em segundos para o qual as solicitações correspondentes são bloqueadas (arredondado para o minuto mais próximo). |
| groupBy | matriz[Getter] | nenhuma | o contador do limitador de taxa será agregado por um conjunto de propriedades de solicitação (por exemplo, clientIp). |

### Exemplos {#ratelimiting-examples}

**Exemplo 1**

Essa regra bloqueia um cliente para 5m quando ele excede 100 req/s nos últimos 60 segundos:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Exemplo 2**

Bloquear solicitações para 60s no caminho /crítico/recurso quando ele exceder 100 req/s nos últimos 60 segundos:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when: { reqProperty: path, equals: /critical/resource }
        action:
          type: block
        rateLimit: { limit: 100, window: 60, penalty: 60 }
```

## Logs CDN {#cdn-logs}

O AEM as a Cloud Service fornece acesso a logs de CDN, que são úteis para casos de uso, incluindo otimização da taxa de ocorrência do cache e configuração de regras de CDN e WAF. Os logs do CDN aparecem no Cloud Manager **Baixar logs** , ao selecionar o serviço Autor ou Publicar.

A propriedade &quot;rules&quot; descreve quais regras de filtro de tráfego são correspondidas e tem o seguinte padrão:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Por exemplo:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

As regras se comportam da seguinte maneira:

* o nome de regra declarado pelo cliente de qualquer regra correspondente será listado no atributo matches.
* o atributo action detalha se as regras tiveram o efeito de bloquear, permitir ou registrar.
* se o WAF estiver licenciado e ativado, o atributo waf listará quaisquer regras waf (por exemplo, SQLI; observe que isso é independente do nome declarado pelo cliente) que foram detectadas, independentemente das regras waf terem sido listadas na configuração.
* se nenhuma regra declarada pelo cliente for correspondente e nenhuma regra waf for correspondente, a propriedade de atributo de regras ficará em branco.

Em geral, as regras correspondentes aparecem na entrada de log para todas as solicitações para o CDN, independentemente de ser uma ocorrência, transmissão ou erro do CDN. No entanto, as regras do WAF aparecem na entrada do log somente para solicitações ao CDN que são consideradas perdidas ou transmitidas pelo CDN, mas não para ocorrências de CDN.

O exemplo abaixo mostra um cdn.yaml de amostra e duas entradas de log CDN:


```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS ]
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/block-me",
"method": "GET",
"res_ctype": "",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=path-rule,action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

### Formato do Log {#cdn-log-format}

Veja abaixo uma lista dos nomes de campo usados em logs CDN, juntamente com uma breve descrição.

| **Nome do campo** | **Descrição** |
|---|---|
| *carimbo de data e hora* | A hora em que a solicitação foi iniciada, após o término do TLS. |
| *ttfb* | Abreviação de *Tempo até o Primeiro Byte*. O intervalo de tempo entre a solicitação iniciada até o ponto antes do corpo da resposta começar a ser transmitido. |
| *cli_ip* | O endereço IP do cliente. |
| *cli_country* | Duas letras [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) código alfa-2 do país do cliente. |
| *rid* | O valor do cabeçalho da solicitação usado para identificar exclusivamente a solicitação. |
| *req_ua* | O agente do usuário responsável por fazer uma determinada solicitação HTTP. |
| *host* | A autoridade à qual a solicitação se destina. |
| *url* | O caminho completo, incluindo parâmetros de consulta. |
| *método* | Método HTTP enviado pelo cliente, como &quot;GET&quot; ou &quot;POST&quot;. |
| *res_ctype* | O Content-Type usado para indicar o tipo de mídia original do recurso. |
| *cache* | Estado do cache. Os valores possíveis são HIT, MISS ou PASS |
| *status* | O código do status HTTP como um valor inteiro. |
| *res_age* | A quantidade de tempo (em segundos) que uma resposta foi armazenada em cache (em todos os nós). |
| *pop* | Centro de dados do servidor de cache CDN. |
| *regras* | O nome de todas as regras correspondentes.<br><br>Também indica se a correspondência resultou em um bloco. <br><br>Por exemplo, &quot;`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`&quot;<br><br>Vazio se nenhuma regra for correspondente. |
