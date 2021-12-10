---
title: 'Solução de problemas do desempenho do armazenamento em cache  '
seo-title: Troubleshooting caching performance
description: 'Solução de problemas do desempenho do armazenamento em cache  '
seo-description: Troubleshooting caching performance
contentOwner: khsingh
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Desempenho do armazenamento em cache {#caching-performance}

Você pode encontrar alguns dos seguintes problemas ao configurar ou usar o cache Adaptive Forms em um ambiente Cloud Service:

## Alguns Forms adaptáveis que contêm imagens ou vídeos não são invalidados automaticamente do cache do Dispatcher {#images-videos-not-invalidated}

Você pode selecionar e adicionar imagens ou vídeos do navegador de ativos a um Formulário adaptável. Quando essas imagens são editadas no editor de Ativos, a versão em cache de um formulário adaptável contendo essas imagens não é invalidada. O formulário adaptável continua exibindo imagens mais antigas.

Para resolver o problema, depois de publicar as imagens e o vídeo, desfaça a publicação e publique explicitamente o Adaptive Forms que faz referência a esses ativos.

## Alguns Forms adaptáveis contendo fragmentos de conteúdo ou fragmentos de experiência não são invalidados automaticamente do cache do Dispatcher {#content-fragments-experience-fragments-not-invalidated}

É possível adicionar um fragmento de conteúdo ou um fragmento de experiência a um formulário adaptável. Quando esses fragmentos são editados e publicados de maneira independente, a versão em cache de um formulário adaptável contendo esses fragmentos não é invalidada. O formulário adaptável continua exibindo fragmentos mais antigos.

Para resolver o problema, após a publicação do fragmento de conteúdo ou fragmento de experiência atualizado, desfaça a publicação e publique explicitamente o Adaptive Forms que usa esses ativos.

## Somente a primeira instância do Adaptive Forms é armazenada em cache {#only-first-instance-cached}

Quando a URL do formulário adaptável não contém informações de localização e a opção Usar localidade do navegador no gerenciador de configuração está ativada, uma versão localizada do formulário adaptável é disponibilizada e uma instância do formulário adaptável, com base na primeira solicitação (localidade do navegador solicitada), é armazenada em cache e entregue a cada usuário subsequente.

Execute as seguintes etapas para resolver o problema:

1. Abra o projeto do Experience Manager.
1. Abra o `dispatcher/scr/conf.d/rewrites/rewrite.rules` para edição.
1. Abra o `conf.d/httpd-dispatcher.conf` ou qualquer outro arquivo de configuração configurado para carregar no tempo de execução.
1. Adicione o seguinte código ao arquivo e salve-o. É um código de amostra para modificá-lo de acordo com seu ambiente.

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two character which most likely will be the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## O armazenamento em cache CDN para de funcionar após 300 segundos {#cdn-caching-stops-working-after-300-seconds}

O armazenamento em cache do CDN para de funcionar após 300 segundos e todas as solicitações para armazenar em cache no CDN são redirecionadas para o Dispatcher.

Para resolver o problema, defina o cabeçalho da página como 0:

1. Crie um arquivo em `src\conf.d\available_vhosts`

1. Adicione o seguinte ao arquivo para definir o cabeçalho da página

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. Salve e feche o arquivo.
1. Modifique o link suave para `src\conf.d\enabled_vhosts\default.vhost` para apontar para um novo arquivo.
