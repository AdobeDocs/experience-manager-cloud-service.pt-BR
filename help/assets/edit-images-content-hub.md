---
title: Editar imagens no Content Hub usando o Adobe Express
description: Editar imagens no Content Hub usando o Adobe Express
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---

# Editar imagens no Content Hub {#edit-images-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

![Editar imagens no Content Hub usando o Adobe Express](assets/edit-images-content-hub.png)

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

O Content Hub permite criar novo conteúdo com o Adobe Express. Você pode editar o conteúdo existente com ferramentas fáceis de usar, produzir variações na marca com modelos e elementos da marca e criar novo conteúdo com os recursos mais recentes da GenAI da Adobe Firefly.

## Pré-requisitos {#prereqs-edit-image-content-hub}

Direitos de acesso ao Adobe Express e [usuários do Content Hub com direitos de remixar ativos para novas variações](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets) podem editar imagens usando o Content Hub.

>[!NOTE]
>
>Você pode editar imagens de tipos de arquivos PNG e JPG/JPEG usando o [!DNL Adobe Express].

## Edição de imagens usando o [!DNL Adobe Express] {#edit-images-using-content-hub}

Para editar imagens usando o Content Hub:

1. Clique em **[!DNL Open in Adobe Express]**, disponível no cartão de ativos da imagem que você precisa editar. Como alternativa, clique na imagem para abrir seus detalhes e clique no logotipo [!DNL Adobe Express]. O editor incorporado do Adobe Express é carregado sem sair do Content Hub.

   Você pode aproveitar a funcionalidade [!DNL Adobe Express] para executar todas as ações relacionadas à edição de imagens, como [redimensionar imagem](https://helpx.adobe.com/express/using/resize-image.html), [remover ou alterar a cor de fundo](https://helpx.adobe.com/express/using/remove-background.html), [recortar imagem](https://helpx.adobe.com/express/using/crop-image.html), combinar a imagem com a imagem ou o texto gerado pela IA e muito mais.

1. Faça as modificações e clique em **[!UICONTROL Salvar]** para salvar o ativo editado em um dos tipos de formato:

   * **[!UICONTROL PNG]** (usado como um formato de imagem de boa qualidade)
   * **[!UICONTROL JPG]** (adequado para arquivos pequenos)
   * **[!UICONTROL PDF]** (adequado para documentos)

   ![Salvamento de imagens com o Adobe Express](assets/adobe-express-save-as.png)

1. Especifique um nome para o ativo no campo **[!UICONTROL Salvar como]**.

1. Especifique o nome da campanha para seu ativo usando o campo **[!UICONTROL Nome da campanha]**. Você pode usar um nome existente ou criar um novo. À medida que você digita o nome, a Content Hub fornece mais opções. <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   Como prática recomendada, a Adobe recomenda especificar valores no restante dos campos, bem como criar uma experiência de pesquisa aprimorada para os ativos carregados.

1. [Opcional] Defina valores para os campos **[!UICONTROL Palavras-chave]**, **[!UICONTROL Canais]**, **[!UICONTROL Período]** e **[!UICONTROL Região]**. Marcar e agrupar ativos por palavras-chave, canais e localização permite que todos que usam o conteúdo aprovado da empresa encontrem esses ativos e os mantenham organizados.

1. Clique em **[!UICONTROL Salvar como novo ativo]** para salvar o ativo.

Os administradores também podem configurar os campos obrigatórios e opcionais exibidos ao adicionar ativos ao Content Hub, como nome da campanha, palavras-chave, canais e assim por diante. Para obter mais informações, consulte [Configurar a interface do usuário do Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).
