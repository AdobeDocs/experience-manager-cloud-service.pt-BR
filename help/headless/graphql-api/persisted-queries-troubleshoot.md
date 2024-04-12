---
title: Solução de problemas de consultas persistentes do GraphQL
description: Saiba como solucionar problemas com consultas persistentes do GraphQL no Adobe Experience Manager as a Cloud Service.
feature: Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
source-git-commit: 220e86f18e4a61304764753d8daecb68503e9fd0
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Solução de problemas de consultas persistentes do GraphQL {#troubleshoot-persisted-graphql-queries}

A variável [Centro de ações](/help/operations/actions-center.md) inclui o **Erro de consulta persistente do GraphQL** alerta. Isso significa que você é informado sempre que uma das consultas persistentes do GraphQL emite um erro.

Para ajudá-lo a solucionar e resolver esses problemas, explicamos a *mais comum* causas de falhas e etapas sobre como corrigi-las.

## Alterações no modelo de Fragmento de conteúdo {#changes-to-content-fragment-model}

Uma consulta persistente do GraphQL pode falhar quando baseada em tipos de GraphQL obsoletos, geralmente devido a uma alteração nos modelos subjacentes de Fragmento de conteúdo.

Isso pode acontecer por várias razões. Por exemplo, quando um autor de modelo de conteúdo:

* remove ou renomeia um campo
* atualiza os modelos permitidos definidos para uma referência de fragmento
* cancela a publicação de um modelo referenciado por outros modelos
* outras ações e motivos

Para resolver isso:

* a consulta persistente que está falhando deve ser atualizada para acomodar a alteração no modelo de Fragmento de conteúdo
* ou a alteração no modelo que introduziu o problema deve ser revertida

## Ponto de extremidade do GraphQL não configurado {#graphql-endpoint-not-configured}

Quando consultas persistentes retornam a variável `404` código de erro, juntamente com as informações `No suitable endpoint found`, isso significa que nenhum endpoint do GraphQL está configurado no ambiente AEM.

Para corrigir isso, siga as etapas para ativar e publicar seu endpoint no [Gerenciar endpoints do GraphQL no AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Caminho ausente no URL da consulta persistente do GraphQL {#missing-path-query-url}

Se consultas persistentes retornarem a variável `400` código de erro com as informações `Suffix: '/' does not contain a path`, o servlet GraphQL está sendo chamado sem um sufixo de caminho.

O padrão deve ser `/graphql/execute.json/thePath`.

## Bloqueado devido à lista de permissões de IP {#blocked-due-to-ip-allow-list}

Nesse caso, a consulta retorna o parâmetro `405` código de erro.

Isso não é algo específico do GraphQL. Consulte o artigo da KB [Erro 405 não permitido](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-20824.html).

## Bloqueado pelo Dispatcher {#blocked-dispatcher}

Se o endpoint do GraphQL retornar o `404` erro ao publicar para `POST` , significa que as consultas do GraphQL são bloqueadas no nível do dispatcher e o endpoint precisa ser ativado manualmente.

Esse não deve ser o caso por padrão, mas uma configuração personalizada do dispatcher pode causar esse problema. Veja mais em [Dispatcher - Configuração de ponto de extremidade com AEM Headless](/help/headless/deployment/dispatcher.md).
