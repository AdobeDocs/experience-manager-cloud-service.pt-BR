---
title: Tags de cores para imagens
description: O Experience Manager Assets permite distinguir entre cores em uma imagem e aplicá-las automaticamente como tags. Em seguida, você pode usar essas tags para pesquisar e filtrar imagens.
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 8%

---

# Tags de cores para imagens {#color-tag-images}

![Banner de marcação de cores](assets/banner-image.png)

O Experience Manager Assets usa os recursos do Adobe Sensei AI para distinguir entre cores em uma imagem e aplicá-las automaticamente como tags na assimilação. Essas tags permitem uma experiência de pesquisa aprimorada, com base na composição de cores da imagem.

É possível configurar o número de cores, dentro de um intervalo de uma a quarenta, que são marcadas em uma imagem para que, posteriormente, você possa pesquisar por imagens com base nessas cores. O Experience Manager Assets aplica as tags com base na cobertura de cor em uma imagem. Você também pode configurar o formato de exibição para uma tag de cor.

A figura a seguir ilustra a sequência de tarefas que você executa para configurar e gerenciar a marcação de cores para imagens no Experience Manager Assets:

![Marcação de cores](assets/color-tagging-dfd.gif)

## Formatos de arquivo não compatíveis {#supported-file-formats-color-tags}

