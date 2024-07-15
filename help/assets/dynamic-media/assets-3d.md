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
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '2252'
ht-degree: 2%

---

# Trabalhar com ativos 3D no Dynamic Media {#working-with-three-d-assets-dm}

O Dynamic Media permite carregar, gerenciar, visualizar e fornecer ativos 3D como experiências imersivas.

* Publicação de ativos 3D com um clique (usando o **[!UICONTROL Quick Publish]** na barra de ferramentas) para gerar uma URL.
* Suporte otimizado para visualizar ativos 3D com a predefinição interativa e de alta qualidade do visualizador dimensional baseada no Adobe Dimension.
* O componente WCM de mídia 3D permite adicionar facilmente ativos 3D às páginas do [!DNL Adobe Experience Manager Sites].

Não é necessária nenhuma instalação adicional para usar ativos 3D no Dynamic Media.

![Sapato em 3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D compatíveis com o Dynamic Media {#supported-three-d-file-formats-in-dm}

O Dynamic Media é compatível com os seguintes formatos de arquivo 3D.

Consulte também [formatos 3D compatíveis com o Experience Manager Assets](/help/assets/file-format-support.md#support-3d-formats)

| Extensão de arquivo 3D | Formato do arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão GL Binária | model/gltf-binary | Inclui os materiais e texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D do WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Arquivo Zip de Descrição de Cena Universal | model/vnd.usdz+zip | *Suporte somente para assimilação; não há visualização ou interação disponíveis.* USDZ é um formato 3D proprietário que pode ser visualizado nativamente pelo Safari ou iOS. |

O componente WCM do Media 3D e a visualização 3D na página Detalhes de um ativo não são compatíveis com a versão mais recente do Chrome (97.x). Em vez disso, para trabalhar com ativos 3D, use o Firefox ou o Safari, ou use uma versão anterior do Chrome (96.x).

## Início rápido: ativos 3D no Dynamic Media {#quick-start-three-d}

A descrição do fluxo de trabalho passo a passo a seguir foi projetada para ajudar você a começar a usar rapidamente os ativos 3D no Dynamic Media.

Antes de trabalhar com ativos 3D no Dynamic Media, verifique se o administrador do [!DNL Experience Manager] já habilitou e configurou o Dynamic Media Cloud Service.

Consulte [Configurar o Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

1. **Carregar ativos 3D**

   * [Fazer upload de ativos 3D para uso no Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Formatos de arquivo 3D compatíveis com upload no Dynamic Media](#supported-three-d-file-formats-in-dm)

1. **Gerenciar ativos 3D**

   * Organizar e pesquisar ativos 3D

      * [Organizar ativos digitais](/help/assets/organize-assets.md)
      * [Pesquisar ativos 3D](/help/assets/search-assets.md)

   * Exibir ativos 3D

      * [Exibir e interagir com ativos 3D](#viewing-three-d-assets)
      * [Gerenciar a predefinição do visualizador Dimensional](/help/assets/dynamic-media/managing-viewer-presets.md)

   * Trabalhar com metadados de ativos 3D

      * [Gerenciar metadados para ativos digitais](/help/assets/manage-digital-assets.md#editing-properties)
      * [Esquemas de metadados](/help/assets/metadata-schemas.md)

1. **Publish 3D Assets**

   * [Ativos estáticos do Dynamic Media 3D para Publish](#publishing-three-d-assets)
   * [Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional](#alternate-publish-methods)

## Sobre visualização e interação com ativos 3D {#viewing-three-d-assets}

Esta seção descreve como visualizar e interagir com ativos 3D de duas maneiras diferentes: na página de detalhes do ativo e no componente de Mídia 3D do Sites.

O visualizador 3D interativo inclui, entre outras coisas, uma coleção de controles interativos de câmera que permitem que você orbite, amplie e desloque o ativo 3D.

O tempo necessário para abrir um ativo 3D na exibição de página Detalhes do ativo depende de vários fatores. Esses fatores incluem coisas como as seguintes:

* Largura de banda do servidor.
* Latências no servidor
* Complexidade da imagem.

Além disso, os recursos do computador cliente - como estação de trabalho, notebook ou dispositivo de toque móvel - também são importantes ao manipular a câmera interativamente. Um sistema razoavelmente eficiente com boas capacidades gráficas pode tornar a experiência de visualização 3D interativa mais suave e favorável.

>[!TIP]
>
>É possível abrir a predefinição do visualizador Dimensional no Editor de predefinições do visualizador para praticar a navegação em um ativo 3D sem precisar primeiro fazer upload de arquivos 3D. A predefinição do visualizador Dimensional tem um ativo 3D incorporado para você interagir.
>
>Consulte [Gerenciar predefinições do visualizador](/help/assets/dynamic-media/managing-viewer-presets.md).

## Exibir e interagir com um ativo 3D na página de detalhes do ativo {#viewing-three-d-assets-from-asset-details-page}

Consulte também [Visualizar ativos usando a interface de software](/help/assets/dynamic-media/previewing-assets.md).

**Para exibir e interagir com um ativo 3D a partir da página de detalhes do ativo:**

1. Verifique se você carregou ativos 3D no [!DNL Experience Manager].

   Consulte [Carregar seus ativos 3D para uso no Dynamic Media](/help/assets/add-assets.md#upload-assets).

1. Em [!DNL Experience Manager], na página **[!UICONTROL Navegação]**, selecione **[!UICONTROL Assets > Arquivos]**.
1. Próximo ao canto superior direito da página, na lista suspensa **[!UICONTROL Exibir]**, selecione **[!UICONTROL Exibição de Cartão]**.
1. Navegue até um ativo 3D que deseja visualizar.
1. Para abrir o ativo na página Detalhes, selecione o cartão do ativo 3D.
1. Na página Detalhes do ativo 3D, siga um destes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Girar sua câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo + arraste. | Pressione com um dedo + arraste. |
   | **Deslocar sua câmera** | Desloque sua exibição para a esquerda, direita, para cima ou para baixo. | Clique com o botão direito + arraste. | Pressione com dois dedos + arraste. |
   | **Aplicar zoom à sua câmera** | Mova para dentro e para fora das áreas na cena 3D. | Roda de rolagem. | Pinça de dois dedos. |
   | **Recentralize sua câmera** | Recentralize sua câmera em um ponto sobre um objeto na cena 3D. | Clique duas vezes em. | Selecione duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino de exibição para o centro do ativo 3D. A redefinição também move a câmera para mais perto ou mais longe, para mostrar o ativo em sua totalidade e em um tamanho de visualização razoável. |   |   |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone Tela cheia. |   |   |

1. No canto superior direito da página, selecione **[!UICONTROL Fechar]** para retornar à página do Assets.

## Visualizar e interagir com um ativo 3D dentro de um componente de Mídia 3D {#interacting-with-asset-inside-three-d-media-component}

Quando uma página da Web está no modo **[!UICONTROL Editar]**, nenhuma interação é possível com um ativo 3D. Para tornar o ativo interativo, você pode usar o recurso **[!UICONTROL Visualização]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de Mídia 3D.

>[!IMPORTANT]
>
>Essa tarefa só pode ser realizada após a adição de um componente de Mídia 3D a uma página da Web e a atribuição de um ativo 3D ao componente. Consulte [Adicionar o componente de mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page) e [Atribuir um ativo 3D a um componente de mídia 3D](#assigning-a-three-d-asset-to-the-component).

Consulte também [Visualizar ativos usando a interface de software](/help/assets/dynamic-media/previewing-assets.md).

**Para exibir e interagir com um ativo 3D dentro de um componente de Mídia 3D:**

1. Enquanto a página da Web estiver no modo **[!UICONTROL Editar]**, siga um destes procedimentos:

   * Próximo ao canto superior direito da página, clique em **[!UICONTROL Visualizar]** para entrar no modo **[!UICONTROL Visualizar]**.
   * Exclua `/editor.html` da URL da página no navegador.

   ![Ativo 3D sendo exibido dentro do componente de Mídia 3D](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
Um ativo 3D totalmente interativo conforme exibido no modo **[!UICONTROL Visualização]**.

1. No modo **[!UICONTROL Visualizar]**, siga um destes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Girar sua câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo + arraste. | Pressione com um dedo + arraste. |
   | **Deslocar sua câmera** | Desloque sua exibição para a esquerda, direita, para cima ou para baixo. | Clique com o botão direito + arraste. | Pressione com dois dedos + arraste. |
   | **Aplicar zoom à sua câmera** | Mova para dentro e para fora das áreas na cena 3D. | Roda de rolagem. | Pinça de dois dedos. |
   | **Recentralize sua câmera** | Recentralize sua câmera em um ponto sobre um objeto na cena 3D. | Clique duas vezes em. | Selecione duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino de exibição para o centro do ativo 3D. A redefinição também move a câmera para mais perto ou mais longe, para mostrar o ativo em sua totalidade e em um tamanho de visualização razoável. |   |   |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone Tela cheia. |   |   |

## Como trabalhar com o componente de Mídia 3D {#working-with-three-d-media-component}

O Dynamic Media inclui um componente de Mídia 3D do Dynamic Media que você pode usar no [!DNL Experience Manager Sites] para habilitar a exibição interativa de modelos 3D em suas páginas da Web.

* [Adicionar o componente de Mídia 3D ao modelo de página](#adding-three-d-media-component-to-page-template)
* [Adicionar o componente de Mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional - Configuração do componente de Mídia 3D](#configuring-the-three-d-component)
* [Atribuir um ativo 3D ao componente de Mídia 3D](#assigning-a-three-d-asset-to-the-component)

## Adicionar o componente de Mídia 3D ao modelo de página {#adding-three-d-media-component-to-page-template}

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]**.
1. Navegue até o modelo de página em que deseja ativar o componente 3D e selecione o modelo.
1. Para abrir o modelo, selecione **[!UICONTROL Editar]**.
1. Próximo ao canto superior direito da página, no menu suspenso, selecione o modo **[!UICONTROL Estrutura]**, se ele ainda não estiver ativo.

   ![3d-estrutura-componente-de-mídia](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. Para selecionar uma área vazia e abrir sua barra de ferramentas associada, selecione a área vazia na região **[!UICONTROL Contêiner de layout]**.
1. Na barra de ferramentas, selecione o ícone **[!UICONTROL Política]** para abrir o **[!UICONTROL Editor de Políticas]**.
1. Na seção **[!UICONTROL Propriedades]**, na guia **[!UICONTROL Componentes Permitidos]**, navegue até **[!UICONTROL Dynamic Media]**, expanda a lista e verifique a **[!UICONTROL Mídia 3D]**.
1. Selecione **[!UICONTROL Concluído]** para salvar as alterações e fechar o **[!UICONTROL Editor de Políticas]**.

   Agora é possível colocar o componente de Mídia 3D do Dynamic Media em todas as páginas que usam esse modelo.

## Adicionar o componente de Mídia 3D a uma página da Web {#adding-the-three-d-media-component-to-a-web-page}

Se você estiver usando o [!DNL Experience Manager] como sistema de gerenciamento de conteúdo da Web, poderá adicionar ativos 3D às suas páginas da Web por meio do componente de Mídia 3D.

Consulte também [Adicionar ativos do Dynamic Media a páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

1. Abra [!DNL Experience Manager Sites] e selecione a página da Web à qual deseja adicionar o componente de Mídia 3D do Dynamic Media.
1. Para abrir a página no editor de páginas, selecione o ícone **[!UICONTROL Editar]** (lápis). Verifique se o modo **[!UICONTROL Editar]** está selecionado próximo ao canto superior direito da página.

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. Na barra de ferramentas, selecione o ícone Painel lateral para alternar ou &quot;ativar&quot; a exibição do painel.

1. No painel lateral, selecione o ícone de sinal de mais para abrir a lista **[!UICONTROL Componentes]**.

   ![3d-componente-mídia-arrastar-soltar](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. Arraste o componente **[!UICONTROL Mídia 3D]** da lista **[!UICONTROL Componentes]** para o local da página em que você deseja que o visualizador 3D apareça.

Agora você está pronto para atribuir um ativo 3D ao componente.

Consulte [Atribuir um ativo 3D ao componente de Mídia 3D](#assigning-a-three-d-asset-to-the-component)

### Opcional - Configuração do componente de Mídia 3D {#configuring-the-three-d-component}

1. No editor de páginas do [!DNL Experience Manager Sites], selecione o componente **[!UICONTROL Visualizador de Mídia 3D]** que você adicionou anteriormente à página.
1. Para abrir a caixa de diálogo de configuração do componente, selecione o ícone **[!UICONTROL Configuração]** (chave inglesa).

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. Na caixa de diálogo Mídia 3D, na lista suspensa Predefinição do visualizador, selecione **[!UICONTROL Dimensional]** para atribuir a predefinição do visualizador Dimensional ao componente.

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. No canto superior direito, selecione a marca de seleção para salvar as alterações.

## Atribuir um ativo 3D ao componente de Mídia 3D {#assigning-a-three-d-asset-to-the-component}

Depois de adicionar um componente de Mídia 3D a uma página da Web, é possível atribuir um ativo 3D a ele.

Consulte [Adicionar o componente de Mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page).

1. No editor de páginas do [!DNL Experience Manager Sites], clique no ícone do **[!UICONTROL Assets]** para abrir o **[!UICONTROL Assets]** no painel lateral.
1. Na lista suspensa, selecione **[!UICONTROL 3D]** para mostrar somente tipos de arquivos de ativos 3D.
1. No painel lateral, procure ou role até o ativo 3D que deseja visualizar na página que está sendo editada.
1. Arraste o ativo 3D do painel lateral do Assets e solte-o no componente **[!UICONTROL Mídia 3D]** adicionado anteriormente à página.

   ![Atribuir ativo 3d ao componente de Mídia 3d](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>Enquanto a página da Web estiver no modo [!DNL Experience Manager Sites] **[!UICONTROL Editar]**, o componente de Mídia 3D exibirá o ativo 3D, mas nenhuma interação com o ativo será possível. Para tornar o ativo interativo, você pode usar o recurso **[!UICONTROL Visualização]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de Mídia 3D.

## Ativos estáticos do Dynamic Media 3D para Publish {#publishing-three-d-assets}

O Dynamic Media aceita vários formatos de arquivo 3D com suporte como *conteúdo estático* no Dynamic Media. O conteúdo estático significa que você pode fazer upload e publicar ativos 3D, mas não há suporte para imagens ou revisões de imagem *dinâmicas* associadas ao ativo 3D. O motivo é que o Dynamic Media Imaging Server não reconhece os formatos 3D. Assim, depois de publicar um ativo 3D no Dynamic Media, você tem um URL instantâneo que pode ser copiado. O URL do ativo 3D segue a estrutura normal do URL do Dynamic Media. No entanto, não é possível editar parâmetros no URL do ativo, ao contrário dos ativos de imagem tradicionais no Dynamic Media.

Consulte também [Obter uma URL para um ativo estático](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

Na **[!UICONTROL Exibição de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda de sua data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

Se você estiver usando o [!DNL Experience Manager] como o WCM, use esse método de publicação para adicionar os ativos 3D do Dynamic Media diretamente na sua página da Web.

Consulte também [Publish Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

Consulte também [páginas do Publish](/help/sites-cloud/authoring/sites-console/publishing-pages.md).

**Para publicar ativos 3D estáticos do Dynamic Media:**

1. Abra um ativo 3D (formato de arquivo GLB, OBJ ou STL).
1. Na página Detalhes, na barra de ferramentas, selecione **[!UICONTROL Publish Rápido]**.

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. Selecione **[!UICONTROL Fechar]** para sair da caixa de diálogo e retornar à página de detalhes do ativo.
1. Na lista suspensa à esquerda do nome do arquivo do ativo 3D, selecione **[!UICONTROL Representações]**.

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. Selecione **[!UICONTROL original]**. Quando um ativo 3D é publicado (ou &quot;ativado&quot;), o botão **[!UICONTROL URL]** é exibido próximo ao canto inferior esquerdo da página se todas as condições de ativos 3D a seguir forem atendidas:
   * O ativo 3D é um formato compatível (GLB, OBJ, STL e USDZ).
   * O ativo 3D foi assimilado no Sistema de produção de imagem (IPS) da Dynamic Media.
   * O ativo 3D é publicado.

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. Para exibir a URL de produção direta do ativo 3D, que você pode copiar e usar em páginas da Web, selecione **[!UICONTROL URL]**.

### Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional {#alternate-publish-methods}

Use os dois métodos a seguir para publicar ativos 3D do Dynamic Media se você *não* estiver usando [!DNL Experience Manager] como o WCM.

* **[!UICONTROL URL]** - Use **[!UICONTROL URL]** se estiver usando um sistema de gerenciamento de conteúdo da Web de terceiros e quiser vincular ativos do Dynamic Media 3D às suas páginas da Web usando o visualizador Dimensional.

  Consulte [Vincular URLs ao aplicativo Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incorporar]** - Use **[!UICONTROL Incorporar]** quando quiser exibir um ativo 3D do Dynamic Media inserido em uma página da Web usando o visualizador Dimensional. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na caixa de diálogo **[!UICONTROL Incorporar]**.

  Consulte [Incorporar o Vídeo do Dynamic Media, o Visualizador de imagens ou o Visualizador dimensional em uma página da Web](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
