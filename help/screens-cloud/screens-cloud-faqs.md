---
title: Perguntas frequentes as a Cloud Service do Screens
description: Esta página descreve as perguntas frequentes as a Cloud Service do Screens.
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 02c9cbff56399ea2ca1baad7d2289d5d4c17c1c5
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Perguntas frequentes as a Cloud Service do Screens {#screens-cloud-faqs}

A seção a seguir fornece respostas às Perguntas frequentes relacionadas ao projeto do Screens as a Cloud Service.

## O que devo fazer se o Player do AEM Screens que aponta para o Screens as a Cloud Service não selecionar as clientlibs personalizadas com o formato /etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css?

AEM as a Cloud Service alterações nas chaves de cache longas com cada implantação. O AEM Screens gera os caches offline quando o conteúdo é modificado, em vez de quando o Cloud Manager executa a implantação. Essas chaves de cache longas nos manifestos são inválidas, portanto, o reprodutor não consegue baixá-las *clientlibs*.

Usando `longCacheKey="none"` em seu `clientlib` a pasta remove completamente as chaves de cache longas para elas *clientlibs*.


## O que devemos fazer se o manifesto offline não incluir todos os recursos conforme planejado? {#offline-manifest}

Os caches offline são gerados usando **bulk-offline-update-screens-service** usuário do serviço. Determinados caminhos, não acessíveis por `bulk-offline-update-screens-service`, levar ao conteúdo ausente em manifestos offline.

No seu código, isto é, `ui.config or ui.apps`, crie uma configuração OSGi na pasta de configuração, com o seguinte conteúdo, e nomeie o nome do arquivo como `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

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

É recomendável usar imagens no formato `.png` e `.jpeg` em um canal as a Cloud Service AEM Screens, para obter a melhor experiência em sinalização digital.
As imagens no formato `*.tif` (Formato de arquivo de imagem de tag) não é compatível com o AEM Screens as a Cloud Service. Caso um canal tenha esse formato de imagem, então, no lado do reprodutor, a imagem não será renderizada.

## O que devo fazer se um Canal no modo Desenvolvedor (online) não estiver sendo renderizado no AEM Screens Player?{#screens-cloud-online-channel-blank-iframe}

É recomendável aproveitar os recursos de armazenamento em cache do AEM Screens, mas se você precisar executar seu Canal no modo Desenvolvedor e o AEM Screens Player mostrar uma tela em branco, verificar as ferramentas do desenvolvedor do Player e procurar `X-Frame-Options` ou `frame-ancestors` erros. A resolução é configurar o dispatcher para permitir o conteúdo em execução no iFrames. Normalmente, a seguinte configuração funcionará:

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## Qual é o uso do limite do código de registro?

Como prática recomendada, é possível limitar o uso do código de registro. Se um código de registro estiver comprometido, mas tiver um limite de 100 registros, o invasor poderá se registrar apenas até esse número, mas não mais. Você sempre pode atualizar o limite de uso depois que o código de registro é criado e alguns dos players do cliente já foram registrados. Se o cliente observar uma atividade de registro incomum para um código de registro específico, ele poderá reduzir o limite em tempo real enquanto investiga e aumentar o número novamente se for um alarme falso, sem afetar os players já registrados.
