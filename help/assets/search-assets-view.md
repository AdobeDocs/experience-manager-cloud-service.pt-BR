---
title: Saiba como pesquisar e descobrir ativos no [!DNL Assets view]?
description: Saiba como pesquisar e descobrir ativos na visualização do AEM Assets. A eficiente funcionalidade de pesquisa permite descobrir rapidamente o ativo apropriado e ajuda a melhorar a velocidade do conteúdo.
role: User
exl-id: abfe6a91-1699-436f-8bf4-0d0bf2369f46
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: 32bc8ba2a7e7a783b3e816c78873c6a8c559c1a1
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 77%

---

# Pesquisar ativos no [!DNL Assets view] {#search-assets}

>[!CONTEXTUALHELP]
>id="assets_search"
>title="Pesquisar ativos"
>abstract="Pesquise por ativos especificando uma palavra-chave na barra de pesquisa ou filtrando ativos com base no status, tipo de arquivo, tipo MIME, tamanho, criação, modificação e datas de expiração. Também é possível aplicar filtros personalizados, além dos filtros padrão. Você pode salvar os resultados filtrados como uma Pesquisa salva ou uma Coleção inteligente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-assets-essentials/help/manage-collections.html?lang=pt-BR#manage-smart-collection" text="Criar coleções inteligentes"

O [!DNL Assets view] oferece uma pesquisa eficiente, que funciona por padrão. A pesquisa é abrangente, pois é uma pesquisa de texto completo. Essa eficiente funcionalidade de pesquisa permite descobrir rapidamente o ativo apropriado e ajuda a melhorar a velocidade do conteúdo. O [!DNL Assets view] fornece pesquisa de texto completo e até mesmo pesquisas por meio de metadados, como tags inteligentes, título, data de criação e direito autoral.

Para pesquisar ativos:

* Clique na caixa de pesquisa na parte superior da página. Por padrão, a pesquisa é feita na pasta em que você está navegando no momento. Siga uma das seguintes opções:

  ![caixa de pesquisa](assets/search-box.png)

   * Pesquise usando uma palavra-chave e, opcionalmente, altere a pasta. Pressione Return.

   * Comece a trabalhar com um ativo visualizado recentemente procurando diretamente por ele. Clique na caixa de pesquisa e selecione um ativo visualizado recentemente a partir das sugestões.

## Filtrar os resultados da pesquisa {#refine-search-results}

É possível refinar os resultados da pesquisa para localizar ativos relevantes aplicando vários filtros. Esses filtros, configurados por um administrador, são baseados em arquivos, pastas e coleções. Consulte [Personalizar Filtros De Pesquisa](custom-search-filters.md).

![Filtros de pesquisa](assets/filters-panel.gif)

Você pode filtrar os resultados da pesquisa com base nos seguintes parâmetros.

