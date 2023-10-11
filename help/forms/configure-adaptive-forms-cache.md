---
title: O que é o cache de formulários adaptáveis? e como armazenar em cache um formulário adaptável para AEM?
description: O cache do Adaptive Forms foi projetado para o Adaptive Forms e documentos com o objetivo de reduzir o tempo necessário para renderizar um Formulário ou documento adaptável.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 1%

---


# Configurar cache adaptável do Forms {#configure-adaptive-forms-cache}

Um cache é um mecanismo para reduzir os tempos de acesso aos dados, reduzir a latência e melhorar as velocidades de entrada/saída (E/S). O cache do Adaptive Forms armazena somente o conteúdo HTML e a estrutura JSON de um Formulário adaptável sem salvar os dados pré-preenchidos. Ajuda a reduzir o tempo necessário para renderizar um Formulário adaptável no cliente. Ele foi projetado especificamente para o Adaptive Forms.

## Configurar o cache do Adaptive Forms nas instâncias de criação e publicação {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vá para o gerenciador de configuração do console da Web do AEM em `https://[server]:[port]/system/console/configMgr`.
1. Clique em **[!UICONTROL Configuração do canal da Web do formulário adaptável e da comunicação interativa]** para editar os valores de configuração.
1. No [!UICONTROL editar valores de configuração] especificar o número máximo de formulários ou documentos para uma instância do AEM [!DNL Forms Server] pode armazenar em cache no **[!UICONTROL Número de Forms adaptáveis]** campo. O valor padrão é 100.

   >[!NOTE]
   >
   >Para desativar o cache, defina o valor no campo Número de Forms adaptáveis como **0**. O cache é redefinido e todos os formulários e documentos são removidos do cache quando você desativa ou altera a configuração do cache.

   ![Caixa de diálogo de configuração para o cache de HTML do Adaptive Forms](assets/cache-configuration-edit.png)

1. Clique em **[!UICONTROL Salvar]** para salvar a configuração.

Seu ambiente está configurado para usar o Forms adaptável em cache e ativos relacionados.


## (Opcional) Configurar o cache do formulário adaptável no Dispatcher {#configure-the-cache}

Você também pode configurar o armazenamento em cache do formulário adaptável no Dispatcher para aumentar ainda mais o desempenho.

### Pré-requisitos {#pre-requisites}

