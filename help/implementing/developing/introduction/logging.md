---
title: Registro para AEM as a Cloud Service
description: Saiba como usar o Logging for AEM as a Cloud Service para configurar parâmetros globais para o serviço de log central, configurações específicas para os serviços individuais ou como solicitar o log de dados.
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
source-git-commit: 9e67b4f68fe450e80249c3959e3517c6cba3275d
workflow-type: tm+mt
source-wordcount: '2382'
ht-degree: 3%

---

# Registro para AEM as a Cloud Service {#logging-for-aem-as-a-cloud-service}

AEM as a Cloud Service é uma plataforma para clientes incluírem código personalizado para criar experiências exclusivas para a base de clientes. Com isso em mente, o serviço de registro é uma função essencial para depurar e entender a execução de código em ambientes de desenvolvimento local e em nuvem, especialmente os ambientes de desenvolvimento AEM as a Cloud Service.

AEM configurações de registro as a Cloud Service e níveis de log são gerenciados em arquivos de configuração que são armazenados como parte do projeto AEM no Git e implantados como parte do projeto AEM pelo Cloud Manager. O logon AEM as a Cloud Service pode ser dividido em dois conjuntos lógicos:

* Registro de AEM, que executa o registro em log no nível de aplicativo AEM
* Apache HTTPD Web Server/Dispatcher logging, que executa o log do servidor da Web e do Dispatcher na camada de Publicação.

## Registro de AEM {#aem-logging}

O registro no nível do aplicativo AEM é feito por três logs:

1. AEM logs Java, que renderizam instruções de registro Java para o aplicativo AEM.
1. Logs de solicitação HTTP, que registram informações sobre solicitações HTTP e suas respostas fornecidas por AEM
1. Logs de acesso HTTP, que registram informações resumidas e solicitações HTTP atendidas por AEM

>[!NOTE]
>
>As solicitações HTTP veiculadas a partir do cache do Dispatcher da camada de publicação ou do CDN upstream não são refletidas nesses logs.

## Registro do Java do AEM {#aem-java-logging}

AEM as a Cloud Service fornece acesso às instruções de log do Java. Os desenvolvedores de aplicativos para AEM devem seguir as práticas recomendadas gerais de registro em Java, registrando declarações pertinentes sobre a execução do código personalizado, nos seguintes níveis de log:

<table>
<tr>
<td>
<b>Ambiente AEM</b></td>
<td>
<b>Nível de registro</b></td>
<td>
<b>Descrição</b></td>
<td>
<b>Disponibilidade da Declaração de Log</b></td>
</tr>
<tr>
<td>
Desenvolvimento</td>
<td>
DEPURAR</td>
<td>
Descreve o que está acontecendo no aplicativo.<br>
Quando o log DEBUG está ativo, as instruções que fornecem uma imagem clara de quais atividades ocorrem, bem como quaisquer parâmetros principais que afetam o processamento são registradas.</td>
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
Quando o registro em log do WARN está ativo, somente as instruções que indicam condições que estão se aproximando da subotimização são registradas.</td>
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
Descreve as condições que indicam uma falha e precisam ser resolvidas.<br>
Quando o registro de ERROR está ativo, somente as instruções que indicam falhas são registradas. As declarações de log de ERRO indicam um problema grave que deve ser resolvido o mais rápido possível.</td>
<td>
<ul>
<li> Desenvolvimento local</li>
<li>Desenvolvimento</li>
<li>Fase</li>
<li>Produção</li>
</ul></td>
</tr>
</table>

Embora o registro em log do Java ofereça suporte a vários outros níveis de granularidade de registro, AEM a as a Cloud Service recomenda o uso dos três níveis descritos acima.

AEM Os níveis de log são definidos por tipo de ambiente por meio da configuração OSGi, que, por sua vez, são comprometidos com o Git e implantados por meio do Cloud Manager para AEM as a Cloud Service. Por causa disso, é melhor manter as declarações de log consistentes e bem conhecidas para tipos de ambiente, para garantir que os logs disponíveis via AEM como Cloud Service estejam disponíveis no nível de log ideal sem exigir a reimplantação do aplicativo com a configuração atualizada do nível de log.

**Exemplo de saída de log**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**Formato de registro**

<table>
<tbody>
<tr>
<td>Data e hora</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>ID de nó as a Cloud Service AEM</td>
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
<td>Mensagem de registro</td>
<td>Nenhum aprovador especificado, padrão para [ Grupo de usuários Creative Aprovvers ]</td>
</tr>
</tbody>
</table>

### Logs de configuração {#configuration-loggers}

