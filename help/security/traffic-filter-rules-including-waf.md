---
title: Regras de filtro de tráfego incluindo regras WAF
description: Configuração das regras de filtro de tráfego incluindo as regras do WAF (Web Application Firewall)
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 221f6df73fe660c6f8dbf79affdccdd081ad3906
workflow-type: tm+mt
source-wordcount: '4210'
ht-degree: 1%

---


# Regras de filtro de tráfego incluindo regras WAF {#traffic-filter-rules-including-waf-rules}

>[!NOTE]
>
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada em andamento, envie um email para **aemcs-waf-adopter@adobe.com**, incluindo o nome da organização e o contexto sobre o interesse no recurso.

As regras de filtro de tráfego podem ser usadas para bloquear ou permitir solicitações na camada CDN, que pode ser útil em cenários como:

* Restrição do acesso a domínios específicos para tráfego interno da empresa, antes que um novo site entre em funcionamento
* Estabelecimento de limites de taxa para que sejam menos susceptíveis a ataques de DDoS volumétricos
* Impedindo que endereços IP conhecidos como mal-intencionados direcionem suas páginas

Algumas dessas regras de filtro de tráfego estão disponíveis para todos os clientes do AEM as a Cloud Service Sites e do Forms. Eles operam principalmente em propriedades de solicitação e cabeçalhos de solicitação, incluindo IP, nome do host, caminho e agente do usuário.

