---
title: Criação de conteúdo para Edge Delivery Services
description: Saiba como a criação de conteúdo funciona com Edge Delivery Services e como criar conteúdo AEM com Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
source-git-commit: 58d85886ef04b548c09e3ef9308fe596dd3eda38
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# Criação de conteúdo para Edge Delivery Services {#authoring-edge}

Com o Edge Delivery Services, a criação é fácil, rápida e flexível. Há duas opções para criar conteúdo para Edge Delivery Services:

* [Criação baseada em documento](#document-based) - Como o Microsoft Word ou o Google Docs
* [Editor universal](#universal-editor) - Uma interface moderna para a criação de conteúdo no AEM

## Criação baseada em documento {#document-based}

No caso da criação baseada em documentos, é possível trabalhar com várias fontes, como o Microsoft Word e o Google Docs. Os documentos dessas fontes se tornam páginas do site. Cabeçalhos, listas, imagens, elementos de fonte, vídeos podem ser transferidos da fonte inicial para o seu site. Você pode adicionar metadados para fins de SEO ou usar blocos para trabalhar com conteúdo estruturado e adicionar funcionalidades.

Para obter mais detalhes sobre a criação baseada em documentos, consulte [este documento na documentação do Edge Delivery Services.](/help/edge/docs/authoring.md)

## Criação no Editor universal {#universal-editor}

Ao usar Edge Delivery Services com AEM as a Cloud Service AEM, o fato mais fundamental a entender é que o conteúdo que você cria é mantido no as a Cloud Service.

![Como a criação do AEM funciona com o Edge Delivery Services](assets/how-aem-edge-works.png)

1. [O ambiente de criação do AEM](/help/sites-cloud/authoring/quick-start.md) O é usado para gerenciamento de conteúdo, como criar novas páginas, Fragmentos de experiência, Fragmentos de conteúdo etc.
   * Todos os recursos do AEM estão disponíveis, como fluxos de trabalho, MSM, tradução, inicializações etc.
1. [O Editor universal](/help/sites-cloud/authoring/universal-editor/authoring.md) é usado para criar o conteúdo gerenciado no AEM.
   * O Editor universal oferece uma interface de usuário nova e moderna para a criação de conteúdo.
   * Para criação, o AEM renderiza o HTML, mas inclui os scripts, estilos, ícones e outros recursos de Edge Delivery Services.
   * Embora o Editor universal seja usado, todas as alterações são persistentes no AEM.
   * O Universal Editor ainda não está em paridade de recursos com o AEM Page Editor e alguns recursos AEM podem não estar disponíveis no Universal Editor.
1. O conteúdo criado com o Editor universal e persistente no AEM é publicado no Edge Delivery Services.
   * O conteúdo permanece armazenado no AEM.
   * O AEM renderiza o HTML semântico necessário para a assimilação.
   * O conteúdo é publicado no Edge Delivery Services.
1. [Edge Delivery Services](/help/edge/developer/keeping-it-100.md) garanta uma pontuação de 100% no Lighthouse.

Os blocos são componentes fundamentais de uma página entregue pelo Edge Delivery Services. Os autores podem escolher entre blocos padrão fornecidos como padrão pelo Adobe ou entre blocos personalizados para seu projeto pelos desenvolvedores.

O Editor universal fornece uma interface gráfica moderna e intuitiva para a criação de conteúdo, arrastando e soltando blocos.

![Arrastar e soltar blocos no Editor universal](assets/blocks.png)

Os detalhes dos blocos podem ser configurados no painel Propriedades.

![Configuração de propriedades de bloco](assets/block-properties.png)

Para obter detalhes sobre como criar usando o Editor universal, consulte o documento [Criação de conteúdo com o Universal Editor.](/help/sites-cloud/authoring/universal-editor/authoring.md)

Consulte a [Guia de introdução do desenvolvedor para criação de AEM com o Edge Delivery Services](/help/edge/edge-dev-getting-started.md) para saber como iniciar seu próprio projeto para criar com AEM e Edge Delivery Services.

## Como começar {#how-to-get-started}

Entre em contato com o representante da Adobe para obter acesso a esse recurso.
