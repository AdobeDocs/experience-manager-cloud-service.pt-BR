---
title: Pesquise ativos e imagens digitais em [!DNL Adobe Experience Manager].
description: Saiba como localizar os ativos necessários em [!DNL Adobe Experience Manager] usando o painel Filtros e como usar os ativos exibidos na pesquisa.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 836e4e7fa727e350ef757984306b32df25921663
workflow-type: tm+mt
source-wordcount: '4741'
ht-degree: 5%

---


# Pesquisar ativos em [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] fornece métodos robustos de descoberta de ativos que ajudam você a atingir uma velocidade de conteúdo mais alta. Suas equipes podem reduzir o tempo de comercialização com uma experiência de pesquisa inteligente e perfeita usando recursos prontos para uso e métodos personalizados. Pesquisar ativos é fundamental para o uso de um sistema de gerenciamento de ativos digitais — seja para uso adicional por parte de profissionais de criação, para o gerenciamento robusto de ativos por parte de usuários e comerciantes, ou para administração por administradores de DAM. Pesquisas simples, avançadas e personalizadas que você pode executar por meio da [!DNL Assets] interface do usuário ou outros aplicativos e superfícies ajudam a atender a esses casos de uso.

[!DNL Experience Manager Assets] suporta os seguintes casos de uso e este artigo descreve o uso, os conceitos, as configurações, as limitações e a solução de problemas para esses casos de uso.

