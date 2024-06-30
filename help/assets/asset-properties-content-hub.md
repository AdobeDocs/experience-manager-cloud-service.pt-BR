---
title: Propriedades do ativo no [!DNL the Content Hub]
description: Saiba como visualizar e gerenciar propriedades de ativos no [!DNL Content Hub]
role: User
source-git-commit: 5a968440c8841abe7af2c81c4af12258b7e4547f
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 8%

---


# Gerenciar propriedades de ativos no Content Hub {#asset-properties}

![Imagem do banner de metadados](assets/metadata-banner-image.png)

[!DNL The Content Hub] O permite visualizar informações sobre o ativo que é essencial para a distribuição eficiente do ativo. É a coleção de todos os dados disponíveis para um ativo.

A visualização de propriedades de ativos ajuda a categorizar os ativos e é útil à medida que a quantidade de informações digitais cresce. É possível gerenciar algumas centenas de arquivos com base apenas nos nomes de arquivo, miniaturas e memória. No entanto, essa abordagem não é escalável quando o número de pessoas envolvidas e o número de ativos gerenciados aumentam. Além disso, o valor de um ativo digital cresce à medida que o ativo se torna:

* Mais acessível — os sistemas e usuários podem encontrá-lo facilmente.
* Mais fácil de gerenciar — é possível encontrar ativos com o mesmo conjunto de propriedades facilmente e aplicar alterações a eles.
* Completo — o ativo carrega mais informações e contexto.

## Pré-requisitos {#prerequisites}

[Usuários do Content Hub](deploy-content-hub.md#onboard-content-hub-users) O pode executar as ações mencionadas neste artigo.

## Exibir propriedades de um ativo {#properties-ui}

Antes de usar, compartilhar ou baixar um ativo, é possível visualizá-lo mais detalhadamente. O recurso de visualização permite exibir não apenas as imagens, mas alguns outros tipos de ativos compatíveis também. Você pode não apenas visualizar o ativo, mas também visualizar suas informações detalhadas e realizar outras ações. Para exibir informações de um ativo, navegue até o ativo ou [pesquisa](search-assets.md) o ativo e, em seguida, clique no ativo para abrir suas propriedades. A figura a seguir demonstra os campos disponíveis em uma página de propriedades de ativos:

![Propriedades de uma interface do usuário do ativo](assets/properties-ui.png)

* **R:** Título de um ativo
* **B:** Porcentagem de zoom ou ativo de visualização mais próximo ao aumentar ou diminuir o zoom
* **C:** Desfazer zoom para a porcentagem selecionada anteriormente
* **D:** Prosseguir para o ativo anterior ou seguinte
* **E:** Contagem de Assets
* **F:** Baixar o ativo
* **G:** Editar ativo usando [!DNL Adobe Express]
* **A:** Recolher ou visualizar informações de um ativo
* **I:** Compartilhar o ativo
* **J:** Adicionar ativo a [!DNL Collection]
* **K:** Fechar tela de visualização
* **L:** Informações de um ativo que incluem título, formato, tamanho, resolução, tags, tags de cor e tags inteligentes.

## Formatos compatíveis {#supported-formats}

A tabela a seguir demonstra os formatos de arquivo compatíveis com o [!DNL the Content Hub]:

<table> 
    <tbody>
     <tr>
      <th><strong>Tipo de arquivo</strong></th>
      <th><strong>Formatos compatíveis</strong></th>
     </tr>
     <tr>
      <td>Imagem</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL SVG]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Vídeo</td>
      <td>
        <ul>
            <li>[!UICONTROL Quicktime]</li>  
            <li>[!UICONTROL MP4]</li> 
        </ul>
      </td>
     </tr>
      <tr>
      <td>Documento</td>
      <td>
        <ul>
            <li>[!UICONTROL txt] (Simples)</li>  
            <li>[!UICONTROL Doc/Docx]</li> 
            <li>[!UICONTROL XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Mídia de impressão</td>
      <td>
        <ul>
            <li>[!UICONTROL PDF]</li>  
        </ul>
      </td>
     </tr>  
    </tbody>
   </table>

### Propriedades derivadas após fazer upload de um ativo {#derived-properties}

Depois de fazer upload de um ativo, a Content Hub deriva algumas propriedades que são geradas automaticamente. Veja a seguir uma lista de alguns deles:

* **Tamanho:** O tamanho demonstra o valor lógico de um ativo de acordo com suas dimensões. Esclarece o espaço que um ativo está ocupando em um repositório. [!DNL The Content Hub] suporta ativos de até 2 GB.

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **Tags inteligentes:** [!DNL The Content Hub] O usa os serviços de conteúdo inteligente da Adobe Sensei para treinar ativos usando o algoritmo de reconhecimento na estrutura baseada em tags. Essa inteligência de conteúdo é usada para aplicar tags relevantes em um conjunto diferente de ativos. As Tags inteligentes aumentam a velocidade do conteúdo de seus projetos, ajudando você a encontrar ativos relevantes rapidamente. As tags inteligentes são um exemplo de informações de ativos que não estão contidas na imagem. [!DNL The Content Hub] O aplica tags inteligentes do automaticamente a ativos, por padrão.

* **Tags de cores:** [Tags de cores](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en) Ajudar a reconhecer um ativo usando cores identificadas automaticamente em um ativo usando os recursos de IA do Adobe Sensei.

* Data de upload

* Upload feito por

* Última modificação

* Última modificação por

Também há propriedades especificadas ao adicionar ativos ao Content Hub. Para obter mais informações, consulte [Adicionar ativos aprovados pela marca à Content Hub](upload-brand-approved-assets.md). Essas propriedades também são exibidas na página de propriedades do ativo.

Os administradores também podem configurar as propriedades exibidas para cada ativo. Para obter mais informações, consulte [Configurar a interface do usuário do Content Hub](configure-content-hub-ui-options.md#configure-asset-details-content-hub).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->

