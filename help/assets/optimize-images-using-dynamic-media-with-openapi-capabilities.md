---
title: Otimizar imagens usando o Dynamic Media com recursos OpenAPI
description: Saiba como otimizar imagens em tempo real antes da entrega pública usando os recursos de otimização de imagem do Dynamic Media com recursos OpenAPI
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 3d5ae3bae9635625912a4afb2f74d002cd0ab670
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 0%

---


# Otimizar imagens usando o Dynamic Media com recursos OpenAPI{#Optimize-images-using-Dynamic-Media-with-OpenAPI-Capabilities}

[!DNL Dynamic Media with OpenAPI capabilities] oferece recursos de otimização de imagem, como [!DNL Smart Crop], [!DNL Image Presets] e [!DNL Smart Imaging]. Esses recursos ajudam a fornecer imagens responsivas de alta qualidade que são carregadas rapidamente em diferentes dispositivos e redes.

## Corte inteligente{#smart-crop-using-dynamic-media-with-openapi-capabilities}

[Recorte inteligente](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request) é uma capacidade de dimensionamento dinâmico de [!DNL Dynamic Media with OpenAPI capabilities]. [!DNL Smart Crop] é uma técnica avançada de processamento de imagens que usa o recorte com reconhecimento de conteúdo habilitado por IA para cortar imagens de forma inteligente para vários tamanhos de tela, preservando o contexto visual em versões cortadas. A IA analisa a imagem para identificar o ponto focal ou ponto de interesse pretendido e, em seguida, corta automaticamente a imagem para manter o ponto focal em todas as versões cortadas. [!DNL Smart Crop], um elemento-chave de design responsivo, fornece uma maneira econômica e eficiente de cortar imagens.

