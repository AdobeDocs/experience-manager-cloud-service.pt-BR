---
title: Editor de imagem
description: O Editor de imagens é um componente central do AEM e pode ser aproveitado por componentes para facilitar a manipulação de imagens por autores de conteúdo.
exl-id: c8ae4f59-75b1-49b4-8dd4-957d2e33000b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---

# Editor de imagem  {#image-editor}

O Editor de imagens é um componente central do AEM e pode ser aproveitado por componentes para facilitar a manipulação de imagens por autores de conteúdo.

## Unidades relativas do mapa de imagem {#relative-units-for-image-map}

O Editor de imagens mantém as áreas do mapa de imagens como unidades absolutas e relativas. As unidades relativas são úteis quando fornecidas como atributos de dados para redimensionar dinamicamente um mapa de imagem (em relação ao tamanho da imagem) no lado do cliente em um componente de imagem responsivo.

### Propriedade imageMap {#imagemap-property}

As coordenadas do mapa de imagem são mantidas para o JCR como uma `imageMap` propriedade pelo Editor de imagens. Ela tem o formato a seguir.

A propriedade armazena áreas de mapa da seguinte maneira:

`[area1][area2][...]`

Formato da área:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Exemplo:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Suporte para imagens SVG {#support-for-svg-images}

Scalable Vetor Graphics (SVG) são compatíveis com o Editor de imagens.

* Tanto o processo de arrastar e soltar um ativo SVG do DAM quanto o de fazer upload de um arquivo SVG de um sistema de arquivos local são compatíveis.

## Habilitando plug-ins por tipo de MIME {#enabling-plugins-by-mime-type}

Em determinadas situações, as ações de criação devem ser restritas para determinados tipos MIME, devido à falta de suporte no processamento do lado do servidor. Por exemplo, a edição de imagens de SVG pode não ser permitida.

Os plug-ins no Editor de imagens podem ser ativados seletivamente pelo tipo MIME ao configurar um `supportedMimeTypes` no nó de configuração do plug-in individual.

### Exemplo {#example}

Como exemplo, digamos que a capacidade de recorte só seja permitida para imagens de GIF, JPEG, PNG, WEBP e TIFF.

A variável `supportedMimeTypes` A propriedade deve ser definida como uma cadeia de caracteres dos tipos MIME permitidos no nó de configuração do plug-in na `cq:editConfig` nó do componente de imagem.

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
