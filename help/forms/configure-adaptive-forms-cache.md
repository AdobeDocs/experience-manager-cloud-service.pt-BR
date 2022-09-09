---
title: Configurar o cache adaptável do Forms
seo-title: Configure Adaptive Forms cache
description: O cache do Adaptive Forms foi projetado especificamente para documentos e Forms adaptativos. Armazena em cache o Adaptive Forms e documentos adaptáveis com o objetivo de reduzir o tempo necessário para renderizar um formulário ou documento adaptável no cliente.
seo-description: The Adaptive Forms cache is designed specifically for Adaptive Forms and documents. It caches Adaptive Forms and adaptive documents with the objective of reducing the time required to render an Adaptive Form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 1%

---


# Configurar o cache adaptável do Forms {#configure-adaptive-forms-cache}

Um cache é um mecanismo para reduzir o tempo de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (I/O). O cache adaptável do Forms armazena somente o conteúdo de HTML e a estrutura JSON de um formulário adaptável sem salvar os dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um formulário adaptável no cliente. Foi projetado especificamente para o Adaptive Forms.

## Configurar o cache do Adaptive Forms nas instâncias de criação e publicação {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vá para AEM gerenciador de configuração do console da Web em `https://[server]:[port]/system/console/configMgr`.
1. Clique em **[!UICONTROL Configuração do canal Web de comunicação interativa e formulário adaptável]** para editar seus valores de configuração.
1. No [!UICONTROL editar valores de configuração] , especifique o número máximo de formulários ou documentos que uma instância do AEM [!DNL Forms] O servidor pode armazenar em cache no **[!UICONTROL Número de Forms adaptáveis]** campo. O valor padrão é 100.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Number of Adaptive Forms como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

   ![Caixa de diálogo Configuração do cache do HTML Adaptive Forms](assets/cache-configuration-edit.png)

1. Clique em **[!UICONTROL Salvar]** para salvar a configuração.

Seu ambiente é configurado para usar o cache Adaptive Forms e ativos relacionados.


## (Opcional) Configurar o cache do formulário adaptável no dispatcher {#configure-the-cache}

Você também pode configurar o armazenamento em cache do Adaptive Form no Dispatcher para aumentar ainda mais o desempenho.

### Pré-requisitos {#pre-requisites}

