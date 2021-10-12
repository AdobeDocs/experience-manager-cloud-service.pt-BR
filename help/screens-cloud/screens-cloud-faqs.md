---
title: Perguntas frequentes as a Cloud Service do Screens
description: Esta página descreve as perguntas frequentes as a Cloud Service do Screens.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: cf091056bdb96917a6d22bf1197d9b34ebbf9610
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Perguntas frequentes as a Cloud Service do Screens {#screens-cloud-faqs}

A seção a seguir fornece respostas às Perguntas frequentes relacionadas ao projeto do Screens as a Cloud Service.

## O que devo fazer se o reprodutor do AEM Screens que aponta para o Screens as a Cloud Service não selecionar as clientlibs personalizadas com o formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service alterações nas chaves de cache longas com cada implantação. O AEM Screens gera os caches offline quando o conteúdo é modificado, em vez de quando o Cloud Manager executa a implantação. Essas chaves de cache longas nos manifestos são inválidas, portanto, o reprodutor falha ao baixar esses *clientlibs*.

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

## Quais formatos de imagem são recomendados para a representação contínua de imagens em canais as a Cloud Service do AEM Screens?{#screens-cloud-image-format}

É recomendável usar imagens no formato `.png` e `.jpeg` em um canal as a Cloud Service do AEM Screens, para obter a melhor experiência em sinalização digital.
As imagens no formato `*.tif` (Tag Image File format) não são suportadas no AEM Screens as a Cloud Service. Caso um canal tenha esse formato de imagem, então, no lado do reprodutor, a imagem não será renderizada.