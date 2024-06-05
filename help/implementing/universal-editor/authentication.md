---
title: Autenticação do Editor universal
description: Saiba como o Editor universal usa o Sistema Adobe Identity Management (IMS) para autenticação.
exl-id: fb86c510-3c41-4511-81b7-1bdf2f5e7dd3
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 92%

---


# Autenticação do Editor universal {#authentication}

Saiba como funciona a autenticação do Editor universal.

## Opções {#options}

O Editor universal utiliza o sistema de Identify Management (IMS) da Adobe como forma de autenticação, que é fornecido por meio do Unified Shell.

Todos os aplicativos/páginas remotas são responsáveis pela autenticação dos sistemas de back-end necessários. A autenticação é essencial no Editor universal para que os sistemas de back-end realizem operações CRUD, que é um serviço independente.

## Fluxo padrão {#standard-flow}

Essa é a solução que permite que o AEM as a Cloud Service e AMS utilizem o IMS para fazer uso do Editor universal.

Para utilizar o Editor universal, o usuário precisar estar conectado no Unified Shell, que utiliza o IMS na autenticação. O token do IMS fornecido é armazenado na sessão do usuário.

Ao executar uma operação CRUD, uma chamada é enviada para o serviço do Editor universal com o token do portador do IMS no cabeçalho HTTP. Em seguida, o token do portador é utilizado pelo serviço do Editor universal para autenticar a solicitação no sistema de back-end do AEM e executar operações no nome do usuário.

![Fluxo de autenticação padrão](assets/standard-flow.png)
