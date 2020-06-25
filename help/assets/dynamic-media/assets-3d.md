---
title: Trabalhar com ativos 3D na Dynamic Media
seo-title: Trabalhar com ativos 3D na Dynamic Media
description: Saiba como trabalhar com ativos 3D na Dynamic Media
seo-description: Saiba como trabalhar com ativos 3D na Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and AEM as a Cloud Service
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: b44e6a522b6f2363daa40c6c6f9640ba2fadd35e
workflow-type: tm+mt
source-wordcount: '2276'
ht-degree: 5%

---


# Trabalhar com ativos 3D na Dynamic Media {#working-with-three-d-assets-dm}

A Dynamic Media permite que você carregue, gerencie, visualização e entregue ativos 3D como experiências imersivas.

* Publicação com um clique (usando a Publicação **** rápida na barra de ferramentas) de ativos 3D para gerar um URL.
* Suporte otimizado para exibir ativos 3D com a predefinição do visualizador Dimensional interativo de alta qualidade, capacitado pelo Adobe Dimension.
* O componente WCM de mídia 3D permite que você adicione facilmente ativos 3D às suas páginas de AEM Sites.

Não há necessidade de instalação adicional para usar ativos 3D no Dynamic Media.

![sapato em 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes.](/help/release-notes/aem3d-release-notes.md) -->

## Formatos 3D suportados no Dynamic Media {#supported-three-d-file-formats-in-dm}

A Dynamic Media oferece suporte aos seguintes formatos de arquivo 3D.

