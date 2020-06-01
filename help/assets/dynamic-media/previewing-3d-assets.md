---
title: Visualização de ativos 3D
description: Saiba como pré-visualização ativos 3D
translation-type: tm+mt
source-git-commit: e8b6f7e80c1a19c645e1c848a6bfe5c082935d21
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 16%

---


# Visualização de ativos 3D{#previewing-3d-assets}

O Experience Manager oferece suporte ao carregamento, delivery e pré-visualização interativa de ativos 3D como parte do processo de criação.

 O visualizador 3D interativo está disponível na página de detalhes do ativo no AEM. O visualizador inclui, entre outras coisas, uma coleção de controles de câmera interativos que permitem girar, aplicar zoom e deslocar o ativo 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Formatos suportados para pré-visualização 3D{#supported-3d-previewing-assets}

A pré-visualização 3D interativa suporta os seguintes formatos de arquivo:

| extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão binária do GL | model/gltf-binary |  |
| GLTF | Formato de transmissão GL | model/gltf+json | Consulte a **Nota** abaixo. |
| OBJ | Arquivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Apoio unicamente à ingestão; pré-visualização não disponível. |
| USDZ | Arquivo Zip de descrição do Universal Scene | model/vnd.usdz+zip | Apoio unicamente à ingestão; pré-visualização não disponível. |

**Observação**: Se os materiais não forem renderizados na pré-visualização de um modelo gLTF, verifique se eles foram nomeados corretamente e se estão localizados em uma `textures` pasta na mesma pasta raiz do modelo, semelhante ao seguinte:

    Ativo (pasta)
    model.
    gltfmodel.
    bintextures (pasta)
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## Performance considerations when you preview 3D assets{#performance-3d-previewing-assets}

O tempo necessário para abrir um ativo 3D na página de visualização de detalhes do ativo depende de vários fatores, como largura de banda, complexidade da imagem e latências para o servidor.

Além disso, os recursos do computador cliente, como uma estação de trabalho, um notebook ou um dispositivo de toque móvel, também são importantes de se considerar ao manipular a câmera interativamente. Um sistema bastante eficiente com bons recursos gráficos pode tornar a experiência de visualização interativa em 3D mais fácil e favorável.

**Para pré-visualização de ativos 3D**

1. Verifique se você fez upload dos ativos 3D no AEM.
See [Supported formats for 3D preview](#supported-3d-previewing-assets) and [Uploading assets](/help/assets/manage-digital-assets.md#uploading-assets).
1. No AEM, na página **[!UICONTROL Navegação]** , toque em **[!UICONTROL Ativos > Arquivos]**.

   ![Página de navegação](/help/assets/dynamic-media/assets/navigation-assets.png)

1. Próximo ao canto superior direito da página, na lista suspensa Exibição, toque em **[!UICONTROL Exibição de cartão]** e navegue até um ativo 3D que deseja visualizar.

   ![Seleção de cartão 3D](/help/assets/dynamic-media/assets/3d-card-select.png)
   _Na Visualização do cartão, toque na placa do ativo 3D que você deseja pré-visualização._

1. Toque no cartão do ativo 3D para abri-lo na página de visualização de detalhes do ativo.

   ![pré-visualização 3D interativa](/help/assets/dynamic-media/assets/3d-preview.png)
   _pré-visualização interativa de um ativo 3D na página de visualização de detalhes do ativo._
1. Na página de visualização de detalhes do ativo 3D, execute um dos procedimentos a seguir:
   * **Vire sua câmera**—Orbite sua visualização em torno da cena 3D e dos objetos.
      * _Mouse_: Clique com o botão esquerdo + arraste.
      * _Tela_ sensível ao toque: Pressione um único dedo + arraste.
   * **Deslocar sua câmera**- Desloce a visualização para a esquerda, direita, para cima ou para baixo.
      * _Mouse_: Clique com o botão direito do mouse e arraste.
      * _Tela_ sensível ao toque: Pressione com dois dedos e arraste.
   * **Zoom na câmera**—Aplica zoom na câmera para mover para dentro e para fora das áreas da cena 3D.
      * _Mouse_: Roda de rolagem.
      * _Tela_ sensível ao toque: Pinça com dois dedos.
   * **Recenter your camera**— Recenter your camera to a point on a object in a 3D scenation (Recentro em cena sua câmera, insira novamente sua câmera em um ponto de um objeto na cena 3D).
      * _Mouse_: Duplo-clique.
      * _Tela_ sensível ao toque: Toque em Duplo.
   * **Redefinir**— próximo ao canto inferior direito da página, toque no ícone Redefinir para restaurar o ponto de público alvo da visualização para o centro do ativo 3D. A redefinição também aproxima a câmera ou afasta-a para mostrar o ativo na totalidade e em um tamanho de visualização razoável.
   * **Modo** de tela cheia — Para entrar no modo de tela cheia, no canto inferior direito da página, toque no ícone Tela cheia.

1. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Close]**.
