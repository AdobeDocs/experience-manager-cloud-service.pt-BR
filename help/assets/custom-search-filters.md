---
title: Filtros de pesquisa personalizados
description: Saiba como personalizar o formulário de filtros de pesquisa
role: User, Leader, Developer
exl-id: 383e8165-439e-447b-a19d-d5446238a13f
source-git-commit: 836805b4eac5ab940dff5c66ec0dcf1ca8652837
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 12%

---


# Personalizar filtros de pesquisa {#customize-search-filters}

Os filtros de pesquisa permitem refinar os resultados da pesquisa com base em vários parâmetros, como data, tipo de arquivo, tags e relevância, melhorando a precisão das consultas de pesquisa. Ao aplicar filtros, você pode analisar os resultados mais relevantes com eficiência. Isso não apenas economiza tempo, mas também melhora a experiência geral de pesquisa, adaptando os resultados às preferências e necessidades específicas.
Veja mais sobre a [pesquisa](search-assets-view.md).

Personalizar filtros de pesquisa O AEM Assets só pode ser mapeado a entradas no Índice de propriedades pesquisáveis. Certifique-se de que todos os metadados personalizados estejam incluídos antes de configurar sua experiência de filtro personalizada. [!DNL Assets view] ajuda a personalizar os filtros de pesquisa para simplificar o processo de pesquisa. Para personalizar os filtros de pesquisa personalizados do AEM Assets, execute as seguintes etapas:

1. Navegue até **[!UICONTROL Configurações]** > **[!UICONTROL Configurações Gerais]** > **[!UICONTROL Pesquisa]**.

   <!--1. Go to the **[!UICONTROL Search]** tab. Click **[!UICONTROL Customize]** to configure your search form.-->

   ![configurações de filtro de pesquisa personalizado](assets/custom-search-filter.png)

1. Na seção **[!UICONTROL Filtros]**, você pode configurar o seguinte:

   * **[!UICONTROL Arquivos]:** a configuração de arquivos envolve tipos de arquivos, formatos de arquivo, status de ativos, tamanho de arquivo, dimensões de imagem, data de criação, data de modificação e assim por diante.
   * **[!UICONTROL Pastas]:** a configuração de pastas envolve data de criação, data de descarte, descarte por e assim por diante.
   * **[!UICONTROL Coleções]:** a configuração de coleções envolve visibilidade de coleção, tipo de coleção, data de criação, etc.

1. Você pode visualizar o formulário padrão **[!UICONTROL Filtros predefinidos]** disponível para Arquivo, Pasta ou Coleções. Ao passo que não é possível personalizar ou excluir este formulário pré-existente. Como alternativa, para criar um formulário de filtros personalizados, clique em **[!UICONTROL Adicionar novo formulário]**.

   >[!NOTE]
   >
   >Somente um formulário de filtro personalizado pode ser criado por categoria (Arquivo, Pasta ou Coleção).

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

## Ações em um formulário configurado {#Actions-on-configured-form}

Você pode usar as seguintes ações em um formulário de filtros configurado:

