---
title: Renomear e renomear ativos em massa em  [!DNL Assets view]
description: Saiba como renomear ativos em massa usando a nova interface do usuário do Assets (visualização do Assets). Ele oferece a capacidade de renomear vários ativos de uma só vez.
role: User
exl-id: e041811b-0246-408f-9246-248da55f66a1
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 13%

---

# Renomear ativo ou pasta em [!DNL Assets view] {#rename-single-asset-or-folder}

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

A renomeação pode ajudar a organizar, categorizar e identificar melhor os ativos sem alterar seu conteúdo ou local. [!DNL Assets view] permite renomear o ativo ou pasta selecionada.

Execute as etapas abaixo para renomear um ativo ou uma pasta:

1. Localize o ativo ou pasta que deseja renomear.

1. Use uma das seguintes maneiras para renomear um ativo ou uma pasta:

   * Selecione o ativo ou pasta e clique em ![renomear ícone](assets/do-not-localize/rename-icon.png) **[!UICONTROL Renomear]** no menu superior.
   * Clique em mais opções `...` no ativo ou pasta e selecione **[!UICONTROL Renomear]**.
   * Clique no título de um ativo ou em uma pasta para renomeá-lo. Insira o novo texto na caixa de texto **Renomear ativo** e clique em **Salvar**. Esse recurso está disponível nas exibições em grade, galeria, cascata e lista.

## Renomear ativos alimentados por IA em massa {#rename-bulk-assets-using-ai}

[!DNL Assets view] permite renomear vários ativos de uma só vez usando IA. A funcionalidade de Renomeação em massa de IA só pode ser aplicada a arquivos, não a pastas. Você pode selecionar vários arquivos de uma vez e renomeá-los todos juntos.

Siga as etapas abaixo para renomear a massa de ativos de uma só vez usando prompts gerados por IA:

1. Selecione vários ativos e clique em **[!UICONTROL Renomear em massa]** no menu superior.

1. Adicione o prompt que descreve como você deseja renomear os ativos selecionados. Consulte [alguns exemplos ilustrando a Renomeação em Massa de IA](#examples-ai-bulk-rename).

1. Clique em **[!UICONTROL Executar]** para permitir que a IA renomeie os ativos como mencionado no prompt.

1. [Opcional] Clique em ![ícone desfazer](assets/do-not-localize/undo.svg) para reverter ou cancelar a última ação executada.

1. Verifique as alterações na coluna [!UICONTROL Nova visualização de nome] e clique em **[!UICONTROL Salvar]**.

   ![Renomear AI em massa](assets/ai-bulk-rename.png)

## Alguns exemplos ilustrando a Renomeação em massa de IA {#examples-ai-bulk-rename}

Veja a seguir alguns exemplos de como usar a IA para renomear ativos em massa com base em um prompt de IA:

* Prefixe com 00, 01 e assim por diante e sufixo com a data de hoje.
* Altere todos os arquivos para &#39;my-file&#39; e anexe um número incremental.
* Remova o prefixo e o sufixo, apenas mantenha a parte do meio do nome.
* Prefixe os arquivos com 001, 002, etc. e traduzir para inglês.

>[!VIDEO](https://video.tv.adobe.com/v/3440975)

>[!NOTE]
>
> * Não é possível converter emojis em texto.
> * Use um nome exclusivo para evitar mensagens de aviso ao renomear ativos. Embora você possa tentar novamente com um novo nome.
> * Também é possível converter caracteres Unicode ou não alfanuméricos em texto.

## Próximas etapas {#next-steps}

* [Assista a um vídeo sobre gerenciamento de formulários de metadados no modo de exibição do Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html?lang=pt-BR)

* Forneça feedback sobre o produto usando a opção [!UICONTROL Feedback] disponível na interface de visualização do Assets

* Forneça feedback sobre a documentação usando as opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/pt-br?support-solution=General&amp;lang=pt-BR#support)
