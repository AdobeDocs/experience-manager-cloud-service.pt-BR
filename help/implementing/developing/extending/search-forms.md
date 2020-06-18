---
title: Configuração de formulários de pesquisa
description: Configuração de formulários de pesquisa para Adobe Experience Manager como Cloud Service.
translation-type: tm+mt
source-git-commit: 18841ec94b8dd92ca92deda0869f2698786458aa
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 16%

---


# Configuração de formulários de pesquisa {#configuring-search-forms}

Adobe Experience Manager como Cloud Service, vem com um poderoso mecanismo de [pesquisa](/help/sites-cloud/authoring/getting-started/search.md) .

Em combinação com isso, também há um conjunto de opções predefinidas para ajudar a filtrar o conteúdo. Eles possuem aspectos predefinidos, como Data **** Modificada, Status **de** Publicação ou Status **do** Livecopy, para ajudá-lo a detalhar rapidamente os recursos necessários.

![uso de pesquisa e filtro](assets/csf-usage.png)

Juntas, essas metas ajudam a localizar o conteúdo de forma rápida e fácil:

* [Pesquisar e filtrar](/help/sites-cloud/authoring/getting-started/search.md#search-and-filter)
* [Seletor de painéis](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)
* o Navegador [de](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) ativos (ao editar páginas)

>[!NOTE]
>
>Você pode configurar o serviço subjacente de Pesquisa e Indexação [de](/help/operations/indexing.md) Conteúdo.

Usando o **Search Forms**, você pode personalizar e estender esses painéis, de acordo com suas necessidades específicas.

O **Search Forms** fornece uma seleção predefinida de [predicados](#predicates-and-their-settings) que você pode combinar e definir. As [caixas de diálogo para configurar esses formulários](#configuring-your-search-forms) podem ser acessadas por meio de:

* **Ferramentas**

   * **Geral**

      * **Formulários de pesquisa**

## Formulários padrão {#default-forms}

Ao acessar o console **Pesquisar formulários** pela primeira vez, é possível ver que todas as configurações têm um símbolo de cadeado. Isso indica que a configuração correspondente é a configuração padrão (out-of-the-box) e não pode ser excluída. Depois que você tiver personalizado e salvo, uma configuração do bloqueio desaparecerá. Ele será reexibido quando você [excluir sua configuração](#deleting-a-configuration-to-reinstate-the-default)personalizada; nesse caso, o padrão (e o indicador de cadeado) será reinstalado.

![configuração da visão geral dos formulários de pesquisa](assets/csf-overview.png)

As configurações padrão (listadas em ordem alfabética) disponíveis são:

* **Trilho de pesquisa do administrador de ativos:**

* **Editor de páginas (Pesquisa de documentos):**

* **Editor de páginas (Pesquisa de Fragmentos de experiência):**

* **Editor de páginas (Pesquisa de imagens):**

* **Editor de páginas (Pesquisa de manuscrito):**

* **Editor de páginas (Pesquisa de páginas):**

* **Editor de páginas (Pesquisa de parágrafos):**

* **Editor de páginas (Pesquisa de produto):**

* **Editor de páginas (pesquisa do Scene7)**:

* **Editor de página (Pesquisa de vídeos)**:

* **Trilho de pesquisa do administrador de projetos:**

* **Painel de pesquisa de tradução de projetos:**

* **Trilho de pesquisa do administrador de sites**:

* **Painel de pesquisa do administrador de trechos**:

* **Painel de pesquisa do Admin do Stock**:

>[!NOTE]
>
> Para obter mais detalhes sobre os formulários de pesquisa relacionados ao ativo, consulte [Ativos - Aspectos de pesquisa](/help/assets/search-facets.md)


## Predicados e suas configurações {#predicates-and-their-settings}

### Predicados {#predicates}

Os seguintes predicados estão disponíveis, dependendo da configuração:

<table>
 <tbody>
  <tr>
   <th>Predicado</th>
   <th>Propósito</th>
   <th>Configurações</th>
  </tr>
  <tr>
   <td>Análise</td>
   <td>Recursos de pesquisa/filtro no navegador Sites ao mostrar dados ativados pelo Analytics. Os filtros de pesquisa do Analytics são carregados para corresponder às colunas de análise personalizadas mapeadas.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status de aprovação</td>
   <td>Pesquise de acordo com o status de aprovação.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Autor</td>
   <td>Pesquise de acordo com o autor.</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Retirado por</td>
   <td>Procure ativos cujo check-out foi feito por um usuário específico.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Espaço reservado</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Status da retirada</td>
   <td>Procure ativos com um status de check-out específico.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Componentes</td>
   <td>Permite que um autor pesquise/filtre por páginas que têm um componente específico nele. For example an image gallery.<br /> </td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade*</li>
     <li>Profundidade da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo de datas</td>
   <td>Procure recursos criados em um intervalo especificado para uma propriedade de data. No painel Pesquisar, é possível especificar datas de Start e término.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade*</li>
     <li>Texto do intervalo (de)*</li>
     <li>Texto do intervalo (até)*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status da expiração</td>
   <td>Pesquisar recursos com base no status de expiração.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tamanho do arquivo</td>
   <td>Filtre os recursos com base no tamanho.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tipo de arquivo</td>
   <td>Pesquisar ativos com base no tipo de arquivo/mime.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li> 
     <li>Nome da Propriedade*</li>
     <li>Caminho Mimetype</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Texto completo</td>
   <td>Projetar pesquisa para pesquisas de texto completo. Ela é mapeada com o operador ‘jcr:contains’.</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Grupo</td>
   <td>Predicado de pesquisa para grupo (usado somente no Predicado de insights).</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Filtro oculto</td>
   <td>Um filtro na propriedade e no valor, não visível para o usuário.</td>
   <td>
    <ul>
     <li>Nome da Propriedade*</li>
     <li>Valor da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Insights</td>
   <td>Pesquisar de acordo com uma seleção de parâmetros do Insights.</td>
   <td>Este é um predicado complexo composto de vários predicados:
    <ul>
     <li>Grupo</li>
     <li>Intervalo</li>
     <li>Opções</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Membro da coleção</td>
   <td>Procurar ativos que sejam membros de uma coleção</td>
   <td>
    <ul>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Propriedade de valores múltiplos</td>
   <td>Pesquisar em vários valores de uma propriedade especificada.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade*</li>
     <li>Suporte do delimitador</li>
     <li>Delimitadores de entrada</li>
     <li>Ignorar diferença entre maiúsculas e minúsculas</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Opções</td>
   <td><p>As opções são nós de conteúdo criados pelo usuário.</p> <p>Consulte <a href="#addinganoptionspredicate">Adicionando um Predicado</a> de opções para obter mais informações.</p> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Única seleção</li>
     <li>Adicionar opções</li>
     <li>Manual</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Propriedade de opções</td>
   <td>Pesquise em uma ou mais propriedades da opção.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Caminho do nó de opções</li>
     <li>Profundidade da propriedade</li>
     <li>Única seleção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status da página</td>
   <td>Filtre as páginas de acordo com seu status.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade de publicação*</li>
     <li>Nome de propriedade das páginas bloqueadas*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Caminho</td>
   <td>Filtrar de acordo com o caminho específico. É possível especificar vários caminhos como opções.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Adicionar caminhos de pesquisa</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Navegador de caminhos</td>
   <td>Forneça um navegador de caminho para pesquisar em um caminho raiz predefinido.</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Caminho raiz</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Caminho oculto</td>
   <td>Um filtro no caminho, não visível para o usuário.</td>
   <td>
    <ul>
     <li>Nome da Propriedade (`path`)</li>
     <li>Valor da propriedade (`/content/dam`)</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Propriedade</td>
   <td>Pesquisar em uma propriedade especificada.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade</li>
     <li>Pesquisa parcial</li>
     <li>Ignorar diferença entre maiúsculas e minúsculas</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Publicar status</td>
   <td>Filtre os recursos com base no status de publicação.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo</td>
   <td>Pesquise os recursos que estão dentro de um intervalo especificado. No painel Pesquisar, você pode especificar valores mínimos e máximos para o intervalo.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Classificação</td>
   <td>Procure recursos de acordo com sua classificação média.<br /> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Data relativa</td>
   <td>Filtre os recursos com base na data relativa de sua criação. Por exemplo, 1 semana atrás, 1 mês atrás.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Data relativa</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo do controle deslizante</td>
   <td>Um predicado de pesquisa comum que estende o predicado de intervalo com o recurso de controle deslizante. O valor da propriedade pesquisada deve estar entre os limites do controle deslizante.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da Propriedade*</li>
     <li>Caminho do nó de opções</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status</td>
   <td>Pesquise de acordo com o status de aprovação e check-out.</td>
   <td>Este é um predicado complexo composto de vários predicados:
    <ul>
     <li>Status de aprovação</li>
     <li>Status da retirada</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Tags</td>
   <td>Pesquisar com base em tags.</td>
   <td>
    <ul>
     <li>Campo Lavel</li>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade*</li>
     <li>Exibir a opção Corresponder todas as tags</li>
     <li>Caminho das tags raiz</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelos</td>
   <td>Pesquisar de acordo com o modelo selecionado.</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Nome da Propriedade*</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Status da tradução</td>
   <td>Pesquisar de acordo com o status da tradução.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
    </ul> 
   </td>
  </tr>
 </tbody>
</table>

<!--
  <tr>
   <td>Date ???</td>
   <td>Slider-based search of assets based on a date property.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Asset Last Modified ?????</td>
   <td>Date the asset was last modified.<br /> </td>
   <td>A customized predicate, based on the Date Predicate.</td>
  </tr>
  <tr>
   <td>Range Options ???</td>
   <td>A specific search predicate for Assets and the same as common Slider Predicate. Is still available due to backward compatibilty issues.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Search assets based on tags. You can configure the Path property to populate various tags in the Tags list.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
-->

>[!NOTE]
>
>* Os predicados de pesquisa comuns são definidos em:
   >  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>
Essas informações são apenas para referência, você não deve fazer alterações em `/libs`.

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### Configurações de previsão {#predicate-settings}

Dependendo do predicado, uma seleção de configurações está disponível para configuração, incluindo:

* **Rótulo do campo**

   O rótulo que aparecerá como o cabeçalho flexível ou como o rótulo do campo do predicado.

* **Descrição**

   Detalhes descritivos do usuário.

* **Espaço reservado**

   Texto vazio ou o espaço reservado do predicado caso nenhum texto de filtragem seja inserido.

* **Nome da Propriedade**

   A propriedade a ser pesquisada. Ele usa um caminho relativo e os curingas `*/*/*` especificam a profundidade da propriedade em relação ao `jcr:content` nó (cada asterisco representa um nível de nó).

   Se você quiser pesquisar somente em um nó filho de primeiro nível do recurso que tenha a `x` propriedade no `jcr:content` nó, use `*/jcr:content/x`

* **Profundidade da propriedade**

   A profundidade máxima para procurar essa propriedade dentro dos recursos. Portanto, uma pesquisa nessa propriedade pode ser executada em um recurso e filhos recursivos até que o nível dos filhos seja igual a profundidade especificada.

* **Valor da propriedade**

   O valor da propriedade como uma string absoluta ou como uma linguagem de expressão; por exemplo, `cq:Page` ou

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Texto do intervalo**

   O rótulo do campo de intervalo no predicado Intervalo de **datas** .

* **Caminho de opção**

   O usuário pode selecionar o caminho usando o Navegador de caminhos na guia de configuração de predicado. Depois de selecionar o ícone **+** , a seleção é usada para adicionar à lista de opções válidas (em seguida, o ícone **-** para remover, se necessário).

   As opções são nós de conteúdo criados pelo usuário, com a seguinte estrutura:

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Caminho** do nó OpçõesEfetivamente o mesmo que o 
**Caminho** de opções, somente este está no campo predicado comum comum, o outro é específico para ativos.

* **Seleção**&#x200B;única Se marcada, as opções são renderizadas como caixas de seleção que permitem apenas uma seleção. Se estiver selecionado por engano, uma caixa de seleção pode ser desmarcada.

* **Nome(s) de propriedade de publicação e Live Copy** Os rótulos das caixas de seleção de publicação e live copy para o predicado específico Sites.

* O &amp;ast; nos rótulos de campo na guia **Configurações** significa que os campos são obrigatórios e, se deixados em branco, uma mensagem de erro será exibida.

## Configuração dos formulários de pesquisa {#configuring-your-search-forms}

### Criando/Abrindo uma Configuração Personalizada {#creating-opening-a-customized-configuration}

1. Navegue até **Ferramentas**, **Geral**, **Pesquisar formulários**.

1. Selecione a configuração que deseja personalizar.
1. Use o ícone **Editar** para abrir a configuração para atualização.
1. Se uma nova personalização você provavelmente desejará [adicionar novos campos de predicado e definir as configurações](#add-edit-a-predicate-field-and-define-field-settings) conforme necessário. Se uma personalização existente você pode selecionar um campo existente e [atualizar as configurações](#add-edit-a-predicate-field-and-define-field-settings).
1. Select **Done** to save the configuration. Suas alterações poderão ser vistas na próxima vez que a configuração for usada.

   >[!NOTE]
   >
   >As configurações personalizadas são armazenadas (conforme o caso) em:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### Adicionar/editar um campo previsto e definir configurações de campo {#add-edit-a-predicate-field-and-define-field-settings}

Você pode adicionar ou editar campos e definir/atualizar suas configurações:

1. [Abra a configuração](#creating-opening-a-customized-configuration) personalizada para atualização.
1. Se você quiser adicionar um novo campo, abra a guia **Selecionar predicado** e arraste o predicado necessário para o local desejado. Por exemplo, o Predicado **de intervalo de** datas:

   ![adicionar um predicado](assets/csf-add-predicate.png)

1. Dependendo de:

   * Você está adicionando um novo campo:

      Depois de adicionar o predicado, a guia **Configurações** abrirá e mostrará as propriedades que podem ser definidas.

   * Você deseja atualizar um predicado existente:

      Selecione o campo predicado (à direita) e abra a guia **Configurações** .
   Por exemplo, as configurações para o Predicado **de intervalo de** datas:

   ![modificar predicado](assets/csf-modify-predicate.png)

1. Faça as alterações necessárias e confirme com **Concluído**. Suas alterações poderão ser vistas na próxima vez que a configuração for usada.

### Pré-visualização da Configuração de Pesquisa {#previewing-the-search-configuration}

1. Selecione o ícone de Pré-visualização:

   ![Ícone pré-visualização](assets/csf-preview-icon.png)

1. Isso exibirá os formulários de pesquisa da forma que eles serão exibidos (totalmente expandidos) na coluna Pesquisar do console apropriado.

   ![formulário de pré-visualização](assets/csf-preview-form.png)

1. **Feche** a pré-visualização para retornar e concluir a configuração.

### Excluindo um campo de previsão {#deleting-a-predicate-field}

1. [Abra a configuração](#creating-opening-a-customized-configuration) personalizada para atualização.
1. Selecione o campo predicado (à direita), abra a guia **Configurações** e selecione o ícone **Excluir** (embaixo à esquerda).

   ![ícone excluir](assets/csf-delete-icon.png)

1. Uma caixa de diálogo solicitará a confirmação da ação de exclusão.

1. Confirme esta e quaisquer outras alterações com **Concluído**.

### Excluindo uma configuração (para reinstalar o padrão) {#deleting-a-configuration-to-reinstate-the-default}

Depois de personalizar uma configuração, isso substituirá os padrões. É possível reinstalar a configuração padrão excluindo a configuração personalizada.

>[!NOTE]
>
>Não é possível excluir as configurações padrão.

A exclusão de uma configuração personalizada é feita do console:

1. Selecione a configuração necessária (por exemplo, Editor de **páginas (pesquisa de parágrafos)** e, em seguida, o ícone **Excluir** na barra de ferramentas:

   ![restaurar padrão](assets/csf-restore-default.png)

1. A configuração personalizada será excluída e o padrão será reinstalado (isso é indicado pelo reaparecimento do símbolo de cadeado no console).

### Adicionando Predicados de Opções {#adding-options-predicates}

Os predicados de opção (Opções, Propriedade de opções) permitem que você configure um item a ser pesquisado. Normalmente, eles são usados para procurar algo diretamente abaixo da página; por exemplo, uma propriedade no nó da página.

O exemplo a seguir (para pesquisar de acordo com o modelo usado para criar uma página) ilustra as etapas envolvidas:

1. Crie o nó que define a propriedade a ser pesquisada.

   Você precisará de um nó raiz contendo as definições das opções individuais para estar disponível para o usuário.

   Os nós das opções individuais precisam das propriedades:

   * `jcr:title` - o rótulo do campo a ser mostrado no painel de pesquisa
   * `value` - o valor da propriedade a ser pesquisada

   ![Definição de previsão](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >Você não ***deve*** alterar nada no `/libs` caminho.
   >
   >Isso ocorre porque o conteúdo do é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos). `/libs`
   >
   >O método recomendado para configuração e outras alterações é:
   >
   >1. Recrie o item desejado, como ele existe em `/libs`, em `/apps`. Neste caso a partir de:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Faça quaisquer alterações em `/apps.`


1. Abra o console **Pesquisar formulários** e selecione a configuração que deseja atualizar. Por exemplo, Painel **de pesquisa do administrador de** sites. Em seguida, selecione **Editar**.

1. Dependendo da configuração, adicione uma Propriedade **Options** ou **Options** à configuração.
1. Atualize os campos, em especial:

   * **Nome da Propriedade**

      Específico da propriedade node a ser pesquisada nos nós do público alvo. Por exemplo:

      `jcr:content/cq:template`

   * **Caminho do nó de opção**

      Selecione o caminho para onde suas opções são mantidas. Por exemplo:

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![Previsões de opção](assets/csf-options-predicate-02.png)

1. Select **Done** to save your configuration.
1. Navegue até o console apropriado (neste exemplo, **Sites**) e abra o painel **Pesquisar - Filtros** . Os formulários de pesquisa recém-definidos, juntamente com as várias opções, estarão visíveis. Selecione a opção necessária para ver os resultados da pesquisa.

   ![opções que estão sendo usadas](assets/csf-options-usage.png)


## Permissões de usuário {#user-permissions}

A tabela a seguir lista as permissões necessárias para executar ações de edição, exclusão e pré-visualização em formulários de pesquisa.

<table>
 <thead>
  <tr>
   <td><strong>Ação</strong></td>
   <td><strong>Permissões    </strong></td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Editar </td>
   <td>Permissões de leitura e gravação no <code>/apps </code>nó.</td>
  </tr>
  <tr>
   <td>Excluir</td>
   <td>Permissões de Leitura, Gravação e Exclusão no <code>/apps</code> nó</td>
  </tr>
  <tr>
   <td>Visualizar</td>
   <td>Permissões de Leitura, Gravação e Exclusão no <code>/var/dam/content</code> nó.<br /> Permissões de leitura e gravação no <code>/apps</code> nó.</td>
  </tr>
 </tbody>
</table>
