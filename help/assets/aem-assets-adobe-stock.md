---
title: Gerenciar [!DNL Adobe Stock] ativos [!DNL Adobe Experience Manager Assets].
description: Pesquise, busque, licencie e [!DNL Adobe Stock] gerencie ativos de dentro [!DNL Adobe Experience Manager]. Use os ativos licenciados como qualquer outro ativo digital.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 453a8459e042f57820c10fb90f30c2016aa0f5d0
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---


# Usar [!DNL Adobe Stock] ativos em [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

As organizações podem integrar seus planos [!DNL Adobe Stock] corporativos [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos criativos e de marketing, com os poderosos recursos de gerenciamento de ativos da [!DNL Experience Manager].

[!DNL Adobe Stock]O serviço do fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties. [!DNL Experience Manager] os usuários podem localizar, pré-visualização e licenciar rapidamente [!DNL Adobe Stock] ativos salvos em [!DNL Experience Manager], sem sair da [!DNL Experience Manager] interface.

## Integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Para permitir a comunicação entre [!DNL Experience Manager] e [!DNL Adobe Stock], crie uma configuração IMS e uma [!DNL Adobe Stock] configuração em [!DNL Experience Manager].

>[!NOTE]
>
>Somente [!DNL Experience Manager] administradores e [!DNL Admin Console] administradores de uma organização podem executar a integração, pois ela requer privilégios de administrador.

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Clique em **[!UICONTROL Criar]** e selecione **[!UICONTROL Solução da nuvem]** > **[!UICONTROL Adobe Stock]**.
1. Reutilize um certificado existente ou selecione **[!UICONTROL Criar novo certificado]**.
1. Clique em **[!UICONTROL Criar certificado]**. Depois de criada, baixe a chave pública. Clique em **[!UICONTROL Avançar]**.
1. Adicione a chave pública baixada à sua conta [!DNL Adobe Developer Console] de serviço. Clique em **[!UICONTROL Avançar]**. Deixe a tela Configuração  de conta técnica Adobe IMS aberta para fornecer os valores em breve.
1. Acesse o Console [do desenvolvedor do](https://console.adobe.io)Adobe. Certifique-se de que sua conta tenha permissões de administrador para a organização para a qual a integração é necessária.
1. Clique em **[!UICONTROL Criar novo projeto]** e em **[!UICONTROL Adicionar API]**. Selecione **[!UICONTROL Adobe Stock]** na lista de APIs disponíveis para você. Selecione [!UICONTROL OAUTH 2.0 Web]. Configure e copie os vários valores apresentados.
1. In [!DNL Experience Manager] provide the values in the fields titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. Consulte start [rápido de autenticação](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)JWT para obter informações detalhadas sobre esses valores.

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Criar [!DNL Adobe Stock] configuração em [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Clique em **[!UICONTROL Criar]** para criar uma configuração e associá-la à sua Configuração IMS existente. Selecione `PROD` o parâmetro ambiente.
1. No campo Caminho **[!UICONTROL dos ativos]** licenciados, deixe um local como está. Não altere o local onde deseja armazenar os [!DNL Adobe Stock] ativos.
1. Conclua a criação adicionando todas as propriedades necessárias. Clique em **[!UICONTROL Salvar e fechar]**.
1. Adicione [!DNL Experience Manager] usuários ou grupos que podem licenciar os ativos.

>[!NOTE]
>
>Se houver várias [!DNL Adobe Stock] configurações, selecione a configuração desejada no painel Preferências do usuário. Para acessar o painel a partir do home page do Experience Manager, clique no ícone do usuário e, em seguida, clique em Preferências **** do usuário > Configuração **[!UICONTROL do]** estoque).

## Usar e gerenciar [!DNL Adobe Stock] ativos em [!DNL Experience Manager] {#usemanage}

Usando esse recurso, as organizações podem permitir que seus usuários trabalhem usando [!DNL Adobe Stock] ativos em [!DNL Experience Manager Assets]. Na interface do [!DNL Experience Manager] usuário, os usuários podem pesquisar [!DNL Adobe Stock] ativos e licenciar os ativos necessários.

Quando um [!DNL Adobe Stock] ativo é licenciado em [!DNL Experience Manager], ele pode ser usado e gerenciado como um ativo comum. Em [!DNL Experience Manager], os usuários podem pesquisar e pré-visualização os ativos; copiar e publicar os ativos; compartilhar os ativos em [!DNL Brand Portal]; acessar e usar os ativos por meio do aplicativo [!DNL Experience Manager] desktop; e assim por diante.

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

### Localizar ativos {#find-assets}

Seus [!DNL Experience Manager] usuários podem pesquisar ativos em ambos [!DNL Experience Manager] e [!DNL Adobe Stock]. Quando o local de pesquisa não estiver limitado a [!DNL Adobe Stock], os resultados da pesquisa de [!DNL Experience Manager] e [!DNL Adobe Stock] serão exibidos.

* Para pesquisar por [!DNL Adobe Stock] ativos, clique em **[!UICONTROL Navegação]** > **[!UICONTROL Ativos]** > **[!UICONTROL Pesquisar no Adobe Stock]**.

* Para pesquisar ativos [!DNL Adobe Stock] e [!DNL Experience Manager Assets], clique em pesquisar ![pesquisa](assets/do-not-localize/search_icon.png).

Como alternativa, digite um start `Location: Adobe Stock` na barra de pesquisa para selecionar [!DNL Adobe Stock] ativos. [!DNL Experience Manager] oferta os recursos de filtragem avançada nos ativos pesquisados, permitindo que os usuários façam rapidamente o logon zero nos ativos necessários usando filtros, como tipos de ativos suportados, orientação de imagem e estado licenciado.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] os ativos são buscados e armazenados no [!DNL Experience Manager] repositório somente depois que um usuário [salva um ativo](/help/assets/aem-assets-adobe-stock.md#saveassets) ou [licencia e salva um ativo](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Pesquisar filtros no Experience Manager e ativos Adobe Stock destacados nos resultados da pesquisa](assets/aem-search-filters2.jpg)

*Figura: Pesquise filtros em[!DNL Experience Manager]e[!DNL Adobe Stock]ativos destacados nos resultados da pesquisa.*

### Salve e visualização os ativos necessários {#saveassets}

Selecione um ativo no qual deseja salvar [!DNL Experience Manager]. Clique em [!UICONTROL Salvar] na barra de ferramentas na parte superior e forneça o nome e o local do ativo. Os ativos não licenciados são salvos localmente com uma marca d&#39;água.

Na próxima vez que você pesquisar ativos, os ativos salvos serão realçados com um selo, para indicar que tais ativos estão disponíveis em [!DNL Experience Manager Assets].

>[!NOTE]
>
>Os ativos adicionados recentemente exibem um novo selo em vez de um selo licenciado.

### Ativos da licença {#licenseassets}

Os usuários podem licenciar [!DNL Adobe Stock] ativos usando a cota de seu plano de [!DNL Adobe Stock] empresa. Quando você licencia um ativo, ele é salvo sem uma marca d&#39;água e está disponível para pesquisa e uso no [!DNL Experience Manager Assets].

![Caixa de diálogo para licenciar e salvar ativos Adobe Stock nos Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figura: Caixa de diálogo para licenciar e salvar[!DNL Adobe Stock]ativos em[!DNL Experience Manager Assets].*

### Acessar metadados e propriedades de ativos {#access-metadata-and-asset-properties}

Os usuários podem acessar e pré-visualização os metadados, incluindo as propriedades de [!DNL Adobe Stock] metadados dos ativos salvos em [!DNL Experience Manager]e adicionar Referências **[!UICONTROL de]** licença para um ativo. No entanto, as atualizações para referência de licença não são sincronizadas entre [!DNL Experience Manager] e o [!DNL Adobe Stock] site.

Os usuários podem ver as propriedades dos ativos licenciados e não licenciados.

![Visualização e acesso a metadados e referências de licença de ativos salvos](assets/metadata_properties.jpg)

*Figura: Visualização e acesso metadados e referências de licença de ativos salvos.*

## Limitações conhecidas {#known-limitations}

* **O aviso de imagem editorial não é exibido**: Ao licenciar uma imagem, os usuários não poderão verificar se uma imagem é Somente para uso editorial. Para evitar um possível uso indevido, os administradores podem desativar o acesso a ativos editoriais do Admin Console.

* **O tipo de licença incorreto é exibido**: É possível que um tipo de licença incorreto seja exibido em [!DNL Experience Manager] um ativo. Os usuários podem fazer logon no [!DNL Adobe Stock] site para ver o tipo de licença.

* **Campos de referência e metadados não são sincronizados**: Quando um usuário atualiza um campo de referência de licença, as informações de referência de licença são atualizadas no [!DNL Experience Manager] site, mas não no [!DNL Adobe Stock] . Da mesma forma, se o usuário atualizar os campos de referência no [!DNL Adobe Stock] site, as atualizações não serão sincronizadas no [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial em vídeo sobre como usar ativos Adobe Stock com ativos Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Ajuda do plano corporativo Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Perguntas frequentes sobre a Adobe Stock](https://helpx.adobe.com/stock/faq.html)