Consulte também formatos [3D suportados](/help/assets/file-format-support.md#supported-3d-formats)

| extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão binária do GL | model/gltf-binary | Inclui os materiais e as texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Arquivo Zip de descrição do Universal Scene | model/vnd.usdz+zip | *Apoio unicamente à ingestão; nenhuma visualização ou interação está disponível.* USDZ é um formato 3D proprietário que pode ser visualizado nativamente pelo Safari ou iOS. |

## Start rápido: Recursos 3D no Dynamic Media {#quick-start-three-d}

A seguinte descrição passo a passo do fluxo de trabalho foi projetada para ajudá-lo a iniciar e executar rapidamente com ativos 3D no Dynamic Media.

Antes de trabalhar com ativos 3D no Dynamic Media, verifique se o administrador do AEM já habilitou e configurou Cloud Service Dynamic Media.

Consulte [Configuração de Cloud Service Dynamic Media.](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

1. **Carregar ativos 3D**

   * [Fazer upload de seus ativos 3D para uso no Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Formatos de arquivo 3D suportados para upload no Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Gerenciar ativos 3D**

   * Organizar e pesquisar ativos 3D

      * [Organização de ativos digitais](/help/assets/organize-assets.md)
      * [Pesquisar ativos 3D](/help/assets/search-assets.md)
   * Visualização de ativos 3D

      * [Exibir e interagir com ativos 3D](#viewing-three-d-assets)
      * [Gerenciar a predefinição do visualizador Dimensional](/help/assets/dynamic-media/managing-viewer-presets.md)
   * Trabalhar com metadados de ativos 3D

      * [Gerenciamento de metadados para ativos digitais](/help/assets/manage-digital-assets.md#editing-properties)
      * [Esquemas de metadados](/help/assets/metadata-schemas.md)



1. **Publicar ativos 3D**

   * [Publicar ativos estáticos Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar ativos 3D do Dynamic Media usando o Visualizador Dimensional](#alternate-publish-methods)

## Sobre a visualização e interação com ativos 3D {#viewing-three-d-assets}

Esta seção descreve como visualização e interagir com ativos 3D de duas maneiras diferentes: na página de detalhes do ativo e a partir do componente de mídia 3D no Sites.

O visualizador 3D interativo inclui, entre outras coisas, uma coleção de controles de câmera interativos que permitem que você orbite, aplique zoom e desloce o ativo 3D.

Esteja ciente de que o tempo necessário para abrir um ativo 3D na visualização da página Detalhes do ativo depende de vários fatores. Esses fatores incluem informações como as seguintes:

* Largura de banda para o servidor.
* Latências para o servidor
* Complexidade da imagem.

Além disso, os recursos do computador cliente, como uma estação de trabalho, um notebook ou um dispositivo de toque móvel, também são importantes de se considerar ao manipular a câmera interativamente. Um sistema bastante eficiente com bons recursos gráficos pode tornar a experiência de visualização interativa em 3D mais fácil e favorável.

>[!TIP]
>
>Você pode abrir a predefinição do visualizador Dimensional no Editor de predefinições do visualizador para praticar a navegação de um ativo 3D sem a necessidade de primeiro carregar qualquer arquivo 3D. A predefinição do visualizador Dimensional tem um ativo 3D incorporado para você interagir.
>
>See [Managing viewer presets.](/help/assets/dynamic-media/managing-viewer-presets.md)

## Exibir e interagir com um ativo 3D na página de detalhes do ativo {#viewing-three-d-assets-from-asset-details-page}

Consulte também [Visualizar ativos usando a interface de software.](/help/assets/dynamic-media/previewing-assets.md)

**Para visualização e interação com um ativo 3D na página de detalhes do ativo**

1. Verifique se você fez upload dos ativos 3D no AEM.

   Consulte [Fazer upload de ativos 3D para uso no Dynamic Media.](/help/assets/add-assets.md#upload-assets)

1. No AEM, na página **[!UICONTROL Navegação]** , toque em **[!UICONTROL Ativos > Arquivos]**.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL Card View]**.
1. Navegue até o ativo 3D que deseja visualizar.
1. Toque no cartão de ativo 3D para abri-lo na página de detalhes do ativo.
1. Na página de visualização de detalhes do ativo 3D, execute um dos procedimentos a seguir:

   * **Rode sua câmera** - Orbite sua visualização em torno da cena 3D e dos objetos.
      * _Mouse_: Clique com o botão esquerdo + arraste.
      * _Tela_ sensível ao toque: Pressione um único dedo + arraste.
   * **Deslocar sua câmera** - Desloce sua visualização para a esquerda, direita, para cima ou para baixo.
      * _Mouse_: Clique com o botão direito do mouse e arraste.
      * _Tela_ sensível ao toque: Pressione com dois dedos e arraste.
   * **Zoom na sua câmera** - Zoom na câmera para mover para dentro e para fora das áreas da cena 3D.
      * _Mouse_: Roda de rolagem.
      * _Tela_ sensível ao toque: Pinça com dois dedos.
   * **Recenter your camera** - Recenter your camera to a point on a object in the 3D scenation (Recentro em cena sua câmera - Insira novamente sua câmera em um ponto em um objeto na cena 3D).
      * _Mouse_: Duplo-clique.
      * _Tela_ sensível ao toque: Toque em Duplo.
   * **Redefinir** - próximo ao canto inferior direito da página, toque no ícone Redefinir para restaurar o ponto de público alvo da visualização para o centro do ativo 3D. A redefinição também aproxima a câmera ou afasta-a para mostrar o ativo na totalidade e em um tamanho de visualização razoável.
   * **Modo** de tela cheia - Para entrar no modo de tela cheia, no canto inferior direito da página, toque no ícone Tela cheia.

1. No canto superior direito da página, toque em **[!UICONTROL Fechar]** para voltar à página Assets.

## Exibir e interagir com um ativo 3D dentro de um componente de mídia 3D {#interacting-with-asset-inside-three-d-media-component}

Quando uma página da Web está no modo **[!UICONTROL Editar]** , nenhuma interação é possível com um ativo 3D. Para tornar o ativo interativo, você pode usar o recurso de **[!UICONTROL Pré-visualização]** para visualização da página da Web no editor de páginas com total acesso à funcionalidade do componente de mídia 3D.

>[!IMPORTANT]
>
>Você pode realizar essa tarefa somente depois de ter adicionado um componente de mídia 3D a uma página da Web e atribuído um ativo 3D ao componente. Consulte [Adicionar o componente de mídia 3D a uma página](#adding-the-three-d-media-component-to-a-web-page) da Web e [Atribuir um ativo 3D a um componente de mídia 3D.](#assigning-a-three-d-asset-to-the-component)

Consulte também [Visualizar ativos usando a interface de software.](/help/assets/dynamic-media/previewing-assets.md)

**Para visualização e interação com um ativo 3D dentro de um componente de mídia 3D**

1. Enquanto uma página da Web estiver no modo **[!UICONTROL Editar]** , execute um dos procedimentos a seguir:

   * Perto do canto superior direito da página, clique em **[!UICONTROL Pré-visualização]** para entrar no modo **[!UICONTROL Pré-visualização]** .
   * Exclua `/editor.html` do URL da página no navegador.

Um ativo 3D totalmente interativo, conforme exibido em    ![Ativo 3D exibido dentro do componente](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)Mídia 3D Um ativo 3D totalmente interativo como exibido no modo de **[!UICONTROL Pré-visualização]** .

1. No modo de **[!UICONTROL Pré-visualização]** , execute um dos procedimentos a seguir:

   * **Rode sua câmera** - Orbite sua visualização em torno da cena 3D e dos objetos.
      * _Mouse_: Clique com o botão esquerdo + arraste.
      * _Tela_ sensível ao toque: Pressione um único dedo + arraste.
   * **Deslocar sua câmera** - Desloce sua visualização para a esquerda, direita, para cima ou para baixo.
      * _Mouse_: Clique com o botão direito do mouse e arraste.
      * _Tela_ sensível ao toque: Pressione com dois dedos e arraste.
   * **Zoom na sua câmera** - Zoom na câmera para mover para dentro e para fora das áreas da cena 3D.
      * _Mouse_: Roda de rolagem.
      * _Tela_ sensível ao toque: Pinça com dois dedos.
   * **Recenter your camera** - Recenter your camera to a point on a object in the 3D scenation (Recentro em cena sua câmera - Insira novamente sua câmera em um ponto em um objeto na cena 3D).
      * _Mouse_: Duplo-clique.
      * _Tela_ sensível ao toque: Toque em Duplo.
   * **Redefinir** - próximo ao canto inferior direito da página, toque no ícone Redefinir para restaurar o ponto de público alvo da visualização para o centro do ativo 3D. A redefinição também aproxima a câmera ou afasta-a para mostrar o ativo na totalidade e em um tamanho de visualização razoável.
   * **Modo** de tela cheia - Para entrar no modo de tela cheia, no canto inferior direito da página, toque no ícone Tela cheia.

## Sobre como trabalhar com o componente de mídia 3D {#working-with-three-d-media-component}

A Dynamic Media inclui um componente de mídia 3D da Dynamic Media que você pode usar em AEM Sites para permitir a visualização interativa de modelos 3D em suas páginas da Web.

* [Adicionar o componente de mídia 3D ao modelo de página](#adding-three-d-media-component-to-page-template)
* [Adicionar o componente de mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional - Configuração do componente de mídia 3D](#configuring-the-three-d-component)
* [Atribuição de um ativo 3D ao componente de mídia 3D](#assigning-a-three-d-asset-to-the-component)


## Adicionar o componente de mídia 3D ao modelo de página {#adding-three-d-media-component-to-page-template}

1. Navegue até **[!UICONTROL Ferramentas > Geral > Modelos]**.
1. Navegue até o modelo de página no qual você deseja ativar o componente 3D e selecione o modelo.
1. Toque em **[!UICONTROL Editar]** para abrir o modelo.
1. Próximo ao canto superior direito da página, no menu suspenso, selecione o modo **[!UICONTROL Estrutura]** , se ainda não estiver ativo.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Toque em uma área vazia na região do Container **** Layout para selecioná-la e abrir a barra de ferramentas associada.
1. Na barra de ferramentas, toque no ícone **[!UICONTROL Política]** para abrir o Editor **[!UICONTROL de]** políticas.
1. Na seção **[!UICONTROL Propriedades]** , na guia Componentes **** permitidos, role até **[!UICONTROL Dynamic Media]**, expanda a lista e marque Mídia **** 3D.
1. Toque em **[!UICONTROL Concluído]** para salvar as alterações e fechar o Editor **[!UICONTROL de]** políticas.

   Agora você pode colocar o componente de mídia 3D do Dynamic Media em todas as páginas que usam esse modelo.

## Adicionar o componente de mídia 3D a uma página da Web {#adding-the-three-d-media-component-to-a-web-page}

Se você estiver usando o Adobe Experience Manager como seu sistema de gestão de conteúdo da Web, poderá adicionar ativos 3D às suas páginas da Web por meio do componente de mídia 3D.

See also [Adding Dynamic Media assets to pages.](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

1. Abra AEM Sites e selecione a página da Web à qual deseja adicionar o componente de mídia 3D do Dynamic Media.
1. Toque no ícone **[!UICONTROL Editar]** (lápis) para abrir a página no editor de páginas. Verifique se o modo **[!UICONTROL Editar]** está selecionado perto do canto superior direito da página.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. Na barra de ferramentas, toque no ícone Painel lateral para alternar ou &quot;ativar&quot; a exibição do painel.

1. No painel lateral, toque no ícone de sinal de mais para abrir a lista **[!UICONTROL Componentes]** .

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Arraste o componente de mídia **[!UICONTROL 3D da lista]** Components **** para o local na página onde deseja que o visualizador 3D apareça.

Agora você está pronto para atribuir um ativo 3D ao componente.

Consulte [Atribuindo um ativo 3D a um componente de mídia 3D.](#assigning-a-three-d-asset-to-the-component)

### Opcional - Configuração do componente de mídia 3D {#configuring-the-three-d-component}

1. No editor de páginas AEM Sites, selecione o componente **[!UICONTROL 3D Media Viewer]** que você adicionou anteriormente à página.
1. Toque no ícone **[!UICONTROL Configuração]** (chave) para abrir a caixa de diálogo de configuração do componente.

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. Na caixa de diálogo Mídia 3D, na lista suspensa Predefinições do visualizador, selecione **[!UICONTROL Dimensionamento]** para atribuir a predefinição do visualizador Dimensional ao componente.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. No canto superior direito, toque na marca de seleção para salvar as alterações.

## Atribuição de um ativo 3D ao componente de mídia 3D {#assigning-a-three-d-asset-to-the-component}

Depois de adicionar um componente de mídia 3D a uma página da Web, você pode atribuir um ativo 3D a ela.

Consulte [Adicionar o componente de mídia 3D a uma página da Web.](#adding-the-three-d-media-component-to-a-web-page)

1. No editor de páginas AEM Sites, clique no ícone **[!UICONTROL Ativos]** para abrir **[!UICONTROL Ativos]** no painel lateral.
1. Na lista suspensa, selecione **[!UICONTROL 3D]** para mostrar apenas os tipos de arquivos de ativos 3D.
1. No painel lateral, procure ou role até o ativo 3D que você deseja que seja visualização na página que está sendo editada.
1. Arraste o ativo 3D do painel lateral Ativos e solte-o no componente Mídia **** 3D que você adicionou anteriormente à página.

   ![Atribuir ativo 3d ao componente de mídia 3d](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Enquanto uma página da Web está no modo **[!UICONTROL Editar]** do AEM Sites, o componente Mídia 3D exibe o ativo 3D, mas nenhuma interação com o ativo é possível. Para tornar o ativo interativo, você pode usar o recurso de **[!UICONTROL Pré-visualização]** para visualização da página da Web no editor de páginas com total acesso à funcionalidade do componente de mídia 3D.

## Publicar ativos estáticos Dynamic Media 3D {#publishing-three-d-assets}

A Dynamic Media aceita uma variedade de formatos de arquivo 3D suportados como conteúdo ** estático no Dynamic Media. O conteúdo estático significa que você pode fazer upload e publicar ativos 3D, mas não há suporte para geração de imagens *dinâmicas* ou para redefinição de imagens que esteja associada ao ativo 3D. O motivo é que o Dynamic Media Imaging Server não reconhece formatos 3D. Assim, depois de publicar um ativo 3D no Dynamic Media, você tem um URL instantâneo que pode ser copiado. O URL do ativo 3D segue a estrutura normal de URL da Dynamic Media. No entanto, não é possível editar nenhum parâmetro no URL do ativo, ao contrário dos ativos de imagem tradicionais no Dynamic Media.

Consulte também [Obter um URL para um ativo estático.](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)

Na Visualização **[!UICONTROL de]** cartão, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda da data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

Se você estiver usando o AEM como seu WCM, use este método de publicação para adicionar os ativos 3D da Dynamic Media diretamente na sua página da Web.

Consulte também [Publicação de ativos da Dynamic Media.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

Consulte também [Publicar páginas.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

**Para publicar ativos 3D estáticos do Dynamic Media**

1. Abra um ativo 3D (formato de arquivo GLB, OBJ ou STL) para visualização na página de detalhes do ativo.
1. Na barra de ferramentas, toque em Publicação **[!UICONTROL rápida]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Toque em **[!UICONTROL Fechar]** para sair da caixa de diálogo e retornar à página de detalhes do ativo.
1. Na lista suspensa à esquerda do nome de arquivo do ativo 3D, toque em **[!UICONTROL Representações]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Toque em **[!UICONTROL original]**. Quando um ativo 3D é publicado (ou &quot;ativado&quot;), o botão **[!UICONTROL URL]** aparece próximo ao canto inferior esquerdo da página se todas as seguintes condições de ativo 3D forem atendidas:
   * O ativo 3D é um formato compatível (GLB, OBJ, STL e USDZ).
   * O ativo 3D foi assimilado ao Dynamic Media Image Production System (IPS).
   * O ativo 3D é publicado.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Toque em **[!UICONTROL URL]** para exibir o URL de produção direta do ativo 3D que você pode copiar e usar em páginas da Web.

### Métodos alternativos para publicar ativos 3D do Dynamic Media usando o Visualizador Dimensional {#alternate-publish-methods}

Use os dois métodos a seguir para publicar ativos Dynamic Media 3D se *não* estiver usando o AEM como seu WCM.

* **[!UICONTROL URL]** - Use o **[!UICONTROL URL]** se estiver usando um sistema de gestão de conteúdo da Web de terceiros e quiser vincular ativos 3D da Dynamic Media a suas páginas da Web usando o Visualizador Dimensional.

   See [Linking URLs to your web application.](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)

* **[!UICONTROL Incorporar]** - Use **[!UICONTROL Incorporar]** quando quiser visualização um ativo Dynamic Media 3D incorporado em uma página da Web usando o Visualizador Dimensional. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. Editing of the code is not permitted in the **[!UICONTROL Embed]** dialog box.

   Consulte [Incorporação do Dynamic Media Video, do Visualizador de imagens ou do Visualizador de dimensões em uma página da Web.](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)
