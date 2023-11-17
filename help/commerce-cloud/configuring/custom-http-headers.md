---
title: Cabeçalhos HTTP personalizados
description: Saiba como configurar cabeçalhos HTTP personalizados que serão enviados para o mecanismo de comércio, juntamente com aqueles já enviados pelo CIF.
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 5%

---

# Cabeçalhos HTTP personalizados {#custom-http-headers}

## Visão geral {#overview}

Para obter mais controle sobre o back-end, os autores podem configurar cabeçalhos HTTP personalizados que seriam enviados ao mecanismo de comércio, juntamente com aqueles já enviados pelo CIF. Casos de uso comuns incluem configurações de várias lojas nas quais você pode usar cabeçalhos HTTP para controlar a resposta do back-end de comércio.

>[!NOTE]
>
>Os desenvolvedores sempre podem configurar cabeçalhos HTTP personalizados usando a configuração do cliente GraphQL.
>

## Configuração {#configuration}

Para configurar os cabeçalhos HTTP personalizados, é necessário primeiro defini-los. Os cabeçalhos HTTP personalizados devem ser definidos primeiro adicionando-os à `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` configuração do serviço usando uma configuração OSGi.

Você pode configurar os valores dos cabeçalhos HTTP na página Configuração de Cloud Service do seu projeto:

1. Acesse a página de configuração do Cloud Service em Ferramentas -> Cloud Services -> Configuração do CIF
1. Abrir uma configuração existente ou criar uma
1. Vá para a guia &quot;Avançado&quot; e localize o multicampo &quot;Cabeçalhos HTTP personalizados&quot;. Você pode selecionar os cabeçalhos definidos anteriormente e atribuir valores a eles.

Os componentes que usam a configuração do Cloud Service acima enviarão esses cabeçalhos HTTP com cada solicitação do GraphQL.

## Restrições {#restrictions}

Embora o serviço permita a definição de qualquer nome de cabeçalho, incluindo os padrão, eles não estarão disponíveis para configuração. Em outras palavras, não é possível substituir os cabeçalhos HTTP padrão usando esse recurso. Uma lista de nomes de cabeçalho restritos pode ser encontrada [aqui](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Headers). Além desses, há mais dois cabeçalhos que não podem ser usados:

* &quot;Loja&quot; - usado pelo CIF para identificar a loja da Adobe Commerce
* &quot;Versão de visualização&quot; - usado pelo CIF para recuperar produtos preparados
