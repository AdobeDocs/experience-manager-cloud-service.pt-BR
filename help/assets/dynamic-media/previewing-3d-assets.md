---
title: Pré-visualizar ativos 3D
description: Saiba como visualizar ativos 3D no Experience Manager.
contentOwner: Rick Brough
feature: 3D Assets
role: User
exl-id: e873bd25-f841-4063-824f-7e48f40bb678
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 4%

---

# Visualizar ativos 3D no Adobe Experience Manager{#previewing-3d-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

O Experience Manager oferece suporte para upload, delivery e visualização interativa de ativos 3D como parte do processo de criação.

O visualizador 3D interativo está disponível na página de detalhes do ativo no Experience Manager. O visualizador inclui, entre outras coisas, uma coleção de controles interativos de câmera que permitem que você orbite, amplie e desloque o ativo 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Formatos compatíveis com a visualização 3D no Experience Manager{#supported-3d-previewing-assets}

A visualização 3D interativa no Experience Manager oferece suporte aos seguintes formatos de arquivo:

| extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão binária GL | modelo/gltf-binário |  |
| GLTF | Formato de transmissão GL | model/gltf+json | Consulte a **Observação** abaixo. |
| OBJ | Arquivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Suporte apenas para ingestão; visualização não disponível. |
| USDZ | Arquivo Zip de descrição da cena universal | model/vnd.usdz+zip | Suporte apenas para ingestão; visualização não disponível. |

>[!NOTE]
>
>Se os materiais não forem renderizados na visualização de um modelo GLTF, certifique-se de que eles sejam nomeados corretamente e em um `textures` na mesma pasta raiz do modelo, semelhante ao seguinte:

    Ativo (pasta)
    model.gltf
    model.bin
    texturas (pasta)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Considerações de desempenho ao visualizar ativos 3D no Experience Manager{#performance-3d-previewing-assets}

O tempo necessário para abrir um ativo 3D na página de visualização de detalhes do ativo depende de vários fatores, como largura de banda, complexidade da imagem e latências para o servidor.

Além disso, os recursos do computador cliente - como uma estação de trabalho, um notebook ou um dispositivo de toque móvel - também são importantes a serem considerados ao manipular a câmera interativamente. Um sistema bastante poderoso com bons recursos gráficos pode tornar a experiência interativa de visualização em 3D mais fácil e favorável.

**Para visualizar ativos 3D no Experience Manager:**

1. Certifique-se de ter carregado ativos 3D no Experience Manager.
Consulte [Formatos compatíveis com a visualização 3D](#supported-3d-previewing-assets) e [Fazer upload de ativos](/help/assets/manage-digital-assets.md#uploading-assets).
1. De Experience Manager, no **[!UICONTROL Navegação]** página, vá para **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.

   ![Página de navegação](/help/assets/dynamic-media/assets/navigation-assets.png)

1. Próximo ao canto superior direito da página, na lista suspensa Exibir, selecione **[!UICONTROL Exibição de cartão]**, em seguida, navegue até um ativo 3D que deseja visualizar.

   ![Seleção do cartão 3D](/help/assets/dynamic-media/assets/3d-card-select.png)
   _Na Exibição de cartão, selecione o cartão do ativo 3D que deseja visualizar._

1. Selecione o cartão do ativo 3D.

   ![Visualização 3D interativa](/help/assets/dynamic-media/assets/3d-preview.png)
   _Visualização interativa de um ativo 3D na página de visualização de detalhes do ativo._
1. Na página de exibição de detalhes do ativo para o ativo 3D, siga um destes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Rode a câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo e arraste. | Pressione com um único dedo e arraste. |
   | **Deslocar a câmera** | Deslocar a vista para a esquerda, para a direita, para cima ou para baixo. | Clique com o botão direito + arraste. | Pressione com dois dedos e arraste. |
   | **Zoom da câmera** | Mova para dentro e para fora das áreas da cena 3D. | Roda de rolagem. | Um beliscão de dois dedos. |
   | **Recenter a câmera** | Insira novamente sua câmera em um ponto em um objeto na cena 3D. | Clique duas vezes. | Toque duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino da exibição para o centro do ativo 3D. A redefinição também aproxima ou afasta a câmera para mostrar o ativo inteiro e com um tamanho de visualização razoável. |  |  |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone de tela cheia. |  |  |

1. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Fechar]**.
