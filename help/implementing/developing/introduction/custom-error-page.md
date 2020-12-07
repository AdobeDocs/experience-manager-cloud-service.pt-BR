---
title: Páginas de erro personalizadas
description: AEM vem com um manipulador de erros padrão para lidar com erros HTTP, que podem ser personalizados.
translation-type: tm+mt
source-git-commit: d7e9bdee83f1b85436185ca57420ee178268cb33
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Personalizando páginas de erro {#customizing-error-pages}

AEM vem com um manipulador de erros padrão para lidar com erros HTTP; por exemplo, mostrando:

![Mensagem de erro padrão](assets/error-message-standard.png)

Para responder a erros, AEM fornece um script `404.jsp` em `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Como o AEM é baseado no Apache Sling, mais informações estão disponíveis [na documentação de tratamento de erros do Apache.](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>Em uma instância do autor, [CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) está ativado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento completo da pilha na resposta.
>
>Em uma instância de publicação, o Filtro de Depuração do CQ WCM está **always** desativado (mesmo se configurado como ativado).

## Como personalizar páginas mostradas pelo manipulador de erros {#how-to-customize-pages-shown-by-the-error-handler}

Você pode desenvolver seus próprios scripts para personalizar as páginas mostradas pelo manipulador de erros quando um erro for encontrado. Para fazer isso, você aproveitará [AEM mecanismo de sobreposição padrão](/help/implementing/developing/introduction/overlays.md) para que suas páginas personalizadas sejam criadas em `/apps` e sobreponham as páginas padrão que estão em `/libs`.

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
>O script `404.jsp` foi projetado especificamente para atender à autenticação AEM; em particular, para permitir o logon do sistema no caso desses erros.
>
>Portanto, a substituição desse script deve ser feita com muito cuidado.

### Personalizando a resposta para erros HTTP 500 {#customizing-the-response-to-http-errors}

O HTTP [500 Internal Server Error](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indica um erro do lado do servidor, como o servidor que encontra uma condição inesperada que o impedia de atender à solicitação.

Quando o processamento da solicitação resulta em uma exceção, a estrutura Apache Sling (que AEM incorporada):

* Registra a exceção
* E retorna ao corpo da resposta:
   * O código de resposta HTTP 500
   * O rastreamento da pilha de exceções

Ao [personalizar as páginas mostradas pelo manipulador de erros](#how-to-customize-pages-shown-by-the-error-handler) é possível criar um script `500.jsp`. No entanto, ele só é usado se `HttpServletResponse.sendError(500)` for executado explicitamente; Ou seja, de um coletor de exceção.

Caso contrário, o código de resposta será definido como 500, mas o script `500.jsp` não será executado.

Para lidar com erros 500, o nome do arquivo do script do manipulador de erros deve ser o mesmo da classe de exceção (ou superclasse). Para lidar com todas essas exceções, você pode criar um script `/apps/sling/servlet/errorhandler/Throwable.jsp` ou `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>Em uma instância do autor, [CQ WCM Debug Filter](/help/implementing/deploying/configuring-osgi.md) está ativado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento completo da pilha na resposta.
>
>Para um manipulador de erros personalizado, as respostas com o código 500 são necessárias; portanto, o [Filtro de Depuração CQ WCM precisa ser desativado.](/help/implementing/deploying/configuring-osgi.md) Isso garante que o código de resposta 500 seja retornado, o que, por sua vez, aciona o manipulador de erros Sling correto.
>
>Em uma instância de publicação, o Filtro de Depuração do CQ WCM está **always** desativado (mesmo se configurado como ativado).
