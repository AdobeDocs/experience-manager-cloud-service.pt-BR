---
title: Integrar o AEM Assets ao criar conteúdo para o Edge Delivery Services
description: Saiba como integrar o AEM Assets ao Edge Delivery Services. Essa integração permite integrar o AEM Assets com o Microsoft Word e o Google Docs, integrar o AEM Assets com o Universal Editor, integrar o Dynamic Media com recursos OpenAPI com o Universal Editor e integrar o Dynamic Media com recursos OpenAPI com o Microsoft Word e o Google Docs.
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: e4a71d1a513bebed67b9571a483871dc16c36daa
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Integrar o AEM Assets ao criar conteúdo para o Edge Delivery Services {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![Ativos do AEM com UE](/help/assets/assets/EDS2.png)

O [Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/overview) é um conjunto de serviços combináveis que permite um alto grau de flexibilidade na maneira como você cria e entrega conteúdo no seu site. Você pode usar a [criação de conteúdo do AEM](/help/sites-cloud/authoring/author-publish.md) e do [WYSIWYG usando o Editor Universal, bem como a Criação Baseada em Documento](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

É possível editar conteúdo em:

* [Microsoft Word ou Google Docs](#integrate-aem-assets-with-document-based-authoring-tools)
* [Editor universal](#integrate-aem-assets-with-UE-universal-editor)

Após editar o conteúdo, você pode publicá-lo no Edge Delivery Services.

## Integração do AEM Assets com fluxos de criação baseados em documento para o Edge Delivery Services {#integrate-aem-assets-with-document-based-authoring-tools}

Quando o AEM Assets é integrado às ferramentas de Criação baseadas em documentos, como o Microsoft Word ou o Google Docs, ele fornece um seletor de ativos no editor. Use este seletor de ativos para acessar o AEM Assets e inserir ativos aprovados em seu documento.
Se você já tiver um site do Edge Delivery Services, consulte o documento [Plug-in do AEM Assets](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) para saber como integrar o AEM Assets ao seu projeto existente do AEM.
Siga os [Pré-requisitos](#integrate-aem-assets-with-microsoft-word-and-google-docs) e [Integrando o AEM Assets com o ambiente de Criação baseada em documentos](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) seções a seguir se você não tiver um site do Edge Delivery Services para publicar seu conteúdo incluído do AEM Assets criado nas ferramentas de criação baseadas em documentos.

### Pré-requisitos{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Antes de começar, verifique se o ambiente de Criação Baseada em Documento está pronto:

* Integre o AEM a uma ferramenta de Criação baseada em documento para configurar o ambiente de criação. Consulte [Introdução - Tutorial do desenvolvedor](https://www.aem.live/developer/tutorial) para saber como configurar o ambiente de criação.

### Integração do AEM Assets ao ambiente de criação baseado em documentos{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Configure o plug-in do AEM Assets Sidekick para usar ativos durante a criação de conteúdo no Microsoft Word ou Google Docs.

* Consulte [Plug-in do Adobe Experience Manager Assets Sidekick](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) para saber como acessar e usar o AEM Assets no Microsoft Word ou Google Docs.
* Consulte [Configurando o Plug-in do Adobe Experience Manager Assets Sidekick](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin) para obter detalhes sobre a configuração.
  ![usar mídia dinâmica com recursos de openAPI no ms word e no google docs](/help/assets/assets/my-assets-sidebar.png)

## Fornecer ativos usando o Dynamic Media com recursos OpenAPI {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

Você também pode usar ativos fornecidos usando o DM com recursos OpenAPI. Ele oferece muitos benefícios, como:

* Acesso somente a ativos aprovados pela marca (imagens, vídeos, PDFs e outros tipos de ativos) do AEM Assets Cloud Services.
* Governança (referências versus cópias do ativo), que ajuda na propagação automática de eventos do ciclo de vida do ativo, como expiração, exclusão e atualizações.
* Representações de imagem dinâmicas e Recorte inteligente.
* Otimização e entrega de mídia avançada, como transmissão contínua de vídeo adaptável pronta para uso e entrega de ativos originais para PDFs.
* Relatório de impressões no nível do ativo ([disponibilidade limitada](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Para obter mais detalhes sobre os recursos, consulte a documentação do [Dynamic Media com recursos OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Pré-requisitos {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

Para usar a referência do ativo, você deve ter:

* Direito a um ambiente do Assets Cloud Service em que o Dynamic Media com recursos de API aberta esteja ativado.
* Uma licença do Dynamic Media.
* O plug-in do AEM Assets sidekick está habilitado com a opção copiar referência para ativos de imagem. Para obter mais detalhes, consulte [isto](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) para Criação Baseada em Documento e consulte [isto](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para criação baseada em Editor Universal.
* Assets aprovados. Os ativos aprovados têm `dam:status=Approved` por meio das ações de back-end ou interface do usuário do Assets Cloud Services.

### Usar ativos fornecidos usando o Dynamic Media com recursos OpenAPI{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

Selecione os links a seguir para saber como usar o Dynamic Media com recursos OpenAPI para fornecer imagens, vídeos e outros tipos de ativos no seu conteúdo:

* [Adicionar imagens ao seu conteúdo](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Adicionar vídeos ao seu conteúdo](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Adicione ativos que não sejam de imagem e vídeo, como PDF, arquivos Zip e muito mais, ao seu conteúdo](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

Assista a este vídeo para saber como fornecer ativos em seu conteúdo usando o Dynamic Media com recursos de OpenAPI.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Site de exemplo do Edge Delivery Services{#example-of-an-Edge-Delivery-Services-site}

Consulte [WKND Travel](http://bit.ly/3DExLnf), um site que é construído usando os recursos de autoria baseada em documentos do Edge Delivery Services. O conteúdo do site foi criado no [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) e o Dynamic Media com recursos OpenAPI é usado para fornecer ativos no conteúdo. Após a criação, o conteúdo é publicado diretamente do documento. Explore este [repositório Git](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) para saber sobre todos os arquivos, pastas, configurações, estilos do site e códigos de funcionalidade essenciais usados para criar a configuração de Criação Baseada em Documento para este site do Edge Delivery Services (EDS).

## Integração do AEM Assets com fluxos de criação baseados no Universal Editor para o Edge Delivery Services {#integrate-aem-assets-with-UE-universal-editor}

Configure o Editor universal para integrar com o AEM Assets. Essa integração permite usar o Dynamic Media com recursos OpenAPI para fornecer ativos.

* Consulte [Configuração no Site do Edge Delivery](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) para saber como adicionar uma função personalizada de seleção de ativos no Editor Universal. O seletor de ativos personalizado permite inserir ativos no conteúdo do Editor universal diretamente.
* Consulte [Visão geral da extensão](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para saber como acessar o AEM Assets e inserir os ativos durante a criação no Universal Editor.
