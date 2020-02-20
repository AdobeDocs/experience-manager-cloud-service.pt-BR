---
title: Pesquisar ativos digitais e imagens no AEM
description: Saiba como localizar os ativos necessários no AEM usando o painel Filtros e como usar os ativos exibidos na pesquisa.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 7141e42f53c556c0ac21def6085182ef400f5a71

---


# Pesquisar ativos no AEM {#search-assets-in-aem}

Você pode alcançar uma velocidade de conteúdo maior usando opções de descoberta de ativos amigáveis no Experience Manager. Suas equipes podem reduzir o tempo de comercialização com uma experiência de pesquisa inteligente e perfeita usando recursos prontos para uso e métodos personalizados. Pesquisar ativos é fundamental para o uso de um sistema de gerenciamento de ativos digitais — seja para uso adicional por parte de profissionais de criação, para o gerenciamento robusto de ativos pelos usuários e comerciantes de negócios ou para administração por administradores de DAM. Pesquisas simples, avançadas e personalizadas que você pode executar por meio da interface de usuário do AEM Assets ou outros aplicativos e superfícies ajudam a atender a esses casos de uso.

O AEM oferece suporte aos seguintes casos de uso e este artigo descreve o uso, os conceitos, as configurações, as limitações e a solução de problemas desses casos de uso.

