---
title: 'Editor de imagem '
description: O Editor de imagens é uma peça central de AEM e pode ser aproveitado por componentes para facilitar a manipulação de imagens pelos autores de conteúdo.
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---


# Editor de imagem {#image-editor}

O Editor de imagens é uma peça central de AEM e pode ser aproveitado por componentes para facilitar a manipulação de imagens pelos autores de conteúdo.

## Unidades relativas para o Mapa de imagem {#relative-units-for-image-map}

O Editor de imagens persiste nas áreas do mapa de imagem como unidades absolutas e relativas. As unidades relativas são úteis quando fornecidas como atributos de dados para redimensionar dinamicamente um mapa de imagem (relativo ao tamanho da imagem) no lado do cliente em um componente de imagem responsiva.

### propriedade imageMap {#imagemap-property}

As coordenadas do mapa de imagem são mantidas no JCR como uma propriedade `imageMap` pelo Editor de imagens. Ele tem o seguinte formato:

Os armazenamentos de propriedades mapeiam as áreas da seguinte maneira:

`[area1][area2][...]`

Formato de área:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Exemplo:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Suporte para imagens SVG {#support-for-svg-images}

O SVG (Scalable Vetor Graphics) é compatível com o Editor de imagens.

* Arrastar e soltar um ativo SVG do DAM e carregar um upload de arquivo SVG de um sistema de arquivos local são suportados.

## Ativação de plug-ins por tipo MIME {#enabling-plugins-by-mime-type}

Em determinadas situações, as ações de criação devem ser restritas para determinados tipos de MIME, devido à falta de suporte no processamento no servidor. Por exemplo, a edição de imagens SVG pode não ser permitida.

Os plug-ins no Editor de imagens podem ser habilitados seletivamente pelo tipo MIME, definindo uma propriedade `supportedMimeTypes` no nó de configuração do plug-in individual.

### Exemplo {#example}

Como exemplo, digamos que a capacidade de cortar só deve ser permitida para imagens GIF, JPEG, PNG, WEBP e TIFF.

A propriedade `supportedMimeTypes` deve ser definida como uma string dos tipos MIME permitidos no nó de configuração do plug-in no nó `cq:editConfig` do componente de imagem.

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