Uma subcategoria de regras de filtro de tráfego exige uma licença de Segurança aprimorada ou uma licença de Segurança de proteção WAF-DDoS. Essas regras avançadas são conhecidas como regras de filtro de tráfego do WAF (Web Application Firewall) (ou regras do WAF abreviadas) e têm acesso à [Sinalizadores do WAF](#waf-flags-list) descrito posteriormente neste artigo. Os clientes do Sites e do Forms podem entrar em contato com a equipe da conta Adobe para obter detalhes sobre como licenciar esse recurso avançado.

As regras de filtro de tráfego podem ser implantadas por meio dos pipelines de configuração do Cloud Manager para desenvolvimento, preparo e tipos de ambiente de produção em programas de produção (que não são de sandbox). O suporte a RDEs virá no futuro.

## Como este artigo está organizado {#how-organized}

Este artigo está organizado nas seguintes seções:

* **Visão geral da proteção de tráfego:** Saiba como você está protegido contra tráfego mal-intencionado.
* **Processo sugerido para configurar as regras:** Leia sobre uma metodologia de alto nível para proteger seu site.
* **Configuração:** Descubra como configurar e implantar regras de filtro de tráfego, incluindo as regras avançadas do WAF.
* **Sintaxe de regras:** Leia sobre como declarar regras de filtro de tráfego no `cdn.yaml` arquivo de configuração. Isso inclui as regras de filtro de tráfego disponíveis para todos os clientes do Sites e do Forms, bem como a subcategoria de regras do WAF para aqueles que licenciam esse recurso.
* **Exemplos de regras:** Veja exemplos de regras declaradas para começar.
* **Regras de limite de taxa:** Saiba como usar regras de limitação de taxa para proteger seu site contra ataques de alto volume.
* **Logs da CDN:** Veja quais regras e sinalizadores do WAF declarados correspondem ao seu tráfego.
* **Ferramentas do painel:** Analise seus logs de CDN para criar novas regras de filtro de tráfego.
* **Tutorial:** Conhecimento prático sobre o recurso, incluindo como usar ferramentas de painel de controle para declarar as regras certas.
<!-- About the tutorial: sets the context for a linked tutorial, which gives you practical knowledge about the feature, including how to use dashboard tooling to declare the right rules. -->

## Visão geral da proteção de tráfego {#traffic-protection-overview}

No cenário digital atual, o tráfego mal-intencionado é uma ameaça constante. Reconhecemos a gravidade do risco e oferecemos várias abordagens para proteger os aplicativos dos clientes e mitigar ataques quando eles ocorrem.

Na borda, o CDN gerenciado por Adobe absorve ataques de DDoS na camada de rede (camadas 3 e 4), incluindo ataques de inundação e de reflexão/amplificação.

Por padrão, o Adobe adota medidas para evitar a degradação do desempenho devido a picos de tráfego inesperadamente alto além de um determinado limite. No caso de um ataque de DDoS afetar a disponibilidade do site, as equipes de operações do Adobe são alertadas e tomam medidas para atenuar o problema.

Os clientes podem tomar medidas proativas para atenuar os ataques à camada do aplicativo (camada 7), configurando regras em várias camadas do fluxo de entrega de conteúdo.

Por exemplo, na camada Apache, os clientes podem configurar a variável [módulo do dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) ou [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) para limitar o acesso a determinados conteúdos.

E, como este artigo descreve, as regras de filtro de tráfego podem ser implantadas na CDN, usando o pipeline de configuração do Cloud Manager. Além das regras de filtro de tráfego baseadas em solicitações de tráfego baseadas em propriedades como endereço IP, caminho e cabeçalhos, os clientes também podem licenciar uma subcategoria poderosa de regras de filtro de tráfego chamada regras WAF.

## Processo sugerido {#suggested-process}

Veja a seguir um processo completo recomendado de alto nível para criar as regras certas de filtro de tráfego:

1. Configure um pipeline de configuração de não produção e produção, conforme descrito na seção [Configuração](#setup) seção.
1. Os clientes que licenciaram a subcategoria das regras de filtro de tráfego do WAF devem habilitá-los no Cloud Manager.
1. Leia e experimente o tutorial para entender concretamente como usar as regras de filtro de tráfego, incluindo as regras do WAF, se tiverem sido licenciadas. O tutorial o orienta pela implantação de regras em um ambiente de desenvolvimento, simulando tráfego mal-intencionado, baixando o [Logs da CDN](#cdn-logs)e analisá-los em [ferramentas do painel](#dashboard-tooling).
1. Copiar as regras iniciais recomendadas para `cdn.yaml` e implante a configuração na produção no modo de log.
1. Depois de coletar algum tráfego, analise os resultados usando [ferramentas do painel](#dashboard-tooling) para ver se havia correspondências. Procure falsos positivos e faça os ajustes necessários, ativando as regras padrão no modo de bloco.
1. Adicione regras personalizadas com base na análise dos logs de CDN, primeiro testando com tráfego simulado em ambientes de desenvolvimento, antes de implantar em preparo e produção no modo de log e, em seguida, no modo de bloqueio.
1. Monitore o tráfego continuamente, fazendo alterações nas regras à medida que o cenário de ameaças evolui.

## Configurar {#setup}

1. Primeiro, crie a seguinte pasta e estrutura de arquivo para a pasta de nível superior em seu projeto no Git:

   ```
   config/
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
       # Block simple path
       - name: block-path
         when:
           allOf:
             - reqProperty: tier
               matches: "author|publish"
             - reqProperty: path
               equals: '/block/me'
         action: block
   ```

A variável `kind` O parâmetro deve ser definido como `CDN` e a versão deve ser definida como a versão do schema, que está `1`. Veja mais exemplos abaixo.


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. Para configurar as regras do WAF, o WAF deve estar ativado no Cloud Manager, conforme descrito abaixo, para os cenários de programa novos e existentes. Observe que uma licença separada deve ser adquirida para o WAF.

   1. Para configurar o WAF em um novo programa, marque a opção **Proteção WAF-DDOS** caixa de seleção na **Segurança** quando você [adicionar um programa de produção.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. Para configurar o WAF em um programa existente, [editar seu programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) e no **Segurança** desmarque ou marque a opção **WAF-DDOS** a qualquer momento.

1. Para tipos de ambiente diferentes do RDE, crie um pipeline de configuração de implantação direcionada no Cloud Manager.

   * [Consulte este documento para ver os pipelines de produção.](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Consulte este documento para ver se há pipelines de não produção.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

Para RDEs, a linha de comando será usada, mas RDE não é compatível no momento.

## Sintaxe das regras de filtro de tráfego {#rules-syntax}

Você pode configurar `traffic filter rules` para corresponder a padrões como IPs, agente de usuário, cabeçalhos de solicitação, nome do host, localização geográfica e url.

Os clientes que licenciam a oferta Segurança aprimorada ou Segurança de proteção WAF-DDoS também podem configurar uma categoria especial de regras de filtro de tráfego chamada `WAF traffic filter rules` (ou regras WAF para abreviar) que fazem referência a um ou mais [Sinalizadores do WAF](#waf-flags-list).

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

O formato das regras de filtro de tráfego na variável `cdn.yaml` arquivo está descrito abaixo. Ver alguns [outros exemplos](#examples) em uma seção posterior, bem como em uma seção separada sobre [Regras de limite de taxa](#rate-limit-rules).


| **Propriedade** | **Maioria das regras de filtro de tráfego** | **Regras de filtro de tráfego do WAF** | **Tipo** | **Valor padrão** | **Descrição** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Nome da regra (64 caracteres de comprimento, pode conter apenas alfanuméricos e - ) |
| quando | X | X | `Condition` | - | A estrutura básica é:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[Consulte Sintaxe da estrutura de condição](#condition-structure) abaixo, que descreve os getters, predicados e como combinar várias condições. |
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
| reqCookie | `string` | Retorna o cookie com o nome especificado |
| postParam | `string` | Retorna o parâmetro com o nome especificado do corpo. Funcionar somente quando o corpo for do tipo de conteúdo `application/x-www-form-urlencoded` |

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
| **existe** | `boolean` | verdadeiro quando definido como verdadeiro e a propriedade existe ou quando definido como falso e a propriedade não existe |

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

A variável `wafFlags` que pode ser usada nas regras de filtro de tráfego WAF licenciáveis, pode fazer referência ao seguinte:

| **ID do sinalizador** | **Nome do sinalizador** | **Descrição** |
|---|---|---|
| SQLI | Injeção de SQL | A Injeção de SQL é a tentativa de obter acesso a um aplicativo ou obter informações privilegiadas executando consultas arbitrárias ao banco de dados. |
| BACKDOOR | Backdoor | Um sinal backdoor é uma solicitação que tenta determinar se um arquivo backdoor comum está presente no sistema. |
| CMDEXE | Execução de comando | Execução de Comando é a tentativa de obter controle ou danificar um sistema alvo através de comandos arbitrários do sistema por meio da entrada do usuário. |
| XSS | Criação de script entre sites | Cross-Site Scripting é a tentativa de sequestrar a conta de um usuário ou a sessão de navegação na Web por meio de um código JavaScript mal-intencionado. |
| PASSAGEM | Diretório de passagem | O Diretory Traversal é a tentativa de navegar pelas pastas privilegiadas em todo o sistema, na esperança de obter informações confidenciais. |
| USERAGENT | Ferramentas de ataque | Ferramentas de ataque é o uso de software automatizado para identificar vulnerabilidades de segurança ou para tentar explorar uma vulnerabilidade detectada. |
| LOG4J-JNDI | Log4J JNDI | Os ataques ao Log4J JNDI tentam explorar a [Vulnerabilidade do Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente nas versões do Log4J anteriores à 2.16.0 |
| BHH | Cabeçalhos de salto inválidos | Os cabeçalhos de salto inválido indicam uma tentativa de contrabando de HTTP por meio de um cabeçalho TE (Transferir Codificação) ou CL (Conteúdo Comprimento) malformado, ou um cabeçalho TE e CL bem formado |
| ANORMALPATH | Caminho anormal | Caminho anormal indica que o caminho original difere do caminho normalizado (por exemplo, `/foo/./bar` é normalizado para `/foo/bar`) |
| CODIFICAÇÃODUPLA | Codificação dupla | A Codificação dupla verifica a técnica de evasão de caracteres html de codificação dupla |
| NOTUTF8 | Codificação inválida | Codificação inválida pode fazer com que o servidor traduza caracteres mal-intencionados de uma solicitação em uma resposta, causando uma negação de serviço ou XSS |
| ERRO JSON | Erro de codificação JSON | Um corpo de solicitação POST, PUT ou PATCH especificado como contendo JSON no cabeçalho de solicitação &quot;Content-Type&quot;, mas que contém erros de análise JSON. Isso geralmente está relacionado a um erro de programação ou a uma solicitação automatizada ou mal-intencionada. |
| DADOS MALFORMADOS | Dados malformados no corpo da solicitação | Um corpo de solicitação POST, PUT ou PATCH que está malformado de acordo com o cabeçalho de solicitação &quot;Content-Type&quot;. Por exemplo, se um cabeçalho de solicitação &quot;Content-Type: application/x-www-form-urlencoded&quot; for especificado e contiver um corpo de POST que seja json. Isso geralmente é um erro de programação, uma solicitação automatizada ou mal-intencionada. Exige o agente 3.2 ou superior. |
| SANS | Tráfego IP mal-intencionado | [SANS Internet Storm Center](https://isc.sans.edu/) lista de endereços IP relatados como envolvidos em atividades mal-intencionadas |
| SIGSCI-IP | Efeito de rede | IP sinalizado por SignalSciences: sempre que um IP é sinalizado devido a um sinal mal-intencionado pelo mecanismo de decisão, esse IP é propagado para todos os clientes. As solicitações subsequentes desses endereços IP que contêm qualquer sinal adicional durante o sinalizador são registradas |
| NO-CONTENT-TYPE | Cabeçalho da solicitação &quot;Content-Type&quot; ausente | Uma solicitação POST, PUT ou PATCH que não tem um cabeçalho de solicitação &quot;Content-Type&quot;. Por padrão, os servidores de aplicativos devem assumir &quot;Content-Type: text/plain; charset=us-ascii&quot; neste caso. Muitas solicitações automatizadas e mal-intencionadas podem estar sem &quot;Tipo de conteúdo&quot;. |
| NOUA | Nenhum agente de usuário | Muitas solicitações automatizadas e mal-intencionadas usam User-Agents falsos ou ausentes para dificultar a identificação do tipo de dispositivo que faz as solicitações. |
| TORNODE | Tráfego Tor | Tor é um software que oculta a identidade de um usuário. Um pico no tráfego Tor pode indicar um invasor tentando mascarar sua localização. |
| NULLBYTE | Byte nulo | Bytes nulos normalmente não aparecem em uma solicitação e indicam que a solicitação está malformada e é potencialmente maliciosa. |
| ARQUIVOPRIVADO | Arquivos privados | Os arquivos privados geralmente têm natureza confidencial, como um Apache `.htaccess` ou um arquivo de configuração que poderia vazar informações confidenciais |
| SCANNER | Scanner | Identifica ferramentas e serviços de digitalização populares |
| RESPONSESPLIT | Divisão de resposta HTTP | Identifica quando os caracteres CRLF são enviados como entrada para o aplicativo para inserir cabeçalhos na resposta HTTP |
| XML-ERROR | Erro de codificação de XML | Um corpo de solicitação POST, PUT ou PATCH especificado como contendo XML dentro do cabeçalho de solicitação &quot;Content-Type&quot;, mas que contém erros de análise XML. Isso geralmente está relacionado a um erro de programação ou a uma solicitação automatizada ou mal-intencionada. |

## Considerações {#considerations}

* Quando duas regras conflitantes são criadas, as regras de permissão sempre têm prioridade sobre as regras de bloqueio. Por exemplo, se você criar uma regra para bloquear um caminho específico e uma regra para permitir um endereço IP específico, as solicitações desse endereço IP no caminho bloqueado serão permitidas.

* Se uma regra for correspondente e bloqueada, a CDN responderá com uma `406` código de retorno.

* Os arquivos de configuração não devem conter segredos, pois eles podem ser lidos por qualquer pessoa com acesso ao repositório Git.

## Exemplos de regras {#examples}

Alguns exemplos de regras se seguem. Consulte a [seção limite de taxa](#rules-with-rate-limits) mais abaixo para exemplos de regras de limite de taxa.

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
        when:
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

Essa regra bloqueia solicitações de caminho `/block-me`, e bloqueia cada solicitação que corresponda a um `SQLI` ou `XSS` padrão. Este exemplo inclui regras de filtro de tráfego WAF, que fazem referência a `SQLI` e `XSS` [Sinalizadores do WAF](#waf-flags-list), que exigem uma licença separada.

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

**Exemplo 5**

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
            - reqProperty: tier
              matches: "author|publish"
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

## Regras de limite de taxa {#rate-limits-rules}

Às vezes, é desejável bloquear o tráfego correspondente a uma regra somente se a correspondência exceder uma determinada taxa ao longo do tempo. Definir um valor para o `rateLimit` A propriedade limita a taxa dessas solicitações que correspondem à condição da regra.

As regras de limite de taxa não podem fazer referência aos sinalizadores WAF. Eles estão disponíveis para todos os clientes do Sites e do Forms.

### Estrutura rateLimit {#ratelimit-structure}

| **Propriedade** | **Tipo** | **Padrão** | **SIGNIFICADO** |
|---|---|---|---|
| limite | número inteiro de 10 a 10000 | obrigatório | Taxa de solicitações (por CDN POP) em solicitações por segundo para as quais a regra é acionada. |
| janela | enumeração de inteiros: 1, 10 ou 60 | 10 | Janela de amostragem em segundos para a qual a taxa de solicitação é calculada. |
| penalidade | número inteiro de 60 a 3600 | 300 (5 minutos) | Um período em segundos para o qual as solicitações correspondentes são bloqueadas (arredondado para o minuto mais próximo). |
| groupBy | matriz[Getter] | nenhuma | o contador do limitador de taxa será agregado por um conjunto de propriedades de solicitação (por exemplo, clientIp). |

### Exemplos {#ratelimiting-examples}

**Exemplo 1**

Essa regra bloqueia um cliente para 5m quando ele excede 100 req/s (por POP CDN) nos últimos 60 segundos:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Exemplo 2**

Bloquear solicitações para 60s no caminho /crítico/recurso quando ele exceder 100 solic./s (por POP CDN) nos últimos 60 segundos:

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

Observe que os logs CDN podem atrasar até 5 minutos.

A variável `rules` A propriedade descreve quais regras de filtro de tráfego são correspondidas e tem o seguinte padrão:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Por exemplo:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

As regras se comportam da seguinte maneira:

* O nome de regra declarado pelo cliente de qualquer regra correspondente será listado no atributo matches.
* O atributo action detalha se as regras tiveram o efeito de bloquear, permitir ou registrar.
* Se o WAF estiver licenciado e ativado, o atributo waf listará quaisquer regras waf (por exemplo, SQLI; observe que isso é independente do nome declarado pelo cliente) que foram detectadas, independentemente das regras waf terem sido listadas na configuração.
* Se nenhuma regra declarada pelo cliente for correspondente e nenhuma regra waf for correspondente, a propriedade de atributo de regras ficará em branco.

Em geral, as regras correspondentes aparecem na entrada de log para todas as solicitações para o CDN, independentemente de ser uma ocorrência, transmissão ou erro do CDN. No entanto, as regras do WAF aparecem na entrada do log somente para solicitações ao CDN que são consideradas perdidas ou transmitidas pelo CDN, mas não para ocorrências de CDN.

O exemplo abaixo mostra uma amostra `cdn.yaml` e duas entradas de log CDN:


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

## Ferramentas do painel {#dashboard-tooling}

O Adobe fornece um mecanismo para baixar ferramentas de painel no computador a fim de assimilar logs CDN baixados pelo Cloud Manager. Com essa ferramenta, você pode analisar o tráfego para ajudar a criar as regras de filtro de tráfego apropriadas a serem declaradas, incluindo regras WAF.

As ferramentas do painel de controle podem ser clonadas diretamente do [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Repositório Github.

[Veja o tutorial](#tutorial) para obter instruções concretas sobre como usar as ferramentas do painel.

## Tutorial {#tutorial}

O Adobe fornece um mecanismo para baixar ferramentas de painel no computador a fim de assimilar logs CDN baixados pelo Cloud Manager. Com essa ferramenta, você pode analisar o tráfego para ajudar a criar as regras de filtro de tráfego apropriadas a serem declaradas, incluindo regras WAF. Esta seção primeiro fornece algumas instruções para se familiarizar com as ferramentas do painel em um ambiente de desenvolvimento, seguidas de orientação sobre como aproveitar esse conhecimento para criar regras em um ambiente de produção.

As ferramentas do painel de controle podem ser clonadas diretamente do [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Repositório GitHub.


### Conhecimento das ferramentas de painel de controle {#dashboard-getting-familiar}

1. Crie um pipeline de configuração de não produção do Cloud Manager associado a um ambiente de desenvolvimento. Selecione primeiro o **Pipeline de implantação** opção. Em seguida, selecione **Implantação direcionada**, Config, o repositório, a ramificação Git e defina o local do código como /config.

   ![Adicionar implantação selecionada de pipeline de não produção](/help/security/assets/waf-select-pipeline1.png)

   ![Adicionar seleção de pipeline de não produção direcionada](/help/security/assets/waf-select-pipeline2.png)

[Consulte este documento para obter detalhes sobre a configuração de pipelines de não produção.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. No espaço de trabalho, crie uma configuração de pasta no nível raiz e adicione um arquivo chamado `cdn.yaml`, em que você declarará uma regra simples, definindo-a no modo de log, em vez de no modo de bloqueio.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: log
```

1. Confirme e envie suas alterações e implante sua configuração usando o pipeline de configuração.

   ![Executar pipeline de configuração](/help/security/assets/waf-run-pipeline.png)

1. Depois que a configuração for implantada, tente acessar `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` usando seu navegador da web ou com o comando curl abaixo. Você deve receber uma página de erro 404, pois essa página não existe.

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Baixe os logs CDN do Cloud Manager e valide se as regras corresponderam como esperado, com uma propriedade de regras que corresponda ao nome da regra:

   ```
   "rules": "match=log-rule-example"
   ```

   ![Selecionar logs de download](/help/security/assets/waf-download-logs1.png)

   ![Baixar logs](/help/security/assets/waf-download-logs2.png)

1. Carregue a imagem do Docker com a ferramenta de painel e siga o arquivo README para assimilar os logs de CDN. Conforme representado nas capturas de tela a seguir, selecione o período certo, o ambiente certo e os filtros corretos.

   ![Selecionar tempo no painel](/help/security/assets/dashboard-select-time.png)

   ![Selecionar ambiente no painel](/help/security/assets/dashboard-select-env.png)

1. Depois que os filtros corretos forem aplicados, você poderá ver um painel carregado com os dados esperados. Na captura de tela abaixo, o log-rule-example da regra foi acionado 3 vezes nas últimas 2 horas, pelo mesmo IP localizado na Irlanda, usando um navegador da Web e curl.

   ![Exibir dados do painel de desenvolvimento](/help/security/assets/dashboard-see-data-logmode.png)
   ![Exibir widgets de dados do painel de desenvolvimento](/help/security/assets/dashboard-see-data-logmode2.png)

1. Agora altere o cdn.yaml para colocar a regra no modo de bloqueio para garantir que as páginas sejam bloqueadas, conforme esperado. Em seguida, confirme, envie e acione o pipeline de configuração conforme feito anteriormente.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: block
```

1. Depois que a configuração for implantada, tente acessar `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` usando seu navegador da web ou com o comando curl abaixo. Você deve receber uma página de erro 406, indicando que a solicitação foi bloqueada.

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Mais uma vez, baixe os logs de CDN no Cloud Manager (observação: pode levar até 5 minutos para que as novas solicitações sejam expostas nos logs de CDN) e importe-as na ferramenta do painel, como fizemos anteriormente. Depois de concluído, atualize o painel. Como você pode ver na captura de tela abaixo, as solicitações para `/log/me` são bloqueados por nossa regra.

   ![Exibir dados do painel de produção](/help/security/assets/dashboard-see-data-blockmode.png)
   ![Exibir dados do painel de produção](/help/security/assets/dashboard-see-data-blockmode2.png)

1. Se você tiver os filtros de tráfego WAF ativados (isso exigirá uma licença adicional depois que o recurso for GA), repita com uma regra de filtro de tráfego WAF, no modo de log, e implante as regras.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: log-waf-flags
        when:
          reqProperty: tier
          matches: "author|publish"
        action:
          type: log
          wafFlags:
              - SANS
              - SIGSCI-IP
              - TORNODE
              - NOUA
              - SCANNER
              - USERAGENT
              - PRIVATEFILE
              - ABNORMALPATH
              - TRAVERSAL
              - NULLBYTE
              - BACKDOOR
              - LOG4J-JNDI
              - SQLI
              - XSS
              - CODEINJECTION
              - CMDEXE
              - NO-CONTENT-TYPE
              - UTF8
```

1. Use uma ferramenta como [nikto](https://github.com/sullo/nikto/tree/master) para gerar solicitações correspondentes. O comando abaixo enviará cerca de 550 solicitações mal-intencionadas em menos de 1 minuto.

   ```
   ./nikto.pl -useragent "MyAgent (Demo/1.0)" -D V -Tuning 9 -ssl -h https://publish-pXXXXX-eYYYYY.adobeaemcloud.com
   ```

1. Baixe os logs CDN do Cloud Manager (lembre-se de que eles podem levar até 5 minutos para serem exibidos) e valide se as regras declaradas correspondentes e os sinalizadores WAF são exibidos.

   Como você pode ver, várias das solicitações produzidas por Nikto estão sendo sinalizadas pela WAF como sendo maliciosas. Podemos ver que o Nikto tentou explorar vulnerabilidades CMDEXE, SQLI e NULLBYTE. Se agora você alterar a ação de registro para bloqueio e acionar novamente uma verificação usando Nikto, todas as solicitações que foram sinalizadas anteriormente serão bloqueadas desta vez.

   ![Exibir dados do WAF](/help/security/assets/dashboard-see-data-waf.png)


   Observe que sempre que uma solicitação corresponder a qualquer um dos sinalizadores do WAF, esses sinalizadores do WAF aparecerão, mesmo que não façam parte da regra declarada; isso é para que você esteja sempre ciente do tráfego mal-intencionado potencialmente novo, para o qual você ainda não declarou regras correspondentes. Como exemplo:

   ```
   "rules": "match=log-waf-flags,waf=SQLI,action=blocked"
   ```

1. Repita com uma regra que use a limitação de taxa no modo de log. Como sempre, confirme, envie e acione o pipeline de configuração para aplicar sua configuração.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: limit-requests-client-ip
        when:
          reqProperty: tier
          matches: "author|publish"
        rateLimit:
          limit: 10
          window: 1
          penalty: 60
          groupBy:
            - reqProperty: clientIp
        action: log
```

1. Use uma ferramenta como [Vegeta](https://github.com/tsenart/vegeta) para gerar tráfego.

   ```
   echo "GET https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com" | vegeta attack -duration=5s | tee results.bin | vegeta report
   ```

1. Depois de executar a ferramenta, você pode baixar os logs de CDN e assimilá-los no painel para verificar se a regra do limitador de taxa foi acionada

   ![Exibir dados do WAF](/help/security/assets/waf-dashboard-ratelimiter-1.png)

   ![Exibir dados do WAF](/help/security/assets/waf-dashboard-ratelimiter-2.png)

   Como você pode ver nossa regra **limit-requests-client-ip** foi acionado.

   Agora que você está familiarizado com o funcionamento das regras de filtro de tráfego, pode migrar para o ambiente de produção.

### Implantação de regras no ambiente de produção {#dashboard-prod-env}

Declare as regras inicialmente no modo de log para validar se não há falsos positivos, o que significa um tráfego legítimo que seria bloqueado incorretamente.

1. Crie um pipeline de configuração de produção associado ao seu ambiente de produção.

1. Copie as regras recomendadas abaixo no cdn.yaml. Talvez você queira modificar as regras com base nas características exclusivas do tráfego direto do seu site. Confirme, envie e acione o pipeline de configuração. Verifique se as regras estão no modo de log.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds 100 req/sec on a time window of 1sec
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 100
        window: 1
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
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
      action: log
    # Enable recommended WAF protections (only works if WAF is enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        matches: "author|publish"
      action:
        type: log
        wafFlags:
          - SANS
          - SIGSCI-IP
          - TORNODE
          - NOUA
          - SCANNER
          - USERAGENT
          - PRIVATEFILE
          - ABNORMALPATH
          - TRAVERSAL
          - NULLBYTE
          - BACKDOOR
          - LOG4J-JNDI
          - SQLI
          - XSS
          - CODEINJECTION
          - CMDEXE
          - NO-CONTENT-TYPE
          - UTF8
    # Disable protection against CMDEXE on /bin
    - name: allow-cdmexe-on-root-bin
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            matches: "^/bin/.*"
      action:
        type: log
        wafFlags:
          - CMDEXE
```

1. Adicione regras adicionais para bloquear o tráfego mal-intencionado que você possa estar ciente. Por exemplo, determinados IPs que têm atacado seu site.

1. Após alguns minutos, horas ou dias, dependendo do volume de tráfego do site, baixe os logs de CDN do Cloud Manager e analise-os com o painel.

1. Estas são algumas considerações:
   1. As regras declaradas de correspondência de tráfego são exibidas em gráficos e registros de solicitações para que você possa verificar facilmente se suas regras declaradas estão sendo acionadas.
   1. Os sinalizadores de correspondência de tráfego do WAF aparecem em gráficos e logs de solicitação, mesmo que você não os tenha registrado em uma regra. Dessa forma, você está sempre ciente do tráfego mal-intencionado potencialmente novo e pode criar novas regras conforme necessário. Observe os sinalizadores do WAF que não são refletidos nas regras declaradas e considere declará-los.
   1. Para regras correspondentes, verifique se há falsos positivos nos registros de solicitações e veja se você pode filtrá-los para fora das regras. Por exemplo, talvez sejam um falso positivo apenas para certos caminhos.

1. Defina as regras apropriadas para o modo de bloqueio e considere adicionar outras regras. Talvez algumas das regras devam permanecer no modo de log ao analisar mais detalhadamente com mais tráfego.

1. Reimplante a configuração.

1. Repita a análise dos painéis regularmente.

