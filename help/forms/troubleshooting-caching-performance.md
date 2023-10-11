---
title: Como podemos solucionar problemas relacionados ao armazenamento em cache do AEM Forms as a Cloud Service?
description: Solucionar problemas relacionados ao cache do AEM Forms as a Cloud Service.
contentOwner: khsingh
exl-id: eae44a6f-25b4-46e9-b38b-5cec57b6772c
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Desempenho de cache {#caching-performance}

Você pode encontrar alguns dos seguintes problemas ao configurar ou usar o cache Adaptive Forms em um ambiente de Cloud Service:

## Alguns Forms adaptáveis contendo imagens ou vídeos não são invalidados automaticamente do cache do Dispatcher {#images-videos-not-invalidated}

Você pode selecionar e adicionar imagens ou vídeos do navegador de ativos a um Formulário adaptável. Quando essas imagens são editadas no editor de ativos, a versão em cache de um Formulário adaptável que contém essas imagens não é invalidada. O Formulário adaptável continua mostrando imagens mais antigas.

Para resolver o problema, após a publicação das imagens e do vídeo, cancele explicitamente a publicação e publique o Forms adaptável que faz referência a esses ativos.

## Alguns Forms adaptáveis que contêm fragmento de conteúdo ou fragmentos de experiência não são invalidados automaticamente do cache do Dispatcher {#content-fragments-experience-fragments-not-invalidated}

Você pode adicionar um fragmento de conteúdo ou um fragmento de experiência a um formulário adaptável. Quando esses fragmentos são editados e publicados independentemente, a versão em cache de um Formulário adaptável que contém esses fragmentos não é invalidada. O Formulário adaptável continua mostrando fragmentos mais antigos.

Para resolver o problema, após publicar o fragmento de conteúdo ou o fragmento de experiência atualizado, desfaça explicitamente a publicação e publique o Forms adaptável que usa esses ativos.

## Somente a primeira instância do Forms adaptável é armazenada em cache {#only-first-instance-cached}

Quando a URL do Formulário adaptável não contiver nenhuma informação de localização e a opção Usar localidade do navegador no gerenciador de configurações estiver habilitada, uma versão localizada do Formulário adaptável será fornecida e uma instância do Formulário adaptável, com base na primeira solicitação (localidade do navegador solicitada), será armazenada em cache e entregue a cada usuário subsequente.

Execute as seguintes etapas para resolver o problema:

1. Abra o projeto Experience Manager.
1. Abra o `dispatcher/scr/conf.d/rewrites/rewrite.rules` para edição.
1. Abra o `conf.d/httpd-dispatcher.conf` ou qualquer outro arquivo de configuração configurado para ser carregado no tempo de execução.
1. Adicione o código a seguir ao arquivo e salve-o. É uma amostra de código, modifique-a para atender ao seu ambiente.

```shellscript
    # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
    
    # Handle selector-based redirection based on browser language
    <VirtualHost *:80>
            # Handle actual URL convention (just pass through)
    RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]

    # Handle selector based redirection basded on browser language
    # The Rewrite Condition is looking for the Accept-Language header and if found takes the first two characters which most likely are the desired language selector.
    RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
    RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
```

## O armazenamento em cache do CDN para de funcionar após 300 segundos {#cdn-caching-stops-working-after-300-seconds}

O armazenamento em cache do CDN para de funcionar após 300 segundos e todas as solicitações para armazenar em cache no CDN são redirecionadas para o Dispatcher.

Para resolver o problema, defina o cabeçalho de idade como 0:

1. Criar um arquivo em `src\conf.d\available_vhosts`

1. Adicione o seguinte ao arquivo para definir o cabeçalho da página

   ```shellscript
       <IfModule mod_headers.c>
               Header add X-Vhost "publish"
               Header set age 0
       </IfModule>
   ```

1. Salvar e fechar o arquivo.
1. Modificar o link flexível para `src\conf.d\enabled_vhosts\default.vhost` para apontar para o novo arquivo.
