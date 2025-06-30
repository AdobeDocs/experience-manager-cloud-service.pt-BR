---
title: Pesquisar aspectos.
description: Este artigo descreve como criar, modificar e usar aspectos de pesquisa no Experience Manager.
feature: Metadata
role: Admin, User
exl-id: f994c1bf-3f9d-4cb2-88f4-72a9ad6fa999
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '2505'
ht-degree: 19%

---

# Pesquisar aspectos {#search-facets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/search-facets.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

Uma implantação corporativa do Adobe Experience Manager Assets tem a capacidade de armazenar muitos ativos. Às vezes, encontrar o ativo certo pode ser trabalhoso e demorado se você usar apenas os recursos de pesquisa genéricos do Experience Manager.

Use os aspectos de pesquisa no painel Filtros para adicionar mais granularidade à sua experiência de pesquisa e tornar a funcionalidade de pesquisa mais eficiente e versátil. Os aspectos de pesquisa adicionam várias dimensões (predicados) que permitem realizar pesquisas mais complexas. O painel Filtros inclui algumas facetas padrão. Você também pode adicionar aspectos de pesquisa personalizados.

Em resumo, os aspectos de pesquisa permitem pesquisar ativos de várias maneiras, em vez de em uma única ordem taxonômica predeterminada. Você pode facilmente detalhar o nível desejado de detalhes para uma pesquisa mais focada.

Por exemplo, se estiver procurando uma imagem, você pode escolher se deseja uma imagem de bitmap ou de vetor. É possível reduzir ainda mais o escopo da pesquisa especificando o tipo MIME da imagem. Da mesma forma, ao pesquisar documentos, você pode especificar o formato, por exemplo, PDF ou MS Word.

## Adicionar um predicado {#adding-a-predicate}

Os aspectos de pesquisa exibidos no painel Filtros são definidos no formulário de pesquisa subjacente usando predicados. Para exibir mais facetas ou diferentes, adicione predicados ao formulário padrão ou use um formulário personalizado que inclua facetas de sua escolha.

Para pesquisas de texto completo, adicione o predicado `Fulltext` ao formulário. Use o predicado Propriedade para pesquisar ativos que correspondem a uma única propriedade especificada. Use o predicado Opções para pesquisar ativos que correspondem a um ou mais valores de uma propriedade específica. Adicione o predicado Intervalo de datas para pesquisar ativos criados em um intervalo de datas especificado.

1. Clique no logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar Forms]**.
1. Na página Pesquisar Forms, selecione **[!UICONTROL Painel de pesquisa do administrador do Assets]** e **Editar** ![aemassets_edit](assets/aemassets_edit.png).

   ![Localize e selecione o Painel de Pesquisa do Administrador do Assets](assets/assets_admin_searchrail.png)

1. Na página Editar Forms de Pesquisa, arraste um predicado da guia **[!UICONTROL Selecionar predicado]** para o painel principal. Por exemplo, arraste o **[!UICONTROL Predicado de propriedade]**.

   ![Selecione e mova um predicado para personalizar os filtros de pesquisa](assets/drag_predicate.png)

   *Figura: selecione e mova um predicado para personalizar os filtros de pesquisa.*

1. Na guia Configurações, insira um rótulo de campo, um texto de espaço reservado e uma descrição para o predicado. Especifique um nome válido para a propriedade de metadados que deseja associar ao predicado. O rótulo do cabeçalho na guia Configurações identifica o tipo do predicado selecionado.

   ![Use a guia Configurações para fornecer as opções necessárias de um predicado](assets/settings.png)

   *Figura: use a guia Configurações para fornecer as opções necessárias de um predicado.*

1. No campo **[!UICONTROL Nome da propriedade]**, especifique um nome válido para a propriedade de metadados que deseja associar ao predicado. É o nome com base no qual a pesquisa é realizada. Por exemplo, digite `jcr:content/metadata/dc:description` ou `./jcr:content/metadata/dc:description`. Você também pode selecionar um nó existente na caixa de diálogo de seleção.

   ![Associe uma propriedade de metadados a um predicado no campo Nome da Propriedade](assets/property_settings.png)

   *Figura: associe uma propriedade de metadados a um predicado no campo Nome da Propriedade.*

