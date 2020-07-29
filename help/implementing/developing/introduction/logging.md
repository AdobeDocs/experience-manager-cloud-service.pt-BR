---
title: Registro
description: Saiba como configurar parâmetros globais para o serviço de registro central, configurações específicas para os serviços individuais ou como solicitar registro de dados.
translation-type: tm+mt
source-git-commit: 68445e086aeae863520d14cb712f0cbebbffb5ab
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 3%

---


# Registro {#logging}

AEM como um Cloud Service é uma plataforma para os clientes incluírem código personalizado para criar experiências exclusivas para sua base de clientes. Com isso em mente, o registro em log é uma função essencial para depurar e entender a execução do código no desenvolvimento local, e ambientes em nuvem, especialmente o AEM como ambientes Cloud Service Dev.

Os níveis de registro e registro AEM são gerenciados em arquivos de configuração armazenados como parte do projeto AEM no Git e implantados como parte do projeto AEM pelo Cloud Manager. Fazer logon AEM como um Cloud Service pode ser dividido em dois conjuntos lógicos:

* AEM registro, que executa o registro em log no nível do aplicativo AEM
* Apache HTTPD Web Server/Dispatcher logging, que executa o log do servidor da Web e do Dispatcher na camada Publicar.

## Registro de AEM {#aem-loggin}

O registro no nível do aplicativo AEM é realizado por três registros:

1. AEM registros Java, que renderizam declarações de registro Java para o aplicativo AEM.
1. Registros de solicitação HTTP, que registram informações sobre solicitações HTTP e suas respostas fornecidas por AEM
1. Registros de acesso HTTP, que registram informações resumidas e solicitações HTTP fornecidas por AEM

Observe que as solicitações HTTP fornecidas pelo cache do Dispatcher da camada de publicação ou pelo CDN upstream não são refletidas nesses logs.

## AEM registro em Java {#aem-java-logging}

AEM como um Cloud Service fornece acesso às instruções do log Java Os desenvolvedores de aplicativos para AEM devem seguir as práticas recomendadas gerais de registro em Java, registrando declarações pertinentes sobre a execução do código personalizado, nos seguintes níveis de registro:

<table>
<tr>
<td>
<b>Ambiente AEM</b></td>
<td>
<b>Nível de registro</b></td>
<td>
<b>Descrição</b></td>
<td>
<b>Disponibilidade do demonstrativo de registro</b></td>
</tr>
<tr>
<td>
Desenvolvimento</td>
<td>
DEPURAR</td>
<td>
Descreve o que está acontecendo no aplicativo.<br>
Quando o registro DEBUG estiver ativo, as declarações que fornecem uma imagem clara do que ocorre com as atividades, bem como quaisquer parâmetros chave que afetam o processamento, são registradas em log.</td>
<td>
<ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
</ul></td>
</tr>
<tr>
<td>
Estágio</td>
<td>
AVISO</td>
<td>
Descreve as condições que podem se tornar erros.<br>
Quando o registro em log do WARN estiver ativo, somente as declarações indicando os condicionais que estão se aproximando da subotimização serão registradas.</td>
<td>
<ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
<li>Estágio</li>
</ul></td>
</tr>
<tr>
<td>
Produção</td>
<td>
ERRO</td>
<td>
Descreve as condições que indicam uma falha e que precisam ser resolvidas.<br>
Quando o registro em log ERROR está ativo, somente as declarações que indicam falhas são registradas em log. Declarações de log de ERROS indicam um problema grave que deve ser resolvido o mais rápido possível.</td>
<td>
<ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
<li>Estágio</li>
<li>Produção</li>
</ul></td>
</tr>
</table>

Embora o registro em log do Java suporte vários outros níveis de granularidade de registro em log, AEM como um Cloud Service recomenda o uso dos três níveis descritos acima.

Os níveis de registro de AEM são definidos por tipo de ambiente pela configuração OSGi, que por sua vez são comprometidos com Git, e implantados pelo Gerenciador de nuvem para AEM como Cloud Service. Por isso, é melhor manter as declarações de log consistentes e bem conhecidas para tipos de ambientes, para garantir que os registros disponíveis via AEM como Cloud Service estejam disponíveis no nível de log ideal sem a necessidade de reimplantação do aplicativo com a configuração atualizada do nível de log.

### Formato de registro {#log-format}

| Data e hora | AEM como uma ID de código de Cloud Service | Nível de registro | Thread | Classe Java | Mensagem de registro |
|---|---|---|---|---|---|
| 29.04.2020 21:50:13.398 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` | `*DEBUG*` | qtp2130572036-1472 | com.example.approval.workflow.impl.CustomApprovalWorkflow | `No specified approver, defaulting to [ Creative Approvers user group ]` |

**Exemplo de saída de registro**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

### Registradores de configuração {#configuration-loggers}

AEM logs Java são definidos como configuração OSGi e, portanto, AEM específicos do público alvo como ambientes de Cloud Service usando pastas de modo de execução.

Configure o registro java para pacotes Java personalizados por meio de configurações OSGi para a fábrica do Sling LogManager. Há duas propriedades de configuração compatíveis:

| Propriedade Configuração OSGi | Descrição |
|---|---|
| org.apache.sling.commons.log.names | Os pacotes Java para os quais coletar declarações de log. |
| org.apache.sling.commons.log.level | O nível de log no qual os pacotes Java serão registrados, especificado por org.apache.sling.commons.log.names |

Alterar outras propriedades de configuração do LogManager OSGi pode resultar em problemas de disponibilidade no AEM como Cloud Service.

A seguir estão exemplos das configurações de registro recomendadas (usando o pacote Java de espaço reservado `com.example`) para os três AEM como tipos de ambientes Cloud Service.

### Desenvolvimento {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.fatory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### Estágio {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.fatory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
}
```

