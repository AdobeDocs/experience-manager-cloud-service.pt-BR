---
title: Autenticação do Editor universal
description: Saiba como funciona a autenticação do Editor universal.
exl-id: fb86c510-3c41-4511-81b7-1bdf2f5e7dd3
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 100%

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

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Editor universal, consulte estes documentos.

* [Introdução ao Editor universal](introduction.md): saiba como o Editor Universal permite editar qualquer aspecto do conteúdo das implementações, a fim de entregar experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvedor de última geração.
* [Criação de conteúdo com o Editor universal](authoring.md): saiba como é fácil e intuitivo para os autores criarem conteúdo usando o Editor universal.
* [Publicação de conteúdo com o Editor universal](publishing.md): saiba como o Editor visual universal publica o conteúdo e como seus aplicativos podem lidar com esse conteúdo.
* [Introdução ao Editor universal no AEM](getting-started.md): saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
* [Arquitetura do Editor universal](architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Atributos e tipos](attributes-types.md): saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
