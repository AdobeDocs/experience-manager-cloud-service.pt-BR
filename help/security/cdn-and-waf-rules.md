---
title: Configuração de regras CDN e WAF para filtrar o tráfego
description: Usar as regras de firewall do CDN e do aplicativo da Web para filtrar o tráfego mal-intencionado
source-git-commit: 579f2842a72c7da1c9d24772bdae354a943de40c
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 2%

---


# Configuração de regras CDN e WAF para filtrar o tráfego {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada em andamento, envie um email para **aemcs-waf-adopter@adobe.com**, incluindo o nome da organização e o contexto sobre o interesse no recurso.

O Adobe tenta mitigar os ataques contra sites do cliente, mas pode ser útil filtrar proativamente as solicitações que correspondem a determinados padrões para que o tráfego mal-intencionado não chegue ao seu aplicativo. As possíveis abordagens incluem:

* Módulos de camada do Apache, como `mod_security`
* Configuração de regras que são implantadas na CDN por meio do pipeline de configuração do Cloud Manager.

Este artigo descreve a última abordagem, que oferece duas categorias de regras:

1. **Regras CDN**: bloqueia ou permite solicitações com base nas propriedades de solicitação e nos cabeçalhos de solicitação, incluindo IP, caminhos e agente do usuário. Essas regras podem ser configuradas por todos os clientes do AEM as a Cloud Service
1. **WAF** Regras do (Web Application Firewall): bloqueiam solicitações que correspondem a vários padrões conhecidos por estarem associados ao tráfego mal-intencionado. Essas regras podem ser configuradas por clientes que licenciam o complemento WAF; entre em contato com a equipe de conta do Adobe para obter detalhes. Observe que nenhuma licença adicional é necessária durante o programa de adoção antecipada.

Essas regras podem ser implantadas nos tipos de ambiente de nuvem de desenvolvimento, preparo e produção para programas de produção (não sandbox). O suporte a ambientes RDE estará disponível no futuro.

## Configurar {#setup}

1. Primeiro, crie a seguinte pasta e estrutura de arquivo para a pasta de nível superior no Git:

   ```
   config/
        cdn/
           cdn.yaml
           _config.yaml
   ```

1. `_config.yaml` A descreve alguns metadados sobre a configuração. O parâmetro &quot;kind&quot; deve ser definido como &quot;CDN&quot; e a versão deve ser definida como a versão do schema, que atualmente é &quot;1&quot;. Consulte o trecho abaixo:

   ```
   kind: "CDN"
   version: "1"
   ```

   <!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. `cdn.yaml` deve incluir uma lista de regras CDN e regras WAF, conforme descrito nas seções abaixo
1. Para corresponder às regras do WAF, o WAF deve ser ativado no Cloud Manager, conforme descrito abaixo, para os cenários de programa novos e existentes. Observe que uma licença separada deve ser adquirida para o WAF.

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
      >Você pode configurar e executar apenas um pipeline de configuração por ambiente.

   1. Selecione **Salvar**. Seu novo pipeline aparecerá no cartão de pipeline e poderá ser executado quando estiver pronto.
   1. Para RDE, a linha de comando será usada, mas RDE não é compatível no momento.

## Sintaxe de regras {#rules-syntax}

O formato das regras é descrito abaixo, seguido por alguns exemplos em uma seção subsequente.

| **Propriedade** | **Regras CDN** | **Regras do WAF** | **Tipo** | **Valor padrão** | **Descrição** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Nome da regra (64 caracteres de comprimento, pode conter apenas alfanuméricos e - ) |
| quando | X | X | `Condition` | - | A estrutura básica é:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>Consulte Sintaxe de estrutura de condição abaixo, que descreve os getters, predicados e como combinar várias condições. |
| ação | X | X | `Enum` | log (regras CDN) | Para regras CDN: permitir, bloquear, registrar. O padrão é log.<br><br>Para regras WAF: `enableWafRules`, `disableWafRules`, log. Nenhum padrão. |
| rateLimit | X |   | `RateLimit` | não definido | Configuração de limitação de taxa. A limitação de taxa está desabilitada se não estiver definida.<br><br>Há uma seção separada mais abaixo que descreve a sintaxe rateLimit, juntamente com exemplos. |
| wafRules |   | X | `array[Enum]` | - | Lista de regras do WAF que devem ser ativadas ou desativadas.<br><br>Os exemplos incluem SQLI e XSS. Consulte a lista de regras waf abaixo para obter uma lista completa. |

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

