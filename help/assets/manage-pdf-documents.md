---
title: Gerencie seus documentos do PDF no [!DNL Adobe Experience Manager].
description: Gerenciar documentos do PDF em [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
feature: Asset Management
role: User, Admin
exl-id: 29660869-6902-4093-845b-cd629be59d4d
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 4%

---

# Gerenciar documentos do PDF no Experience Manager Assets as a Cloud Service {#add-assets-to-experience-manager}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

O Experience Manager Assets integra-se perfeitamente ao Visualizador de PDF de Document Cloud, o que permite a visualização de várias páginas de um documento PDF. Além disso, você também pode usar recursos avançados do visualizador de PDF Document Cloud, como anotações, texto de pesquisa, navegar pelo documento PDF usando marcadores e miniaturas e muito mais, sob o mesmo teto. O Experience Manager Assets também permite carregar documentos em outros formatos compatíveis e visualizá-los em um formato PDF.

O visualizador de PDF Document Cloud beneficia o AEM Assets das seguintes maneiras:
* [Suporte para componentes do visualizador de Document Cloud do PDF](#pdf-doc-cloud)
* [Suporte para visualização de várias páginas e anotações para o ativo PDF](#multi-page)
* [Suporte para Visualização de Várias Páginas para Documentos em Outros Formatos](#multi-format)

> Dica
> Se você não conseguir obter a visualização de várias páginas de um documento de PDF carregado anteriormente, selecione o PDF e clique em **![Reprocessar](/help/assets/assets/Reprocess.svg) Reprocessar Assets**.
>

## Suporte para componentes do visualizador de Document Cloud do PDF {#pdf-doc-cloud}

O visualizador nativo da PDF Doc Cloud tem os seguintes componentes no AEM Assets:

* Visualizador de **PDF usando miniaturas de página** O modo de exibição de miniatura é uma pequena visualização das páginas de um documento PDF. Usando miniaturas, você pode ir diretamente para a página desejada. Você pode acessar miniaturas do documento PDF selecionado por meio da ![miniatura](/help/assets/assets/thumbnail.svg) no painel esquerdo.

* O visualizador de **PDF usando marcadores** é um link direto que direciona você ao conteúdo no documento. Você pode acessar marcadores do documento PDF selecionado por meio de ![marcador](/help/assets/assets/bookmark.svg) no painel esquerdo.

* **Pesquisar em PDF** Você pode usar a pesquisa ![pesquisar](/help/assets/assets/Search.svg) para pesquisar o texto no documento PDF.

* **Página Acima/Página Abaixo** Use Página Acima ![Página Acima](/help/assets/assets/ArrowUp.svg) ou Página Abaixo ![Página Abaixo](/help/assets/assets/ArrowDown.svg) para rolar pelo documento.

* **Menos Zoom/Mais Zoom** Use Menos Zoom ![Menos Zoom](/help/assets/assets/ZoomOut.svg) ou Menos Zoom ![Mais Zoom](/help/assets/assets/ZoomIn.svg) para distribuir o documento.

* **Ajuste da Página** Use dimensões de largura ou altura para ajustar o documento de acordo com o tamanho da tela.

* **Encaixar/Desencaixar PDF** Você pode encaixar ou desencaixar os componentes do visualizador de PDF nativo usando esta opção.

## Suporte para visualização de várias páginas e anotações para o ativo PDF {#multi-page}

O Adobe Experience Manager Assets permite a visualização do documento PDF com várias páginas. Para visualizar várias páginas de um documento PDF, considere as seguintes etapas:

1. Siga as etapas para [carregar ativos no AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Navegue pelo documento PDF que você deseja carregar e visualizar.
1. Abra o documento.
1. O visualizador de documentos do PDF é carregado por padrão. Você também pode selecionar representação de PDF no painel de representação.
1. No menu suspenso Representações, selecione **Todas as representações**.

Você também pode aplicar [anotações](#pdf-annotations) ao documento PDF em uma visualização de várias páginas.

> OBSERVAÇÃO
> O tamanho máximo de um Ativo que pode ser visualizado é de até 100 MB.
>

>[!VIDEO](https://video.tv.adobe.com/v/3409355)

<!--
![Multi-page Preview](/help/assets/assets/multi-page.png)
-->

**Anotações PDF{#pdf-annotations}**

O Experience Manager Assets permite adicionar comentários a um documento PDF. Um documento PDF pode ter várias anotações.

Para anotar um documento PDF, execute as seguintes etapas:
1. Vá para a interface do Assets e navegue até o documento PDF que deseja anotar. O visualizador de PDF nativo é aberto à direita, mostrando a pré-visualização do documento de PDF selecionado.
1. Clique em **Anotar** no menu superior.
Veja a seguir as Anotações que podem ser aplicadas a um documento PDF:

<table>
        <tr>
             <th> Anotação </th>
            <th> Descrição </th>
        </tr>
        <tr>
           <td> Comentário <img src="/help/assets/assets/Comment.svg"> </td>
            <td> Selecione Comentário para expressar uma observação. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Text.svg"> Caixa de texto </td>
            <td> Selecione Textbox para inserir o texto. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Note.svg"> Notas adesivas </td>
            <td> Adicione um pequeno texto ou lembrete que você pode adicionar a uma área específica no PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Comment.svg"> Realçador de texto </td>
            <td> Selecione o texto a ser realçado em cores diferentes. </td>
        </tr>
        <tr>
            <td> Sublinhado de texto <img src="/help/assets/assets/TextUnderline.svg"> </td>
            <td> Selecione o texto que deseja sublinhar. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/TextStrikethrough.svg"> Tachado </td>
            <td> Selecione o texto que deseja riscar. </td>
        </tr>
        <tr>
            <td> Desenho <img src="/help/assets/assets/Draw.svg"> </td>
            <td> Insira uma arte visual no PDF. </td>
        </tr>
        <tr>
            <td> <img src="/help/assets/assets/Erase.svg"> Apagar desenho </td>
             <td> Remover ou desfazer desenho. </td>
        </tr>
    </table>

>[!NOTE]
>
>As anotações adicionadas ao documento PDF estão disponíveis no modo de visualização. No entanto, as anotações não são exibidas quando você baixa ou imprime o documento PDF.

## Suporte para Visualização de Várias Páginas para Documentos em Outros Formatos {#multi-format}

Além dos documentos PDF, você também pode visualizar várias páginas de documentos em outros tipos de formato. Os tipos de formato de documento compatíveis são TXT, RTF, DOC, DOCX, PPT, PPTX, XLS e XLSX. O Experience Manager Assets converte automaticamente esses formatos de documento em um formato PDF e os disponibiliza para visualização.

![Visualização de Documentos em Outros Formatos em Várias Páginas](/help/assets/assets/multi-page-other-formats.png)

Para a visualização de várias páginas de outros formatos de documento compatíveis, execute as seguintes etapas:
1. Siga as etapas para [carregar ativos no AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/add-assets.html?lang=en).
1. Procure o documento que você deseja carregar e visualizar.
1. Abra o documento.
1. Selecione PDF na seção estática, no painel esquerdo. O painel direito mostra a pré-visualização de várias páginas de um ativo. Selecione miniatura, no painel esquerdo, para escolher a página que deseja visualizar.

> OBSERVAÇÃO
> * O tamanho máximo de um Ativo que pode ser visualizado é de até 100 MB.
> * O tamanho máximo de arquivos XLS ou XLSX para visualizar é 20 MB.
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
* [Publish Assets para AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