AEM logs Java são definidos como configuração OSGi e, portanto, direcionam ambientes AEM as a Cloud Service específicos usando pastas de modo de execução.

Configure o registro do java para pacotes Java personalizados por meio de configurações OSGi para a fábrica do Sling LogManager. Há duas propriedades de configuração compatíveis:

| Propriedade Configuração OSGi | Descrição |
|---|---|
| org.apache.sling.commons.log.names | Os pacotes Java para os quais coletar instruções de log. |
| org.apache.sling.commons.log.level | O nível de log no qual registrar os pacotes Java, especificado por org.apache.sling.commons.log.names |

Alterar outras propriedades de configuração do OSGi do LogManager pode resultar em problemas de disponibilidade AEM as a Cloud Service.

A seguir estão exemplos das configurações de registro recomendadas (usando o pacote Java de espaço reservado de `com.example`) para os três tipos de ambiente AEM as a Cloud Service.

### Desenvolvimento {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.fatory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### Fase {#stage}

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

AEM registro de solicitação HTTP do as a Cloud Service fornece informações sobre as solicitações HTTP feitas para AEM e suas respostas HTTP em ordem de tempo. Esse log é útil para entender as Solicitações HTTP feitas no AEM e a ordem em que são processadas e respondidas.

A chave para entender esse log é mapear os pares de solicitação e resposta HTTP por suas IDs, indicadas pelo valor numérico entre colchetes. Observe que frequentemente as solicitações e suas respostas correspondentes têm outras solicitações HTTP e respostas interpeladas entre elas no log.

**Exemplo de log**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**Formato de registro**

<table>
<tbody>
<tr>
<td>Data e hora</td>
<td>29/Abr/2020:19:14:21 +0000</td>
</tr>
<tr>
<td>ID do Par de Solicitação/Resposta</td>
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
<td>ID de nó as a Cloud Service AEM</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### Configuração do log {#configuring-the-log}

O log de Solicitação HTTP AEM não pode ser configurado AEM as a Cloud Service.

## Registro de acesso HTTP AEM {#aem-http-access-logging}

AEM como registro de acesso HTTP do Cloud Service mostra solicitações HTTP em ordem de tempo. Cada entrada de log representa a Solicitação HTTP que acessa AEM.

Esse log é útil para entender rapidamente quais solicitações HTTP são feitas para AEM, se elas tiverem êxito ao analisar o código de status de resposta HTTP associado e quanto tempo a solicitação HTTP levou para ser concluída. Esse log também pode ser útil para depurar a atividade de um usuário específico filtrando entradas de log por usuários.

**Exemplo de saída de log**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| AEM ID de nó as a Cloud Service | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| Endereço IP do cliente | - |
| Usuário | myuser@adobe.com |
| Data e hora | 30/Abr/2020:17:37:14 +0000 |
| método HTTP | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| Protocolo | HTTP/1.1 |
| Status da resposta HTTP | 200 |
| Tamanho do corpo da resposta em bytes | 1141 |
| Referenciador | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| Agente do usuário | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### Configurar o registro de acesso HTTP {#configuring-the-http-access-log}

O log de Acesso HTTP não pode ser configurado AEM as a Cloud Service.

## Apache Web Server e Registro do Dispatcher {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service fornece três logs para os Servidores Web Apache e a camada do dispatcher na Publicação:

* Log de acesso do servidor Web Apache HTTPD
* Log de erros do servidor Web Apache HTTPD
* Log do Dispatcher

Observe que esses logs só estão disponíveis para a camada Publicar .

Esse conjunto de logs fornece insights sobre solicitações HTTP para a camada de Publicação as a Cloud Service AEM antes que essas solicitações cheguem ao aplicativo AEM. Isso é importante para entender, pois, idealmente, a maioria das solicitações HTTP para os servidores da camada de Publicação é veiculada pelo conteúdo armazenado em cache pelo Apache HTTPD Web Server e AEM Dispatcher, e nunca alcança o aplicativo AEM em si. Portanto, não há instruções de log para essas solicitações em AEM logs de Java, Solicitação ou Acesso.

### Log de acesso do servidor Web Apache HTTPD {#apache-httpd-web-server-access-log}

O log de acesso do Apache HTTP Web Server fornece instruções para cada solicitação HTTP que chega ao servidor Web/Dispatcher da camada de publicação. Observe que as solicitações enviadas por um CDN upstream não são refletidas nesses logs.

