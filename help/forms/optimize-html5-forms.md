---
title: Otimização de formulários do HTML5
description: Você pode otimizar o tamanho de saída dos formulários HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: HTML5 Forms,Mobile Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Otimização de formulários do HTML5 {#optimizing-html-forms}

<span class="preview"> O recurso HTML5 Forms é oferecido como parte do Programa de acesso antecipado. Para solicitar acesso, envie um email de sua ID de email oficial (comercial) para aem-forms-ea@adobe.com.
</span>

O HTML5 forms renderiza formulários no formato HTML5. A saída resultante pode ser grande, dependendo de fatores como o tamanho do formulário e as imagens no formulário. Para otimizar a transferência de dados, a abordagem recomendada é compactar a resposta do HTML usando o Servidor Web do qual a solicitação está sendo atendida. Essa abordagem reduz o tamanho da resposta, o tráfego de rede e o tempo necessário para transmitir dados entre as máquinas do servidor e do cliente.

Este artigo descreve as etapas necessárias para habilitar a compactação para o Apache Web Server 2.0 de 32 bits, com JBoss.

>[!NOTE]
>
>As instruções a seguir não se aplicam a servidores diferentes do Apache Web Server 2.0 de 32 bits.

Obtenha o software Apache Web Server aplicável ao seu sistema operacional:

* Para Windows, baixe o servidor Web Apache do site do Projeto Apache HTTP Server.
* Para Solaris 64 bits, baixe o servidor Web Apache do site Sunfreeware para Solaris.
* Para Linux, o servidor Web Apache é pré-instalado em um sistema Linux.

O Apache pode se comunicar com o JBoss usando HTTP ou o protocolo AJP.

1. Remova o comentário das seguintes configurações de módulo no arquivo *APACHE_HOME/conf/httpd.conf*.

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Para Linux, o diretório padrão APACHE_HOME é /etc/httpd/.

1. Configure o proxy na porta 8080 do JBoss.

   Adicione a seguinte configuração ao arquivo de configuração *APACHE_HOME/conf/httpd.conf*.

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >Quando você usa um proxy, as seguintes alterações de configuração são necessárias:
   >
   >* Acesso: *https://&lt;servidor>:&lt;porta>/system/console/configMgr*
   >* Editar a configuração do Filtro referenciador do Apache Sling
   >* Em Permitir hosts, adicione a entrada para o servidor proxy

1. Ative a compactação.

   Adicione a seguinte configuração ao arquivo de configuração *APACHE_HOME/conf/httpd.conf*.

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don't compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. Para acessar o servidor AEM, use https://[Apache_server]:80.