* Ativar o [mesclar ou preencher previamente os dados no cliente](prepopulate-adaptive-form-fields.md#prefill-at-client) opção. Ele ajuda a mesclar dados exclusivos para cada instância de um formulário pré-preenchido.
* [Ativar um agente de limpeza para cada instância de publicação](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance). Ele ajuda a obter melhor desempenho de cache do Adaptive Forms. O URL padrão dos agentes de limpeza é `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Considerações para armazenamento em cache do Adaptive Forms em um Dispatcher {#considerations}

* Ao usar o cache do Adaptive Forms, use o AEM [!DNL Dispatcher] para armazenar em cache bibliotecas de clientes (CSS e JavaScript) de um Formulário adaptável.
* Ao desenvolver componentes personalizados, no servidor usado para desenvolvimento, mantenha o cache Adaptive Forms desativado.
* Os URLs sem extensão não são armazenados em cache. Por exemplo, URL com padrão `/content/forms/[folder-structure]/[form-name].html` são armazenados em cache e o armazenamento em cache ignora URLs com padrão `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Portanto, use URLs com extensões para aproveitar os benefícios do armazenamento em cache.
* Considerações para o Forms adaptável localizado:
   * Usar formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar uma versão localizada de um Formulário adaptável em vez de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Desativar usando localidade do navegador <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->para URLs com formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Quando você usa o formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`, e **[!UICONTROL Usar localidade do navegador]** no gerenciador de configurações estiver desativado, a versão não localizada do Formulário adaptável será fornecida. O idioma não localizado é o idioma usado ao desenvolver o Formulário adaptável. A localidade configurada para seu navegador (localidade do navegador) não é considerada e uma versão não localizada do Formulário adaptável é fornecida.
   * Quando você usa o formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`, e **[!UICONTROL Usar localidade do navegador]** no gerenciador de configurações estiver ativado, uma versão localizada do Formulário adaptável será fornecida, se disponível. O idioma do Formulário adaptável localizado se baseia no local configurado para seu navegador (local do navegador). Pode levar a [armazenamento em cache somente da primeira instância de um Formulário adaptável]. Para evitar que o problema ocorra na sua instância, consulte [solução de problemas](#only-first-insatnce-of-adptive-forms-is-cached).

### Ativar o cache no Dispatcher

Execute as etapas listadas abaixo para habilitar e configurar o armazenamento em cache do Adaptive Forms no Dispatcher:

1. Abra o seguinte URL para cada instância de publicação do seu ambiente e configure o agente de replicação:
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

   * Um formulário adaptável permanece no cache até que uma versão atualizada do formulário não seja publicada.

   * Quando uma versão mais recente de um recurso referenciado em um Formulário adaptável é publicada, o Formulário adaptável afetado é invalidado automaticamente. Há algumas exceções à invalidação automática de recursos referenciados. Para obter uma solução alternativa para as exceções, consulte [solução de problemas](#troubleshooting) seção.
1. [Adicione o arquivo de regras dispatcher.any abaixo ou um arquivo de regras personalizado](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache). Ela exclui os URLs que não oferecem suporte ao armazenamento em cache. Por exemplo, Comunicação interativa.

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

1. [Adicionar os seguintes parâmetros à lista para ignorar parâmetros de URL](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

Seu ambiente AEM está configurado para armazenar em cache o Adaptive Forms. Ele armazena em cache todos os tipos de Forms adaptável. Se você precisar verificar as permissões de acesso do usuário para uma página antes de entregar a página em cache, consulte [armazenamento em cache de conteúdo protegido](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=pt-BR).

## Resolução de problemas {#troubleshooting}

### Alguns Forms adaptáveis contendo imagens ou vídeos não são invalidados automaticamente do cache do Dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Ao selecionar e adicionar imagens ou vídeos por meio do navegador de ativos a um Formulário adaptável e eles forem editados no editor de ativos, esses ativos não são invalidados automaticamente do cache do Dispatcher.

#### Solução {#Solution1}

Após a publicação das imagens e do vídeo, cancele explicitamente a publicação e publique o Forms adaptável que faz referência a esses ativos.

### Alguns Forms adaptáveis que contêm fragmento de conteúdo ou fragmentos de experiência não são invalidados automaticamente do cache do Dispatcher {#content-or-experience-fragment-not-auto-invalidated}

#### Problema {#issue2}

Quando você adiciona um fragmento de conteúdo ou um Fragmento de experiência a um Formulário adaptável e esses ativos são editados e publicados de forma independente, o Forms adaptável que contém esses ativos não é invalidado do cache do Dispatcher automaticamente.

#### Solução {#Solution2}

Depois de publicar um fragmento de conteúdo ou fragmento de experiência atualizado, cancele explicitamente a publicação e publique o Forms adaptável que usa esses ativos.

### Somente a primeira instância de um formulário adaptável é armazenada em cache{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problema {#issue3}

Quando a URL do formulário adaptável não tiver informações de localização e **[!UICONTROL Usar localidade do navegador]** no gerenciador de configurações está habilitado. Uma versão localizada do Formulário adaptável é fornecida e somente a primeira instância do Formulário adaptável é armazenada em cache e entregue a cada usuário subsequente.

#### Solução {#Solution3}

1. Abra o arquivo conf.d/httpd-dispatcher.conf ou qualquer outro arquivo de configuração configurado para ser carregado no tempo de execução.

1. Adicione o código a seguir ao arquivo e salve-o. É uma amostra de código, modifique-a para atender ao seu ambiente.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two characters which most likely is the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
