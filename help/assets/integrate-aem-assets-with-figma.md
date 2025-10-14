---
title: Integrar [!DNL AEM Assets] com [!DNL Figma].
description: Saiba como integrar o [!DNL AEM Assets] com o [!DNL Figma] para acessar e usar os ativos de sua organização no fluxo de trabalho de design do [!DNL Figma] .
hide: false
role: User
exl-id: 530561ca-497b-4331-a014-72c561e1ca84
source-git-commit: 3603a98dfee62db49f3201c8d75aa8eee4909cc1
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Integrar [!DNL AEM Assets] a [!DNL Figma]{#integrate-aem-assets-with-figma}

O [!DNL AEM Assets] integra-se nativamente ao [!DNL Figma], o que permite que os designers acessem diretamente os ativos armazenados no [!DNL AEM Assets] de dentro da interface do usuário do [!DNL Figma]. Você pode colocar conteúdo gerenciado em [!DNL AEM Assets] na tela [!DNL Figma] e depois salvar conteúdo novo ou editado no repositório [!DNL AEM Assets].

## Antes de começar{#prerequisites-for-aem-assets-and-figma-integration}

* A versão mínima necessária do AEM é `19149`.

* Você deve ter [!DNL AEM Assets] e [!DNL Figma] licenças válidas para integrar o [!DNL AEM Assets] ao [!DNL Figma].

## Acessar o [!UICONTROL Conector Assets do Adobe Experience Manager (AEM)]{#access-aem-assets-connector}

Execute as seguintes etapas para acessar o [!UICONTROL Conector Assets do Adobe Experience Manager (AEM)]:

1. Na home page do [!DNL Figma], clique em **[!UICONTROL Ações]** na barra de ferramentas, na parte inferior da tela, e procure [!DNL Adobe Experience Manager (AEM) Assets Connector] na barra de pesquisa disponível na caixa de diálogo.
1. Selecione [!DNL Adobe Experience Manager (AEM) Assets Connector] para exibir o painel [!DNL Adobe Experience Manager (AEM) Assets Connector]. [Importe [!DNL AEM] ativos para sua [!DNL Figma] tela](#import-aem-assets-into-figma-workflow) usando este painel.
   ![ações](/help/assets/assets/actions-on-figma.png)
Como alternativa, acesse o [[!DNL Adobe Experience Manager (AEM) Assets Connector]](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) disponível na comunidade [!DNL Figma], clique em **[!UICONTROL Abrir em...]**, selecione um arquivo recente ou crie um novo arquivo e clique em **[!UICONTROL Executar]** para acessar o painel [!DNL Adobe Experience Manager (AEM) Assets Connector].
   ![plugin-page-on-figma-community](/help/assets/assets/plugin-page-on-figma-community.png)

>[!NOTE]
>
> [Contate o Suporte da Adobe](https://helpx.adobe.com/br/contact.html) para obter ajuda se você vir uma mensagem de **[!UICONTROL Erro de Rede]** depois de fazer logon no ambiente [!DNL AEM].

## Importar [!DNL AEM] ativos para a tela [!DNL Figma]{#import-aem-assets-into-figma-workflow}

[Acesse o [!UICONTROL painel &#x200B;] do Assets do Adobe Experience Manager (AEM)](#access-aem-assets-connector) na interface de design do [!DNL Figma] e faça o seguinte:

1. Pesquise ativos no painel [!UICONTROL Conector do Assets do Adobe Experience Manager (AEM)]. Para obter mais informações, consulte [usando o Seletor de ativos](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector#using-asset-selector).

1. Arraste e solte o ativo na tela ou selecione o ativo e clique em **[!UICONTROL Selecionar]** para trazer o ativo para a tela.

1. Clique em ![três pontos](/help/assets/assets/three-dots.svg) no caminho da pasta para exibir todas as pastas pai e filho na hierarquia atual. Selecione uma pasta para navegar até esse local.
   ![três pontos](/help/assets/assets/assets-folder-structure.png)

Quando o design do Figma estiver pronto, você poderá [exportar o ativo para o repositório do AEM Assets](#export-figma-design-to-aem-assets-folder).

## Exportar ativos para o repositório [!DNL AEM Assets]{#export-figma-design-to-aem-assets-folder}

[Acesse o painel &#x200B;](#access-aem-assets-connector) do [!UICONTROL Conector Assets do Adobe Experience Manager (AEM)] na interface de design do [!DNL Figma] e execute as seguintes etapas para exportar seu design para o repositório do [!DNL AEM Assets]:

1. Navegue até a pasta de destino onde deseja salvar o design do [!DNL Figma]. Se você já estiver dentro de uma pasta, clique em Mais opções (![três pontos](/help/assets/assets/three-dots.svg)) no caminho da pasta para selecionar uma pasta de destino diferente.
1. Opcional: agrupe ativos na tela para selecioná-los como uma única unidade para fazer upload em sua pasta.
1. Clique em ![carregamento de arquivo](/help/assets/assets/upload-icon.svg) **[!UICONTROL Carregar]** para exibir a caixa de diálogo **[!UICONTROL Carregar ativo]**.
1. Na caixa de diálogo, especifique um nome de arquivo, escolha um formato de arquivo, selecione **[!UICONTROL Item Selecionado]** ou **[!UICONTROL Página]** e clique em **[!UICONTROL Carregar]** para carregar o ativo selecionado ou o design inteiro para a pasta de destino.
   ![carregar design de imagem](/help/assets/assets/upload-figma-design.png)

## Pontos importantes a observar{#Limitations-of-using-aem-assets-into-figma}

No momento, essa integração tem as seguintes limitações:

* Para importar ativos do [!DNL AEM] para o Figma, os formatos aceitos são **JPEG**, **PNG**.
* Para exportar designs do [!DNL Figma] para o [!DNL AEM Assets], os formatos com suporte são **PNG**, **PDF**, **JPG**, **SVG**.
