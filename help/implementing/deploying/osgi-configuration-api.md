---
title: API de configuração do OSGi
description: Descrição da superfície de configuração do OSGi do AEM as a Cloud Service
feature: Deploying
exl-id: 94d3df65-71d7-4442-8412-fe2cca7e79ff
source-git-commit: cba6648d7ef18f3cccbd9562f3a66d9c683ae852
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 3%

---

# API de configuração do OSGi

As duas listas abaixo refletem a superfície de configuração OSGi as a Cloud Service do AEM, descrevendo o que os clientes podem configurar.

1. Uma lista de configurações OSGi que não devem ser definidas pelo código do cliente
1. Uma lista de configurações OSGi cujas propriedades podem ser configuradas, mas devem obedecer às regras de validação indicadas. Essas regras incluem se a declaração da propriedade é obrigatória, seu tipo e, em alguns casos, seu intervalo permitido de valores.

Se uma configuração OSGI não estiver listada, ela poderá ser configurada pelo código do cliente.

Essas regras são validadas durante o processo de criação do Cloud Manager. Regras adicionais podem ser adicionadas ao longo do tempo e a data de aplicação esperada é anotada na tabela. Espera-se que os clientes cumpram essas regras até a data de aplicação prevista. Não seguir as regras após a data de remoção gerará erros no processo de compilação do Cloud Manager. Os projetos Maven devem incluir a [Plug-in Maven Analisador de build do SDK as a Cloud Service do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR) para sinalizar erros de configuração OSGI durante o desenvolvimento do SDK local.

Informações adicionais sobre a configuração OSGI podem ser encontradas em [este local](/help/implementing/deploying/configuring-osgi.md).

## Configurações do OSGi que não podem ser modificadas {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Data do anúncio: 30/4/2021, Data de execução: 31/7/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Data do anúncio: 30/4/2021, Data de execução: 31/7/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Data do anúncio: 30/4/2021, Data de execução: 31/7/2021)
* **`org.apache.felix.http (Factory)`** (Data do anúncio: 30/4/2021, Data de execução: 31/7/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (Data do anúncio: 25/8/2021, Data de execução: 26/11/2021)

## Configurações de OSGi sujeitas às regras de validação de build {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Data do anúncio: 30/4/2021, Data de execução: 31/7/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * Tipo: número inteiro
      * Intervalo obrigatório: 2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * Tipo: duplo
   * `org.apache.felix.eventadmin.Timeout`
      * Tipo: número inteiro
   * `org.apache.felix.eventadmin.RequireTopic`
      * Tipo: booleano
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * Obrigatório
      * Tipo: matriz de cadeias de caracteres
      * Intervalo obrigatório: deve incluir pelo menos todos `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * Tipo: matriz de cadeias de caracteres
* **`org.apache.felix.http`** (Data do anúncio: 30/4/2021, Data de execução: 31/7/2021)
   * `org.apache.felix.http.timeout`
      * Tipo: número inteiro
   * `org.apache.felix.http.session.timeout`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.threadpool.max`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Tipo: número inteiro
   * `org.apache.felix.http.jetty.maxFormSize`
      * Tipo: número inteiro
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Tipo: booleano
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Tipo: sequência de caracteres
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Tipo: sequência de caracteres
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Tipo: sequência de caracteres
   * `org.eclipse.jetty.servlet.SessionPath`
      * Tipo: sequência de caracteres
   * `org.eclipse.jetty.servlet.MaxAge`
      * Tipo: número inteiro
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Tipo: número inteiro
   * `org.apache.felix.jetty.gziphandler.enable`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Tipo: número inteiro
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Tipo: número inteiro
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Tipo: número inteiro
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Tipo: sequência de caracteres
   * `org.apache.felix.jetty.gzip.includedMethods`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.includedPaths`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.http.session.invalidate`
      * Tipo: booleano
   * `org.apache.felix.http.session.container.attribute`
      * Tipo: matriz de cadeias de caracteres
   * `org.apache.felix.http.session.uniqueid`
      * Tipo: booleano
* **`org.apache.sling.scripting.cache`** (Data do anúncio: 30/4/2021, Data de execução: 31/7/2021)
   * `org.apache.sling.scripting.cache.size`
      * Tipo: número inteiro
      * Intervalo obrigatório: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Obrigatório
      * Tipo: matriz de cadeias de caracteres
      * Intervalo obrigatório: deve incluir js
* **`com.day.cq.mailer.DefaultMailService`** (Data do anúncio: 30/4/2021, Data de execução: 31/7/2021)
   * `smtp.host`
      * Tipo: sequência de caracteres
   * `smtp.port`
      * Tipo: número inteiro
      * Intervalo obrigatório: 465, 587 ou 25
   * `smtp.user`
      * Tipo: sequência de caracteres
   * `smtp.password`
      * Tipo: sequência de caracteres
   * `from.address`
      * Tipo: sequência de caracteres
   * `smtp.ssl`
      * Tipo: sequência de caracteres
   * `smtp.starttls`
      * Tipo: booleano
   * `smtp.requiretls`
      * Tipo: booleano
   * `debug.email`
      * Tipo: booleano
   * `oauth.flow`
      * Tipo: booleano
* **`org.apache.sling.commons.log.LogManager.factory.config`** (Data do anúncio: 16/11/21, Data de execução: 16/2/21)
   * `org.apache.sling.commons.log.level`
      * Tipo: enumeração
      * Intervalo obrigatório: INFO, DEBUG ou TRACE
   * `org.apache.sling.commons.log.names`
      * Tipo: sequência de caracteres
   * `org.apache.sling.commons.log.file`
      * Tipo: sequência de caracteres
   * `org.apache.sling.commons.log.additiv`
      * Tipo: booleano