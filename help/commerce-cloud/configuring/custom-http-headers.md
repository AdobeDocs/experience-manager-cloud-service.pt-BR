---
title: Cabeçalhos HTTP personalizados
description: Saiba como configurar cabeçalhos HTTP personalizados que serão enviados para o mecanismo de comércio, juntamente com aqueles já enviados pelo CIF.
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
feature: Commerce Integration Framework
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# Cabeçalhos HTTP personalizados {#custom-http-headers}

## Visão geral {#overview}

Para obter mais controle sobre o back-end, os autores podem configurar cabeçalhos HTTP personalizados que seriam enviados ao mecanismo de comércio, juntamente com aqueles já enviados pelo CIF. Casos de uso comuns incluem configurações de várias lojas nas quais você pode usar cabeçalhos HTTP para controlar a resposta do back-end de comércio.

>[!NOTE]
>
>Os desenvolvedores sempre podem configurar cabeçalhos HTTP personalizados usando a configuração do cliente GraphQL.
>

## Configuração {#configuration}

Para configurar os cabeçalhos HTTP personalizados, é necessário primeiro defini-los. Os cabeçalhos HTTP personalizados devem ser definidos primeiro adicionando-os à configuração do serviço `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` usando uma configuração OSGi.

Você pode configurar os valores dos cabeçalhos HTTP na página Configuração de Cloud Service do seu projeto:

1. Acesse a página de configuração do Cloud Service em Ferramentas > Cloud Services > Configuração do CIF
1. Abrir uma configuração existente ou criar uma
1. Vá para a guia &quot;Avançado&quot; e localize o multicampo &quot;Cabeçalhos HTTP personalizados&quot;. Você pode selecionar os cabeçalhos definidos anteriormente e atribuir valores a eles.

Os componentes que usam a configuração do Cloud Service acima enviarão esses cabeçalhos HTTP com cada solicitação do GraphQL.

## Restrições {#restrictions}

Embora o serviço permita a definição de qualquer nome de cabeçalho, incluindo os padrão, eles não estarão disponíveis para configuração. Em outras palavras, não é possível substituir os cabeçalhos HTTP padrão usando esse recurso. Uma lista de nomes de cabeçalho restritos pode ser encontrada em [mdn web docs - HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Além desses, há mais dois cabeçalhos que não podem ser usados:

* &quot;Loja&quot; - usado pelo CIF para identificar a loja da Adobe Commerce
* &quot;Versão de visualização&quot; - usado pelo CIF para recuperar produtos preparados
