---
title: Cabeçalhos HTTP personalizados
description: Configuração de cabeçalhos HTTP personalizados
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 3%

---

# Cabeçalhos HTTP personalizados {#custom-http-headers}

## Visão geral {#overview}

Para obter mais controle sobre o back-end, os autores podem configurar cabeçalhos HTTP personalizados que seriam enviados para o mecanismo de comércio, juntamente com os já enviados pela CIF. Casos de uso comuns incluem configurações de várias lojas nas quais você pode usar cabeçalhos HTTP para controlar a resposta do back-end de comércio.

>[!NOTE]
>
>Os desenvolvedores sempre podem configurar cabeçalhos HTTP personalizados usando a configuração de cliente GraphQL.

## Configuração {#configuration}

Para configurar os cabeçalhos HTTP personalizados, é necessário defini-los primeiro. Os cabeçalhos HTTP personalizados devem ser definidos primeiro, adicionando-os ao `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` configuração de serviço usando uma configuração OSGi.

Você pode configurar os valores dos cabeçalhos HTTP na página Configuração do Cloud Service para o seu projeto:

1. Vá para a página de configuração do Cloud Service em Ferramentas -> Cloud Services -> Configuração da CIF
1. Abra uma configuração existente ou crie uma nova
1. Vá para a guia &quot;Avançado&quot; e localize o campo múltiplo &quot;Cabeçalhos HTTP personalizados&quot;. Você pode selecionar os cabeçalhos definidos anteriormente e atribuir valores a eles.

Os componentes que usam a configuração do serviço de nuvem acima enviarão esses cabeçalhos HTTP com cada solicitação GraphQL.

## Restrições {#restrictions}

Embora o serviço permita que qualquer nome de cabeçalho seja definido, incluindo os padrão, eles não estarão disponíveis para configuração. Em outras palavras, não é possível substituir os cabeçalhos HTTP padrão usando esse recurso. Uma lista de nomes de cabeçalho restritos pode ser encontrada [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Além disso, há mais dois cabeçalhos que não podem ser usados:

* &quot;Loja&quot; - usada pela CIF para identificar a loja da Adobe Commerce
* &quot;Versão de visualização&quot; - usado pela CIF para recuperar produtos preparados