| Formato de arquivo | Extensão | Tipo MIME | Colorspace de entrada | Tamanho máximo de arquivo de origem suportado | Resolução máxima de tamanho de arquivo suportado |
|---|---|---|---|---|---|
| JPEG | .jpg, .jpeg | image/jpeg | sRGB | 15GB | 20000px X 20000px |
| PNG | .png | image/png | sRGB | 15GB | 20000px X 20000px |
| TIFF | .tif, .tiff | image/tiff | sRGB | 4 GB (limitado pelas especificações de formato | 20000px X 20000px |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB (limitado pelas especificações de formato) | 20000px X 20000px |
| GIF | .gif | image/gif | sRGB | 15GB | 20000px X 20000px |
| BMP | .bmp | image/bmp | sRGB | 4 GB (limitado pelas especificações de formato) | 20000px X 20000px |

## Gerenciar propriedades de marcação de cores {#manage-color-tagging-properties}

Para gerenciar as propriedades de marcação de cores de imagens:

1. Navegar para **[!UICONTROL Ferramentas > Ativos > Marcação de cores]**.

   ![Propriedades da marcação de cores](assets/color-tag-settings.png)

1. Especifique um formato de exibição para a tag de cor no **[!UICONTROL Exibir formato]** campo. As opções possíveis incluem o nome da cor, o RGB ou o formato HEX.

1. Especifique o número de cores a serem marcadas para as imagens no **[!UICONTROL Limite]** campo. Essas cores são exibidas quando você visualiza as propriedades de uma imagem.  É possível definir um número entre um e quarenta nesse campo. O valor padrão para esse campo é de dez cores.

1. Especifique a porcentagem mínima de cobertura de cor para incluir uma tag de cor nos resultados da pesquisa no **[!UICONTROL Limite de Cobertura/Domínio %]** campo. Por exemplo, se a cobertura da cor vermelha em uma imagem for de 10% e você definir 9% nesse campo, a imagem será incluída quando você pesquisar por imagens com a cor vermelha. No entanto, se a cobertura da cor vermelha em uma imagem for de 10% e você definir 11% nesse campo, a imagem não será incluída quando você procurar imagens com a cor vermelha.

   Você pode especificar qualquer número entre cinco e cem neste campo. O valor padrão é onze.

   >[!NOTE]
   >
   >O Adobe recomenda usar um valor próximo ao valor padrão neste campo. A configuração de um valor de número alto para esse campo (por exemplo, maior que 25) pode retornar muito poucos resultados de pesquisa. Da mesma forma, definir um valor de número baixo (por exemplo, menor que 6) pode retornar muitos resultados de pesquisa, o que pode não ser útil.

1. Clique em **[!UICONTROL Salvar]**.


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### Desativar marcação de cores {#disable-color-tagging}

A marcação de cores de imagens é ativada por padrão. Você pode desativar a marcação de cores no nível da pasta. Todas as pastas secundárias herdam as propriedades de marcação de cores da pasta principal.

Para desativar a marcação de cores no nível da pasta:

1. Navegar para **[!UICONTROL Adobe Experience Manager > Ativos > Arquivos]**.

1. Selecione a pasta e clique em **[!UICONTROL Propriedades]**.

1. No **[!UICONTROL Processamento de ativos]** , navegue até a guia **[!UICONTROL Tags de cores para imagens]** pasta. Selecione um dos seguintes valores na lista suspensa:

   * Herdada - A pasta herda as opções ativar ou desativar da pasta principal.

   * Ativar - Ativa a marcação de cores para a pasta selecionada.

   * Desativar - Desativa a marcação de cores para a pasta selecionada.

   ![Configurações de marcação de cores](assets/color-tags-folder.png)

## Configurar esquema de metadados para adicionar o componente de tags de cores inteligentes {#configure-metadata-schema}

Os esquemas de metadados contêm campos específicos para informações específicas a serem preenchidas. Também contém informações de layout para exibir campos de metadados de maneira fácil de usar. As propriedades dos metadados incluem título, descrição, tipos MIME, tags e muito mais. Você pode usar o [!UICONTROL Forms do esquema de metadados] para modificar os esquemas existentes ou adicionar esquemas de metadados personalizados.

>[!NOTE]
>
>O campo Tag de cor inteligente está disponível no esquema de metadados padrão. Se estiver usando um esquema de metadados personalizado, configure o esquema para adicionar um campo de tag de cor inteligente.

Para adicionar o componente Tags de cores inteligentes ao Editor de formulário do esquema de metadados:

1. Navegar para **[!UICONTROL Ferramentas > Ativos > Esquemas de metadados]**.

1. Selecione o nome do esquema e clique em **[!UICONTROL Editar]**.

1. Arrastar **[!UICONTROL Tags de cores inteligentes]** do **[!UICONTROL Criar formulário]** para **[!UICONTROL Editor de formulário do esquema de metadados]**.

1. Clique no botão **[!UICONTROL Campo de tag de cores inteligentes]** no **[!UICONTROL Editor de formulário do esquema de metadados]**.

1. Especifique um valor apropriado no **[!UICONTROL Rótulo do campo]** no campo **[!UICONTROL Configurações]**  guia .

1. Clique em **[!UICONTROL Salvar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## Tags de cores para imagens existentes no DAM {#color-tags-existing-images}

As imagens já existentes no DAM não são marcadas por cores automaticamente. Você precisa [!UICONTROL Reprocessar ativos] para gerar tags de cores manualmente.

Para colorir imagens de tags ou pastas (incluindo subpastas) de ativos que já existem no repositório de ativos, siga estas etapas:

1. Selecione o [!DNL Adobe Experience Manager] e, em seguida, selecione ativos no [!UICONTROL Navegação] página.

1. Selecionar [!UICONTROL Arquivos] para exibir a interface do Assets.

1. Navegue até a pasta na qual deseja aplicar tags de cores.

1. Selecione a pasta inteira ou imagens específicas.

1. Selecionar ![Ícone Reprocessar ativos](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocessar ativos] e selecione o [!UICONTROL Processo completo] opção.

Depois que o processo for concluído, navegue até a [!UICONTROL Propriedades] de qualquer imagem dentro da pasta. As tags adicionadas automaticamente são vistas em [!UICONTROL Tags de cores inteligentes] seção em [!UICONTROL Básico] guia .


## Exibir tags de cores inteligentes para imagens {#view-color-tags}

Para exibir tags de cores inteligentes para imagens:

1. Navegar para **[!UICONTROL Adobe Experience Manager > Ativos > Arquivos]**.

1. Clique na pasta apropriada e selecione a imagem.

1. Selecionar **[!UICONTROL Propriedades]** e visualize as tags no **[!UICONTROL Tags de cores inteligentes]** campo.

   ![Exibir tags de cores](assets/view-color-tags.png)

   Passe o mouse sobre uma tag de cor para visualizar o **[!UICONTROL Limite de Cobertura/Domínio %]** de uma cor em uma imagem.

## Configurar o predicado de cores do AEM Assets {#configure-search-predicate}

Você pode configurar o filtro de pesquisa para imagens. Você pode então basear seus critérios de pesquisa em uma cor específica para filtrar os resultados.

>[!NOTE]
>
>Configure o predicado de cores do AEM Assets somente se você não estiver usando o formulário de pesquisa padrão.

Para configurar o filtro de pesquisa, crie um Predicado de cores do ativo usando o Painel de pesquisa do administrador de ativos.

Para configurar o filtro de pesquisa:

1. Navegar para **[!UICONTROL Ferramentas > Geral > Pesquisar Forms]**.

1. Selecionar **[!UICONTROL Painel de pesquisa do administrador de ativos]** e clique em **[!UICONTROL Editar]**.

1. Arrastar **[!UICONTROL Predicado de cores do ativo]** do **[!UICONTROL Selecionar predicado]** para **[!UICONTROL Editor de formulário de pesquisa]**.

1. Especifique um valor apropriado no **[!UICONTROL Rótulo do campo]** no campo **[!UICONTROL Configurações]**  guia .

1. Clique em **[!UICONTROL Concluído]** para salvar as configurações.

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## Pesquisar imagens com base em cores {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

Após configurar todas as propriedades de marcação de cores e [configuração do predicado de cores do Assets](#search-images-based-on-colors), você pode pesquisar imagens com base em uma cor como filtro.

Para pesquisar imagens com base nas cores:

1. Navegar para **[!UICONTROL Ativos > Arquivos]**.

1. Selecionar **[!UICONTROL Filtro]** na lista suspensa.
   ![Filtrar ativos](assets/filter-assets.png)

1. Selecione o [Predicado de cores do AEM Assets](#configure-search-predicate).

1. Arraste o seletor de cores para selecionar a cor apropriada. A cor selecionada é exibida no campo somente leitura disponível abaixo do seletor de cores. Você pode selecionar RGB ou HEX como o formato de exibição para a cor.

   ![Seletor de cores](assets/color-picker-color-tags.png)

   Você pode filtrar imagens com base na seleção de uma cor. As imagens que têm a cor selecionada como uma das tags de cores inteligentes e acima da [% Limite de Cobertura/Domínio](#manage-color-tagging-settings) no painel direito.

1. Clique em x na barra de Pesquisa para limpar o filtro.

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
