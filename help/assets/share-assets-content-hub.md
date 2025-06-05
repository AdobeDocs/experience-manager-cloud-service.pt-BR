---
title: Compartilhar Assets em  [!DNL the Content Hub]
description: Compartilhar Assets em  [!DNL the Content Hub]
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 0e66b355d09e2fd2c4c8a5ddacc9b2d033b41bf2
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 5%

---

# Compartilhar ativos na Content Hub {#search-assets-as-a-link}

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
            <a href="/help/assets/search-best-practices.md"><b>Práticas recomendadas de pesquisa</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas para metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de conteúdo</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos da OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentação do AEM Assets para desenvolvedores</b></a>
        </td>
    </tr>
</table>

![Compartilhar imagem do banner de ativos](assets/share-assets-banner.png)

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Crie um link para ativos selecionados para compartilhá-los facilmente com outras pessoas. Como usuário autorizado do [!DNL Content Hub], selecione um ou mais ativos disponíveis no ambiente [!DNL Content Hub], gere um link e envie-o para outros usuários públicos ou privados.

## Pré-requisitos {#prerequisites}

[Os usuários do Content Hub](deploy-content-hub.md#onboard-content-hub-users) podem criar um link para os ativos selecionados e compartilhá-lo com outros usuários.

## Compartilhar ativos {#share-assets}

Para compartilhar um ou mais ativos com usuários privados ou públicos, execute as seguintes etapas:
1. Navegue até a página inicial do [!DNL Content Hub], selecione um ou mais ativos e clique em ![Compartilhar](/help/assets/assets/share.svg) **[!UICONTROL Compartilhar]** para exibir um único ativo selecionado ou uma lista de vários ativos selecionados na caixa de diálogo **[!UICONTROL Compartilhar ativos]**.
Você também pode selecionar e compartilhar ativos disponíveis em ![coleções](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL Coleções]**.
1. Exiba um ativo ou revise a lista de ativos disponíveis na caixa de diálogo **[!UICONTROL Compartilhar ativos]**. Clique em ![desmarcar](/help/assets/assets/Close.svg) ao lado de um ativo para desmarcá-lo da lista.
1. Selecione um **[!UICONTROL período de expiração]** e clique em **[!UICONTROL Gerar link privado]** para gerar um link para compartilhar com usuários privados. Os usuários privados fazem logon no ambiente [!DNL Content Hub] para acessar a página de ativos compartilhados.
   ![link privado e público](/help/assets/assets/private-and-public-link.png)
Habilite o **[!UICONTROL Link Público]**, selecione um **[!UICONTROL período de expiração]** e clique em **[!UICONTROL Gerar Link Público]** para gerar um link a ser compartilhado com usuários públicos. Usuários públicos, como convidados, acessam a página de ativos compartilhados sem entrar no [!DNL Content Hub].
   ![link privado e público](/help/assets/assets/public-and-private-link.png)

   >[!NOTE]
   > 
   > [Habilite o compartilhamento de link público na página de configuração](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing) para exibir a opção **[!UICONTROL Link público]** na caixa de diálogo **[!UICONTROL Compartilhar ativos]**.

## Compartilhar um ativo da página de visualização {#share-asset-from-preview-page}

Execute as seguintes etapas para compartilhar um ativo ao pré-visualizá-lo:

1. Navegue até a página inicial do [!DNL Content Hub] e clique na miniatura do ativo para visualizar o ativo e exibir as opções de menu no painel direito da caixa de diálogo.
1. Selecione ![compartilhar](/help/assets/assets/share.svg) para exibir o painel **[!UICONTROL Compartilhar]**.
   ![compartilhar ativo ao visualizá-lo](/help/assets/assets/share-assets-from-share-panel.png)
1. Siga a etapa 3 na seção [compartilhar ativos](#share-assets) para gerar e compartilhar o link de ativos (Privado ou público) neste painel **[!UICONTROL Compartilhar]**.

## Acessar os ativos compartilhados {#access-shared-assets}

Acesse a página de ativos compartilhados por meio do link e faça o seguinte:

* Selecione um ou mais ativos e clique em ![Baixar](/help/assets/assets/download-icon.svg) **[!UICONTROL Baixar]** para selecionar as representações **[!UICONTROL Original]**, **[!UICONTROL Estático]** ou ambas das opções de download disponíveis.
  ![](/help/assets/assets/download-shared-assets.png)
* Clique na miniatura do ativo para ver os metadados do ativo.
* Na página de ativos compartilhados ([acessada por meio de um link privado](#share-assets)), clique em uma miniatura de ativo e selecione ![baixar](/help/assets/assets/download-icon.svg) para selecionar e exibir as representações dinâmicas disponíveis do ativo no painel **[!UICONTROL Baixar]** antes de selecioná-las e baixá-las.
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)





