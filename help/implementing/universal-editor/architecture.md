---
title: Arquitetura do Editor universal
description: Saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
exl-id: e6f40743-0f21-4fb6-bf23-76426ee174be
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 74%

---


# Arquitetura do Editor universal {#architecture}

Saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.

## Blocos de construção da arquitetura {#building-blocks}

O Editor universal é composto de quatro elementos essenciais que interagem para permitir que autores(as) de conteúdo editem qualquer aspecto do conteúdo das implementações, a fim de entregar experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvimento de última geração.

1. [Editores](#editors)
1. [Aplicativo remoto](#remote-app)
1. [Camada de API](#api-layer)
1. [Camada de persistência](#persistence-layer)

Este documento descreve cada um desses blocos de construção e como eles trocam dados.

![Arquitetura do Editor universal](assets/architecture.png)

>[!TIP]
>
>Para ver o Editor Universal e sua arquitetura em ação, consulte [Introdução ao Editor Universal no AEM](getting-started.md) para saber como obter acesso ao Editor Universal e como começar a instrumentar seu primeiro aplicativo AEM para usá-lo.

### Editores {#editors}

* **Editor universal**: o Editor universal usa um DOM instrumentado para permitir a edição local do conteúdo. Consulte o documento [Atributos e tipos](attributes-types.md) para obter detalhes sobre os metadados necessários. Consulte o documento [Introdução ao Editor universal no AEM](getting-started.md) para obter um exemplo da instrumentação no AEM.
* **Painel de propriedades** - Algumas propriedades de componentes não podem ser editadas no contexto, por exemplo, o tempo de rotação de um carrossel ou qual guia do acordeão deve ser sempre aberta ou fechada. Para permitir a edição dessas informações do componente, um editor baseado em formulário é fornecido no painel lateral do editor.

### Aplicativo remoto {#remote-app}

Para tornar um aplicativo editável no contexto do Editor universal, o DOM deve ser instrumentado. O aplicativo remoto deve renderizar determinados atributos no DOM. Consulte o documento [Atributos e tipos](attributes-types.md) para obter detalhes sobre os metadados necessários. Consulte o documento [Introdução ao Editor universal no AEM](getting-started.md) para obter um exemplo da instrumentação no AEM.

O Editor universal busca manter um SDK simples, portanto, a instrumentação é de responsabilidade da implementação remota do aplicativo.

### Camada de API {#api-layer}

* **Dados de conteúdo**: para o Editor universal, nem os sistemas de origem dos dados de conteúdo nem a forma como são consumidos são importantes. É importante apenas definir e fornecer os atributos necessários usando dados editáveis no contexto.
* **Dados persistentes**: para cada dado editável, há um identificador de URN. Esse URN é usado para rotear a persistência para o sistema e recurso corretos.

### Camada de persistência {#persistence-layer}

* **Modelo de fragmento de conteúdo** - Para oferecer suporte ao painel para edição de propriedades do Fragmento de conteúdo, são necessários o Editor de fragmento de conteúdo e editores baseados em formulário, modelos por componente e fragmento de conteúdo.
* **Conteúdo** - O conteúdo pode ser armazenado em qualquer lugar, por exemplo, no AEM, Magento e assim por diante.

![Camada de persistência](assets/persistence-layer.png)

## Serviço do editor universal e envio do sistema de back-end {#service}

O Editor universal envia todas as alterações de conteúdo para um serviço centralizado chamado Serviço do editor universal. Este serviço, que é executado no Adobe I/O Runtime, carrega plug-ins disponíveis no Registro de extensão com base no URN fornecido. O plug-in é responsável pela comunicação com o back-end e pelo retorno de uma resposta unificada.

![Serviço do editor universal](assets/universal-editor-service.png)

## Renderizar pipelines {#rendering-pipelines}

### Renderização do lado do servidor {#server-side}

![Renderização do lado do servidor](assets/server-side.png)

### Geração de site estático {#static-generation}

![Geração de site estático](assets/static-generation.png)

### Renderização do lado do cliente {#client-side}

![Renderização do lado do cliente](assets/client-side.png)
