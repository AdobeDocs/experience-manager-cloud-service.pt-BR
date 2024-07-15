---
title: Perguntas frequentes sobre o Screens as a Cloud Service
description: Esta página descreve as perguntas as a Cloud Service do Screens.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 2%

---

# Perguntas frequentes sobre o Screens as a Cloud Service {#screens-cloud-faqs}

A seção a seguir fornece respostas às perguntas frequentes relacionadas ao projeto Screens as a Cloud Service.

## O que devo fazer se o AEM Screens Player que aponta para o Screens as a Cloud Service não escolher as clientlibs personalizadas com o formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

O AEM as a Cloud Service altera as longas chaves de cache a cada implantação. O AEM Screens gera os caches offline quando o conteúdo é modificado, em vez de quando o Cloud Manager executa a implantação. Essas chaves de cache longas nos manifestos são inválidas, portanto, o player não pode baixar o *clientlibs*.

Usar o `longCacheKey="none"` na pasta `clientlib` remove as chaves de cache longas juntas para o *clientlibs*.


## O que devo fazer se o manifesto offline não incluir todos os recursos conforme esperado? {#offline-manifest}

Os caches offline são gerados usando o usuário do serviço **bulk-offline-update-screens-service**. Determinados caminhos, não acessíveis por `bulk-offline-update-screens-service`, levam a conteúdo ausente em manifestos offline.

Em seu código, ou seja, `ui.config or ui.apps`, crie uma configuração OSGi na pasta de configuração, com o conteúdo a seguir, e nomeie o arquivo como `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## Quais formatos de imagem são recomendados para a representação contínua de imagens em um canal as a Cloud Service do AEM Screens?{#screens-cloud-image-format}

A Adobe recomenda usar imagens no formato `.png` e `.jpeg` em um canal as a Cloud Service AEM Screens, para obter a melhor experiência de sinalização digital.
As imagens no formato `*.tif` (formato de Arquivo de Imagem de Marca) não têm suporte no AEM Screens as a Cloud Service. Se um canal tiver esse formato de imagem, no lado do reprodutor, a imagem não será renderizada.

## O que devo fazer se um Canal no modo de Desenvolvedor (online) não estiver sendo renderizado no AEM Screens Player?{#screens-cloud-online-channel-blank-iframe}

A Adobe recomenda que você use os recursos de cache do AEM Screens. No entanto, se você precisar executar o Canal no modo de Desenvolvedor e o AEM Screens Player mostrar uma tela em branco, verifique as ferramentas de desenvolvedor do Player e procure por erros `X-Frame-Options` ou `frame-ancestors`. A resolução é configurar o Dispatcher para permitir a execução de conteúdo em iFrames. Normalmente, a seguinte configuração funciona:

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## Qual é o uso do limite do código de registro?

Como prática recomendada, você pode limitar o uso do código de registro. Se um código de registro for comprometido, mas tiver um limite de 100 registros, o invasor poderá registrar somente até esse número, mas não mais. Você sempre pode atualizar o limite de uso depois que o código de registro for criado e alguns dos players do cliente já tiverem sido registrados. Se o cliente observar uma atividade de registro incomum para um código de registro específico, ele poderá diminuir o limite em tempo real enquanto investiga. Eles podem aumentar o número de volta se for um alarme falso, sem afetar os jogadores já registrados.
