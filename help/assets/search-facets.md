---
title: Pesquisar aspectos
description: Este artigo descreve como criar, modificar e usar aspectos de pesquisa no AEM.
translation-type: tm+mt
source-git-commit: dfa9b099eaf7f0d155986bbab7d56901876d98f6

---


# Pesquisar aspectos {#search-facets}

Saiba como criar, modificar e usar aspectos de pesquisa no AEM.

Uma implantação corporativa dos ativos Adobe Experience Manager (AEM) tem a capacidade de armazenar muitos ativos. Às vezes, encontrar o ativo certo pode ser difícil e demorado se você usar apenas os recursos de pesquisa genéricos do AEM.

Use aspectos de pesquisa no painel Filtros para adicionar mais granularidade à sua experiência de pesquisa e tornar a funcionalidade de pesquisa mais eficiente e versátil. Os aspectos de pesquisa adicionam várias dimensões (predicados) que permitem executar pesquisas mais complexas. O painel Filtros inclui algumas facetas padrão. Você também pode adicionar aspectos de pesquisa personalizados.

Em resumo, as facetas de pesquisa permitem que você pesquise ativos de várias maneiras em vez de em uma única ordem taxonômica pré-determinada. É possível detalhar facilmente para o nível de detalhes desejado para uma pesquisa mais focada.

Por exemplo, se você estiver procurando uma imagem, poderá escolher se deseja um bitmap ou uma imagem vetorial. Você pode reduzir ainda mais o escopo da pesquisa especificando o tipo MIME da imagem. Da mesma forma, ao pesquisar documentos, você pode especificar o formato, por exemplo PDF ou MS Word.

## Adicionar um predicado {#adding-a-predicate}

Os aspectos de pesquisa exibidos no painel Filtros são definidos no formulário de pesquisa subjacente usando predicados. Para exibir mais ou diferentes aspectos, adicione predicados ao formulário padrão ou use um formulário personalizado que inclua aspectos de sua escolha.

Para pesquisas de texto completo, adicione o `Fulltext` predicado ao formulário. Use o predicado Propriedade para procurar ativos que correspondam a uma única propriedade especificada. Use o predicado Opções para pesquisar ativos que correspondam a um ou mais valores para uma propriedade específica. Adicione o predicado Intervalo de datas para pesquisar ativos criados dentro de um intervalo de datas especificado.

1. Toque/clique no logotipo do AEM e vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar formulários]**.
1. Na página Pesquisar formulários, selecione Painel **[!UICONTROL de pesquisa do administrador de]** ativos e toque em **Editar** ![ativos_editar](assets/aemassets_edit.png).

   ![Localize e selecione o painel de pesquisa do administrador de ativos](assets/assets_admin_searchrail.png)

1. Na página Editar formulários de pesquisa, arraste um predicado da guia **[!UICONTROL Selecionar predicado]** para o painel principal. Por exemplo, arraste o Predicado **[!UICONTROL de propriedade]**.

   ![Arraste e solte um predicado para personalizar os filtros de pesquisa](assets/drag_predicate.png)

   Arraste e solte um predicado para personalizar os filtros de pesquisa

1. Na guia Configurações, digite um rótulo de campo, um texto de espaço reservado e uma descrição para o predicado. Especifique um nome válido para a propriedade de metadados que deseja associar ao predicado.

   O rótulo do cabeçalho na guia Configurações identifica o tipo do predicado selecionado.

   ![Use a guia Configurações para fornecer as opções necessárias de um predicado](assets/settings.png)

   Use a guia Configurações para fornecer as opções necessárias de um predicado

1. No campo Nome **[!UICONTROL da]** propriedade, especifique um nome válido para a propriedade de metadados que você deseja associar ao predicado. É o nome com base no qual a pesquisa é realizada. Por exemplo, insira `jcr:content/metadata/dc:description` ou `./jcr:content/metadata/dc:description`.

   Você também pode selecionar um nó existente na caixa de diálogo de seleção.

   ![Associar uma propriedade de metadados a um predicado no campo Nome da propriedade](assets/property_settings.png)

   Associar uma propriedade de metadados a um predicado no campo Nome da propriedade

