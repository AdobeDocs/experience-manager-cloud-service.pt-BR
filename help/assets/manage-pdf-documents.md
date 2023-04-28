---
title: Gerencie seus documentos do PDF em [!DNL Adobe Experience Manager].
description: Gerenciar documentos PDF em [!DNL Adobe Experience Manager] como [!DNL Cloud Service].
feature: Asset Management
role: User,Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 3%

---

# Gerenciar documentos do PDF no Experience Manager Assets as a Cloud Service {#add-assets-to-experience-manager}

O Experience Manager Assets integra-se perfeitamente ao Visualizador de PDF de Document Cloud, o que permite que você visualize várias páginas de um documento de PDF. Além disso, também é possível usar recursos avançados do visualizador de PDF de Document Cloud, como anotações, texto de pesquisa, navegar no documento de PDF usando marcadores e miniaturas e muito mais sob o mesmo teto. O Experience Manager Assets também permite carregar documentos em outros formatos compatíveis e visualizá-los em um formato PDF.

O visualizador de PDF Document Cloud beneficia a AEM Assets das seguintes maneiras:
* [Suporte para componentes do visualizador de Document Cloud PDF](#pdf-doc-cloud)
* [Suporte para visualização de várias páginas e anotações para o PDF Asset](#multi-page)
* [Suporte para visualização de várias páginas em outros formatos](#multi-format)

> Dica
> Se você não conseguir obter a visualização de várias páginas de um documento do PDF carregado anteriormente, selecione o PDF e clique em **![Reprocessar](/help/assets/assets/Reprocess.svg) Reprocessar ativos**.

## Suporte para componentes do visualizador de Document Cloud PDF {#pdf-doc-cloud}

O visualizador nativo da nuvem do PDF Doc tem os seguintes componentes no AEM Assets:

* **Visualizador de PDF usando miniaturas de página** A exibição em miniatura é uma pequena visualização das páginas de um documento do PDF. Usando miniaturas, você pode ir diretamente para a página desejada. Você pode acessar as miniaturas do documento PDF selecionado por meio de ![miniatura](/help/assets/assets/thumbnail.svg) no painel esquerdo.

* **Visualizador de PDF usando marcadores** Marcador é um link direto que navega até o conteúdo no documento. Você pode acessar marcadores do documento PDF selecionado por meio de ![marcador](/help/assets/assets/bookmark.svg) no painel esquerdo.

* **Pesquisar no PDF** Você pode usar a pesquisa ![pesquisa](/help/assets/assets/Search.svg) para buscar o texto no documento PDF.

* **Page Up/Page Down** Usar Page Up ![Page Up](/help/assets/assets/ArrowUp.svg) ou Page Down ![Page Down](/help/assets/assets/ArrowDown.svg) para percorrer o documento.

* **Menos zoom/Menos zoom** Usar Menos Zoom ![Menos zoom](/help/assets/assets/ZoomOut.svg) ou Ampliar ![Ampliar](/help/assets/assets/ZoomIn.svg) para transmitir o documento.

* **Ajuste da página** Use as dimensões de largura ou altura para ajustar o documento de acordo com o tamanho da tela.

* **Encaixar/Desancorar PDF** Você pode ancorar ou desancorar os componentes do visualizador de PDF nativo usando essa opção.

## Suporte para visualização de várias páginas e anotações para o PDF Asset {#multi-page}

O Adobe Experience Manager Assets permite visualizar o documento do PDF que consiste em várias páginas. Para visualizar várias páginas de um documento PDF, considere as seguintes etapas:

1. Siga as etapas para [fazer upload de ativos no AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Procure o documento do PDF que você deseja fazer upload e visualizar.
1. Abra o documento.
1. O visualizador de documentos do PDF é carregado por padrão. Você também pode selecionar PDF rendition no painel representação.
1. Em Representações , selecione **Todas as Representações**.

Também é possível aplicar [anotações](#pdf-annotations) para o documento do PDF em uma visualização de várias páginas.

> OBSERVAÇÃO
> O tamanho máximo de um Ativo que você pode visualizar é de até 100 MB.

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**Anotações PDF{#pdf-annotations}**

O Experience Manager Assets permite adicionar comentários a um documento do PDF. Um documento PDF pode ter várias anotações.

Para anotar um documento PDF, execute as seguintes etapas:
1. Vá para a interface Ativos e navegue até o documento do PDF que deseja anotar. O visualizador de PDF nativo é aberto à direita, mostrando a visualização do documento de PDF selecionado.
1. Clique em **Anotar** no menu superior.
A seguir estão as Anotações que podem ser aplicadas em um documento PDF:

<table>
        <tr>
             <th> Anotação </th>
            <th> Descrição </th>
        </tr>
        <tr>
           <td> <img src="/help/assets/assets/Comment.svg"> Comentar </td>
            <td> Selecione Comentário para expressar uma observação. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> Caixa de texto </td>
            <td> Selecione Caixa de texto para inserir o texto. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> Notas adesivas </td>
            <td> Adicione um pequeno texto ou lembrete que pode ser adicionado a uma área específica no PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> Destaque de texto </td>
            <td> Selecione o texto a ser realçado em cores diferentes. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextUnderline.svg"> Sublinhado de texto </td>
            <td> Selecione o texto que deseja sublinhar. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> Tachado </td>
            <td> Selecione o texto que deseja excluir. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Draw.svg"> Desenho </td>
            <td> Insira uma arte visual no PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> Apagar desenho </td>
             <td> Remover ou desfazer desenho. </td>
        </tr>
    </table>

## Suporte para visualização de várias páginas em outros formatos {#multi-format}

Além dos documentos do PDF, você também pode visualizar várias páginas para documentos em outros tipos de formato. Os tipos de formato de documento compatíveis são TXT, RTF, DOC, DOCX, PPT, PPTX, XLS e XLSX. O Experience Manager Assets converte automaticamente esses formatos de documento em um formato de PDF e os disponibiliza para visualização.

![Visualização de várias páginas de documentos em outros formatos](/help/assets/assets/multi-page-other-formats.png)

Para a visualização de várias páginas de outros formatos de documento compatíveis, execute as seguintes etapas:
1. Siga as etapas para [fazer upload de ativos no AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Navegue pelo documento que deseja carregar e visualizar.
1. Abra o documento.
1. Selecione PDF na seção estática do painel esquerdo. O painel direito mostra a visualização de várias páginas de um ativo. Selecione a miniatura no painel esquerdo para escolher a página que deseja visualizar.

> OBSERVAÇÃO
> * O tamanho máximo de um Ativo que você pode visualizar é de até 100 MB.
> * O tamanho máximo dos arquivos XLS ou XLSX para visualização é de 20 MB.
>


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
