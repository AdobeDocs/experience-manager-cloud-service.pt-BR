---
title: Como incorporar o formulário adaptável a uma página da Web externa?
description: Saiba como incorporar uma Forms adaptável a um site.
topic-tags: author
feature: Adaptive Forms
source-git-commit: 2d4a81aa0d6755270d4d6efb8649782f4bde4537
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 2%

---

# Incorporar formulário adaptável na página externa da Web{#embed-adaptive-form-in-external-web-page}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-external-web-page.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Você pode [incorporar formulários adaptáveis em uma página do AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md) ou uma página da Web hospedada fora do AEM. O formulário adaptável incorporado é totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ele ajuda o usuário a permanecer no contexto de outros elementos na página da Web e interagir simultaneamente com o formulário.

## Pré-requisitos {#prerequisites}

Execute as seguintes etapas antes de incorporar um formulário adaptável a um site externo

* Publique o formulário adaptável a ser incorporado à instância de publicação do AEM Forms Server.
* Crie ou identifique uma página da Web em seu site onde você possa hospedar o formulário adaptável. Certifique-se de que a página da Web possa [ler arquivos jQuery de um CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) ou tem uma cópia local do jQuery incorporado. O jQuery é necessário para renderizar um formulário adaptável.
* Quando o servidor AEM e a página da Web estiverem em domínios diferentes, execute as etapas listadas na seção, [permitir que o AEM Forms forneça formulários adaptáveis a um site entre domínios](#cross-site).

## Incorporar formulário adaptável {#embed-adaptive-form}

Você pode incorporar um formulário adaptável inserindo algumas linhas de JavaScript na página da Web. A API no código envia uma solicitação HTTP ao servidor AEM para recursos de formulários adaptáveis e injeta o formulário adaptável no contêiner de formulários especificado.

Para incorporar o formulário adaptável:

1. Crie uma página da Web em seu site com o seguinte código:

   ```html
   <!doctype html>
   <html>
     <head>
       <title>This is the title of the webpage!</title>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
     </head>
     <body>
     <div class="customafsection"/>
       <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
       if(options.path) {
           // options.path refers to the path of the adaptive form
           // For Example: /content/forms/af/ABC, where ABC is the adaptive form
           // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
           var path = options.path;
           path += "/jcr:content/guideContainer.html";
           $.ajax({
               url  : path ,
               type : "GET",
               data : {
                   // Set the wcmmode to be disabled
                   wcmmode : "disabled"
                   // Set the data reference, if any
                  // "dataRef": options.dataRef
                   // Specify a different theme for the form object
                 //  "themeOverride" : options.themepath
               },
               async: false,
               success: function (data) {
                   // If jquery is loaded, set the inner html of the container
                   // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                   // For example: document.getElementById().innerHTML
                   if(window.$ && options.CSS_Selector){
                       // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                       $(options.CSS_Selector).html(data);
                   }
               },
               error: function (data) {
                   // any error handler
               }
           });
       } else {
           if (typeof(console) !== "undefined") {
               console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
           }
       }
    }(options);
   
    </script>
     </body>
   </html>
   ```

1. No código incorporado:

   * Altere o valor de *options.path* com o caminho da URL de publicação do formulário adaptável. Se o servidor AEM estiver sendo executado em um caminho de contexto, verifique se o URL inclui o caminho de contexto. Sempre mencione o nome completo do formulário adaptável, incluindo a extensão. Por exemplo, o código acima e o formulário adaptável residem no mesmo AEM Forms Server, de modo que o exemplo usa o caminho de contexto do formulário adaptável `/content/forms/af/locbasic.html`.
   * Substituir *options.dataRef* com atributos a serem transmitidos com o URL. Você pode usar a variável dataref para [preencher previamente um formulário adaptável](/help/forms/prepopulate-adaptive-form-fields.md).
   * Substituir *options.themePath* com o caminho para um tema diferente do tema configurado no formulário adaptável. Como alternativa, você pode especificar o caminho do tema usando o atributo de solicitação.
   * CSS_Selector é o seletor de CSS do container de formulário no qual o formulário adaptável está incorporado. Por exemplo, a classe css .customafsection é o seletor de CSS no exemplo acima.

O formulário adaptável é incorporado na página da Web. Observe o seguinte no formulário adaptável incorporado:

* O cabeçalho e o rodapé no formulário adaptável original não estão incluídos no formulário incorporado.
* Rascunhos e formulários enviados estão disponíveis na guia Rascunhos e envios no Portal do Forms.
* A ação Enviar configurada no formulário adaptável original é retida no formulário incorporado.
* As regras de formulário adaptáveis são mantidas e totalmente funcionais no formulário incorporado.
* O Direcionamento de experiência e os testes A/B configurados no formulário adaptável original não funcionam no formulário incorporado.
* Se o Adobe Analytics estiver configurado no formulário original, os dados de análise serão capturados pelo servidor do Adobe Analytics. No entanto, não está disponível no relatório de análise do Forms.

## Topologia de exemplo {#sample-topology}

A página externa da Web que incorpora o formulário adaptável envia solicitações para o servidor AEM, que normalmente fica atrás do firewall em uma rede privada. Para garantir que as solicitações sejam direcionadas com segurança ao servidor AEM, é recomendável configurar um servidor proxy reverso.

Vamos ver um exemplo de como configurar um servidor proxy reverso do Apache 2.4 sem um Dispatcher. Neste exemplo, você está hospedando o servidor AEM com `/forms` caminho e mapa do contexto `/forms` para o proxy reverso. Assegura que qualquer pedido de `/forms` no servidor Apache são direcionados à instância AEM. Essa topologia ajuda a reduzir o número de regras na camada do Dispatcher como todas as solicitações com prefixo `/forms` para o servidor AEM.

1. Abra o `httpd.conf` e remova o comentário das linhas de código a seguir. Como alternativa, você pode adicionar essas linhas de código no arquivo.

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. Configure regras de proxy adicionando as seguintes linhas de código na `httpd-proxy.conf` arquivo de configuração.

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   Substituir `[AEM_Instance]` com o URL de publicação do servidor AEM nas regras.

Se você não montar o servidor AEM em um caminho de contexto, as regras de proxy na camada do Apache são as seguintes:

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>Se você configurar qualquer outra topologia, adicione o envio, o preenchimento prévio e outros URLs ao arquivo de inclui na lista de permissões na camada do Dispatcher.

## Práticas recomendadas {#best-practices}

Ao incorporar um formulário adaptável em uma página da Web, considere as seguintes práticas recomendadas:

* Certifique-se de que as regras de estilo definidas no CSS da página da Web não estejam em conflito com o CSS do objeto de formulário. Para evitar os conflitos, você pode reutilizar o CSS da página da Web no tema de formulário adaptável usando a biblioteca do cliente AEM. Para obter informações sobre como usar a biblioteca do cliente em temas de formulários adaptáveis, consulte [Temas no AEM Forms](/help/forms/themes.md).
* Faça com que o container do formulário na página da Web use toda a largura da janela. Ela garante que as regras CSS configuradas para dispositivos móveis funcionem sem alterações. Se o contêiner de formulário não ocupa toda a largura da janela, você deve gravar CSS personalizado para fazer o formulário se adaptar a diferentes dispositivos móveis.
* Uso `[getData](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/GuideBridge.html)` API para obter a representação XML ou JSON dos dados de formulário no cliente.
* Uso `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/GuideBridge.html)` API para descarregar o formulário adaptável do DOM do HTML.
* Configurar o cabeçalho access-control-origin ao enviar uma resposta de um servidor AEM.

## Permitir que o AEM Forms forneça formulários adaptáveis a um site entre domínios {#cross-site}

1. Na instância de publicação do AEM, acesse o Gerenciador de configuração do console da Web AEM em `https://'[server]:[port]'/system/console/configMgr`.
1. Localize e abra o **Filtro referenciador do Apache Sling** configuração.
1. No campo Hosts permitidos, especifique o domínio em que reside a página da Web. Ela permite que o host faça solicitações de POST para o servidor AEM. Você também pode usar expressões regulares para especificar uma série de domínios de aplicativos externos.

>[!MORELIKETHIS]
>
>* [Incorporar formulário adaptável baseado nos Componentes principais a uma página da Web externa](/help/forms/embed-adaptive-form-core-components-external-web-page.md)
