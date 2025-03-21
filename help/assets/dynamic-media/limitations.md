---
title: Limitações do Dynamic Media
description: Saiba mais sobre as práticas recomendadas e os limites impostos ao criar um Conjunto de imagens ou um Conjunto de rotação ou fazer upload de uma PDF. Saiba mais sobre combinações incompatíveis de navegador da Web e sistema operacional para Dynamic Media.
contentOwner: Rick Brough
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 2%

---

# Limitações do Dynamic Media

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
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

As seções a seguir descrevem as limitações do Dynamic Media.

Este tópico inclui as seguintes seções:

* [Práticas recomendadas e limites impostos pelo Dynamic Media em tipos de ativos](#best-practice-enforced-limits)
* [Combinações de navegador da Web e sistema operacional não compatíveis com o Dynamic Media](#unsupported-browser-os)

## Práticas recomendadas e limites impostos pelo Dynamic Media em tipos de ativos {#best-practice-enforced-limits}

Ao criar um Conjunto de rotação ou um Conjunto de imagens, ou fazer upload de PDFs para extração de página, a Adobe recomenda as seguintes práticas recomendadas e impõe os seguintes limites:

| Ativo - Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| **Imagem** - Número de Recortes Inteligentes por imagem | 5 | 100 |
| **Todos os conjuntos** - Número de ativos duplicados por conjunto | Sem duplicatas | 20 |
| **Todos os conjuntos** - Número máximo de ativos por conjunto | De 5 a 10 imagens por conjunto | 1000 |
| **Grupo de rotação** - Número máximo de linhas/colunas por conjunto 2D | 12 a 18 imagens por conjunto | 1000 |
| **PDF** - Número máximo de páginas para que uma PDF seja considerada para extração |  | 100 (para todos os PDFs) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Combinações de navegador da Web e sistema operacional não compatíveis com o Dynamic Media {#unsupported-browser-os}

O Dynamic Media não é compatível com as seguintes combinações de navegador da Web e sistema operacional.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Atualização do Windows Phone 8.1
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## Fim do suporte para Secure Socket Layer 2.0 e 3.0 e Transport Layer Security 1.0 e 1.1 {#tls}

<!-- CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->

A partir de 30 de abril de 2024, o Adobe Dynamic Media encerrará o suporte para o seguinte:

* SSL (Secure Socket Layer) 2.0
* SSL 3.0
* TLS (Transport Layer Security) 1.0 e 1.1
* As seguintes cifras fracas no TLS 1.2:
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_RSA_WITH_AES_256_GCM_SHA384`
   * `TLS_RSA_WITH_AES_256_CBC_SHA256`
   * `TLS_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_AES_128_GCM_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
   * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`