* Status do ativo: filtre os resultados da pesquisa usando um status de ativo `Approved`, `Rejected` ou `No Status`.
* Tipo de arquivo: filtre os resultados da pesquisa pelos tipos de arquivos compatíveis, ou seja, `Images`, `Documents` e `Videos`.
* Tipo MIME: filtrar um ou mais formatos de arquivo compatíveis. <!-- TBD:  [supported file formats](/help/using/supported-file-formats.md). -->
* Tamanho da imagem: forneça um ou mais valores máximos e mínimos de dimensão para filtrar imagens. O tamanho é fornecido em valores de dimensão de pixel e não é o tamanho do arquivo das imagens.
* Data de criação: a data de criação do ativo fornecida pelos metadados. O formato de data padrão usado é `yyyy-mm-dd`.
* Data de modificação: a data da última modificação dos ativos. O formato de data padrão usado é `yyyy-mm-dd`.
* Data de expiração: filtre os resultados da pesquisa com base no status `Expired` de um ativo. Além disso, é possível especificar um intervalo de datas para a expiração dos ativos, permitindo filtrar ainda mais os resultados da pesquisa.
* Filtros Personalizados: [Adicione filtros personalizados](#custom-filters) à interface do usuário de exibição do Assets. Aplique filtros personalizados além dos filtros padrão para refinar os resultados da pesquisa.

E possível classificar os ativos pesquisados em ordem crescente ou decrescente de `Name`, `Relevance`, `Size`, `Modified` e `Created`. Os ativos pesquisados são classificados com base em `Relevance`, por padrão.

## Gerenciar filtros personalizados {#custom-filters}

**Permissões necessárias:** `Can Edit`, `Owner` ou Administrador.

A visualização Assets também permite adicionar filtros personalizados à interface. É possível aplicar esses filtros personalizados além dos [filtros padrão](#refine-search-results) para refinar os resultados da pesquisa.

A visualização Assets fornece os seguintes filtros personalizados:

<table>
    <tbody>
     <tr>
      <th><strong>Nome do filtro personalizado</strong></th>
      <th><strong>Descrição</strong></th>
     </tr>
     <tr>
      <td>Título</td>
      <td>Filtrar ativos usando o título do ativo. O título especificado nos critérios de pesquisa que diferenciam maiúsculas e minúsculas deve corresponder ao título exato do ativo a ser exibido nos resultados.</td>
     </tr>
     <tr>
      <td>Nome</td>
      <td>Filtre ativos usando o nome do arquivo de ativo. O nome especificado nos critérios de pesquisa que diferenciam maiúsculas e minúsculas deve corresponder ao nome exato do arquivo do ativo a ser exibido nos resultados.</td>
     </tr>
     <tr>
      <td>Tamanho do ativo</td>
      <td>Filtre ativos definindo um intervalo de tamanho, em bytes, nos critérios de pesquisa para um ativo ser exibido nos resultados.</td>
     </tr>
     <tr>
      <td>Tags previstas</td>
      <td>Filtrar ativos usando a tag inteligente de ativos. O nome da tag inteligente especificada nos critérios de pesquisa que diferenciam maiúsculas e minúsculas deve corresponder ao nome exato da tag inteligente do ativo a ser exibido nos resultados. Não é possível especificar várias tags inteligentes nos critérios de pesquisa.</td>
     </tr>    
    </tbody>
   </table>

<!--
   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. For example, if you define <b>ma*</b> as the search criteria, Assets view displays assets with title, such as, market, marketing, man, manchester, and so on in the results.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria.

   You can use a wildcard operator (*) to enable Assets view to display assets in the results that partially match the search criteria. You can specify multiple smart tags separated by a comma in the search criteria.

   -->

### Adicionar filtros personalizados {#add-custom-filters}

Para adicionar filtros personalizados:

1. Clique em **[!UICONTROL Filtros]**.

1. Na seção **[!UICONTROL Filtros personalizados]**, clique em **[!UICONTROL Editar]** ou **[!UICONTROL Adicionar filtros]**.

   ![Adicionar filtros personalizados](assets/add-custom-filters.png)

1. Na caixa de diálogo **[!UICONTROL Gerenciamento de filtros personalizados]**, selecione os filtros que precisam ser adicionados à lista de filtros existente. Selecionar **[!UICONTROL Filtros personalizados]** para selecionar todos os filtros.

1. Clique em **[!UICONTROL Confirmar]** para adicionar os filtros à interface.

### Remover filtros personalizados {#remove-custom-filters}

Para remover filtros personalizados:

1. Clique em **[!UICONTROL Filtros]**.

1. Na seção **[!UICONTROL Filtros personalizados]**, clique em **[!UICONTROL Editar]**.

1. Na caixa de diálogo **[!UICONTROL Gerenciamento de filtros personalizados]**, desmarque os filtros que precisam ser removidos da lista de filtros existente.

1. Clique em **[!UICONTROL Confirmar]** para remover os filtros da interface.

## Pesquisar com IA {#ai-search}

A Pesquisa de IA é um recurso de pesquisa avançada que entende o significado e a intenção por trás da consulta de um usuário, em vez de depender de correspondências exatas de palavras-chave. Ele usa inteligência artificial (IA) e aprendizado de máquina para fornecer resultados mais precisos e com reconhecimento de contexto.

Ao contrário da pesquisa tradicional baseada em palavras-chave, que procura termos exatos, a Pesquisa AI interpreta as relações entre palavras, conceitos e intenção do usuário. Isso garante que os usuários encontrem o que procuram, mesmo que a consulta seja redigida de forma diferente, contenha erros de digitação ou esteja em outro idioma.

Alguns, se seus principais benefícios incluírem:

* **Suporte multilíngue**: pesquise em vários idiomas sem exigir traduções exatas. Os usuários podem encontrar conteúdo relevante independentemente do idioma de consulta.

* **Lida com erros ortográficos**: interpreta erros de digitação e de ortografia, garantindo resultados precisos mesmo com uma entrada imperfeita.

* **Entende sinônimos**: fornece resultados para termos e frases relacionados, de modo que os usuários não precisam adivinhar a palavra-chave correta.

* **Pesquisa sensível ao contexto**: reconhece a intenção por trás de uma consulta, não apenas as palavras exatas.

### Exemplos para a pesquisa de IA {#examples-ai-search}

**Exemplo de prompt**: *Mulher tomando café*

A pesquisa tradicional baseada em palavras-chave procura correspondências exatas de metadados de ativos, como `Woman`, `drinking`, `Coffee`, e retorna ativos que incluem todos esses termos nos metadados.

No entanto, a Pesquisa de IA corresponde a palavras semelhantes, como `Girl`, `Lady` no caso de `Woman` e `Cappuccino` e `Latte` no caso de `Coffee`.

Da mesma forma, você pode especificar este prompt em espanhol ou digitar incorretamente `Woman` como `Wman` e ainda obter os mesmos resultados.

![Pesquisa semântica no modo de exibição Assets](assets/semantic-search.png)

### Ativar ou desativar a pesquisa de IA na exibição do Assets {#enable-disable-ai-search}

Execute as seguintes etapas para ativar ou desativar a Pesquisa de IA:

1. Navegue até **[!UICONTROL Configurações]** >> **[!UICONTROL Configurações Gerais]** e selecione a guia **[!UICONTROL Pesquisa]**.

1. Na seção **[!UICONTROL Pesquisa]**, selecione **[!UICONTROL Pesquisa de IA]** para habilitar a Pesquisa de IA ou **[!UICONTROL Palavra-chave]** para desabilitá-la.

   ![Pesquisa semântica no modo de exibição Assets](/help/assets/assets/enable-disable-ai-search.png)

1. Clique em **[!UICONTROL Salvar]**.


## Pesquisar ativos usando o [!DNL Adobe Firefly] {#search-firefly}

Você pode pesquisar um ativo que não está disponível em nenhuma das pastas de ativos utilizando o recurso de pesquisa de ativos do [!DNL Adobe Firefly] no [!DNL Experience Manager Assets]. Isso permite gerar ativos com eficiência em tempo real que não estão armazenados nas pastas de ativos.

### Antes de começar {#search-assets-firefly-prereqs}

Você precisa ter uma assinatura do [!DNL Adobe Express] ativa.

### Geração de ativos {#generate-assets-firefly}

Para gerar novos ativos usando o [!DNL Adobe Firefly]:

1. Navegue até o espaço de trabalho do [!DNL AEM Assets].

1. Digite o nome do ativo na barra de pesquisa. Por exemplo, você pode pesquisar um ativo usando a palavra-chave `Bugatti Type 57`. Ao pesquisar o ativo, nenhum resultado é encontrado porque o ativo não existe em nenhuma das pastas de ativos. Para gerar ativos usando a IA, clique em **[!UICONTROL Gerar com Firefly]**. A tela do [!DNL Adobe Firefly] é exibida.

   ![Integração do Firefly](assets/firefly-integration.png)

   Os novos ativos foram gerados com sucesso. Além disso, você pode alterar a descrição da imagem digitando o novo prompt de texto na caixa de descrição. [Saiba como escrever um bom prompt de IA para gerar conteúdo extraordinário e relevante](https://helpx.adobe.com/br/firefly/using/tips-and-tricks.html). Como alternativa, você pode [editar a imagem com vários outros recursos, como alterar o estilo, as dimensões da imagem e muito mais](https://helpx.adobe.com/br/firefly/using/text-to-image.html).

   ![Integração do Firefly](assets/bugatti-type-57.png)

1. Selecione uma imagem que deseja salvar. Clique em **[!UICONTROL Salvar]** e salve os ativos na pasta de sua preferência para facilitar o acesso.

1. O formulário Salvar ativo é exibido. Especifique os seguintes campos:

   * Insira um nome para o arquivo no campo **Salvar como**.
   * Selecione uma pasta de destino.
   * Forneça detalhes como o nome do projeto ou da campanha, palavras-chave, canais, intervalo de tempo e região.

   ![Integração do Firefly](assets/save-generated-asset.png)

1. Clique em **Salvar como novo ativo** para salvar o(s) ativo(s).

### Upload de ativos {#upload-assets-firefly}

Para fazer upload do ativo gerado para o repositório de ativos:

1. Clique em **[!UICONTROL Fazer upload]**.
1. Selecione a pasta de ativos para a qual você deseja fazer upload do ativo e clique em **[!UICONTROL Selecionar pasta]**.
   ![Faça o upload do ativo](assets/upload-asset-firefly.jpg)

## Pesquisas salvas {#saved-search}

A funcionalidade de pesquisa é bastante fácil de usar no [!DNL Assets view]. Na caixa de pesquisa, você pode digitar uma palavra-chave e pressionar Enter para ver os resultados, além disso, é possível pesquisar novamente por palavras-chave recentes de maneira rápida, com um único clique.

Também é possível filtrar os resultados da pesquisa com base em critérios específicos relacionados aos metadados e tipos de ativos. O [!DNL Assets view] também permite salvar os parâmetros de uma pesquisa para melhorar a experiência de busca de filtros usados com frequência. Em seguida, você pode selecionar a pesquisa salva para pesquisar e aplicar o filtro com apenas um clique.

Para criar uma pesquisa salva, pesquise por algum ativo, aplique um ou mais filtros e clique em **[!UICONTROL Salvar como]** > **[!UICONTROL Pesquisa salva]** no painel [!UICONTROL Filtros]. Você também pode clicar em **[!UICONTROL Salvar como]** e selecionar **[!UICONTROL Coleção inteligente]** para salvar os resultados como uma coleção inteligente. Consulte [Criar uma coleção inteligente](manage-collections.md#create-a-smart-collection) para obter mais detalhes.

![Criar coleção inteligente](assets/create-smart-collection.png)

<!-- TBD: Search behavior. Full-text search. Ranking and rank boosts. Hidden assets.
Report poor UX that users can only save a filtered search and not a simple search.
.
Are other supported files fully indexed and support full-text search? Eg. audio/videos files can at best have metadata indexed.
Anything about ranking of assets displayed in search results?

What about temporarily hiding an asset (suspending search on it) from the search results? If an asset is undergoing review collaboration, should it be used by others? Should it be hidden in search?

When userA is searching and userB add an asset that matches search results, will the asset display in search as soon as userA refreshes the page? Assuming indexing is near real-time. May not be so for bulk uploads.
-->

## Trabalhar com os resultados da pesquisa {#work-with-search-results}

Você pode selecionar os ativos exibidos nos resultados da pesquisa e realizar as seguintes ações:

* **Localizar imagem semelhante**: encontre ativos de imagem semelhantes na interface do Assets com base nos metadados e nas tags inteligentes.

* **Detalhes**: visualizar e editar as propriedades do ativo.

* **Baixar**: baixar um ativo.

* **Adicionar à coleção**: adicionar o ativo selecionado a uma coleção.

* **Fixar no Acesso rápido**: [fixar um ativo](my-workspace-assets-view.md) para agilizar o acesso quando precisar. Todos os itens fixados são exibidos na seção **Acesso rápido** do Meu espaço de trabalho.

* **Abrir no Adobe Express**: edite uma imagem no Adobe Express integrado na tela do Experience Manager Assets.

* **Editar**: editar a imagem usando o Adobe Express.

* **Compartilhar link**: [compartilhar links](share-links-for-assets-view.md) para um ativo com outros usuários, para que possam acessá-lo e baixá-lo.

* **Excluir**: excluir um ativo.

* **Copiar**: copiar um ativo para um local de pasta diferente.

* **Mover**: mover um ativo para um local de pasta diferente.

* **Renomear**: renomear um ativo.

* **Copiar para bibliotecas**: adicione um ativo à biblioteca.

* **Atribuir tarefas**: atribuir tarefas de um ativo a usuários.

* **Observar**: [monitorar as operações](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/manage/search-assets) executadas em um ativo.

## Configurar a página inicial da pesquisa {#configuring-search-first-homepage}

A visualização do Assets permite selecionar a página de aterrissagem padrão da sua organização. Ao usar a opção “Pesquisar primeiro” como a página inicial, é possível personalizar a identidade visual da página, através da configuração das imagens de fundo e do logotipo que corresponde à sua marca.

Para configurar a primeira página de pesquisa, execute as etapas abaixo:

1. Navegue até **[!UICONTROL Configurações]** >; **[!UICONTROL Configurações gerais]**.
1. Selecione **[!UICONTROL Pesquisar primeiro]**. Isso abre mais configurações relacionadas à primeira pesquisa. Você pode configurar o [alinhamento](#setting-alignment-search-bar) ou [definir a imagem de fundo e o logotipo](#setting-background-image-and-logo) da sua página inicial.

### Configuração do alinhamento da barra de pesquisa {#setting-alignment-search-bar}

O [!DNL Assets view] permite alterar o alinhamento da barra de pesquisa. Você pode fazer a barra de pesquisa aparecer no centro ou na parte superior. Selecione o alinhamento apropriado e clique em **[!UICONTROL Salvar]**.

![Alinhamento da primeira página de pesquisa](assets/search-first-alignment.png)

### Configuração da imagem de fundo e logotipo da página inicial {#setting-background-image-and-logo}

Você pode adicionar o logotipo da marca e a imagem de fundo à sua primeira página de pesquisa. Execute as seguintes etapas:

1. Navegue até a seção **[!UICONTROL Imagem de fundo e logotipo]** na **[!UICONTROL Página inicial]**.
1. Clique em **[!UICONTROL Substituir]** para procurar imagens do repositório de ativos.
1. Clique em **[!UICONTROL Salvar]**. [Visualize](#preview-configured-homepage) as alterações para revisar as modificações.

### Visualizar a página inicial configurada {#preview-configured-homepage}

Você pode visualizar o layout e a formatação da primeira página de pesquisa. Com a opção **[!UICONTROL Visualizar]**, é possível corrigir o layout ou fazer as modificações necessárias. Para visualizar a página inicial configurada, execute as etapas abaixo:

1. Clique em **[!UICONTROL Configurações gerais]** e selecione **[!UICONTROL Pesquisar primeiro]**.
1. Navegue até **[!UICONTROL Personalizar a primeira página de pesquisa]** e clique em **[!UICONTROL Visualizar]**. Alterne o botão **[!UICONTROL Tema escuro]** para visualizar a página inicial em um tema escuro ou claro.
1. Clique em **[!UICONTROL Fechar]** para fechar a janela de visualização.

   ![Visualização da primeira página de pesquisa](/help/assets/assets/search-first-preview.gif)


<!--

## Contextual Search {#contextual-search}

You can also search assets available in the repository by defining text prompts. Experience Manager Assets automatically transforms those text prompts to search filters and displays the search results. You can view and modify automatic filters using the Filters Pane to further narrow down the search results.

### Access Contextual Search {#access-contextual-search}

To access Contextual Search in Experience Manager Assets:

1. Click **[!UICONTROL Search]** in the left pane.

   ![Contextual Search](assets/access-contextual-search.png)

1. Define the text prompt in the Search text box and click **[!UICONTROL Contextual Search]**.

   ![Contextual Search text prompt](/help/assets/assets/wknd-contextual-search.png)

   [!DNL Experience Manager Assets] displays the search results.

### Supported filters {#supported-filters}

Contextual Search supports the following filters out-of-the-box. Base your text prompts on these filters to view appropriate search results.

* Image height

* Image width

* File type: image, document, video, or folder.

* MIME type: JPG, PNG, TIFF, GIF, MP4, PDF, PPTX, DOCX or XLSX

* Created date

* Modified date

* Expiration date

* Asset status: Approved, Rejected, or all

* Expired assets

### Examples for the text prompts {#text-prompts-examples}

**Example 1**

**Text Prompt**: Images created this month.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 1](assets/contextual-search-example1.png)

**Example 2**

**Text prompt**: Images at least 200px tall and 100px wide with beach and clear sky.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 2](assets/contextual-search-example2.png)

**Example 3**

**Text prompt**: I need images of blue sky that are 1500 and 2500 pixel height and created in the past month that is not expired and approved.

[!DNL Experience Manager Assets] applies the following filters automatically and displays the search results:

![Contextual Search Example 3](assets/contextual-search-example3.png)

The following video illustrates the end-to-end process from accessing the Contextual Search User Interface to defining text prompts, and viewing the search results.

>[!VIDEO](https://video.tv.adobe.com/v/3428407)

### Disable Contextual Search {#disable-contextual-search}

Administrators also have the option to disable Contextual Search for users in your organization. To do so, execute the following steps:

1. Navigate to **[!UICONTROL Settings]** > **[!UICONTROL General Settings]**.

1. In the [!UICONTROL Contextual Search] section, turn off the **[!UICONTROL Enable Contextual Search for your organization]** toggle to disable the Contextual Search feature for all users in your organization.  

### Contextual Search feedback {#contextual-search-feedback}

If you need to provide feedback on the Contextual Search feature, click ![Contextual Search icon](assets/do-not-localize/Smock_Help_18_N.svg)  and click the Feedback icon. Select the feedback type, specify the subject and description, and click **[!UICONTROL Submit]**.

![Contextual Search feedback](assets/contextual-search-feedback.png)

-->

## Próximas etapas {#next-steps}

* [Assista a um vídeo para pesquisar ativos no modo de exibição Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/using.html?lang=pt-BR)

* Forneça feedback sobre o produto usando a opção [!UICONTROL Feedback] disponível na interface de visualização do Assets

* Forneça feedback sobre a documentação por meio das opções [!UICONTROL Editar esta página] ![editar a página](assets/do-not-localize/edit-page.png) ou [!UICONTROL Registrar um problema] ![criar um problema do GitHub](assets/do-not-localize/github-issue.png) disponíveis na barra lateral direita.

* Entre em contato com o [Atendimento ao cliente](https://experienceleague.adobe.com/?support-solution=General&lang=pt-BR#support)