1. Clique em **[!UICONTROL Visualizar]** ![visualizar](assets/preview.png) para gerar uma visualização do painel Filtros como ele aparece após a adição do predicado.
1. Revise o layout do predicado no modo Visualizar.

   ![Visualizar o formulário de pesquisa antes de enviar as alterações](assets/preview-1.png)

   Pré-visualizar o formulário de pesquisa antes de enviar as alterações

1. Para fechar a visualização, clique em **[!UICONTROL Fechar]** ![fechar](assets/do-not-localize/close_icon.png) no canto superior direito da visualização.
1. Selecione **[!UICONTROL Concluído]** para salvar as configurações.
1. Navegue até o painel Pesquisar na interface do usuário do Assets. O predicado Propriedade é adicionado ao painel.
1. Insira uma descrição para o ativo a ser pesquisado na caixa de texto. Por exemplo, digite &quot;Adobe&quot;. Ao realizar uma pesquisa, os ativos com descrição correspondente a &quot;Adobe&quot; são listados nos resultados da pesquisa.

## Adicionar um predicado de Opções {#adding-an-options-predicate}

O predicado Opções permite adicionar várias opções de pesquisa no painel Filtros. É possível selecionar uma ou mais dessas opções no painel Filtros para procurar ativos. Por exemplo, para pesquisar ativos com base no tipo de arquivo, configure opções como Imagens, Multimídia, Documentos e Arquivos no formulário de pesquisa. Após configurar essas opções, a pesquisa é executada em ativos do tipo GIF, JPEG, PNG e assim por diante, ao selecionar a opção Imagens no painel Filtros.

Para mapear as opções para a respectiva propriedade, crie uma estrutura de nó para as opções e forneça o caminho do nó principal na propriedade Nome da propriedade do predicado Opções. O nó pai deve ser do tipo `sling`: `OrderedFolder`. As opções devem ser do tipo `nt:unstructured`. Os nós de opção devem ter as propriedades `jcr:title` e `value` configuradas.

A propriedade `jcr:title` é um nome amigável para a opção que é exibida no painel Filtros. O campo `value` é usado na consulta para corresponder à propriedade especificada.

Quando você seleciona uma opção, a pesquisa é executada com base na propriedade `value` do nó de opção e seus nós filhos, se houver. A árvore inteira sob o nó de opção é percorrida e a propriedade `value` de cada nó filho é combinada usando uma operação OR para formar a consulta de pesquisa.

Por exemplo, se você selecionar &quot;Imagens&quot; para tipos de arquivos, a consulta de pesquisa dos ativos será criada ao combinar a propriedade `value` usando uma operação OR. Por exemplo, a consulta de pesquisa de imagens é construída combinando os resultados correspondentes de *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* e *image/tiff* da propriedade `jcr:content/metadata/dc:format` usando uma operação OR.

A propriedade Value de um tipo de arquivo, como visto no CRXDE, é usada para consultas de pesquisa funcionarem

Em vez de criar manualmente uma estrutura de nó para as opções no repositório CRX, defina as opções em um arquivo JSON especificando pares de valores chave correspondentes. Especifique o caminho do arquivo JSON no campo **[!UICONTROL Nome da propriedade]**. Por exemplo, defina os pares de valores chave, `image/bmp`, `image/gif`, `image/jpeg` e `image/png` e especifique os valores, como mostrado no seguinte arquivo JSON de amostra. No campo **[!UICONTROL Nome da propriedade]**, especifique o caminho CRX desse arquivo.

