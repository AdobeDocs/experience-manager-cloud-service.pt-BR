---
title: Pesquisar práticas recomendadas do  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Práticas recomendadas para pesquisar, localizar e recuperar metadados de ativos no aplicativo.
contentOwner: KK
exl-id: 446692de-5cea-4dbd-a98e-ec5177c7017e
feature: Best Practices
role: User
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '2527'
ht-degree: 2%

---

# Práticas recomendadas de pesquisa do AEM Assets

O [!DNL Adobe Experience Manager Assets] fornece métodos de pesquisa de ativos robustos que ajudam a alcançar maior velocidade do conteúdo. Às vezes, encontrar o ativo certo pode ser árduo e demorado. Portanto, o recurso de pesquisa de ativos no [!DNL Adobe Experience Manager Assets] é fundamental para o uso de um sistema de gerenciamento de ativos digitais - seja para uso posterior por criadores, para o gerenciamento robusto de ativos por usuários empresariais e profissionais de marketing ou para administração por administradores do DAM.

Este documento de ajuda contém as práticas recomendadas de pesquisa do AEM com a ajuda de vários cenários para ajudar os usuários do AEM a realizar pesquisa básica a avançada.

## Acessar a pesquisa do Experience Manager {#access-experience-manager-search}

A seguir estão as etapas básicas a serem executadas no Experience Manager antes de você iniciar sua pesquisa:

* Na **exibição de Administrador**, vá para Assets > Arquivos no Experience Manager e clique no ícone de pesquisa na barra superior. Como alternativa, use uma barra (/) para abrir o campo Omni Search.
Na **exibição do Assets**, a barra de pesquisa está visível na parte superior e pode ser acessada diretamente.
* `Location:Assets` e `Path:/content/dam` são pré-selecionados para limitar o escopo de pesquisa ao seu repositório do Experience Manager Assets. Se você navegar para qualquer outra pasta, `Path:/content/dam/<folder name>` será exibido no campo Pesquisa Omni para limitar o escopo de pesquisa à pasta atual.

## Pesquisa básica {#basic-search}

**Cenário 1: executar uma pesquisa básica usando `classic car` como palavra-chave de pesquisa.**

A pesquisa por palavra-chave não diferencia maiúsculas de minúsculas e é uma pesquisa de texto completo nos campos de metadados incluídos no índice de Ativo *pesquisa de texto completo* (configurável na definição do índice). Se mais de uma palavra-chave for usada, **AND será o operador padrão entre as palavras-chave; portanto, ele considerará uma pesquisa por &#39;carro clássico&#39; como &#39;carro AND clássico&#39;**.

Os resultados da pesquisa que correspondem a todos os termos de pesquisa em campos de metadados são exibidos primeiro, seguido pelos resultados da pesquisa que correspondem a qualquer um dos termos de pesquisa nas tags inteligentes. A ordem aproximada de exibição dos resultados da pesquisa é:

1. Correspondências de `Classic Car` nos vários campos de metadados.
2. Correspondências de `Classic Car` em tags inteligentes.
3. Correspondências de `Classic` ou de `Car` nas marcas inteligentes.

Especifique `classic car` como a palavra-chave de pesquisa e clique em Pesquisar. É possível exibir as sugestões de pesquisa em uma lista suspensa à medida que você digita a palavra-chave. As sugestões de pesquisa se baseiam no conteúdo do índice de pesquisa na implantação do Experience Manager. Se não conseguir exibir os ativos apropriados no menu suspenso, pressione a tecla Enter para exibir a lista de resultados. Os resultados são classificados por relevância, a partir das correspondências mais próximas.

<!--![Performing basic search method 1](assets/simple-search-1.png)-->

Você pode tornar a pesquisa mais específica adicionando sua palavra-chave de pesquisa entre aspas duplas (&quot; &quot;). Essa pesquisa inclui apenas Assets que contêm os termos especificados juntos. Os critérios de pesquisa parecem - `"classic car"`. Portanto, os resultados da pesquisa com os termos `classic` e `car` são mostrados.

<!--![Finding exact match](assets/simple-search-2.png)-->

A pesquisa exibe resultados semelhantes se você também estiver trabalhando na **[!UICONTROL exibição do Assets]**.

