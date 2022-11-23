---
title: Páginas de erro personalizadas
description: AEM vem com um manipulador de erros padrão para lidar com erros HTTP, que podem ser personalizados.
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: db997127c6cbba434b86990852d1ba590d5f12a5
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 2%

---

# Personalização de páginas de erro {#customizing-error-pages}

AEM vem com um manipulador de erros padrão para lidar com erros HTTP; por exemplo, mostrando:

![Mensagem de erro padrão](assets/error-message-standard.png)

Para responder a erros, AEM fornece uma `404.jsp` script em `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Como o AEM é baseado no Apache Sling, mais informações estão disponíveis [na documentação de tratamento de erros do Apache.](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>Em uma instância do autor, [Filtro de depuração do CQ WCM](/help/implementing/deploying/configuring-osgi.md) está ativada por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento completo da pilha na resposta.
>
>Em uma instância de publicação, o Filtro de depuração do CQ WCM é **always** desativado (mesmo se configurado como ativado).

## Como personalizar páginas exibidas pelo manipulador de erros {#how-to-customize-pages-shown-by-the-error-handler}

Você pode desenvolver seus próprios scripts para personalizar as páginas mostradas pelo manipulador de erros quando um erro for encontrado. Para fazer isso, você aproveitará [AEM mecanismo de sobreposição padrão](/help/implementing/developing/introduction/overlays.md) para que suas páginas personalizadas sejam criadas em `/apps` e sobrepor as páginas padrão que estão em `/libs`.

1. No repositório, copie os scripts padrão:

   * de `/libs/sling/servlet/errorhandler/`
   * para `/apps/sling/servlet/errorhandler/`

   O caminho de destino não existe por padrão, portanto, será necessário criá-lo ao fazer isso pela primeira vez.

1. Vá até `/apps/sling/servlet/errorhandler`. Aqui você pode:

   * edite o script existente apropriado para fornecer as informações necessárias. Ou
   * crie e edite um novo script para o código necessário.

1. Salve as alterações e teste.

>[!CAUTION]
>
>O `404.jsp` O script foi especificamente concebido para servir AEM autenticação; em particular, para permitir o login do sistema no caso desses erros.
>
>Portanto, a substituição deste script deve ser feita com muito cuidado.

### Personalização da resposta a erros HTTP 500 {#customizing-the-response-to-http-errors}

O HTTP [Erro interno do servidor 500](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indica um erro do lado do servidor, como o servidor encontrando uma condição inesperada que o impedia de atender à solicitação.

Quando o processamento da solicitação resulta em uma exceção, a estrutura do Apache Sling (que AEM é criada):

* Registra a exceção
* E retorna ao corpo da resposta:
   * O código de resposta HTTP 500
   * O rastreamento da pilha de exceções

Por [personalização das páginas mostradas pelo manipulador de erros](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` é possível criar um script. No entanto, ele só será usado se `HttpServletResponse.sendError(500)` é executado explicitamente; ou seja, de um apanhador de exceções.

Caso contrário, o código de resposta será definido como 500, mas a variável `500.jsp` script não é executado.

Para lidar com erros 500, o nome do arquivo do script do manipulador de erros deve ser igual à classe de exceção (ou superclasse). Para lidar com todas essas exceções, é possível criar um script `/apps/sling/servlet/errorhandler/Throwable.jsp` ou `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>No AEM como Cloud Service, a CDN serve uma página de erro genérica sempre que um erro 5XX é recebido do back-end. Para permitir que a resposta real do back-end passe por você precisa adicionar o seguinte cabeçalho à resposta:
>`x-aem-error-pass: true`
>Isso funcionará somente para respostas provenientes de AEM ou da camada do Apache/Dispatcher. Outros erros inesperados provenientes de camadas de infraestrutura intermediárias ainda exibirão a página de erro genérica.

>[!CAUTION]
>
>Em uma instância do autor, [Filtro de depuração do CQ WCM](/help/implementing/deploying/configuring-osgi.md) está ativada por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento completo da pilha na resposta.
>
>Para um manipulador de erros personalizado, as respostas com código 500 são necessárias, portanto, a variável [O filtro de depuração do CQ WCM precisa ser desativado.](/help/implementing/deploying/configuring-osgi.md) Isso garante que o código de resposta 500 seja retornado, o que, por sua vez, aciona o manipulador de erros do Sling correto.
>
>Em uma instância de publicação, o Filtro de depuração do CQ WCM é **always** desativado (mesmo se configurado como ativado).