* Ative o [mesclagem ou preenchimento prévio de dados no cliente](prepopulate-adaptive-form-fields.md#prefill-at-client) opção. Ajuda a unir dados exclusivos para cada instância de um formulário pré-preenchido.
* [Habilitar agente de limpeza para cada instância de publicação](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance). Ele ajuda a melhorar o desempenho do armazenamento em cache do Adaptive Forms. O URL padrão dos agentes de limpeza é `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Considerações para o armazenamento em cache do Adaptive Forms em um dispatcher {#considerations}

* Ao usar o cache do Adaptive Forms, use o AEM [!DNL Dispatcher] para armazenar em cache as bibliotecas de clientes (CSS e JavaScript) de um formulário adaptável.
* Ao desenvolver componentes personalizados, no servidor usado para desenvolvimento, mantenha o cache do Adaptive Forms desativado.
* URLs sem extensão não são armazenados em cache. Por exemplo, URL com padrão`/content/forms/[folder-structure]/[form-name].html` são armazenadas em cache e o armazenamento em cache ignora URLs com padrão `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Portanto, use URLs com extensões para aproveitar os benefícios do armazenamento em cache.
* Considerações para Forms adaptável localizado:
   * Usar formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Desabilitar usando a localidade do navegador <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->para URLs com formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Ao usar o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`e **[!UICONTROL Usar a localidade do navegador]** no gerenciador de configuração estiver desativado, a versão não localizada do Formulário adaptável será disponibilizada. O idioma não localizado é o idioma usado durante o desenvolvimento do Formulário adaptável. O local configurado para seu navegador (localidade do navegador) não é considerado e uma versão não localizada do formulário adaptativo é disponibilizada.
   * Ao usar o Formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`e **[!UICONTROL Usar a localidade do navegador]** no gerenciador de configuração estiver ativado, uma versão localizada do Formulário adaptável será disponibilizada, se disponível. O idioma do formulário adaptável localizado é baseado na localidade configurada para seu navegador (localidade do navegador). Pode levar a [armazenamento em cache somente da primeira instância de um formulário adaptável]. Para evitar que o problema ocorra em sua instância, consulte [solução de problemas](#only-first-insatnce-of-adptive-forms-is-cached).

### Habilitar o armazenamento em cache no dispatcher

Execute as etapas listadas abaixo para ativar e configurar o armazenamento em cache do Adaptive Forms no dispatcher:

1. Abra o seguinte URL para cada instância de publicação do ambiente e configure o agente de replicação:
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Adicione o seguinte ao arquivo dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#automatically-invalidating-cached-files):

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   Ao adicionar o acima:

   * Um formulário adaptável permanece em cache até que uma versão atualizada do formulário não seja publicada.

   * Quando uma versão mais recente do recurso referenciado em um Formulário adaptável é publicada, o Adaptive Forms afetado é automaticamente invalidado. Há algumas exceções para a invalidação automática dos recursos referenciados. Para obter uma solução alternativa para exceções, consulte [solução de problemas](#troubleshooting) seção.
1. [Adicione o arquivo de regras abaixo dispatcher.any ou personalizado](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache). Ela exclui os URLs que não oferecem suporte ao armazenamento em cache. Por exemplo, Comunicação interativa.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Adicione os seguintes parâmetros à lista ignorar parâmetros de URL](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Seu ambiente de AEM está configurado para armazenar em cache o Adaptive Forms. Armazena em cache todos os tipos de Adaptive Forms. Se você tiver um requisito para verificar as permissões de acesso do usuário para uma página antes de entregar a página em cache, consulte [armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Resolução de problemas {#troubleshooting}

### Alguns Forms adaptáveis que contêm imagens ou vídeos não são invalidados automaticamente do cache do dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Quando você seleciona e adiciona imagens ou vídeos por meio do navegador de ativos a um Formulário adaptável e essas imagens e vídeos são editados no editor de Ativos, o Adaptive Forms que contém essas imagens não é invalidado do cache do dispatcher automaticamente.

#### Solução {#Solution1}

Após publicar as imagens e o vídeo, desfaça a publicação e publique explicitamente o Adaptive Forms que faz referência a esses ativos.

### Alguns fragmentos de conteúdo ou de experiência do Adaptive Forms que contêm fragmento de conteúdo não são invalidados automaticamente do cache do dispatcher {#content-or-experience-fragment-not-auto-invalidated}

#### Problema {#issue2}

Quando você adiciona um fragmento de conteúdo ou um fragmento de experiência a um formulário adaptável e esses ativos são editados e publicados de maneira independente, o Adaptive Forms que contém esses ativos não é invalidado do cache do dispatcher automaticamente.

#### Solução {#Solution2}

Após publicar o fragmento de conteúdo ou fragmento de experiência atualizado, desfaça a publicação e publique explicitamente o Adaptive Forms que usa esses ativos.

### Somente a primeira instância de um formulário adaptável é armazenada em cache{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problema {#issue3}

Quando o URL do formulário adaptável não tiver informações de localização, e **[!UICONTROL Usar a localidade do navegador]** no gerenciador de configuração estiver ativado, uma versão localizada do formulário adaptável será disponibilizada e somente a primeira instância do formulário adaptável será armazenada em cache e entregue a cada usuário subsequente.

#### Solução {#Solution3}

Execute as seguintes etapas para resolver o problema:

1. Abra o conf.d/httpd-dispatcher.conf ou qualquer outro arquivo de configuração configurado para carregar no tempo de execução.

1. Adicione o seguinte código ao arquivo e salve-o. É um código de amostra para modificá-lo de acordo com seu ambiente.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
