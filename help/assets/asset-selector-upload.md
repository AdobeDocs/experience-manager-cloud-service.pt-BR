---
title: Seletor de ativos para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Use o Seletor de ativos para pesquisar, localizar e recuperar metadados e representações de ativos no aplicativo.
role: Admin,User
exl-id: d6ff601c-3111-421a-9a94-cc524ce7e432
source-git-commit: f9f5b2a25933e059cceacf2ba69e23d528858d4b
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---

# Fazer upload de arquivos e pastas para o Seletor de ativo {#upload-files-folders}

Você pode fazer upload de arquivos ou pastas para o Seletor de ativos no seu sistema de arquivos local. Para carregar arquivos usando o sistema de arquivos local, geralmente é necessário usar um recurso de upload fornecido por um aplicativo de micro front-end do Seletor de ativos.

## Fazer upload de ativos do sistema de arquivos local {#basic-upload}

Para adicionar ativos ao Seletor de ativos, execute as seguintes etapas:

1. Se você estiver usando a exibição do painel, vá para reticências e clique em ![ícone de carregamento](assets/upload-icon.svg) **[!UICONTROL Carregar]**. Por outro lado, clique no ![ícone de carregamento](assets/upload-icon.svg) **[!UICONTROL Carregar]** no canto superior direito em caso de exibição modal. A tela [!UICONTROL Carregar Assets] é exibida.

   ![Carregar ativos no Seletor de ativos](assets/upload-assets.png)

   Além disso, na seção **[!UICONTROL Arraste arquivos ou pastas aqui]**, você pode arrastar os ativos do sistema de arquivos local ou clicar em **[!UICONTROL Procurar]** para selecionar manualmente os arquivos ou pastas disponíveis no sistema de arquivos local. Essa lista de arquivos que fazem parte do upload está disponível como uma lista.

   ![Carregar ativos básicos no Seletor de ativos](assets/basic-upload.png)

   Também é possível visualizar as imagens selecionadas usando as miniaturas e clicar no ícone X para remover qualquer imagem específica da lista. O ícone X é exibido somente quando você passa o mouse sobre o nome ou o tamanho da imagem. Você também pode clicar em **[!UICONTROL Remover tudo]** para excluir todos os itens da lista de carregamento.

1. Para concluir o processo de carregamento, clique em **[!UICONTROL Carregar]**. Os ativos carregados são exibidos. Consulte [carregamento básico](/help/assets/asset-selector-customization.md#basic-upload) para obter o código configurável.

## Fazer upload de ativos com metadados {#upload-assets-with-metadata}

Você pode adicionar metadados aos ativos enquanto faz o upload deles imediatamente em seu aplicativo. Os metadados incluem vários campos, como linha de assunto da empresa, detalhes do produto, campanha e assim por diante. Para fazer isso, a propriedade `metadataSchema` é usada. Vá para [propriedades do seletor de ativos](/help/assets/asset-selector-properties.md) para saber mais sobre a propriedade `metadataSchema`.

Consulte [carregar com metadados](/help/assets/asset-selector-customization.md#upload-with-metadata) para obter o trecho de código necessário para a configuração.

![carregar ativos com metadados](assets/upload-with-metadata.png)

1. Defina o nome do upload usando o campo **[!UICONTROL Nome da campanha]**. Você pode usar um nome existente ou criar um novo. Ao digitar o nome, o Seletor de ativos fornece mais opções.

   Como prática recomendada, o Adobe recomenda especificar valores no restante dos campos, bem como criar uma experiência de pesquisa aprimorada para os ativos carregados.

1. Da mesma forma, defina valores para os campos **[!UICONTROL Palavras-chave]**, **[!UICONTROL Canais]**, **[!UICONTROL Cronograma]** e **[!UICONTROL Região]**. Marcar e agrupar ativos por palavras-chave, canais e localização permite que todos que usam o conteúdo aprovado da empresa encontrem esses ativos e os mantenham organizados.

1. Clique em **[!UICONTROL Carregar]** para carregar ativos no Seletor de ativos. A caixa de confirmação [!UICONTROL Detalhes da revisão] é exibida. Clique em [!UICONTROL Continuar].

1. O Assets inicia o upload. Clique em [!UICONTROL Novo carregamento] para reiniciar o procedimento de carregamento. Clique em [!UICONTROL Concluído] para concluir o carregamento.


## Upload personalizado {#customize-upload}

O Seletor de ativos permite adicionar um formulário de upload personalizado. Há várias personalizações disponíveis. Por exemplo, a propriedade [hideUploadButton](/help/assets/asset-selector-properties.md) permite ocultar o botão de carregamento mostrado por padrão no aplicativo. Em vez disso, você pode personalizá-lo para renderizar fora do aplicativo MFE, de acordo com o requisito. Consulte [upload personalizado](/help/assets/asset-selector-customization.md#customized-upload) para obter a configuração.

![Upload personalizado](assets/customized-upload.png)
