---
title: Organize seus ativos digitais
description: Organize seus ativos digitais, imagens, arquivos, pastas e assim por diante, usando o Experience Manager.
contentOwner: AG
feature: Asset Management, Search
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 3%

---

# Organize seus ativos digitais {#organize-digital-assets}

Todos os ativos digitais, metadados e conteúdo de documentos do Microsoft® Office e PDF são extraídos e podem ser pesquisados. A pesquisa permite uma filtragem sofisticada em ativos e respeita completamente as permissões apropriadas. Os metadados são abordados detalhadamente em Metadados no Gerenciamento de ativos digitais.

[!DNL Experience Manager Assets] O suporta várias maneiras de organizar o conteúdo. Você pode organizá-las de maneira hierárquica usando pastas ou pode organizá-las de maneira não ordenada e ad hoc, por exemplo, tags. Os usuários podem editar tags no Editor de ativos DAM, onde subativos, representações e metadados são exibidos.

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a new folder.
1. In the menu, click **[!UICONTROL Create]**. Select **[!UICONTROL New Folder]**.
1. In the **[!UICONTROL Title]** field, provide a folder name. By default, DAM uses the title that you provided as the folder name. Once the folder is created, you can override the default and specify another folder name.
1. Click **[!UICONTROL Create]**. Your folder is displayed in the digital assets folder.

## Add CUG properties to folders {#add-cug-properties-to-folders}

You can limit who can access certain folders in Assets by making the folder part of a closed user group (CUG). To make a folder part of a CUG:

1. In Assets, right-click the folder you want to add closed user group properties for and select **Properties**.  
1. Click the **CUG** tab.
1. Select the **Enabled** check box to make the folder and its assets available only to a closed user group.  
1. Browse to the login page, if there is one, to add that information. Add admitted groups by clicking **Add item**. If necessary, add the realm. Click **OK** to save your changes.

## Use tags to organize assets {#use-tags-to-organize-assets}

You can use folders or tags or both to organize assets. Adding tags to assets makes them more easy to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## Organizar ativos em pastas {#organize-using-folders}

A maneira mais básica de organizar ativos é salvar os ativos em pastas. É semelhante a organizar arquivos em pastas no sistema de arquivos local. Para obter mais informações sobre como criar e gerenciar pastas, consulte [Gerenciar ativos](manage-digital-assets.md). A forma como você nomeia arquivos e pastas, como organiza subpastas e como você manipula os arquivos nessas pastas pode ter um impacto significativo na maneira como esses ativos são processados. Ao usar estratégias consistentes e apropriadas de nomenclatura de arquivos e pastas, juntamente com uma boa prática de metadados, você pode aproveitar ao máximo seu repositório de ativos digitais.

* Geralmente, seu repositório de ativos digitais está sempre crescendo. Portanto, é importante formalizar o uso de metadados, a estrutura de pastas e a nomenclatura de arquivos no início do ciclo de criação de conteúdo.
* Use pastas somente para impor uma estrutura de armazenamento consistente para seus ativos digitais. Essa consistência ajuda a processar e gerencia melhor seus ativos. Por exemplo, os ativos colocados nos seguintes tipos de pastas podem ajudar a segregar seus ativos:

   * **Pastas de desenvolvimento**: contém ativos digitais em que você está trabalhando no momento.
   * **Pastas de clientes**: contém ativos digitais com base em clientes ou nomes de projeto.
   * **Pastas primárias**: contém ativos digitais de origem original.
   * **Pastas de representação**: contém representações e cópias dos ativos digitais de origem original.
   * **Pastas de tamanho de arquivo**: contém ativos digitais com base em tamanhos de arquivo pequenos, médios ou grandes.
   * **Pastas de preparo**: O contém ativos digitais prontos para publicação ao vivo em seu site.
   * **Pastas de tipo MIME**: contém ativos digitais específicos para tipos MIME, como imagens, documentos e multimídia.
   * **Arquivar pastas**: contém ativos digitais removidos.
   * **Pastas baseadas em data**: contém ativos digitais com base em uma data de criação ou em uma data da última modificação.

