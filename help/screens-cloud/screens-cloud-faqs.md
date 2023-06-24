---
title: Perguntas frequentes sobre o Screens as a Cloud Service
description: Esta página descreve as perguntas mais frequentes sobre o Screens as a Cloud Service.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 2%

---

# Perguntas frequentes sobre o Screens as a Cloud Service {#screens-cloud-faqs}

A seção a seguir fornece respostas às perguntas frequentes relacionadas ao projeto do Screens as a Cloud Service.

## O que devo fazer se o AEM Screens Player que aponta para o Screens as a Cloud Service não escolher as clientlibs personalizadas com o formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

O AEM as a Cloud Service altera as longas chaves de cache a cada implantação. O AEM Screens gera os caches offline quando o conteúdo é modificado, em vez de quando o Cloud Manager executa a implantação. Essas chaves de cache longas nos manifestos são inválidas, portanto, o reprodutor não baixa o *clientlibs*.

Usar `longCacheKey="none"` no seu `clientlib` A pasta remove as chaves de cache longas completamente para o *clientlibs*.


## O que devo fazer se o manifesto offline não incluir todos os recursos conforme esperado? {#offline-manifest}

Os caches offline são gerados usando **bulk-offline-update-screens-service** usuário do serviço. Determinados caminhos, não acessíveis pelo `bulk-offline-update-screens-service`, levam a conteúdo ausente em manifestos offline.

Em seu código, ou seja, `ui.config or ui.apps`, crie uma configuração OSGi na pasta de configuração, com o seguinte conteúdo e nomeie o arquivo como `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

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

É recomendável usar imagens no formato `.png` e `.jpeg` em um canal AEM Screens as a Cloud Service, para obter a melhor experiência de sinalização digital.
As imagens no formato `*.tif` (Formato de arquivo de imagem de tag) não são compatíveis com o AEM Screens as a Cloud Service. Se um canal tiver esse formato de imagem, no lado do reprodutor, a imagem não será renderizada.

## O que devo fazer se um Canal no modo de Desenvolvedor (online) não estiver sendo renderizado no AEM Screens Player?{#screens-cloud-online-channel-blank-iframe}

A Adobe recomenda que você use os recursos de cache do AEM Screens. No entanto, se você precisar executar o Canal no modo Desenvolvedor e o AEM Screens Player mostrar uma tela em branco, verifique as ferramentas do desenvolvedor do Player e procure `X-Frame-Options` ou `frame-ancestors` erros. A resolução é configurar o Dispatcher para permitir a execução de conteúdo em iFrames. Normalmente, a seguinte configuração funciona:

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## Qual é o uso do limite do código de registro?

Como prática recomendada, você pode limitar o uso do código de registro. Se um código de registro for comprometido, mas tiver um limite de 100 registros, o invasor poderá registrar somente até esse número, mas não mais. Você sempre pode atualizar o limite de uso depois que o código de registro for criado e alguns dos players do cliente já tiverem sido registrados. Se o cliente observar uma atividade de registro incomum para um código de registro específico, ele poderá diminuir o limite em tempo real enquanto investiga. Eles podem aumentar o número de volta se for um alarme falso, sem afetar os jogadores já registrados.