>[!VIDEO](https://video.tv.adobe.com/v/3425489)

## Arquivos e pastas {#files-folders}

**Cenário 2: procure todos os arquivos usando a palavra-chave `classic car` na pasta `automobile`.**

O filtro de arquivos e pastas ajuda a restringir a pesquisa. Use as opções Arquivos, Pastas ou Arquivos e pastas disponíveis na lista suspensa com base em sua necessidade. A opção para escolher entre Arquivos, Pastas ou Arquivos e Pastas está acessível somente no **[!UICONTROL modo de exibição de Administrador]**. No **[!UICONTROL modo de exibição do Assets]**, vá para [!UICONTROL Caminho] e procure a pasta em que deseja realizar uma pesquisa.

* Use a opção **[!UICONTROL Arquivos]** quando precisar pesquisar especificamente por arquivos em um caminho específico dentro do repositório. Não é necessário pesquisar pastas no caminho definido.
* Use a opção **[!UICONTROL Pastas]** quando precisar limitar sua pesquisa a pastas em um caminho específico.
* Use a opção **[!UICONTROL Arquivos e pastas]** se precisar pesquisar todos os ativos disponíveis no caminho especificado no repositório.

Para chegar a esse cenário, execute as etapas abaixo:

1. Especifique `classic car` como a palavra-chave de pesquisa e clique em Pesquisar.
2. Clique em Filtros e defina o caminho da pasta `automobile`. Por exemplo, `/content/dam/multiple-assets/automobile`
Selecione a pasta no caminho e navegue até a pasta desejada se desejar pesquisar na pasta específica.
3. Selecione Arquivos na lista suspensa para exibir todos os arquivos com a palavra-chave `classic car`.

<!--![Search using files and folders](assets/files-folders.png)-->

>[!VIDEO](https://video.tv.adobe.com/v/3425487)

## Operadores {#operators}

**Cenário 3: pesquise por palavras-chave `Classic Car` ou `Car` usando várias combinações de operador para restringir sua pesquisa.**

Para executar o cenário acima no **[!UICONTROL modo de exibição de Administrador]**, você pode usar uma combinação de vários operadores para aprimorar sua experiência de pesquisa. Os operadores compatíveis são:

### Operador AND {#and-operator}

O operador AND é o operador padrão entre duas palavras-chave na Pesquisa Omni. Por exemplo, quando você digita `classic car` na barra de pesquisa, os resultados com as palavras-chave `classic` e `car` aparecem nos resultados da pesquisa, por padrão.

![Pesquisar usando operador AND](assets/simple-search-1.png)

### Operador OR {#or-operator}

Quando quiser ser específico com os resultados da pesquisa e quiser uma opção nos resultados da pesquisa, você poderá usar o operador OU. Por exemplo, a palavra-chave `classic OR car` fornece resultados de pesquisa com qualquer uma das palavras-chave em seus metadados.

![Pesquisar usando operador OR](assets/or-operator.png)

### Operador NOT {#not-operator}

Quando quiser recuperar os resultados, excluindo algumas palavras-chave, você pode usar o operador NOT. O operador NOT usa o hífen (-) para direcionar a pesquisa do AEM sobre o que excluir dos resultados da pesquisa. Por exemplo, a consulta de pesquisa `car - classic` que especifica metadados que contêm `car`, mas exclui `classic`.

![Pesquisar usando operador NOT](assets/not-operator.png)

Da mesma forma, você pode procurar todos os carros, mas não jipe. A consulta tem a seguinte aparência: `car - jeep`. Ele exibe todos os ativos com metadados `car`, mas exclui ativos com metadados `jeep`.

![Pesquisar usando operador NOT](assets/images-jeep.png)

**[!UICONTROL O modo de exibição do Assets]** não oferece suporte ao uso de Operadores.

## Curingas {#wildcards}

Os curingas são usados para substituir um ou mais caracteres na pesquisa. Para executar o cenário acima no **[!UICONTROL modo de exibição de Administrador]**, você pode usar uma combinação de vários curingas para aprimorar sua experiência de pesquisa. Há dois curingas usados para executar a pesquisa - Ponto de interrogação (?) e Asterisco (*). O símbolo de ponto de interrogação é usado para pesquisar um único caractere, enquanto o símbolo de asterisco é usado para pesquisar vários caracteres.

### Ponto de interrogação (?) {#question-mark}

O símbolo de ponto de interrogação pode ser usado como operador condicional para facilitar a pesquisa no Experience Manager.

* A consulta `car?` corresponde a palavra com um caractere após o carro. Por exemplo, carrinho.
* A consulta `?car` corresponde a palavra com um caractere antes do carro. Por exemplo, cicatriz.
* A consulta `car????` corresponde à palavra com quatro caracteres após o carro. Por exemplo, lavagem de carro.

### Asterisco (*) {#asterisk}

O asterisco é um operador curinga usado para ampliar sua pesquisa digitando menos caracteres. Quando você conhece os caracteres iniciais do ativo que está pesquisando, mas não sabe o resto, é possível usar o operador asterisco na pesquisa. Por exemplo, a consulta `*car` retorna todos os ativos com o carro de sufixo disponível em seus metadados. Os resultados podem ser carro clássico, carro esportivo, clássico e carro esportivo, e assim por diante. Abaixo estão alguns exemplos de como usar o operador asterisco de várias maneiras:

* `*car*` retorna todas as combinações possíveis.
* `car*` retorna ativos com lavagem de carro, transportadora, transporte e assim por diante.
* `*car` retorna ativos com carro moderno, carro esportivo e assim por diante.

>[!VIDEO](https://video.tv.adobe.com/v/3425488)

**[!UICONTROL O modo de exibição do Assets]** não oferece suporte ao uso de Curingas.

## Filtros {#filters}

O Adobe Experience Manager fornece vários filtros de pesquisa que você pode usar para refinar e segmentar sua pesquisa usando uma consulta com escopo. Quando não tiver certeza sobre o título ou a metadescrição de um ativo, você pode usar vários filtros de pesquisa para tornar sua pesquisa mais relevante. Você pode usar filtros de pesquisa com ou sem digitar uma palavra-chave. Para abrir o painel de filtros no **[!UICONTROL modo de exibição de Administrador]**, clique no ícone **GlobalNav** e selecione **[!UICONTROL Filtros]**. Enquanto isso, para abrir o painel de filtros no **[!UICONTROL modo de exibição do Assets]**, clique em [!UICONTROL Filtros] ao lado da barra de pesquisa.

![Painel de filtros](assets/filters.png)

Você pode selecionar um ou vários filtros para refinar sua pesquisa no Adobe Experience Manager.
<!--The following filters are available out of the box for all the users of Experience Manager:

* File Type Search Filters  
* File Size Search Filters 
* Date of Creation 
* Created by 
* Last Modified date 
* Last Modified by 
* Search by Language 
* Search by Status 
* Search based on Orientation 
* Search by Style 
* Search based on insights 
* Search by Adobe Stock 
* Color specific Asset search 
* Content fragment model 
 -->

<!--**Scenario 5: Search for an Asset named 'classic car' in Black color which has either meta description or a similar asset in Japanese language.**  
 
To perform a search on such a requirement, type 'classic car' in the search bar.  Navigate to the filters panel and expand the language search filter drop-down. Type "ja-jp", which represents the Japanese language. Expand the 'Asset Color' filter and select black color or add the hexadecimal code for the black color (#000000).

![Filter example 1](assets/filter-1.png)
-->

**Cenário 4: procure documentos do tipo PDF não publicados com a palavra-chave `classic car` neles.**

Execute as seguintes etapas no **[!UICONTROL Modo de exibição de Administração]**:

1. Digite `classic car` na barra de pesquisa.
1. Vá para Filtros. Em [!UICONTROL Tipo de Arquivo], expanda [!UICONTROL Documentos] e expanda [!UICONTROL Processamento de Texto].
1. Selecione [!UICONTROL PDF].
1. Ir para [!UICONTROL Status] > [!UICONTROL Publicar] > [!UICONTROL Não publicado].

<!--![Filter example 2](assets/filter-2.png)-->

Execute as seguintes etapas no **[!UICONTROL modo de exibição do Assets]**:

1. Digite `classic car` na barra de pesquisa.
1. Vá para Filtros. Em [!UICONTROL Tipo MIME], selecione [!UICONTROL PDF].
1. Vá para [!UICONTROL Status do ativo], selecione [!UICONTROL Todos] para incluir todos os ativos publicados e não publicados.

**Cenário 5: pesquisar todas as imagens, exceto PNG**

Quando não tiver certeza sobre o título ou a metadescrição de um ativo, você pode usar vários filtros de pesquisa para tornar sua pesquisa mais relevante. Por exemplo, para pesquisar ativos no **[!UICONTROL modo de exibição de Administrador]**, siga as etapas abaixo:

1. Ir para filtros de pesquisa.
1. Vá para Filtros. Em [!UICONTROL Tipo de Arquivo], expanda [!UICONTROL Imagens] e selecione [!UICONTROL Web habilitado]
1. Desmarque PNG.

<!--![Search all images except jeep](assets/images-png.png)-->

Para pesquisar ativos usando o cenário mencionado no **[!UICONTROL modo de exibição do Assets]**, siga as etapas abaixo:

1. Ir para filtros de pesquisa.
1. Vá para Filtros. Em [!UICONTROL Tipo MIME], selecione todos os tipos MIME fornecidos, mas desmarque PNG.

>[!VIDEO](https://video.tv.adobe.com/v/3425486)

## Pesquisa avançada {#advanced-search}

A pesquisa no AEM permite criar consultas de pesquisa complexas com menos esforço. Veja a seguir os vários exemplos para ajudar você a criar consultas de pesquisa complexas:

**Cenário 6: procure todos os documentos no repositório do Experience Manager com `classic car` em seus metadados. O conteúdo do documento deve conter a palavra-chave `classic car`.**

O Adobe Experience Manager permite adicionar vários critérios à pesquisa. Você pode usar uma combinação de palavras-chave, operadores e filtros para restringir os resultados da pesquisa.

Para executar uma pesquisa para o cenário 6:

1. Digite a palavra-chave `classic car` na barra de pesquisa.
2. Navegue até o painel Filtros e selecione Documentos em Tipo de arquivo.
3. Refine sua pesquisa usando o curinga asterisco. Digite `"classic car"` para pesquisar todos os ativos que contêm a palavra-chave `classic car`.

<!--![Scenario 6](assets/scenario-6.png)-->

Não é possível executar o cenário 6 no **[!UICONTROL modo de exibição do Assets]**, pois ele não oferece suporte ao uso de Curingas.

**Cenário 7: procure todos os documentos no repositório do Experience Manager em que o conteúdo do documento deve incluir `car`, mas excluir `classic`. A mesma condição se aplica aos metadados de um ativo.**

Para executar uma pesquisa para o cenário 7:

Digite a palavra-chave `car - classic` na barra de pesquisa. Navegue até o painel Filtros e selecione Documentos em Tipo de arquivo. A ordem de prioridade da pesquisa é baseada no seguinte:
Prioridade 1: Metadados
Prioridade 2: tags inteligentes

<!--![Scenario 7](assets/scenario-7.png)-->

Não é possível executar o cenário 7 no **[!UICONTROL modo de exibição do Assets]**, pois ele não oferece suporte ao uso de Curingas.

<!--
**Scenario 9: Search for all images except PNG**

When you are unsure about the title or meta description of an asset, you can use various search filters to make your search more relevant. Follow the steps below:

1. Go to search filters. 
1. Under [!UICONTROL File Type], expand [!UICONTROL Images] and select [!UICONTROL Web enabled]
1. Deselect PNG.

**Method 1:** Go to search bar and type `images - PNG`. All the images appear excluding PNG.

**Method 2:** Go to search filters. Under [!UICONTROL File Type], expand [!UICONTROL Images] > select [!UICONTROL Web enabled] > deselect PNG.

![Search all images except jeep](assets/images-jeep.png)
-->

**Cenário 8: pesquisar marcas de metadados com jipe de metadados**

Você pode capturar um critério específico usando vários filtros de pesquisa. Tag é uma palavra-chave atribuída a um ativo para torná-lo identificável entre um grande número de ativos. Por exemplo, neste cenário, pesquise por ativos com tags *jeep*. Para fazer isso, digite `tags:jeep` na barra de pesquisa. Somente os ativos que atendem a esse critério são listados nos resultados da pesquisa.

<!--![Search using tags](assets/search-tags.png)-->

A pesquisa exibe resultados semelhantes se você também estiver trabalhando na **[!UICONTROL exibição do Assets]**.

>[!VIDEO](https://video.tv.adobe.com/v/3425490)

**Cenário 9: encontrar correspondência semelhante para carro vermelho**

Ao realizar a pesquisa no AEM, você pode filtrar os resultados mostrando ativos semelhantes aos selecionados. Você pode usar a opção **Localizar semelhante** para restringir sua pesquisa à correspondência exata ou semelhante do ativo pesquisado. Isso ajuda a encontrar ativos que têm tags inteligentes semelhantes ao ativo selecionado. Por exemplo, quando você deseja pesquisar por ativos semelhantes, execute as seguintes etapas:

1. Pesquise o ativo de acordo com sua necessidade.
1. Passe o mouse sobre o ativo > clique nas reticências > selecione [!UICONTROL Localizar semelhante].
ou
Selecione o ativo > navegue até as reticências na parte superior direita > selecione [!UICONTROL Localizar semelhante].

   ![Localizar semelhante](assets/find-similar.png)

1. Observe a barra de pesquisa. A miniatura do ativo selecionado aparece na barra de pesquisa, indicando o requisito de pesquisa. Como resultado, ele retorna ativos com tags inteligentes semelhantes.

Execute as seguintes etapas no **[!UICONTROL modo de exibição do Assets]**:

1. Pesquise o ativo de acordo com sua necessidade.
1. Selecione a imagem > navegue até a opção [!UICONTROL Localizar imagem semelhante] na barra de navegação na parte superior.
Isso leva você à coleção de ativos com cores e metadados semelhantes.

## Aspectos da pesquisa personalizada {#custom-search-facets}

Os aspectos de pesquisa no Adobe Experience Manager permitem pesquisar ativos de várias maneiras, em vez de em uma única ordem pré-determinada ou taxonômica. Você pode personalizar os aspectos de pesquisa e adicionar predicados de acordo com sua necessidade. Leia [Aspectos da Pesquisa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=pt-BR#) para obter o guia passo a passo sobre como adicionar um predicado personalizado.

<!--**Scenario 10: Search assets based on Sku ID**
to be added later
-->

**Cenário 10: pesquisar ativos específicos com base em sua última data de modificação ou expiração**

Restrições de data permitem restringir a pesquisa personalizada a um período específico, por exemplo, usando os filtros de pesquisa de período. Para pesquisar o requisito acima, digite `classic car` na barra de pesquisa. Selecione o intervalo de datas nos filtros de data [!UICONTROL Data de Criação] e [!UICONTROL Última Modificação].

![Filtros de data](assets/date-filters.png)

A pesquisa exibe resultados semelhantes se você também estiver trabalhando na [!UICONTROL exibição do Assets].

## Aumentar a relevância de palavras-chave {#boosting-keywords}

Você pode melhorar a relevância de palavras-chave para ativos específicos para ajudar a impulsionar pesquisas com base nas palavras-chave. Em outras palavras, as imagens para as quais você promove palavras-chave específicas aparecem na parte superior dos resultados da pesquisa quando você pesquisa com base nessas palavras-chave.

1. Na interface do usuário do Assets, abra a página de propriedades do ativo. Clique em [!UICONTROL Avançado] e em [!UICONTROL Adicionar] em [!UICONTROL Elevar para palavras-chave de pesquisa].
2. Na caixa Pesquisar Promover, especifique uma palavra-chave para a qual deseja impulsionar a pesquisa da imagem e clique em [!UICONTROL Adicionar]. Você pode especificar várias palavras-chave da mesma maneira.
3. Clique em [!UICONTROL Salvar e fechar]. O ativo que você promoveu para essa palavra-chave aparece entre os principais resultados da pesquisa.

## Itens importantes ao realizar uma pesquisa no Experience Manager {#notable-things}

* Forneça informações de metadados do ativo para preparar seu ativo pesquisável pelo algoritmo Omni Search. Verifique se as informações de metadados do ativo foram atualizadas.
* Use aspas duplas (&quot; &quot;) para tornar sua pesquisa exata e direta.
* Verifique o caminho que você está procurando. Selecione a opção apropriada entre pasta, arquivo ou arquivo e pasta para executar a consulta de pesquisa no local apropriado.
* Você pode verificar os filtros que estão sendo aplicados à sua pesquisa na barra de pesquisa Omni.
* Caso não esteja obtendo resultados, verifique o caminho que está procurando. Além disso, verifique a pasta na qual você está realizando a pesquisa. Por exemplo, se você estiver fazendo uma pesquisa dentro da &quot;Pasta de automóveis&quot;, mas a palavra-chave que está usando estiver relacionada a &quot;Apparels&quot;, os resultados da pesquisa serão inadequados.
* Caso tenha adicionado um espaço em branco antes da palavra-chave que você está procurando.
* Usar uma combinação de palavras-chave, operadores e filtros pode facilitar e nivelar sua experiência de pesquisa.

<!--
* Use stemming search approach while searching for the asset. It means using an exact keyword that you are looking for.
* Specify Smart tags to the asset properties to boost the ranking of the search results.
The newly added assets are not indexed.
-->

## Diferenças entre a [!UICONTROL Exibição do administrador] e a [!UICONTROL Exibição do Assets] Pesquisa {#differences-asset-and-admin-view}

<table>
    <tr>
        <th> Parâmetros </th>
        <th> Exibição do administrador </th>
        <th> Visualização do Assets </th>
    </tr>
    <tr>
        <td> Aspectos personalizados </td>
        <td> Você pode adicionar <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=pt-BR">aspectos de pesquisa personalizados de acordo com o requisito.</td>
        <td> Os aspectos personalizados são parcialmente compatíveis com a visualização do Assets. Os aspectos suportados são:
            <ul>
            <li> Tags previstas
            <li> Nome
            <li> Confiança de tags prevista
            <li> Tamanho do ativo
            <li> Título
            </ul>
        </td>
    </tr>
    <tr>
        <td> Operadores </td>
        <td> Suporta AND, OR e NOT </td>
        <td> Não suportado </td>
    </tr>
    <tr>
        <td> Curingas </td>
        <td> Suporta ponto de interrogação (?) e asterisco (*).</td>
        <td> Não suportado </td>
    </tr>
    <tr>
        <td> Aumento dos resultados de pesquisa </td>
        <td> Compatível </td>
        <td> Não suportado </td>
    </tr>
     <tr>
        <td> Limpar todos os filtros de uma só vez </td>
        <td> Não suportado </td>
        <td> Compatível</td>
    </tr>
     <tr>
        <td> Arquivos/pastas/Arquivos e pastas </td>
        <td> Compatível </td>
        <td> Uma opção para selecionar uma pasta está disponível em "Tipo de arquivo" </td>
    </tr>
     <tr>
        <td> Status do ativo </td>
        <td> 
            As opções compatíveis são:
            <ul>
            <li> Publicação
            <li> Data de publicação
            <li> Última publicação feita por
            <li> Aprovação 
            <li> Check-out
            <li> Expiração
            <li> Dynamic Media
            </ul>
        </td>
        <td>
        As opções compatíveis são:
            <ul>
            <li> Todos
            <li> Aprovado
            <li> Rejeitado
            <li> Sem status
            </ul> 
        </td>
    </tr>
     <tr>
        <td> Tipo de arquivo </td>
        <td>
        As opções compatíveis são:
            <ul>
            <li> Imagens
            <li> Documentos
            <li> Multimídia
            <li> Arquivos 
            </ul>
            Elas têm mais opções hierárquicas.
        </td>
        <td>
        As opções compatíveis são:
            <ul>
            <li> Imagens
            <li> Documentos
            <li> Vídeo
            <li> Pasta 
            </ul> 
        Mais opções estão listadas em Tipo MIME.
        </td>
    </tr>
     <tr>
        <td> Tamanho do arquivo </td>
        <td>
        As opções compatíveis são:
            <ul>
            <li> De - Para
            <li> Tamanho (Bytes, KB, MB, GB)
            </ul> 
        </td>
        <td> Não suportado </td>
    </tr>
     <tr>
        <td> Outros filtros </td>
        <td>
            <ul>
            <li> Idioma
            <li> Status
            <li> Orientação
            <li> Estilo 
            <li> Insights
            <li> Stock
            <li> Cor do ativo
            <li> Modelo de fragmento de conteúdo
            </ul> 
        </td>
        <td> Não suportado </td>
    </tr>
</table>

>[!MORELIKETHIS]
>
>* [Pesquisar ativos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/search-assets.html?lang=pt-BR)
>* [Pesquisar aspectos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=pt-BR)
