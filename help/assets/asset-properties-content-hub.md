---
title: Visualizar ativo e suas propriedades em  [!DNL the Content Hub]
description: Saiba como visualizar ativos e propriedades no [!DNL Content Hub]
role: User
exl-id: a85af980-4c51-4d30-9fad-afd16370e9db
source-git-commit: 44e9c1f016bfdad909d9e2aa1c9a301dcecd763b
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 5%

---

# Visualizar ativo e suas propriedades no Content Hub {#asset-properties}

![Imagem do banner de metadados](assets/metadata-banner-image.png)

O [!DNL The Content Hub] permite exibir informações sobre o ativo que são essenciais para uma distribuição eficiente do ativo. É a coleção de todos os dados disponíveis para um ativo.

A visualização de ativos e suas propriedades ajudam a categorizar os ativos e são úteis à medida que a quantidade de informações digitais cresce. É possível gerenciar algumas centenas de arquivos com base apenas nos nomes de arquivo, miniaturas e memória. No entanto, essa abordagem não é escalável quando o número de pessoas envolvidas e o número de ativos gerenciados aumentam. Além disso, o valor de um ativo digital cresce à medida que o ativo se torna:

* Mais acessível — os sistemas e usuários podem encontrá-lo facilmente.
* Mais fácil de agir - você tem informações completas sobre os recursos visuais dos ativos e informações relacionadas, para poder agir com mais rapidez e confiança.
* Completo — o ativo carrega mais informações e contexto.

## Pré-requisitos {#prerequisites}

[Usuários do Content Hub](deploy-content-hub.md#onboard-content-hub-users) podem executar as ações mencionadas neste artigo.

## Visualizar ativo e suas propriedades {#properties-ui}

Antes de usar, compartilhar ou baixar um ativo, é possível visualizá-lo mais detalhadamente. O recurso de visualização permite exibir não apenas as imagens, mas alguns outros tipos de ativos compatíveis também. Você pode não apenas visualizar o ativo, mas também visualizar suas informações detalhadas e realizar outras ações. Para exibir informações de um ativo, navegue até o ativo ou [pesquise](search-assets.md) o ativo e clique nele para abrir suas propriedades. A figura a seguir demonstra os campos disponíveis em uma página de propriedades de ativos:

![Propriedades de uma interface do usuário do ativo](assets/properties-ui.png)

* **A:** Título de um ativo
* **B:** Porcentagem de zoom ou ativo de visualização mais próxima ao aumentar ou diminuir o zoom
* **C:** Desfazer zoom até a porcentagem selecionada anteriormente
* **D:** Prosseguir para o ativo anterior ou seguinte
* **E:** Contagem de Assets
* **F:** Baixar o ativo
* **G:** Editar ativo usando [!DNL Adobe Express]
* **H:** Recolher ou visualizar informações de um ativo
* **I:** Compartilhar o ativo
* **J:** Adicionar ativo a [!DNL Collection]
* **K:** Fechar tela de visualização
* **L:** Informações de um ativo que inclui título, formato, tamanho, resolução, marcas, marcas de cor e marcas inteligentes.

## Formatos de ativos compatíveis {#supported-formats}

O [!DNL Content Hub] oferece suporte a todos os tipos e formatos de ativos aceitos pelo repositório [!DNL Assets] subjacente. A tabela a seguir lista os principais formatos de arquivo em [!DNL the Content Hub], que fornecem suporte adicional para a visualização de ativos visualmente:

<table> 
    <tbody>
     <tr>
      <th><strong>Tipo de arquivo</strong></th>
      <th><strong>Formatos compatíveis</strong></th>
     </tr>
     <tr>
        <td rowspan="3"> Imagem </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL JPEG]</td>
    </tr>
    <tr>
        <td>[!UICONTROL PNG]</td>
    </tr>
    <tr>
        <td rowspan="4"> Vídeo </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL Quicktime]</td>
    </tr>
    <tr>
        <td>[!UICONTROL MP4]</td>
    </tr>
    <tr>
        <td>[!UICONTROL MPEG]</td>
    </tr>
    <tr>
        <td rowspan="4"> Documento </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL txt] (Simples)</td>
    </tr>
    <tr>
        <td>[!UICONTROL Doc/Docx]</td>
    </tr>
    <tr>
        <td>[!UICONTROL XML]</td>
    </tr>
    <tr>
        <td rowspan="2"> Mídia de impressão </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL PDF]</td>
    </tr>
    </tbody>
</table>

### Propriedades derivadas {#derived-properties}

