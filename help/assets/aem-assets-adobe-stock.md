---
title: Gerencie  [!DNL Adobe Stock] ativos em [!DNL Assets].
description: Pesquise, busque, licencie e gerencie [!DNL Adobe Stock] ativos de dentro de [!DNL Adobe Experience Manager]. Use os ativos licenciados como qualquer outro ativo digital.
contentOwner: AG
feature: Search,Adobe Stock
role: Admin,User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 034899c2a717fafdc50cc269d6db3feb77d907c5
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 5%

---

# Use [!DNL Adobe Stock] ativos em [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

As empresas podem integrar o [!DNL Adobe Stock] plano corporativo com [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos criativos e de marketing, com os poderosos recursos de gerenciamento de ativos [!DNL Experience Manager].

[!DNL Adobe Stock]O serviço do fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos em 3D de alta qualidade e isentos de royalties. [!DNL Experience Manager] os usuários podem localizar, visualizar e licenciar rapidamente  [!DNL Adobe Stock] ativos que são salvos no  [!DNL Experience Manager], sem sair da  [!DNL Experience Manager] interface.

## Integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Para estabelecer a comunicação entre [!DNL Experience Manager] e [!DNL Adobe Stock], crie uma configuração IMS e uma configuração [!DNL Adobe Stock] em [!DNL Experience Manager].

>[!NOTE]
>
>Somente administradores [!DNL Experience Manager] e administradores [!DNL Admin Console] de uma organização podem executar a integração, pois ela requer privilégios de administrador.

### Criar uma configuração IMS {#create-an-ims-configuration}

1. Na interface do usuário [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**. Clique em **[!UICONTROL Criar]** e selecione **[!UICONTROL Solução da nuvem]** > **[!UICONTROL Adobe Stock]**.
1. Reutilize um certificado existente ou selecione **[!UICONTROL Criar novo certificado]**.
1. Clique em **[!UICONTROL Criar certificado]**. Depois de criada, baixe a chave pública. Clique em **[!UICONTROL Avançar]**. Deixe a tela [!UICONTROL Adobe IMS Technical Account Configuration] aberta para fornecer os valores necessários em breve.
1. Acesse [Console do Desenvolvedor do Adobe](https://console.adobe.io). Certifique-se de que sua conta tenha permissões de administrador para a organização para a qual a integração é necessária.
1. Clique em **[!UICONTROL Criar novo projeto]** e clique em **[!UICONTROL Adicionar API]**. Selecione **[!UICONTROL Adobe Stock]** na lista de APIs disponíveis para você. Selecione [!UICONTROL OAUTH 2.0 Web].
1. Forneça os valores **[!UICONTROL Default redirect URI]** e **[!UICONTROL Redirect URI pattern]**. Clique em **[!UICONTROL Salvar API configurada]**. Copie a ID gerada e o segredo.
1. Na tela [!UICONTROL Configuração de Conta Técnica do Adobe IMS], forneça os valores nas caixas intituladas **[!UICONTROL Título]**, **[!UICONTROL Servidor de Autorização]**, **[!UICONTROL Chave da API]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL Carga&lt;a11/ .]** Para obter informações detalhadas sobre esses valores, consulte [Início rápido da autenticação JWT](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Criar configuração [!DNL Adobe Stock] em [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. No [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Clique em **[!UICONTROL Criar]** para criar uma configuração e associá-la à sua Configuração IMS existente. Selecione `PROD` como o parâmetro de ambiente.
1. No campo **[!UICONTROL Caminho dos ativos licenciados]**, deixe um local como está. Não altere o local onde deseja armazenar os ativos [!DNL Adobe Stock].
1. Conclua a criação adicionando todas as propriedades necessárias. Clique em **[!UICONTROL Salvar e fechar]**.
1. Adicione [!DNL Experience Manager] usuários ou grupos que podem licenciar os ativos.

>[!NOTE]
>
>Se houver várias configurações [!DNL Adobe Stock], selecione a configuração desejada no painel Preferências do usuário. Para acessar o painel a partir da página inicial do Experience Manager, clique no ícone do usuário e em **[!UICONTROL Preferências do usuário]** > **[!UICONTROL Configuração do Stock]**.

## Usar e gerenciar [!DNL Adobe Stock] ativos em [!DNL Experience Manager] {#usemanage}

Usando esse recurso, os usuários da organização podem trabalhar usando [!DNL Adobe Stock] ativos em [!DNL Experience Manager Assets]. Na interface do usuário [!DNL Experience Manager], os usuários podem pesquisar [!DNL Adobe Stock] ativos e licenciar os ativos necessários.

Depois que um ativo [!DNL Adobe Stock] é licenciado em [!DNL Experience Manager], ele pode ser usado e gerenciado como um ativo típico. Em [!DNL Experience Manager], os usuários podem pesquisar e visualizar os ativos; copiar e publicar os ativos; compartilhar os ativos em [!DNL Brand Portal]; acessar e usar os ativos por meio do [!DNL Experience Manager] aplicativo de desktop; e assim por diante.

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

### Localizar ativos {#find-assets}

Seus usuários [!DNL Experience Manager] podem pesquisar ativos em ambos, [!DNL Experience Manager] e [!DNL Adobe Stock]. Quando o local de pesquisa não está limitado a [!DNL Adobe Stock], os resultados da pesquisa de [!DNL Experience Manager] e [!DNL Adobe Stock] são exibidos.

* Para pesquisar ativos [!DNL Adobe Stock], clique em **[!UICONTROL Navegação]** > **[!UICONTROL Ativos]** > **[!UICONTROL Pesquisar Adobe Stock]**.

* Para pesquisar ativos em [!DNL Adobe Stock] e [!DNL Experience Manager Assets], clique em pesquisar ![pesquisar](assets/do-not-localize/search_icon.png).

Como alternativa, comece a digitar `Location: Adobe Stock` na barra de pesquisa para selecionar [!DNL Adobe Stock] ativos. [!DNL Experience Manager] O oferece recursos de filtragem avançados nos ativos pesquisados, permitindo que os usuários entrem rapidamente nos ativos necessários usando filtros, como tipos de ativos compatíveis, orientação de imagem e estado licenciado.

>[!NOTE]
>
>Os ativos pesquisados a partir de [!DNL Adobe Stock] são exibidos apenas em [!DNL Experience Manager]. [!DNL Adobe Stock] os ativos são buscados e armazenados no  [!DNL Experience Manager] repositório somente depois que um usuário  [salva uma ](/help/assets/aem-assets-adobe-stock.md#saveassets) licença do ativo e  [salva um ativo](/help/assets/aem-assets-adobe-stock.md#licenseassets). Os ativos que já estão armazenados em [!DNL Experience Manager] são exibidos e destacados para facilitar a referência e o acesso. Além disso, os ativos [!DNL Stock] são salvos com alguns metadados adicionais para indicar a fonte como [!DNL Stock].

![Filtros de pesquisa no Experience Manager e ativos Adobe Stock destacados nos resultados de pesquisa](assets/aem-search-filters2.jpg)

*Figura: Pesquise filtros em  [!DNL Experience Manager] e  [!DNL Adobe Stock] ativos destacados nos resultados de pesquisa.*

### Salvar e exibir os ativos necessários {#saveassets}

Selecione um ativo que deseja salvar em [!DNL Experience Manager]. Clique em [!UICONTROL Save] na barra de ferramentas na parte superior e forneça o nome e o local do ativo. Os ativos não licenciados são salvos localmente com uma marca d&#39;água.

Na próxima vez que você pesquisar ativos, os ativos salvos serão destacados com um selo, para indicar que tais ativos estão disponíveis em [!DNL Experience Manager Assets].

>[!NOTE]
>
>Os ativos adicionados recentemente exibem um novo selo em vez do selo Licenciado .

### Ativos da licença {#licenseassets}

Os usuários podem licenciar [!DNL Adobe Stock] ativos usando a cota de seu [!DNL Adobe Stock] plano corporativo. Ao licenciar um ativo, ele é salvo sem uma marca d&#39;água e está disponível para pesquisa e uso em [!DNL Experience Manager Assets].

![Caixa de diálogo para licenciar e salvar ativos Adobe Stock no Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figura: Caixa de diálogo para licenciar e salvar  [!DNL Adobe Stock] ativos no  [!DNL Experience Manager Assets].*

### Acessar metadados e propriedades de ativos {#access-metadata-and-asset-properties}

Os usuários podem acessar e visualizar os metadados, incluindo as propriedades de metadados [!DNL Adobe Stock] dos ativos salvos em [!DNL Experience Manager], e adicionar **[!UICONTROL Referências de licença]** para um ativo. No entanto, as atualizações para a referência de licença não são sincronizadas entre o [!DNL Experience Manager] e o [!DNL Adobe Stock] site.

Os usuários podem ver as propriedades dos ativos licenciados e não licenciados.

![Exibir e acessar metadados e referências de licença de ativos salvos](assets/metadata_properties.jpg)

*Figura: Visualize e acesse metadados e referências de licença de ativos salvos.*

## Limitações conhecidas {#known-limitations}

* **O aviso de imagem editorial não é exibido**: Ao licenciar uma imagem, os usuários não podem verificar se uma imagem é Somente para uso editorial. Para evitar um possível uso indevido, os administradores podem desativar o acesso a ativos editoriais no Admin Console.

* **O tipo de licença incorreto é exibido**: É possível que um tipo de licença incorreto seja exibido no  [!DNL Experience Manager] para um ativo. Os usuários podem fazer logon no site [!DNL Adobe Stock] para visualizar o tipo de licença.

* **Os campos e metadados de referência não são sincronizados**: Quando um usuário atualiza um campo de referência de licença, as informações de referência da licença são atualizadas no,  [!DNL Experience Manager] mas não no  [!DNL Adobe Stock] site. Da mesma forma, se o usuário atualizar os campos de referência no site [!DNL Adobe Stock], as atualizações não serão sincronizadas em [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial em vídeo sobre o uso de ativos Adobe Stock com ativos Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Ajuda do plano corporativo Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Perguntas frequentes sobre o Adobe Stock](https://helpx.adobe.com/stock/faq.html)