Consulte informações sobre o formato do log de erros no [documentação oficial do apache](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

**Exemplo de saída de log**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**Formato de registro**

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

### Configurando o Log de Acesso do Servidor Web Apache HTTPD {#configuring-the-apache-httpd-webs-server-access-log}

Este log não pode ser configurado AEM as a Cloud Service.

## Log de erros do servidor Web Apache HTTPD {#apache-httpd-web-server-error-log}

O log de erros do Apache HTTP Web Server fornece instruções para cada erro no servidor Web/Dispatcher da camada de publicação.

Consulte informações sobre o formato do log de erros no [documentação oficial do apache](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

**Exemplo de saída de log**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**Formato de registro**

<table>
<tbody>
<tr>
<td>Data e hora</td>
<td>Sex 17 de julho de 2002:16:42 608913 2020</td>
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

### Configurando o Log de Erros do Servidor Web Apache HTTPD {#configuring-the-apache-httpd-web-server-error-log}

Os níveis de log mod_rewrite são definidos pela variável REWRITE_LOG_LEVEL no arquivo `conf.d/variables/global.var`.

Ele pode ser definido como error, warn, info, debug e trace1 - trace8, com um valor padrão de warn. Para depurar as RewriteRules, é recomendável elevar o nível de log para trace2.

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

**Formato de registro**

<table>
<tbody>
<tr>
<td>Data e hora</td>
<td>[17/07/2020:23:48:16 +000]</td>
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
<td>1949ms</td>
</tr>
<tr>
<td>Farm</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>Status do cache</td>
<td>[ação falhada]</td>
</tr>
<tr>
<td>Host</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### Configurar o log de erros do Dispatcher {#configuring-the-dispatcher-error-log}

Os níveis de log do dispatcher são definidos pela variável DISP_LOG_LEVEL no arquivo `conf.d/variables/global.var`.

Ele pode ser definido como error, warn, info, debug e trace1, com um valor padrão de warn.

Embora o log do Dispatcher ofereça suporte a vários outros níveis de granularidade de log, a AEM as a Cloud Service recomenda o uso dos níveis descritos abaixo.

Para definir o nível de log por ambiente, use a ramificação condicional apropriada no `global.var` conforme descrito abaixo:

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
>Para AEM ambientes as a Cloud Service, debug é o nível máximo de verbosidade. O nível de log de rastreamento não é compatível, portanto, evite configurá-lo ao trabalhar em ambientes de nuvem.

## Como acessar logs {#how-to-access-logs}

### Ambientes em nuvem {#cloud-environments}

AEM os registros as a Cloud Service para serviços em nuvem podem ser acessados baixando pela interface do Cloud Manager ou ajustando os logs na linha de comando usando o usando a interface de linha de comando Adobe I/O. Para obter mais informações, consulte o [Documentação de registro do Cloud Manager](/help/implementing/cloud-manager/manage-logs.md).

### SDK local {#local-sdk}

AEM SDK as a Cloud Service fornece arquivos de logs para dar suporte ao desenvolvimento local.

AEM logs estão localizados na pasta `crx-quickstart/logs`, onde os seguintes logs podem ser visualizados:

* AEM log do Java: `error.log`
* AEM log de solicitação HTTP: `request.log`
* Log de acesso HTTP AEM: `access.log`

Os logs de camada do Apache, incluindo o dispatcher, estão no contêiner Docker que contém o Dispatcher. Consulte a [Documentação do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) para obter informações sobre como iniciar o Dispatcher.

Para recuperar os logs:

1. Na linha de comando, digite `docker ps` para listar seus contêineres
1. Para fazer logon no contêiner, digite &quot;`docker exec -it <container> /bin/sh`&quot;, onde `<container>` é a id do contêiner do dispatcher da etapa anterior
1. Navegue até a raiz do cache em `/mnt/var/www/html`
1. Os logs estão em `/etc/httpd/logs`
1. Inspect os logs: eles podem ser acessados na pasta XYZ, onde os seguintes logs podem ser visualizados:
   * Log de acesso do servidor Web Apache HTTPD - `httpd_access.log`
   * Logs de erro do servidor Web Apache HTTPD - `httpd_error.log`
   * Logs do Dispatcher - `dispatcher.log`

Os registros também são impressos diretamente na saída do terminal. Na maioria das vezes, esses registros devem ser DEBUG, o que pode ser feito transmitindo o nível de Depuração como um parâmetro ao executar o Docker. Por exemplo:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## Depuração da produção e do estágio {#debugging-production-and-stage}

Em circunstâncias excepcionais, os níveis de log precisam ser alterados para registrar em uma granularidade mais fina em ambientes de Preparo ou Produção.

Embora isso seja possível, ele requer alterações nos níveis de log nos arquivos de configuração no Git de Aviso e Erro para Depuração, além de executar uma implantação para AEM as a Cloud Service para registrar essas alterações de configuração nos ambientes.

Dependendo do tráfego e da quantidade de declarações de log gravadas pelo Debug, isso pode resultar em um impacto negativo no desempenho do ambiente. Portanto, é recomendável que as alterações nos níveis de depuração de Preparo e Produção sejam:

* Feito criteriosamente e apenas quando absolutamente necessário
* Revertido para os níveis apropriados e reimplantado o mais rápido possível

## Logs do Splunk {#splunk-logs}

Os clientes que têm contas do Splunk podem solicitar, por meio do tíquete de suporte ao cliente, que os logs do AEM Cloud Service sejam encaminhados ao índice apropriado. Os dados de registro são equivalentes ao que está disponível por meio dos downloads de log do Cloud Manager, mas os clientes podem achar conveniente aproveitar os recursos de query disponíveis no produto Splunk.

A largura de banda de rede associada aos logs enviados ao Splunk é considerada parte do uso de E/S de rede do cliente.

### Ativar o encaminhamento do Splunk {#enabling-splunk-forwarding}

Na solicitação de suporte, os clientes devem indicar:

* Endereço do ponto de extremidade HEC do Splunk. Esse terminal deve ter um certificado SSL válido e estar acessível publicamente.
* O índice Splunk
* A porta Splunk
* O token HEC do Splunk. Consulte [esta página](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) para obter mais informações.

As propriedades acima devem ser especificadas para cada combinação de programa/tipo de ambiente relevante. Por exemplo, se um cliente deseja ambientes de desenvolvimento, armazenamento temporário e produção, ele deve fornecer três conjuntos de informações, conforme indicado abaixo.

>[!NOTE]
>
>O encaminhamento de segmentos para ambientes de programa sandbox não é suportado.

>[!NOTE]
>
>O recurso de encaminhamento do Splunk não é possível em um endereço IP de saída dedicado.

Certifique-se de que a solicitação inicial inclua todo o ambiente de desenvolvimento que deve ser ativado, além dos ambientes stage/prod. O Splunk deve ter um certificado SSL e ser aberto publicamente.

Se qualquer novo ambiente de desenvolvimento criado após a solicitação inicial tiver o encaminhamento do Splunk, mas não o tiver ativado, uma solicitação adicional deverá ser feita.

Observe também que, se os ambientes de desenvolvimento tiverem sido solicitados, é possível que outros ambientes de desenvolvimento que não estejam nos ambientes de solicitação ou mesmo sandbox tenham o encaminhamento de Splunk ativado e compartilhem um índice de Splunk. Os clientes podem usar o `aem_env_id` para distinguir entre esses ambientes.

Abaixo você encontrará um exemplo de solicitação de suporte ao cliente:

Programa 123, Env de produção

* Endereço do ponto de extremidade de Splunk HEC: `splunk-hec-ext.acme.com`
* Índice de partes: acme_123prod (o cliente pode escolher qualquer convenção de nomenclatura que desejar)
* Porta de tronco: 443
* Token de HEC do Splunk: ABC123

Programa 123, Stage Env

* Endereço do ponto de extremidade de Splunk HEC: `splunk-hec-ext.acme.com`
* Índice de partes: acme_123stage
* Porta de tronco: 443
* Token de HEC do Splunk: ABC123

Programa 123, Dev Envs

* Endereço do ponto de extremidade de Splunk HEC: `splunk-hec-ext.acme.com`
* Índice de partes: acme_123dev
* Porta de tronco: 443
* Token de HEC do Splunk: ABC123

Pode ser suficiente para que o mesmo índice Splunk seja usado em cada ambiente, nesse caso, a variável `aem_env_type` pode ser usado para diferenciar com base nos valores dev, stage e prod. Se houver vários ambientes de desenvolvimento, a variável `aem_env_id` também pode ser usado. Algumas organizações podem escolher um índice separado para os logs do ambiente de produção se o índice associado limitar o acesso a um conjunto reduzido de usuários do Splunk.

Veja um exemplo de entrada de log:

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
file_path: /var/log/aem/error.log
host: 172.34.200.12 
level: INFO
msg: [FelixLogListener] com.adobe.granite.repository Service [5091, [org.apache.jackrabbit.oak.api.jmx.SessionMBean]] ServiceEvent REGISTERED
orig_time: 16.07.2020 08:35:32.346
pod_name: aemloggingall-aem-author-77797d55d4-74zvt
splunk_customer: true
```