1. Toque/clique na **[!UICONTROL visualização]** ![Visualizar](assets/preview.png) para gerar uma visualização do painel Filtros como ele aparece depois de adicionar o predicado.
1. Revise o layout do predicado no modo de Visualização.

   ![Visualizar o formulário de pesquisa antes de enviar as alterações](assets/preview-1.png)

   Visualizar o formulário de pesquisa antes de enviar as alterações

1. Para fechar a visualização, toque/clique em **[!UICONTROL Fechar]** ![feche](assets/do-not-localize/close_icon.png) no canto superior direito da visualização.
1. Toque em **[!UICONTROL Concluído]** para salvar as configurações.
1. Navegue até o painel Pesquisar na interface do usuário Ativos. O predicado Propriedade é adicionado ao painel.
1. Insira uma descrição para o ativo a ser pesquisado na caixa de texto. Por exemplo, digite &quot;Adobe&quot;. Quando você realiza uma pesquisa, os ativos com descrição correspondente a &quot;Adobe&quot; são listados nos resultados da pesquisa.

## Adicionar um predicado de opções {#adding-an-options-predicate}

O predicado Opções permite que você adicione várias opções de pesquisa no painel Filtros. Você pode selecionar uma ou mais dessas opções no painel Filtros para pesquisar ativos. Por exemplo, para pesquisar ativos com base no tipo de arquivo, configure opções, como Imagens, Multimídia, Documentos e Arquivos, no formulário de pesquisa. Depois de configurar essas opções, a pesquisa será realizada em ativos do tipo GIF, JPEG, PNG e assim por diante, quando você selecionar a opção Imagens no painel Filtros.

Para mapear as opções para a respectiva propriedade, crie uma estrutura de nó para as opções e forneça o caminho do nó pai na propriedade Nome da propriedade do predicado Opções. O nó pai deve ser do tipo `sling`: `OrderedFolder`. As opções devem ser do tipo `nt:unstructured`. Os nós de opção devem ter as propriedades `jcr:title` e `value` configurados.

A `jcr:title` propriedade é um nome amigável para a opção exibida no painel Filtros. O `value` campo é usado na consulta para corresponder à propriedade especificada.

Quando você seleciona uma opção, a pesquisa é executada com base na `value` propriedade do nó de opção e de seus nós filhos, se houver. A árvore inteira sob o nó de opção é atravessada e a `value` propriedade de cada nó filho é combinada usando uma operação OU para formar a consulta de pesquisa.

Por exemplo, se você selecionar &quot;Imagens&quot; para tipos de arquivos, a consulta de pesquisa para os ativos será criada combinando a `value` propriedade usando uma operação OU. Por exemplo, a consulta de pesquisa de imagens é construída combinando os resultados correspondentes para *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* e *image/tiff* `jcr:content/metadata/dc:format` para a propriedade usando uma operação OR.

A propriedade value de um tipo de arquivo, como visto no CRXDE, é usada para que as consultas de pesquisa funcionem

Em vez de criar manualmente uma estrutura de nó para as opções no repositório CRX, você pode definir as opções em um arquivo JSON especificando pares de valores chave correspondentes. Especifique o caminho do arquivo JSON no campo Nome **[!UICONTROL da]** propriedade. Por exemplo, você pode definir os pares de valores chave, `image/bmp`, `image/gif`, `image/jpeg`e `image/png` especificar seus valores como mostrado no seguinte arquivo JSON de amostra. No campo Nome **[!UICONTROL da]** propriedade, você pode especificar o caminho CRX para esse arquivo.