Consulte o artigo [Perfis de Imagem de Mídia Dinâmica](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles) para saber como [criar representações de Recorte Inteligente](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#creating-image-profiles) em [!DNL Admin View], [aplicá-las a pastas](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#applying-an-image-profile-to-folders) ou [editar representações](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#editing-the-smart-crop-or-smart-swatch-of-a-single-image) já aplicadas a uma imagem ou pasta. Saiba como criar um [!DNL Smart Crop] passo a passo neste [vídeo](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

O parâmetro [!DNL Smart Crop] espera que perfis de smartcrop nomeados existam e tenham sido aplicados ao ativo. Consulte [Perfis de corte inteligente](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request) para saber mais sobre o parâmetro [!DNL Smart Crop] e como perfis nomeados [!DNL Smart Crop] são aplicados.

>[!IMPORTANT]
>
> Você pode criar [!DNL Smart Crop] representações somente no modo de exibição de Administração.

## Predefinições de imagem{#image-presets-using-dynamic-media-with-openapi-capabilities}

Transforme imagens em tempo real usando o recurso [Predefinições de Imagem](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=preset&t=request) em [!DNL Dynamic Media with OpenAPI capabilities]. Um [!DNL image preset] é um conjunto predefinido de regras de dimensionamento e formatação para uma imagem de saída.

O [!DNL Dynamic Media with OpenAPI capabilities] usa nomes predefinidos para transformar uma imagem em tempo real e gerar sua representação instantaneamente. Quando você solicita uma imagem por meio de uma URL de entrega do [!DNL Dynamic Media with OpenAPI] que inclui um parâmetro predefinido, o [!DNL DM with OpenAPI] aplica as transformações da predefinição, cria a representação sob demanda e a entrega ao usuário.

É possível aplicar uma única predefinição a várias imagens por meio das URLs de entrega de [!DNL Dynamic Media with OpenAPI]. Isso garante uma formatação consistente entre os ativos sem editar manualmente cada um.

Consulte o artigo [gerenciando predefinições de imagens](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets) para saber [como criar predefinições de imagens no Modo de Exibição de Administração](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-image-presets) e [como criar predefinições de imagens responsivas](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-a-responsive-image-preset) que adaptam ativos automaticamente para se ajustarem a diferentes tamanhos de tela.

### Benefícios do uso de predefinições de imagem{#benefits-of-image-presets}

O [!DNL Image Presets] oferece várias vantagens para gerenciar e fornecer imagens no [!DNL Dynamic Media with OpenAPI]. Alguns dos principais benefícios incluem:

* As predefinições encurtam os URLs de entrega de imagens. Em vez de adicionar vários modificadores de imagem que tornam o URL de entrega mais longo, use uma única predefinição. URLs mais curtos são mais fáceis de gerenciar e garantem uma entrega consistente de imagens em sites, aplicativos móveis, emails e outros canais.
* As predefinições de imagem criam representações just-in-time de um arquivo de imagem de origem. Esse recurso de geração de representação sob demanda elimina a necessidade de criar e armazenar várias representações estáticas do mesmo arquivo, economizando tempo e armazenamento.
* Aplique uma única predefinição a um grande conjunto de ativos de uma só vez, evitando edições manuais em cada ativo individualmente, garantindo uma formatação consistente e permitindo escalabilidade.
* Ao atualizar os parâmetros de uma predefinição, todas as imagens que usam essa predefinição são reformatadas automaticamente. Isso simplifica a edição centralizando as atualizações de formatação, eliminando a necessidade de reeditar ativos individuais ou código da Web.
* Melhora a eficiência e o desempenho com representações dinâmicas armazenadas em cache pela CDN, resultando em carregamento mais rápido e desempenho otimizado em dispositivos e redes.

### Usar predefinições de imagem{#use-image-presets-using-dynamic-media-with-openapi-capabilities}

Depois de criar o [!DNL Image Presets], você pode usá-los para os seguintes fluxos de trabalho:

* [Use predefinições no URL de entrega de imagens para criar suas representações em tempo real antes de entregá-las ao usuário final](#use-presets-in-delivery-urls)
* [Usar predefinições durante a criação no AEM Sites](#use-presets-during-authoring-in-aem-sites)

#### Usar predefinições no URL de entrega da imagem{#use-presets-in-delivery-urls}

As predefinições tornam os URLs de entrega mais curtos e fáceis de usar.  Cada nome predefinido serve como um identificador exclusivo no URL de entrega. Em vez de adicionar vários modificadores ao URL de entrega de um ativo, faça referência ao nome predefinido para gerar sua representação instantaneamente. [Saiba como aplicar Predefinições de Imagem do Dynamic Media à sua imagem](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-presets).
O exemplo a seguir compara um URL com uma predefinição a um URL sem uma predefinição.

**URL sem uma predefinição (URL longa)**:

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?width=400&height=300&fit=crop&qualit=85&sharpen=true
```

**URL com uma predefinição (URL curta)**:

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?preset=thumbnail
```

A miniatura predefinida agrupa as mesmas configurações do modificador de imagem.

#### Usar predefinições durante a criação no AEM Sites{#use-presets-during-authoring-in-aem-sites}

Os autores podem selecionar [!DNL Image Presets] durante a edição da página na página de criação [!DNL AEM Sites], quando o suporte para [!DNL Dynamic Media] estiver habilitado.
Execute as seguintes etapas para usar predefinições de imagem na página de criação:
1. Navegue até a página de criação do Sites.
1. Execute as etapas na seção [Acessar ativos remotos no Editor de páginas do AEM](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) para usar o painel [!DNL Asset Selector] para selecionar um ativo.
1. No painel [!DNL asset selector], role até **[!UICONTROL Tipo de predefinição]**, especifique `Preset=Preset Name` no campo **[!UICONTROL Modificadores de imagem]** e clique em **[!UICONTROL Concluído]**.
   ![predefinição](/help/assets/assets/preset-in-asset-selector-panel.png)

## Imagem inteligente{#use-smart-imaging-using-dynamic-media-with-openapi-capabilities}

Quando você usa o [!DNL Dynamic Media with OpenAPI capabilities] para entrega de imagens, as imagens são otimizadas automaticamente por meio da [Imagem inteligente](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/). A entrega otimizada garante que as imagens sejam carregadas mais rapidamente, tenham qualidade visual máxima e tamanho mínimo de arquivo. Isso resulta em carregamentos de página mais rápidos e qualidade visual consistentemente alta em todos os dispositivos e redes, consumindo o mínimo de largura de banda, tornando seu site mais rápido e mais ágil.

[!DNL Smart Imaging] inclui os seguintes recursos:

* [Conversão automática de formatação](#auto-format-conversion)
* [Otimização da largura de banda da rede](#network-bandwidth-optimisation)

### Conversão automática de formatação{#auto-format-conversion}

O [!DNL Dynamic Media with OpenAPI] [converte automaticamente imagens em formatos modernos e otimizados para a Web, como AVIF ou WEBP](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=auto-format&t=request). A conversão depende dos recursos do navegador e do [direito-licença](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate), independentemente do formato solicitado.

Os formatos AVIF e WEBP oferecem melhor compactação, tornando as imagens menores e mais rápidas de serem entregues e carregadas. O AVIF é usado como o formato padrão, pois lida com todos os recursos do navegador.

[!DNL Dynamic Media with OpenAPI] usa o parâmetro de consulta `auto-format` para controlar o comportamento do navegador para converter uma imagem em vários formatos para entrega otimizada. A conversão de formatação automática inclui **promoção automática** e **rebaixamento automático**. Quando o sistema promove um formato otimizado para a Web (AVIF ou WEBP) em JPEG ou PNG para entrega, ele é chamado de promoção automática.

Por padrão, o parâmetro de consulta `auto-format` está definido como `true`. Quando o `auto-format` está habilitado (true), o sistema ignora o formato solicitado e seleciona automaticamente um formato otimizado para a Web (AVIF ou WEBP) com base nas características da imagem, nos recursos do navegador e no [direito de licença](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate).

Quando `auto-format` é verdadeiro, o sistema fornece o formato de imagem na seguinte sequência:

* ***AVIF***: o AVIF será entregue se o navegador permitir e a licença permitir. Isso é chamado de promoção automática.
* ***WEBP***: o WEBP será entregue se o AVIF não tiver suporte ou licença. Também é uma promoção automática.
* ***JPEG***: o JPEG é entregue somente quando não há suporte para AVIF e WEBP e a imagem não tem um canal alfa (transparência). Isso é chamado de rebaixamento automático.
* ***PNG***: o PNG é entregue quando o navegador não oferece suporte a formatos modernos e a imagem tem um canal alfa (transparência). Isso também é chamado de rebaixamento automático.

Desabilite `auto-format` definindo o parâmetro de consulta como `false` e especifique o formato necessário para obter a imagem entregue nesse formato.

### Otimização da largura de banda da rede{#network-bandwidth-optimisation}

As imagens são otimizadas automaticamente com base nas condições de rede do cliente para garantir uma entrega mais rápida e um carregamento suave. Os parâmetros [Quality](#quality-parameter) e [Max-quality](#max-quality-parameter) ajustam automaticamente a qualidade controlando os níveis de compactação de imagem, com valores variando de 1 a 100.

Veja os seguintes comportamentos de chave de `quality` e `max-quality ` parâmetros:

* Se [!DNL quality] e [!DNL max-quality] forem especificados, [!DNL quality] terá prioridade.
* Se apenas [!DNL quality] for especificado, a qualidade será entregue independentemente do tempo de carregamento com base na velocidade da rede.
* Se apenas [!DNL max-quality] for especificado, a qualidade da imagem será ajustada automaticamente com base nas condições da rede, fornecendo a melhor qualidade possível até o valor [!DNL max-quality] especificado.
* Se nenhum for especificado, o sistema aplicará a otimização dinâmica com um padrão `max-quality` de `85`.

#### Parâmetro de qualidade{#quality-parameter}

O parâmetro de qualidade prioriza a qualidade da imagem em relação à velocidade de carregamento. Ele corrige a qualidade da imagem de saída para o valor solicitado (entre 1 e 100) e ignora as condições da rede. Saiba mais sobre o [parâmetro de qualidade](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request).

#### Parâmetro de qualidade máxima{#max-quality-parameter}

A qualidade máxima equilibra a qualidade da imagem e o tempo de carregamento com base na velocidade da rede do cliente. Ele prioriza tempos de carregamento mais rápidos ao reduzir a qualidade da imagem em redes mais lentas, ao mesmo tempo em que fornece a maior qualidade possível (1-100) para as condições de rede especificadas. Saiba mais sobre o [parâmetro de qualidade máxima](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request).
