---
title: Integrar o AEM Assets durante a criação de conteúdo para Edge Delivery Services
description: Saiba como integrar o AEM Assets com o Edge Delivery Services. Essa integração permite integrar o AEM Assets ao Microsoft Word e Google Docs, integrar o AEM Assets ao Universal Editor, integrar o Dynamic Media aos recursos OpenAPI com o Universal Editor e integrar o Dynamic Media aos recursos OpenAPI com o Microsoft Word e o Google Docs.
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 9e7701152e1da4afc73d3d5ba271b04df2054397
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Integrar o AEM Assets durante a criação de conteúdo para Edge Delivery Services {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![EDS2](/help/assets/assets/EDS2.png)

O Edge Delivery Services é um conjunto de serviços combináveis que permite um alto grau de flexibilidade na maneira como você cria e entrega conteúdo no seu site. Você pode usar a [criação de conteúdo do AEM](/help/sites-cloud/authoring/author-publish.md) e o [WYSIWYG usando o Editor Universal, bem como a Criação Baseada em Documento](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

É possível editar conteúdo em:

* [Documentação do Microsoft Word ou Google](#integrate-aem-assets-with-document-based-authoring-tools)

* [Editor universal](#integrate-aem-assets-with-universal-editor)

Após editar o conteúdo, você pode publicá-lo no Edge Delivery Services.

## Integração do AEM Assets com fluxos de criação baseados em documento para Edge Delivery Services {#integrate-aem-assets-with-document-based-authoring-tools}

A integração do AEM Assets com as ferramentas de Criação baseadas em documentos, como o Microsoft Word ou o Google Docs, fornece um seletor de ativos diretamente no editor. Use este seletor de ativos para acessar o AEM Assets e inserir ativos aprovados em seu documento.

### Pré-requisitos{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Antes de começar, verifique se o ambiente de Criação Baseada em Documento está pronto:

* Integre o AEM a uma ferramenta de Criação baseada em documentos para configurar o ambiente de criação. Consulte [Introdução - Tutorial do desenvolvedor](https://www.aem.live/developer/tutorial) para configurar o ambiente de criação.

### Integração do AEM Assets ao ambiente de criação baseado em documentos{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Configure o plug-in Sidekick do AEM Assets para usar ativos durante a criação de conteúdo no Microsoft Word ou Google Docs.

* Consulte [Plug-in do Adobe Experience Manager Assets Sidekick](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) para saber como acessar e usar o AEM Assets no Microsoft Word ou Google Docs.
* Consulte [Configurando o plug-in do Sidekick Adobe Experience Manager Assets](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin) para obter detalhes sobre a configuração.
  ![barra lateral de meus ativos](/help/assets/assets/my-assets-sidebar.png)

## Fornecer ativos usando o Dynamic Media com recursos OpenAPI {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

Você também pode usar ativos fornecidos usando o DM com recursos OpenAPI. Ele oferece muitos benefícios, como:

* Acesso somente aos ativos aprovados pela marca (imagens, vídeos, PDF e outros tipos de ativos) do AEM Assets Cloud Service.
* Governança (referências versus cópias do ativo), que ajuda na propagação automática de eventos do ciclo de vida do ativo, como expiração, exclusão e atualizações.
* Representações de imagem dinâmicas e Recorte inteligente.
* Otimização e entrega de mídia avançada, como transmissão contínua de vídeo adaptável pronta para uso e entrega de ativos originais para PDF.
* Relatório de impressões no nível do ativo ([disponibilidade limitada](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Para obter mais detalhes sobre os recursos, consulte a documentação do [Dynamic Media com recursos OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Pré-requisitos {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

Para usar a referência do ativo, você deve ter:

* Direito a um ambiente de Cloud Service Assets em que o Dynamic Media com recursos de API aberta esteja habilitado.
* Uma licença do Dynamic Media.
* O plug-in do AEM Assets sidekick está habilitado com a opção copiar referência para ativos de imagem. Para obter mais detalhes, consulte [isto](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) para Criação Baseada em Documento e consulte [isto](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para criação baseada em Editor Universal.
* Assets aprovados. Os ativos aprovados têm `dam:status=Approved` por meio das ações de back-end ou interface do Assets Cloud Service.

### Usar ativos fornecidos usando o Dynamic Media com recursos OpenAPI{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

Para usar ativos entregues usando o Dynamic Media com recursos OpenAPI durante a criação de conteúdo, consulte:

* [Usando referências de imagem](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Usando referências de vídeo](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Usando referências de ativos para ativos que não sejam de imagem e vídeo, como PDF, arquivos Zip e muito mais](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

Assista a este vídeo para saber como fornecer ativos usando o Dynamic Media com recursos OpenAPI.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Exemplo de site do Edge Delivery Services{#example-of-an-Edge-Delivery-Services-site}

Consulte [WKND Travel](https://aem-dynamicmedia-demo--dm--hlxsites.aem.live/travel-hospitality/wknd-trvl-home). Este site foi criado usando os recursos de Criação baseada em documentos do Edge Delivery Services. O conteúdo do site é criado em [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT), usando o Dynamic Media com recursos OpenAPI para a entrega de ativos. Depois de criado, o conteúdo é publicado diretamente do documento. Para esta configuração de Criação Baseada em Documento, todos os arquivos essenciais, pastas, configurações, estilos do site e códigos de funcionalidade são armazenados neste [repositório Git](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks).

## Integração do AEM Assets com fluxos de criação baseados no Universal Editor para Edge Delivery Services {#integrate-aem-assets-with-universal-editor}

Configure o Editor universal para integrar com o AEM Assets. Essa integração permite usar o Dynamic Media com recursos OpenAPI para fornecer ativos.

* Consulte [Configuração no Site do Edge Delivery](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) para adicionar uma função personalizada do seletor de ativos no Editor Universal. O seletor de ativos personalizado permite inserir ativos no conteúdo do Editor universal diretamente.
* Consulte [Visão geral da extensão](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para saber como acessar o AEM Assets e inserir os ativos durante a criação no Universal Editor.
