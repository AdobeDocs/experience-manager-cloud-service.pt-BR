---
title: Páginas de erro personalizadas
description: O AEM vem com um manipulador de erros padrão para lidar com erros HTTP, que pode ser personalizado.
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Personalização de Páginas de Erro {#customizing-error-pages}

O AEM vem com um manipulador de erros padrão para lidar com erros HTTP; por exemplo, mostrando:

![Mensagem de erro padrão](assets/error-message-standard.png)

Para responder a erros, a AEM fornece um script `404.jsp` em `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>Como o AEM é baseado no Apache Sling, há mais informações disponíveis [na documentação de tratamento de erros do Apache](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html).

>[!NOTE]
>
>Em uma instância de autor, o [Filtro de Depuração WCM do CQ](/help/implementing/deploying/configuring-osgi.md) está habilitado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento de pilha completa na resposta.
>
>Em uma instância de publicação, o Filtro de Depuração CQ WCM está **sempre** desabilitado (mesmo se configurado como habilitado).

>[!NOTE]
>
>Para obter mais informações sobre a manipulação de erros com o Dispatcher, consulte [Configurando Páginas de Erro da CDN](/help/implementing/dispatcher/cdn-error-pages.md).

## Como personalizar páginas mostradas pelo manipulador de erros {#how-to-customize-pages-shown-by-the-error-handler}

Você pode desenvolver seus próprios scripts para personalizar as páginas mostradas pelo manipulador de erros quando um erro for encontrado. Para fazer isso, você usa o [mecanismo de sobreposição padrão do AEM](/help/implementing/developing/introduction/overlays.md) para que suas páginas personalizadas sejam criadas em `/apps` e sobreponham as páginas padrão em `/libs`.

1. No repositório, copie o(s) script(s) padrão:

   * de `/libs/sling/servlet/errorhandler/`
   * para `/apps/sling/servlet/errorhandler/`

   O caminho de destino não existe por padrão, portanto, é necessário criá-lo ao fazer isso pela primeira vez.

1. Navegue até `/apps/sling/servlet/errorhandler`. Aqui é possível:

   * edite o script existente apropriado para fornecer as informações necessárias. Ou
   * crie e edite um novo script para o código necessário.

1. Salve as alterações e teste.

>[!CAUTION]
>
>O script `404.jsp` foi projetado especificamente para atender à autenticação do AEM; especificamente, para permitir o logon do sistema no caso desses erros.
>
>Portanto, a substituição desse script deve ser feita com muito cuidado.

### Personalização da resposta a erros HTTP 500 {#customizing-the-response-to-http-errors}

O HTTP [500 Erro Interno do Servidor](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) indica um erro do lado do servidor, como o servidor ter encontrado uma condição inesperada que o impediu de atender à solicitação.

Quando o processamento de solicitações resulta em uma exceção, a estrutura Apache Sling (na qual o AEM é construído):

* Registra a exceção
* E retorna no corpo da resposta:
   * O código de resposta HTTP 500
   * O rastreamento de pilha de exceção

Com a [personalização das páginas mostradas pelo manipulador de erros](#how-to-customize-pages-shown-by-the-error-handler), um script `500.jsp` pode ser criado. No entanto, ele só é usado se `HttpServletResponse.sendError(500)` for executado explicitamente; ou seja, a partir de um capturador de exceção.

Caso contrário, o código de resposta será definido como 500, mas o script `500.jsp` não será executado.

Para tratar erros 500, o nome de arquivo do script do manipulador de erros deve ser igual à classe de exceção (ou superclasse). Para lidar com todas essas exceções você pode criar um script `/apps/sling/servlet/errorhandler/Throwable.jsp` ou `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>No AEM as Cloud Service, o CDN fornece uma página de erro genérica quando um erro 5XX é recebido do back-end. Para permitir a passagem da resposta real do back-end, é necessário adicionar o seguinte cabeçalho à resposta: `x-aem-error-pass: true`.
>Isso funciona somente para respostas provenientes do AEM ou da camada Apache/Dispatcher. Outros erros inesperados provenientes de camadas de infraestrutura intermediária ainda exibirão a página de erro genérico.

>[!CAUTION]
>
>Em uma instância de autor, o [Filtro de Depuração WCM do CQ](/help/implementing/deploying/configuring-osgi.md) está habilitado por padrão. Isso sempre resulta no código de resposta 200. O manipulador de erros padrão responde gravando o rastreamento de pilha completa na resposta.
>
>Para um manipulador de erros personalizado, são necessárias respostas com o código 500; portanto, o [Filtro de Depuração WCM do CQ deve ser desabilitado](/help/implementing/deploying/configuring-osgi.md). Isso garante que o código de resposta 500 seja retornado, o que, por sua vez, aciona o manipulador de erros Sling correto.
>
>Em uma instância de publicação, o Filtro de Depuração CQ WCM está **sempre** desabilitado (mesmo se configurado como habilitado).
