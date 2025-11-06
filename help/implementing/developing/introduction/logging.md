---
title: Logon no AEM as a Cloud Service
description: Saiba como usar o Logging para AEM as a Cloud Service a fim de configurar parâmetros globais para o serviço de log central, configurações específicas para os serviços individuais ou como solicitar o registro de dados.
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
feature: Log Files, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 2%

---

# Logon no AEM as a Cloud Service {#logging-for-aem-as-a-cloud-service}

O AEM as a Cloud Service é uma plataforma na qual os clientes incluem código personalizado para criar experiências exclusivas para sua base de clientes. Com isso em mente, o serviço de registro é uma função crítica para depurar e entender a execução de código em ambientes de desenvolvimento local e de nuvem, especialmente os ambientes de desenvolvimento do AEM as a Cloud Service.

As configurações de registro do AEM as a Cloud Service e os níveis de log são gerenciados em arquivos de configuração que são armazenados como parte do projeto do AEM no Git e implantados como parte do projeto do AEM por meio do Cloud Manager. O logon no AEM as a Cloud Service pode ser dividido em três conjuntos lógicos:

* Registro do AEM, que realiza o registro no nível do aplicativo do AEM
* Registro do Apache HTTPD Web Server/Dispatcher, que realiza o registro do servidor Web e do Dispatcher na camada Publicar.
* O registro em log da CDN, que, como seu nome indica, executa registros em log na CDN.

## Registro do AEM {#aem-logging}

O registro no nível do aplicativo AEM é feito por três registros:

1. Logs Java do AEM, que renderizam instruções de log Java para o aplicativo do AEM.
1. Logs de solicitação HTTP, que registram informações sobre solicitações HTTP e suas respostas fornecidas pelo AEM
1. Logs de acesso HTTP, que registram informações resumidas e solicitações HTTP atendidas pelo AEM

>[!NOTE]
>
>As solicitações HTTP atendidas pelo cache Dispatcher do nível de publicação ou pela CDN upstream não são refletidas nesses logs.

## Log Java do AEM {#aem-java-logging}

O AEM as a Cloud Service fornece acesso às instruções de log Java. Os desenvolvedores de aplicativos para o AEM devem seguir as práticas recomendadas gerais de registro em Java, registrando as instruções pertinentes sobre a execução do código personalizado, nos seguintes níveis de registro:

<table>
<tr>
<td>
<b>Ambiente AEM</b></td>
<td>
<b>Nível de log</b></td>
<td>
<b>Descrição</b></td>
<td>
<b>Disponibilidade da Instrução de Log</b></td>
</tr>
<tr>
<td>
Desenvolvimento</td>
<td>
DEPURAR</td>
<td>
Descreve o que está acontecendo no aplicativo.<br>
Quando o registro DEBUG está ativo, são registradas instruções que fornecem uma imagem clara de quais atividades ocorrem e quaisquer parâmetros-chave que afetam o processamento.</td>
<td>
<ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
</ul></td>
</tr>
<tr>
<td>
Fase</td>
<td>
AVISO</td>
<td>
Descreve condições que têm o potencial de se tornarem erros.<br>
Quando o registro de AVISO estiver ativo, somente as instruções que indicam condicionais que estão se aproximando da subotimização serão registradas.</td>
<td>
<ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
<li>Fase</li>
</ul></td>
</tr>
<tr>
<td>
Produção</td>
<td>
ERRO</td>
<td>
Descreve as condições que indicam uma falha e que precisam ser resolvidas.<br>
Quando o registro em log de ERRO estiver ativo, somente as instruções indicando falhas serão registradas. As instruções de log de ERROS indicam um problema grave que deve ser resolvido o mais rápido possível.</td>
<td>
<ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
<li>Fase</li>
<li>Produção</li>
</ul></td>
</tr>
</table>

Embora o registro em log do Java seja compatível com vários outros níveis de granularidade de registro, a AEM as a Cloud Service recomenda usar os três níveis descritos acima.

Os níveis de log do AEM são definidos por tipo de ambiente por meio da configuração do OSGi, que, por sua vez, é comprometida com o Git, e implantada pelo Cloud Manager na AEM as a Cloud Service. Por causa disso, é melhor manter as instruções de registro consistentes e bem conhecidas para tipos de ambiente, a fim de garantir que os registros disponíveis via AEM as Cloud Service estejam disponíveis no nível de registro ideal sem exigir a reimplantação do aplicativo com a configuração atualizada do nível de registro.