| **Propriedade** | **Tipo** | **Descrição** |
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

| **Propriedade** | **Tipo** | **Descrição** |
|---|---|---|
| **igual** | `string` | true se o resultado de getter for igual ao valor fornecido |
| **doesNotEqual** | `string` | true se o resultado de getter não for igual ao valor fornecido |
| **gostar** | `string` | true se o resultado de getter corresponder ao padrão fornecido |
| **notLike** | `string` | true se o resultado de getter não corresponder ao padrão fornecido |
| **matches** | `string` | true se o resultado de getter corresponder ao regex fornecido |
| **doesNotMatch** | `string` | true se o resultado de getter não corresponder ao regex fornecido |
| **em** | `array[string]` | true se a lista fornecida contiver o resultado getter |
| **notIn** | `array[string]` | true se a lista fornecida não contiver o resultado getter |

**Lista de regras waf**

A variável `wafRules` propriedade pode incluir as seguintes regras:

| **ID da regra** | **Nome da regra** | **Descrição** |
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

## Exemplos {#examples}

Alguns exemplos de regras se seguem. Consulte a [seção limite de taxa](#rules-with-rate-limits) mais abaixo para exemplos de limitação de taxa.

**Exemplo 1**

Esta regra bloqueia solicitações provenientes do IP 192.168.1.1:

```
data:
  rules:
    - name: "block-request-from-ip"
      when: { reqProperty: clientIp, equals: "192.168.1.1" }
      action: block
```

**Exemplo 2**

Essa regra bloqueia solicitações no caminho `/helloworld` ao publicar com um usuário-agente que contenha o Chrome:

```
data:
  rules:
    - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
      when:
        allOf:
          - { reqProperty: path, equals: /helloworld }
          - { reqProperty: tier, equals: publish }
          - { reqHeader: user-agent, matches: '.*Chrome.*'  }
      action: block
```

**Exemplo 3**

Essa regra bloqueia solicitações que contêm o parâmetro de consulta `foo`, mas permite todas as solicitações provenientes do IP 192.168.1.1:

```
data:
  rules:
    - name: "block-request-that-contains-query-parameter-foo"
      when: { queryParam: url-param, equals: foo }
      action: block
    - name: "allow-all-requests-from-ip"
      when: { reqProperty: clientIp, equals: 192.168.1.1 }
      action: allow
```

**Exemplo 4**

Essa regra bloqueia solicitações para o caminho /block-me e bloqueia todas as solicitações que correspondam a um padrão SQLI ou XSS:

```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
```

## Regras com Limites de Taxa {#rules-with-rate-limits}

Às vezes, é desejável bloquear o tráfego correspondente a uma regra somente se a correspondência exceder uma determinada taxa ao longo do tempo. Definir um valor para o `rateLimit` A propriedade limita a taxa dessas solicitações que correspondem à condição da regra.

### Estrutura rateLimit {#ratelimit-structure}

| **Propriedade** | **Tipo** | **Valor padrão** | **Descrição** |
|---|---|---|---|
| limite | número inteiro de 10 a 10000 | obrigatório | Taxa de solicitações em solicitações por segundo para as quais a regra é acionada |
| janela | enumeração de inteiros: 1, 10 ou 60 | 10 | Janela de amostragem em segundos para a qual a taxa de solicitação é calculada |
| penalidade | número inteiro de 60 a 3600 | 300 (5 minutos) | Um período em segundos para o qual as solicitações correspondentes são bloqueadas (arredondado para o minuto mais próximo) |

### Exemplos {#ratelimiting-examples}

Exemplo 1: quando a taxa de solicitação exceder 100 solicitações por segundo nos últimos 60 segundos, bloquear `/critical/resource` por 60 segundos

```
- name: rate-limit-example
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit: { limit: 100, window: 60, penalty: 60 }
```

Exemplo 2: quando a taxa de solicitação exceder 10 solicitações por segundo em 10 segundos, bloquear o recurso por 300 segundos:

```
- name: rate-limit-using-defaults
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit:
    limit: 10
```

## Logs CDN {#cdn-logs}

O AEM as a Cloud Service fornece acesso a logs de CDN, que são úteis para casos de uso, incluindo otimização da taxa de ocorrência do cache e configuração de regras de CDN e WAF. Os logs do CDN aparecem no Cloud Manager **Baixar logs** , ao selecionar o serviço Autor ou Publicar.

O nome da regra é mostrado na propriedade rules se a solicitação corresponder à regra, mesmo se a ação for &quot;permitir&quot; e, portanto, o tráfego não for bloqueado.

As regras CDN correspondentes aparecem na entrada de log para todas as solicitações para o CDN, independentemente de ser uma ocorrência, transmissão ou erro de CDN. No entanto, as regras do WAF aparecem na entrada do log somente para solicitações ao CDN que são consideradas perdidas ou transmitidas pelo CDN, mas não para ocorrências de CDN.

O exemplo abaixo mostra uma amostra `cdn.yaml` e duas entradas de log CDN, com valores não vazios na propriedade rules devido a solicitações bloqueadas que correspondem à regra CDN e à regra WAF, respectivamente.


```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cip": "147.160.230.112",
"rid": "974e67f6",
"host": "example.com",
"url": "/block-me",
"req_mthd": "GET",
"res_type": "",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=path-rule;waf=;action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cip": "147.160.230.112",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"req_mthd": "GET",
"res_type": "",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=;waf=SQLI;action=blocked"
}
```

### Formato do Log {#cdn-log-format}

Veja abaixo uma lista dos nomes de campo usados em logs CDN, juntamente com uma breve descrição.

| **Nome do campo** | **Descrição** |
|---|---|
| *carimbo de data e hora* | A hora em que a solicitação foi iniciada, após o término do TLS |
| *ttfb* | Abreviação de *Tempo até o Primeiro Byte*. O intervalo de tempo entre a solicitação iniciada até o ponto antes do corpo da resposta começar a ser transmitido. |
| *cip* | O endereço IP do cliente. |
| *rid* | O valor do cabeçalho da solicitação usado para identificar exclusivamente a solicitação. |
| *host* | A autoridade à qual a solicitação se destina. |
| *url* | O caminho completo, incluindo parâmetros de consulta. |
| *req_mthd* | Método HTTP enviado pelo cliente, como &quot;GET&quot; ou &quot;POST&quot;. |
| *res_type* | O Content-Type usado para indicar o tipo de mídia original do recurso |
| *cache* | Estado do cache. Os valores possíveis são HIT, MISS ou PASS |
| *res_status* | O código do status HTTP como um valor inteiro. |
| *res_bsize* | Bytes de corpo enviados ao cliente na resposta. |
| *servidor* | Centro de dados do servidor de cache CDN. |
| *regras* | O nome de qualquer regra correspondente, para regras CDN e regras waf.<br><br>As regras CDN correspondentes aparecem na entrada de log para todas as solicitações para o CDN, independentemente de ser uma ocorrência, transmissão ou erro de CDN.<br><br>Também indica se a correspondência resultou em um bloco. <br><br>Por exemplo, &quot;`cdn=;waf=SQLI;action=blocked`&quot;<br><br>Vazio se nenhuma regra for correspondente. |
