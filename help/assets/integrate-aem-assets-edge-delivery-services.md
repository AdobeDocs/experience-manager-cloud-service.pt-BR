---
title: Integrar  [!DNL AEM Assets] ao criar conteúdo para [!DNL Edge Delivery Services]
description: Saiba como integrar o [!DNL AEM Assets] com [!DNL Edge Delivery Services]. This integration enables you to integrate [!DNL AEM Assets] com [!DNL Microsoft Word] e [!DNL Google Docs], integrate [!DNL AEM Assets] com [!DNL Universal Editor], integrate [!DNL Dynamic Media] com [!DNL Edge Delivery Services], integrate [!DNL Dynamic Media with OpenAPI capabilities] com [!DNL Universal Editor] e integrar [!DNL Dynamic Media with OpenAPI capabilities] com [!DNL Microsoft Word] e [!DNL Google Docs].
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 84fde065602d8303a03eb2c82bfa4c4bef0c1193
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# Integrar [!DNL AEM Assets] ao criar conteúdo para [!DNL Edge Delivery Services] {#integrate-aem-assets-with-edge-delivery-services}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
         <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

![Integração do AEM Assets com o editor universal](/help/assets/assets/EDS2.png)

[[!DNL Edge Delivery Services]](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/overview) é um conjunto de serviços combináveis que permite um alto grau de flexibilidade na maneira como você cria e entrega conteúdo no seu site. Você pode usar a [criação do gerenciamento de conteúdo do AEM](/help/sites-cloud/authoring/author-publish.md) e a [criação do WYSIWYG [!DNL Universal Editor] bem como a Criação baseada em documento](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

É possível editar conteúdo em:

* [[!DNL Microsoft Word] ou [!DNL Google Docs]](#integrate-dynamic-media-with-edge-delivery-services)
* [[!DNL Universal Editor]](#integrate-aem-assets-with-universal-editor-UE)

Após editar o conteúdo, você pode publicá-lo no Edge Delivery Services.

## Integrando [!DNL AEM Assets] com fluxos de Criação Baseada em Documento para [!DNL Edge Delivery Services] {#integrate-dynamic-media-with-edge-delivery-services}

Quando o [!DNL AEM Assets] se integra às suas ferramentas de Criação Baseada em Documentos, como o [!DNL Microsoft Word] ou o [!DNL Google Docs], ele fornece um seletor de ativos na sua ferramenta de criação. Use este seletor de ativos para acessar [!DNL AEM Assets] e inserir ativos aprovados em seu conteúdo.
Se você já tiver um site do [!DNL Edge Delivery Services], consulte a documentação do [[!DNL AEM Assets] plugin](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) para saber como integrar o [!DNL AEM Assets] ao seu projeto existente do [!DNL AEM].
Siga os [Pré-requisitos](#integrate-aem-assets-with-microsoft-word-and-google-docs) e [Integração [!DNL AEM Assets] com as seções do ambiente de Criação Baseada em Documentos](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) se você não tiver um site do [!DNL Edge Delivery Services] para publicar seu conteúdo inclusivo do [!DNL AEM Assets] criado nas ferramentas de criação baseadas em documentos.

### Pré-requisitos{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Antes de começar, verifique se o ambiente de Criação Baseada em Documento está pronto:

* Integre o [!DNL AEM] a uma ferramenta de Criação Baseada em Documento para configurar o ambiente de criação. Consulte [Introdução - Tutorial do desenvolvedor](https://www.aem.live/developer/tutorial) para saber como configurar o ambiente de criação.

### Integrando o [!DNL AEM Assets] ao ambiente de Criação Baseada em Documento{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Configure o plug-in do Sidekick [!DNL AEM Assets] para usar ativos durante a criação de conteúdo no [!DNL Microsoft Word] ou [!DNL Google Docs].

* Consulte [[!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) para saber como acessar e usar o AEM Assets no Microsoft Word ou Google Docs.
* Consulte [Configurando [!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin) para obter detalhes sobre a configuração.
  ![usar mídia dinâmica com recursos de openAPI no ms word e no google docs](/help/assets/assets/my-assets-sidebar.png)

## Entregar ativos usando [!DNL Dynamic Media with OpenAPI capabilities] {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

Você também pode usar os ativos entregues usando o [!DNL Dynamic Media with OpenAPI capabilities]. Ele oferece muitos benefícios, como:

* Acesso somente a ativos aprovados pela marca (imagens, vídeos, PDFs e outros tipos de ativos) do [!DNL AEM Assets Cloud Services].
* Governança (referências versus cópias do ativo), que ajuda na propagação automática de eventos do ciclo de vida do ativo, como expiração, exclusão e atualizações.
* Representações de imagem dinâmicas e Recorte inteligente.
* Otimização e entrega de mídia avançada, como transmissão contínua de vídeo adaptável pronta para uso e entrega de ativos originais para PDFs.
* Relatório de impressões no nível do ativo ([disponibilidade limitada](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Para obter mais detalhes sobre os recursos, consulte a documentação de [[!DNL Dynamic Media with OpenAPI capabilities]](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Pré-requisitos {#dynamic-media-with-universal-editor-and-edge-delivery-services}

Para usar a referência do ativo, você deve ter:

* Qualificação para um ambiente Cloud Service do Assets em que [!DNL Dynamic Media with Open API capabilities] está habilitado.
* Uma licença do [!DNL Dynamic Media].
* O [!DNL AEM Assets sidekick plugin] está habilitado com a cópia de referência para ativos de imagem habilitada. Para obter mais detalhes, consulte [esta documentação](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) para Criação Baseada em Documento e consulte [esta documentação](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para criação baseada em Editor Universal.
* Assets aprovados. Os ativos aprovados têm `dam:status=Approved` por meio das ações de back-end ou interface do usuário do Assets Cloud Services.

### Usar ativos entregues usando o [!DNL Dynamic Media with OpenAPI capabilities]{#Using-Dynamic-Media-with-edge-delivery-services}

Selecione os links a seguir para saber como usar o [!DNL Dynamic Media with OpenAPI capabilities] para fornecer imagens, vídeos e outros tipos de ativos ao seu conteúdo:

* [Adicionar imagens ao seu conteúdo](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Adicionar vídeos ao seu conteúdo](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Adicione ativos que não sejam de imagem e vídeo, como PDF, arquivos Zip e muito mais, ao seu conteúdo](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

Assista a este vídeo para saber como fornecer ativos em seu conteúdo usando o Dynamic Media com recursos de OpenAPI.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Site de exemplo [!DNL Edge Delivery Services]{#dynamic-media-with-google-docs-and-ms-word}

Consulte [WKND Travel](http://bit.ly/3DExLnf), um site que é construído usando os recursos de Criação baseada em documentos do [!DNL Edge Delivery Services]. O conteúdo do site foi criado no [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) e o [!DNL Dynamic Media with OpenAPI capabilities] é usado para entregar ativos no conteúdo. Após a criação, o conteúdo é publicado diretamente do documento. Explore este [repositório Git](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) para saber sobre todos os arquivos, pastas, configurações, estilos do site e códigos de funcionalidade essenciais usados para criar a configuração de Criação Baseada em Documento para este site [!DNL Edge Delivery Services (EDS)].

## Integrando [!DNL AEM Assets] com fluxos de criação baseados em [!DNL Universal Editor] para [!DNL Edge Delivery Services] {#integrate-aem-assets-with-universal-editor-UE}

Configure o [!DNL Universal Editor] para integrar com [!DNL AEM Assets]. Essa integração permite que você use o [!DNL Dynamic Media with OpenAPI capabilities] para entregar ativos.

* Consulte [Configuração no [!DNL Edge Delivery] Site](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) para saber como adicionar uma função de seletor de ativos personalizada no [!DNL Universal Editor]. O seletor de ativos personalizados permite inserir ativos no conteúdo do [!DNL Universal Editor] diretamente.
* Consulte [Visão geral da extensão](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para saber como acessar [!DNL AEM Assets] e inserir os ativos durante a criação em [!DNL Universal Editor].