Algumas propriedades dos ativos exibidos em [!DNL Content Hub] são derivadas, ou geradas automaticamente, quando os ativos são carregados para [!DNL Assets] e depois aprovados para disponibilidade em [!DNL Content Hub]. Veja a seguir uma lista de alguns deles:

* **Tamanho:** Tamanho representa o tamanho do binário de ativo armazenado no repositório subjacente.

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **Tags inteligentes:** o [!DNL The Content Hub] usa os serviços de conteúdo inteligente da Adobe AI para treinar ativos usando o algoritmo de reconhecimento na estrutura baseada em tags. Essa inteligência de conteúdo é usada para aplicar tags relevantes em um conjunto diferente de ativos. As Tags inteligentes aumentam a velocidade do conteúdo de seus projetos, ajudando você a encontrar ativos relevantes rapidamente. As tags inteligentes são um exemplo de informações de ativos que não estão contidas na imagem. O [!DNL Experience Manager Assets] aplica tags inteligentes automaticamente a ativos, por padrão.

* **Marcas de cores:** [Marcas de cores](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=pt-BR) ajudam a reconhecer um ativo usando cores identificadas automaticamente em um ativo por meio dos recursos de IA da Adobe.

* Data de upload

* Upload feito por

* Última modificação

* Última modificação por

Também há propriedades especificadas ao adicionar ativos ao Content Hub. Para obter mais informações, consulte [Adicionar ativos aprovados pela marca à Content Hub](upload-brand-approved-assets.md). Essas propriedades também são exibidas na página de propriedades do ativo.

Os administradores também podem configurar as propriedades, que são exibidas para cada ativo:

* Na interface de visualização de ativos: consulte [Configurar a interface de usuário do Content Hub](configure-content-hub-ui-options.md#configure-asset-details-content-hub).
* Em cartões de ativos em resultados de pesquisa ou coleções: consulte [Configurar a interface de usuário do Content Hub](configure-content-hub-ui-options.md#asset-card).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->

## Perguntas frequentes {#faqs-asset-properties-content-hub}

### Por que você visualiza ativos e suas propriedades no AEM Assets Content Hub?

A visualização de ativos e suas propriedades no Content Hub permite que os usuários visualizem detalhadamente os detalhes do ativo, que são essenciais para a distribuição e o gerenciamento eficientes de ativos. À medida que as informações digitais crescem, simplesmente confiar nos nomes de arquivo e nas miniaturas torna-se indimensionável. A exibição de propriedades detalhadas ajuda a categorizar ativos, torna-os mais acessíveis, fácil de usar e garante que as informações estejam completas para todos os usuários.

### Como posso visualizar e interagir com as propriedades de um ativo no AEM Assets Content Hub?

Para visualizar as propriedades de um ativo no Content Hub, navegue até o ativo ou pesquise por ele e clique nele para abrir a página de propriedades dele. Aqui, é possível aumentar ou diminuir o zoom na visualização, desfazer o zoom, mover para ativos anteriores ou seguintes, baixar o ativo, editá-lo com o Adobe Express, adicioná-lo a uma coleção ou fechar a visualização. A página de propriedades exibe informações detalhadas, como título, formato, tamanho, resolução, tags, tags de cor e tags inteligentes.

### O que são propriedades derivadas no AEM Assets Content Hub e como elas são geradas?

As propriedades derivadas no Content Hub são geradas automaticamente quando os ativos são carregados e aprovados. Os exemplos incluem o tamanho do ativo, as tags inteligentes e as tags de cores. As tags inteligentes usam os serviços de conteúdo inteligente da Adobe AI para reconhecer e aplicar automaticamente tags relevantes, melhorando a descoberta de ativos. As tags de cor também são identificadas automaticamente usando IA, ajudando os usuários a reconhecer ativos por suas cores de destaque.

### Os administradores podem personalizar quais propriedades de ativos estão visíveis no Content Hub?

Sim, os administradores têm a capacidade de configurar quais propriedades são exibidas para cada ativo no Content Hub. Isso pode ser feito para a interface do usuário de visualização de ativos e cartões de ativos em resultados de pesquisa ou coleções, garantindo que os usuários vejam as informações mais relevantes com base nos requisitos.

### Quais são os formatos de arquivo compatíveis com a visualização de ativos?

Os formatos de arquivo compatíveis incluem JPEG e PNG para imagens, Quicktime, MP4 e MPEG para vídeos, TXT, DOC/DOCX e XML para documentos, e PDF para mídia de impressão.


