---
title: Remoção do cache da CDN
description: Saiba como remover objetos em cache do cache CDN do Adobe configurando o token de API de limpeza que pode ser usado em chamadas de API.
feature: CDN Cache
exl-id: 4d091677-b817-4aeb-b131-7a5407ace3e0
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# Remoção do cache da CDN {#cdn-purge-cache}

>[!NOTE]
>Esse recurso ainda não está disponível para o público geral. Para participar do programa de adoção antecipada, envie um email para `aemcs-cdn-config-adopter@adobe.com`.

A limpeza remove um objeto do cache CDN do Adobe, resultando em solicitações futuras que prosseguem para a origem como um erro de cache, em vez de serem fornecidas do cache.
O AEM as a Cloud Service permite configurar um Token de API de limpeza, que pode ser usado em chamadas de API. Leia o [artigo sobre Configuração de Credenciais e Autenticação da CDN](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) para saber como configurar este token usando as diretivas de Autenticação de Pipeline de Configuração do Cloud Manager.

Há três variações de limpeza compatíveis:

* [Limpeza de URL única](#single-purge) - limpar um único recurso por vez.
* [Limpar por chave substituta](#surrogate-key-purge) - limpa vários recursos de uma vez.
* [Limpeza completa](#full-purge) - limpar todos os recursos.

Todas as variações de limpeza compartilham o seguinte:

* O método HTTP deve ser definido como `PURGE`.
* O URL pode ser qualquer domínio associado ao serviço AEM para o qual a solicitação de limpeza se destina.
* O `X-AEM-Purge-Key` deve ser fornecido em um cabeçalho HTTP.

>[!CAUTION]
>A limpeza do cache CDN, especialmente com o sinalizador de hardware, aumentará o tráfego na origem e poderá causar uma interrupção quando não for executada corretamente.

## Limpeza de URL único {#single-purge}

Você pode expurgar um único recurso de cada vez da seguinte maneira:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

Como mostrado no exemplo acima, você pode **opcionalmente** especificar se o CDN deve executar uma limpeza **rígida** (padrão) ou uma limpeza **suave** nos objetos em cache.

A limpeza permanente padrão torna o conteúdo imediatamente inacessível para novas solicitações até que o conteúdo seja recuperado da origem. A limpeza suave marca o conteúdo como obsoleto, mas ainda o envia aos clientes para que eles não precisem aguardar até que o conteúdo seja recuperado da origem.

## Limpeza de chave substituta {#surrogate-key-purge}

Chaves substitutas são identificadores exclusivos que você usa para limpar um conjunto de conteúdo. Eles são aplicados ao conteúdo adicionando um cabeçalho `Surrogate-Key` à resposta. Uma ou mais chaves substitutas podem ser referenciadas em uma chamada de API de limpeza.

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

O(s) `Surrogate-Key` são separados por espaços. De modo semelhante à limpeza de URL único, você pode configurar uma limpeza permanente ou flexível.

## Limpeza completa {#full-purge}

Você pode executar uma limpeza completa de todos os recursos em cache da seguinte maneira:

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

Esteja ciente de que o cabeçalho `X-AEM-Purge` deve incluir o valor &quot;all&quot;.

## Interações com a camada Apache/Dispatcher {#apache-layer}

Conforme descrito no [artigo sobre Fluxo de entrega de conteúdo](/help/implementing/dispatcher/overview.md), a CDN recupera o conteúdo da camada Apache/Dispatcher, se o cache tiver expirado. Isso implica que, antes de limpar um recurso na CDN, você deve garantir que uma nova versão do conteúdo também esteja disponível na Dispatcher. Para obter mais detalhes, consulte também [Invalidação de cache do Dispatcher](/help/implementing/dispatcher/caching.md#disp).