| Pesquisar ativos | Configuração e administração | Trabalhar com resultados de pesquisa |
|--- |--- |--- |
| [Pesquisas básicas](#searchbasics) | [Índice de pesquisa](#searchindex) | [Classificar resultados](#sort) |
| [Entender a interface de usuário de pesquisa](#searchui) |  | [Verificar propriedades e metadados de um ativo](#checkinfo) |
| [Sugestões de pesquisa](#searchsuggestions) | [Metadados obrigatórios](#mandatorymetadata) | [Download](#download) |
| [Compreender os resultados e o comportamento da pesquisa](#searchbehavior) | [Modificar aspectos de pesquisa](#searchfacets) | [Atualizações de metadados em massa](#metadataupdates) |
| [Classificação de pesquisa e aumento](#searchrank) | [Extração de texto](#extracttextupload) | [Coleções inteligentes](#collections) |
| [Pesquisa avançada: filtragem e escopo da pesquisa](#scope) | [Previsões personalizadas](#custompredicates) | [Entenda os resultados](#unexpectedresults) inesperados e [solucione problemas](#troubleshoot) |
| [Pesquise de outras soluções e aplicativos](#beyondomnisearch): Link <br />do [ativo](#aal) Aplicativo <br />para [](#desktopapp) desktop <br />     Imagens [do](#adobestock) Adobe Stock <br />     Ativos do [Dynamic Media](#dynamicmedia) |  |  |
| [Seletor/seletor de ativos](#assetselector) |  |  |
| [Limitações](#tips) e [dicas](#limitations) |  |  |
| [Exemplos ilustrados](#samples) |  |  |

Pesquise ativos usando o campo Omnisearch na parte superior da interface da Web do AEM. Vá para **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]** no AEM, clique em ![search_icon](assets/do-not-localize/search_icon.png) na barra superior, digite a palavra-chave de pesquisa e pressione return. Como alternativa, use o atalho de palavra-chave `/` (barra) para abrir o campo Omnisearch. `Location:Assets` é pré-selecionada para limitar as pesquisas aos ativos DAM. É possível fazer pesquisas avançadas para aumentar ou limitar o [escopo da pesquisa](#scope).

Use o painel **[!UICONTROL Filtros]** para procurar ativos, pastas, tags e metadados. Você pode filtrar os resultados da pesquisa com base nas várias opções (predicados), como tipo de arquivo, tamanho do arquivo, data da última modificação, status do ativo, dados de insights e licenciamento do Adobe Stock. Você pode personalizar o painel Filtros e adicionar/remover predicados de pesquisa usando aspectos [de](/help/assets/search-facets.md)pesquisa.

O recurso de pesquisa do AEM oferece suporte à pesquisa de coleções e à pesquisa de ativos em uma coleção. Consulte Coleções [de pesquisa](/help/assets/manage-collections.md).

## Compreender a interface de pesquisa {#searchui}

Familiarize-se com a interface de pesquisa e as ações disponíveis.

![](assets/aem_search_results.png) Noções básicas sobre partes da interface *de resultados de pesquisa do Assets* Figura: Noções básicas da interface de resultados da pesquisa de Ativos

**** A. Salve a pesquisa como uma coleção inteligente. **** B. Filtros (predicados) para restringir os resultados da pesquisa. **C.** Exibir arquivos, pastas ou ambos nos resultados da pesquisa. **** D. Clique em Filtros para abrir ou fechar o painel esquerdo. **** E. O local de pesquisa é DAM. ************ F. Campo Omnisearch com a palavra-chave de pesquisa fornecida pelo usuário **G. Marque a caixa para selecionar todos os resultados da pesquisa** H. Número de resultados de pesquisa exibidos fora do total de resultados de pesquisa **I. Feche a pesquisa** J. Alternar entre a exibição de cartão e a exibição de lista

### Aspectos de pesquisa dinâmica {#dynamicfacets}

Você pode descobrir os ativos desejados mais rapidamente a partir da página de resultados da pesquisa usando o número atualizado dinamicamente dos resultados de pesquisa esperados nas facetas de pesquisa. O número esperado de ativos é atualizado mesmo antes de aplicar o filtro de pesquisa. Ver a contagem esperada em relação ao filtro ajuda a navegar pelos resultados da pesquisa de forma rápida e eficiente. Para obter mais informações, consulte [Pesquisar ativos no AEM](/help/assets/search-assets.md).

![Consulte o número aproximado de ativos sem filtrar os resultados da pesquisa em aspectos de pesquisa.](assets/asset_search_results_in_facets_filters.png)

Consulte o número aproximado de ativos sem filtrar os resultados da pesquisa em aspectos de pesquisa.

## Search suggestions as you type {#searchsuggestions}

Quando você começa a digitar uma palavra-chave, o AEM sugere as possíveis palavras-chave ou frases de pesquisa. As sugestões são baseadas nos ativos no AEM. O AEM indexa todos os campos de metadados para ajudar na pesquisa. Para fornecer sugestões de pesquisa, o sistema usa os valores dos seguintes poucos campos de metadados. Para fornecer sugestões de pesquisa, considere preencher os seguintes campos com as palavras-chave apropriadas:

* Tags de ativos. (mapeia para `jcr:content/metadata/cq:tags`)
* Título do ativo. (mapeia para `jcr:content/metadata/dc:title`)
* Descrição do ativo. (mapeia para `jcr:content/metadata/dc:description`)
* Título no repositório JCR. O valor pode ser mapeado para o título do ativo. (mapeia para `jcr:content/jcr:title`)
* Descrição no repositório JCR. O valor pode ser mapeado para a descrição do ativo. (mapeia para `jcr:content/jcr:description`)

## Compreender os resultados e o comportamento da pesquisa {#searchbehavior}

### Termos e resultados básicos da pesquisa {#searchbasics}

Você pode executar pesquisas de palavras-chave a partir do campo OmniSearch. A pesquisa de palavra-chave não diferencia maiúsculas de minúsculas e é uma pesquisa de texto completo (nos campos de metadados populares). Se mais de uma palavra-chave for usada, `AND` será o operador padrão entre as palavras-chave. Os resultados são classificados por relevância, começando com correspondências mais próximas. Para várias palavras-chave, os resultados mais relevantes são os ativos que contêm ambos os termos em seus metadados. Nos metadados, as palavras-chave que aparecem como tags inteligentes são classificadas mais alto do que as palavras-chave que aparecem em outros campos de metadados.

O AEM permite que você atribua um determinado termo de pesquisa maior peso. Além disso, é possível aumentar a classificação de alguns ativos direcionados para termos de pesquisa específicos. Os administradores do AEM podem realizar essas configurações, conforme descrito abaixo.

Para encontrar rapidamente os ativos relevantes, a interface avançada fornece mecanismos de filtragem, classificação e seleção. Você pode filtrar os resultados com base em vários critérios e ver o número de ativos pesquisados para vários filtros. Como alternativa, você pode executar novamente a pesquisa alterando a consulta no campo Omnisearch. Quando você altera seus termos de pesquisa ou filtros, os outros filtros permanecem aplicados para preservar o contexto da pesquisa.

Às vezes, você pode ver alguns ativos inesperados nos resultados da pesquisa. Para obter mais informações, consulte resultados [](#unexpectedresults)inesperados.

O AEM pode pesquisar vários formatos de arquivo e os filtros de pesquisa podem ser personalizados para atender às suas necessidades comerciais. Entre em contato com os administradores para saber quais opções de pesquisa estão disponíveis para o seu repositório DAM e quais restrições seu logon pode ter.

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

### Classificação de pesquisa e aumento {#searchrank}

Os resultados da pesquisa que correspondem a todos os termos de pesquisa nos campos de metadados são exibidos primeiro, seguidos dos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. No exemplo acima, a ordem aproximada de exibição dos resultados da pesquisa é:

1. Corresponde `woman running` aos vários campos de metadados.
1. Corresponde a `woman running` tags inteligentes.
1. Corresponde a `woman` ou de `running` em tags inteligentes.

Você pode melhorar a relevância das palavras-chave de ativos específicos para ajudar a aumentar as pesquisas com base nas palavras-chave. Em outras palavras, as imagens para as quais você promove palavras-chave específicas aparecem na parte superior dos resultados da pesquisa quando você pesquisa com base nessas palavras-chave.

1. Na interface do usuário Ativos, abra a página de propriedades do ativo. Clique em **[!UICONTROL Avançado]** e clique/toque em **[!UICONTROL Adicionar]** em **[!UICONTROL Elevar para palavras-chave]** de pesquisa.
1. Na caixa **[!UICONTROL Pesquisar promoção]** , especifique uma palavra-chave para a qual deseja aumentar a pesquisa da imagem e clique/toque em **[!UICONTROL Adicionar]**. É possível especificar várias palavras-chave da mesma maneira.
1. Clique/toque em **[!UICONTROL Salvar e fechar]**. O ativo que você promoveu para essa palavra-chave aparece entre os principais resultados da pesquisa.

Você pode usar isso em sua vantagem ao aumentar a classificação de alguns ativos nos resultados da pesquisa para a palavra-chave direcionada. Veja o exemplo de vídeo abaixo. Para obter informações detalhadas, consulte [pesquisar no AEM](https://helpx.adobe.com/experience-manager/kt/help/assets/search-feature-video-use.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*Entenda como os resultados da pesquisa são classificados e como a classificação pode ser influenciada.*

## Advanced search {#scope}

O AEM fornece vários métodos, como filtros, que se aplicam aos ativos pesquisados, para ajudá-lo a localizar os ativos desejados mais rapidamente. Alguns métodos comumente usados estão descritos abaixo. Alguns exemplos [](#samples) ilustrados são compartilhados abaixo.

**Procurar ficheiros ou pastas**: Nos resultados da pesquisa, consulte arquivos, pastas ou ambos. No painel **[!UICONTROL Filtros]** , é possível selecionar a opção apropriada. Consulte interface [de](#searchui)pesquisa.

**Pesquisar ativos em uma pasta**: Você pode limitar a pesquisa a uma pasta específica. No painel **[!UICONTROL Filtros]** , adicione o caminho de uma pasta. Você pode selecionar apenas uma pasta por vez.

![Limitar os resultados da pesquisa a uma pasta adicionando um caminho de pasta no painel Filtros](assets/search_folder_select.gif)

Limitar os resultados da pesquisa a uma pasta adicionando um caminho de pasta no painel Filtros

<!--
### Find similar images {#visualsearch}

To find images that are visually similar to a user-selected image, click **[!UICONTROL Find Similar]** option from the card view of an image or from the toolbar. AEM displays the smart tagged images from the DAM repository that are similar to a user-selected image. See [how to configure similarity search](#configvisualsearch).

![Find similar images using the option in the card view](assets/search_find_similar.png)
*Figure: Find similar images using the option in the card view*
-->

### Imagens do Adobe Stock {#adobestock}

Na interface do usuário do AEM, os usuários podem pesquisar ativos [do](/help/assets/aem-assets-adobe-stock.md) Adobe Stock e licenciar os ativos necessários. Adicione `Location: Adobe Stock` na barra Omnisearch. Você também pode usar o painel Filtros para localizar todos os ativos licenciados ou não licenciados ou pesquisar um ativo específico usando o número de arquivo do Adobe Stock.

### Ativos do Dynamic Media {#dmassets}

Você pode filtrar por imagens do Dynamic Media selecionando **[!UICONTROL Mídia dinâmica > Conjuntos]** no painel **[!UICONTROL Filtros]** . Filtra e exibe ativos como conjuntos de imagens, carrosséis, conjuntos de mídia mista e conjuntos de rotação.

### Pesquisar usando valores específicos em campos de metadados {#gqlsearch}

É possível para ativos com base nos valores exatos de campos de metadados específicos, como título, descrição e autor. O recurso de pesquisa de texto completo do GQL busca somente os ativos cujo valor de metadados corresponda exatamente à sua consulta de pesquisa. Os nomes das propriedades (por exemplo, autor, título e assim por diante) e os valores distinguem maiúsculas de minúsculas.

| Campo de metadados | Valor e uso da faceta |
|---|---|
| Título | título:John |
| Criador | criador:John |
| Local | local:NA |
| Descrição | descrição:&quot;Imagem de amostra&quot; |
| Ferramenta Criador | criatortool:&quot;Adobe Photoshop CC 2015&quot; |
| Proprietário de direitos autorais | copyrights towner:&quot;Adobe Systems&quot; |
| Contribuinte | colaborador:John |
| Termos de Uso  | usageterms:&quot;CopyRights Reserved&quot; |
| Criado | criado:AAAA-MM-DDTHH |
| Data de expiração | expira:AAAA-MM-DDTHH |
| Hora | hora única:AAAA-MM-DTHH |
| Hora de desligar | tempo limite:AAAA-MM-DTHH |
| Intervalo de tempo(expira em dateontime,offtime) | campo de faceta : limite inferior...upperbound |
| Caminho | /content/dam/&lt;nome da pasta> |
| Título do PDF | pdftitle: &quot;Adobe Document&quot; |
| Assunto | assunto: &quot;Formação&quot; |
| Tags | tags:&quot;Localização E Viagem&quot; |
| Tipo | type:&quot;image\png&quot; |
| Largura da imagem | largura:limite inferior..upperbound |
| Altura da imagem | height:limite inferior..upperbound |
| Person | pessoa:John |

O caminho, limite, tamanho e ordem das propriedades não podem ser OUed com nenhuma outra propriedade.

A palavra-chave para uma propriedade gerada pelo usuário é seu rótulo de campo no editor de propriedades em minúsculas, com espaços removidos.

Estes são alguns exemplos de formatos de pesquisa para consultas complexas:

* Para exibir todos os ativos com vários campos de facetas (por exemplo: title=John Doe e ferramenta criadora = Adobe Photoshop): `title:"John Doe" creatortool : Adobe*`
* Para exibir todos os ativos quando o valor de facetas não for uma única palavra, mas uma sentença (por exemplo: title=Scott Reynolds): `title:"Scott Reynolds"`
* Para exibir ativos com vários valores de uma única propriedade (por exemplo: title=Scott Reynolds ou John Doe): `title:"Scott Reynolds" OR "John Doe"`
* Para exibir ativos com valores de propriedade começando com uma string específica (por exemplo: o título é Scott Reynolds): `title:Scott*`
* Para exibir ativos com valores de propriedade que terminam com uma string específica (por exemplo: o título é Scott Reynolds): `title:*Reynolds`
* Para exibir ativos com um valor de propriedade que contenha uma string específica (por exemplo: título = Sala de reuniões de Basileia): `title:*Meeting*`
* Para exibir ativos que contêm uma determinada string e têm um valor de propriedade específico (por exemplo: procure a string Adobe em ativos com título=João da Silva): `*Adobe* title:"John Doe"`

## Pesquisar ativos de outras ofertas ou interfaces do AEM {#beyondomnisearch}

O Adobe Experience Manager (AEM) conecta o repositório DAM a várias outras soluções AEM para fornecer acesso mais rápido aos ativos digitais e simplificar os fluxos de trabalho criativos. Qualquer descoberta de ativo começa com navegação ou pesquisa. O comportamento de pesquisa permanece basicamente o mesmo em várias superfícies e soluções. Alguns métodos de pesquisa mudam conforme o público-alvo, os casos de uso e a interface do usuário variam nas soluções do AEM. Os métodos específicos estão documentados para as soluções individuais nos links abaixo. As dicas e comportamentos universalmente aplicáveis estão documentados neste artigo.

### Pesquisar ativos no painel Adobe Asset Link {#aal}

Usando o Adobe Asset Link, os profissionais criativos agora podem acessar o conteúdo armazenado nos ativos AEM, sem sair dos aplicativos compatíveis da Adobe Creative Cloud. Os profissionais de criação podem navegar, pesquisar, fazer check-out e fazer check-in de ativos sem problemas usando o painel no aplicativo nos aplicativos da Creative Cloud: Photoshop, Illustrator e InDesign. O Link de ativo também permite que os usuários pesquisem resultados visualmente semelhantes. Os resultados da exibição da pesquisa visual são capacitados pelos algoritmos de aprendizado de máquina do Adobe Sensei e ajudam os usuários a encontrar imagens esteticamente semelhantes. Consulte [pesquisar e procurar ativos](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) usando o Adobe Asset Link.

### Pesquisar ativos no aplicativo de desktop do AEM {#desktopapp}

Os profissionais de criação usam o aplicativo de desktop para tornar os ativos AEM facilmente pesquisáveis e disponíveis em seu desktop local (Win ou Mac). Os profissionais de criação podem revelar facilmente os ativos desejados no Mac Finder ou no Windows Explorer, abertos em aplicativos de desktop e alterados localmente - as alterações são salvas no AEM com uma nova versão criada no repositório. O aplicativo suporta pesquisas básicas usando uma ou mais palavras-chave, * e ? curingas e operador E. Consulte [procurar, pesquisar e visualizar ativos](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) no aplicativo de desktop.

### Search assets in Brand Portal {#brandportal}

Usuários e comerciantes de linha de negócios usam o Brand Portal para compartilhar de forma eficiente e segura os ativos digitais aprovados com suas equipes internas, parceiros e revendedores estendidos. See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### Pesquisar imagens do Adobe Stock {#adobestock-1}

Na interface do usuário do AEM, os usuários podem pesquisar ativos do Adobe Stock e licenciar os ativos necessários. Adicione `Location: Adobe Stock` no campo Omnisearch. Você também pode usar o painel **[!UICONTROL Filtros]** para localizar todos os ativos licenciados ou não ou pesquisar um ativo específico usando o número de arquivo do Adobe Stock. Consulte [Gerenciar imagens do Adobe Stock no AEM](/help/assets/aem-assets-adobe-stock.md#usemanage).

### Pesquisar ativos do Dynamic Media {#dynamicmedia}

Você pode filtrar por imagens do Dynamic Media selecionando **[!UICONTROL Dynamic Media]** > **[!UICONTROL Conjuntos]** no painel **[!UICONTROL Filtros]** . Filtra e exibe ativos como conjuntos de imagens, carrosséis, conjuntos de mídia mista e conjuntos de rotação. Durante a criação de páginas da Web, os autores podem pesquisar por conjuntos no Localizador de conteúdo. Um filtro para conjuntos está disponível em um menu pop-up.

### Pesquisar ativos no Localizador de conteúdo ao criar páginas da Web {#contentfinder}

Os autores podem usar o Localizador de conteúdo para pesquisar no repositório do DAM os ativos relevantes e usar os ativos nas páginas da Web que eles criam.

<!-- Authors can also use the Connected Assets functionality to search for assets that are available on a remote AEM deployment. Authors can then use these assets in web pages on a local AEM deployment. See [use remote assets](use-assets-across-connected-assets-instances.md#use-remote-assets).
-->

### Pesquisar coleções {#collections}

O recurso de pesquisa do AEM oferece suporte à pesquisa de coleções e à pesquisa de ativos em uma coleção. Consulte Coleções [de pesquisa](/help/assets/manage-collections.md).

## Asset selector {#assetselector}

O seletor de ativos permite que você pesquise, filtre e navegue pelos ativos DAM de uma maneira especial. O seletor de ativos está disponível em `https://[aem_server]:[port]/aem/assetpicker.html`. Você pode buscar os metadados dos ativos selecionados usando o seletor de ativos. Você pode iniciá-lo com parâmetros de solicitação suportados, como tipo de ativo (imagem, vídeo, texto) e modo de seleção (seleções únicas ou múltiplas). Esses parâmetros definem o contexto do seletor de ativos para uma instância de pesquisa específica e permanecem intactos durante toda a seleção.

O seletor de ativos usa a mensagem HTML5 `Window.postMessage` para enviar dados do ativo selecionado para o destinatário. O seletor de ativos é baseado no vocabulário do seletor de fundações de Granite. Por padrão, o seletor de ativos opera no modo Procurar.

Você pode passar os seguintes parâmetros de solicitação em um URL para iniciar o seletor de ativos em um contexto específico:

| Nome | Valores | Exemplo | Propósito |
|---|---|---|---|
| sufixo do recurso (B) | Caminho da pasta como o sufixo do recurso no URL:[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | Para iniciar o seletor de ativos com uma pasta específica selecionada, por exemplo, com a pasta /content/dam/we-retail/en/activity selecionada, o URL deve ter a seguinte forma: [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | Se você precisar que uma pasta específica seja selecionada quando o seletor de ativos for iniciado, passe-o como um sufixo de recurso. |
| modo | único, múltiplo | [https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single) | No modo múltiplo, você pode selecionar vários ativos simultaneamente usando o seletor de ativos. |
| mimetype | mimetype(s) (`/jcr:content/metadata/dc:format`) de um ativo (curinga também compatível) | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png)</li></ul> | Use-o para filtrar ativos com base em tipos MIME |
| caixa de diálogo | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | Use esses parâmetros para abrir o seletor de ativos como Caixa de diálogo Granite. Essa opção só é aplicável quando você inicia o seletor de ativos por meio do campo Caminho de Granite e o configura como URL pickerSrc. |
| tipo de ativo (S) | imagens, documentos, multimídia, arquivos | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | Use essa opção para filtrar os tipos de ativos com base no valor passado. |
| root | &lt;caminho_da_pasta> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities) | Use essa opção para especificar a pasta raiz do seletor de ativos. Nesse caso, o seletor de ativos permite que você selecione apenas ativos secundários (diretos/indiretos) na pasta raiz. |

Para acessar a interface do seletor de ativos, acesse `https://[AEM server]:[port]/aem/assetpicker`. Navegue até a pasta desejada e selecione um ou mais ativos. Como alternativa, procure o ativo desejado na caixa Omnisearch, aplique o filtro conforme necessário e selecione-o.

![Procurar e selecionar ativo no seletor de ativos](assets/assetpicker.png)

Procurar e selecionar ativo no seletor de ativos

## Limitações {#limitations}

O recurso de pesquisa nos ativos AEM tem as seguintes limitações:

* Não insira um espaço à esquerda na consulta de pesquisa; caso contrário, a pesquisa não funcionará.
* O AEM pode continuar a mostrar o termo de pesquisa depois que você seleciona as propriedades de um ativo dos resultados pesquisados e cancela a pesquisa (CQ-4273540).
* Ao procurar pastas ou arquivos e pastas, os resultados da pesquisa não podem ser classificados em nenhum parâmetro.
* Se você pressionar return sem vincular nada na barra Omnisearch, o AEM retornará uma lista de somente arquivos e não pastas. Se você pesquisar especificamente por pastas sem usar uma palavra-chave, o AEM não retornará nenhum resultado.

Pesquisa visual ou pesquisa de semelhança tem as seguintes limitações:

* A pesquisa visual funciona melhor com repositórios maiores. Embora não haja um número mínimo de imagens necessário para bons resultados, a qualidade das correspondências com algumas imagens pode não ser tão boa quanto as correspondências de um repositório grande.
* Não é possível alterar o modelo ou treinar o AEM para encontrar imagens semelhantes. Por exemplo, adicionar ou remover tags inteligentes a alguns ativos não altera o modelo. Os ativos são excluídos dos resultados de pesquisa visualmente semelhantes.

## Dicas de pesquisa {#tips}

* Ao monitorar o status da revisão de ativos, use a opção apropriada para descobrir quais ativos estão aprovados ou quais ativos estão pendentes de aprovação.
* Use o predicado Insights para pesquisar ativos suportados com base em suas estatísticas de uso obtidas de vários aplicativos Creative. Os dados de uso são agrupados em Pontuação de uso, Impressões, Cliques e Canais de mídia nos quais os ativos aparecem categorias.
* Use a caixa de seleção para selecionar todos os resultados de pesquisa ou os resultados de pesquisa filtrados para operar na seleção. Seleciona todos os ativos pesquisados independentemente de quantos ativos são exibidos na exibição atual do usuário. Por exemplo, você pode baixar todos os ativos selecionados, atualizar as propriedades de metadados em massa para todos os ativos selecionados ou adicionar ativos selecionados a uma coleção.
* Para pesquisar ativos que não contenham os metadados obrigatórios, consulte os metadados [](#mandatorymetadata)obrigatórios.
* A pesquisa usa todos os campos de metadados. Uma pesquisa genérica, como a pesquisa por 12, geralmente retorna muitos resultados. Para obter melhores resultados, use aspas duplas (não simples) ou verifique se o número está contíguo a uma palavra sem um caractere especial (por exemplo, *shoe12*).
* A pesquisa de texto completo oferece suporte a operadores como -, ^ e assim por diante. Para pesquisar essas letras como literais de string, coloque a expressão de pesquisa entre aspas duplas. Por exemplo, use &quot;Notebook - Beauty&quot; em vez de Notebook - Beauty.
* Se os resultados da pesquisa forem demais, limite o [escopo da pesquisa](#scope) para zero nos ativos desejados. Funciona melhor quando você tem alguma ideia de como procurar melhor os ativos desejados, por exemplo, tipo de arquivo específico, local específico, metadados específicos e assim por diante.

* **Marcação**: As tags ajudam a categorizar ativos que podem ser pesquisados e pesquisados com mais eficiência. A marcação ajuda a propagar a taxonomia apropriada para outros usuários e fluxos de trabalho. O AEM oferece métodos para marcar automaticamente ativos usando os serviços inteligentes e artificiais do Adobe Sensei que continuam melhorando a identificação dos ativos com o uso e o treinamento. Quando você pesquisa ativos, as tags inteligentes são fatoradas se o recurso estiver ativado em sua conta. Funciona juntamente com a funcionalidade de pesquisa incorporada. Consulte Comportamento [da](#searchbehavior)pesquisa. Para otimizar a ordem na qual os resultados da pesquisa são exibidos, é possível [aumentar a classificação](#searchrank) de pesquisa de alguns ativos selecionados.

* **Indexação**: Somente metadados indexados e ativos são retornados nos resultados da pesquisa. Para melhor cobertura e desempenho, assegure a indexação correta e siga as práticas recomendadas. Consulte [indexação](#searchindex).

## Alguns exemplos ilustrando a pesquisa {#samples}

Use aspas duplas em torno de palavras-chave para localizar ativos que contenham a frase exata na ordem exata, conforme especificado pelo usuário.

![Comportamento de pesquisa com e sem aspas](assets/search_with_quotes.gif)

Comportamento de pesquisa com e sem aspas

**Pesquisar com um asterisco** curinga: Para ampliar a pesquisa, use um asterisco antes ou depois da palavra de pesquisa para corresponder a qualquer número de caracteres. Por exemplo, a pesquisa por executar sem um asterisco não retorna ativos que contenham qualquer variação da palavra (incluindo nos metadados). Um asterisco substitui qualquer número de caracteres. Por exemplo,

* `run` retorna ativos com uma palavra-chave de execução exata
* `run*` retorna ativos com execução, execução, desistência e assim por diante.
* `*run` retorna para trás, execute-o novamente e assim por diante.
* `*run*` retorna todas as combinações possíveis.

![Ilustrando o uso do curinga de asterisco na pesquisa de Ativos usando um exemplo](assets/search_with_asterisk_run.gif)

Ilustrando o uso do curinga de asterisco na pesquisa de Ativos usando um exemplo

**Pesquisa com curinga de ponto de interrogação**: Para ampliar a pesquisa, use um ou mais &#39;?&#39; caracteres para corresponder ao número exato de caracteres. Por exemplo, na ilustração a seguir,

* `run???` não corresponde a nenhum ativo.

* `run????` corresponde à palavra `running` com quatro caracteres depois `run`.

* `??run` corresponde à palavra `rerun` com dois caracteres antes `run`.

![Ilustrando o uso do caractere curinga de ponto de interrogação na pesquisa de Ativos usando um exemplo](assets/search_with_questionmark_run.gif)

Ilustrando o uso do caractere curinga de ponto de interrogação na pesquisa de Ativos usando um exemplo

**Excluir uma palavra-chave**: Use o traço para procurar ativos que não contêm uma palavra-chave. Por exemplo, `running -shoe` a consulta retorna ativos que contêm `running`, mas não `shoe`. Da mesma forma, `camp -night` a consulta retorna ativos que contêm `camp` , mas não `night`. Observe que `camp-night` a consulta retorna ativos que contêm `camp` e `night`.

![Uso do traço para pesquisar ativos que não contenham uma palavra-chave](assets/search_dash_exclude_keyword.gif)excluída *Figura:Uso do traço para pesquisar ativos que não contenham uma palavra-chave excluída*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).

### Sort on Name column {#sortbyname}

In list view, you can sort the search results just as you can sort assets in any folder. Sorting does not work on the `Name` column by default. To sort by the `Name` column, overlay `/libs/dam/gui/content/commons/availablecolumns` and change the value of sortable to `True`.

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses smart tagging and requires AEM 6.5.2.0 or later. After configuring smart tagging functionality, follow these steps.

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
1. Apply Smart Tags to the assets in your AEM repository. See [how to configure smart tags](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html).
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

<!-- Check with gklebus if this customization is possible in Cloud Service now

### Custom predicates to filter search results {#custompredicates}

Predicates are used to create facets. Administrators can customize the search facets in the Filters panel using pre-configured predicates. These predicates can be customized using overlays. See [create custom predicates](/help/assets/searchx.md).

You can search for digital assets based on one or more of the following properties. Filters that apply on some of these properties are available by default and some other filters can be custom-created to apply on the other properties.

| Search field | Search property values |
|---|---|
| MIME Types | Images, Documents, Multimedia, Archives, or Other. |
| Last Modified | Hour, Day, Week, Month, or Year. |
| File Size | Small, Medium, or Large. |
| Publish Status | Published or Unpublished. |
| Approved Status | Approved or Rejected. |
| Orientation | Horizontal, Vertical, or Square. |
| Style | Color, or Black & White. |
| Video Height | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Width | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Format | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Value is stored in the metadata of the source video and any renditions. |
| Video Codec | x264. Value is stored in the metadata of video renditions only. |
| Video Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Audio Codec | Libvorbis, Lame MP3, AAC Encoding. Value is stored in the metadata of video renditions only. |
| Audio Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |

-->

## Trabalhar com resultados de pesquisa de ativos {#aftersearch}

Depois de ver alguns ativos pesquisados que correspondem aos seus critérios, você pode realizar as seguintes tarefas típicas com ou executar as seguintes ações nestes resultados de pesquisa:

* Exibir propriedades de metadados e outras informações.
* Baixe um ou mais ativos.
* Use as Ações da área de trabalho para abrir esses ativos no aplicativo da área de trabalho.
* Criar coleções inteligentes.

### Classificar resultados pesquisados {#sort}

A classificação dos resultados da pesquisa ajuda a descobrir o ativo necessário mais rapidamente. A classificação dos resultados da pesquisa funciona na exibição de lista e somente quando você seleciona **[!UICONTROL [Arquivos](#searchui)]**no painel**[!UICONTROL  Filtros ]**. O AEM Assets usa a classificação do lado do servidor para classificar rapidamente todos os ativos (independentemente do número) em uma pasta ou nos resultados de uma consulta de pesquisa. A classificação do servidor fornece resultados mais rápidos e precisos do que a classificação do cliente.

Na exibição de lista, você pode classificar os resultados da pesquisa da mesma forma que pode classificar os ativos em qualquer pasta. A classificação funciona nessas colunas — Título, Status, Dimensões, Tamanho, Classificação, Uso, (Data) Modificado, (Data) Publicado, Fluxo de trabalho e Finalizado.

Consulte [configurar a classificação na coluna](#sortbyname)Nome. Para obter as limitações da funcionalidade de classificação, consulte [limitações](#limitations).

### Verificar informações detalhadas de um ativo {#checkinfo}

Você pode verificar informações detalhadas de ativos pesquisados na página de resultados da pesquisa.

Para ver todos os metadados de um ativo, selecione o ativo e clique em **[!UICONTROL propriedades]** na barra de ferramentas.

Para verificar os comentários em um ativo ou histórico de versão de um ativo, clique no ativo para abrir uma visualização de grande porte. Abra a linha do tempo no painel esquerdo e selecione **[!UICONTROL Comentários]** ou **[!UICONTROL Versões]**. Também é possível classificar a atividade da linha do tempo como comentários ou versões em ordem cronológica.

![Classificar entradas de linha do tempo para um ativo de pesquisa](assets/sort_timeline_search_results.gif)

Classificar entradas de linha do tempo para um ativo de pesquisa

### Baixar ativos pesquisados {#download}

Você pode baixar os ativos pesquisados e suas representações da mesma forma que baixa ativos comuns de pastas. Selecione um ou mais ativos dos resultados da pesquisa e clique em **[!UICONTROL Download]** na barra de ferramentas.

### Propriedades de metadados de atualização em massa {#metadataupdates}

É possível fazer atualizações em massa nos campos de metadados comuns de vários ativos. Nos resultados da pesquisa, selecione um ou mais ativos. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas e atualize os metadados conforme necessário. Clique em **[!UICONTROL Salvar e fechar]** quando terminar. Os metadados existentes anteriormente nos campos atualizados são substituídos.

Para os ativos que estão disponíveis em uma única pasta ou coleção, é mais fácil [atualizar os metadados em massa](/help/assets/manage-metadata.md#manage-assets-metadata). Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é mais rápido atualizar os metadados em massa por meio da pesquisa.

### Coleções inteligentes {#collections-1}

Uma coleção é um conjunto ordenado de ativos que podem incluir ativos de locais diferentes, pois as coleções contêm somente referências a esses ativos. As coleções são dos dois tipos a seguir:

* Uma lista de referência estática de ativos, pastas e outras coleções.
* Uma lista dinâmica (coleção inteligente) que preenche ativos na coleção com base em critérios de pesquisa.

Você pode criar coleções inteligentes com base nos critérios de pesquisa. No painel **[!UICONTROL Filtros]** , selecione **[!UICONTROL Arquivos]** e clique em **[!UICONTROL Salvar coleção]** inteligente. Consulte [gerenciar coleções](/help/assets/manage-collections.md).

## Resultados de pesquisa inesperados {#unexpectedresults}

**Procurar metadados** ausentes: Ao pesquisar ativos que não possuem os metadados obrigatórios, o AEM pode exibir alguns ativos que têm metadados válidos. Metadados ausentes são detectados e reportados com base na propriedade de metadados indexados. Mesmo se os metadados do ativo forem fixos, eles continuarão a mostrar como metadados ausentes até que ocorra a reindexação. Consulte metadados [](/help/assets/metadata-schemas.md#defining-mandatory-metadata)obrigatórios.

**Muitos resultados** de pesquisa: Para evitar obter muitos resultados de pesquisa, considere limitar os resultados da pesquisa. Por exemplo, para pesquisar ativos no DAM, selecione `Location:Assets` na barra Omnisearch. Para obter mais filtros de pesquisa, consulte o [escopo da pesquisa](#scope).

<!-- Another reason to get more than expected search results can be use of smarts tags. See [search behavior with smart tags](#withsmarttags). 
-->

<!--
**Partially related or unrelated search results**: AEM may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

**Nenhuma sugestão de preenchimento automático para ativos** carregados recentemente: Os metadados (títulos, tags e assim por diante) dos ativos carregados recentemente não estão disponíveis imediatamente como sugestões quando você começa a digitar uma palavra-chave de pesquisa na barra Omnisearch. Os ativos AEM esperam até o término de um período limite (uma hora por padrão) antes de executar um trabalho em segundo plano para indexar os metadados de todos os ativos recentemente carregados ou atualizados e, em seguida, adicionam os metadados à lista de sugestões.

**Nenhum resultado** de pesquisa: Se o AEM e exibir uma página vazia para uma consulta de pesquisa, os seguintes motivos podem ser:

* Não existem ativos que correspondam à sua consulta.
* Você adiciona um espaço em branco antes da consulta de pesquisa. É uma limitação [](#limitations)conhecida.

* Um campo de metadados não suportado contém a palavra-chave que você pesquisa. Nem todos os campos de metadados são considerados para pesquisas. Consulte [escopo](#scope).
* O tempo de ativação e de desativação é configurado para o ativo e a pesquisa é feita durante o tempo de inatividade do ativo.

**O filtro/predicado de pesquisa não está disponível**: Se uma personalização esperada para pesquisar filtros não estiver disponível na interface do usuário, entre em contato com o administrador para verificar se a personalização foi implementada para todos os autores e no servidor de produção que você está usando. É possível que a configuração esteja incorreta.

## Solução de problemas relacionados à pesquisa {#troubleshoot}

Veja abaixo os problemas e a possível linha de ação:

* Se um filtro/predicado de pesquisa esperado não estiver visível, entre em contato com o administrador.
* Ao pesquisar por imagens visualmente semelhantes, às vezes uma imagem esperada pode estar ausente dos resultados da pesquisa. Verifique se esses ativos estão indexados e com tags inteligentes.
* Ao pesquisar por imagens visualmente semelhantes, às vezes uma imagem aparentemente irrelevante pode ser exibida nos resultados da pesquisa. O AEM exibe quantos ativos potencialmente relevantes forem possíveis. Imagens menos relevantes, se houver, são adicionadas aos resultados, mas com uma classificação de pesquisa mais baixa. A qualidade das correspondências e a relevância dos ativos pesquisados diminuem à medida que você percorre os resultados da pesquisa.
