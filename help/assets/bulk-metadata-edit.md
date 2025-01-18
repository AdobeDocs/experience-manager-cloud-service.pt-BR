---
title: Edição de metadados em massa na exibição do Assets
description: Saiba como atualizar um conjunto predefinido de campos de metadados padrão para vários ativos disponíveis na Exibição do Assets simultaneamente.
exl-id: f5fee1b3-2855-4010-ae4a-216beb20920d
source-git-commit: f986cbc979ecdb9e704257a8b94db9de0d67d4f1
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Edição de metadados em massa na exibição do Assets{#how-to-edit-the-metadata-of-multiple-assets-simultaneously}

O recurso **Edição de metadados em massa** na Exibição do Assets permite que os usuários editem um conjunto predefinido de campos de metadados padrão para vários arquivos de ativos simultaneamente. Selecione vários ativos e atualize em massa o conjunto predefinido de metadados padrão de uma só vez em vez de atualizar os metadados padrão de cada ativo individualmente. Esse recurso melhora a eficiência, a consistência e a precisão das propriedades de metadados padrão em um grande conjunto de ativos, melhorando a capacidade de pesquisa e organização de ativos.

## Editar metadados de ativos em massa {#how-to-bulk-edit-the-metadata-of-multiple-assets-on-assets-view}

Execute essas etapas para editar os metadados de vários ativos em massa de uma só vez:

1. Na Exibição do Assets, clique em **Assets**.
1. Procure ativos específicos ou pesquise-os usando palavras-chave na barra de pesquisa.
1. Selecione os ativos e clique em **Edição de metadados em massa** no menu superior.
   ![editar metadados em massa](/help/assets/assets/bulk-metadata-edit1.png)
1. Na página Editar metadados, edite os seguintes campos no painel **Propriedades**:
   * **Status:** selecione um status para os ativos selecionados.
   * **Data de expiração:** Defina uma data após a qual os ativos não serão mais válidos ou necessários.
   * **Autor:** especifique o nome do autor.
   * **Palavras-chave:** Adicione termos específicos ou cadeias de texto que forneçam informações de alto nível sobre os ativos para aprimorar sua descoberta. Adicione uma palavra-chave e pressione Enter ou return para adicionar outra palavra-chave à lista.
   * **Marcas:** Clique em ![ícone de marcas](/help/assets/assets/tags-icon.svg) para selecionar marcas dentre as opções disponíveis. As tags fornecem informações mais específicas sobre os ativos e melhoram sua descoberta. As marcas já aplicadas aos ativos selecionados são exibidas no painel **Propriedades**. Se você não conseguir encontrar as tags relevantes, crie-as e atribua aos ativos selecionados. Consulte [Gerenciar marcas no modo de exibição Assets](/help/assets/tagging-management-assets-view.md) para obter detalhes sobre como criar e atribuir marcas a ativos.
   * Clique em **Salvar** para aplicar as atualizações de metadados acima aos ativos selecionados. Depois de salvas, as Palavras-chave e as Tags são anexadas, enquanto os detalhes atualizados de Status, Data de expiração e Autor substituem os detalhes existentes.
     ![save-bulk-metadata-edit-properties](/help/assets/assets/save-bulk-metadata-edit-properties2.png)

     >[!NOTE]
     >
     >É possível editar os metadados de 100 ativos de cada vez.

Para ver as atualizações de metadados aplicadas a um ativo, navegue até a página de detalhes do ativo (selecione o ativo e clique em **Detalhes**) e clique em ![](/help/assets/assets/info-icon-solid-black.svg) para ver os metadados do ativo no painel **Informações**.

>[!NOTE]
>
>**Status**, **Data de expiração**, **Autor**, **Palavras-chave** e **Marcas** são propriedades de metadados padrão disponíveis para edição de metadados em massa, independentemente dos metadados específicos da pasta. Essas propriedades de metadados são exibidas na página de detalhes do ativo somente se forem incluídas no formulário de metadados aplicado à pasta do ativo. Se você não conseguir encontrar essas propriedades de metadados padrão na página de detalhes do ativo, edite o formulário de metadados da pasta de ativos para incluí-las. Consulte [Metadados no Assets View](/help/assets/metadata-assets-view.md) para saber como criar ou editar um formulário de metadados e aplicá-lo a uma pasta.
