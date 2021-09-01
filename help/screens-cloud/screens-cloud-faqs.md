---
title: Perguntas frequentes sobre o Screens as a Cloud Service
description: Esta página descreve o Screens como perguntas frequentes do Cloud Service.
source-git-commit: 7a26bb50a8b95a2358912249e21daeb9c5e9c1a3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Perguntas frequentes sobre o Screens as a Cloud Service {#screens-cloud-faqs}

A seção a seguir fornece respostas às Perguntas frequentes relacionadas ao Screens as a Cloud Service.

## O que devo fazer se o reprodutor do AEM Screens que aponta para o Screens como um Cloud Service não escolher as clientlibs personalizadas com o formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-81364378974b0f89d686d9591526d63-lc.min.css?

O AEM as a Cloud Service altera as chaves de cache longas com cada implantação. O AEM Screens gera os caches offline quando o conteúdo é modificado, em vez de quando o Cloud Manager executa a implantação. Essas chaves de cache longas nos manifestos são inválidas, portanto, o reprodutor falha ao baixar esses *clientlibs*.

Usar `longCacheKey="none"` em sua pasta `clientlib` remove completamente as chaves de cache longas para esses *clientlibs*.


## O que devemos fazer se o manifesto offline não incluir todos os recursos conforme planejado? {#offline-manifest}

Os caches offline são gerados usando o usuário de serviço **bulk-offline-update-screens-service**. Determinados caminhos, não acessíveis por `bulk-offline-update-screens-service`, levam ao conteúdo ausente em manifestos offline.

No seu código, ou seja, `ui.config or ui.apps`, crie uma configuração OSGi na pasta de configuração, com o seguinte conteúdo, e nomeie o nome do arquivo como `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```
