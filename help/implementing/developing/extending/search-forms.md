---
title: Configuração de formulários de pesquisa
description: Configuração do Search Forms para Adobe Experience Manager as a Cloud Service.
exl-id: b06649c4-cc91-44e3-8699-00e90140b90d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 10%

---

# Configuração de formulários de pesquisa {#configuring-search-forms}

O Adobe Experience Manager as a Cloud Service vem com um poderoso mecanismo de [Pesquisa](/help/sites-cloud/authoring/search.md).

Em combinação com isso, também há um conjunto de opções predefinidas para ajudar você a filtrar seu conteúdo. Essas facetas predefinidas como **Data de Modificação**, **Status de Publicação** ou **Status da Live Copy** são mantidas para ajudá-lo a detalhar rapidamente os recursos necessários.

![uso de pesquisa e filtro](assets/csf-usage.png)

Juntos, eles têm como objetivo ajudá-lo a localizar seu conteúdo de forma rápida e fácil a partir de:

* [Pesquisar e filtrar](/help/sites-cloud/authoring/search.md#search-and-filter)
* [Seletor de painéis](/help/sites-cloud/authoring/basic-handling.md#rail-selector)
* o [Navegador Assets](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser) (ao editar páginas)

>[!NOTE]
>
>Você pode configurar o serviço [Pesquisa e indexação de conteúdo](/help/operations/indexing.md) subjacente.

Com o **Search Forms**, você pode personalizar e estender esses painéis, de acordo com suas necessidades específicas.

O **Forms de Pesquisa** fornece uma seleção predefinida de [predicados](#predicates-and-their-settings) que você pode combinar e definir. As [caixas de diálogo para configurar estes formulários](#configuring-your-search-forms) podem ser acessadas via:

* **Ferramentas**
   * **Geral**
      * **Pesquisar Forms**

## Forms padrão {#default-forms}

Ao acessar o console **Forms de Pesquisa** pela primeira vez, você pode ver que todas as configurações têm um símbolo de cadeado. Isso indica que a configuração correspondente é a configuração padrão (pronta para uso) e não pode ser excluída. Depois de personalizar e salvar, uma configuração do bloqueio desaparecerá. Ele reaparecerá quando você [excluir sua configuração personalizada](#deleting-a-configuration-to-reinstate-the-default). Nesse caso, o padrão (e o indicador de cadeado) será reinstalado.

![configurando a visão geral dos formulários de pesquisa](assets/csf-overview.png)

As configurações padrão (listadas alfabeticamente) disponíveis são:

* **Painel de pesquisa do administrador do Assets**
* **Editor de páginas (Pesquisa de documentos)**
* **Editor de páginas (Pesquisa de Fragmentos de Experiência)**
* **Editor de páginas (Pesquisa de imagens)**
* **Editor de páginas (Pesquisa de manuscrito)**
* **Editor de páginas (Pesquisa de páginas)**
* **Editor de páginas (Pesquisa de parágrafos)**
* **Editor de páginas (Pesquisa de produtos)**
* **Editor de páginas (pesquisa do Scene7)**
* **Editor de páginas (Pesquisa de vídeos)**
* **Trilho de pesquisa do administrador de projetos**
* **Trilho de pesquisa da tradução do projeto**
* **Painel de pesquisa do administrador de sites**
* **Trilho de pesquisa do administrador de trechos**
* **Painel de pesquisa do administrador do Stock**
* **Painel de Pesquisa de Modelos de Fragmento do Conteúdo**
* **Trilho de pesquisa do administrador de projetos**
* **Trilho de pesquisa da tradução do projeto**

>[!NOTE]
>
>Para obter mais detalhes sobre os formulários de pesquisa relacionados ao ativo, consulte [Assets - Pesquisar aspectos](/help/assets/search-facets.md).


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
   <td>Analytics</td>
   <td>Pesquise/filtre recursos no navegador do Sites ao mostrar dados alimentados por análise. Os filtros de pesquisa do Analytics são carregados para corresponder às colunas de análise personalizadas mapeadas.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status de aprovação</td>
   <td>Pesquisar de acordo com o status de aprovação.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Autor</td>
   <td>Pesquisar de acordo com o autor.</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Retirado por</td>
   <td>Procurar ativos verificados por um usuário específico.</td>
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
   <td>Pesquisar ativos com um status de check-out específico.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Componentes</td>
   <td>Permite que um autor pesquise/filtre por páginas com um componente específico. Por exemplo, uma galeria de imagens.<br /> </td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Nome da propriedade*</li>
     <li>Profundidade da propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo de datas</td>
   <td>Procure recursos criados em um intervalo especificado para uma propriedade de data. No painel Pesquisar, você pode especificar datas de início e término.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Espaço reservado</li>
     <li>Nome da propriedade*</li>
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
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tamanho do arquivo</td>
   <td>Filtrar recursos com base em seu tamanho.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tipo de arquivo</td>
   <td>Pesquise ativos com base no tipo de arquivo/mime.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li> 
     <li>Nome da propriedade*</li>
     <li>Caminho Mimetype</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Texto completo</td>
   <td>Predicado de pesquisa para pesquisas de texto completo. Ele é mapeado com o operador "jcr:contains".</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Nome de propriedade</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Grupo</td>
   <td>Predicado de pesquisa para grupo (usado somente dentro do Predicado do Insights).</td>
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
     <li>Nome da propriedade*</li>
     <li>Valor da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Insights</td>
   <td>Pesquise de acordo com uma seleção de parâmetros de Insights.</td>
   <td>Este é um predicado complexo composto de vários predicados:
    <ul>
     <li>Grupo</li>
     <li>Intervalo</li>
     <li>Opções</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Membro de coleção</td>
   <td>Pesquisar ativos que sejam membros de uma coleção</td>
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
     <li>Nome da propriedade*</li>
     <li>Suporte do delimitador</li>
     <li>Delimitadores de entrada</li>
     <li>Ignorar diferença entre maiúsculas e minúsculas</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Opções</td>
   <td><p>As opções são nós de conteúdo criados pelo usuário.</p> <p>Consulte <a href="#addinganoptionspredicate">Adicionando um Predicado de Opções</a> para obter mais informações.</p> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Seleção única</li>
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
     <li>Nome da propriedade*</li>
     <li>Caminho do nó de opções</li>
     <li>Profundidade da propriedade</li>
     <li>Seleção única</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status da página</td>
   <td>Filtrar páginas de acordo com seu status.</td>
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
   <td>Filtrar de acordo com o caminho específico. Você pode especificar vários caminhos como opções.</td>
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
     <li>Nome da propriedade (`path`)</li>
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
     <li>Nome de propriedade</li>
     <li>Pesquisa parcial</li>
     <li>Ignorar diferença entre maiúsculas e minúsculas</li>
     <li>Descrição</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>Publicar status</td>
   <td>Filtre recursos com base no status de publicação.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo</td>
   <td>Pesquisar recursos que estão dentro de um intervalo especificado. No painel Pesquisar, é possível especificar valores mínimos e máximos para o intervalo.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Avaliação</td>
   <td>Pesquise recursos de acordo com sua classificação média.<br /> </td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
     <li>Caminho de opção</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Data relativa</td>
   <td>Filtrar recursos com base na data relativa de sua criação. Por exemplo, 1 semana atrás, 1 mês atrás.</td>
   <td>
    <ul>
     <li>Rótulo do campo</li>
     <li>Nome da propriedade*</li>
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
     <li>Nome da propriedade*</li>
     <li>Caminho do nó de opções</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Status</td>
   <td>Pesquisar de acordo com o status de aprovação e check-out.</td>
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
     <li>Nível do campo</li>
     <li>Espaço reservado</li>
     <li>Nome da propriedade*</li>
     <li>Exibir a opção Corresponder todas as tags</li>
     <li>Caminho de tags raiz</li>
     <li>Descrição</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelos</td>
   <td>Pesquise de acordo com o template selecionado.</td>
   <td>
    <ul>
     <li>Espaço reservado</li>
     <li>Nome da propriedade*</li>
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
>Os predicados de pesquisa comuns são definidos em:
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>Estas informações são somente para referência, você não deve alterar `/libs`.

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### Configurações de predicado {#predicate-settings}

Dependendo do predicado, uma seleção de configurações está disponível para configuração, incluindo:

* **Rótulo do campo**

  O rótulo que aparecerá como o cabeçalho recolhível ou como o rótulo do campo do predicado.

* **Descrição**

  Detalhes descritivos do usuário.

* **Espaço reservado**

  Texto vazio ou o marcador de posição do predicado, caso nenhum texto de filtragem seja inserido.

* **Nome da Propriedade**

  A propriedade a ser pesquisada. Ele usa um caminho relativo e os curingas `*/*/*` especificam a profundidade da propriedade em relação ao nó `jcr:content` (cada asterisco representa um nível de nó).

  Se você deseja pesquisar apenas em um nó filho de primeiro nível do recurso que tem a propriedade `x` no nó `jcr:content`, use `*/jcr:content/x`

* **Profundidade da propriedade**

  A profundidade máxima para pesquisar essa propriedade nos recursos. Assim, uma pesquisa nessa propriedade pode ser executada em um recurso e em filhos recursivos até que o nível dos filhos seja igual à profundidade especificada.

* **Valor da propriedade**

  O valor da propriedade como uma cadeia absoluta ou linguagem de expressão; por exemplo, `cq:Page` ou

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Texto do Intervalo**

  O rótulo do campo de intervalo no predicado **Intervalo de datas**.

* **Caminho da opção**

  O usuário pode selecionar o caminho usando o Navegador de caminho na guia de configuração do predicado. Após selecionar o ícone **+**, é usado para adicionar a seleção à lista de opções válidas (em seguida, o ícone **-** é removido, se necessário).

  As opções são nós de conteúdo criados pelo usuário, com a seguinte estrutura:

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Caminho do nó de opções**
Efetivamente igual ao **Caminho de opções**, somente isso está no campo de predicado comum, o outro é específico para ativos.

* **Seleção única**
Se marcadas, as opções são renderizadas como caixas de seleção que permitem apenas uma única seleção. Se for marcada por engano, uma caixa de seleção pode ser desmarcada.

* **Nome(s) de Propriedade(s) de Publicação e Live Copy**
Os rótulos das caixas de seleção Publicar e Live Copy para o predicado específico do Sites.

* O &ast; nos rótulos de campo na guia **Configurações** significa que os campos são obrigatórios e, se deixado em branco, uma mensagem de erro será exibida.

## Configuração do Forms de pesquisa {#configuring-your-search-forms}

### Criação/abertura de uma configuração personalizada {#creating-opening-a-customized-configuration}

1. Navegue até **Ferramentas**, **Geral**, **Pesquisar Forms**.

1. Selecione a configuração que deseja personalizar.
1. Use o ícone **Editar** para abrir a configuração para atualização.
1. Se for feita uma nova personalização, você provavelmente desejará [adicionar novos campos de predicado e definir as configurações](#add-edit-a-predicate-field-and-define-field-settings) conforme necessário. Se houver uma personalização, você poderá selecionar um campo existente e [atualizar as configurações](#add-edit-a-predicate-field-and-define-field-settings).
1. Selecione **Concluído** para salvar a configuração. Suas alterações poderão ser vistas na próxima vez que a configuração for usada.

   >[!NOTE]
   >
   >As configurações personalizadas são armazenadas (conforme apropriado) em:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### Adicionar/editar um campo de predicado e definir configurações de campo {#add-edit-a-predicate-field-and-define-field-settings}

É possível adicionar ou editar campos e definir/atualizar suas configurações:

1. [Abra a configuração personalizada](#creating-opening-a-customized-configuration) para atualização.
1. Se quiser adicionar um novo campo, abra a guia **Selecionar predicado** e arraste o predicado necessário para o local desejado. Por exemplo, o **Predicado do intervalo de datas**:

   ![adicionar um predicado](assets/csf-add-predicate.png)

1. Dependendo se:

   * Você está adicionando um novo campo:

     Depois de adicionar o predicado, a guia **Configurações** é aberta e mostra as propriedades que podem ser definidas.

   * Você deseja atualizar um predicado existente:

     Selecione o campo de predicado (à direita) e abra a guia **Configurações**.

   Por exemplo, as configurações para o **Predicado do intervalo de datas**:

   ![modificar predicado](assets/csf-modify-predicate.png)

1. Faça as alterações necessárias e confirme com **Concluído**. Suas alterações poderão ser vistas na próxima vez que a configuração for usada.

### Pré-visualização da configuração de pesquisa {#previewing-the-search-configuration}

1. Selecione o ícone Visualizar:

   ![ícone de visualização](assets/csf-preview-icon.png)

1. Exibe os formulários de pesquisa conforme são mostrados (totalmente expandidos) na coluna Pesquisa do console apropriado.

   ![formulário de visualização](assets/csf-preview-form.png)

1. **Feche** a visualização para retornar e concluir a configuração.

### Exclusão de um campo de predicado {#deleting-a-predicate-field}

1. [Abra a configuração personalizada](#creating-opening-a-customized-configuration) para atualização.
1. Selecione o campo de predicado (à direita), abra a guia **Configurações** e selecione o ícone **Excluir** (canto inferior esquerdo).

   ![ícone excluir](assets/csf-delete-icon.png)

1. Uma caixa de diálogo solicitará a confirmação da ação de exclusão.

1. Confirme esta e todas as outras alterações com **Concluído**.

### Excluir uma configuração (para restaurar o padrão) {#deleting-a-configuration-to-reinstate-the-default}

Depois de personalizar uma configuração, ela substituirá os padrões. Você pode restaurar a configuração padrão excluindo sua configuração personalizada.

>[!NOTE]
>
>Não é possível excluir as configurações padrão.

A exclusão de uma configuração personalizada é feita no console:

1. Selecione a configuração necessária (por exemplo, **Editor de páginas (pesquisa de parágrafos)**) e o ícone **Excluir** na barra de ferramentas:

   ![restaurar padrão](assets/csf-restore-default.png)

1. A configuração personalizada é excluída e o padrão é restabelecido (isso é indicado pela reaparição do símbolo de cadeado no console).

### Adição de predicados de opções {#adding-options-predicates}

Os predicados de opção (Opções, Propriedade de opções) permitem configurar um item a ser pesquisado. Normalmente, eles são usados para pesquisar algo diretamente na página; por exemplo, uma propriedade no nó da página.

O exemplo a seguir (para pesquisar de acordo com o modelo usado para criar uma página) ilustra as etapas envolvidas:

1. Crie o nó que define a propriedade na qual será pesquisada.

   Você precisa de um nó raiz que contenha definições das opções individuais para estar disponível ao usuário.

   Os nós das opções individuais precisam das propriedades:

   * `jcr:title` - o rótulo de campo a ser exibido no painel de pesquisa
   * `value` - o valor da propriedade a ser pesquisada

   ![Definição de predicado](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >Você ***deve*** não alterar nada no caminho `/libs`.
   >
   >Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
   >
   >O método recomendado para configuração e outras alterações é:
   >
   >1. Recrie o item necessário, como ele existe em `/libs`, em `/apps`. Nesse caso, de:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Fazer alterações em `/apps.`

1. Abra o console **Forms de Pesquisa** e selecione a configuração que deseja atualizar. Por exemplo, **Painel de pesquisa do administrador de sites**. Em seguida, selecione **Editar**.

1. Dependendo da configuração, adicione uma **Propriedade de Opções** ou **Propriedade de Opções** à configuração.
1. Atualize os campos, especialmente:

   * **Nome da Propriedade**

     Específica a propriedade do nó a ser pesquisada nos nós de destino. Por exemplo:

     `jcr:content/cq:template`

   * **Caminho do nó de opção**

     Selecione o caminho para onde as opções são mantidas. Por exemplo:

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![Predicados de opção](assets/csf-options-predicate-02.png)

1. Selecione **Concluído** para salvar sua configuração.
1. Navegue até o console apropriado (neste exemplo, **Sites**) e abra o painel **Pesquisar - Filtros**. Os formulários de pesquisa recém-definidos, juntamente com as várias opções, ficam visíveis. Selecione a opção necessária para ver os resultados da pesquisa.

   ![opções sendo usadas](assets/csf-options-usage.png)


## Permissões de usuário {#user-permissions}

A tabela a seguir lista as permissões necessárias para executar ações de edição, exclusão e visualização em formulários de pesquisa.

<table>
 <thead>
  <tr>
   <td><strong>Ação</strong></td>
   <td><strong>Permissões</strong></td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Editar </td>
   <td>Permissões de Leitura e Gravação no nó <code>/apps </code>.</td>
  </tr>
  <tr>
   <td>Excluir</td>
   <td>Permissões de Leitura, Gravação e Exclusão no nó <code>/apps</code></td>
  </tr>
  <tr>
   <td>Visualização</td>
   <td>Permissões de leitura, gravação e exclusão no nó <code>/var/dam/content</code>.<br /> permissões de Leitura e Gravação no nó <code>/apps</code>.</td>
  </tr>
 </tbody>
</table>
