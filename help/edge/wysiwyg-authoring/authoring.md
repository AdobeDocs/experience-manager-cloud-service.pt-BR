---
title: Criação de conteúdo para Edge Delivery Services
description: Saiba como a criação de conteúdo funciona com Edge Delivery Services e como criar conteúdo AEM com Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
role: User
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Criação de conteúdo para Edge Delivery Services {#authoring-edge}

Com o Edge Delivery Services, a criação é fácil, rápida e flexível. Há duas opções para criar conteúdo para Edge Delivery Services:

* [Editor Universal](#universal-editor) - Uma interface WYSIWYG (what you see is what you get, o que você vê é o que você obtém) moderna para a criação de conteúdo no AEM
* [Criação Baseada em Documento](#document-based) - Como os documentos do Microsoft Word ou Google

## Criação no Editor universal {#universal-editor}

Ao usar Edge Delivery Services com o AEM as a Cloud Service, o fato mais fundamental a entender é que o conteúdo que você cria é persistente no AEM as a Cloud Service.

![Como a criação WYSIWYG funciona com o Edge Delivery Services](assets/how-aem-edge-works.png)

1. [O ambiente de criação WYSIWYG](/help/sites-cloud/authoring/quick-start.md) é usado para gerenciamento de conteúdo, como a criação de novas páginas, Fragmentos de experiência, Fragmentos de conteúdo etc.
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

O Editor universal fornece uma interface gráfica moderna e intuitiva para a criação de conteúdo, arrastando e soltando blocos.

![Arrastar e soltar blocos no Editor Universal](assets/blocks.png)

Os detalhes dos blocos podem ser configurados no painel Propriedades.

![Configurando propriedades de bloco](assets/block-properties.png)

Para obter detalhes sobre como criar usando o Universal Editor, consulte o documento [Criação de Conteúdo com o Universal Editor.](/help/sites-cloud/authoring/universal-editor/authoring.md)

Consulte o [Guia de Introdução do Desenvolvedor para Criação WYSIWYG com o Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para saber como iniciar seu próprio projeto para criar com AEM e Edge Delivery Services.

## Criação baseada em documento  {#document-based}

Ao usar a criação baseada em documentos, você pode trabalhar com várias fontes, como documentos do Microsoft Word e do Google Docs. Os documentos dessas fontes se tornam páginas do site. Cabeçalhos, listas, imagens, elementos de fonte, vídeos podem ser transferidos da fonte inicial para o seu site. Você pode adicionar metadados para fins de SEO ou usar blocos para trabalhar com conteúdo estruturado e adicionar funcionalidades.

Para obter mais detalhes sobre a criação baseada em documentos, consulte [este documento na documentação do Edge Delivery Services.](/help/edge/docs/authoring.md)

