---
title: Introdução ao uso do [!DNL Assets View]
description: Como acessar, experiência de logon, casos de uso com suporte e problemas conhecidos do [!DNL Assets View].
role: User, Leader
exl-id: 51ae6657-f6b5-44b0-a47f-451735ab0d01
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 79%

---

# Introdução à visualização de ativos {#assets-view-get-started}

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

<!-- TBD: Make links for these steps. -->

O gerenciamento de ativos digitais usando o [!DNL Assets View] requer apenas três etapas simples:

* **Etapa 1**: [Fazer upload](/help/assets/add-delete-assets-view.md) e [visualizar](/help/assets/navigate-assets-view.md) ativos.
* **Etapa 2**: [Pesquisar](/help/assets/search-assets-view.md) e [baixar](/help/assets/manage-organize-assets-view.md#download) ativos.
* **Etapa 3**: [Gerenciar e organizar](/help/assets/manage-organize-assets-view.md) os ativos.

Para usar o [!DNL Assets View], faça logon em [https://experience.adobe.com/#/assets](https://experience.adobe.com/#/assets). Ao fazer logon, selecione `Company or School Account`. Para receber acesso, entre em contato com o administrador da organização.

<!--In addition, more reference information that can be helpful is [understanding of the user interface](/help/assets/navigate-assets-view.md), [list of use cases](#use-cases), [supported file types](/help/assets/supported-file-formats-assets-view.md), and [known issues](/help/assets/release-notes.md#known-issues).
-->

## Acessar a visualização de ativos {#access-assets-view}

Consulte [Como acessar a visualização de ativos](/help/assets/assets-view-introduction.md#how-to-access-assets-view) para obter instruções detalhadas sobre como acessar essa visualização.

## Configurar o [!DNL Assets View] {#configuration}

Para abrir as preferências, clique no avatar no canto superior direito da interface. Você pode alternar entre os temas claro e escuro nas preferências da solução.

Se fizer parte de organizações diferentes, também poderá alterar a organização e acessar suas contas em várias organizações.

Para alterar as [!UICONTROL Preferências da Experience Cloud], clique em [!UICONTROL Preferências].

![Preferência para alternar entre temas escuro e claro](assets/theme-change.png)

>[!NOTE]
>
>Se você navegar até o modo de exibição do Assets e vir uma mensagem `Network Error`, certifique-se de executar as instruções mencionadas no artigo [Configuração do CORS (Cross-Origin Resource Sharing)](/help/headless/deployment/cross-origin-resource-sharing.md).

## Casos de uso do [!DNL Assets View] {#use-cases}

As várias tarefas de gerenciamento de ativos digitais (DAM) que você pode realizar usando o [!DNL Assets View] estão listadas abaixo.

| Tarefas do usuário | Funcionalidade e informações práticas |
|-----|------|
| Procurar e exibir ativos | <ul> <li>[Navegar pelo repositório](/help/assets/navigate-assets-view.md#view-assets-and-details) </li> <li> [Visualizar um ativo](/help/assets/navigate-assets-view.md#preview-assets) <li> [Exibir representações de um ativo](/help/assets/add-delete-assets-view.md#renditions) </li> <li>[Exibir versões de um ativo](/help/assets/manage-organize-assets-view.md#view-versions)</li></ul> |
| Adicionar novos ativos | <ul> <li>[Fazer upload de novos ativos e pastas](/help/assets/add-delete-assets-view.md)</li> <li>[Monitorar o progresso do upload e gerenciar uploads](/help/assets/add-delete-assets-view.md#upload-progress)</li> <li>[Resolver duplicações](/help/assets/add-delete-assets-view.md)</li> </ul> |
| Atualizar ativos ou informações relacionadas | <ul> <li>[Editar imagens](/help/assets/edit-images-assets-view.md)</li> <li>[Criar versões](/help/assets/manage-organize-assets-view.md#create-versions) e [exibir versões](/help/assets/manage-organize-assets-view.md#view-versions)</li> <li>[Editar imagens](/help/assets/edit-images-assets-view.md)</li> </ul> |
| Editar ativos | <ul> <li>[Edições no navegador usando o Adobe Photoshop Express](/help/assets/edit-images-assets-view.md)</li> <li>[Recortar para um perfil de redes social](/help/assets/edit-images-assets-view.md#crop-straighten-images)</li> <li>[Exibir e gerenciar versões](/help/assets/manage-organize-assets-view.md#view-versions)</li></ul></ul> |
| Pesquisar ativos no repositório | <ul> <li>[Pesquisar em uma pasta específica](/help/assets/search-assets-view.md#refine-search-results)</li> <li>[Pesquisas salvas](/help/assets/search-assets-view.md#saved-search)</li> <li>[Pesquisar ativos visualizados recentemente](/help/assets/search-assets-view.md)</li> <li>[Pesquisa de texto completo](/help/assets/search-assets-view.md) |
| Baixar ativos | <ul> <li> [Pré-visualizar ativo](/help/assets/navigate-assets-view.md#preview-assets) </li> <li> [Baixar ativos](/help/assets/manage-organize-assets-view.md#download) <li> [Baixar representações](/help/assets/add-delete-assets-view.md#renditions) </li></ul> |
| Operações de metadados | <ul> <li>[Visualizar metadados detalhados](/help/assets/metadata-assets-view.md) </li> <li> [Atualizar metadados](/help/assets/metadata-assets-view.md#update-metadata)</li> <li> [Criar novo formulário de metadados](/help/assets/metadata-assets-view.md#metadata-forms) </li> </ul> |

## Próximas etapas {#next-steps}

* [Assista a um vídeo de introdução à visualização de ativos](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/getting-started.html?lang=pt-BR)

* Forneça feedback sobre o produto usando a opção [!UICONTROL Feedback], disponível na interface da visualização de ativos

* Forneça feedback sobre a documentação usando as opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/?support-solution=General&amp;lang=pt-BR#support)


<!--TBD: Merge the below rows in the table when the use cases are documented/available.

| How do I delete assets? | <ul> <li>[Delete assets](/help/assets/manage-organize.md)</li> <li>Recover deleted assets</li> <li>Permanently delete assets</li> </ul> |
| How do I share assets or find shared assets? | <ul> <li>Shared by me</li> <li>Shared with me</li> <li>Share for comments and review</li> <li>Unshare assets</li> </ul> |
| How do I collaborate with others and get my assets reviewed | <ul> <li>Share for review</li> <li>Provide comments. Resolve and filter comments</li> <li>Annotations on images</li> <li>Assign tasks to specific users and prioritize</li> </ul> |

-->

<!-- 

## ![feedback icon](assets/do-not-localize/feedback-icon.png) Provide product feedback {#provide-feedback}

Adobe welcomes feedback about the solution. To provide feedback without even switching your working application, use the [!UICONTROL Feedback] option in the user interface. It also lets you attach files such as screenshots or video recording of an issue.

  ![feedback option in the interface](assets/feedback-panel.png)

To provide feedback for documentation, click [!UICONTROL Edit this page] ![edit the page](assets/do-not-localize/edit-page.png) or [!UICONTROL Log an issue] ![create a GitHub issue](assets/do-not-localize/github-issue.png) from the right sidebar. You can do one of the following: 

* Make the content updates and submit a GitHub pull request.
* Create an issue or ticket in GitHub. Retain the automatically populated article name when creating an issue.

-->
<!--
>[!MORELIKETHIS]
>
>* [Understand the user interface](/help/assets/navigate-asssets-view.md).
>* [Release notes and known issues](/help/assets/release-notes.md).
>* [Supported file types](/help/assets/supported-file-formats.md).
-->
