---
title: Regras de filtro de tráfego, incluindo regras do WAF
description: Configuração das regras de filtro de tráfego, incluindo as regras do Web Application Firewall (WAF).
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
feature: Security
role: Admin
source-git-commit: 3a46db9c98fe634bf2d4cffd74b54771de748515
workflow-type: tm+mt
source-wordcount: '4582'
ht-degree: 1%

---


# Regras De Filtro De Tráfego, Incluindo Regras Do WAF {#traffic-filter-rules-including-waf-rules}

As regras de filtro de tráfego podem ser usadas para bloquear ou permitir solicitações na camada CDN, que pode ser útil em cenários como:

* Restrição do acesso a domínios específicos para tráfego interno da empresa, antes que um novo site entre em funcionamento
* Estabelecer limites de taxa para serem menos susceptíveis a ataques volumétricos de DoS
* Impedindo que endereços IP conhecidos como mal-intencionados direcionem suas páginas

Muitas dessas regras de filtro de tráfego estão disponíveis para todos os clientes do AEM as a Cloud Service Sites e do Forms. Chamadas de *regras padrão de filtro de tráfego*, elas operam principalmente em propriedades de solicitação e cabeçalhos de solicitação, incluindo IP, nome de host, caminho e agente de usuário. As regras padrão de filtro de tráfego incluem regras de limite de taxa para proteção contra picos de tráfego.