* **[!UICONTROL Personalizar]:** Clique para adicionar ou modificar o formulário. Você pode soltar elementos de filtros de [filtros personalizados](#available-custom-filters) na tela ou reordenar, se necessário.

* **[!UICONTROL Visualizar]:** Clique para revisar as alterações.

* **[!UICONTROL Definir como padrão]:** Clique para definir o formulário selecionado como padrão.

* **[!UICONTROL Excluir um formulário]:** Clique em mais opções ![mais opções](assets/do-not-localize/more-icon.svg) e selecione **[!UICONTROL Excluir um formulário]** para excluir o formulário de filtros selecionado.

* **[!UICONTROL Editar rótulos de formulário]:** Clique em mais opções ![mais opções](assets/do-not-localize/more-icon.svg) e adicione um novo rótulo e descrição ao formulário de filtros personalizados.

  ![editar rótulos de formulário](assets/edit-form-labels.png)

## Filtros personalizados disponíveis {#available-custom-filters}

A visualização Assets fornece os seguintes filtros personalizados que são reconfiguráveis de acordo com o requisito:

* [Filtrar elementos](#filter-elements)
* [Filtros pré-configurados](#preconfigured-filters)

### Filtrar elementos {#filter-elements}

O AEM Assets de filtros personalizados permite usar uma coleção de elementos de filtro na tela de filtros de pesquisa personalizados. Esses elementos são reconfiguráveis com base na usabilidade dos atributos de propriedade de pesquisa. No entanto, você pode personalizar as [propriedades de filtro](#filter-properties) de acordo com seus requisitos. Os seguintes elementos de filtro estão disponíveis em [!DNL Assets view]:

<table>
    <tr>
        <th>Filtrar elementos</th>
        <th>Descrição</th>
        <th>Propriedades</th>
    </tr>
    <tr>
        <td>Texto</td>
        <td>Um campo de texto é uma área de entrada na qual você pode digitar informações relacionadas ao filtro.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Valores
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Opções</td>
        <td>As opções referem-se às alternativas disponíveis para selecionar um item preferido de uma lista.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Valores
                <li>Opções
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Booleano</td>
        <td>Um booleano representa um valor verdadeiro. Ele pode ser usado onde você deseja ser específico para escolher uma opção entre outras.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Número</td>
        <td>Use esse elemento de filtro para representar um valor numérico.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Escalonador
                <li>Valor do passo
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Lista suspensa</td>
        <td>Para escolher entre várias opções exibidas em uma lista de opções.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Opções
                <li>Valores
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Data</td>
        <td>Usado para especificar a data.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Navegador de caminho</td>
        <td>Usado para navegar pelos arquivos ou pastas no repositório do Experience Manager.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Explorador de caminho
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Tags</td>
        <td>Usado para selecionar tags das opções disponíveis. As tags fornecem informações mais específicas sobre os ativos e melhoram sua descoberta. As marcas já aplicadas aos ativos selecionados são exibidas no painel <b>Propriedades</b>. Se você armazenar tags em uma propriedade de metadados personalizada e usar o caminho raiz para restringi-lo a uma hierarquia, poderá aproveitar a mesma configuração nos filtros de pesquisa. Se você não conseguir encontrar as tags relevantes, crie-as e atribua aos ativos selecionados. Consulte <a href = "tagging-management-assets-view.md"> Gerenciar tags na exibição do Assets </a> para obter detalhes sobre como criar e atribuir tags a ativos.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Seletor de tags
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Usuário</td>
        <td>Usado para especificar o tipo de usuário entre administradores, usuários comuns e consumidores.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Descrição
            </ul>
        </td>
    </tr>
</table>

### Filtros pré-configurados {#preconfigured-filters}

Os filtros pré-configurados são configurações predefinidas que permitem usá-los diretamente na tela. No entanto, você pode personalizar as [propriedades de filtro](#filter-properties) de acordo com seus requisitos. Os filtros a seguir estão pré-configurados em [!DNL Assets view]:

<table>
    <tr>
        <th>Filtros pré-configurados</th>
        <th>Descrição</th>
        <th>Propriedades</th>
    </tr>
    <tr>
        <td>Tipo de arquivo</td>
        <td>Filtre os resultados da pesquisa pelos tipos de arquivos compatíveis, ou seja, "Imagens", "Documentos" e "Vídeos".</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Opções
                <li>Valores
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Formato do arquivo</td>
        <td>A visualização do Assets é compatível com qualquer formato de arquivo binário com serviços básicos, como armazenamento, upload, cópia, movimentação, exclusão e adição de metadados.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Tamanho da imagem</td>
        <td>Forneça uma ou mais das dimensões mínima e máxima para filtrar imagens. O tamanho é fornecido em valores de dimensão de pixel e não é o tamanho do arquivo das imagens.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Escalonador
                <li>Valor do passo
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Largura da imagem</td>
        <td>Dimensões verticais de uma imagem.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Escalonador
                <li>Valor do passo
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Altura da imagem</td>
        <td>Dimensões horizontais de uma imagem.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Escalonador
                <li>Valor do passo
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Data de criação</td>
        <td>Intervalo de datas de criação dos ativos.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Data de modificação</td>
        <td>Intervalo de datas em que os ativos foram modificados.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Status do ativo</td>
        <td>A visualização do Assets permite que você defina o status em ativos disponíveis no repositório. Defina um status de ativo para melhor administrar e gerenciar o consumo downstream de ativos digitais. Escolha entre <b>Aprovado, Rejeitado ou Sem Status</b>.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Tags inteligentes</td>
        <td>Filtrar ativos usando tags inteligentes adicionadas ao repositório do Experience Manager.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Suporte a delimitadores
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Status da mídia dinâmica</td>
        <td>Escolha o status de um ativo entre publicado e não publicado.</td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Opções
                <li>Valores
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Data de expiração</td>
        <td>Filtrar ativos especificando um intervalo de datas após o qual os ativos não são mais válidos ou necessários. </td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Tipo de seleção
                <li>Descrição
            </ul>
        </td>
    </tr>
    <tr>
        <td>Tags (taxonomia)</td>
        <td>Trata-se de um sistema de organização e classificação de ativos digitais através da utilização de etiquetas, que cria essencialmente uma estrutura hierárquica de palavras-chave que permite aos utilizadores pesquisar e encontrar facilmente conteúdo relevante mediante a aplicação de etiquetas específicas a cada ativo; </td>
        <td>
            <ul>
                <li>Rótulo
                <li>Metadados
                <li>Seletor de tags
                <li>Descrição
            </ul>
        </td>
    </tr>
</table>

#### Filtrar propriedades {#filter-properties}

Cada elemento do filtro está associado a um conjunto de propriedades. Os filtros de pesquisa personalizados do AEM Assets usam as seguintes propriedades no filtro e nos elementos pré-configurados:

<table>
    <tr>
        <th>Propriedades</th>
        <th>Valores</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>Rótulo</td>
        <td>Texto</td>
        <td>É um identificador do filtro que você está usando.</td>
    </tr>
    <tr>
        <td>Metadados</td>
        <td>Lista suspensa</td>
        <td>A propriedade de metadados é usada para mapear metadados aprovados do repositório do Adobe Experience Manager Assets. Você pode escolher o valor dos metadados no menu suspenso que precisa ser mapeado com o elemento de filtro. </td>
    </tr>
    <tr>
        <td>Tipo de seleção</td> 
        <td>Único, Múltiplo, Exato ou Intervalo </td>
        <td>
            <ul>
                <li><b>A seleção única</b> permite escolher um item de cada vez, o que é ideal para escolhas distintas.
                <li><b>Seleção múltipla</b> permite escolher vários itens simultaneamente, o que é útil para selecionar várias opções. 
                <li><b>A seleção exata</b> permite escolher um único item preciso entre várias opções.
                <li><b>A seleção de intervalo</b> permite escolher um conjunto contínuo de valores dentro de um intervalo definido, útil para selecionar um intervalo de datas ou valores numéricos.
            </ul>
        </td>   
    </tr>
    <tr>
        <td>Opções</td>
        <td>Upload manual, caminho JSON ou CSV</td>
        <td>
            <ul>
                <li>Escolha <b>Manual</b> se desejar adicionar opções manualmente. 
                <li>Escolha <b>Caminho JSON</b> para adicionar opções do arquivo JSON. 
                <li>Escolha <b>Carregar CSV</b> para importar um arquivo CSV contendo valores a serem adicionados nas opções.
            </ul>
        </td>
    </tr>
    <tr>
       <td>Valores</td>
        <td>Adicionar ou editar</td>
        <td>
        <ul>
        <li>Clique em <b>adicionar</b> para adicionar um novo valor. 
        <li>Clique em <span>✎</span> para editar o rótulo. 
        <li>Clique em <span>??</span> para excluir o valor da opção. 
        <li>Clique em <b>Editar</b> para modificar as opções de edição. 
        <li>Você também pode alterar a sequência de opções mantendo-as.
        </td>
    </tr>
    <tr>
        <td>Suporte a delimitadores</td>
        <td>Ativar ou desativar</td>
        <td>Um delimitador é um símbolo usado para separar elementos distintos no texto. Por exemplo, vírgulas, espaços ou ponto e vírgula.</td>
    </tr>
    <tr>
        <td>Escalonador</td>
        <td>Valor</td>
        <td>Ative o botão Escalonador no campo de número para incrementar ou diminuir o valor em cada clique. </td>
    </tr>
    <tr>
        <td>Valor do passo </td>
        <td>Número</td>
        <td>Indica o valor de incremento/decremento ao usar o botão do passo a passo. Aparece quando o depurador está ativado.</td>
    </tr>
    <tr>
        <td>Descrição</td>
        <td>Texto</td>
        <td>Adicione uma explicação detalhada para fornecer informações adicionais sobre o elemento de filtro.</td>
    </tr>
</table>

>[!VIDEO](https://video.tv.adobe.com/v/3443080)

## Excluir um elemento de filtro {#delete-a-filter-element}

Para excluir um filtro de pesquisa, siga estas etapas:

1. Navegue até **[!UICONTROL Configurações]** > **[!UICONTROL Configurações gerais]**.
1. Vá para a guia **[!UICONTROL Pesquisa]**. Clique em **[!UICONTROL Personalizar]** para configurar o formulário de pesquisa.
1. O formulário [!UICONTROL Configurar Filtros] é exibido. Certifique-se de estar no modo de Edição para poder fazer modificações no modelo.
1. Selecione o elemento de filtro que deseja excluir. Por exemplo, selecione **[!UICONTROL Altura da imagem]**.
1. Clique em **[!UICONTROL Excluir categoria]** para excluir o elemento de filtro. O elemento **[!UICONTROL Altura da imagem]** foi removido da tela.
1. Clique em **[!UICONTROL Confirmar]** para salvar o formulário.

## Utilização de filtros de pesquisa personalizados{#using-custom-search-filters}

Após configurar os filtros de pesquisa, você pode usá-los para pesquisar ativos no repositório.

![Usando filtros de pesquisa personalizados](assets/using-custom-search-filters.png)

>[!MORELIKETHIS]
>
>* [Pesquisar ativos](search-assets-view.md)