```json
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

Se quiser usar um nó existente, especifique-o usando a caixa de diálogo de seleção.

>[!NOTE]
>
>O predicado Opções é um invólucro personalizado que inclui predicados de propriedade para demonstrar o comportamento descrito. Atualmente, não há nenhum endpoint REST disponível para oferecer suporte à funcionalidade nativamente.

1. Selecione o logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas > Geral > Pesquisar Forms]**.
1. Na página **[!UICONTROL Pesquisar Forms]**, selecione **[!UICONTROL Painel de Pesquisa do Administrador do Assets]** e clique no ícone Editar.
1. Na página **[!UICONTROL Editar formulário de pesquisa]**, arraste o **[!UICONTROL Predicado de opções]** da guia **[!UICONTROL Selecionar predicado]** até o painel principal.
1. Na guia **[!UICONTROL Configurações]**, digite um rótulo e um nome para a propriedade. Por exemplo, para pesquisar ativos com base no formato, especifique um nome amigável para o rótulo, por exemplo, **[!UICONTROL Tipo de arquivo]**. Especifique a propriedade com base na qual a pesquisa deve ser realizada no campo de propriedade, por exemplo, `jcr:content/metadata/dc:format.`
1. Siga uma das seguintes opções:

   * No campo **[!UICONTROL Nome da Propriedade]**, mencione o caminho do arquivo JSON onde você define os nós das opções e especifica os pares de valores chave correspondentes.
   * Selecione o ![ícone de adição do Assets](assets/do-not-localize/aem_assets_add_icon.png) ao lado do campo Opções para especificar o texto de exibição e o valor das opções que você deseja fornecer no painel Filtros. Para adicionar outra opção, selecione ![ícone de adição do Assets](assets/do-not-localize/aem_assets_add_icon.png) e repita a etapa.

1. Certifique-se de que **[!UICONTROL Seleção única]** esteja desmarcada para permitir que o usuário selecione várias opções para tipos de arquivos de cada vez (por exemplo, Imagens, Documentos, Multimídia e Arquivos). Se você marcar **[!UICONTROL Seleção única]**, o usuário poderá selecionar apenas uma opção para tipos de arquivo por vez.

   ![Os campos disponíveis no predicado Opções](assets/options_predicate.png)

   Os campos disponíveis no predicado Opções

1. No campo **Descrição**, insira uma descrição opcional e clique em **[!UICONTROL Concluído]**.
1. Navegue até o painel Pesquisa. O predicado Opções foi adicionado ao painel **Pesquisar**. As opções para **[!UICONTROL Tipo de Arquivo]** são exibidas como caixas de seleção.

## Adicionar um predicado Propriedade de vários valores {#adding-a-multi-value-property-predicate}

O predicado `Multi Value Property` permite procurar vários valores em ativos. Considere um cenário em que você tem imagens de vários produtos no [!DNL Assets] e os metadados de cada imagem incluem um número SKU associado ao produto. Você pode usar esse predicado para pesquisar imagens de produtos com base em vários números SKU.

1. Clique no logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar Forms]**.
1. Na página Pesquisar Forms, selecione **[!UICONTROL Painel de pesquisa do administrador do Assets]** e selecione **Editar** ![aemassets_edit](assets/aemassets_edit.png).
1. Na página Editar formulário de pesquisa, arraste um **[!UICONTROL Predicado de propriedades de vários valores]** da guia **[!UICONTROL Selecionar predicado]** para o painel principal.
1. Na guia **[!UICONTROL Configurações]**, insira um rótulo e um texto de espaço reservado para o predicado. Especifique o nome da propriedade com base na qual a pesquisa deve ser realizada no campo de propriedade, por exemplo, `jcr:content/metadata/dc:value`. Você também pode usar a caixa de diálogo de seleção para selecionar um nó.
1. Verifique se a opção **[!UICONTROL Suporte a delimitadores]** está selecionada. No campo **[!UICONTROL Delimitadores de entrada]**, especifique delimitadores para separar valores individuais. Por padrão, a vírgula é especificada como delimitador. É possível especificar um delimitador diferente.
1. No campo **Descrição**, insira uma descrição opcional e selecione **[!UICONTROL Concluído]**.
1. Navegue até o painel Filtros na interface do usuário do Assets. O predicado **[!UICONTROL Propriedade de vários valores]** é adicionado ao painel.
1. Especifique vários valores no campo Vários valores separados pelos delimitadores e execute a pesquisa. O predicado busca uma correspondência exata de texto para os valores especificados.

## Adicionar um predicado de tags {#adding-a-tags-predicate}

O predicado `Tags` permite realizar pesquisas baseadas em tags para ativos. Por padrão, [!DNL Assets] pesquisa ativos para uma ou mais correspondências de marcas com base nas marcas especificadas. Em outras palavras, a consulta de pesquisa executa uma operação OR usando as tags especificadas. No entanto, você pode usar a opção Corresponder todas as tags para procurar ativos que incluem todas as tags especificadas.

1. Clique no logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Pesquisar Forms]**.
1. Na página Pesquisar Forms, selecione **[!UICONTROL Painel de pesquisa do administrador do Assets]** e **Editar** ![aemassets_edit](assets/aemassets_edit.png).
1. Na página Editar formulário de pesquisa, arraste o **[!UICONTROL Predicado de tags]** da guia Selecionar predicado para o painel principal.
1. Na guia Configurações, insira um texto de espaço reservado para o predicado. Especifique o nome da propriedade com base na qual a pesquisa deve ser realizada no campo de propriedade, por exemplo, `jcr:content/metadata/cq:tags`. Como alternativa, você pode selecionar um nó no CRXDE na caixa de diálogo de seleção.
1. Configure a propriedade Root tags path desse predicado para preencher várias tags na lista Tags.
1. Selecione a opção **[!UICONTROL Mostrar correspondência de todas as tags]** para procurar ativos que incluem todas as tags especificadas.

   ![Configurações típicas do predicado de marcas](assets/tags_predicate.png)

1. No campo **[!UICONTROL Descrição]**, insira uma descrição opcional e selecione **[!UICONTROL Concluído]**.
1. Navegue até o painel Pesquisa. O predicado **[!UICONTROL Tags]** é adicionado ao painel Pesquisar.
1. Especifique as tags com base nas quais deseja pesquisar ativos ou selecione na lista de sugestões.
1. Selecione **[!UICONTROL Corresponder todos]** para procurar correspondências que incluam todas as marcas especificadas.

Você pode classificar a estrutura de marcas em ordem crescente ou decrescente com base na data **[!UICONTROL Nome]** (ordem alfabética), **[!UICONTROL Criada]** ou **[!UICONTROL Modificada]**. Na ilustração a seguir, a estrutura de marcas é classificada em ordem alfabética com base no **[!UICONTROL Nome]**.

![add-tags](assets/add-tags-to-asset.png)


## Adicionar outros predicados {#adding-other-predicates}

Semelhante à maneira como você adiciona um predicado de Propriedade ou um predicado de Opções, é possível adicionar os seguintes predicados adicionais ao painel Pesquisar:

<table>
 <tbody>
  <tr>
   <td><p><strong>Nome do predicado</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
   <td><p><strong>Propriedades</strong></p> </td>
  </tr>
  <tr>
   <td><p>Texto completo</p> </td>
   <td>Pesquisar predicado para executar uma pesquisa de texto completo em um nó de ativo inteiro. Está mapeado com o operador <code>jcr</code>:<code>contains</code>. Você pode especificar um caminho relativo se quiser executar uma pesquisa de texto completo em uma parte específica do nó do ativo.</td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Espaço reservado</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Navegador de caminhos</td>
   <td>Pesquisar predicado para pesquisar ativos em pastas e subpastas em um caminho raiz pré-configurado</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Caminho raiz</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Caminho</p> </td>
   <td><p>Use-a para filtrar os resultados no local. Você pode especificar caminhos diferentes como opções.</p> </td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Caminho</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Publicar status</p> </td>
   <td><p>Pesquisar predicado para pesquisar ativos com base no status de publicação</p> </td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Data relativa</p> </td>
   <td><p>Predicado de pesquisa para pesquisar ativos com base na data relativa de sua criação. Por exemplo, você pode configurar opções, como 2 meses atrás, 3 semanas atrás e assim por diante. </p> </td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Nome da propriedade</li>
     <li>Data relativa</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Intervalo</p> </td>
   <td><p>Pesquisar predicado para pesquisar ativos dentro de um intervalo especificado. No painel Pesquisar, é possível especificar valores mínimos e máximos para o intervalo.</p> </td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Intervalo de datas</p> </td>
   <td><p>Pesquisar predicado para pesquisar ativos criados em um intervalo especificado para uma propriedade de data. No painel Pesquisar, é possível especificar datas de Início e Término usando seletores de datas.</p> </td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Espaço reservado</li>
     <li>Nome da propriedade</li>
     <li>Intervalo de texto (de)</li>
     <li>Intervalo de texto (até)</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p>Pesquisar predicado para uma pesquisa com base em controle deslizante de ativos com base em uma propriedade de data.</p> </td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Tamanho do arquivo</p> </td>
   <td><p>Pesquisar predicado para pesquisar ativos com base em seu tamanho. É um predicado baseado em controle deslizante no qual você seleciona as opções de controle deslizante de um nó configurável. As opções padrão são definidas em /libs/dam/options/predicates/filesize no repositório do CRX. O tamanho do arquivo é fornecido em bytes.</p> </td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Nome da propriedade</li>
     <li>Caminho</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Última modificação do ativo</td>
   <td>Pesquisar predicado para pesquisar ativos modificados recentemente </td>
   <td>
    <ul>
     <li>Nome da propriedade</li>
     <li>Valor da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Publicar status</td>
   <td>Pesquisar predicado para pesquisar ativos com base no status de publicação </td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status da expiração</td>
   <td>Pesquisar predicado para pesquisar ativos com base no status de expiração </td>
   <td>
    <ul>
     <li>Rótulo</li>
     <li>Nome da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Oculto</td>
   <td>Pesquisar predicado que define uma propriedade de campo oculta para pesquisar ativos</td>
   <td>
    <ul>
     <li>Nome da propriedade</li>
     <li>Valor da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Remover aspectos de pesquisa padrão {#removing-default-search-facets}

A Adobe recomenda ter cuidado ao remover aspectos de pesquisa padrão para evitar problemas de desempenho. A remoção de aspectos de pesquisa padrão também pode afetar o comportamento do recurso padrão.

Não remova os seguintes campos ocultos, pois isso causa um problema de desempenho de consulta com o OmniSearch e coleções inteligentes:

* group.2_group.type=dam:Asset

* group.1_group.type=nt:folder

* group.p.or=true

## Redefinir aspectos de pesquisa padrão {#restoring-default-search-facets}

Por padrão, um ícone Bloquear é exibido antes do **[!UICONTROL Painel de Pesquisa do Administrador do Assets]** na página **[!UICONTROL Pesquisar Forms]**. O ícone Bloquear desaparecerá se você adicionar aspectos de pesquisa ao formulário, indicando que o formulário padrão foi modificado.

O ícone de Bloqueio em relação a uma opção na página Pesquisar Forms indica que as configurações padrão estão intactas e não são personalizadas.

Para restaurar o aspecto de pesquisa padrão, execute estas etapas:

1. Selecione **[!UICONTROL Painel de Pesquisa do Administrador do Assets]** na página **[!UICONTROL Pesquisar Forms]**.
1. Selecione **[!UICONTROL Excluir]** ![ícone excluir](assets/do-not-localize/deleteoutline.png) na barra de ferramentas.
1. Na caixa de diálogo de confirmação, selecione **[!UICONTROL Excluir]** para remover as alterações personalizadas.

   Após excluir as alterações personalizadas nos aspectos de pesquisa, o ícone Bloquear será exibido novamente antes do **[!UICONTROL Painel de pesquisa do administrador de ativos]** na página **[!UICONTROL Formulários de pesquisa]**.

## Permissões de usuário {#user-permissions}

Se você não recebeu uma função de administrador, esta é uma lista de permissões necessárias para executar ações de edição, exclusão e visualização envolvendo aspectos de pesquisa.

| Ação | Permissão |
|---|---|
| Editar | Permissões de leitura e gravação no nó `/apps` no CRX. |
| Excluir | Permissões de leitura, gravação e exclusão no nó `/apps` no CRX. |
| Visualização | Permissões de leitura, gravação e exclusão no nó `/var/dam/content` no CRX. Além disso, as permissões de leitura e gravação no nó `/apps`. |

**Consulte também**

* [Pesquisar práticas recomendadas](search-best-practices.md)
* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Pesquisar ativos digitais](search-assets.md).
