---
title: Criação de conteúdo do WYSIWYG para Edge Delivery Services
description: Saiba como a criação de conteúdo funciona com Edge Delivery Services e como criar conteúdo AEM com Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Criação de conteúdo do WYSIWYG para Edge Delivery Services {#authoring-edge}

Com o Edge Delivery Services, a criação é fácil, rápida e flexível. Há duas opções para criar conteúdo para Edge Delivery Services:

* [Editor universal](#universal-editor) - Uma interface do WYSIWYG (what-you-see-is-what-you-get, interface do usuário moderna para a criação de conteúdo no AEM
* [Criação Baseada em Documento](#document-based) - Como Microsoft Word ou Google Docs

## Criação no Editor universal {#universal-editor}

Ao usar Edge Delivery Services com o AEM as a Cloud Service, o fato mais fundamental a entender é que o conteúdo que você cria é persistente no AEM as a Cloud Service.

![Como funciona a criação de WYSIWYG com o Edge Delivery Services](assets/how-aem-edge-works.png)

1. [O ambiente do AEM Sites](/help/sites-cloud/authoring/quick-start.md) é usado para gerenciamento de conteúdo, como a criação de novas páginas, Fragmentos de experiência, Fragmentos de conteúdo etc.
   * Todos os recursos do AEM estão disponíveis, como fluxos de trabalho, MSM, tradução, inicializações etc.
1. [O Editor Universal](/help/sites-cloud/authoring/universal-editor/authoring.md) é usado para criar o conteúdo gerenciado no AEM.
   * O Editor universal oferece uma interface de usuário nova e moderna para a criação de conteúdo.
   * Para criação, o AEM renderiza o HTML, mas inclui os scripts, estilos, ícones e outros recursos de Edge Delivery Services.
   * Embora o Editor universal seja usado, todas as alterações são persistentes no AEM.
   * O Universal Editor ainda não está em paridade de recursos com o AEM Page Editor e alguns recursos AEM podem não estar disponíveis no Universal Editor.
1. O conteúdo criado com o Editor universal e persistente no AEM é publicado no Edge Delivery Services.
   * O conteúdo permanece armazenado no AEM.
   * O AEM renderiza o HTML semântico necessário para a assimilação.
   * O conteúdo é publicado no Edge Delivery Services.
1. [Edge Delivery Services](/help/edge/developer/keeping-it-100.md) garanta uma pontuação de 100% do Lighthouse.

Os blocos são componentes fundamentais de uma página entregue pelo Edge Delivery Services. Os autores podem escolher entre blocos padrão fornecidos como padrão pelo Adobe ou entre blocos personalizados para seu projeto pelos desenvolvedores.

O Editor universal fornece uma GUI moderna e intuitiva para a criação de conteúdo, adicionando e organizando blocos.

![Adicionando e organizando blocos no Editor Universal](assets/blocks.png)

Os detalhes dos blocos podem ser configurados no painel Propriedades.

![Configurando propriedades de bloco](assets/block-properties.png)

Para obter detalhes sobre como criar usando o Editor Universal, consulte o documento [Criação de Conteúdo com o Editor Universal](/help/sites-cloud/authoring/universal-editor/authoring.md).

Consulte o [Guia de Introdução do Desenvolvedor para Criação no WYSIWYG com Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para saber como iniciar seu próprio projeto para criar com AEM e Edge Delivery Services.

## Métodos de criação adicionais  {#authoring-methods}

A criação no WYSIWYG é uma ferramenta poderosa e intuitiva para autores de conteúdo. No entanto, há vários casos de uso de criação diferentes, que é o motivo pelo qual o AEM oferece soluções de criação adicionais.

Consulte o documento [Escolhendo um método de criação](/help/edge/authoring-methods.md) para saber mais sobre as ofertas de AEM de soluções de criação, incluindo criação baseada em documento e headless.
