---
title: Conjuntos de imagem
description: Saiba como trabalhar com conjuntos de imagens no Dynamic Media.
feature: Image Sets
role: User
exl-id: 2eb71f24-73d9-4b5c-8605-923a0e3d1505
source-git-commit: a2bbc64051214efa83d74d414e2e5f1407433127
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 5%

---

# Conjuntos de imagem {#image-sets}

Os Conjuntos de imagens fornecem aos usuários uma experiência de visualização integrada, onde os usuários podem ver diferentes visualizações de um item clicando em uma imagem em miniatura. Os Conjuntos de imagens permitem que você apresente visualizações alternativas de um item e o visualizador oferece ferramentas de zoom para examinar imagens cuidadosamente.

Os conjuntos de imagens são designados por um banner com a palavra `IMAGESET`. Além disso, se o Conjunto de imagens for publicado, então a data de publicação, indicada pela variável **[!UICONTROL World]** está no banner. Além disso, a última data de modificação, indicada pela variável **[!UICONTROL Lápis]** é exibido.

![chlimage_1-133](assets/chlimage_1-339.png)

No conjunto de imagens, também é possível criar amostras criando um Conjunto de imagens e adicionando miniaturas.

Esse aplicativo é útil para quando você deseja mostrar um item em uma cor, padrão ou conclusão diferente. Para criar um Conjunto de imagens com amostras de cores, você precisa de uma imagem para cada cor, padrão ou acabamento diferente que deseja apresentar aos usuários. Você também precisa de uma cor, padrão ou amostra de finalização para cada cor, padrão ou finalização.

Por exemplo, suponha que você deseja apresentar imagens de maiúsculas com diferentes notas coloridas; as notas são vermelhas, verdes e azuis. Neste caso, você precisa de três tiros do mesmo boné. Você precisa de um tiro com um vermelho, um com um verde e um com uma nota azul. Você também precisa de uma amostra de cor vermelha, verde e azul. As amostras de cores servem como miniaturas que os usuários clicam no Visualizador de Conjunto de Amostras para ver a tampa vermelha, verde ou azul.

>[!NOTE]
>
>Para obter informações sobre a interface do usuário do Assets, consulte [Gerenciar ativos com a interface de toque](/help/assets/manage-digital-assets.md).

Ao criar um Conjunto de imagens, o Adobe recomenda as seguintes práticas recomendadas e aplica os seguintes limites:

| Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| Número de ativos duplicados por conjunto | Sem duplicatas | 20 |
| Número máximo de imagens por conjunto | 5 a 10 imagens por conjunto | 1000 |

Consulte também [Limitações do Dynamic Media](/help/assets/dynamic-media/limitations.md).

## Início rápido: Conjuntos de imagens {#quick-start-image-sets}

Para ativar e executar rapidamente:

1. Opcional. [Criar uma predefinição de conjunto de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md) e aplicá-lo a uma nova pasta onde as imagens do conjunto de rotação são carregadas.

   Uma predefinição de conjunto de lotes pode ajudar você a automatizar a criação do conjunto de imagens.

   >[!IMPORTANT]
   >
   >Os conjuntos em lotes são criados pelo IPS (Sistema de produção de imagem) como parte da ingestão de ativos.