```
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

Se desejar usar um nó existente, especifique-o usando a caixa de diálogo de seleção.

>[!NOTE]
>
>O predicado Opções é um invólucro personalizado que inclui predicados de propriedade para demonstrar o comportamento descrito. Atualmente, não há um terminal REST disponível para suportar a funcionalidade nativamente.

1. Toque no logotipo do AEM e vá até **[!UICONTROL Ferramentas > Geral > Pesquisar formulários]**.
1. Na página **[!UICONTROL Pesquisar formulários]** , selecione Painel **[!UICONTROL de pesquisa do administrador de]** ativos e toque no ícone Editar.
1. Na página **[!UICONTROL Editar formulário]** de pesquisa, arraste o Predicado **[!UICONTROL de]** opções da guia **[!UICONTROL Selecionar preditivo]** para o painel principal.
1. Na guia **[!UICONTROL Configurações]** , digite um rótulo e um nome para a propriedade. Por exemplo, para pesquisar ativos com base em seu formato, especifique um nome amigável para o rótulo, por exemplo, Tipo **[!UICONTROL de]** arquivo. Especifique a propriedade com base na qual a pesquisa deve ser realizada no campo de propriedade, por exemplo `jcr:content/metadata/dc:format.`
1. Faça uma das seguintes opções:

   * No campo Nome **[!UICONTROL da]** propriedade, mencione o caminho do arquivo JSON no qual você define os nós para as opções e especifica os pares de valores chave correspondentes.
   * Toque ![](assets/do-not-localize/aem_assets_add_icon.png) ao lado do campo Opções para especificar o texto e o valor de exibição para as opções que deseja fornecer no painel Filtros. Para adicionar outra opção, toque/clique ![](assets/do-not-localize/aem_assets_add_icon.png) e repita a etapa.

1. Certifique-se de que **[!UICONTROL Single Select]** esteja apagado para permitir que o usuário selecione várias opções para tipos de arquivos de cada vez (por exemplo, Imagens, Documentos, Multimídia e Arquivos). Se você selecionar Seleção **[!UICONTROL única]**, o usuário poderá selecionar apenas uma opção para tipos de arquivo por vez.

   ![Os campos disponíveis no predicado Opções](assets/options_predicate.png)

   Os campos disponíveis no predicado Opções

1. No campo **Descrição** , digite uma descrição opcional e clique em **[!UICONTROL Concluído]**.
1. Navegue até o painel Pesquisar. O predicado Opções é adicionado ao painel **Pesquisar** . As opções para Tipo **[!UICONTROL de]** arquivo são exibidas como caixas de seleção.

## Adicionar um predicado de propriedade de vários valores {#adding-a-multi-value-property-predicate}

O `Multi Value Property` predicado permite pesquisar ativos para vários valores. Considere um cenário em que você tem imagens de vários produtos nos ativos AEM e os metadados de cada imagem incluem um número SKU associado ao produto. Você pode usar esse predicado para procurar imagens de produtos com base em vários números de SKU.

1. Clique no logotipo do AEM e vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar formulários]**.
1. Na página Pesquisar formulários, selecione Painel **[!UICONTROL de pesquisa do administrador de]** ativos, toque em **Editar** ![ativos_editar](assets/aemassets_edit.png).
1. Na página Editar formulário de pesquisa, arraste um Predicado **[!UICONTROL de propriedades de]** vários valores da guia **[!UICONTROL Selecionar preditivo]** para o painel principal.
1. Na guia **[!UICONTROL Configurações]** , digite um rótulo e um texto de espaço reservado para o predicado. Especifique o nome da propriedade com base no qual a pesquisa deve ser realizada no campo da propriedade, por exemplo `jcr:content/metadata/dc:value`. Você também pode usar a caixa de diálogo de seleção para selecionar um nó.
1. Verifique se a opção Suporte **[!UICONTROL a]** delimitadores está selecionada. No campo Delimitadores **[!UICONTROL de]** entrada, especifique delimitadores para separar valores individuais. Por padrão, a vírgula é especificada como delimitador. É possível especificar um delimitador diferente.
1. No campo **Descrição** , insira uma descrição opcional e toque em **[!UICONTROL Concluído]**.
1. Navegue até o painel Filtros na interface do usuário Ativos. O predicado Propriedade **** de vários valores é adicionado ao painel.
1. Especifique vários valores no campo Vários valores separados pelos delimitadores e execute a pesquisa. O predicado busca uma correspondência de texto exata para os valores especificados.

## Adicionar um predicado de tags {#adding-a-tags-predicate}

O `Tags` predicado permite que você realize pesquisas baseadas em tags para ativos. Por padrão, o AEM Assets pesquisa ativos por uma ou mais correspondências de tags com base nas tags especificadas. Em outras palavras, a consulta de pesquisa executa uma operação OU usando as tags especificadas. No entanto, você pode usar a opção de correspondência de todas as tags para pesquisar ativos que incluem todas as tags especificadas.

1. Clique no logotipo do AEM e vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar formulários]**.
1. Na página Pesquisar formulários, selecione Painel **[!UICONTROL de pesquisa do administrador de]** ativos e toque em **Editar** ![ativos_editar](assets/aemassets_edit.png).
1. Na página Editar formulário de pesquisa, arraste o Predicado **[!UICONTROL de]** tags da guia Selecionar preditivo para o painel principal.
1. Na guia Configurações, insira um texto de espaço reservado para o predicado. Especifique o nome da propriedade com base no qual a pesquisa deve ser realizada no campo da propriedade, por exemplo, *jcr:content/metadata/cq:tags*. Como alternativa, você pode selecionar um nó no CRXDE na caixa de diálogo de seleção.
1. Configure a propriedade de caminho de tags raiz desse predicado para preencher várias tags na lista Tags.
1. Selecione a opção **** Mostrar correspondência de todas as tags para procurar ativos que incluem todas as tags especificadas.

   ![Configurações típicas do predicado Tags](assets/tags_predicate.png)

   Configurações típicas do predicado Tags

1. No campo **[!UICONTROL Descrição]** , digite uma descrição opcional e clique/toque em **[!UICONTROL Concluído]**.
1. Navegue até o painel Pesquisar. O predicado **[!UICONTROL Tags]** é adicionado ao painel Pesquisar.
1. Especifique tags com base nas quais você deseja pesquisar ativos ou selecione na lista de sugestões.
1. Selecione **[!UICONTROL Corresponder tudo]** para procurar correspondências que incluam todas as tags especificadas.

## Adicionar outros predicados {#adding-other-predicates}

Semelhante à forma como você adiciona um predicado de Propriedade ou um predicado de Opções, você pode adicionar os seguintes predicados adicionais ao painel Pesquisar:

<table>
 <tbody>
  <tr>
   <td><p><strong>Nome do Predicado</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
   <td><p><strong>Propriedades</strong></p> </td>
  </tr>
  <tr>
   <td><p>Texto completo</p> </td>
   <td>Predicado de pesquisa para executar pesquisa de texto completo em um nó de ativo inteiro. <code>jcr</code> Está mapeado com o <code>contains</code>: operador. Você pode especificar um caminho relativo se desejar executar uma pesquisa de texto completo em uma parte específica do nó do ativo.</td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Espaço reservado</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Navegador de caminhos</td>
   <td>Projetar pesquisa para procurar ativos em pastas e subpastas em um caminho raiz pré-configurado</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Caminho raiz</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Caminho</p> </td>
   <td><p>Use-o para filtrar os resultados no local. É possível especificar caminhos diferentes como opções.</p> </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Caminho</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Publicar status</p> </td>
   <td><p>Projetar pesquisa para pesquisar ativos com base em seu status de publicação</p> </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Data relativa</p> </td>
   <td><p>O predicado de pesquisa para pesquisar ativos com base na data relativa de sua criação. Por exemplo, você pode configurar opções, como 2 meses atrás, 3 semanas atrás e assim por diante. </p> </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Nome da propriedade</li>
     <li>Data relativa</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Intervalo</p> </td>
   <td><p>O predicado de pesquisa para pesquisar ativos que estão dentro de um intervalo especificado. No painel Pesquisar, você pode especificar valores mínimos e máximos para o intervalo.</p> </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Intervalo de datas</p> </td>
   <td><p>Projete de pesquisa para pesquisar ativos criados em um intervalo especificado para uma propriedade de data. No painel Pesquisar, é possível especificar datas de início e término usando seletores de data.</p> </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Espaço reservado</li>
     <li>Nome da propriedade</li>
     <li>Texto do intervalo (de)</li>
     <li>Texto do intervalo (até)</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p>Projete de pesquisa para uma pesquisa de ativos baseada em controle deslizante com base em uma propriedade de data.</p> </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Tamanho do arquivo</p> </td>
   <td><p>Predicado de pesquisa para pesquisar ativos com base em seu tamanho. É um predicado baseado em silder no qual você seleciona as opções do controle deslizante de um nó configurável. As opções padrão são definidas em /libs/dam/options/predicates/filesize no repositório CRX. O tamanho do arquivo é fornecido em bytes.</p> </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Nome da propriedade</li>
     <li>Caminho</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Última modificação do ativo</td>
   <td>Projetar pesquisa para pesquisar ativos modificados recentemente </td>
   <td>
    <ul>
     <li>Nome da propriedade</li>
     <li>Valor da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Publicar status</td>
   <td>Projetar pesquisa para procurar ativos com base no status de publicação </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Classificação</td>
   <td>Projetar pesquisa para pesquisar ativos com base em sua classificação média </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Nome da propriedade</li>
     <li>Caminho da opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status da expiração</td>
   <td>Projetar pesquisa para pesquisar ativos com base em seu status de expiração </td>
   <td>
    <ul>
     <li>Etiqueta</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Oculto</td>
   <td>predicado de pesquisa que define uma propriedade de campo oculto para procurar ativos</td>
   <td>
    <ul>
     <li>Nome da propriedade</li>
     <li>Valor da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Redefinir aspectos de pesquisa padrão {#restoring-default-search-facets}

Por padrão, um ícone Bloquear é exibido antes do Painel **[!UICONTROL de pesquisa do administrador de]** ativos na página Formulários **[!UICONTROL de]** pesquisa. O ícone Bloquear desaparece se você adicionar aspectos de pesquisa ao formulário, indicando que o formulário padrão foi modificado.

O ícone de bloqueio em relação a uma opção na página Pesquisar formulários indica que as configurações padrão estão intactas e não são personalizadas.

Para restaurar o aspecto de pesquisa padrão, execute estas etapas:

1. Selecione **[!UICONTROL Assets Admin Search Rail]** na página **[!UICONTROL Pesquisar formulários]** .
1. Toque em **[!UICONTROL Excluir]** ícone ![de](assets/do-not-localize/deleteoutline.png) exclusão na barra de ferramentas.
1. Na caixa de diálogo de confirmação, toque em **[!UICONTROL Excluir]** para remover as alterações personalizadas.

   Após excluir as alterações personalizadas nos aspectos de pesquisa, o ícone Bloquear será exibido novamente antes do Painel **[!UICONTROL de pesquisa do administrador de]** ativos na página Formulários **[!UICONTROL de]** pesquisa.

## User permissions {#user-permissions}

Se você não tiver uma função de administrador atribuída, esta é uma lista de permissões necessárias para executar ações de edição, exclusão e visualização envolvendo aspectos de pesquisa.

<table>
 <tbody>
  <tr>
   <td><strong>Ação</strong></td>
   <td><strong>Permissões</strong></td>
  </tr>
  <tr>
   <td>Editar </td>
   <td>Permissões de leitura e gravação no <code>/apps</code> nó no CRX<br /> </td>
  </tr>
  <tr>
   <td>Excluir</td>
   <td>Permissões de leitura, gravação e exclusão no <code>/apps</code> nó no CRX</td>
  </tr>
  <tr>
   <td>Visualizar</td>
   <td>Permissões de Leitura, Gravação e Exclusão no <code>/var/dam/content</code> nó no CRX. Além disso, permissões de leitura e gravação no <code>/apps</code> nó.</td>
  </tr>
 </tbody>
</table>

>[!MORELIKETHIS]
>
>* [Pesquisar ativos digitais](search-assets.md)

