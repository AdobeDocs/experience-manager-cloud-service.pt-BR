---
title: Pré-visualizar ativos 3D
description: Saiba como visualizar ativos 3D no Experience Manager.
contentOwner: Rick Brough
feature: 3D Assets
role: User
exl-id: e873bd25-f841-4063-824f-7e48f40bb678
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 5%

---

# Pré-visualizar ativos 3D no Adobe Experience Manager{#previewing-3d-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/previewing-3d-assets.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

O Experience Manager Assets é compatível com a assimilação, o gerenciamento, a pré-visualização e a entrega de ativos 3D.

É possível visualizar ativos 3D com as representações de miniatura geradas automaticamente ou o visualizador 3D interativo. O visualizador 3D interativo está disponível na página de detalhes do ativo no Experience Manager. O visualizador inclui, entre outras coisas, uma coleção de controles interativos de câmera que permitem girar, aplicar zoom e panorâmica ao redor da cena 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Formatos compatíveis com a visualização de miniaturas no Experience Manager{#supported-thumbnail-previewing-assets}

O Experience Manager gera miniaturas para os seguintes formatos de arquivo por padrão:

| Extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão GL Binária | model/gltf-binary |  |
| FBX | Autodesk FBX | application/octet-stream |  |
| OBJ | Arquivo de objeto 3D do WaveFront | application/x-tgif |  |
| 3DS | Modelo de 3D Studio | application/x-3ds |  |
| USDz | Descrição de cena universal | model/vnd.usdz+zip |  |

## Formatos compatíveis com pré-visualização 3D interativa no Experience Manager{#supported-3d-previewing-assets}

O Experience Manager suporta a pré-visualização 3D interativa para os seguintes formatos de arquivo nativamente:

| Extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão GL Binária | model/gltf-binary |  |
| GLTF | Formato de Transmissão GL | model/gltf+json | Consulte a **Nota** abaixo. |
| OBJ | Arquivo de objeto 3D do WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |


>[!NOTE]
>
>Se os materiais não renderizam na pré-visualização de um modelo gLTF, certifique-se de que sejam nomeados corretamente e em uma `textures` pasta na mesma pasta raiz do modelo, semelhante ao seguinte:

    Ativo (pasta)
    model.gltf
    model.bin
    texturas (pasta)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Considerações de desempenho ao pré-visualizar ativos 3D no Experience Manager{#performance-3d-previewing-assets}

O tempo necessário para abrir um ativo 3D na página de visualização de detalhes do ativo depende de vários fatores, como largura de banda, complexidade da imagem e latências para o servidor.

Além disso, os recursos do computador cliente - como estação de trabalho, notebook ou dispositivo de toque móvel - também são importantes ao manipular a câmera interativamente. Um sistema razoavelmente eficiente com boas capacidades gráficas pode tornar a experiência de visualização 3D interativa mais suave e favorável.

**Para visualizar ativos 3D no Experience Manager:**

1. Verifique se você carregou ativos 3D no Experience Manager.
Consulte [Formatos compatíveis com a visualização 3D](#supported-3d-previewing-assets) e [Fazer upload de ativos](/help/assets/manage-digital-assets.md#uploading-assets).
1. Do Experience Manager, no **[!UICONTROL Navegação]** página, vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.

   ![Página de navegação](/help/assets/dynamic-media/assets/navigation-assets.png)

1. Próximo ao canto superior direito da página, na lista suspensa Exibir, selecione **[!UICONTROL Exibição de cartão]**, em seguida, navegue até um ativo 3D que deseja visualizar.

   ![Seleção do cartão 3D](/help/assets/dynamic-media/assets/3d-card-select.png)
   _Na Exibição de cartão, selecione o cartão do ativo 3D que deseja visualizar._

1. Selecione o cartão do ativo 3D.

   ![Visualização interativa em 3D](/help/assets/dynamic-media/assets/3d-preview.png)
   _Visualização interativa de um ativo 3D na página de exibição de detalhes do ativo._
1. Na página da exibição Detalhes do ativo do ativo 3D, siga um destes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Girar a câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo + arraste. | Pressione com um dedo + arraste. |
   | **Deslocar a câmera** | Desloque sua exibição para a esquerda, direita, para cima ou para baixo. | Clique com o botão direito + arraste. | Pressione com dois dedos + arraste. |
   | **Aplicar zoom à sua câmera** | Mova para dentro e para fora das áreas da cena 3D. | Roda de rolagem. | Pinça de dois dedos. |
   | **Recentralize sua câmera** | Recentralize sua câmera em um ponto sobre um objeto na cena 3D. | Clique duas vezes em. | Selecione duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino de exibição para o centro do ativo 3D. A redefinição também move a câmera para mais perto ou mais longe, para mostrar o ativo em sua totalidade e em um tamanho de visualização razoável. |   |   |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone Tela cheia. |   |   |

1. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Fechar]**.