1. [Fazer upload de imagens de origem primária para várias exibições](#uploading-assets-in-image-sets).

   Carregue as imagens para seus Conjuntos de imagens. Lembre-se de que os usuários podem ampliar imagens no Visualizador de conjunto de imagens. Assim, escolha suas imagens com cuidado. Certifique-se de que as imagens tenham pelo menos 2000 pixels no tamanho maior.

   Consulte [Dynamic Media - Formatos de imagem rasterizada compatíveis](/help/assets/file-format-support.md#image-support-dynamic-media) para obter uma lista de formatos suportados pelos Conjuntos de imagens.

1. [Criar conjuntos de imagens](#creating-image-sets).

   Em Conjuntos de imagens, os usuários clicam em imagens em miniatura no Visualizador do Conjunto de imagens.

   Para criar um Conjunto de imagens no Assets, selecione **[!UICONTROL Criar]** > **[!UICONTROL Conjuntos de imagens]**. Em seguida, adicione imagens e clique em **[!UICONTROL Salvar]**.

   Consulte [Preparar ativos do Conjunto de imagens para carregar e carregar seus arquivos](#uploading-assets-in-image-sets).

   Consulte [Trabalhar com seletores](/help/assets/dynamic-media/working-with-selectors.md).

1. Adicionar [Predefinições do visualizador de conjunto de imagens](/help/assets/dynamic-media/managing-viewer-presets.md), conforme necessário.

   Os administradores podem criar ou modificar as Predefinições do visualizador de conjunto de imagens. Para ver seu conjunto de imagens com uma predefinição do visualizador, selecione o conjunto de imagens e, na lista suspensa do painel à esquerda, selecione **[!UICONTROL Visualizadores]**.

   Para criar ou editar predefinições do visualizador, consulte **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Predefinições do visualizador]**.

1. (Opcional) [Exibir conjuntos de imagens](/help/assets/dynamic-media/image-sets.md#viewing-image-sets) que foram criadas usando predefinições de conjunto de lotes.
1. [Visualizar conjuntos de imagens](/help/assets/dynamic-media/previewing-assets.md).

   Selecione o Conjunto de imagens e você pode visualizá-lo. Para examinar seu Conjunto de imagens no Visualizador selecionado, selecione os ícones de miniatura. Você pode escolher visualizadores diferentes do **[!UICONTROL Visualizadores]** , disponível na lista suspensa do painel à esquerda.

1. [Publicar conjuntos de imagens](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

   A publicação de um conjunto de imagens ativa o URL e a cadeia de caracteres de inserção. Além disso, você deve [publicar qualquer predefinição do visualizador personalizado](/help/assets/dynamic-media/managing-viewer-presets.md) que você criou. As predefinições do visualizador prontas para uso já estão publicadas.

1. [Vincular URLs ao seu aplicativo web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) ou [Incorporar o visualizador de vídeo ou imagem](/help/assets/dynamic-media/embed-code.md).

   O Experience Manager Assets cria chamadas de URL para Conjuntos de imagens e as ativa após publicar os conjuntos de imagens. Você pode copiar esses URLs ao visualizar ativos. Como alternativa, você pode incorporá-los ao seu site.

   Selecione o Conjunto de imagens e, na lista suspensa do painel à esquerda, selecione **[!UICONTROL Visualizadores]**.

   Consulte [Vincular um conjunto de imagens a uma página da Web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) e [Incorporar o visualizador de vídeo ou imagem](/help/assets/dynamic-media/embed-code.md).

Para editar conjuntos de imagens, consulte [editar conjuntos de imagens](#editing-image-sets). Além disso, é possível visualizar e editar [Propriedades do conjunto de imagens](/help/assets/manage-digital-assets.md#editing-properties).

Se tiver problemas ao criar conjuntos, consulte Imagens e conjuntos em [Solução de problemas do Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#images-and-sets).

## Fazer upload de ativos para conjuntos de imagens {#uploading-assets-in-image-sets}

Comece carregando os ativos de imagem dos seus Conjuntos de imagens. Lembre-se de que os usuários podem ampliar imagens no Visualizador de conjunto de imagens. Assim, escolha suas imagens com cuidado. Certifique-se de que as imagens tenham pelo menos 2000 pixels no maior tamanho para obter detalhes ideais de zoom. O Dynamic Media pode renderizar imagens de até 25 megapixels cada. Por exemplo, você pode usar uma imagem de 5000x5000 megapixels ou qualquer outra combinação de tamanho de até 25 megapixels.

<!-- Image Sets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

Consulte [Dynamic Media - Formatos de imagem rasterizada compatíveis](/help/assets/file-format-support.md#image-support-dynamic-media) para obter uma lista de formatos suportados pelos Conjuntos de imagens.

Você pode fazer upload de imagens para conjuntos de imagens da mesma maneira que faria [fazer upload de qualquer outro ativo no Assets](/help/assets/manage-digital-assets.md#uploading-assets).

### Preparar ativos do Conjunto de imagens para upload {#preparing-image-set-assets-for-upload}

Antes de criar Conjuntos de imagens, verifique se as imagens têm o tamanho e o formato corretos.

Para criar um Conjunto de imagens com várias exibições, você precisa de imagens que mostrem um item de diferentes pontos de vista ou que mostrem diferentes aspectos do mesmo item. O objetivo é destacar os recursos importantes de um item para que os visualizadores tenham uma imagem completa de como ele aparece ou o que ele faz.

Como os usuários podem ampliar imagens em Conjuntos de imagens, verifique se as imagens têm pelo menos 2000 pixels no tamanho maior. O Experience Manager Assets oferece suporte a vários formatos de arquivo de imagem, mas as imagens TIFF, PNG e EPS sem perdas são recomendadas.

>[!NOTE]
>
>Se você usar miniaturas para indicar amostras de produtos, faça o seguinte:
>
>Crie vinhetas ou fotos diferentes da mesma imagem, mostrando-a em cores, padrões ou finalizações diferentes. Você também precisa de arquivos de miniatura que correspondam às diferentes cores, padrões ou finalizações. Por exemplo, para apresentar miniaturas com um Conjunto de imagens mostrando a mesma jaqueta em preto, marrom e verde, é necessário:
>
>* Um tiro preto, marrom e verde da mesma jaqueta.
>* Miniatura de cor preta, marrom e verde.


## Criar conjuntos de imagens {#creating-image-sets}

Você pode criar Conjuntos de imagens por meio da interface do usuário ou da API.

>[!NOTE]
>
>Você também pode criar conjuntos de imagens automaticamente por meio de [predefinições do conjunto de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).
>**Importante:** os conjuntos em lotes são criados pelo IPS (Sistema de produção de imagem) como parte da ingestão de ativos.

Ao adicionar ativos ao seu conjunto, eles são automaticamente adicionados em ordem alfanumérica. Você pode reorganizar ou classificar ativos manualmente após sua adição.

>[!NOTE]
>
>Os conjuntos de imagens não são compatíveis com ativos com &quot;&quot; (vírgula) no nome do arquivo.

Ao criar um Conjunto de imagens, o Adobe recomenda as seguintes práticas recomendadas e aplica os seguintes limites:

| Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| Número de ativos duplicados por conjunto | Sem duplicatas | 20º |
| Número máximo de imagens por conjunto | 5 a 10 imagens por conjunto | 1000 |

Consulte também [Limitações do Dynamic Media](/help/assets/dynamic-media/limitations.md).

**Para criar Conjuntos de Imagens:**

1. No Adobe Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global.
1. Toque **[!UICONTROL Navegação]** > **[!UICONTROL Ativos]**. Navegue até o local em que deseja criar um conjunto de imagens, em seguida, vá para **[!UICONTROL Criar]** > **[!UICONTROL Conjunto de imagens]** para abrir a página Editor do conjunto de imagens.

   Além disso, crie o conjunto de dentro de uma pasta que contenha seus ativos.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. Na página Editor do conjunto de imagens, no **[!UICONTROL Título]** , insira um nome para o conjunto de imagens. O nome aparece no banner através do Conjunto de imagens. Opcionalmente, informe uma descrição.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Siga um destes procedimentos:

   * Próximo ao canto superior esquerdo da página Editor do conjunto de imagens, selecione **[!UICONTROL Adicionar ativo]**.

   * Próximo ao meio da página Editor do conjunto de imagens, selecione **[!UICONTROL Toque para abrir o Seletor de ativos]**.
   Toque para selecionar os ativos que deseja incluir no Conjunto de imagens. Os ativos selecionados têm um ícone de marca de seleção sobre eles. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Selecionar]**.

   Com o Seletor de ativos, procure por ativos ao digitar uma palavra-chave e selecionar **[!UICONTROL Retorno]**. Aplique filtros para refinar os resultados da pesquisa. Filtre por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e depois selecione o **[!UICONTROL Filtro]** na barra de ferramentas. Altere a exibição ao selecionar o ícone Exibir e selecionar **[!UICONTROL Exibição de coluna]**, **[!UICONTROL Exibição de cartão]** ou **[!UICONTROL Exibição de lista]**.

   Consulte [Trabalhar com seletores](/help/assets/dynamic-media/working-with-selectors.md).

   ![6_5_imagens_adicionar ativos](assets/6_5_imageset-addingassets.png)

1. Ao adicionar ativos ao seu conjunto, eles são automaticamente adicionados em ordem alfanumérica. Você pode reordenar ou classificar ativos manualmente depois de adicioná-los.

   Se necessário, arraste o ícone Reordenar de um ativo à direita do nome de arquivo do ativo para reorganizar as imagens para cima ou para baixo na lista definida.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Se quiser alterar uma miniatura ou amostra, clique no ícone de **miniatura** **+** ao lado da imagem e navegue até a miniatura ou a amostra desejada. Quando terminar de selecionar todas as imagens, clique em **[!UICONTROL Salvar]**.

1. (Opcional) Siga um destes procedimentos:

   * Para excluir uma imagem, selecione-a e selecione **[!UICONTROL Excluir ativo]**.

   * Para aplicar uma predefinição, próximo ao canto superior direito da página, selecione **[!UICONTROL Predefinição]** e, em seguida, selecione uma predefinição para aplicar a todos os ativos ao mesmo tempo.
   >[!NOTE]
   >
   >Ao criar o conjunto de imagens, você pode alterar a miniatura do conjunto de imagens. Ou você pode permitir que o Experience Manager selecione a miniatura automaticamente com base nos ativos no conjunto de imagens. Para selecionar uma miniatura, selecione **[!UICONTROL Alterar miniatura]** acima do campo Título na página Editor do conjunto de imagens. Em seguida, selecione qualquer imagem (você também pode navegar para outras pastas para localizar imagens). Se tiver selecionado uma miniatura e decidir que deseja que o Experience Manager gere uma a partir do conjunto de imagens, selecione **[!UICONTROL Mudar para]** **[!UICONTROL Miniatura automática]**.

1. Clique em **[!UICONTROL Salvar]**. O Conjunto de imagens recém-criado é exibido na pasta em que você o criou.

## Exibir conjuntos de imagens {#viewing-image-sets}

Você pode criar conjuntos de imagens na interface do usuário ou automaticamente usando [predefinições do conjunto de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).

>[!IMPORTANT]
>
>Os conjuntos em lotes são criados pelo IPS [Sistema de produção de imagens] como parte da ingestão de ativos.

No entanto, os conjuntos criados usando predefinições de conjunto de lotes, *not* forem exibidos na interface do usuário do . Você pode visualizar esses conjuntos de três maneiras diferentes. (Esses métodos estão disponíveis mesmo se você tiver criado os conjuntos de imagens na interface do usuário).

* Abra as propriedades de um ativo. As propriedades indicam quais conjuntos o ativo selecionado é referenciado ou um membro de. Para ver o conjunto inteiro, selecione o nome do conjunto.

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* A partir de uma imagem de membro de qualquer conjunto. Selecione o **[!UICONTROL Conjuntos]** para exibir os conjuntos dos quais o ativo é membro.

   ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* Na pesquisa, você pode selecionar **[!UICONTROL Filtro]**, em seguida expanda **[!UICONTROL Dynamic Media]** e selecione **[!UICONTROL Conjuntos]**.

   A pesquisa retorna conjuntos correspondentes que foram criados manualmente na interface do usuário ou criados automaticamente por meio de predefinições de conjuntos em lotes. Para conjuntos automatizados, a consulta de pesquisa é realizada usando &quot;Inicia com&quot;. Esse critério de pesquisa é diferente do Experience Manager, que é baseado no uso de &quot;Contém&quot;. Definição do filtro como **[!UICONTROL Conjuntos]** é a única maneira de pesquisar conjuntos automatizados.

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Você pode exibir os conjuntos por meio da interface do usuário, conforme descrito em [Editar conjuntos de imagens](#editing-image-sets).

## Editar conjuntos de imagens {#editing-image-sets}

Você pode executar várias tarefas de edição em Conjuntos de imagens, como as seguintes:

* Adicione imagens ao conjunto de imagens.
* Reordene imagens no Conjunto de imagens.
* Exclua ativos no Conjunto de imagens.
* Aplicar predefinições do visualizador.
* Exclua o conjunto de imagens.

**Para editar conjuntos de imagens:**

1. Siga um destes procedimentos:

   * Passe o mouse sobre um ativo do Conjunto de imagens, em seguida, selecione **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o mouse sobre um ativo do Conjunto de imagens, selecione **[!UICONTROL Selecionar]** (ícone de marca de seleção), em seguida selecione **[!UICONTROL Editar]** na barra de ferramentas.
   * Toque em um ativo do Conjunto de imagens e selecione **[!UICONTROL Editar]** (ícone de lápis) na barra de ferramentas.

1. Para editar as imagens no Conjunto de imagens, siga um destes procedimentos:

   * Para reorganizar ativos, arraste uma imagem para um novo local (selecione o ícone de reordenação para mover itens).
   * Para classificar itens em ordem crescente ou decrescente, clique no cabeçalho da coluna.
   * Para adicionar um ativo ou atualizar um ativo existente, clique no botão **[!UICONTROL Adicionar ativo]**. Navegue até um ativo, selecione-o e, em seguida, selecione **[!UICONTROL Selecionar]** próximo ao canto superior direito da página.

      >[!NOTE]
      >
      >Se você excluir a imagem que o Experience Manager usa para a miniatura ao substituí-la por outra imagem, o ativo original ainda é exibido.
   * Para excluir um ativo, selecione-o e **[!UICONTROL Excluir ativo]**.
   * Para aplicar uma predefinição, próximo ao canto superior direito da página, selecione **[!UICONTROL Predefinição]**, em seguida, selecione uma predefinição do visualizador.
   * Para adicionar ou alterar uma miniatura, selecione o ícone de miniatura ao lado direito do ativo. Navegue até a nova miniatura ou ativo de amostra, selecione-o e, em seguida, selecione-o **[!UICONTROL Selecionar]**.
   * Para excluir um conjunto de imagens inteiro, navegue até o conjunto de imagens, selecione-o e selecione **[!UICONTROL Excluir]**.

   >[!NOTE]
   >
   >Você pode editar as imagens em um Conjunto de imagens. Navegue até o conjunto e selecione **[!UICONTROL Definir membros]** no painel esquerdo. Para abrir a janela de edição, selecione o ícone Lápis em um ativo.

1. Toque **[!UICONTROL Salvar]** quando terminar a edição.

## Visualizar conjuntos de imagens {#previewing-image-sets}

Consulte [Visualizar ativos](/help/assets/dynamic-media/previewing-assets.md).

## Publicar conjuntos de imagens {#publishing-image-sets}

Consulte [Publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).
