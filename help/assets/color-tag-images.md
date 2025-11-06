---
title: Tags de cores para imagens
description: O Adobe Experience Manager Assets permite distinguir cores em uma imagem e aplicá-las automaticamente como tags. Em seguida, você pode usar essas tags para pesquisar e filtrar imagens.
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
feature: Smart Imaging, Interactive Images, Asset Management
role: User, Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---

# Tags de cores para imagens {#color-tag-images}

![Banner de Marcação de Cores](assets/banner-image.png)

O Adobe Experience Manager (AEM) Assets usa os recursos de IA do Adobe Sensei para distinguir cores em uma imagem e aplicá-las automaticamente como tags na assimilação. Essas tags permitem uma experiência de pesquisa aprimorada, com base na composição de cores da imagem.

Você pode configurar o número de cores, dentro de um intervalo de um a 40, que são marcados em uma imagem para que você possa pesquisar imagens com base nessas cores posteriormente. O Experience Manager Assets aplica as tags com base na cobertura de cor de uma imagem. Também é possível configurar o formato de exibição de uma tag de cor.

A figura a seguir ilustra a sequência de tarefas executada para configurar e gerenciar a marcação de cores para imagens no Experience Manager Assets:

![Marcação de cores](assets/color-tagging-dfd.gif)

## Formatos de arquivo não compatíveis {#supported-file-formats-color-tags}

| Formato do arquivo | Extensão | Tipo MIME | Espaço de cor de entrada | Tamanho máximo de arquivo de origem com suporte | Resolução máxima de tamanho de arquivo suportada |
|---|---|---|---|---|---|
| JPEG | .jpg e .jpeg | image/jpeg | sRGB | 15 GB | 20000 × 20000 pixels |
| PNG | .png | image/png | sRGB | 15 GB | 20000 × 20000 pixels |
| TIFF | .tif e .tiff | image/tiff | sRGB | 4 GB (limitado pelas especificações de formato) | 20000 × 20000 pixels |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB (limitado pelas especificações de formato) | 20000 × 20000 pixels |
| GIF | .gif | image/gif | sRGB | 15 GB | 20000 × 20000 pixels |
| BMP | .bmp | image/bmp | sRGB | 4 GB (limitado pelas especificações de formato) | 20000 × 20000 pixels |

## Gerenciar propriedades de marcação de cores {#manage-color-tagging-properties}

Para gerenciar as propriedades de marcação de cores para imagens:

1. Navegue até **[!UICONTROL Ferramentas > Assets > Marcação de cores]**.

   ![Propriedades de Marcação de Cores](assets/color-tag-settings.png)

1. Especifique um formato de exibição para a marca de cor no campo **[!UICONTROL Formato de Exibição]**. As opções possíveis incluem o nome da cor, RGB ou formato HEX.

1. Especifique o número de cores que deseja marcar para as imagens no campo **[!UICONTROL Limite]**. Essas cores são exibidas quando você exibe as propriedades de uma imagem. Você pode definir um número entre um e 40 nesse campo. O valor padrão desse campo é dez cores.

1. Especifique a porcentagem mínima de cobertura de cor para incluir uma marca de cor nos resultados da pesquisa no campo **[!UICONTROL Limite de Cobertura/Domínio %]**. Por exemplo, se a cobertura da cor vermelha em uma imagem for de dez por cento e você definir nove por cento nesse campo, a imagem será incluída quando você pesquisar imagens com a cor vermelha. No entanto, se a cobertura da cor vermelha em uma imagem for de dez por cento e você definir 11 por cento nesse campo, a imagem não será incluída quando você pesquisar imagens com cor vermelha.

   Você pode especificar qualquer número entre cinco e 100 nesse campo. O valor padrão é 11.

   >[!NOTE]
   >
   >A Adobe recomenda usar um valor próximo ao valor padrão neste campo. Definir um valor de número alto definido para esse campo (por exemplo, maior que 25) pode retornar poucos resultados de pesquisa. Da mesma forma, definir um valor de número baixo (por exemplo, menor que 6) pode retornar muitos resultados de pesquisa, o que pode não ser útil.

1. Clique em **[!UICONTROL Salvar]**.


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### Desativar marcação de cores {#disable-color-tagging}

A marcação de cores para imagens é ativada por padrão. Você pode desativar a marcação de cores no nível da pasta. Todas as pastas derivadas herdam as propriedades de marcação de cores da pasta principal.

Para desativar a marcação de cores no nível da pasta:

1. Navegue até **[!UICONTROL Adobe Experience Manager > Assets > Arquivos]**.

1. Selecione a pasta e clique em **[!UICONTROL Propriedades]**.

1. Na guia **[!UICONTROL Processamento de ativos]**, navegue até a pasta **[!UICONTROL Marcas de cores para imagens]**. Selecione um dos seguintes valores na lista suspensa:

   * Herdada - A pasta herda as opções ativar ou desativar da pasta principal.

   * Ativar - Ativa a marcação de cores para a pasta selecionada.

   * Desativar - Desativa a marcação de cores para a pasta selecionada.

   ![Configurações de Marcação de Cores](assets/color-tags-folder.png)

## Configurar esquema de metadados para adicionar componente de tags de cores inteligentes {#configure-metadata-schema}