Uma subcategoria de regras de filtro de tráfego requer uma licença de Segurança aprimorada ou uma licença de Proteção WAF-DDoS. Essas regras poderosas são conhecidas como regras de filtro de tráfego do WAF (ou *regras do WAF*) e têm acesso aos [Sinalizadores do WAF](#waf-flags-list) descritos mais adiante neste artigo.

As regras de filtro de tráfego podem ser implantadas por meio de pipelines de configuração do Cloud Manager para tipos de ambiente de desenvolvimento, preparo e produção. O arquivo de configuração pode ser implantado em RDEs (Rapid Development Environments, ambientes de desenvolvimento rápido) usando ferramentas de linha de comando.

[Siga um tutorial](#tutorial) para criar rapidamente uma experiência concreta sobre esse recurso.

>[!NOTE]
>Para obter opções adicionais relacionadas à configuração do tráfego na CDN, incluindo edição da solicitação/resposta, declaração de redirecionamentos e proxy para uma origem que não seja da AEM, consulte o artigo [Configuração de Tráfego na CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md).


## Como este artigo está organizado {#how-organized}

Este artigo está organizado nas seguintes seções:

* **Visão geral da proteção de tráfego:** Saiba como você está protegido contra tráfego mal-intencionado.
* **Processo sugerido para configurar as regras:** Leia sobre uma metodologia de alto nível para proteger seu site.
* **Instalação:** descubra como configurar, configurar e implantar regras de filtro de tráfego, incluindo as regras avançadas do WAF.
* **Sintaxe de regras:** Leia sobre como declarar regras de filtro de tráfego no arquivo de configuração `cdn.yaml`. Isso inclui as regras de filtro de tráfego disponíveis para todos os clientes do Sites e do Forms e a subcategoria de regras do WAF para aqueles que licenciam esse recurso.
* **Exemplos de regras:** veja exemplos de regras declaradas para começar.
* **Regras de limite de taxa:** Saiba como usar regras de limitação de taxa para proteger seu site contra ataques de alto volume.
* **Alertas de Regras de Filtro de Tráfego** Configure os alertas para serem notificados quando as regras forem acionadas.
* **Pico de tráfego padrão no Alerta de Origem** Receba notificações quando houver um pico de tráfego na origem que sugira um ataque de DDoS.
* **Logs da CDN:** veja quais regras e Sinalizadores da WAF declarados correspondem ao seu tráfego.
* **Ferramentas do Painel:** Analise seus logs de CDN para criar novas regras de filtro de tráfego.
* **Regras de Início Recomendadas:** Um conjunto de regras para começar a usar.
* **Tutorial:** conhecimento prático sobre o recurso, incluindo como usar ferramentas do painel para declarar as regras certas.

## Visão geral da proteção de tráfego {#traffic-protection-overview}

No cenário digital atual, o tráfego mal-intencionado é uma ameaça constante. A Adobe reconhece a gravidade do risco e oferece várias abordagens para proteger os aplicativos do cliente e mitigar os ataques quando eles ocorrem.

Na borda, o Adobe Managed CDN absorve ataques de DoS na camada de rede (camadas 3 e 4), incluindo ataques de inundação e de reflexão/amplificação.

Por padrão, o Adobe toma medidas para evitar a degradação do desempenho devido a picos de tráfego inesperadamente alto além de um determinado limite. Se houver um ataque de DoS que afete a disponibilidade do site, as equipes de operações da Adobe serão alertadas e tomarão medidas para atenuar o problema.

Os clientes podem tomar medidas proativas para atenuar os ataques à camada do aplicativo (camada 7), configurando regras em várias camadas do fluxo de entrega de conteúdo.

Por exemplo, na camada do Apache, os clientes podem configurar o [módulo do Dispatcher](https://experienceleague.adobe.com/pt-br/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-access-to-content-filter) ou o [ModSecurity](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection) para limitar o acesso a determinado conteúdo.

Como este artigo descreve, as regras de filtro de tráfego podem ser implantadas na CDN Gerenciada pela Adobe, usando os [pipelines de configuração](/help/operations/config-pipeline.md) da Cloud Manager. Além das *regras padrão de filtro de tráfego* baseadas em propriedades como endereço IP, caminho e cabeçalhos ou regras baseadas na definição de limites de taxa, os clientes também podem licenciar uma subcategoria poderosa de regras de filtro de tráfego chamada *regras do WAF*.

## Processo sugerido {#suggested-process}

Veja a seguir um processo completo recomendado de alto nível para criar as regras certas de filtro de tráfego:

1. Configure pipelines de configuração de não produção e produção, conforme descrito na seção [Configuração](#setup).
1. Os clientes que licenciaram as *regras de filtro de tráfego do WAF* devem habilitá-los no Cloud Manager.
1. Leia e experimente o tutorial para entender concretamente como usar as regras de filtro de tráfego, incluindo as regras do WAF, se elas tiverem sido licenciadas. O tutorial o orienta pela implantação de regras em um ambiente de desenvolvimento, simulando tráfego mal-intencionado, baixando os [logs de CDN](#cdn-logs) e analisando-os em [ferramentas de painel](#dashboard-tooling).
1. Copie as regras de início recomendadas para `cdn.yaml` e implante a configuração no ambiente de produção, com algumas das regras no modo de log.
1. Depois de coletar algum tráfego, analise os resultados usando a [ferramenta de painel](#dashboard-tooling) para ver se há correspondências. Procure falsos positivos e faça os ajustes necessários, ativando todas as regras iniciais no modo de bloco.
1. Se necessário, adicione regras personalizadas com base na análise dos logs de CDN, primeiro testando com tráfego simulado em ambientes de desenvolvimento antes de implantar em ambientes de preparo e produção no modo de log, e depois no modo de bloco.
1. Monitorar o tráfego continuamente, alterando as regras à medida que o cenário de ameaças evolui.

## Configurar {#setup}

1. Crie um arquivo `cdn.yaml` com um conjunto de regras de filtro de tráfego, incluindo regras WAF. Por exemplo:

   ```
   kind: "CDN"
   version: "1"
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

   Consulte [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#common-syntax) para obter uma descrição das propriedades acima do nó `data`. O valor da propriedade `kind` deve ser definido como *CDN* e a versão, como `1`.


1. Se as regras do WAF estiverem licenciadas, você deverá ativar o recurso no Cloud Manager, conforme descrito abaixo, para os cenários de programa novo e existente.

   1. Para configurar o WAF em um novo programa, marque a caixa de seleção **Proteção do WAF-DDOS** na guia **Segurança** ao [adicionar um programa de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

   1. Para configurar o WAF em um programa existente, [edite seu programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) e, na guia **Segurança**, desmarque ou marque a opção **WAF-DDOS** a qualquer momento.

1. Crie um pipeline de configuração no Cloud Manager, conforme descrito no [artigo sobre configuração de pipeline](/help/operations/config-pipeline.md#managing-in-cloud-manager). O pipeline referenciará uma pasta `config` de nível superior com o arquivo `cdn.yaml` colocado em algum lugar abaixo, consulte [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#folder-structure).

## Sintaxe das regras de filtro de tráfego {#rules-syntax}

Você pode configurar *regras de filtro de tráfego* para corresponder a padrões como IPs, agente de usuário, cabeçalhos de solicitação, nome do host, localização geográfica e url.

Os clientes que licenciam a oferta de Segurança aprimorada ou Segurança de proteção WAF-DDoS também podem configurar uma categoria especial de regras de filtro de tráfego chamada *regras de filtro de tráfego do WAF* (ou *regras do WAF*) que fazem referência a um ou mais [sinalizadores do WAF](#waf-flags-list).

Este é um exemplo de um conjunto de regras de filtro de tráfego, que também inclui uma regra WAF.

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

O formato das regras de filtro de tráfego no arquivo `cdn.yaml` está descrito abaixo. Veja alguns [outros exemplos](#examples) em uma seção posterior e uma seção separada sobre [Regras de Limite de Taxa](#rate-limit-rules).


| **Propriedade** | **Maioria das regras de filtro de tráfego** | **Regras de filtro de tráfego do WAF** | **Tipo** | **Valor padrão** | **Descrição** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Nome da regra (64 caracteres de comprimento, pode conter apenas alfanuméricos e - ) |
| quando | X | X | `Condition` | - | A estrutura básica é:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[Consulte a sintaxe de Estrutura de Condição](#condition-structure) abaixo, que descreve os getters, predicados e como combinar várias condições. |
| ação | X | X | `Action` | log | objeto log, allow, block ou Action. O padrão é log |
| rateLimit | X |   | `RateLimit` | não definido | Configuração de limitação de taxa. A limitação de taxa está desabilitada se não estiver definida.<br><br>Há uma seção separada mais abaixo descrevendo a sintaxe rateLimit, juntamente com exemplos. |

### Estrutura de condição {#condition-structure}

Uma Condição pode ser uma Condição simples ou um grupo de Condições.

**Condição simples**

Uma Condição simples é composta por um getter e um predicado.

```
{ <getter>: <value>, <predicate>: <value> }
```

**Agrupar Condições**

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
| **todosDe** | `array[Condition]` | Operação **and**. true se todas as condições listadas retornarem true |
| **anyOf** | `array[Condition]` | Operação **or**. true se qualquer uma das condições listadas retornar true |

**Getter**

| **Propriedade** | **Tipo** | **Descrição** |
|---|---|---|
| reqProperty | `string` | Propriedade de solicitação.<br><br>Um de:<br><ul><li>`path`: Retorna o caminho completo de uma URL sem os parâmetros de consulta. (use `pathRaw` para a variante sem escape)</li><li>`url`: Retorna a URL completa, incluindo os parâmetros de consulta. (use `urlRaw` para a variante sem escape)</li><li>`queryString`: Retorna a parte da consulta de uma URL</li><li>`method`: retorna o método HTTP usado na solicitação.</li><li>`tier`: Retorna um de `author`, `preview` ou `publish`.</li><li>`domain`: retorna a propriedade de domínio (conforme definido no cabeçalho `Host`) em minúsculas</li><li>`clientIp`: Retorna o IP do cliente.</li><li>`forwardedDomain`: retorna o primeiro domínio definido no cabeçalho `X-Forwarded-Host` em minúsculas</li><li>`forwardedIp`: retorna o primeiro IP no cabeçalho `X-Forwarded-For`.</li><li>`clientRegion`: Retorna o código de subdivisão do país que identifica a região em que o cliente está localizado, conforme descrito em [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2).</li><li>`clientCountry`: retorna um código de duas letras ([Símbolo de indicador regional](https://en.wikipedia.org/wiki/Regional_indicator_symbol)) que identifica o país em que o cliente está localizado.</li><li>`clientContinent`: Retorna um código de duas letras (AF, AN, AS, EU, NA, OC, SA) que identifica em qual continente o cliente está localizado.</li><li>`clientAsNumber`: Retorna o número [Sistema Autônomo](https://en.wikipedia.org/wiki/Autonomous_system_(Internet)) associado ao IP do cliente.</li><li>`clientAsName`: Retorna o nome associado ao número do Sistema Autônomo.</li></ul> |
| reqHeader | `string` | Retorna o cabeçalho da solicitação com o nome especificado |
| queryParam | `string` | Retorna o parâmetro de consulta com o nome especificado |
| reqCookie | `string` | Retorna o cookie com o nome especificado |
| postParam | `string` | Retorna o parâmetro Post com o nome especificado do corpo da Solicitação. Funciona somente quando o corpo é do tipo de conteúdo `application/x-www-form-urlencoded` |

**Predicado**

| **Propriedade** | **Tipo** | **Significado** |
|---|---|---|
| **é igual a** | `string` | true se o resultado de getter for igual ao valor fornecido |
| **nãoIgual** | `string` | true se o resultado de getter não for igual ao valor fornecido |
| **curtir** | `string` | true se o resultado de getter corresponder ao padrão fornecido |
| **nãoCurtir** | `string` | true se o resultado de getter não corresponder ao padrão fornecido |
| **correspondências** | `string` | true se o resultado de getter corresponder ao regex fornecido |
| **nãoCorresponde** | `string` | true se o resultado de getter não corresponder ao regex fornecido |
| **em** | `array[string]` | true se a lista fornecida contiver o resultado getter |
| **nãoEm** | `array[string]` | true se a lista fornecida não contiver o resultado getter |
| **existe** | `boolean` | verdadeiro quando definido como verdadeiro e a propriedade existe ou quando definido como falso e a propriedade não existe |

**Notas**

* A propriedade de solicitação `clientIp` só pode ser usada com os seguintes predicados: `equals`, `doesNotEqual`, `in`, `notIn`. `clientIp` também pode ser comparado a intervalos IP ao usar os predicados `in` e `notIn`. O exemplo a seguir implementa uma condição para avaliar se um IP de cliente está no intervalo de IP de 192.168.0.0/24 (então de 192.168.0.0 a 192.168.0.255):

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* A Adobe recomenda o uso do [regex101](https://regex101.com/) e do [Fastly Fiddle](https://fiddle.fastly.dev/) ao trabalhar com o regex. Você também pode saber mais sobre como o Fastly lida com o regex no [fastly documentation - Regular expressions in Fastly VCL](https://www.fastly.com/documentation/reference/vcl/regex/#best-practices-and-common-mistakes).


### Estrutura de ação {#action-structure}

Um `action` pode ser uma cadeia de caracteres especificando a ação (permitir, bloquear ou registrar) ou um objeto composto do tipo de ação (permitir, bloquear ou registrar) e opções como wafFlags e/ou status.

**Tipos de ação**

As ações são priorizadas de acordo com seus tipos na tabela a seguir, que é ordenada para refletir a ordem em que as ações são executadas:

| **Nome** | **Propriedades permitidas** | **Significado** |
|---|---|---|
| **permitir** | `wafFlags` (opcional), `alert` (opcional) | se wafFlags não estiver presente, o interromperá o processamento de regras e continuará a fornecer a resposta. Se wafFlags estiver presente, isso desativará as proteções especificadas do WAF e continuará o processamento de regras. <br>Se um alerta for especificado, uma notificação da Central de Ações será enviada se a regra for acionada 10 vezes em uma janela de 5 minutos. Quando um alerta for acionado para uma regra específica, ele não será acionado novamente até o dia seguinte (UTC). |
| **bloco** | `status, wafFlags` (opcional e mutuamente exclusivo), `alert` (opcional) | se wafFlags não estiver presente, retorna o erro HTTP ignorando todas as outras propriedades, o código de erro é definido pela propriedade de status ou o padrão é 406. Se wafFlags estiver presente, ele ativará as proteções especificadas do WAF e continuará o processamento de regras. <br>Se um alerta for especificado, uma notificação da Central de Ações será enviada se a regra for acionada 10 vezes em uma janela de 5 minutos. Quando um alerta for acionado para uma regra específica, ele não será acionado novamente até o dia seguinte (UTC). |
| **log** | `wafFlags` (opcional), `alert` (opcional) | registra o fato de que a regra foi acionada, caso contrário, não afeta o processamento. wafFlags não tem efeito. <br>Se um alerta for especificado, uma notificação da Central de Ações será enviada se a regra for acionada 10 vezes em uma janela de 5 minutos. Quando um alerta for acionado para uma regra específica, ele não será acionado novamente até o dia seguinte (UTC). |

### Lista de sinalizadores do WAF {#waf-flags-list}

A propriedade `wafFlags`, que pode ser usada nas regras de filtro de tráfego licenciáveis do WAF, pode fazer referência ao seguinte:

#### Tráfego mal-intencionado

| **ID do sinalizador** | **Nome do sinalizador** | **Descrição** |
|---|---|---|
| ATAQUE | Ataque | Um agregado de sinalizadores relacionados ao tráfego mal-intencionado (SQLI, CMDEXE, XSS etc.). Consulte a [seção de regras recomendadas do WAF](#recommended-waf-starter-rules) para saber como esse sinalizador pode ser usado com eficiência. |
| ATAQUE DE IP INVÁLIDO | Ataque de IP incorreto | Semelhante ao sinalizador ATTACK, mas &quot;logicamente AND-ed&quot; com o sinalizador `BAD-IP`, para que uma solicitação seja sinalizada se corresponder a ATTACK e BAD-IP. Consulte a [seção de regras recomendadas do WAF](#recommended-waf-starter-rules) para saber como esse sinalizador pode ser usado com eficiência. |
| SQLI | Injeção de SQL | A Injeção de SQL é a tentativa de obter acesso a um aplicativo ou obter informações privilegiadas executando consultas arbitrárias ao banco de dados. |
| BACKDOOR | Backdoor | Um sinal backdoor é uma solicitação que tenta determinar se um arquivo backdoor comum está presente no sistema. |
| CMDEXE | Execução de comando | Execução de Comando é a tentativa de obter controle ou danificar um sistema alvo através de comandos arbitrários do sistema por meio da entrada do usuário. |
| CMDEXE-NO-BIN | Execução de Comando exceto em `/bin/` | Forneça o mesmo nível de proteção que `CMDEXE` ao desabilitar o falso-positivo em `/bin` devido à arquitetura do AEM. |
| XSS | Criação de script entre sites | Cross-Site Scripting é a tentativa de sequestrar a conta de um usuário ou a sessão de navegação na Web por meio de um código JavaScript mal-intencionado. |
| PASSAGEM | Diretório de passagem | O Diretory Traversal é a tentativa de navegar pelas pastas privilegiadas em todo o sistema, na esperança de obter informações confidenciais. |
| USERAGENT | Ferramentas de ataque | Ferramentas de ataque é o uso de software automatizado para identificar vulnerabilidades de segurança ou para tentar explorar uma vulnerabilidade detectada. |
| LOG4J-JNDI | Log4J JNDI | Os ataques de JNDI do Log4J tentam explorar a [vulnerabilidade do Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente nas versões do Log4J anteriores à 2.16.0 |
| CVE | CVE | Sinalizador para identificar um CVE. É sempre combinado com um sinalizador `CVE-<CVE Number>`. Entre em contato com o Adobe para saber mais sobre quais CVEs o Adobe protegerá. |

#### Tráfego suspeito

| **ID do sinalizador** | **Nome do sinalizador** | **Descrição** |
|---|---|---|
| ANORMALPATH | Caminho anormal | Caminho Anormal indica que o caminho original difere do caminho normalizado (por exemplo, `/foo/./bar` está normalizado para `/foo/bar`) |
| IP INCORRETO | IP inválido | Identifica solicitações originadas de endereços IP conhecidos por serem mal-intencionados, seja devido à inclusão em conjuntos de dados como `SANS` e `TORNODE`, ou com base na detecção prévia de comportamento mal-intencionado pelo WAF |
| BHH | Cabeçalhos de salto inválidos | Os cabeçalhos de salto inválido indicam uma tentativa de contrabando de HTTP por meio de um cabeçalho TE (Transferir Codificação) ou CL (Conteúdo Comprimento) malformado, ou um cabeçalho TE e CL bem formado |
| CODEINJECTION | Injeção de código | Injeção de código é a tentativa de obter controle ou danificar um sistema de destino através de comandos de código de aplicação arbitrários pela entrada do usuário. |
| COMPACTADO | Compactação detectada | O corpo da solicitação POST está compactado e não pode ser inspecionado. Por exemplo, se um cabeçalho de solicitação `Content-Encoding: gzip` for especificado e o corpo POST não for texto simples. |
| RESPONSESPLIT | Divisão de resposta HTTP | Identifica quando os caracteres CRLF são enviados como entrada para o aplicativo para inserir cabeçalhos na resposta HTTP |
| NOTUTF8 | Codificação inválida | Codificação inválida pode fazer com que o servidor traduza caracteres mal-intencionados de uma solicitação em uma resposta, causando uma negação de serviço ou XSS |
| DADOS MALFORMADOS | Dados malformados no corpo da solicitação | Um corpo de solicitação POST, PUT ou PATCH que esteja malformado de acordo com o cabeçalho de solicitação &quot;Content-Type&quot;. Por exemplo, se um cabeçalho de solicitação &quot;Content-Type: application/x-www-form-urlencoded&quot; for especificado e contiver um corpo POST que seja json. Isso geralmente é um erro de programação, uma solicitação automatizada ou mal-intencionada. Exige o agente 3.2 ou superior. |
| SANS | Tráfego IP mal-intencionado | [Lista do SANS Internet Storm Center](https://isc.sans.edu/) de endereços IP relatados que realizaram atividades mal-intencionadas. |
| NO-CONTENT-TYPE | Cabeçalho da solicitação &quot;Content-Type&quot; ausente | Uma solicitação POST, PUT ou PATCH que não tem um cabeçalho de solicitação &quot;Content-Type&quot;. Por padrão, os servidores de aplicativos devem assumir &quot;Content-Type: text/plain; charset=us-ascii&quot; neste caso. Muitas solicitações automatizadas e mal-intencionadas podem estar sem &quot;Tipo de conteúdo&quot;. |
| NOUA | Nenhum agente de usuário | Indica que uma solicitação não continha o cabeçalho &quot;User-Agent&quot; ou que o valor do cabeçalho não foi definido. |
| NULLBYTE | Byte nulo | Bytes nulos normalmente não aparecem em uma solicitação e indicam que a solicitação está malformada e é potencialmente maliciosa. |
| OOB-DOMAIN | Domínio Fora de Banda | Domínios fora de banda geralmente são usados durante testes de penetração para identificar vulnerabilidades nas quais o acesso à rede é permitido. |
| ARQUIVOPRIVADO | Arquivos privados | Os arquivos privados têm natureza confidencial, como um arquivo `.htaccess` do Apache, ou um arquivo de configuração que poderia vazar informações confidenciais |
| SCANNER | Scanner | Identifica ferramentas e serviços de digitalização populares |

#### Tráfego diverso

| **ID do sinalizador** | **Nome do sinalizador** | **Descrição** |
|---|---|---|
| DATA CENTER | Data center | Identifica a solicitação como proveniente de um provedor de hospedagem conhecido. Esse tipo de tráfego geralmente não é associado a um usuário final real. |
| CODIFICAÇÃODUPLA | Codificação dupla | A Codificação dupla verifica a técnica de evasão de caracteres html de codificação dupla |
| ERRO JSON | Erro de codificação JSON | Um corpo de solicitação POST, PUT ou PATCH especificado como contendo JSON no cabeçalho de solicitação &quot;Content-Type&quot;, mas que contém erros de análise JSON. Isso geralmente está relacionado a um erro de programação ou a uma solicitação automatizada ou mal-intencionada. |
| TORNODE | Tráfego Tor | Tor é um software que oculta a identidade de um usuário. Um pico no tráfego Tor pode indicar um invasor tentando mascarar sua localização. |
| XML-ERROR | Erro de codificação de XML | Um corpo de solicitação POST, PUT ou PATCH especificado como contendo XML dentro do cabeçalho de solicitação &quot;Content-Type&quot;, mas que contém erros de análise XML. Isso geralmente está relacionado a um erro de programação ou a uma solicitação automatizada ou mal-intencionada. |

## Considerações {#considerations}

* Quando duas regras conflitantes são criadas, as regras permitidas sempre têm prioridade sobre as regras de bloqueio. Por exemplo, se você criar uma regra para bloquear um caminho específico e uma regra para permitir um endereço IP específico, as solicitações desse endereço IP no caminho bloqueado serão permitidas.

* Se uma regra for correspondente e bloqueada, o CDN responderá com um código de retorno `406`.

* Os arquivos de configuração não devem conter segredos, pois eles podem ser lidos por qualquer pessoa com acesso ao repositório Git.

* As incluis na lista de permissões de IP definidas no Cloud Manager têm prioridade sobre as Regras de filtros de tráfego.

* As correspondências de regras do WAF só aparecem nos logs CDN para erros e passagens de CDN, não para ocorrências.

## Exemplos de regras {#examples}

Alguns exemplos de regras se seguem. Consulte a [seção limite de taxa](#rate-limit-rules) mais abaixo para obter exemplos de regras de limite de taxa.

**Exemplo 1**

Esta regra bloqueia solicitações provenientes de **IP192.168.1.1**:

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**Exemplo 2**

Esta regra bloqueia a solicitação no caminho `/helloworld` na publicação com um usuário-agente que contenha Chrome:

```
kind: "CDN"
version: "1"
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

Esta regra bloqueia solicitações na publicação que contêm o parâmetro de consulta `foo`, mas permite todas as solicitações provenientes do IP 192.168.1.1:

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when:
          allOf:
            - { queryParam: url-param, equals: foo }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**Exemplo 4**

Esta regra bloqueia solicitações para o caminho `/block-me` na publicação e bloqueia todas as solicitações que correspondam a um padrão `SQLI` ou `XSS`. Este exemplo inclui regras de filtro de tráfego do WAF, que faz referência aos `SQLI` e `XSS` [Sinalizadores do WAF](#waf-flags-list) e, portanto, requer uma licença separada.

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
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

## Regras de limite de taxa

Às vezes, é desejável bloquear o tráfego se ele exceder uma determinada taxa de solicitações recebidas, com base em uma condição específica. A definição de um valor para a propriedade `rateLimit` limita a taxa dessas solicitações que correspondem à condição da regra.

As regras de limite de taxa não podem fazer referência aos sinalizadores do WAF. Eles estão disponíveis para todos os clientes do Sites e do Forms.

Os limites de taxa são calculados por CDN POP. Como exemplo, suponha que os POPs em Montreal, Miami e Dublin tenham taxas de tráfego de 80, 90 e 120 solicitações por segundo, respectivamente. E a regra de limite de taxa é definida como um limite 100. Nesse caso, apenas o tráfego com destino a Dublim seria limitado em termos tarifários.

Os limites de taxa são avaliados com base no tráfego que atinge a borda, no tráfego que atinge a origem ou no número de erros.

### Estrutura rateLimit {#ratelimit-structure}

| **Propriedade** | **Tipo** | **Padrão** | **SIGNIFICADO** |
|---|---|---|---|
| limite | número inteiro de 10 a 10000 | obrigatório | Taxa de solicitações (por CDN POP) em solicitações por segundo para as quais a regra é acionada. |
| janela | enumeração de inteiros: 1, 10 ou 60 | 10 | Janela de amostragem em segundos para a qual a taxa de solicitação é calculada. A precisão dos contadores depende do tamanho da janela (maior precisão da janela). Por exemplo, pode-se esperar 50% de precisão para a janela de 1 segundo e 90% de precisão para a janela de 60 segundos. |
| penalidade | número inteiro de 60 a 3600 | 300 (5 minutos) | Um período em segundos para o qual as solicitações correspondentes são bloqueadas (arredondado para o minuto mais próximo). |
| contagem | tudo, buscas, erros | todas | avalie com base no tráfego de borda (todos), no tráfego de origem (buscas) ou no número de erros (erros). |
| groupBy | matriz[Getter] | nenhum | o contador do limitador de taxa será agregado por um conjunto de propriedades de solicitação (por exemplo, clientIp). |

### Exemplos {#ratelimiting-examples}

**Exemplo 1**

Essa regra bloqueia um cliente por 5 milissegundos quando ele excede uma média de 60 solic./seg (por POP CDN) nos últimos 10 segundos:

```
kind: "CDN"
version: "1"
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
        count: all
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Exemplo 2**

Bloqueie solicitações no caminho /crítico/recurso por 60 segundos quando exceder uma média de 100 solicitações de origem por segundo (por POP CDN) em uma janela de tempo de dez segundos:

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when:
          allOf:
            - { reqProperty: path, equals: /critical/resource }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
        rateLimit: { limit: 100, window: 10, penalty: 60, count: fetches }
```

## Regras CVE {#cve-rules}

Se o WAF for licenciado, a Adobe aplicará automaticamente regras de bloqueio para proteger contra muitos CVEs (vulnerabilidades e exposições comuns) conhecidos, e novos CVEs poderão ser adicionados logo após serem detectados. Os clientes não devem e não precisam configurar as regras CVE sozinhos.

Se uma solicitação de tráfego corresponder a um CVE, ela aparecerá na entrada de log CDN correspondente.

Entre em contato com o suporte da Adobe se houver dúvidas sobre um CVE específico ou se houver uma regra CVE específica que sua organização deseja desativar.

## Alertas de regras de filtro de tráfego {#traffic-filter-rules-alerts}

Uma regra pode ser configurada para enviar uma notificação da Central de Ações se for acionada dez vezes em uma janela de 5 minutos. Essa regra alerta quando determinados padrões de tráfego ocorrem, para que você possa tomar as medidas necessárias. Quando um alerta for acionado para uma regra específica, ele não será acionado novamente até o dia seguinte (UTC).

Saiba mais sobre o [Centro de Ações](/help/operations/actions-center.md), incluindo como configurar os Perfis de Notificação necessários para receber emails.

![Notificação da Central de Ações](/help/security/assets/traffic-filter-rules-actions-center-alert.png)


A propriedade alert pode ser aplicada ao nó action para todos os tipos de ação (allow, block, log).

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
          alert: true
```

## Alerta de pico de tráfego padrão no Origin {#traffic-spike-at-origin-alert}

Uma notificação por email do [Centro de Ações](/help/operations/actions-center.md) será enviada quando houver uma quantidade significativa de tráfego enviado à origem, onde um alto limite de solicitações vem do mesmo endereço IP, sugerindo assim um ataque de DDoS.

Se esse limite for atingido, o Adobe bloqueará o tráfego desse endereço IP, mas é recomendável tomar medidas adicionais para proteger sua origem, incluindo a configuração das regras de filtro de tráfego de limite de taxa para bloquear picos de tráfego em limites mais baixos. Consulte o [tutorial Bloqueando ataques de DoS e DDoS usando regras de tráfego](#tutorial-blocking-DDoS-with-rules) para obter uma apresentação guiada.

Este alerta é habilitado por padrão, mas pode ser desabilitado usando a propriedade *defaultTrafficAlerts*, definida como false. Quando o alerta for acionado, ele não será disparado novamente até o dia seguinte (UTC).

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
   defaultTrafficAlerts: false
```

## Logs CDN {#cdn-logs}

O AEM as a Cloud Service fornece acesso aos logs CDN, que são úteis para casos de uso, incluindo otimização da taxa de ocorrência do cache e configuração das regras de filtro de tráfego. Os logs de CDN aparecem na caixa de diálogo **Baixar Logs** do Cloud Manager, ao selecionar o serviço Autor ou Publicar.

Os logs do CDN podem ser atrasados em até cinco minutos.

A propriedade `rules` descreve quais regras de filtro de tráfego são correspondidas e tem o seguinte padrão:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Por exemplo:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

As regras se comportam da seguinte maneira:

* O nome de regra declarado pelo cliente de qualquer regra correspondente está listado no atributo `match`.
* O atributo `action` determina se as regras bloqueiam, permitem ou registram em log.
* Se o WAF estiver licenciado e habilitado, o atributo `waf` listará todos os sinalizadores do WAF (por exemplo, SQLI) que foram detectados. Isso é verdadeiro independentemente de os sinalizadores do WAF terem sido listados em alguma regra. Isso é para fornecer o insight em novas regras em potencial a serem declaradas.
* Se nenhuma regra declarada pelo cliente for correspondente e nenhuma regra waf for correspondente, a propriedade `rules` ficará em branco.

Como observado anteriormente, as correspondências de regras do WAF só aparecem nos logs CDN para erros e passagens de CDN, não para ocorrências.

O exemplo abaixo mostra um exemplo `cdn.yaml` e duas entradas de log CDN:


```
kind: "CDN"
version: "1"
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

| **Nome do Campo** | **Descrição** |
|---|---|
| *carimbo de data/hora* | A hora em que a solicitação foi iniciada, após o término do TLS. |
| *ttfb* | Abreviação de *Tempo até o Primeiro Byte*. O intervalo de tempo entre a solicitação iniciada até o ponto antes do corpo da resposta começar a ser transmitido. |
| *cli_ip* | O endereço IP do cliente. |
| *cli_country* | Código de país alfa-2 de duas letras [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) para o país do cliente. |
| *grade* | O valor do cabeçalho da solicitação usado para identificar exclusivamente a solicitação. |
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

O Adobe fornece um mecanismo para baixar ferramentas de painel no computador a fim de assimilar logs CDN baixados por meio do Cloud Manager. Com essa ferramenta, você pode analisar seu tráfego para ajudar a criar as regras de filtro de tráfego apropriadas a serem declaradas, incluindo regras do WAF.

A ferramenta do painel pode ser clonada diretamente do [repositório GitHub AEMCS-CDN-Log-Analysis-Tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling).

[Um tutorial](#tutorial) está disponível para obter instruções concretas sobre como usar a ferramenta de painel.

## Regras iniciais recomendadas {#recommended-starter-rules}

A Adobe sugere começar com as regras de filtro de tráfego abaixo e, em seguida, refinar ao longo do tempo. As *Regras padrão* estão disponíveis com uma licença do Sites ou do Forms, enquanto as *regras do WAF* exigem uma licença de Segurança Aprimorada ou Proteção WAF-DDoS.

### Regras padrão recomendadas {#recommended-nonwaf-starter-rules}

Comece com estas regras:

1. limite de taxa (Modo Log):
   * registra quando o tráfego de um determinado IP excede um limite de taxa. Alterar para o modo de bloqueio após validar que nenhum alerta foi recebido; se alertas fossem recebidos, isso indicaria que o valor limite era muito baixo.
2. países específicos (Modo Bloco):
   * bloquear o tráfego de determinados países (modifique os códigos de país com base nos requisitos da empresa)

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds an average of 100 req/sec to origin on a time window of 10sec
    - name: limit-origin-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 100
        window: 10
        count: fetches
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    #  Block client for 5m when it exceeds an average of 500 req/sec on a time window of 10sec
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 500
        window: 10
        count: all
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
      alert: true
    # Block requests coming from OFAC countries
    - name: ofac-countries
      when:
        allOf:
          - { reqProperty: tier, in: ["author", "publish"] }
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

### Regras do WAF recomendadas {#recommended-waf-starter-rules}

Adicione as seguintes regras à configuração existente:

1. Sinalizador ATTACK-FROM-BAD-IP (modo de bloqueio):
   * Bloqueie imediatamente o tráfego que corresponde a padrões suspeitos (incluindo vários na [lista de sinalizadores do WAF](#waf-flags-list)) e que se origina de endereços IP conhecidos como mal-intencionados.
   * O sinalizador ATTACK-FROM-BAD-IP satisfaz inerentemente ambas as condições (correspondência de padrão e IP mal-intencionado conhecido), minimizando o risco de falsos positivos. Assim, você pode aplicar com segurança essa regra no modo de bloqueio imediatamente.
2. Sinalizador ATTACK (Modo de Log):
   * Registre inicialmente (em vez de bloquear) o tráfego que corresponde a padrões suspeitos, mas não se origina de endereços IP mal-intencionados conhecidos. Essa abordagem cuidadosa de registro em vez de bloqueio ajuda a evitar o bloqueio inadvertido do tráfego legítimo (falsos positivos).
   * Após implantar essa regra, analise cuidadosamente os logs CDN para verificar se as solicitações legítimas não estão sendo sinalizadas incorretamente. Depois de ter certeza de que nenhum tráfego legítimo será afetado, alterne para o modo de bloqueio.

>[!NOTE]
>
> Nossa experiência indica que falsos positivos associados à bandeira ATAQUE são raros. Portanto, pode ser uma estratégia prática bloquear imediatamente todo o tráfego suspeito, mesmo que o endereço IP não seja reconhecidamente mal-intencionado, e subsequentemente usar a análise de log da CDN para identificar e introduzir regras de permissão para tráfego legítimo. Cada organização deve avaliar sua própria tolerância ao risco, ponderando os benefícios de uma maior proteção contra o risco de bloquear inadvertidamente solicitações legítimas.

```
    # blocks likely attack traffic, which also comes from suspected IPs
    - name: attacks-from-bad-ips-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: block
        wafFlags:
          - ATTACK-FROM-BAD-IP
    # log likely attack traffic, and later switch to block mode if false positives aren't observed
    - name: attacks-from-any-ips-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - ATTACK
```

### Regras herdadas recomendadas do WAF {#previous-waf-starter-rules}

Antes de julho de 2025, a Adobe recomendou as regras do WAF listadas abaixo, que ainda são válidas e eficazes na defesa contra tráfego mal-intencionado. Consulte o tutorial para considerações sobre a migração para as novas regras recomendadas.

+++ Expanda para ver as regras herdadas recomendadas do WAF.

```
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - TRAVERSAL
          - CMDEXE-NO-BIN
          - XSS
          - LOG4J-JNDI
          - BACKDOOR
          - USERAGENT
          - SQLI
          - SANS
          - TORNODE
          - NOUA
          - SCANNER
          - PRIVATEFILE
          - NULLBYTE
```

+++

## Tutorial {#tutorial}

Trabalhe com [uma série de tutoriais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview) para obter conhecimento prático e experiência sobre regras de filtro de tráfego, incluindo regras do WAF.

Os tutoriais incluem:

* Uma visão geral das regras padrão e de filtro de tráfego do WAF
* Configuração das regras de filtro de tráfego padrão e WAF recomendadas para bloquear ataques, incluindo DoS (Negação de serviço) e outras ameaças
* Implantação de regras usando o pipeline de configuração do Cloud Manager
* Testar suas regras usando ferramentas para simular tráfego mal-intencionado
* Analisando resultados usando a Ferramenta de Análise de Log
* Práticas recomendadas