### Produção {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.fatory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
}
```

## Registro de solicitação HTTP AEM {#aem-http-request-logging}

AEM como um Cloud Service de registro de solicitação HTTP fornece informações sobre as solicitações HTTP feitas para AEM suas respostas HTTP em tempo hábil. Esse log é útil para entender as Solicitações HTTP feitas para AEM e a ordem em que são processadas e respondidas.

A chave para entender esse log é mapear os pares de solicitação HTTP e resposta por suas IDs, denotadas pelo valor numérico entre colchetes. Observe que frequentemente as solicitações e suas respostas correspondentes têm outras solicitações HTTP e respostas interjetadas entre elas no log.

### Formato de registro {#http-request-logging-format}

| Data e hora | ID do Par de Solicitação/Resposta |  | Método HTTP | URL | Protocolo | AEM como uma ID de nó Cloud Service |
|---|---|---|---|---|---|---|
| 29/Abr/2020:19:14:21 +0000 | `[137]` | -> | POST | /conf/global/settings/dam/adminui-extension/metadataprofile/ | HTTP/1.1 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` |

**Exemplo de registro**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

### Configuração do registro {#configuring-the-log}

O registro de Solicitação HTTP AEM não é configurável em AEM como um Cloud Service.

## Registro de acesso HTTP AEM {#aem-http-access-logging}

AEM como registro de acesso HTTP Cloud Service mostra solicitações HTTP em ordem de tempo. Cada entrada de registro representa a Solicitação HTTP que acessa AEM.

Esse log é útil para entender rapidamente quais solicitações HTTP estão sendo feitas para AEM, se forem bem-sucedidas ao observar o código de status de resposta HTTP associado e quanto tempo a solicitação HTTP demorou para ser concluída. Esse log também pode ser útil para depurar uma atividade específica do usuário ao filtrar entradas de log por usuários.

### Formato de registro {#access-log-format}

| AEM como uma ID de nó Cloud Service | cm-p1234-e26813-aem-publish-5c787687c-lqlxr |
|---|---|
| Endereço IP do cliente | - |
| Usuário | myuser@adobe.com |
| Data e hora | 30/Abr/2020:17:37:14 +0000 |
| Método HTTP | GET |
| URL | /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css |
| Protocolo | HTTP/1.1 |
| Status de resposta HTTP | 200 |
| Tempo de solicitação HTTP em milissegundos | 1141 |
| Referenciador | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| Agente do usuário | &quot;Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, como Gecko) Chrome/81.0.4044.122 Safari/537.36&quot; |

**Exemplo**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

### Configuração do registro de acesso HTTP {#configuring-the-http-access-log}

O registro de Acesso HTTP não é configurável em AEM como um Cloud Service.

## Apache Web Server e Dispatcher Logging {#apache-web-server-and-dispatcher-logging}

AEM como Cloud Service, fornece três registros para os servidores Web Apache e a camada de despachante no Publish:

* Log de acesso do servidor Web Apache HTTPD
* Log de erro do servidor Web Apache HTTPD
* Log do Dispatcher

Observe que esses logs estão disponíveis somente para a camada de Publicação.

Esse conjunto de registros fornece insights sobre solicitações HTTP para o AEM como uma camada de publicação de Cloud Service antes que essas solicitações cheguem ao aplicativo AEM. Isso é importante para entender, já que, idealmente, a maioria das solicitações HTTP para os servidores da camada de publicação são atendidas por conteúdo armazenado em cache pelo Apache HTTPD Web Server e AEM Dispatcher, e nunca chegam ao aplicativo AEM. Portanto, não há declarações de log para essas solicitações nos registros AEM Java, Solicitação ou Acesso.

### Log de acesso do servidor Web Apache HTTPD {#apache-httpd-web-server-access-log}

O log de acesso do Apache HTTP Web Server fornece instruções para cada solicitação HTTP que chega ao servidor Web/Dispatcher da camada de publicação. Observe que as solicitações que são atendidas a partir de um CDN upstream não são refletidas nesses logs.

Consulte as informações sobre o formato do log de erros na documentação [do cache](https://httpd.apache.org/docs/2.4/logs.html#accesslog)oficial.

**Formato de registro**

<!--blank until prod build finishes-->

**Exemplo**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

### Configurando o log de acesso do servidor Web Apache HTTPD {#configuring-the-apache-httpd-webs-server-access-log}

Este registro não é configurável em AEM como um Cloud Service.

## Log de erros do Apache HTTPD Web Server {#apache-httpd-web-server-error-log}

O log de erros do Apache HTTP Web Server fornece instruções para cada erro no servidor Web/Dispatcher da camada de publicação.

Consulte as informações sobre o formato do log de erros na documentação [do cache](https://httpd.apache.org/docs/2.4/logs.html#errorlog)oficial.

**Formato de registro**

<!--placeholder-->

**Exemplo**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

### Configurando o registro de erros do servidor Web Apache HTTPD {#configuring-the-apache-httpd-web-server-error-log}

Os níveis de log mod_rewrite são definidos pela variável REWRITE_LOG_LEVEL no arquivo `conf.d/variables/global.var`.

Ele pode ser definido como Erro, Aviso, Informações, Depuração e Trace1 - Trace8, com um valor padrão de Aviso. Para depurar RewriteRules, é recomendável elevar o nível de log para Trace2.

Consulte a documentação [do módulo](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) mod_rewrite para obter mais informações.

Para definir o nível de log por ambiente, use a ramificação condicional apropriada no arquivo global.var, conforme descrito abaixo:

```
Define REWRITE_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL Error
  ...
</IfDefine>
```

## Log do Dispatcher {#dispatcher-log}

**Formato de registro**