Os esquemas de metadados contêm campos específicos para informações específicas a serem preenchidas. Ele também contém informações de layout para exibir campos de metadados de forma simples. As propriedades de metadados incluem título, descrição, tipos MIME, tags e muito mais. Você pode usar o editor [!UICONTROL Forms de Esquema de Metadados] para modificar os esquemas existentes ou adicionar esquemas de metadados personalizados.

>[!NOTE]
>
>O campo Tag de cor inteligente está disponível no esquema de metadados padrão. Se estiver usando um esquema de metadados personalizado, configure o esquema para adicionar um campo de tag de cor inteligente.

Para adicionar o componente Tags de cores inteligentes ao Editor do formulário de esquema de metadados:

1. Navegue até **[!UICONTROL Ferramentas > Assets > Esquemas de metadados]**.

1. Selecione o nome do esquema e clique em **[!UICONTROL Editar]**.

1. Arraste **[!UICONTROL Marcas de Cores Inteligentes]** da guia **[!UICONTROL Criar Formulário]** para o **[!UICONTROL Editor de Formulário de Esquema de Metadados]**.

1. Clique no **[!UICONTROL Campo de Marca de Cores Inteligentes]** no **[!UICONTROL Editor do Formulário de Esquema de Metadados]**.

1. Especifique um valor apropriado no campo **[!UICONTROL Rótulo do campo]** da guia **[!UICONTROL Configurações]**.

1. Clique em **[!UICONTROL Salvar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## Tags de cores para imagens existentes no DAM {#color-tags-existing-images}

As imagens existentes no DAM não são marcadas com tags de cores automaticamente. [!UICONTROL Reprocesse o Assets] manualmente para gerar marcas de cores para eles.

Para colorir imagens de tags ou pastas (incluindo subpastas) de ativos que existem no repositório de ativos, siga estas etapas:

1. Selecione o logotipo [!DNL Adobe Experience Manager] e selecione os ativos da página [!UICONTROL Navegação].

1. Selecione [!UICONTROL Arquivos].

1. Na interface do Assets, navegue até a pasta à qual deseja aplicar tags de cor.

1. Selecione a pasta inteira ou imagens específicas.

1. Selecione o ícone ![Reprocessar ativos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocessar Assets] e selecione a opção [!UICONTROL Processo completo].

Quando o processo for concluído, navegue até a página [!UICONTROL Propriedades] de qualquer imagem dentro da pasta. As marcas adicionadas automaticamente são vistas na seção [!UICONTROL Tags de Cores Inteligentes] da guia [!UICONTROL Básicas].


## Exibir tags de cores inteligentes para imagens {#view-color-tags}

Para exibir tags de cores inteligentes para imagens:

1. Navegue até **[!UICONTROL Adobe Experience Manager > Assets > Arquivos]**.

1. Clique na pasta apropriada e selecione a imagem.

1. Selecione **[!UICONTROL Propriedades]** e exiba as marcas no campo **[!UICONTROL Marcas de Cores Inteligentes]**.

   ![Exibir Marcas de Cores](assets/view-color-tags.png)

   Passe o mouse sobre uma marca de cor para que você possa visualizar o **[!UICONTROL Limite de Cobertura/Domínio %]** de uma cor em uma imagem.

## Configurar predicado de cor do AEM Assets {#configure-search-predicate}

É possível configurar um filtro de pesquisa para imagens. Em seguida, você pode basear os critérios de pesquisa em uma cor específica para filtrar os resultados.

>[!NOTE]
>
>Configure o predicado de cor do AEM Assets somente se não estiver usando o formulário de pesquisa padrão.

Para configurar o filtro de pesquisa, crie um predicado de cor do ativo usando o painel de pesquisa do administrador do Assets.

Para configurar o filtro de pesquisa:

1. Navegue até **[!UICONTROL Ferramentas > Geral > Pesquisar Forms]**.

1. Selecione **[!UICONTROL Painel de pesquisa do administrador do Assets]** e clique em **[!UICONTROL Editar]**.

1. Arraste **[!UICONTROL Predicado de cor do ativo]** da guia **[!UICONTROL Selecionar predicado]** para o **[!UICONTROL Editor de formulário de pesquisa]**.

1. Especifique um valor apropriado no campo **[!UICONTROL Rótulo do campo]** da guia **[!UICONTROL Configurações]**.

1. Clique em **[!UICONTROL Concluído]** para salvar as configurações.

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## Pesquisar imagens com base nas cores {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

Após configurar todas as propriedades de marcação de cores e [configurar o predicado de cores do Assets](#search-images-based-on-colors), você pode pesquisar imagens com base em uma cor como filtro.

Para pesquisar imagens com base em cores:

1. Navegue até **[!UICONTROL Assets > Arquivos]**.

1. Selecione **[!UICONTROL Filtro]** na lista suspensa.
   ![Filtrar Assets](assets/filter-assets.png)

1. Selecione o [predicado de cor do AEM Assets](#configure-search-predicate).

1. Arraste o seletor de cores para selecionar a cor apropriada. A cor selecionada é exibida no campo somente leitura disponível abaixo do seletor de cores. Você pode selecionar RGB ou HEX como o formato de exibição da cor.

   ![Seletor de Cores](assets/color-picker-color-tags.png)

   É possível filtrar imagens com base na seleção de uma cor. As imagens que têm a cor selecionada como uma das marcas de cores inteligentes e acima do [Limite de Cobertura/ Domínio %](#manage-color-tagging-settings) são exibidas no painel direito.

1. Limpe o filtro clicando em X na barra de Pesquisa.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
