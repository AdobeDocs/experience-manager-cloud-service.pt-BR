---
title: Como compartilhar links com ativos?
description: Gere um link e compartilhe ativos com outras pessoas que não têm acesso ao aplicativo  [!DNL Assets view] .
exl-id: 7d7d488b-410b-4e90-bd10-4ffbb5fcec49
feature: Adobe Asset Link, Link Sharing
role: Admin
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 83%

---

# Compartilhar links para ativos {#share-links-assets}

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

O [!DNL Assets view] permite gerar um link e compartilhar ativos com participantes externos, que não têm acesso ao aplicativo [!DNL Assets view]. Você pode definir uma data de expiração para o link e, em seguida, compartilhá-la com outras pessoas usando o método de comunicação preferido, como email ou serviços de mensagens. Os recipients do link podem visualizar ativos e baixá-los.

## Gerar um link para ativos {#generate-link-for-assets}

Para gerar um link para um ativo ou uma pasta contendo ativos:

1. Selecione os ativos, as pastas ou ambos que contêm ativos e clique em **[!UICONTROL Compartilhar link]**.

1. Se desejar ajustá-lo, clique no ícone Calendário para definir uma data de expiração para o link usando o campo **[!UICONTROL Data de vencimento]**. Também é possível especificar uma data diretamente no formato `yyyy-mm-dd`. Por padrão, a data de expiração de um link é definida como 2 semanas a partir da data de compartilhamento.

1. Copie o link do campo **[!UICONTROL Compartilhar link]**.

   ![Opção de cortar e endireitar](assets/share-asset-link.png)

1. Clique em **[!UICONTROL Fechar]** e compartilhe o link por email ou outras ferramentas de colaboração.

## Acessar os ativos compartilhados {#access-shared-assets}

Após compartilhar o link público para os ativos, os destinatários podem clicar no link para visualizar ou baixar os ativos compartilhados em um navegador da Web, sem precisar fazer logon no [!DNL Assets view].

Clique no link, clique na pasta para navegar até o ativo e, em seguida, clique no ativo para visualizá-lo. Você pode optar por exibir os ativos compartilhados em uma Exibição de lista ou em uma Exibição de cartão.

Você pode passar o mouse sobre o ativo compartilhado ou a pasta de ativos compartilhados para selecionar o ativo ou baixá-lo.

Você também pode selecionar vários ativos e clicar em **[!UICONTROL Download]**. O [!DNL Assets view] baixa os ativos selecionados como um arquivo ZIP. O [!DNL Assets view] cria uma subpasta no arquivo ZIP pai, com o mesmo nome do ativo, para cada ativo que você seleciona para download.

Para baixar todos os ativos de uma só vez, alterne para a **[!UICONTROL Exibição de lista]**, clique em **[!UICONTROL Selecionar tudo]** e, em seguida, clique em **[!UICONTROL Download]**.

![Visualizar ativos compartilhados](assets/preview-shared-assets.png)

## Próximas etapas {#next-steps}

* [Assista a um vídeo sobre compartilhamento de links de ativos no modo de exibição do Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/link-sharing.html?lang=pt-BR)

* Forneça feedback sobre o produto usando a opção [!UICONTROL Feedback] disponível na interface de visualização do Assets

* Forneça feedback sobre a documentação usando as opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/pt-br?support-solution=General&amp;lang=pt-BR#support)
