---
title: Criação de conteúdo do WYSIWYG para o Edge Delivery Services
description: Saiba como a criação de conteúdo funciona com o Edge Delivery Services e como criar conteúdo do AEM com o Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
role: User
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Criação de conteúdo do WYSIWYG para o Edge Delivery Services {#authoring-edge}

Com o Edge Delivery Services, a criação é fácil, rápida e flexível. Você tem duas opções para criar conteúdo para o Edge Delivery Services:

* [Editor universal](#universal-editor) - Uma interface moderna do WYSIWYG para a criação de conteúdo no AEM
* [Criação Baseada em Documento](#document-based) - Como Microsoft Word ou Google Docs

## Criação no Editor universal {#universal-editor}

Ao usar o Edge Delivery Services com o AEM as a Cloud Service, o fato mais fundamental a entender é que o conteúdo que você cria é persistente no AEM as a Cloud Service.

![Como a criação do WYSIWYG funciona com o Edge Delivery Services](assets/how-aem-edge-works.png)

1. [O ambiente do AEM Sites](/help/sites-cloud/authoring/quick-start.md) é usado para gerenciamento de conteúdo, como a criação de novas páginas, Fragmentos de experiência, Fragmentos de conteúdo etc.
   * Todos os recursos do AEM estão disponíveis, como fluxos de trabalho, MSM, tradução, inicializações etc.
1. [O Editor Universal](/help/sites-cloud/authoring/universal-editor/authoring.md) é usado para criar o conteúdo gerenciado no AEM.
   * O Editor universal oferece uma interface de usuário nova e moderna para a criação de conteúdo.
   * Para criação, o AEM renderiza a HTML, mas inclui scripts, estilos, ícones e outros recursos do Edge Delivery Services.
   * Embora o Editor universal seja usado, todas as alterações são persistentes no AEM.
   * O Editor universal ainda não está em paridade de recursos com o Editor de páginas do AEM e alguns recursos do AEM podem não estar disponíveis no Editor universal.
1. O conteúdo criado com o Editor universal e mantido no AEM é publicado no Edge Delivery Services.
   * O conteúdo permanece armazenado no AEM.
   * O AEM renderiza o HTML semântico necessário para assimilação.
   * O conteúdo é publicado no Edge Delivery Services.
1. [Edge Delivery Services](/help/edge/developer/keeping-it-100.md) garanta uma pontuação de 100% do Lighthouse.

Os blocos são componentes fundamentais de uma página entregue pelo Edge Delivery Services. Os autores podem escolher entre blocos padrão fornecidos pelo Adobe ou entre blocos personalizados para seu projeto pelos desenvolvedores.

O Editor universal fornece uma GUI moderna e intuitiva para a criação de conteúdo, adicionando e organizando blocos.

![Adicionando e organizando blocos no Editor Universal](assets/blocks.png)

Os detalhes dos blocos podem ser configurados no painel Propriedades.

![Configurando propriedades de bloco](assets/block-properties.png)

Para obter detalhes sobre como criar usando o Editor Universal, consulte o documento [Criação de Conteúdo com o Editor Universal](/help/sites-cloud/authoring/universal-editor/authoring.md).

Consulte o [Guia de Introdução do Desenvolvedor para Criação no WYSIWYG com o Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para saber como iniciar seu próprio projeto para criar com o AEM e o Edge Delivery Services.

## Métodos de criação adicionais  {#authoring-methods}

A criação no WYSIWYG é uma ferramenta poderosa e intuitiva para autores de conteúdo. No entanto, há vários casos de uso de criação diferentes, que é o motivo pelo qual o AEM oferece soluções de criação adicionais.

Consulte o documento [Escolhendo um método de criação](/help/edge/authoring-methods.md) para saber mais sobre as soluções de criação que a AEM oferece, incluindo criação baseada em documento e headless.