>[!NOTE]
>
>Para garantir o monitoramento eficaz dos ambientes do cliente, não altere o nível de log padrão. Além disso, não modifique o formato de log padrão. A saída do registro deve permanecer direcionada aos arquivos padrão. Consulte [a seção abaixo](#configuration-loggers) para obter diretrizes específicas.

**Exemplo de Saída de Log**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**Formato do Log**

<table>
<tbody>
<tr>
<td>Data e hora</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>ID do nó AEM as a Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>Nível de log</td>
<td>DEPURAR</td>
</tr>
<tr>
<td>Thread</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Classe Java</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>Mensagem de log</td>
<td>Nenhum aprovador especificado, padronizando para [ grupo de usuários Aprovadores do Creative ]</td>
</tr>
</tbody>
</table>

### Loggers de configuração {#configuration-loggers}

Os logs do Java da AEM são definidos como configuração OSGi e, portanto, têm como alvo ambientes AEM as a Cloud Service específicos usando pastas de modo de execução.

Configure o log Java para pacotes Java personalizados por meio de configurações OSGi para a fábrica do Sling LogManager. Há três propriedades de configuração compatíveis:

| Propriedade de configuração OSGi | Descrição |
|---|---|
| `org.apache.sling.commons.log.names` | Os pacotes Java para os quais coletar instruções de log. |
| `org.apache.sling.commons.log.level` | O nível de log no qual registrar os pacotes Java, especificado por `org.apache.sling.commons.log.names` |

A alteração de outras propriedades de configuração OSGi do LogManager pode resultar em problemas de disponibilidade no AEM as a Cloud Service.

Conforme observado em uma seção anterior, para garantir o monitoramento eficaz dos ambientes do cliente:

* O nível de log da configuração de log padrão do AEM (Configuração de log do Apache Sling) não deve ser modificado de seu valor padrão de &quot;INFO&quot;.
* É aceitável definir os níveis de log como DEBUG para pacotes individuais de código de produto (usando instâncias da fábrica de configuração OSGi &quot;Configuração do Apache Sling Logging Logger&quot;), mas usá-lo com moderação para evitar a degradação do desempenho e restaurar de volta para INFO quando não for mais necessário.
* É aceitável ajustar os níveis de log para o código desenvolvido pelo cliente.
* Todos os registros — tanto para código de produto do AEM quanto para código desenvolvido pelo cliente — devem manter o formato de registro padrão.
* A saída do log deve permanecer direcionada ao arquivo padrão &quot;logs/error.log&quot;.

Para esse fim, as alterações não devem ser feitas nas seguintes propriedades OSGi:

* **Configuração do Log do Apache Sling** (PID: `org.apache.sling.commons.log.LogManager`) — *todas as propriedades*
* **Configuração do Agente de Log do Apache Sling** (PID de Fábrica: `org.apache.sling.commons.log.LogManager.factory.config`):

   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

A seguir estão exemplos das configurações de log recomendadas (usando o pacote Java de espaço reservado `com.example`) para os três tipos de ambiente do AEM as a Cloud Service.

### Desenvolvimento {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.fatory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### Fase {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.fatory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### Produção {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.fatory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

## Log de solicitação HTTP do AEM {#aem-http-request-logging}

O registro de solicitações HTTP do AEM as a Cloud Service fornece ao insight as solicitações HTTP feitas ao AEM e suas respostas HTTP em ordem de tempo. Esse log é útil para entender as solicitações HTTP feitas ao AEM e a ordem em que são processadas e respondidas.

A chave para entender esse log é mapear a solicitação HTTP e os pares de resposta por suas IDs, indicadas pelo valor numérico entre parênteses. Muitas vezes, as solicitações e suas respostas correspondentes têm outras solicitações HTTP e respostas interjetadas entre elas no log.

**Log de Exemplo**

```
29/Apr/2020:19:14:21 +0000 [137] > POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] > GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**Formato do Log**

<table>
<tbody>
<tr>
<td>Data e hora</td>
<td>29/Abr/2020:19:14:21 +0000</td>
</tr>
<tr>
<td>ID do par de solicitação/resposta</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>Método HTTP</td>
<td>POST</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui-extension/metadataprofile/</td>
</tr>
<tr>
<td>Protocolo</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>ID do nó AEM as a Cloud Service</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Configuração do registro {#configuring-the-log}

O log de Solicitação HTTP do AEM não pode ser configurado no AEM as a Cloud Service.

## Log de acesso HTTP do AEM {#aem-http-access-logging}

O log de acesso HTTP do AEM as Cloud Service mostra as solicitações HTTP em ordem de tempo. Cada entrada de log representa a Solicitação HTTP que acessa o AEM.

Esse log é útil para entender rapidamente quais solicitações HTTP estão sendo feitas ao AEM, se elas são bem-sucedidas observando o código de status de resposta HTTP que as acompanha e quanto tempo a solicitação HTTP levou para ser concluída. Esse log também pode ser útil para depurar a atividade de um usuário específico filtrando entradas de log por Usuários.

**Exemplo de Saída de Log**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| ID do nó AEM as a Cloud Service | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| Endereço IP do cliente | - |
| Usuário | myuser@adobe.com |
| Data e hora | 30/abr/2020:17:37:14 +0000 |
| método HTTP | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| Protocolo | HTTP/1.1 |
| Status de resposta HTTP | 200 |
| Tamanho do corpo da resposta em bytes | 1141 |
| Referenciador | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| Agente do usuário | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### Configurar o log de acesso HTTP {#configuring-the-http-access-log}

O log de acesso HTTP não pode ser configurado no AEM as a Cloud Service.

## Apache Web Server e registro do Dispatcher {#apache-web-server-and-dispatcher-logging}

O AEM as a Cloud Service fornece três logs para os servidores Web Apache e a camada do Dispatcher na Publicação:

* Log de acesso ao servidor Web Apache HTTPD
* Log de erros do servidor Web Apache HTTPD
* Log do Dispatcher

Esses logs só estão disponíveis para o nível de Publicação.

Esse conjunto de logs fornece informações sobre solicitações HTTP para o nível de publicação do AEM as a Cloud Service antes que essas solicitações cheguem ao aplicativo do AEM. Isso é importante para entender, pois, idealmente, a maioria das solicitações HTTP para os servidores da camada Publicar é atendida pelo conteúdo que é armazenado em cache pelo Apache HTTPD Web Server e pelo AEM Dispatcher, e nunca chega ao próprio aplicativo do AEM. Portanto, não há instruções de log para essas solicitações nos logs Java, de solicitação ou de acesso da AEM.

### Log de acesso do servidor Web Apache HTTPD {#apache-httpd-web-server-access-log}

O log de acesso do Apache HTTP Web Server fornece instruções para cada solicitação HTTP que atinge o servidor Web/Dispatcher da camada de publicação. As solicitações atendidas de um CDN upstream não são refletidas nesses logs.

Consulte informações sobre o formato de log de erros na [documentação oficial do Apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

**Exemplo de Saída de Log**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**Formato do Log**

<table>
<tbody>
<tr>
<td>ID do nó do AEM as a Cloud Service</td>
<td>cm-p1234-e26813-aem-publish-5c787687c-lqlxr</td>
</tr>
<tr>
<td>Endereço IP do cliente</td>
<td>-</td>
</tr>
<tr>
<td>Usuário</td>
<td>-</td>
</tr>
<tr>
<td>Data e hora</td>
<td>01/maio/2020:00:09:46 +0000</td>
</tr>
<tr>
<td>Método HTTP</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/example.html</td>
</tr>
<tr>
<td>Protocolo</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>Status da resposta HTTP</td>
<td>200</td>
</tr>
<tr>
<td>Tamanho</td>
<td>310</td>
</tr>
<tr>
<td>Referenciador</td>
<td>-</td>
</tr>
<tr>
<td>Agente do usuário</td>
<td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### Configurar o log de acesso do servidor Web Apache HTTPD {#configuring-the-apache-httpd-webs-server-access-log}

Este log não pode ser configurado no AEM as a Cloud Service.

## Log de erros do servidor Web Apache HTTPD {#apache-httpd-web-server-error-log}

O log de erros do Apache HTTP Web Server fornece instruções para cada erro no servidor Web/Dispatcher da camada de publicação.

Consulte informações sobre o formato de log de erros na [documentação oficial do Apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

**Exemplo de Saída de Log**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**Formato do Log**

<table>
<tbody>
<tr>
<td>Data e hora</td>
<td>sexta-feira, 17 de julho de 2020:16:42.608913 2020</td>
</tr>
<tr>
<td>Nível do evento</td>
<td>[mpm_worker:notice]</td>
</tr>
<tr>
<td>ID do processo</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>Nome do pod</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>Mensagem</td>
<td>AH00094: Linha de comando: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### Configuração do log de erros do servidor Web Apache HTTPD {#configuring-the-apache-httpd-web-server-error-log}

Os níveis de log mod_rewrite são definidos pela variável REWRITE_LOG_LEVEL no arquivo `conf.d/variables/global.var`.

Pode ser definido como error, warn, info, debug e trace1 - trace8, com um valor padrão de warn. Para depurar as RewriteRules, é recomendável aumentar o nível de log para trace2. É recomendável depurar regras de regravação usando a [Dispatcher SDK](../../dispatcher/validation-debug.md). O nível máximo de log para o AEM as a Cloud Service é `debug`. Portanto, no momento, não é efetivamente possível depurar regras de regravação na nuvem.

Consulte a [documentação do módulo mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) para obter mais informações.

Para definir o nível de log por ambiente, use a ramificação condicional apropriada no arquivo global.var, conforme descrito abaixo:

```
Define REWRITE_LOG_LEVEL debug

<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL error
  ...
</IfDefine>
```

## Log do Dispatcher {#dispatcher-log}

**Exemplo**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

**Formato do Log**

<table>
<tbody>
<tr>
<td>Data e hora</td>
<td>[17/jul/2020:23:48:16 +0000]</td>
</tr>
<tr>
<td>Nome do pod</td>
<td>[cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr]</td>
</tr>
<tr>
<td>Protocolo</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Código de status de resposta do Dispatcher</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Duração</td>
<td>1949 ms</td>
</tr>
<tr>
<td>Farm</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>Status do cache</td>
<td>[ação ausente]</td>
</tr>
<tr>
<td>Host</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Configuração do registro de erros do Dispatcher {#configuring-the-dispatcher-error-log}

Os níveis de log do dispatcher são definidos pela variável DISP_LOG_LEVEL no arquivo `conf.d/variables/global.var`.

Ele pode ser definido como error, warn, info, debug e trace1, com um valor padrão de warn.

Embora o registro do Dispatcher seja compatível com vários outros níveis de granularidade de registro, a AEM as a Cloud Service recomenda usar os níveis descritos abaixo.

Para definir o nível de log por ambiente, use a ramificação condicional apropriada no arquivo `global.var`, conforme descrito abaixo:

```
Define DISP_LOG_LEVEL debug

<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL error
  ...
</IfDefine>
```

>[!NOTE]
>
>Para ambientes AEM as a Cloud Service, depurar é o nível máximo de detalhamento. O nível de log de rastreamento não é compatível, portanto, evite configurá-lo ao trabalhar em ambientes de nuvem.

## Log da CDN {#cdn-log}

O AEM as a Cloud Service fornece acesso a logs CDN, que são úteis para casos de uso, incluindo otimização da taxa de ocorrência do cache. O formato de log CDN não pode ser personalizado e não há conceito de configurá-lo para modos diferentes, como info, warn ou error.

**Exemplo**

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

**Formato do Log**

Os logs CDN são distintos dos outros logs no sentido de que seguem um formato json.

| **Nome do Campo** | **Descrição** |
|---|---|
| *carimbo de data/hora* | A hora em que a solicitação foi iniciada, após o término do TLS |
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
| *regras* | Os nomes de quaisquer [regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md) e sinalizadores WAF correspondentes, indicando também se a correspondência resultou em um bloqueio. Vazio se nenhuma regra for correspondente. |

Os logs CDN podem ser estendidos com suas próprias propriedades usando [transformações de solicitação/resposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#logproperty).

## Como acessar logs {#how-to-access-logs}

### Ambientes em nuvem {#cloud-environments}

Os logs do AEM as a Cloud Service para serviços em nuvem podem ser acessados baixando pela interface do Cloud Manager ou adaptando logs na linha de comando usando a interface de linha de comando do Adobe I/O. Para obter mais informações, consulte a [documentação de log do Cloud Manager](/help/implementing/cloud-manager/manage-logs.md).

### Logs para regiões de publicação adicionais {#logs-for-additional-publish-regions}

Se regiões de publicação adicionais estiverem habilitadas para um ambiente específico, os logs de cada região estarão disponíveis para download no Cloud Manager, conforme mencionado acima.

Os logs do AEM e os logs do Dispatcher para as regiões de publicação adicionais especificarão a região nas primeiras 3 letras após a ID de ambiente, como exemplificado por **nld2** na amostra abaixo, que se refere a uma instância de publicação adicional do AEM localizada na Holanda:

```
cm-p7613-e12700-nld2-aem-publish-bcbb77549-5qmmt 127.0.0.1 - 07/Nov/2023:23:57:11 +0000 "HEAD /libs/granite/security/currentuser.json HTTP/1.1" 200 - "-" "Java/11.0.19"
```

### SDK local {#local-sdk}

O AEM as a Cloud Service SDK fornece arquivos de registro para oferecer suporte ao desenvolvimento local.

Os logs do AEM estão localizados na pasta `crx-quickstart/logs`, onde os seguintes logs podem ser exibidos:

* Log Java do AEM: `error.log`
* Log de Solicitação HTTP do AEM: `request.log`
* Log de Acesso HTTP do AEM: `access.log`

Os logs da camada do Apache, incluindo o Dispatcher, estão no contêiner do Docker que contém o Dispatcher. Consulte a [documentação do Dispatcher](/help/implementing/dispatcher/disp-overview.md) para obter informações sobre como iniciar o Dispatcher.

Para recuperar os logs:

1. Na linha de comando, digite `docker ps` para listar seus contêineres
1. Para fazer logon no contêiner, digite &quot;`docker exec -it <container> /bin/sh`&quot;, onde `<container>` é a ID do contêiner do Dispatcher da etapa anterior
1. Navegar até a raiz do cache em `/mnt/var/www/html`
1. Os logs estão em `/etc/httpd/logs`
1. Inspecione os logs: eles podem ser acessados na pasta XYZ, onde os seguintes logs podem ser visualizados:
   * Log de acesso do servidor Web Apache HTTPD - `httpd_access.log`
   * Logs de erros do servidor Web Apache HTTPD - `httpd_error.log`
   * Logs do Dispatcher - `dispatcher.log`

Os logs também são impressos diretamente na saída do terminal. Na maioria das vezes, esses registros devem ser DEBUG, o que pode ser realizado passando o nível de Depuração como um parâmetro ao executar o Docker. Por exemplo:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Depuração da produção e do preparo {#debugging-production-and-stage}

Em circunstâncias excepcionais, os níveis de log precisam ser alterados para registrar em uma granularidade mais fina em ambientes de Preparo ou Produção.

Embora isso seja possível, requer alterações nos níveis de log nos arquivos de configuração no Git, de Aviso e Erro a Depuração, e realizar uma implantação no AEM as a Cloud Service para registrar essas alterações de configuração com os ambientes.

Dependendo do tráfego e da quantidade da instrução de log gravada pela Depuração, isso pode resultar em um impacto adverso no desempenho do ambiente. Portanto, recomenda-se que as alterações nos níveis de depuração de Preparo e Produção sejam:

* Feito de forma criteriosa e somente quando absolutamente necessário
* Revertido para os níveis apropriados e reimplantado o mais rápido possível

## Encaminhamento de logs {#log-forwarding}

Embora os logs possam ser baixados do Cloud Manager, algumas organizações acham útil encaminhá-los para um destino de registro preferencial. O AEM oferece suporte a logs de transmissão para os seguintes destinos:

* Armazenamento Azure Blob
* Datadog
* HTTPD
* Elasticsearch (e OpenSearch)
* Splunk

Consulte o [artigo sobre encaminhamento de logs](/help/implementing/developing/introduction/log-forwarding.md) para obter detalhes sobre como configurar esse recurso.

>[!NOTE]
>
>O encaminhamento de logs para ambientes de programas de sandbox não é compatível.
