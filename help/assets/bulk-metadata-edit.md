---
title: Edição de metadados em massa em  [!DNL Assets View]
description: Saiba como atualizar um conjunto predefinido de campos de metadados padrão para vários ativos disponíveis no [DNL! Visualização do Assets] simultaneamente.
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Editar metadados em massa em [!DNL Assets View]{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

O recurso **[!DNL Bulk Metadata Edit]** do [!DNL Assets View] permite que você edite um conjunto predefinido de campos de metadados padrão para vários arquivos de ativos simultaneamente. Selecione vários ativos e atualize em massa o conjunto predefinido de metadados padrão de uma só vez em vez de atualizar os metadados padrão de cada ativo individualmente. Esse recurso mantém a eficiência, a consistência e a precisão do conjunto de propriedades de metadados padrão nos grandes conjuntos de ativos, melhorando a capacidade de pesquisa e a organização desses ativos.

## Editar metadados de ativos em massa {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

Execute essas etapas para editar os metadados de vários ativos em massa de uma só vez:

1. Navegue até **[!DNL Assets View]** e clique em **[!UICONTROL Assets]**.
1. Procure ativos específicos ou pesquise-os usando palavras-chave na barra de pesquisa.
1. Selecione os ativos e clique em **[!UICONTROL Edição de metadados em massa]** no menu superior.
   ![editar metadados em massa](/help/assets/assets/bulk-metadata-edit1.png)
1. Na [!UICONTROL página Editar metadados], edite os seguintes campos no painel **[!UICONTROL Propriedades]**:
   * **[!UICONTROL Status]:** selecione um status para os ativos selecionados.
   * **[!UICONTROL Data de expiração]:** Defina uma data após a qual os ativos não serão mais válidos ou necessários.
   * **[!UICONTROL Autor]:** Especifique o nome do autor.
   * **[!UICONTROL Palavras-chave]:** adicione termos específicos ou cadeias de texto que forneçam informações de alto nível sobre os ativos para aprimorar sua descoberta. Adicione uma palavra-chave e pressione **Enter** ou **return** para adicionar outra palavra-chave à lista.
   * **[!UICONTROL Marcas]:** Clique em ![editar metadados em massa](/help/assets/assets/tags-icon.svg) para selecionar marcas nas opções disponíveis. As tags fornecem informações mais específicas sobre os ativos e melhoram sua descoberta. As marcas já aplicadas aos ativos selecionados são exibidas no painel **[!UICONTROL Propriedades]**. Se não conseguir encontrar as tags relevantes, crie-as e atribua aos ativos selecionados. Consulte [Gerenciar tags em [!DNL Assets view]](/help/assets/tagging-management-assets-view.md) para obter detalhes sobre como criar e atribuir tags a ativos.
   * Clique em **[!UICONTROL Salvar]** para aplicar as atualizações de metadados acima aos ativos selecionados. Depois de salvas, as **[!UICONTROL Palavras-chave]** e as **[!UICONTROL Marcas]** são anexadas, enquanto os detalhes atualizados do **[!UICONTROL Status]**, da **[!UICONTROL Data de vencimento]** e do **[!UICONTROL Autor]** substituem os detalhes existentes.
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >É possível editar os metadados de 100 ativos de cada vez.

Para ver as atualizações de metadados aplicadas a um ativo, navegue até [!DNL asset details page] (selecione o ativo e clique em **[!UICONTROL Detalhes]**) e clique em ![editar metadados em massa](/help/assets/assets/info-icon-solid-black.svg) para ver os metadados do ativo no painel **[!UICONTROL Informações]**.

>[!NOTE]
>
>**[!UICONTROL Status]**, **[!UICONTROL Data de expiração]**, **[!UICONTROL Autor]**, **[!UICONTROL Palavras-chave]** e **[!UICONTROL Marcas]** são propriedades de metadados padrão disponíveis para edição de metadados em massa, independentemente dos metadados específicos da pasta. Essas propriedades de metadados são exibidas na [!UICONTROL página de detalhes do ativo] somente se forem incluídas no formulário de metadados aplicado à pasta do ativo. Se você não conseguir localizar essas propriedades de metadados padrão na [!UICONTROL página de detalhes do ativo], edite o formulário de metadados da pasta de ativos para incluí-los. Consulte [Metadados em [!DNL Assets View]](/help/assets/metadata-assets-view.md) para saber como criar ou editar um formulário de metadados e aplicá-lo a uma pasta.
