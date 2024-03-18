---
title: Consultas persistentes do GraphQL - ativação do armazenamento em cache no Dispatcher
description: O Dispatcher é uma camada de segurança e cache na frente dos ambientes de publicação do Adobe Experience Manager. Você pode ativar o armazenamento em cache de consultas persistentes no AEM Headless.
feature: Dispatcher, GraphQL API
exl-id: 30a97e56-6699-41c4-a4eb-fc6236667f8f
source-git-commit: 859ea382cce6822da1da7d11213c3f44a25edef3
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 7%

---

# Consultas persistentes do GraphQL - ativação do armazenamento em cache no Dispatcher {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>Se o armazenamento em cache no Dispatcher estiver ativado, a variável [Filtro CORS](/help/headless/deployment/cross-origin-resource-sharing.md) não é necessária e, portanto, essa seção pode ser ignorada.

O armazenamento em cache de consultas persistentes não é ativado por padrão no Dispatcher. A ativação padrão não é possível, pois os clientes que usam CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens) precisam revisar e possivelmente atualizar a configuração do Dispatcher.

>[!NOTE]
>
>O Dispatcher não armazena em cache os `Vary` cabeçalho.
>
>O armazenamento em cache de outros cabeçalhos relacionados ao CORS pode ser habilitado no Dispatcher, mas pode ser insuficiente quando há várias origens do CORS.

>[!NOTE]
>
>Para obter a documentação detalhada sobre o Dispatcher, consulte o [Guia do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR).

## Habilitar armazenamento em cache de consultas persistentes {#enable-caching-persisted-queries}

Para habilitar o armazenamento em cache de consultas persistentes, defina a variável do Dispatcher `CACHE_GRAPHQL_PERSISTED_QUERIES`:

1. Adicionar a variável ao arquivo do Dispatcher `global.vars`:

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>Para atingir objetivos `ETag` cálculo de cabeçalho nas consultas persistentes em cache (para *cada* resposta única) a `FileETag Digest` a configuração deve ser usada na configuração do Dispatcher configuração do host virtual (se ainda não existir):
>
>```xml
><Directory />    
>   ...    
>   FileETag Digest
></Directory> 
>```

>[!NOTE]
>
>Para estar em conformidade com [Requisitos do Dispatcher para documentos que podem ser armazenados em cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F), o Dispatcher adiciona o sufixo `.json` para todos os URLS de consulta persistentes, para que o resultado possa ser armazenado em cache.
>
>Esse sufixo é adicionado por uma regra de regravação, depois que o cache de consultas persistentes é ativado.

## Configuração do CORS no Dispatcher {#cors-configuration-in-dispatcher}

Clientes que usam solicitações do CORS podem precisar revisar e atualizar sua configuração do CORS no Dispatcher.

* A variável `Origin` O cabeçalho não deve ser transmitido para a publicação do AEM por meio do Dispatcher:
   * Verifique a `clientheaders.any` arquivo.
* Em vez disso, as solicitações do CORS devem ser avaliadas para as origens permitidas no nível do Dispatcher. Essa abordagem também garante que os cabeçalhos relacionados ao CORS sejam definidos corretamente, em um local, em todos os casos.
   * Essa configuração deve ser adicionada à variável `vhost` arquivo. Um exemplo de configuração é fornecido abaixo; para simplificar, somente a parte relacionada ao CORS foi fornecida. Você pode adaptá-la aos seus casos de uso específicos.

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```
