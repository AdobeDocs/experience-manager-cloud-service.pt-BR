---
title: Trabalhar com ativos 3D no Dynamic Media
description: Saiba como trabalhar com ativos 3D no Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: b31fa5af7bcaa944d8bd7b0bb7d7b8deb36906a8
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 5%

---

# Trabalhar com ativos 3D no Dynamic Media {#working-with-three-d-assets-dm}

O Dynamic Media permite carregar, gerenciar, visualizar e fornecer ativos 3D como experiências imersivas.

* Publicação com um clique (usando **[!UICONTROL Publicação rápida]** na barra de ferramentas) de ativos 3D para gerar um URL.
* Suporte otimizado para visualizar ativos 3D com a predefinição interativa de visualizador Dimensional de alta qualidade fornecida pela Adobe Dimension.
* O componente WCM de mídia 3D permite adicionar facilmente os ativos 3D ao [!DNL Adobe Experience Manager Sites] páginas.

Não é necessária nenhuma instalação adicional para usar ativos 3D no Dynamic Media.

![Sapato em 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D compatíveis com o Dynamic Media {#supported-three-d-file-formats-in-dm}

O Dynamic Media é compatível com os seguintes formatos de arquivo 3D.

Consulte também [Formatos 3D compatíveis com o Experience Manager Assets](/help/assets/file-format-support.md#support-3d-formats)

| extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão binária GL | modelo/gltf-binário | Inclui os materiais e as texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Arquivo Zip de descrição da cena universal | model/vnd.usdz+zip | *Suporte apenas para ingestão; nenhuma visualização ou interação está disponível.* USDZ é um formato 3D proprietário que pode ser visualizado originalmente pelo Safari ou pelo iOS. |

## Início rápido: Ativos 3D no Dynamic Media {#quick-start-three-d}

A seguinte descrição passo a passo do fluxo de trabalho foi criada para ajudar você a ativar e executar rapidamente com ativos 3D no Dynamic Media.

Antes de trabalhar com ativos 3D na Dynamic Media, verifique se [!DNL Experience Manager] O administrador já ativou e configurou o Dynamic Media Cloud Services.

Consulte [Configurar Dynamic Media Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **Fazer upload de ativos 3D**

   * [Faça upload de seus ativos 3D para usar no Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Formatos de arquivo 3D compatíveis para upload no Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Gerenciar ativos 3D**

   * Organizar e pesquisar ativos 3D

      * [Organizar ativos digitais](/help/assets/organize-assets.md)
      * [Pesquisar ativos 3D](/help/assets/search-assets.md)
   * Exibir ativos 3D

      * [Exibir e interagir com ativos 3D](#viewing-three-d-assets)
      * [Gerenciar a predefinição do visualizador dimensional](/help/assets/dynamic-media/managing-viewer-presets.md)
   * Trabalhar com metadados de ativos 3D

      * [Gerenciar metadados para ativos digitais](/help/assets/manage-digital-assets.md#editing-properties)
      * [Esquemas de metadados](/help/assets/metadata-schemas.md)



1. **Publicar ativos 3D**

   * [Publicar ativos estáticos em Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional](#alternate-publish-methods)

## Sobre a visualização e interação com ativos 3D {#viewing-three-d-assets}

Esta seção descreve como visualizar e interagir com ativos 3D de duas maneiras diferentes: na página de detalhes do ativo e a partir do componente Mídia 3D no Sites.

O visualizador 3D interativo inclui, entre outras coisas, uma coleção de controles interativos de câmera que permitem que você orbite, amplie e desloque o ativo 3D.

O tempo que leva para abrir um ativo 3D na exibição de página Detalhes do ativo depende de vários fatores. Esses fatores incluem informações como as seguintes:

* Largura de banda para o servidor.
* Latências para o servidor
* Complexidade da imagem.

Além disso, os recursos do computador cliente, como uma estação de trabalho, um notebook ou um dispositivo de toque móvel, também são importantes a serem considerados ao manipular a câmera interativamente. Um sistema bastante eficiente com bons recursos gráficos pode tornar a experiência de visualização interativa em 3D mais fácil e favorável.

>[!TIP]
>
>Você pode abrir a predefinição do visualizador Dimensional no Editor de predefinições do visualizador para praticar a navegação de um ativo 3D sem a necessidade de fazer upload primeiro de qualquer arquivo 3D. A predefinição do visualizador Dimensional tem um ativo 3D integrado com o qual você pode interagir.
>
>Consulte [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

## Exibir e interagir com um ativo 3D na página de detalhes do ativo {#viewing-three-d-assets-from-asset-details-page}

Consulte também [Visualizar ativos usando a interface do software](/help/assets/dynamic-media/previewing-assets.md).

**Para visualizar e interagir com um ativo 3D na página de detalhes do ativo:**

1. Verifique se você fez upload dos ativos 3D no [!DNL Experience Manager].

   Consulte [Faça upload de seus ativos 3D para usar no Dynamic Media](/help/assets/add-assets.md#upload-assets).

1. De [!DNL Experience Manager], no **[!UICONTROL Navegação]** página, selecione **[!UICONTROL Ativos > Arquivos]**.
1. Próximo ao canto superior direito da página, da **[!UICONTROL Exibir]** , selecione **[!UICONTROL Exibição de cartão]**.
1. Navegue até o ativo 3D que deseja visualizar.
1. Para abrir o ativo na página Detalhes, selecione o cartão do ativo 3D.
1. Na página Detalhes do ativo 3D, siga um destes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Rode a câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo e arraste. | Pressione com um único dedo e arraste. |
   | **Deslocar a câmera** | Deslocar a vista para a esquerda, para a direita, para cima ou para baixo. | Clique com o botão direito + arraste. | Pressione com dois dedos e arraste. |
   | **Zoom da câmera** | Mova para dentro e para fora de áreas na cena 3D. | Roda de rolagem. | Um beliscão de dois dedos. |
   | **Recenter a câmera** | Insira novamente sua câmera em um ponto em um objeto na cena 3D. | Duplo clique. | Toque duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino da exibição para o centro do ativo 3D. A redefinição também aproxima ou afasta a câmera para mostrar o ativo inteiro e com um tamanho de visualização razoável. |  |  |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone de tela cheia. |  |  |

1. No canto superior direito da página, selecione **[!UICONTROL Fechar]** para retornar à página Ativos .

## Exibir e interagir com um ativo 3D em um componente de mídia 3D {#interacting-with-asset-inside-three-d-media-component}

Quando uma página da Web está em **[!UICONTROL Editar]** , nenhuma interação é possível com um ativo 3D. Para tornar o ativo interativo, você pode usar o **[!UICONTROL Visualizar]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de mídia 3D.

>[!IMPORTANT]
>
>Essa tarefa só pode ser realizada depois de ter adicionado um componente de mídia 3D a uma página da Web e atribuído um ativo 3D ao componente. Consulte [Adicionar o componente de mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page) e [Atribuir um ativo 3D a um componente de mídia 3D](#assigning-a-three-d-asset-to-the-component).

Consulte também [Visualizar ativos usando a interface do software](/help/assets/dynamic-media/previewing-assets.md).

**Para visualizar e interagir com um ativo 3D dentro de um componente de mídia 3D:**

1. Enquanto uma página da Web está em **[!UICONTROL Editar]** , execute um dos seguintes procedimentos:

   * Próximo ao canto superior direito da página, clique em **[!UICONTROL Visualizar]** para inserir **[!UICONTROL Visualizar]** modo.
   * Excluir `/editor.html` no URL da página no navegador.

Um ativo 3D totalmente interativo, como exibido em    ![Ativo 3D exibido dentro do componente Mídia 3D](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
Um ativo 3D totalmente interativo, como exibido em **[!UICONTROL Visualizar]** modo.

1. Enquanto em **[!UICONTROL Visualizar]** , execute um dos seguintes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Rode a câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo e arraste. | Pressione com um único dedo e arraste. |
   | **Deslocar a câmera** | Deslocar a vista para a esquerda, para a direita, para cima ou para baixo. | Clique com o botão direito + arraste. | Pressione com dois dedos e arraste. |
   | **Zoom da câmera** | Mova para dentro e para fora de áreas na cena 3D. | Roda de rolagem. | Um beliscão de dois dedos. |
   | **Recenter a câmera** | Insira novamente sua câmera em um ponto em um objeto na cena 3D. | Duplo clique. | Toque duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino da exibição para o centro do ativo 3D. A redefinição também aproxima ou afasta a câmera para mostrar o ativo inteiro e com um tamanho de visualização razoável. |  |  |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone de tela cheia. |  |  |

## Sobre como trabalhar com o componente de mídia 3D {#working-with-three-d-media-component}

O Dynamic Media inclui um componente de mídia 3D do Dynamic Media que você pode usar em [!DNL Experience Manager Sites] para permitir a visualização interativa de modelos 3D em suas páginas da Web.

* [Adicionar o componente de mídia 3D ao modelo da página](#adding-three-d-media-component-to-page-template)
* [Adicionar o componente de mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional - Configuração do componente de mídia 3D](#configuring-the-three-d-component)
* [Atribuir um ativo 3D ao componente de mídia 3D](#assigning-a-three-d-asset-to-the-component)

## Adicionar o componente de mídia 3D ao modelo da página {#adding-three-d-media-component-to-page-template}

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]**.
1. Navegue até o modelo de página no qual você deseja ativar o componente 3D e selecione o modelo.
1. Para abrir o modelo, selecione **[!UICONTROL Editar]**.
1. Próximo ao canto superior direito da página, no menu suspenso, selecione **[!UICONTROL Estrutura]** , se ainda não estiver ativo.

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Para selecionar uma área vazia e abrir sua barra de ferramentas associada, selecione a área vazia no **[!UICONTROL Contêiner de layout]** região.
1. Na barra de ferramentas, selecione o **[!UICONTROL Política]** ícone para abrir o **[!UICONTROL Editor de políticas]**.
1. No **[!UICONTROL Propriedades]** na seção **[!UICONTROL Componentes permitidos]** guia , role até **[!UICONTROL Dynamic Media]**, em seguida, expanda a lista e marque **[!UICONTROL Mídia 3D]**.
1. Toque **[!UICONTROL Concluído]** para salvar as alterações e fechar o **[!UICONTROL Editor de políticas]**.

   Agora é possível colocar o componente de mídia 3D do Dynamic Media em todas as páginas que usam esse modelo.

## Adicionar o componente de mídia 3D a uma página da Web {#adding-the-three-d-media-component-to-a-web-page}

Se estiver usando [!DNL Experience Manager] como sistema de gerenciamento de conteúdo da Web, você pode adicionar ativos 3D às páginas da Web por meio do componente Mídia 3D.

Consulte também [Adicionar ativos do Dynamic Media às páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Abrir [!DNL Experience Manager Sites] e selecione a página da Web à qual deseja adicionar o componente de mídia 3D do Dynamic Media.
1. Para abrir a página no editor de páginas, selecione o **[!UICONTROL Editar]** ícone (lápis). Certifique-se de que **[!UICONTROL Editar]** O modo é selecionado próximo ao canto superior direito da página.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. Na barra de ferramentas, selecione o ícone do painel lateral para alternar ou &quot;ativar&quot; a exibição do painel.

1. No painel lateral, selecione o ícone de sinal de mais para abrir o **[!UICONTROL Componentes]** lista.

   ![3d-mídia-componente-arrastar-soltar](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Arraste o **[!UICONTROL Mídia 3D]** do **[!UICONTROL Componentes]** liste para o local na página onde você deseja que o visualizador 3D apareça.

Agora você está pronto para atribuir um ativo 3D ao componente.

Consulte [Atribuir um ativo 3D ao componente de mídia 3D](#assigning-a-three-d-asset-to-the-component)

### Opcional - Configuração do componente de mídia 3D {#configuring-the-three-d-component}

1. No [!DNL Experience Manager Sites] no editor de páginas, selecione o **[!UICONTROL Visualizador de mídia 3D]** componente adicionado anteriormente à página.
1. Para abrir a caixa de diálogo configuração do componente, selecione a **[!UICONTROL Configuração]** ícone (chave inglesa).

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. Na caixa de diálogo Mídia 3D, na lista suspensa Predefinição do visualizador , selecione **[!UICONTROL Dimensões]** para atribuir a predefinição do visualizador Dimensional ao componente.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. No canto superior direito, selecione a marca de seleção para salvar suas alterações.

## Atribuir um ativo 3D ao componente de mídia 3D {#assigning-a-three-d-asset-to-the-component}

Após adicionar um componente de Mídia 3D a uma página da Web, é possível atribuir um ativo 3D a ela.

Consulte [Adicionar o componente de mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page).

1. No [!DNL Experience Manager Sites] no editor de páginas, clique no botão **[!UICONTROL Ativos]** ícone para abrir **[!UICONTROL Ativos]** no painel lateral.
1. Na lista suspensa, selecione **[!UICONTROL 3D]** para mostrar apenas tipos de arquivos de ativos 3D.
1. No painel lateral, procure ou role até o ativo 3D que deseja visualizar na página que está sendo editada.
1. Arraste o ativo 3D do painel lateral Ativos e solte-o no **[!UICONTROL Mídia 3D]** componente adicionado anteriormente à página.

   ![Atribuir ativo 3d ao componente de mídia 3d](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Enquanto uma página da Web está no [!DNL Experience Manager Sites] **[!UICONTROL Editar]** modo , o componente Mídia 3D exibe o ativo 3D, mas nenhuma interação com o ativo é possível. Para tornar o ativo interativo, você pode usar o **[!UICONTROL Visualizar]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de mídia 3D.

## Publicar ativos estáticos em Dynamic Media 3D {#publishing-three-d-assets}

O Dynamic Media aceita vários formatos de arquivo 3D compatíveis com *conteúdo estático* no Dynamic Media. O conteúdo estático significa que você pode fazer upload e publicar ativos 3D, mas não há suporte para *dinâmico* imagem ou redefinição de imagem associada ao ativo 3D. Isso ocorre porque o Dynamic Media Imaging Server não reconhece formatos 3D. Dessa forma, depois de publicar um ativo 3D no Dynamic Media, você tem um URL instantâneo que pode ser copiado. O URL para o ativo 3D segue a estrutura normal de URL do Dynamic Media. No entanto, não é possível editar nenhum parâmetro no URL do ativo, ao contrário dos ativos de imagem tradicionais na Dynamic Media.

Consulte também [Obter um URL para um ativo estático](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

No **[!UICONTROL Exibição de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda de sua data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

Se estiver usando [!DNL Experience Manager] como seu WCM, use este método de publicação para adicionar os ativos 3D do Dynamic Media diretamente em sua página da Web.

Consulte também [Publicar ativos do Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

Consulte também [Publicar páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

**Para publicar ativos 3D estáticos do Dynamic Media:**

1. Abra um ativo 3D (formato de arquivo GLB, OBJ ou STL).
1. Na página Detalhes , na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Toque **[!UICONTROL Fechar]** para sair da caixa de diálogo e retornar à página de detalhes do ativo.
1. Na lista suspensa à esquerda do nome de arquivo do ativo 3D, selecione **[!UICONTROL Representações]**.

   ![3d-representação de ativos](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Toque **[!UICONTROL original]**. Quando um ativo 3D é publicado (ou &quot;ativado&quot;), a variável **[!UICONTROL URL]** será exibido próximo ao canto inferior esquerdo da página se todas as seguintes condições de ativos 3D forem atendidas:
   * O ativo 3D é um formato compatível (GLB, OBJ, STL e USDZ).
   * O ativo 3D foi assimilado no Sistema de produção de imagem da Dynamic Media (IPS).
   * O ativo 3D é publicado.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Para exibir o URL de produção direta do ativo 3D que você pode copiar e usar nas páginas da Web, selecione **[!UICONTROL URL]**.

### Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional {#alternate-publish-methods}

Use os dois métodos a seguir para publicar ativos 3D do Dynamic Media se você *not* usar [!DNL Experience Manager] como seu WCM.

* **[!UICONTROL URL]** - Uso **[!UICONTROL URL]** se você estiver usando um sistema de gerenciamento de conteúdo da Web de terceiros e quiser vincular ativos 3D do Dynamic Media às suas páginas da Web usando o visualizador Dimensional.

   Consulte [Vincular URLs ao aplicativo da Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incorporar]** - Uso **[!UICONTROL Incorporar]** quando quiser exibir um ativo 3D do Dynamic Media incorporado em uma página da Web usando o visualizador Dimensional. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na variável **[!UICONTROL Incorporar]** caixa de diálogo.

   Consulte [Incorporar o vídeo do Dynamic Media, o visualizador de imagens ou o visualizador dimensional em uma página da Web](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
