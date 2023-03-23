---
title: Arquitetura do editor universal
description: Saiba mais sobre a arquitetura do Editor Universal e como os dados fluem entre seus serviços e camadas.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---


# Arquitetura do editor universal {#architecture}

Saiba mais sobre a arquitetura do Editor Universal e como os dados fluem entre seus serviços e camadas.

## Blocos de construção da arquitetura {#building-blocks}

O Editor Universal é composto de quatro blocos fundamentais essenciais que interagem para permitir que os autores de conteúdo editem qualquer aspecto de qualquer conteúdo em qualquer implementação, para fornecer experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvedor de última geração.

1. [Editores](#editors)
1. [Aplicativo remoto](#remote-app)
1. [Camada de API](#api-layer)
1. [Camada de persistência](#persistence-layer)

Este documento descreve cada um desses blocos fundamentais e como eles trocam dados.

![Arquitetura do Editor Universal](assets/architecture.png)

>[!TIP]
>
>Se você quiser ver o Editor Universal e sua arquitetura em ação, consulte o documento [Introdução ao Editor universal no AEM](getting-started.md) para saber como obter acesso ao Universal Editor e como começar a instrumentar seu primeiro aplicativo AEM para usá-lo.

### Editores {#editors}

* **Editor universal** - O Editor Universal usa um DOM instrumentado para permitir a edição local do conteúdo. Consulte o documento [Atributos e tipos](attributes-types.md) para obter detalhes sobre os metadados necessários. Consulte o documento [Introdução ao Editor universal no AEM](getting-started.md) para obter um exemplo da instrumentação em AEM.
* **Painel Propriedades** - Algumas propriedades dos componentes não podem ser editadas no contexto, por exemplo, o tempo de rotação de um carrossel ou que deve ser sempre aberto ou fechado. Para permitir a edição dessas informações de componente, um editor baseado em formulário é fornecido no painel lateral do editor.

### Aplicativo remoto {#remote-app}

Para tornar um aplicativo no contexto editável no Editor universal, o DOM deve ser instrumentado. O aplicativo remoto deve renderizar determinados atributos no DOM. Consulte o documento [Atributos e tipos](attributes-types.md) para obter detalhes sobre os metadados necessários. Consulte o documento [Introdução ao Editor universal no AEM](getting-started.md) para obter um exemplo da instrumentação em AEM.

O Universal Editor se esforça para obter um SDK mínimo, portanto, a instrumentação é da responsabilidade da implementação remota do aplicativo.

### Camada de API {#api-layer}

* **Dados de conteúdo** - Para o Editor Universal, nem os sistemas de origem dos dados de conteúdo nem a forma como são consumidos são importantes. É importante apenas definir e fornecer os atributos necessários usando dados editáveis no contexto.
* **Dados persistentes** - Para cada dado editável, há um identificador de URN. Esse URN é usado para rotear a persistência para o sistema e recurso corretos.

### Camada de persistência {#persistence-layer}

* **Modelo de fragmento de conteúdo** - Para oferecer suporte ao painel para edição das propriedades do Fragmento de conteúdo, do Editor de fragmento de conteúdo e dos editores baseados em formulário, são necessários modelos por componente e fragmento de conteúdo.
* **Conteúdo** - O conteúdo pode ser armazenado em qualquer lugar, como em AEM, Magento, etc.

![Camada de persistência](assets/persistence-layer.png)

## Expedição de sistema de back-end e serviço de editor universal {#service}

O Universal Editor envia todas as alterações de conteúdo para um serviço centralizado chamado Universal Editor Service. Este serviço, em execução no Adobe I/O Runtime, carrega plug-ins disponíveis no Registro de extensão com base no URN fornecido. O plug-in é responsável pela comunicação com o backend e pelo retorno de uma resposta unificada.

![Universal Editor Service](assets/universal-editor-service.png)

## Renderizar pipelines {#rendering-pipelines}

### Renderização do lado do servidor {#server-side}

![Renderização do lado do servidor](assets/server-side.png)

### Geração estática de site {#static-generation}

![Geração estática de site](assets/static-generation.png)

### Renderização do lado do cliente {#client-side}

![Renderização do lado do cliente](assets/client-side.png)

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Universal Editor, consulte estes documentos.

* [Introdução ao Editor Universal](introduction.md) - Saiba como o Editor Universal permite editar qualquer aspecto de qualquer conteúdo em qualquer implementação para fornecer experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvedor de última geração.
* [Criação de conteúdo com o editor universal](authoring.md) - Saiba como é fácil e intuitivo para os autores de conteúdo criar conteúdo usando o Editor Universal.
* [Publicação de conteúdo com o editor universal](publishing.md) - Saiba como o Editor visual universal publica conteúdo e como seus aplicativos podem lidar com o conteúdo publicado.
* [Introdução ao Editor universal no AEM](getting-started.md) - Saiba como obter acesso ao Universal Editor e como começar a instrumentar seu primeiro aplicativo AEM para usá-lo.
* [Atributos e tipos](attributes-types.md) - Saiba mais sobre os atributos e tipos de dados exigidos pelo Editor Universal.
* [Autenticação do editor universal](authentication.md) - Saiba como o Editor Universal se autentica.
