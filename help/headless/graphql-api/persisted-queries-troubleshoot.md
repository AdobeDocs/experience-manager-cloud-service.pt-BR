---
title: Solução de problemas de consultas persistentes do GraphQL
description: Saiba como solucionar problemas com consultas persistentes do GraphQL no Adobe Experience Manager as a Cloud Service.
feature: Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
source-git-commit: 09ef5fb49ba638f888c9c101760ffa3c7d258fda
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Solução de problemas de consultas persistentes do GraphQL {#troubleshoot-persisted-graphql-queries}

A variável [Centro de ações](/help/operations/actions-center.md) inclui o **Erro de consulta persistente do GraphQL** alerta. Isso significa que você é informado sempre que uma das consultas persistentes do GraphQL emite um erro.

Para ajudá-lo a solucionar e resolver esses problemas, esta página aborda a *mais comum* causas de falhas e etapas sobre como corrigi-las.

## Alterações no modelo de Fragmento de conteúdo {#changes-to-content-fragment-model}

Uma consulta persistente do GraphQL pode falhar quando baseada em tipos de GraphQL obsoletos, geralmente devido a uma alteração nos modelos subjacentes de Fragmento de conteúdo.

Esses erros podem ocorrer por várias razões. Por exemplo, quando o autor de um modelo de fragmento de conteúdo (a lista não é exaustiva):

* remove ou renomeia um campo
* atualiza o **Tipo de modelo** que define os modelos permitidos para a referência do fragmento
* cancela a publicação de um modelo referenciado por outros modelos

Para resolver esses erros, você deve:

* atualizar a consulta persistente que não acomoda as alterações feitas no modelo de fragmento de conteúdo
* reverter a alteração no modelo que introduziu o problema

## Ponto de extremidade do GraphQL não configurado {#graphql-endpoint-not-configured}

Quando consultas persistentes retornam a variável `404` código de erro, juntamente com as informações `No suitable endpoint found`, isso significa que nenhum endpoint do GraphQL está configurado no ambiente AEM.

Para corrigir isso, siga as etapas para ativar e publicar seu endpoint no [Gerenciar endpoints do GraphQL no AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Caminho ausente no URL da consulta persistente do GraphQL {#missing-path-query-url}

Se consultas persistentes retornarem a variável `400` código de erro com as informações `Suffix: '/' does not contain a path`, o servlet GraphQL está sendo chamado sem um sufixo de caminho.

O padrão deve ser `/graphql/execute.json/thePath`.

## Bloqueado devido à lista de permissões de IP {#blocked-due-to-ip-allow-list}

Nesse caso, a consulta retorna o parâmetro `405` código de erro.

Esse erro não é específico do GraphQL. Consulte o artigo da KB [Erro 405 não permitido](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-20824).

## Bloqueado pelo Dispatcher {#blocked-dispatcher}

Se o endpoint do GraphQL retornar o `404` erro ao publicar para `POST` , significa que as consultas do GraphQL são bloqueadas no nível do dispatcher e o endpoint precisa ser ativado manualmente.

Esse não deve ser o caso por padrão, mas uma configuração personalizada do dispatcher pode causar esse problema. Veja mais em [Dispatcher - Configuração de ponto de extremidade com AEM Headless](/help/headless/deployment/dispatcher.md).
