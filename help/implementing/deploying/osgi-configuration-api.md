---
title: API de configuração do OSGi
description: Descrição da superfície de configuração AEM do OSGi as a Cloud Service
feature: Deploying
exl-id: 94d3df65-71d7-4442-8412-fe2cca7e79ff
source-git-commit: cba6648d7ef18f3cccbd9562f3a66d9c683ae852
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 3%

---

# API de configuração do OSGi

As duas listas abaixo refletem a AEM superfície de configuração OSGi as a Cloud Service, descrevendo o que os clientes podem configurar.

1. Uma lista de configurações OSGi que não devem ser configuradas pelo código do cliente
1. Uma lista de configurações OSGi cujas propriedades podem ser configuradas, mas devem seguir as regras de validação indicadas. Essas regras incluem se a declaração da propriedade é obrigatória, seu tipo e, em alguns casos, seu intervalo de valores permitido.

Se uma configuração OSGI não estiver listada, ela pode ser configurada por código de cliente.

Essas regras são validadas durante o processo de criação do Cloud Manager. Poderão ser acrescentadas regras adicionais ao longo do tempo e a data de execução prevista é anotada no quadro. Espera-se que os clientes cumpram essas regras até a data de imposição do target. O não cumprimento das regras após a data de remoção gerará erros no processo de build do Cloud Manager. Os projetos Maven devem incluir o [AEM Plug-in Maven do Analisador de Compilação do SDK as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=pt-BR) para sinalizar erros de configuração de OSGI durante o desenvolvimento local do SDK.

Informações adicionais sobre a configuração do OSGI podem ser encontradas em [esta localização](/help/implementing/deploying/configuring-osgi.md).

## Configurações OSGi que não podem ser modificadas {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Data de anúncio: 30/4/2021, Data de execução: 31/7/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Data de anúncio: 30/4/2021, Data de execução: 31/7/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Data de anúncio: 30/4/2021, Data de execução: 31/7/2021)
* **`org.apache.felix.http (Factory)`** (Data de anúncio: 30/4/2021, Data de execução: 31/7/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (Data de anúncio: 25/8/2021, Data de execução: 26/11/2021)

## Configurações do OSGi sujeitas às regras de validação de criação {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Data de anúncio: 30/4/2021, Data de execução: 31/7/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * Tipo: integer
      * Intervalo necessário: 2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * Tipo: double
   * `org.apache.felix.eventadmin.Timeout`
      * Tipo: integer
   * `org.apache.felix.eventadmin.RequireTopic`
      * Tipo: booleano
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * Obrigatório
      * Tipo: matriz de cadeias de caracteres
      * Intervalo necessário: Deve incluir pelo menos todos os `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * Tipo: matriz de cadeias de caracteres
* **`org.apache.felix.http`** (Data de anúncio: 30/4/2021, Data de execução: 31/7/2021)
   * `org.apache.felix.http.timeout`
      * Tipo: integer
   * `org.apache.felix.http.session.timeout`
      * Tipo: integer
   * `org.apache.felix.http.jetty.threadpool.max`
      * Tipo: integer
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Tipo: integer
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Tipo: integer
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Tipo: integer
   * `org.apache.felix.http.jetty.maxFormSize`
      * Tipo: integer
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Tipo: booleano
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Tipo: string
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Tipo: booleano
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Tipo: string
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Tipo: string
   * `org.eclipse.jetty.servlet.SessionPath`
      * Tipo: string
   * `org.eclipse.jetty.servlet.MaxAge`
      * Tipo: integer
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Tipo: integer
   * `org.apache.felix.jetty.gziphandler.enable`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Tipo: integer
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Tipo: integer
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Tipo: integer
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Tipo: booleano
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Tipo: string
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
* **`org.apache.sling.scripting.cache`** (Data de anúncio: 30/4/2021, Data de execução: 31/7/2021)
   * `org.apache.sling.scripting.cache.size`
      * Tipo: integer
      * Intervalo necessário: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Obrigatório
      * Tipo: matriz de cadeias de caracteres
      * Intervalo necessário: deve incluir js
* **`com.day.cq.mailer.DefaultMailService`** (Data de anúncio: 30/4/2021, Data de execução: 31/7/2021)
   * `smtp.host`
      * Tipo: string
   * `smtp.port`
      * Tipo: integer
      * Intervalo necessário: 465, 587 ou 25
   * `smtp.user`
      * Tipo: string
   * `smtp.password`
      * Tipo: string
   * `from.address`
      * Tipo: string
   * `smtp.ssl`
      * Tipo: string
   * `smtp.starttls`
      * Tipo: booleano
   * `smtp.requiretls`
      * Tipo: booleano
   * `debug.email`
      * Tipo: booleano
   * `oauth.flow`
      * Tipo: booleano
* **`org.apache.sling.commons.log.LogManager.factory.config`** (Data de anúncio: 16/11/21, Data de execução: 16/2/21)
   * `org.apache.sling.commons.log.level`
      * Tipo: enumeração
      * Intervalo necessário: INFO, DEBUG ou TRACE
   * `org.apache.sling.commons.log.names`
      * Tipo: string
   * `org.apache.sling.commons.log.file`
      * Tipo: string
   * `org.apache.sling.commons.log.additiv`
      * Tipo: booleano