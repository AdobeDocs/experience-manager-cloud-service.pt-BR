---
title: Solução de problemas de consultas persistentes do GraphQL
description: Saiba como solucionar problemas com consultas persistentes do GraphQL no Adobe Experience Manager as a Cloud Service.
feature: Headless, Content Fragments,GraphQL API
exl-id: 71bd1f68-ca96-4c78-a936-abed250ecec1
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Solução de problemas de consultas persistentes do GraphQL {#troubleshoot-persisted-graphql-queries}

O [Centro de Ações](/help/operations/actions-center.md) inclui o alerta **erro de consulta persistente do GraphQL**. Isso significa que você é informado sempre que uma das consultas persistentes do GraphQL emite um erro.

Para ajudá-lo a solucionar e resolver esses problemas, esta página aborda as *causas mais comuns* das falhas e as etapas sobre como corrigi-las.

## Alterações no modelo de Fragmento de conteúdo {#changes-to-content-fragment-model}

Uma consulta persistente do GraphQL pode falhar quando baseada em tipos de GraphQL obsoletos, geralmente devido a uma alteração nos modelos subjacentes de Fragmento de conteúdo.

Esses erros podem ocorrer por várias razões. Os exemplos incluem (a lista não é exaustiva), quando o autor de um modelo de fragmento de conteúdo:

* remove ou renomeia um campo
* atualiza o **Tipo de modelo** que define os modelos permitidos para a referência do fragmento
* cancela a publicação de um modelo referenciado por outros modelos

Para resolver esses erros, você deve:

* atualizar a consulta persistente que não acomoda as alterações feitas no modelo de fragmento de conteúdo
* reverter a alteração no modelo que introduziu o problema

## Ponto de extremidade do GraphQL não configurado {#graphql-endpoint-not-configured}

Quando consultas persistentes retornam o código de erro `404`, juntamente com as informações `No suitable endpoint found`, isso significa que nenhum terminal GraphQL está configurado no ambiente AEM.

Para corrigir isso, siga as etapas para habilitar e publicar seu ponto de extremidade em [Gerenciar pontos de extremidade do GraphQL no AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Caminho ausente no URL da consulta persistente do GraphQL {#missing-path-query-url}

Se consultas persistentes retornarem o código de erro `400` com as informações `Suffix: '/' does not contain a path`, o servlet GraphQL será chamado sem um sufixo de caminho.

O padrão deve ser `/graphql/execute.json/thePath`.

## Bloqueado devido à lista de permissões de IP {#blocked-due-to-ip-allow-list}

Nesse caso, a consulta retorna o código de erro `405`.

Esse erro não é específico do GraphQL. Consulte o artigo da Base de Dados de Conhecimento [Erro 405 Não Permitido](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-20824).

## Bloqueado pelo Dispatcher {#blocked-dispatcher}

Se o ponto de extremidade do GraphQL retornar o erro `404` ao publicar para `POST` solicitações, significa que as consultas do GraphQL são bloqueadas no nível do dispatcher e o ponto de extremidade precisa ser habilitado manualmente.

Esse não deve ser o caso por padrão, mas uma configuração personalizada do dispatcher pode causar esse problema. Veja mais em [Dispatcher - Configuração de ponto de extremidade com AEM Headless](/help/headless/deployment/dispatcher.md).
