---
title: Organize seus ativos digitais
description: Organize ativos digitais, imagens, arquivos, pastas e assim por diante usando o Experience Manager.
contentOwner: AG
feature: Asset Management, Best Practices
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 5%

---

# Organize seus ativos digitais {#organize-digital-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/organize-assets.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

Todos os ativos digitais, metadados e conteúdo dos documentos do Microsoft® Office e do PDF são extraídos e tornados pesquisáveis. A pesquisa permite uma filtragem sofisticada de ativos e respeita completamente as permissões apropriadas. Os metadados são abordados em detalhes em Metadados no Gerenciamento de ativos digitais.

O [!DNL Experience Manager Assets] oferece suporte a várias formas de organização de conteúdo. Você pode organizá-los de maneira hierárquica usando pastas ou de maneira não ordenada e ad hoc, por exemplo, tags. Os usuários podem editar tags no Editor de ativos DAM, onde subativos, representações e metadados são exibidos.

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a folder.
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

You can use folders or tags or both to organize assets. Adding tags to assets makes them easier to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## Organizar ativos em pastas {#organize-using-folders}

A maneira mais básica de organizar ativos é salvá-los em pastas. É análogo a organizar arquivos em pastas em seu sistema de arquivos local. Para obter mais informações sobre como criar e gerenciar pastas, consulte [Gerenciar ativos](manage-digital-assets.md). A maneira como você nomeia arquivos e pastas, como organiza subpastas e como lida com os arquivos dentro dessas pastas pode ter um impacto significativo na maneira como esses ativos são processados. Usando estratégias consistentes e apropriadas de nomenclatura de arquivos e pastas, juntamente com boas práticas de metadados, você pode aproveitar ao máximo seu repositório de ativos digitais.

* Normalmente, o repositório de ativos digitais está sempre crescendo. Portanto, é importante formalizar o uso de metadados, a estrutura de pastas e a nomenclatura de arquivos no início do ciclo de criação de conteúdo.
* Use pastas somente para impor uma estrutura de armazenamento consistente para seus ativos digitais. Essa consistência ajuda a processar e gerenciar melhor seus ativos. Por exemplo, os ativos colocados nos seguintes tipos de pastas podem ajudá-lo a segregar seus ativos:

   * **Pastas de desenvolvimento**: contém ativos digitais nos quais você está trabalhando atualmente.
   * **Pastas do cliente**: contém ativos digitais com base em clientes ou nomes de projeto.
   * **Pastas primárias**: contém ativos digitais originais e de origem.
   * **Pastas de representação**: contém representações e cópias dos ativos digitais originais e de origem.
   * **Pastas de Tamanho de Arquivo**: contém ativos digitais baseados em arquivos pequenos, médios ou grandes.
   * **Pastas de preparo**: contém ativos digitais que estão prontos para serem publicados em tempo real no seu site.
   * **pastas do tipo MIME**: contém ativos digitais específicos para tipos MIME, como imagens, documentos e multimídia.
   * **Arquivar pastas**: contém ativos digitais desativados.
   * **Pastas baseadas em data**: contém ativos digitais com base em uma data de criação ou uma data da última modificação.

* Crie um diretório de pastas que provavelmente não serão alteradas para que qualquer personalização ou automação continue a funcionar. Por exemplo, os perfis de processamento atribuídos continuam a funcionar.
* Se um ativo já estiver publicado, você usará o [!DNL Experience Manager] para movê-lo para outra pasta e republicar a partir do novo local. O local do ativo original publicado ainda está disponível junto com o ativo recém-republicado. No entanto, o ativo original publicado está *perdido* para [!DNL Experience Manager] e não pode ter sua publicação desfeita. Portanto, como prática recomendada, primeiro cancele a publicação de um ativo e, em seguida, mova-o para uma pasta diferente.

## Organizar ativos usando tags {#use-tags-to-organize-assets}

Adicionar tags aos ativos facilita a recuperação durante uma pesquisa, cria coleções usando os resultados da pesquisa, aumenta a classificação de pesquisa para alguns ativos e aplica algoritmos de IA do Adobe Sensei para a descoberta de ativos.

O [!DNL Adobe Experience Manager Assets] usa um algoritmo de autoaprendizado para criar marcas altamente descritivas que permitem encontrar o ativo correto com apenas alguns cliques. A marcação inteligente usa Adobe Sensei, inteligência artificial e estrutura de aprendizado de máquina, que podem ser treinadas para reconhecer e aplicar tags padrão e específicas de negócios a imagens. As Tags inteligentes também podem identificar conteúdo, palavras individuais ou frases e aplicar automaticamente tags descritivas aos ativos.

Veja a seguir as etapas para adicionar tags a um ativo:

1. Faça logon em [!DNL Experience Manager Assets].
1. Clique em **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**, selecione o ativo e clique em **[!UICONTROL Propriedades]** para abrir as propriedades do ativo.
1. Na guia **[!UICONTROL Básico]**, clique no ícone de pasta nos metadados de **[!UICONTROL Marcas]**. Uma janela pop-up é aberta.
1. Pesquise ou selecione as marcas apropriadas das marcas existentes em `cq-tags`. É possível atribuir várias tags ao ativo.

   Você pode classificar a estrutura de marcas em ordem crescente ou decrescente com base na data **[!UICONTROL Nome]** (ordem alfabética), **[!UICONTROL Criada]** ou **[!UICONTROL Modificada]**. Na ilustração a seguir, a estrutura de marcas é classificada em ordem alfabética com base no **[!UICONTROL Nome]**.

   ![add-tags](assets/add-tags-to-asset.png)

1. Clique em **Salvar** para atualizar as alterações nos metadados do ativo.

Para obter mais informações, consulte os seguintes artigos:

* [Editar metadados de ativos](meta-edit.md)
* [Tags inteligentes no Assets](smart-tags.md)
* [Adicionar predicado de tags ao painel de pesquisa](/help/assets/search-facets.md#adding-a-tags-predicate)

## Organizar como coleções {#organize-as-collections}

Com as coleções de ativos no [!DNL Experience Manager Assets], você pode simplificar a capacidade de criar, editar e compartilhar ativos entre usuários. Crie vários tipos de coleções com base na maneira como você as usa, incluindo coleções que contêm uma lista de referência estática de ativos, pastas e coleções e coleções que extraem ativos com base em critérios de pesquisa. Você pode criar coleções com ativos de diferentes locais e compartilhá-las com vários usuários com diferentes níveis de privilégios de acesso, visualização e edição.

Para obter mais informações, consulte [gerenciar coleções](manage-collections.md)


## Usar perfis para organizar seus ativos {#organize-to-use-profiles}

Um perfil de processamento contém [!DNL Assets] comandos de processamento que se aplicam a ativos carregados em pastas predefinidas. Os perfis são usados para automatizar o processamento de conteúdo de uma pasta ou de ativos carregados recentemente. Você pode usar perfis para organizar melhor seus ativos.

A padronização do uso de metadados, da nomeação de arquivos e da estrutura de pastas garante que, à medida que seu pool de ativos digitais cresce, você possa aplicar perfis de processamento a pastas com mais precisão e consistência.

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

>[!MORELIKETHIS]
>
>* [Usar microsserviços de ativos e perfis de processamento](asset-microservices-configure-and-use.md)
>* [Perfis de metadados](metadata-profiles.md)
>* [Perfis de vídeo](/help/assets/dynamic-media/video-profiles.md)
>* [Perfis de imagem do Dynamic Media](/help/assets/dynamic-media/image-profiles.md)