| Pesquisar ativos | Configuração e administração | Trabalhar com resultados de pesquisa |
|---|---|---|
| [Pesquisas básicas](#searchbasics) | [Índice de pesquisa](#searchindex) | [Classificar resultados](#sort) |
| [Compreender a interface de usuário de pesquisa](#searchui) |  | [Verificar propriedades e metadados de um ativo](#checkinfo) |
| [Sugestões de pesquisa](#searchsuggestions) | [Metadados obrigatórios](#mandatorymetadata) | [Download](#download) |
| [Compreender os resultados e o comportamento da pesquisa](#searchbehavior) | [Modificar aspectos de pesquisa](#searchfacets) | [Atualizações de metadados em massa](#metadataupdates) |
| [Classificação de pesquisa e aumento](#searchrank) | [Extração de texto](#extracttextupload) | [Coleções inteligentes](#collections) |
| [Pesquisa avançada: filtragem e escopo da pesquisa](#scope) | [Previsões personalizadas](#custompredicates) | [Entender e solucionar problemas de resultados inesperados](#unexpectedresults) |
| [Pesquise de outras soluções e aplicativos](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brandportal)</li><li>[aplicativo de desktop Experience Manager](#desktopapp)</li><li>[Imagens do Adobe Stock](#adobestock)</li><li>[Ativos do Dynamic Media](#dynamicmedia)</li></ul> |  |  |
| [Seletor de ativos](#assetselector) |  |  |
| [Limitações ](#tips) e  [dicas](#limitations) |  |  |
| [Exemplos ilustrados](#samples) |  |  |

Pesquise ativos usando o campo Omnisearch na parte superior da interface da Web [!DNL Experience Manager]. Vá para **[!UICONTROL Ativos]** > **[!UICONTROL Ficheiros]** em [!DNL Experience Manager], clique em ![ícone_de_pesquisa](assets/do-not-localize/search_icon.png) na barra superior, introduza a palavra-chave de pesquisa e selecione `Return`. Como alternativa, use o atalho de palavra-chave `/` (barra) para abrir o campo Omnisearch. `Location:Assets` é pré-selecionada para limitar as pesquisas aos ativos DAM. [!DNL Experience Manager] fornece sugestões enquanto seu start digita uma palavra-chave de pesquisa.

Use o painel **[!UICONTROL Filtros]** para procurar ativos, pastas, tags e metadados. Você pode filtrar os resultados da pesquisa com base nas várias opções (predicados), como tipo de arquivo, tamanho do arquivo, data da última modificação, status do ativo, dados de insights e licenciamento da Adobe Stock. Você pode personalizar o painel Filtros e adicionar ou remover predicados de pesquisa usando [aspectos de pesquisa](/help/assets/search-facets.md). O filtro [!UICONTROL Tipo de arquivo] no painel [!UICONTROL Filtros] tem caixas de seleção de estado misto. Portanto, a menos que você selecione todos os predicados aninhados (ou formatos), as caixas de seleção de primeiro nível estarão parcialmente marcadas.

[!DNL Experience Manager] o recurso de pesquisa suporta a pesquisa por coleções e a pesquisa por ativos dentro de uma coleção. Consulte [procurar coleções](/help/assets/manage-collections.md).

## Compreender a interface de pesquisa {#searchui}

Familiarize-se com a interface de pesquisa e as ações disponíveis.

![Compreender a interface de resultados de pesquisa do Experience Manager Assets](assets/aem_search_results.png)

*Figura: Entenda a interface dos resultados da  [!DNL Experience Manager Assets] pesquisa.*

**A.** Salve a pesquisa como uma coleção inteligente. **B.** Filtros ou previsões para restringir os resultados da pesquisa. **C.** Exibir arquivos, pastas ou ambos. **D.** Clique em Filtros para abrir ou fechar o painel à esquerda. **E.** O local de pesquisa é DAM. **F.** Omnisearch com palavra-chave de pesquisa fornecida pelo usuário. **G.** Selecione os resultados de pesquisa carregados. **H.** Número de resultados de pesquisa exibidos fora do total de resultados de pesquisa. **I.** Feche a pesquisa. **J.** Alterne entre a visualização da placa e a visualização da lista.

### Aspectos de pesquisa dinâmica {#dynamicfacets}

Você pode descobrir os ativos desejados mais rapidamente a partir da página de resultados da pesquisa usando o número atualizado dinamicamente dos resultados de pesquisa esperados nas facetas de pesquisa. O número esperado de ativos é atualizado mesmo antes de aplicar o filtro de pesquisa. Ver a contagem esperada em relação ao filtro ajuda a navegar pelos resultados da pesquisa de forma rápida e eficiente.

![Consulte o número aproximado de ativos sem filtrar os resultados da pesquisa em aspectos de pesquisa.](assets/asset_search_results_in_facets_filters.png)

*Figura: Consulte o número aproximado de ativos sem filtrar os resultados da pesquisa em aspectos de pesquisa.*

## Pesquisar sugestões ao digitar {#searchsuggestions}

Ao digitar uma palavra-chave com start, AEM sugere as possíveis palavras-chave ou frases de pesquisa. As sugestões são baseadas nos ativos em AEM. AEM indexa todos os campos de metadados para ajudar na pesquisa. Para fornecer sugestões de pesquisa, o sistema usa os valores dos seguintes poucos campos de metadados. Para fornecer sugestões de pesquisa, considere preencher os seguintes campos com as palavras-chave apropriadas:

* Tags de ativos. (mapeia para `jcr:content/metadata/cq:tags`)
* Título do ativo. (mapeia para `jcr:content/metadata/dc:title`)
* Descrição do ativo. (mapeia para `jcr:content/metadata/dc:description`)
* Título no repositório JCR. O valor pode ser mapeado para o título do ativo. (mapeia para `jcr:content/jcr:title`)
* Descrição no repositório JCR. O valor pode ser mapeado para a descrição do ativo. (mapeia para `jcr:content/jcr:description`)

## Compreender os resultados e o comportamento da pesquisa {#searchbehavior}

### Termos e resultados básicos de pesquisa {#searchbasics}

Você pode executar pesquisas de palavras-chave a partir do campo OmniSearch. A pesquisa de palavra-chave não diferencia maiúsculas de minúsculas e é uma pesquisa de texto completo (nos campos de metadados populares). Se mais de uma palavra-chave for usada, `AND` será o operador padrão entre as palavras-chave.

Os resultados são classificados por relevância, começando com correspondências mais próximas. Para várias palavras-chave, os resultados mais relevantes são os ativos que contêm ambos os termos em seus metadados. Nos metadados, as palavras-chave que aparecem como tags inteligentes são classificadas mais alto do que as palavras-chave que aparecem em outros campos de metadados. [!DNL Experience Manager] permite fornecer um termo de pesquisa específico com maior peso. Além disso, é possível [aumentar a classificação](#searchrank) de alguns ativos direcionados para termos de pesquisa específicos.

Para encontrar rapidamente os ativos relevantes, a interface avançada fornece mecanismos de filtragem, classificação e seleção. Você pode filtrar os resultados com base em vários critérios e ver o número de ativos pesquisados para vários filtros. Como alternativa, você pode executar novamente a pesquisa alterando o query no campo Omnisearch. Quando você altera seus termos ou filtros de pesquisa, os outros filtros permanecem aplicados para preservar o contexto da pesquisa.

Quando os resultados forem muitos ativos, [!DNL Experience Manager] exibirá os primeiros 100 na visualização do cartão e 200 na visualização da lista. À medida que os usuários rolam, mais ativos são carregados. Isso é para melhorar o desempenho. Assista a uma demonstração em vídeo do [número de ativos exibidos](https://www.youtube.com/watch?v=LcrGPDLDf4o).

Às vezes, você pode ver alguns ativos inesperados nos resultados da pesquisa. Para obter mais informações, consulte [resultados inesperados](#unexpectedresults).

AEM pode pesquisar vários formatos de arquivo e os filtros de pesquisa podem ser personalizados para atender às suas necessidades comerciais. Entre em contato com os administradores para saber quais opções de pesquisa estão disponíveis para o seu repositório DAM e quais restrições seu logon pode ter.

<!-- 
### Results with and without Enhanced Smart Tags {#withsmarttags}

By default, AEM search combines the search terms with an AND clause. For example, consider searching for keywords woman running. Only the assets with both woman and running keywords in the metadata appear in the search results by default. The same behavior is retained when special characters (periods, underscores, or dashes) are used with the keywords. The following search queries return the same results:

* `woman running`
* `woman.running`
* `woman-running`

However, the query `woman -running` returns assets without `running` in their metadata.
Using smart tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. So the search results are a combination of,

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Assets smart tagged with either of the keywords (Smart Tags behavior).
-->

### Classificação de pesquisa e otimização {#searchrank}

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos dos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. Corresponde a `woman running` nos vários campos de metadados.
1. Corresponde a `woman running` em tags inteligentes.
1. Corresponde de `woman` ou de `running` em tags inteligentes.

Você pode melhorar a relevância das palavras-chave de ativos específicos para ajudar a aumentar as pesquisas com base nas palavras-chave. Em outras palavras, as imagens para as quais você promove palavras-chave específicas aparecem na parte superior dos resultados da pesquisa quando você pesquisa com base nessas palavras-chave.

1. Na interface do usuário [!DNL Assets], abra a página de propriedades do ativo. Clique em **[!UICONTROL Avançado]** e clique em **[!UICONTROL Adicionar]** em **[!UICONTROL Elevar para palavras-chave de pesquisa]**.
1. Na caixa **[!UICONTROL Promote de pesquisa]**, especifique uma palavra-chave para a qual deseja aumentar a pesquisa da imagem e clique em **[!UICONTROL Adicionar]**. É possível especificar várias palavras-chave da mesma maneira.
1. Clique em **[!UICONTROL Salvar e fechar]**. O ativo que você promoveu para essa palavra-chave aparece entre os principais resultados da pesquisa.

Você pode usar isso em sua vantagem ao aumentar a classificação de alguns ativos nos resultados da pesquisa para a palavra-chave direcionada. Veja o exemplo de vídeo abaixo. Para obter informações detalhadas, consulte [pesquisar em Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Vídeo: Entenda como os resultados da pesquisa são classificados e como a classificação pode ser influenciada.*

## Pesquisa avançada {#scope}

AEM fornece vários métodos, como filtros que se aplicam aos ativos pesquisados, para ajudá-lo a localizar os ativos desejados mais rapidamente. Alguns métodos comumente usados estão descritos abaixo. Alguns [exemplos ilustrados](#samples) são compartilhados abaixo.

**Procurar ficheiros ou pastas**: Nos resultados da pesquisa, consulte arquivos, pastas ou ambos. No painel **[!UICONTROL Filtros]**, você pode selecionar a opção apropriada. Consulte [interface de pesquisa](#searchui).

**Pesquisar ativos em uma pasta**: Você pode limitar a pesquisa a uma pasta específica. No painel **[!UICONTROL Filtros]**, adicione o caminho de uma pasta. Você pode selecionar apenas uma pasta por vez.

![Limitar os resultados da pesquisa a uma pasta adicionando um caminho de pasta no painel Filtros](assets/search_folder_select.gif)

Limitar os resultados da pesquisa a uma pasta adicionando um caminho de pasta no painel Filtros

<!--
### Find similar images {#visualsearch}

To find images that are visually similar to a user-selected image, click **[!UICONTROL Find Similar]** option from the card view of an image or from the toolbar. AEM displays the smart tagged images from the DAM repository that are similar to a user-selected image. See [how to configure similarity search](#configvisualsearch).

![Find similar images using the option in the card view](assets/search_find_similar.png)
*Figure: Find similar images using the option in the card view*
-->

### Imagens do Adobe Stock {#adobestock}

Na interface do usuário AEM, os usuários podem pesquisar [ativos Adobe Stock](/help/assets/aem-assets-adobe-stock.md) e licenciar os ativos necessários. Adicione `Location: Adobe Stock` na barra do Omnisearch. Você também pode usar o painel Filtros para localizar todos os ativos licenciados ou não licenciados ou pesquisar um ativo específico usando o número de arquivo Adobe Stock.

### Ativos do Dynamic Media {#dmassets}

Você pode filtrar por imagens do Dynamic Media selecionando **[!UICONTROL Dynamic Media > Conjuntos]** no painel **[!UICONTROL Filtros]**. Isso filtra e exibe ativos como conjuntos de imagens, carrosséis, conjuntos de mídia mista e conjuntos de rotação.

### Pesquisar usando valores específicos em campos de metadados {#gqlsearch}

É possível para ativos com base nos valores exatos de campos de metadados específicos, como título, descrição e autor. O recurso de pesquisa de texto completo do GQL busca apenas os ativos cujo valor de metadados corresponda exatamente ao seu query de pesquisa. Os nomes das propriedades (por exemplo, autor, título e assim por diante) e os valores distinguem maiúsculas de minúsculas.

| Campo de metadados | Valor e uso da faceta |
|---|---|
| Título | título:John |
| Criador | criador:John |
| Local | local:NA |
| Descrição | descrição:&quot;Imagem de amostra&quot; |
| Ferramenta Criador | creatortool: &quot;Adobe Photoshop CC 2015&quot; |
| Proprietário de direitos autorais | copyrights towner: &quot;Adobe Systems&quot; |
| Contribuinte | colaborador:John |
| Termos de Uso  | usageterms:&quot;CopyRights Reserved&quot; |
| Criado | criado:AAAA-MM-DDTHH |
| Data de expiração | expira:AAAA-MM-DDTHH |
| Hora | hora única:AAAA-MM-DTHH |
| Hora de desligar | offtime:YYYY-MM-DTHH |
| Intervalo de tempo(expira em dateontime,offtime) | campo de faceta : limite inferior...upperbound |
| Caminho | /content/dam/&lt;nome da pasta> |
| Título do PDF | pdftitle: &quot;Adobe Documento&quot; |
| Assunto | assunto: &quot;Formação&quot; |
| Tags | tags:&quot;Localização E Viagem&quot; |
| Tipo | type:&quot;image\png&quot; |
| Largura da imagem | largura:limite inferior..upperbound |
| Altura da imagem | height:limite inferior..upperbound |
| Person | pessoa:John |

O caminho, limite, tamanho e ordem das propriedades não podem ser OUed com nenhuma outra propriedade.

A palavra-chave para uma propriedade gerada pelo usuário é seu rótulo de campo no editor de propriedades em minúsculas, com espaços removidos.

Estes são alguns exemplos de formatos de pesquisa para query complexos:

* Para exibir todos os ativos com vários campos de facetas (por exemplo: title=John Doe e ferramenta criadora = Adobe Photoshop): `title:"John Doe" creatortool : Adobe*`
* Para exibir todos os ativos quando o valor de facetas não for uma única palavra, mas uma sentença (por exemplo: title=Scott Reynolds): `title:"Scott Reynolds"`
* Para exibir ativos com vários valores de uma única propriedade (por exemplo: title=Scott Reynolds ou John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Para exibir ativos com valores de propriedade começando com uma string específica (por exemplo: o título é Scott Reynolds): `title:Scott*`
* Para exibir ativos com valores de propriedade que terminam com uma string específica (por exemplo: o título é Scott Reynolds): `title:*Reynolds`
* Para exibir ativos com um valor de propriedade que contenha uma string específica (por exemplo: título = Sala de reuniões de Basileia): `title:*Meeting*`
* Para exibir ativos que contêm uma determinada string e têm um valor de propriedade específico (por exemplo: procure por Adobe de string em ativos com título=João da Silva): `*Adobe* title:"John Doe"`

## Pesquisar ativos de outras ofertas ou interfaces AEM {#beyondomnisearch}

A Adobe Experience Manager (AEM) conecta o repositório DAM a várias outras soluções AEM para fornecer acesso mais rápido aos ativos digitais e dinamizar os workflows criativos. Qualquer start de descoberta de ativos com navegação ou pesquisa. O comportamento de pesquisa permanece basicamente o mesmo em várias superfícies e soluções. Alguns métodos de pesquisa mudam conforme a audiência do público alvo, os casos de uso e a interface do usuário variam nas soluções AEM. Os métodos específicos estão documentados para as soluções individuais nos links abaixo. As dicas e comportamentos universalmente aplicáveis estão documentados neste artigo.

### Pesquisar ativos no painel Link do ativo do Adobe {#aal}

Usando o Adobe Asset Link, os profissionais criativos agora podem acessar o conteúdo armazenado no AEM Assets, sem sair dos aplicativos Adobe Creative Cloud suportados. Os profissionais de criação podem navegar, pesquisar, fazer check-out e fazer check-in de ativos sem problemas usando o painel no aplicativo nos aplicativos do Creative Cloud: Photoshop, Illustrator e InDesign. O Link de ativo também permite que os usuários pesquisem resultados visualmente semelhantes. Os resultados da exibição da pesquisa visual são capacitados por algoritmos de aprendizado de máquina da Adobe Sensei e ajudam os usuários a encontrar imagens esteticamente semelhantes. Consulte [pesquisar e procurar ativos](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) usando o Link de ativo do Adobe.

### Pesquisar ativos em AEM aplicativo de desktop {#desktopapp}

Profissionais criativos usam o aplicativo de desktop para tornar o AEM Assets facilmente pesquisável e disponível em seu desktop local (Win ou Mac). Os profissionais de criação podem revelar facilmente os ativos desejados no Mac Finder ou no Windows Explorer, abertos em aplicativos de desktop e alterados localmente - as alterações são salvas em AEM com uma nova versão criada no repositório. O aplicativo suporta pesquisas básicas usando uma ou mais palavras-chave, * e ? curingas e operador E. Consulte [procurar, procurar e pré-visualização assets](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) no aplicativo de desktop.

### Pesquisar ativos no Brand Portal {#brandportal}

Usuários e comerciantes de linha de negócios usam o Brand Portal para compartilhar de forma eficiente e segura os ativos digitais aprovados com suas equipes internas, parceiros e revendedores estendidos. Consulte [ativos de pesquisa no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Pesquisar imagens do Adobe Stock {#adobestock-1}

Na interface do usuário AEM, os usuários podem pesquisar ativos da Adobe Stock e licenciar os ativos necessários. Adicione `Location: Adobe Stock` no campo Omnisearch. Você também pode usar o painel **[!UICONTROL Filtros]** para localizar todos os ativos licenciados ou não licenciados ou pesquisar um ativo específico usando o número de arquivo Adobe Stock. Consulte [gerenciar imagens do Adobe Stock em AEM](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Pesquisar ativos do Dynamic Media {#dynamicmedia}

Você pode filtrar por imagens do Dynamic Media selecionando **[!UICONTROL Dynamic Media]** > **[!UICONTROL Conjuntos]** no painel **[!UICONTROL Filtros]**. Isso filtra e exibe ativos como conjuntos de imagens, carrosséis, conjuntos de mídia mista e conjuntos de rotação. Ao criar páginas da Web, os autores podem pesquisar por conjuntos no Localizador de conteúdo. Há um filtro para conjuntos disponível em um menu pop-up.

### Pesquisar ativos no Localizador de conteúdo ao criar páginas da Web {#contentfinder}

Os autores podem usar o Localizador de conteúdo para pesquisar no repositório do DAM os ativos relevantes e usar os ativos nas páginas da Web que eles criam.

<!-- Authors can also use the Connected Assets functionality to search for assets that are available on a remote AEM deployment. Authors can then use these assets in web pages on a local AEM deployment. See [use remote assets](use-assets-across-connected-assets-instances.md#use-remote-assets).
-->

### Pesquisar coleções {#collections}

AEM recurso de pesquisa suporta a pesquisa por coleções e a pesquisa por ativos dentro de uma coleção. Consulte [procurar coleções](/help/assets/manage-collections.md).

## Seletor de ativos {#assetselector}

O seletor de ativos permite que você pesquise, filtre e navegue pelos ativos DAM de uma maneira especial. O seletor de ativos está disponível em `https://[aem_server]:[port]/aem/assetpicker.html`. Você pode buscar os metadados dos ativos selecionados usando o seletor de ativos. Você pode iniciá-lo com parâmetros de solicitação suportados, como tipo de ativo (imagem, vídeo, texto) e modo de seleção (seleções únicas ou múltiplas). Esses parâmetros definem o contexto do seletor de ativos para uma instância de pesquisa específica e permanecem intactos durante toda a seleção.

O seletor de ativos usa a mensagem HTML5 `Window.postMessage` para enviar dados do ativo selecionado para o recipient. O seletor de ativos é baseado no vocabulário do seletor de fundações de Granite. Por padrão, o seletor de ativos opera no modo Procurar.

Você pode passar os seguintes parâmetros de solicitação em um URL para iniciar o seletor de ativos em um contexto específico:

| Nome | Valores | Exemplo | Propósito |
|---|---|---|---|
| sufixo do recurso (B) | Caminho da pasta como sufixo de recurso no URL:[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | Para iniciar o seletor de ativos com uma pasta específica selecionada, por exemplo, com a pasta /content/dam/we-retail/en/atividade, selecionada, o URL deve ter a seguinte forma: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Se você precisar que uma pasta específica seja selecionada quando o seletor de ativos for iniciado, passe-o como um sufixo de recurso. |
| modo | único, múltiplo | [https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single) | No modo múltiplo, você pode selecionar vários ativos simultaneamente usando o seletor de ativos. |
| mimetype | mimetype(s) (`/jcr:content/metadata/dc:format`) de um ativo (curinga também suportada) | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png)</li></ul> | Use-o para filtrar ativos com base em tipos MIME |
| caixa de diálogo | verdadeiro, falso | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Use esses parâmetros para abrir o seletor de ativos como Caixa de diálogo Granite. Essa opção só é aplicável quando você inicia o seletor de ativos por meio do campo Caminho de Granite e o configura como URL pickerSrc. |
| tipo de ativo (S) | imagens, documentos, multimídia, arquivos | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | Use essa opção para filtrar os tipos de ativos com base no valor passado. |
| root | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities) | Use essa opção para especificar a pasta raiz do seletor de ativos. Nesse caso, o seletor de ativos permite que você selecione apenas ativos secundários (diretos/indiretos) na pasta raiz. |

Para acessar a interface do seletor de ativos, vá para `https://[aem_server]:[port]/aem/assetpicker`. Navegue até a pasta desejada e selecione um ou mais ativos. Como alternativa, procure o ativo desejado na caixa Omnisearch, aplique o filtro conforme necessário e selecione-o.

![Procurar e selecionar ativo no seletor de ativos](assets/assetpicker.png)

*Figura: Procure e selecione o ativo no seletor de ativos.*

## Limitações           {#limitations}

O recurso de pesquisa em [!DNL Experience Manager Assets] tem as seguintes limitações:

* Não insira um espaço à esquerda no query de pesquisa; caso contrário, a pesquisa não funcionará.
* [!DNL Experience Manager] pode continuar a mostrar o termo de pesquisa depois de selecionar as propriedades de um ativo dos resultados pesquisados e cancelar a pesquisa.  <!-- (CQ-4273540) -->
* Ao procurar pastas ou arquivos e pastas, os resultados da pesquisa não podem ser classificados em nenhum parâmetro.
* Se você selecionar `Return` sem digitar na barra do Omnisearch, [!DNL Experience Manager] retornará uma lista de somente arquivos e não pastas. Se você pesquisar especificamente por pastas sem usar uma palavra-chave, [!DNL Experience Manager] não retornará nenhum resultado.

Pesquisa visual ou pesquisa de semelhança tem as seguintes limitações:

* A pesquisa visual funciona melhor com repositórios maiores. Embora não haja um número mínimo de imagens necessário para bons resultados, a qualidade das correspondências com algumas imagens pode não ser tão boa quanto as correspondências de um repositório grande.
* Não é possível alterar o modelo ou o trem [!DNL Experience Manager] para localizar imagens semelhantes. Por exemplo, adicionar ou remover tags inteligentes a alguns ativos não altera o modelo. Os ativos são excluídos dos resultados de pesquisa visualmente semelhantes.

A funcionalidade de pesquisa pode ter limitações de desempenho nos seguintes cenários:

* A visualização de cartão tem um tempo de carregamento mais rápido do que a visualização de lista para exibir os resultados da pesquisa.

## Dicas de pesquisa {#tips}

* Ao monitorar o status da revisão de ativos, use a opção apropriada para descobrir quais ativos estão aprovados ou quais ativos estão pendentes de aprovação.
* Use o predicado Insights para pesquisar ativos suportados com base em suas estatísticas de uso obtidas de vários aplicativos Creative. Os dados de uso são agrupados em Pontuação de uso, Impressões, Cliques e canais de mídia nos quais os ativos aparecem categorias.
* Use a caixa de seleção **[!UICONTROL Selecionar tudo]** para selecionar os ativos pesquisados. [!DNL Experience Manager] exibe inicialmente 100 ativos na visualização do cartão e 200 ativos na visualização da lista. Mais ativos são carregados à medida que você percorre os resultados da pesquisa. Você pode selecionar mais ativos do que os ativos carregados. A contagem dos ativos selecionados é exibida no canto superior direito da página de resultados da pesquisa. Você pode operar na seleção, por exemplo, baixar os ativos selecionados, atualizar as propriedades de metadados em massa para os ativos selecionados ou adicionar os ativos selecionados a uma Coleção. Quando mais ativos são selecionados do que exibidos, uma ação é aplicada em todos os ativos selecionados ou uma caixa de diálogo exibe o número de ativos nos quais ela é aplicada. Para aplicar uma ação aos ativos que não foram carregados, verifique se todos os ativos estão selecionados explicitamente.
* Para pesquisar ativos que não contenham os metadados obrigatórios, consulte [metadados obrigatórios](#mandatorymetadata).
* A pesquisa usa todos os campos de metadados. Uma pesquisa genérica, como a pesquisa por 12, geralmente retorna muitos resultados. Para obter melhores resultados, use aspas de duplo (não simples) ou verifique se o número está contíguo a uma palavra sem um caractere especial (por exemplo `shoe12`).
* A pesquisa de texto completo oferece suporte a operadores como `-` e `^`. Para pesquisar essas letras como literais de string, coloque a expressão de pesquisa entre aspas duplos. Por exemplo, use `"Notebook - Beauty"` em vez de `Notebook - Beauty`.
* Se os resultados da pesquisa forem muitos, limite o escopo [de pesquisa](#scope) para zero nos ativos desejados. Funciona melhor quando você tem alguma ideia de como procurar melhor os ativos desejados, por exemplo, tipo de arquivo específico, local específico, metadados específicos e assim por diante.

* **Marcação**: As tags ajudam a categorizar ativos que podem ser pesquisados e pesquisados com mais eficiência. A marcação ajuda a propagar a taxonomia apropriada para outros usuários e workflows. [!DNL Experience Manager] Métodos do oferta para marcar automaticamente ativos usando serviços inteligentes e artificialmente Adobe Sensei que continuam melhorando ao marcar seus ativos com uso e treinamento. Quando você pesquisa ativos, as tags inteligentes são fatoradas se o recurso estiver ativado em sua conta. Funciona juntamente com a funcionalidade de pesquisa incorporada. Consulte [comportamento de pesquisa](#searchbehavior). Para otimizar a ordem na qual os resultados da pesquisa são exibidos, você pode [aumentar a classificação de pesquisa](#searchrank) de alguns ativos selecionados.

* **Indexação**: Somente metadados indexados e ativos são retornados nos resultados da pesquisa. Para melhor cobertura e desempenho, assegure a indexação correta e siga as práticas recomendadas. Consulte [indexação](#searchindex).

## Alguns exemplos ilustrando a pesquisa {#samples}

Use aspas de duplo em torno de palavras-chave para localizar ativos que contenham a frase exata na ordem exata, conforme especificado pelo usuário.

![Comportamento de pesquisa com e sem aspas](assets/search_with_quotes.gif)

*Figura: Comportamento de pesquisa com e sem aspas.*

**Pesquisar com o curinga** de asterisco: Para ampliar a pesquisa, use um asterisco antes ou depois da palavra de pesquisa para corresponder a qualquer número de caracteres. Por exemplo, a pesquisa por executar sem um asterisco não retorna ativos que contenham qualquer variação da palavra (incluindo nos metadados). Um asterisco substitui qualquer número de caracteres. Por exemplo,

* `run` retorna ativos com uma palavra-chave de execução exata
* `run*` retorna ativos com execução, execução, desistência e assim por diante.
* `*run` retorna para trás, execute-o novamente e assim por diante.
* `*run*` retorna todas as combinações possíveis.

![Ilustrando o uso do curinga de asterisco na pesquisa de Ativos usando um exemplo](assets/search_with_asterisk_run.gif)

*Figura: Ilustrando o uso de um asterisco curinga na pesquisa Ativos usando um exemplo.*

**Pesquisa com curinga de ponto de interrogação**: Para ampliar a pesquisa, use um ou mais &#39;?&#39; caracteres para corresponder ao número exato de caracteres. Por exemplo, na ilustração a seguir,

* `run???` O query não corresponde a nenhum ativo.

* `run????` query corresponde à palavra  `running` com quatro caracteres depois  `run`.

* `??run` O query corresponde à palavra  `rerun` com dois caracteres antes  `run`.

![Ilustrando o uso do caractere curinga de ponto de interrogação na pesquisa de Ativos usando um exemplo](assets/search_with_questionmark_run.gif)

*Figura: Ilustrando o uso do caractere curinga de ponto de interrogação na pesquisa de Ativos usando um exemplo.*

**Excluir uma palavra-chave**: Use o traço para procurar ativos que não contêm uma palavra-chave. Por exemplo, o query `running -shoe` retorna ativos que contêm `running`, mas não `shoe`. Da mesma forma, o query `camp -night` retorna ativos que contêm `camp`, mas não `night`. O query `camp-night` retorna ativos que contêm `camp` e `night`.

![Uso do traço para pesquisar ativos que não contenham uma palavra-chave excluída](assets/search_dash_exclude_keyword.gif)

*Figura: Uso do traço para pesquisar ativos que não contenham uma palavra-chave excluída.*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).
-->

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses smart tags. After configuring smart tagging functionality, follow these steps.

1. In AEM CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

    * `costPerEntry` property of type `Double` with the value `10`.

    * `costPerExecution` property of type `Double` with the value `2`.

    * `refresh` property of type `Boolean` with the value `true`.

   This configuration allows searches from the appropriate index.

1. To create Lucene index, in CRXDE, at `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, create node named `imageFeatures` of type `nt-unstructured`. In `imageFeatures` node,

    * Add `name` property of type `String` with the value `jcr:content/metadata/imageFeatures/haystack0`.

    * Add `nodeScopeIndex` property of type `Boolean` with the value of `true`.

    * Add `propertyIndex` property of type `Boolean` with the value of `true`.

    * Add `useInSimilarity` property of type `Boolean` with the value `true`.

   Save the changes.

1. Access `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` and add `similarityTags` property of type `Boolean` with the value of `true`.
1. Apply Smart Tags to the assets in your AEM repository. See [how to configure smart tags](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html?lang=en#configuring).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Save the changes.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Save all the changes.

For related information, see [understand smart tags in AEM](https://helpx.adobe.com/experience-manager/kt/help/assets/smart-tags-feature-video-understand.html) and [how to manage smart tags](/help/assets/smart-tags.md).
-->

<!--
### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#defining-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, AEM Assets offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administrators can customize the Filters panel to modify the default facets using the in-built predicates. AEM provides a good collection of in-built predicates and an editor to customize the facets. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure AEM to extract the text from the assets when users upload assets, such as PSD or PDF files. AEM indexes the extracted text and helps users search these assets based on the extracted text. See [upload assets](/help/assets/manage-digital-assets.md#uploading-assets).
-->

<!-- TBD: Check with gklebus and engineering if these customization are possible in CS.

### Custom predicates to filter search results {#custompredicates}

Predicates are used to create facets. Administrators can customize the search facets in the Filters panel using pre-configured predicates. These predicates can be customized using overlays. See [create custom predicates](/help/assets/searchx.md).

You can search for digital assets based on one or more of the following properties. Filters that apply on some of these properties are available by default and some other filters can be custom-created to apply on the other properties.

| Search field | Search property values |
|---|---|
| Approved Status | Approved or Rejected. |
| Audio Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Audio Codec | Libvorbis, Lame MP3, AAC Encoding. Value is stored in the metadata of video renditions only. |
| File Size | Small, Medium, or Large. |
| Last Modified | Hour, Day, Week, Month, or Year. |
| MIME Types | Images, Documents, Multimedia, Archives, or Other. |
| Orientation | Horizontal, Vertical, or Square. |
| Publish Status | Published or Unpublished. |
| Style | Color, or Black & White. |
| Video Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Codec | x264. Value is stored in the metadata of video renditions only. |
| Video Format | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Value is stored in the metadata of the source video and any renditions. |
| Video Height | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Width | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |

-->

## Trabalhar com resultados de pesquisa de ativos {#aftersearch}

Você pode fazer o seguinte com os ativos que pesquisou em [!DNL Experience Manager]:

* Propriedades de metadados de visualização e outras informações.
* Baixe um ou mais ativos.
* Use as Ações da área de trabalho para abrir esses ativos no aplicativo da área de trabalho.
* Crie coleções inteligentes.

### Classificar resultados da pesquisa {#sort}

Classifique os resultados da pesquisa para descobrir os ativos necessários mais rapidamente. Você pode classificar os resultados da pesquisa na visualização da lista e somente ao selecionar **[[!UICONTROL Arquivos]](#searchui)** no painel **[!UICONTROL Filtros]**. [!DNL Assets]O usa a classificação do lado do servidor para classificar rapidamente todos os ativos (independente da quantidade) em uma pasta ou nos resultados de uma consulta de pesquisa. A classificação do lado do servidor fornece resultados mais rápidos e precisos do que a classificação do lado do cliente.

Na visualização da lista, você pode classificar os resultados da pesquisa da mesma forma que pode classificar os ativos em qualquer pasta. A classificação funciona nessas colunas — Nome, Título, Status, Dimension, Tamanho, Classificação, Uso, (Data) Criado, (Data) Modificado, (Data) Publicado, Fluxo de trabalho e Finalizado.

Para obter as limitações da funcionalidade de classificação, consulte [limitações](#limitations).

### Verificar informações detalhadas de um ativo {#checkinfo}

Você pode verificar informações detalhadas de ativos pesquisados na página de resultados da pesquisa.

Para ver todos os metadados de um ativo, selecione-o e clique em **[!UICONTROL propriedades]** na barra de ferramentas.

Para verificar os comentários em um ativo ou histórico de versão de um ativo, clique nele para abrir uma visualização de grande. Abra a linha do tempo no painel à esquerda e selecione **[!UICONTROL Comentários]** ou **[!UICONTROL Versões]**. Também é possível classificar a atividade da linha do tempo, como comentários ou versões em ordem cronológica.

![Classificar entradas de linha do tempo para um ativo de pesquisa](assets/sort_timeline_search_results.gif)

*Figura: Classificar entradas de linha do tempo para um ativo de pesquisa.*

### Baixar ativos pesquisados {#download}

Você pode baixar os ativos pesquisados e suas representações da mesma forma que baixa ativos comuns de pastas. Selecione um ou mais ativos dos resultados da pesquisa e clique em **[!UICONTROL Download]** na barra de ferramentas.

### Propriedades de metadados de atualização em massa {#metadataupdates}

É possível fazer atualizações em massa nos campos de metadados comuns de vários ativos. Nos resultados da pesquisa, selecione um ou mais ativos. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas e atualize os metadados conforme necessário. Clique em **[!UICONTROL Salvar e Fechar]** quando terminar. Os metadados existentes anteriormente nos campos atualizados são substituídos.

Para os ativos que estão disponíveis em uma única pasta ou coleção, é mais fácil [atualizar os metadados em massa](/help/assets/manage-metadata.md#manage-assets-metadata) sem usar a funcionalidade de pesquisa. Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é mais rápido atualizar os metadados em massa por meio da pesquisa.

### Coleções inteligentes {#collections-1}

Uma coleção é um conjunto ordenado de ativos que podem incluir ativos de locais diferentes, pois as coleções contêm somente referências a esses ativos. As coleções são dos dois tipos a seguir:

* Uma lista de referência estática de ativos, pastas e outras coleções.
* Uma lista dinâmica (coleção inteligente) que preenche ativos na coleção com base em critérios de pesquisa.

Você pode criar coleções inteligentes com base nos critérios de pesquisa. No painel **[!UICONTROL Filtros]**, selecione **[!UICONTROL Arquivos]** e clique em **[!UICONTROL Salvar coleção inteligente]**. Consulte [gerenciar coleções](/help/assets/manage-collections.md).

## Resultados e problemas de pesquisa inesperados {#unexpectedresults}

<!--
**Partially related or unrelated search results**: AEM may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

| Erro, problemas, sintomas | Possível motivo | Possível correção ou compreensão do problema |
|---|---|---|
| Resultados incorretos ao procurar ativos com metadados ausentes. | Ao pesquisar ativos que não têm os metadados obrigatórios, [!DNL Experience Manager] pode exibir alguns ativos que têm metadados válidos. Os resultados são baseados na propriedade de metadados indexados. | Após a atualização dos metadados, a reindexação é necessária para refletir o estado correto dos metadados dos ativos. Consulte [metadados obrigatórios](metadata-schemas.md#define-mandatory-metadata). |
| Muitos resultados de pesquisa. | Parâmetro de pesquisa abrangente. | Considere limitar o escopo [de pesquisa](#scope). O uso de tags inteligentes pode fornecer mais resultados de pesquisa do que o esperado. Consulte [comportamento de pesquisa com tags inteligentes](#withsmarttags). |
| Resultados de pesquisa não relacionados ou parcialmente relacionados. | Alterações no comportamento da pesquisa com marcação inteligente. | Entenda [como a pesquisa muda após a marcação inteligente](#withsmarttags). |
| Nenhuma sugestão de preenchimento automático para ativos. | Os ativos carregados recentemente ainda não estão indexados. Os metadados não estão disponíveis imediatamente como sugestões quando você start digitar uma palavra-chave de pesquisa na barra Omnisearch. | [!DNL Assets] aguarda até a expiração de um período de tempo limite (uma hora por padrão) antes de executar um trabalho em segundo plano para indexar os metadados de todos os ativos recentemente carregados ou atualizados e, em seguida, adiciona os metadados à lista de sugestões. |
| Nenhum resultado de pesquisa. | <ul><li>Os ativos correspondentes ao seu query não existem. </li><li> Espaço em branco adicionado antes do query de pesquisa. </li><li> O campo de metadados não suportados contém a palavra-chave que você pesquisou.</li><li> Pesquisa feita durante o tempo de inatividade de um ativo. </li></ul> | <ul><li>Pesquise usando uma palavra-chave diferente. Como alternativa, use a marcação inteligente ou a pesquisa de semelhança para melhorar os resultados da pesquisa. </li><li>[Limitação](#limitations) conhecida.</li><li>Nem todos os campos de metadados são considerados para pesquisas. Consulte [scope](#scope).</li><li>Pesquise mais tarde ou modifique os ativos necessários em tempo real e inativo.</li></ul> |
| O filtro de pesquisa ou um predicado não está disponível. | <ul><li>O filtro de pesquisa não está configurado.</li><li>Ele não está disponível para seu logon.</li><li>(Menos provável) As opções de pesquisa não são personalizadas na implantação que você está usando.</li></ul> | <ul><li>Entre em contato com o administrador para verificar se as personalizações de pesquisa estão disponíveis ou não.</li><li>Entre em contato com o administrador para verificar se sua conta tem o privilégio/permissões para usar a personalização.</li><li>Entre em contato com o administrador e verifique as personalizações disponíveis para a implantação [!DNL Assets] que você está usando.</li></ul> |
| Ao procurar imagens visualmente semelhantes, uma imagem esperada está ausente. | <ul><li>A imagem não está disponível em [!DNL Experience Manager].</li><li>A imagem não está indexada. Normalmente, quando é carregado recentemente.</li><li>A imagem não está com tags inteligentes.</li></ul> | <ul><li>Adicione a imagem a [!DNL Assets].</li><li>Entre em contato com o administrador para indexar novamente o repositório. Além disso, verifique se você está usando o índice apropriado.</li><li>Entre em contato com o administrador para obter uma tag inteligente dos ativos relevantes.</li></ul> |
| Ao procurar imagens visualmente semelhantes, uma imagem irrelevante é exibida. | Comportamento da pesquisa visual. | [!DNL Experience Manager] exibe quantos ativos potencialmente relevantes forem possíveis. Imagens menos relevantes, se houver, são adicionadas aos resultados, mas com uma classificação de pesquisa mais baixa. A qualidade das correspondências e a relevância dos ativos pesquisados diminuem à medida que você percorre os resultados da pesquisa. |
| Ao selecionar e operar nos resultados da pesquisa, todos os ativos pesquisados não são operados. | A opção [!UICONTROL Selecionar tudo] seleciona apenas os primeiros 100 resultados da pesquisa na visualização do cartão e os primeiros 200 resultados da pesquisa na visualização da lista. |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] guia de implementação de pesquisa](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [Configuração avançada para aumentar os resultados da pesquisa](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [Configurar pesquisa de tradução inteligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

