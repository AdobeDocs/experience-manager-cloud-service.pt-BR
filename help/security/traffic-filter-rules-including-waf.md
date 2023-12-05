---
title: Regras de filtro de tráfego incluindo regras WAF
description: Configuração das regras de filtro de tráfego incluindo as regras do WAF (Web Application Firewall)
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '3357'
ht-degree: 0%

---


# Regras de filtro de tráfego incluindo regras WAF {#traffic-filter-rules-including-waf-rules}

As regras de filtro de tráfego podem ser usadas para bloquear ou permitir solicitações na camada CDN, que pode ser útil em cenários como:

* Restrição do acesso a domínios específicos para tráfego interno da empresa, antes que um novo site entre em funcionamento
* Estabelecimento de limites de taxa para que sejam menos susceptíveis a ataques volumétricos de DoS
* Impedindo que endereços IP conhecidos como mal-intencionados direcionem suas páginas

A maioria dessas regras de filtro de tráfego está disponível para todos os clientes do AEM as a Cloud Service Sites e do Forms. Eles operam principalmente em propriedades de solicitação e cabeçalhos de solicitação, incluindo IP, nome do host, caminho e agente do usuário.

Uma subcategoria de regras de filtro de tráfego exige uma licença de Segurança aprimorada ou uma licença de Proteção WAF-DDoS e estará disponível no final deste ano. Essas regras avançadas são conhecidas como regras de filtro de tráfego do WAF (Web Application Firewall) (ou regras do WAF abreviadas) e têm acesso à [Sinalizadores do WAF](#waf-flags-list) descrito posteriormente neste artigo.

As regras de filtro de tráfego podem ser implantadas por meio dos pipelines de configuração do Cloud Manager para desenvolvimento, preparo e tipos de ambiente de produção em programas de produção (que não são de sandbox). O suporte a RDEs virá no futuro.

[Seguir um tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html) para criar rapidamente conhecimentos concretos sobre esse recurso.

## Como este artigo está organizado {#how-organized}

Este artigo está organizado nas seguintes seções:

* **Visão geral da proteção de tráfego:** Saiba como você está protegido contra tráfego mal-intencionado.
* **Processo sugerido para configurar as regras:** Leia sobre uma metodologia de alto nível para proteger seu site.
* **Configuração:** Descubra como configurar e implantar regras de filtro de tráfego, incluindo as regras avançadas do WAF.
* **Sintaxe de regras:** Leia sobre como declarar regras de filtro de tráfego no `cdn.yaml` arquivo de configuração. Isso inclui as regras de filtro de tráfego disponíveis para todos os clientes do Sites e do Forms, e a subcategoria de regras do WAF para aqueles que licenciam esse recurso.
* **Exemplos de regras:** Veja exemplos de regras declaradas para começar.
* **Regras de limite de taxa:** Saiba como usar regras de limitação de taxa para proteger seu site contra ataques de alto volume.
* **Logs da CDN:** Veja quais regras e sinalizadores do WAF declarados correspondem ao seu tráfego.
* **Ferramentas do painel:** Analise seus logs de CDN para criar novas regras de filtro de tráfego.
* **Regras de Início Recomendadas:** Um conjunto de regras para começar.
* **Tutorial:** Conhecimento prático sobre o recurso, incluindo como usar ferramentas de painel de controle para declarar as regras certas.

Convidamos você a fornecer feedback ou fazer perguntas sobre as regras do filtro de tráfego enviando um email **aemcs-waf-adopter@adobe.com**.

## Visão geral da proteção de tráfego {#traffic-protection-overview}

No cenário digital atual, o tráfego mal-intencionado é uma ameaça constante. Reconhecemos a gravidade do risco e oferecemos várias abordagens para proteger os aplicativos dos clientes e mitigar ataques quando eles ocorrem.

Na borda, o CDN gerenciado por Adobe absorve ataques de DoS na camada de rede (camadas 3 e 4), incluindo ataques de inundação e de reflexão/amplificação.

Por padrão, o Adobe adota medidas para evitar a degradação do desempenho devido a picos de tráfego inesperadamente alto além de um determinado limite. No caso de um ataque de DoS afetar a disponibilidade do site, as equipes de operações do Adobe são alertadas e tomam medidas para atenuar o problema.

Os clientes podem tomar medidas proativas para atenuar os ataques à camada do aplicativo (camada 7), configurando regras em várias camadas do fluxo de entrega de conteúdo.

Por exemplo, na camada Apache, os clientes podem configurar a variável [módulo do dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) ou [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) para limitar o acesso a determinados conteúdos.

E, como este artigo descreve, as regras de filtro de tráfego podem ser implantadas no CDN gerenciado pelo Adobe, usando o pipeline de configuração do Cloud Manager. Além das regras de filtro de tráfego baseadas em propriedades como endereço IP, caminho e cabeçalhos ou regras baseadas na definição de limites de taxa, os clientes também podem licenciar uma subcategoria avançada de regras de filtro de tráfego chamada regras WAF.

## Processo sugerido {#suggested-process}

Veja a seguir um processo completo recomendado de alto nível para criar as regras certas de filtro de tráfego:

1. Configure pipelines de configuração de não produção e produção, conforme descrito na seção [Configuração](#setup) seção.
1. Os clientes que licenciaram a subcategoria das regras de filtro de tráfego do WAF devem habilitá-los no Cloud Manager.
1. Leia e experimente o tutorial para entender concretamente como usar as regras de filtro de tráfego, incluindo as regras do WAF, se tiverem sido licenciadas. O tutorial o orienta pela implantação de regras em um ambiente de desenvolvimento, simulando tráfego mal-intencionado, baixando o [Logs da CDN](#cdn-logs)e analisá-los em [ferramentas do painel](#dashboard-tooling).
1. Copiar as regras de início recomendadas para `cdn.yaml` e implante a configuração no ambiente de produção no modo de log.
1. Depois de coletar algum tráfego, analise os resultados usando [ferramentas do painel](#dashboard-tooling) para ver se havia correspondências. Procure falsos positivos e faça os ajustes necessários, permitindo, em última análise, as regras de início no modo de bloco.
1. Adicione regras personalizadas com base na análise dos logs de CDN, primeiro testando com tráfego simulado em ambientes de desenvolvimento antes de implantar em ambientes de preparo e produção no modo de log e, em seguida, no modo de bloqueio.
1. Monitore o tráfego continuamente, fazendo alterações nas regras à medida que o cenário de ameaças evolui.

## Configurar {#setup}

1. Primeiro, crie a seguinte pasta e estrutura de arquivo para a pasta de nível superior em seu projeto no Git:

   ```
   config/
        cdn.yaml
   ```

1. `cdn.yaml` deve conter metadados e uma lista de regras de filtros de tráfego e regras WAF.

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


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (for example, "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. Se as regras do WAF estiverem licenciadas, você deverá habilitar o recurso no Cloud Manager, conforme descrito abaixo, para os cenários de programa novo e existente.

   1. Para configurar o WAF em um novo programa, marque a opção **Proteção WAF-DDOS** caixa de seleção na **Segurança** quando você [adicionar um programa de produção.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. Para configurar o WAF em um programa existente, [editar seu programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) e no **Segurança** desmarque ou marque a opção **WAF-DDOS** a qualquer momento.

1. Para tipos de ambiente diferentes do RDE, crie um pipeline de configuração de implantação direcionada no Cloud Manager.

   * [Consulte configuração de pipelines de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).
   * [Consulte configuração de pipelines de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

Para RDEs, a linha de comando será usada, mas RDE não é compatível no momento.

**Notas**

* Você pode usar `yq` para validar localmente a formatação YAML do seu arquivo de configuração (por exemplo, `yq cdn.yaml`).

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

O formato das regras de filtro de tráfego na variável `cdn.yaml` arquivo está descrito abaixo. Ver alguns [outros exemplos](#examples) em uma seção posterior, e em uma seção separada sobre [Regras de limite de taxa](#rate-limit-rules).


| **Propriedade** | **Maioria das regras de filtro de tráfego** | **Regras de filtro de tráfego do WAF** | **Tipo** | **Valor padrão** | **Descrição** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Nome da regra (64 caracteres de comprimento, pode conter apenas alfanuméricos e - ) |
| quando | X | X | `Condition` | - | A estrutura básica é:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[Consulte Sintaxe da estrutura de condição](#condition-structure) abaixo, que descreve os getters, predicados e como combinar várias condições. |
| ação | X | X | `Action` | log | objeto log, allow, block ou Action. O padrão é log |
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
| reqProperty | `string` | Propriedade de solicitação.<br><br>Um de:<br><ul><li>`path`: retorna o caminho completo de um URL sem os parâmetros de consulta.</li><li>`queryString`: retorna a parte da consulta de um URL</li><li>`method`: retorna o método HTTP usado na solicitação.</li><li>`tier`: retorna um de `author`, `preview` ou `publish`.</li><li>`domain`: retorna a propriedade do domínio (conforme definido na variável `Host` cabeçalho) em minúsculas</li><li>`clientIp`: retorna o IP do cliente.</li><li>`clientCountry`: retorna um código de duas letras ([https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) que identificam o país em que o cliente está localizado.</li></ul> |
| reqHeader | `string` | Retorna o cabeçalho da solicitação com o nome especificado |
| queryParam | `string` | Retorna o parâmetro de consulta com o nome especificado |
| reqCookie | `string` | Retorna o cookie com o nome especificado |
| postParam | `string` | Retorna o parâmetro Post com o nome especificado do corpo da Solicitação. Funciona somente quando o corpo é do tipo de conteúdo `application/x-www-form-urlencoded` |

**Predicado**

| **Propriedade** | **Tipo** | **Significado** |
|---|---|---|
| **igual a** | `string` | true se o resultado de getter for igual ao valor fornecido |
| **doesNotEqual** | `string` | true se o resultado de getter não for igual ao valor fornecido |
| **curtir** | `string` | true se o resultado de getter corresponder ao padrão fornecido |
| **notLike** | `string` | true se o resultado de getter não corresponder ao padrão fornecido |
| **corresponde a** | `string` | true se o resultado de getter corresponder ao regex fornecido |
| **doesNotMatch** | `string` | true se o resultado de getter não corresponder ao regex fornecido |
| **in** | `array[string]` | true se a lista fornecida contiver o resultado getter |
| **notIn** | `array[string]` | true se a lista fornecida não contiver o resultado getter |
| **existe** | `boolean` | verdadeiro quando definido como verdadeiro e a propriedade existe ou quando definido como falso e a propriedade não existe |

**Notas**

* A propriedade da solicitação `clientIp` só pode ser usado com os seguintes predicados: `equals`, `doesNotEqual`, `in`, `notIn`. `clientIp` também podem ser comparados com intervalos IP ao usar `in` e `notIn` predicados. O exemplo a seguir implementa uma condição para avaliar se um IP de cliente está no intervalo IP de 192.168.0.0/24 (portanto, de 192.168.0.0 a 192.168.0.255):

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* Recomendamos o uso de [regex101](https://regex101.com/) e [Fastly Fiddle](https://fiddle.fastly.dev/) ao trabalhar com regex. Você também pode saber mais sobre como o Fastly lida com regex neste [artigo](https://developer.fastly.com/reference/vcl/regex/#best-practices-and-common-mistakes).


### Estrutura de ação {#action-structure}

Um `action` pode ser uma string que especifica a ação (permitir, bloquear ou registrar) ou um objeto composto pelo tipo de ação (permitir, bloquear ou registrar) e opções como wafFlags e/ou status.

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

* As Listas de permissões IP definidas no Cloud Manager têm prioridade sobre as Regras de filtros de tráfego.

* As correspondências de regras do WAF aparecem somente nos logs CDN para erros e passagens de CDN, não para ocorrências.

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

Essa regra bloqueia solicitações de caminho `/block-me`, e bloqueia cada solicitação que corresponda a um `SQLI` ou `XSS` padrão. Este exemplo inclui regras de filtro de tráfego WAF, que fazem referência a `SQLI` e `XSS` [Sinalizadores do WAF](#waf-flags-list)e, portanto, requer uma licença separada.

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

Às vezes, é desejável bloquear o tráfego se ele exceder uma determinada taxa de solicitações recebidas, talvez com base em uma condição específica. Definir um valor para o `rateLimit` A propriedade limita a taxa dessas solicitações que correspondem à condição da regra.

As regras de limite de taxa não podem fazer referência aos sinalizadores WAF. Eles estão disponíveis para todos os clientes do Sites e do Forms.

Os limites de taxa são calculados por CDN POP. Como exemplo, suponha que os POPs em Montreal, Miami e Dublin tenham taxas de tráfego de 80, 90 e 120 solicitações por segundo, respectivamente, e que a regra de limite de taxa seja definida como um limite de 100. Nesse caso, apenas o tráfego com destino a Dublim seria limitado em termos tarifários.

### Estrutura rateLimit {#ratelimit-structure}

| **Propriedade** | **Tipo** | **Padrão** | **SIGNIFICADO** |
|---|---|---|---|
| limite | número inteiro de 10 a 10000 | obrigatório | Taxa de solicitações (por CDN POP) em solicitações por segundo para as quais a regra é acionada. |
| janela | enumeração de inteiros: 1, 10 ou 60 | 10 | Janela de amostragem em segundos para a qual a taxa de solicitação é calculada. A precisão dos contadores dependerá do tamanho da janela (maior precisão da janela). Por exemplo, pode-se esperar 50% de precisão para a janela de 1 segundo e 90% de precisão para a janela de 60 segundos. |
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

O AEM as a Cloud Service fornece acesso aos logs de CDN, que são úteis para casos de uso, incluindo otimização da taxa de ocorrência do cache e configuração das regras de filtro de tráfego. Os logs do CDN aparecem no Cloud Manager **Baixar logs** , ao selecionar o serviço Autor ou Publicar.

Os logs do CDN podem ser atrasados em até cinco minutos.

A variável `rules` A propriedade descreve quais regras de filtro de tráfego são correspondidas e tem o seguinte padrão:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Por exemplo:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

As regras se comportam da seguinte maneira:

* O nome de regra declarado pelo cliente de qualquer regra correspondente será listado no `match` atributo.
* A variável `action` determina se as regras tiveram o efeito de bloquear, permitir ou registrar.
* Se o WAF estiver licenciado e ativado, a variável `waf` O atributo listará todos os sinalizadores WAF (por exemplo, SQLI) que foram detectados, independentemente de os sinalizadores WAF terem sido listados em alguma regra. Isso é para fornecer insight sobre novas regras em potencial a serem declaradas.
* Se nenhuma regra declarada pelo cliente for correspondente e nenhuma regra waf for correspondente, a variável `rules` A propriedade estará em branco.

Como observado anteriormente, as correspondências de regras do WAF só aparecem nos registros CDN para erros e passagens de CDN, não para ocorrências.

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

## Regras de início recomendadas {#recommended-starter-rules}

Você pode copiar as regras recomendadas abaixo na sua `cdn.yaml` para começar. Comece no modo de log, analise seu tráfego e, quando satisfeito, altere para o modo de bloqueio. Talvez você queira modificar as regras com base nas características exclusivas do tráfego direto do seu site.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
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
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        matches: "author|publish"
      action:
        type: log
        wafFlags:
          - SANS
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
    # Disable protection against CMDEXE on /bin (only works if WAF is licensed enabled for your environment)
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

## Tutorial {#tutorial}

[Trabalhar em um tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html) para obter conhecimento prático e experiência em torno das regras de filtro de tráfego.

O tutorial o guiará por:

* Definição do pipeline de configuração do Cloud Manager
* Uso de ferramentas para simular tráfego mal-intencionado
* Regras de filtro de tráfego declarativo, incluindo regras WAF
* Análise de resultados com ferramentas de painel
* Práticas recomendadas