* Crie um diretório de pastas que provavelmente não serão alteradas para que qualquer personalização ou automação continue a funcionar. Por exemplo, os perfis de processamento atribuídos continuam a funcionar.
* Se um ativo já estiver publicado, você usará [!DNL Experience Manager] para mover o ativo para outra pasta e republicar de seu novo local. O local do ativo publicado original ainda está disponível junto com o ativo republicado recentemente. O ativo publicado original, no entanto, é *perdido* para [!DNL Experience Manager] e não pode desfazer a publicação. Portanto, como prática recomendada, primeiro cancele a publicação de um ativo e depois o mova para uma pasta diferente.

## Organizar ativos usando tags {#use-tags-to-organize-assets}

Adicionar tags a ativos facilita sua recuperação durante uma pesquisa, criar coleções usando os resultados da pesquisa, aumentar a classificação de pesquisa para alguns ativos e aplicar algoritmos de IA do Adobe Sensei para descoberta de ativos.

[!DNL Adobe Experience Manager Assets] O usa um algoritmo de autoaprendizado para criar tags altamente descritivas que permitem encontrar o ativo certo em apenas alguns cliques. A marcação inteligente usa a Adobe Sensei, a inteligência artificial e a estrutura de aprendizado de máquina, que podem ser treinadas para reconhecer e aplicar tags padrão e específicas de negócios a imagens. As Tags inteligentes também podem identificar conteúdo, palavras individuais ou frases e aplicar automaticamente tags descritivas aos ativos.

Veja a seguir as etapas para adicionar tags a um ativo:

1. Faça logon em [!DNL Experience Manager Assets].
1. Clique em **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**, selecione o ativo e clique em **[!UICONTROL Propriedades]** para abrir as propriedades do ativo.
1. No **[!UICONTROL Básico]** , clique no ícone da pasta em **[!UICONTROL Tags]** metadados. Uma janela pop-up é aberta.
1. Pesquise ou selecione as tags apropriadas a partir das tags existentes em `cq-tags`. Você pode atribuir várias tags ao ativo.

   Você pode classificar a estrutura das tags em ordem crescente ou decrescente com base na variável **[!UICONTROL Nome]** (ordem alfabética), **[!UICONTROL Criado]** data, ou **[!UICONTROL Modificado]** data. Na ilustração a seguir, a estrutura de tags é classificada alfabeticamente com base na variável **[!UICONTROL Nome]**.

   ![adicionar tags](assets/add-tags-to-asset.png)

1. Clique em **Salvar** para atualizar as alterações nos metadados do ativo.

Para obter mais informações, consulte os seguintes artigos:

* [Editar metadados de ativos](meta-edit.md)
* [Tags inteligentes no Assets](smart-tags.md)
* [Adicionar tags predicado ao painel de pesquisa](/help/assets/search-facets.md/#adding-a-tags-predicate)

## Organizar como coleções {#organize-as-collections}

Com coleções de ativos em [!DNL Experience Manager Assets], você pode otimizar a capacidade de criar, editar e compartilhar ativos entre usuários. Crie vários tipos de coleções com base na maneira como você as usa, incluindo coleções que contêm uma lista de referência estática de ativos, pastas e coleções, e coleções que extrai ativos com base em critérios de pesquisa. Você pode criar coleções com ativos de diferentes locais e compartilhá-las com vários usuários com diferentes níveis de acesso, privilégios de visualização e edição.

Para obter mais informações, consulte [gerenciar coleções](manage-collections.md)


## Usar perfis para organizar seus ativos {#organize-to-use-profiles}

Um perfil de processamento contém [!DNL Assets] comandos de processamento que se aplicam a ativos que são carregados em pastas predefinidas. Os perfis são usados para automatizar o processamento do conteúdo de uma pasta ou dos ativos carregados recentemente. Você pode usar perfis para organizar seus ativos melhor.

Padronizar o uso de metadados, a nomenclatura de arquivos e a estrutura de pastas garante que, à medida que seu conjunto de ativos digitais cresce, você possa aplicar perfis de processamento a pastas com maior precisão e consistência.

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

>[!MORELIKETHIS]
>
>* [Usar microsserviços de ativos e perfis de processamento](asset-microservices-configure-and-use.md)
>* [Perfis de metadados](metadata-profiles.md)
>* [Perfis de vídeo](/help/assets/dynamic-media/video-profiles.md)
>* [Perfis de imagem do Dynamic Media](/help/assets/dynamic-media/image-profiles.md)


