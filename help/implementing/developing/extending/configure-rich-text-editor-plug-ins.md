---
title: Configure os plug-ins do Editor de Rich Text [!DNL Adobe Experience Manager].
description: Saiba como configurar [!DNL Adobe Experience Manager] os plug-ins do Editor de Rich Text.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 739dde6f9a6a7f4fe773e27e53f23a395f2881dc
workflow-type: tm+mt
source-wordcount: '4301'
ht-degree: 3%

---


# Configurar os plug-ins do Editor de Rich Text {#configure-the-rich-text-editor-plug-ins}

As funcionalidades do RTE são disponibilizadas por meio de uma série de plug-ins, cada um com a propriedade features. Você pode configurar a propriedade features para ativar ou desativar um ou mais recursos do RTE. Este artigo descreve como configurar especificamente os plug-ins RTE.

Para obter detalhes sobre as outras configurações do RTE, consulte [configurar o Editor](/help/implementing/developing/extending/rich-text-editor.md)de Rich Text.

>[!NOTE]
>
>Ao trabalhar com o CRXDE Lite, é recomendável salvar as alterações regularmente usando a opção [!UICONTROL Salvar tudo] .

## Ativar um plug-in e configurar a propriedade features {#activateplugin}

Para ativar um plug-in, siga estas etapas. Algumas etapas são necessárias somente quando você configura um plug-in pela primeira vez, pois os nós correspondentes não existem.

Por padrão, `format`, `link`, `list`e `justify``control` plug-ins e todos os seus recursos estão habilitados no RTE.

>[!NOTE]
>
>O respectivo `rtePlugins` nó é chamado `<rtePlugins-node>` para evitar a duplicação neste artigo.

1. Usando o CRXDE Lite, localize o componente de texto para seu projeto.
1. Crie o nó pai de `<rtePlugins-node>` se ele não existir, antes de configurar qualquer plug-in RTE:

   * Dependendo do seu componente, os nós principais são:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * um nó de configuração alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * São do tipo: **jcr:PrimaryType** `cq:Widget`
   * Ambas têm a seguinte propriedade:

      * **Nome** `name`
      * **Tipo** `String`
      * **Valor** `./text`


1. Dependendo da interface para a qual você está configurando, crie um nó `<rtePlugins-node>`, se ele não existir:

   * **Nome** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Abaixo, crie um nó para cada plug-in que você deseja ativar:

   * **Tipo** `nt:unstructured`
   * **Nomeie** a ID do plug-in necessário

Depois de ativar um plug-in, siga estas diretrizes para configurar a `features` propriedade.

|  | Ativar todos os recursos | Ative alguns recursos específicos. | Desative todos os recursos. |
|---|---|---|---|
| Nome | feições | feições | feições |
| Tipo | Sequência de caracteres | `String` (multistring; defina Tipo como `String` e clique `Multi` no CRXDE Lite) | Sequência de caracteres |
| Valor | `*` (um asterisco) | Defina para um ou mais valores de recurso. | - |

## Entenda o plug-in findreplace {#findreplace}

O plug- `findreplace` -in não precisa de nenhuma configuração. Funciona fora da caixa.

Ao usar a funcionalidade de substituição, a string de substituição a ser substituída deve ser inserida ao mesmo tempo que a string de localização. No entanto, você ainda pode clicar em localizar para procurar a string antes de substituí-la. Se a string de substituição for inserida após clicar em Localizar, a pesquisa será redefinida para o início do texto.

A caixa de diálogo localizar e substituir fica transparente quando a localização é clicada e se torna opaca quando a substituição é clicada. O comportamento permite que o autor reveja o texto a ser substituído. Se os usuários clicarem em substituir tudo, a caixa de diálogo será fechada e exibirá o número de substituições feitas.

## Configurar os modos de colagem {#pastemodes}

Ao usar o RTE, os autores podem colar o conteúdo em um dos três modos a seguir:

* **Modo** de navegador: Cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode introduzir marcações indesejadas.

* **Modo** de texto simples: Cole o conteúdo da área de transferência como texto sem formatação. Remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir no [!DNL Experience Manager] componente.

* **Modo** MS Word: Cole o texto, incluindo tabelas, com a formatação ao copiar do MS Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou o MS Excel, e a formatação apenas parcial é mantida.

### Configure as opções de Colagem disponíveis na barra de ferramentas do RTE  {#configure-paste-options-available-on-the-rte-toolbar}

Você pode fornecer alguns, todos ou nenhum desses três ícones aos seus autores na barra de ferramentas do RTE:

* **[!UICONTROL Colar (Ctrl+V)]**: Pode ser pré-configurado para corresponder a um dos três modos Colar acima.

* **[!UICONTROL Colar como texto]**: Fornece funcionalidade de modo de texto simples.

* **[!UICONTROL Colar do Word]**: Fornece a funcionalidade do modo MS Word.

Para configurar o RTE para exibir os ícones necessários, siga estas etapas.

1. Navegue até o seu componente, por exemplo `/apps/<myProject>/components/text`.
1. Navegue até o nó `rtePlugins/edit`. Consulte [ativar um plug-in](#activateplugin) se o nó não existir.
1. Crie a `features` propriedade no `edit` nó e adicione um ou mais dos recursos. Salve todas as alterações.

### Configurar o comportamento do ícone e do atalho Colar (Ctrl+V) {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Você pode pré-configurar o comportamento do ícone **[!UICONTROL Colar (Ctrl+V)]** , usando as seguintes etapas. Essa configuração também define o comportamento do atalho de teclado Ctrl+V que os Autores usam para colar o conteúdo.

A configuração permite os três tipos de casos de uso a seguir:

* Cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode introduzir marcações indesejadas. Configurado usando `browser` abaixo.

* Cole o conteúdo da área de transferência como texto sem formatação. Remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir no [!DNL Experience Manager] componente. Configurado usando `plaintext` abaixo.

* Cole o texto, incluindo tabelas, com a formatação ao copiar do MS Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou o MS Excel, e a formatação apenas parcial é mantida. Configurado usando `wordhtml` abaixo.

1. Em seu componente, navegue até o `<rtePlugins-node>/edit` nó. Crie os nós se eles não existirem. Para obter mais informações, consulte [ativar um plug-in](#activateplugin).
1. No `edit` nó, crie uma propriedade usando os seguintes detalhes:

   * **Nome** `defaultPasteMode`
   * **Tipo** `String`
   * **O valor** é um dos modos de colagem `browser`, `plaintext`ou `wordhtml` necessários.

### Configurar os formatos permitidos ao colar conteúdo {#pasteformats}

O modo colar como Microsoft Word (`paste-wordhtml`) pode ser configurado ainda mais para que você possa permitir explicitamente alguns estilos ao colar em outro programa, como [!DNL Experience Manager] [!DNL Microsoft Word].

Por exemplo, se apenas formatos em negrito e listas forem permitidos ao colar em, [!DNL Experience Manager]você poderá filtrar os outros formatos. Isso é chamado de filtragem de colagem configurável, que pode ser feita para ambos:

* [Texto](#pastemodes)
* [Links](#linkstyles)

Para links, também é possível definir os protocolos que são automaticamente aceitos.

Para configurar quais formatos são permitidos ao colar texto em [!DNL Experience Manager] de outro programa:

1. Em seu componente, navegue até o nó `<rtePlugins-node>/edit`. Crie os nós se o nó não existir. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie um nó sob o `edit` nó para manter as regras de colagem HTML:

   * **Nome** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Crie um nó em `htmlPasteRules`, para manter detalhes dos formatos básicos permitidos:

   * **Nome** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Para controlar os formatos individuais aceitos, crie uma ou mais das seguintes propriedades no `allowBasics` nó:

   * **Nome** `bold`
   * **Nome** `italic`
   * **Nome** `underline`
   * **Nome** `anchor` (para links e âncoras nomeadas)
   * **Nome** `image`

   Todas as propriedades são do **Tipo** , portanto, no `Boolean`Valor **** apropriado, você pode selecionar ou remover a marca de seleção para ativar ou desativar a funcionalidade.

   >[!NOTE]
   >
   >Se não estiver explicitamente definido, o valor padrão de true será usado e o formato será aceito.

1. Outros formatos também podem ser definidos usando uma variedade de outras propriedades ou nós, também aplicados ao `htmlPasteRules` nó:

| Propriedade | Tipo | Descrição |
|--- |--- |--- |
| `allowBlockTags` | `String` | Define a lista de tags de bloqueio permitidas. Algumas tags de bloco possíveis incluem títulos (h1, h2, h3), parágrafos (p), listas (ol, ul), tabelas (tabela). |
| `fallbackBlockTag` | `String` | Define a tag de bloco usada para qualquer bloco que tenha uma tag de bloco não incluída em `allowBlockTags`. Normalmente, `p` basta. |
| `table` | `nt:unstructured` | Define o comportamento ao colar tabelas. Esse nó deve ter a propriedade que permite (digite Booliano) para definir se a colagem de tabelas é permitida. Se allow estiver definido como false, você deverá especificar a propriedade ignoreMode (tipo String) para definir como o conteúdo da tabela colada é tratado. Valores válidos para ignoreMode são `remove` para remover o conteúdo da tabela e `paragraph` transformar as células da tabela em parágrafos. |
| `list` | `nt:unstructured` | Define o comportamento ao colar listas. É necessário ter a propriedade `allow` (tipo Booliano) para definir se a colagem de listas é permitida. Se `allow` estiver definido como `false`, especifique a propriedade `ignoreMode` (tipo `String`) para definir como lidar com qualquer conteúdo de lista colado. Os valores válidos para ignoreMode são `remove` que remove o conteúdo da lista e `paragraph` transforma os itens da lista em parágrafos. |

Um exemplo de uma `htmlPasteRules` estrutura válida está abaixo:

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. Salve todas as alterações.

## Configurar estilos de texto {#textstyles}

Os autores podem aplicar estilos para alterar a aparência de uma parte do texto. Os estilos são baseados em classes CSS pré-definidas na folha de estilos CSS. O conteúdo estilizado é delimitado por `span` tags que usam o `class` atributo para fazer referência à classe CSS. Por exemplo:

`<span class=monospaced>Monospaced Text Here</span>`

Quando o plug-in Estilos é ativado pela primeira vez, nenhum Estilo padrão está disponível. A lista pop-up está vazia. Para fornecer estilos aos autores, faça o seguinte:

* Ative o seletor suspenso Estilo.
* Especifique um ou mais locais das folhas de estilos.
* Especifique os estilos individuais que podem ser selecionados na lista pop-up de estilo.

Para reconfigurações posteriores, digamos para adicionar mais estilos, siga apenas as instruções para fazer referência a uma nova folha de estilos e especificar os estilos adicionais.

>[!NOTE]
>
>Os estilos também podem ser definidos para [tabelas ou células](configure-rich-text-editor-plug-ins.md#tablestyles)de tabela. Essas configurações exigem procedimentos separados.

### Ativar a lista do seletor suspenso Estilo {#styleselectorlist}

Isso é feito ao ativar o plug-in de estilos.

1. Em seu componente, navegue até o nó `<rtePlugins-node>/styles`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie a `features` propriedade no `styles` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

1. Salve todas as alterações.

>[!NOTE]
>
>Quando o plug-in Estilos estiver ativado, a lista suspensa Estilo será exibida na caixa de diálogo de edição. No entanto, a lista está vazia, pois nenhum Estilo está configurado.

### Especificar o local da folha de estilos {#locationofstylesheet}

Em seguida, especifique os locais das folhas de estilos que deseja referenciar:

1. Navegue até o nó raiz do componente de texto, por exemplo `/apps/<myProject>/components/text`.
1. Adicione a propriedade `externalStyleSheets` ao nó pai de `<rtePlugins-node>`:

   * **Nome** `externalStyleSheets`
   * **Tipo** `String[]` (multistring; clique em **Vários** no CRXDE)
   * **Valor(es)** O caminho e o nome de arquivo de cada folha de estilos que você deseja incluir. Use caminhos do repositório.

   >[!NOTE]
   >
   >É possível adicionar referências a folhas de estilos adicionais a qualquer momento.

1. Salve todas as alterações.

Ao usar o RTE em uma caixa de diálogo (Interface clássica), você pode especificar folhas de estilos que são otimizadas para edição de rich text. Devido a restrições técnicas, o contexto CSS é perdido no editor, portanto, você pode emular esse contexto para melhorar a experiência WYSIWYG.

O Editor de Rich Text usa um elemento DOM de container com uma ID `CQrte` que fornece estilos diferentes para visualização e edição:

```css
#CQ td {
// defines the style for viewing
 }
```

```css
#CQrte td {
 // defines the style for editing
 }
```

### Especificar os Estilos disponíveis na lista pop-up {#stylesindropdown}

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/styles`, conforme criado em [Ativando o seletor](#styleselectorlist)suspenso de estilo.
1. No nó `styles`, crie um nó (também chamado `styles`) para manter a lista disponível:

   * **Nome** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Crie um nó sob o `styles` nó para representar um estilo individual:

   * **Nome**, você pode especificar o nome, mas ele deve ser adequado para o estilo
   * **Tipo** `nt:unstructured`

1. Adicione a propriedade `cssName` a este nó para fazer referência à classe CSS:

   * **Nome** `cssName`
   * **Tipo** `String`
   * **Valor** O nome da classe CSS (sem um &#39;.&#39; anterior; for example, `cssClass` instead of `.cssClass`)

1. Adicione a propriedade `text` ao mesmo nó; isso define o texto mostrado na caixa de seleção:

   * **Nome** `text`
   * **Tipo** `String`
   * **Valor** Descrição do estilo; é exibida na caixa de seleção suspensa Estilo.

1. Salve as alterações.

   Repita as etapas acima para cada estilo necessário.

### Configurar o RTE para quebras de palavras ideais em japonês {#jpwordwrap}

Os autores que usam [!DNL Experience Manager] para criar conteúdo de idioma japonês podem aplicar um estilo a caracteres para evitar quebras de linha onde uma quebra não é necessária. Isso permite que os autores deixem as frases quebrarem na posição desejada. O estilo para essa funcionalidade é baseado na classe CSS predefinida na folha de estilos CSS.

Para criar o estilo que os autores podem aplicar ao texto em japonês, siga estas etapas:

1. Crie um nó sob o nó estilos. Consulte [especificar um estilo](#stylesindropdown).
   * Nome: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Adicione a propriedade `cssName` ao nó para referenciar a classe CSS. Este nome de classe é um nome reservado para o recurso de quebra automática de texto em japonês.
   * Nome: `cssName`
   * Tipo: `String`
   * Valor: `jpn-word-wrap` (sem precedentes `.`)

1. Adicione o texto da propriedade ao mesmo nó. O valor é o nome do estilo que os autores veem ao selecionar o estilo.
   * Nome: `text`
*Tipo: 
`String`
   * Valor: `Japanese word-wrap`

1. Crie uma folha de estilos e especifique seu caminho. Consulte [especificar o local da folha de estilos](#locationofstylesheet). Adicione o seguinte conteúdo à folha de estilos. Altere a cor do plano de fundo conforme desejado.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Folha de estilos para disponibilizar o recurso de quebra automática de texto em japonês para autores](assets/rte_jpwordwrap_stylesheet.jpg)

## Configurar os formatos de parágrafo {#paraformats}

Qualquer texto criado no RTE é colocado dentro de uma tag de bloco, sendo o padrão `<p>`. Ao ativar o `paraformat` plug-in, você especifica tags de bloco adicionais que podem ser atribuídas a parágrafos, usando uma lista de seleção suspensa. Os formatos de parágrafo determinam o tipo de parágrafo atribuindo a tag de bloco correta. O autor pode selecioná-los e atribuí-los usando o seletor de Formato. As tags de bloco de exemplo incluem, entre outras, o parágrafo padrão &lt;p> e os cabeçalhos &lt;h1>, &lt;h2> e assim por diante.

>[!CAUTION]
>
>Esse plug-in não é adequado para conteúdo com estrutura complexa, como listas ou tabelas.

>[!NOTE]
>
>Se uma tag block, por exemplo, uma `<hr>` tag, não puder ser atribuída a um parágrafo, não será um caso de uso válido para um `paraformat` plug-in.

Quando o plug-in Formatos de parágrafo estiver ativado pela primeira vez, nenhum Formato de parágrafo padrão estará disponível. A lista pop-up está vazia. Para fornecer aos autores formatos de parágrafo, faça o seguinte:

* Ative a lista do seletor pop-up [!UICONTROL Formatar] .
* Especifique as tags de bloco que podem ser selecionadas como formatos de parágrafo no menu pop-up.

Para reconfigurações posteriores, digamos para adicionar mais formatos, siga somente a parte relevante das instruções.

### Ativar o seletor suspenso Formato {#formatselectorlist}

Para ativar o `paraformat` plug-in, siga estas etapas:

1. Em seu componente, navegue até o nó `<rtePlugins-node>/paraformat`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie a `features` propriedade no `paraformat` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

>[!NOTE]
>
>Se o plug-in não estiver configurado mais, os formatos padrão que estão ativados são Parágrafo ( `<p>`), Cabeçalho 1 ( `<h1>`), Cabeçalho 2 ( `<h2>`), Cabeçalho 3 ( `<h3>`).

>[!CAUTION]
>
>Ao configurar os formatos de parágrafo do RTE, não remova a tag de parágrafo &lt;p> como uma opção de formatação. Se a `<p>` tag for removida, o autor do conteúdo não poderá selecionar a opção Formatos [!UICONTROL de] parágrafo mesmo se houver outros formatos configurados.

### Especificar os formatos de parágrafo disponíveis {#paraformatsindropdown}

Os formatos de parágrafo são disponibilizados para seleção por:

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/paraformat`, conforme criado em [Ativando o seletor](#styleselectorlist)suspenso de formato.
1. No `paraformat` nó, crie um nó para manter a lista de formatos:

   * **Nome** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Crie um nó sob o `formats` nó, isso contém detalhes para um formato individual:

   * **Nome**, você pode especificar o nome, mas ele deve ser adequado para o formato (por exemplo, myparágrafo, myheader1).
   * **Tipo** `nt:unstructured`

1. Para esse nó, adicione a propriedade para definir a tag de bloco usada:

   * **Nome** `tag`
   * **Tipo** `String`
   * **Valor** A tag de bloco para o formato; por exemplo: p, h1, h2, etc.

      Não é necessário digitar as chaves delimitadoras.

1. Para que o mesmo nó adicione outra propriedade, para que o texto descritivo apareça na lista suspensa:

   * **Nome** `description`
   * **Tipo** `String`
   * **Valor** O texto descritivo para este formato; por exemplo, Parágrafo, Cabeçalho 1, Cabeçalho 2 e assim por diante. Esse texto é exibido na lista de seleção de Formato.

1. Salve as alterações.

   Repita as etapas para cada formato necessário.

>[!CAUTION]
Se você definir formatos personalizados, os formatos padrão (`<p>`, `<h1>`, `<h2>`e `<h3>`) serão removidos. Recrie o `<p>` formato, pois ele é o formato padrão.

## Configurar caracteres especiais {#spchar}

Em uma [!DNL Experience Manager] instalação padrão, quando o `misctools` plug-in está ativado para caracteres especiais (`specialchars`) uma seleção padrão está imediatamente disponível para uso; por exemplo, os símbolos de direitos autorais e marcas registradas.

Você pode configurar o RTE para disponibilizar sua seleção de caracteres; definindo caracteres distintos ou uma sequência inteira.

>[!CAUTION]
A adição de caracteres especiais substitui a seleção padrão. Se necessário, redefina esses caracteres na sua seleção.

### Definir um único caractere {#definesinglechar}

1. Em seu componente, navegue até o nó `<rtePlugins-node>/misctools`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie a `features` propriedade no `misctools` nó:

   * **Nome** `features`
   * **Tipo** `String[]`
   * **Valor** `specialchars`

          (ou `String / *` se estiver aplicando todos os recursos para este plug-in)

1. Em `misctools` criar um nó para manter as configurações de caracteres especiais:

   * **Nome** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. Em `specialCharsConfig` criar outro nó para manter a lista de caracteres:

   * **Nome** `chars`
   * **Tipo** `nt:unstructured`

1. Em `chars` Adicionar um nó para manter uma definição de caractere individual:

   * **Nome** que você pode especificar, mas que deve refletir o caractere; por exemplo, metade.
   * **Tipo** `nt:unstructured`

1. Para esse nó, adicione a seguinte propriedade:

   * **Nome** `entity`
   * **Tipo** `String`
   * **Valor** da representação HTML do caractere desejado; por exemplo, `&189;` para a fração metade.

1. Salve as alterações.

No CRXDE, depois que a propriedade é salva, o caractere representado é exibido. Veja abaixo o exemplo da metade. Repita as etapas acima para disponibilizar caracteres mais especiais para os autores.

![No CRXDE, adicione um único caractere a ser disponibilizado na](assets/chlimage_1-106.png "barra de ferramentas do RTEno CRXDE, adicione um único caractere a ser disponibilizado na barra de ferramentas do RTE")

### Definir um intervalo de caracteres {#definerangechar}

1. Use as etapas de 1 a 3 de [Definir um único caractere](#definesinglechar).
1. Em `chars` Adicionar um nó para manter a definição do intervalo de caracteres:

   * **Nome** que você pode especificar, mas deve refletir o intervalo de caracteres; por exemplo, lápis.
   * **Tipo** `nt:unstructured`

1. Neste nó (nomeado de acordo com seu intervalo de caracteres especial), adicione as duas propriedades a seguir:

   * **Nome** `rangeStart`

      **Tipo** `Long`
      **Valor** da representação [Unicode](https://unicode.org/) (decimal) do primeiro caractere no intervalo

   * **Nome** `rangeEnd`

      **Tipo** `Long`
      **Valor** da representação [Unicode](https://unicode.org/) (decimal) do último caractere no intervalo

1. Salve as alterações.

   Por exemplo, definir um intervalo de 9998 - 10000 fornece os seguintes caracteres.

   ![No CRXDE, defina um intervalo de caracteres a ser disponibilizado no RTE](assets/chlimage_1-107.png)

   *Figura: No CRXDE, defina um intervalo de caracteres a ser disponibilizado no RTE*

   ![Caracteres especiais disponíveis no RTE são exibidos aos autores em uma](assets/rtepencil.png "janela pop-upCaracteres especiais disponíveis no RTE são exibidos aos autores em uma janela pop-up")

## Configurar estilos de tabela {#tablestyles}

Os estilos são normalmente aplicados no texto, mas um conjunto separado de Estilos também pode ser aplicado em uma tabela ou em algumas células da tabela. Esses Estilos estão disponíveis para os autores na caixa do seletor Estilo na caixa de diálogo Propriedades da célula ou Propriedades da tabela. Os estilos estão disponíveis ao editar uma tabela em um componente de Texto (ou derivado) e não no componente de Tabela padrão.

>[!NOTE]
Você pode definir estilos para tabelas e células somente para a interface clássica.

>[!NOTE]
A cópia e colagem de tabelas no componente RTE ou a partir dele depende do navegador. Não há suporte imediato para todos os navegadores. Você pode obter resultados variados dependendo da estrutura da tabela e do navegador. Por exemplo, ao copiar e colar uma tabela em um componente RTE no Mozilla Firefox na interface clássica e na interface de usuário de toque, o layout da tabela não é preservado.

1. No componente, navegue até o nó `<rtePlugins-node>/table`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie a `features` propriedade no `table` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*`

   >[!NOTE]
   Se você não quiser ativar todos os recursos da tabela, poderá criar a `features` propriedade como:
   * **Tipo** `String[]`

   * **Valor**(s) um ou ambos, do seguinte, conforme necessário:
      * `table` permitir a edição de propriedades de tabelas; incluindo os estilos.
      * `cellprops` para permitir a edição de propriedades de células, incluindo os estilos.


1. Defina o local das folhas de estilos CSS para referenciá-las. Consulte [Especificação do local da folha](#locationofstylesheet) de estilos, pois é o mesmo que ao definir [estilos para o texto](#textstyles). O local pode ser definido se você tiver definido outros estilos.
1. No `table` nó, crie os seguintes nós, conforme necessário:

   * Para definir estilos para a tabela inteira (disponível nas propriedades **[!UICONTROL da]** tabela):

      * **Nome** `tableStyles`
      * **Tipo** `cq:WidgetCollection`
   * Para definir estilos para células individuais (disponíveis nas propriedades **[!UICONTROL da]** Célula),

      * **Nome** `cellStyles`
      * **Tipo** `cq:WidgetCollection`


1. Crie um nó (sob o `tableStyles` ou `cellStyles` nó, conforme o caso) para representar um estilo individual,

   * **Nome** que você pode especificar, mas deve refletir o estilo.
   * **Tipo** `nt:unstructured`

1. Neste nó, crie as propriedades:

   * Para definir o estilo CSS referenciado,

      * **Nome** `cssName`
      * **Tipo** `String`
      * **Valor** do nome da classe CSS (sem um nome anterior `.`, por exemplo, `cssClass` em vez de `.cssClass`)
   * Para definir um texto descritivo a ser exibido no seletor pop-up,

      * **Nome** `text`
      * **Tipo** `String`
      * **Valor** do texto a ser exibido na lista de seleção


1. Salve todas as alterações.

Repita as etapas acima para cada estilo necessário.

### Configurar cabeçalhos ocultos em tabelas para acessibilidade {#hiddenheader}

Às vezes, você pode criar tabelas de dados sem texto visual em um cabeçalho de coluna, assumindo que a finalidade do cabeçalho é implícita pela relação visual da coluna com outras colunas. Nesse caso, é necessário fornecer texto interno oculto dentro da célula do cabeçalho para permitir que leitores de tela e outras tecnologias de assistência ajudem os leitores com várias necessidades a compreender a finalidade da coluna.

Para melhorar a acessibilidade em tais cenários, o RTE suporta células de cabeçalho ocultas. Além disso, fornece configurações relacionadas a cabeçalhos ocultos em tabelas. Essas configurações permitem aplicar estilos CSS em cabeçalhos ocultos nos modos de edição e pré-visualização. Para ajudar os autores a identificar cabeçalhos ocultos no modo de edição, inclua os seguintes parâmetros no código:

* `hiddenHeaderEditingCSS`: Especifica o nome da classe CSS aplicada na célula de cabeçalho oculto, quando o RTE é editado.
* `hiddenHeaderEditingStyle`: Especifica uma string de estilo que é aplicada na célula de cabeçalho oculto quando o RTE é editado.

Se você especificar o CSS e a string de estilo no código, a classe CSS terá precedência sobre a string de estilo e poderá substituir quaisquer alterações de configuração feitas pela string de estilo.

Para ajudar os autores a aplicar CSS em cabeçalhos ocultos no modo de pré-visualização, você pode incluir os seguintes parâmetros no código:

* `hiddenHeaderClassName`: Especifica o nome da classe CSS aplicada na célula de cabeçalho oculta no modo de pré-visualização.
* `hiddenHeaderStyle`: Especifica uma string de estilo que é aplicada na célula de cabeçalho oculto no modo de pré-visualização.

Se você especificar o CSS e a string de estilo no código, a classe CSS terá precedência sobre a string de estilo e poderá substituir quaisquer alterações de configuração feitas pela string de estilo.

## Adicionar dicionários para o verificador ortográfico {#adddict}

Quando o plug-in de verificação ortográfica é ativado, o RTE usa dicionários para cada idioma apropriado. Estes são então selecionados de acordo com o idioma do site, tirando a propriedade de idioma da subárvore ou extraindo o idioma do URL; por exemplo. a `/en/` sucursal é verificada em inglês, a `/de/` sucursal em alemão.

>[!NOTE]
A mensagem &quot;Falha na verificação ortográfica&quot;. é exibido se uma verificação for feita para um idioma que não está instalado.

Uma instalação padrão de Experience Manager inclui os dicionários para:

* Inglês Americano (pt_br)
* Inglês britânico (en_gb)

>[!NOTE]
Os dicionários padrão estão localizados em `/libs/cq/spellchecker/dictionaries`, juntamente com os arquivos ReadMe apropriados. Não modifique os arquivos.

Para adicionar mais dicionários, se necessário, siga estas etapas.

1. Navegue até a página [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. Selecione o idioma necessário e baixe o arquivo ZIP com as definições de ortografia. Extraia o conteúdo do arquivo em seu sistema de arquivos.

   >[!CAUTION]
   Somente os dicionários no `MySpell` formato para OpenOffice.org v2.0.1 ou anterior são suportados. Como os dicionários agora são arquivos de arquivamento, recomenda-se verificar o arquivo após o download.

1. Localize os arquivos .aff e .dic. Mantenha o nome do arquivo em minúsculas. Por exemplo, `de_de.aff` e `de_de.dic`.
1. Carregue os arquivos .aff e .dic no repositório em `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
O verificador ortográfico do RTE está disponível sob demanda. Ele não é executado automaticamente à medida que você start digitar um texto.
Para executar o verificador ortográfico, toque/clique no botão Verificador ortográfico da barra de ferramentas. O RTE verifica a ortografia de palavras e realça palavras com ortografia incorreta.
Se você incorporar qualquer alteração sugerida pelo verificador ortográfico, o estado do texto muda e as palavras com ortografia incorreta não são mais destacadas. Para executar o verificador ortográfico, toque/clique novamente no botão Verificador ortográfico.

## Configurar o tamanho do histórico para ações de desfazer e refazer {#undohistory}

O RTE permite que os autores desfaçam ou refaçam algumas últimas edições. Por padrão, 50 edições são armazenadas no histórico. Você pode configurar esse valor conforme necessário.

1. No componente, navegue até o nó `<rtePlugins-node>/undo`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `undo` nó, crie a propriedade:

   * **Nome** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valor** do número de etapas de desfazer que você deseja salvar no histórico. O padrão é 50. Use `0` para desativar completamente o comando desfazer/refazer.

1. Salve as alterações.

## Configurar o tamanho da guia {#tabsize}

Quando o caractere de tabulação é pressionado dentro de qualquer texto, é inserido um número predefinido de espaços; por padrão, são três espaços sem quebra e um espaço.

Para definir o tamanho da guia:

1. Em seu componente, navegue até o nó `<rtePlugins-node>/keys`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `keys` nó, crie a propriedade:

   * **Nome** `tabSize`
   * **Tipo** `String`
   * **Valor** do número de caracteres de espaço a serem usados para o tabulador.

1. Salve as alterações.

## Definir margem de recuo {#indentmargin}

Quando o recuo está ativado (padrão), é possível definir o tamanho do recuo:

>[!NOTE]
O tamanho do travessão só é aplicado aos parágrafos (blocos) do texto; não afeta o recuo das listas reais.

1. No componente, navegue até o nó `<rtePlugins-node>/lists`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `lists` nó, crie o `identSize` parâmetro:

   * **Nome**: `identSize`
   * **Tipo**: `Long`
   * **Valor**: número de pixels necessários para a margem de recuo.

## Configurar a altura do espaço editável {#editablespace}

É possível definir a altura do espaço editável mostrado na caixa de diálogo do componente. A configuração só é aplicável ao usar o RTE em uma caixa de diálogo. A configuração não altera a altura da janela de diálogo.

1. No `../items/text` nó, na definição da caixa de diálogo do componente, crie uma propriedade:

   * **Nome** `height`
   * **Tipo** `Long`
   * **Valor** da altura da tela de edição em pixels.

1. Salve as alterações.

## Configurar estilos e protocolos para links {#linkstyles}

Ao adicionar links em [!DNL Experience Manager], você pode definir os estilos CSS a serem usados e os protocolos a serem aceitos automaticamente. Para configurar como os links são adicionados a [!DNL Experience Manager] partir de outro programa, defina as regras HTML.

1. Usando o CRXDE Lite, localize o componente de texto para seu projeto.
1. Crie um nó no mesmo nível `<rtePlugins-node>`, ou seja, crie o nó sob o nó pai de `<rtePlugins-node>`:

   * **Nome** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   O `../items/text` nó tem a propriedade:
   * **Nome** `xtype`
   * **Tipo** `String`
   * **Valor** `richtext`

   O local do `../items/text` nó pode variar, dependendo da estrutura da caixa de diálogo. Dois exemplos são `/apps/myProject>/components/text/dialog/items/text` e `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Em `htmlRules`, crie um nó.

   * **Nome** `links`
   * **Tipo** `nt:unstructured`

1. No `links` nó, defina as propriedades conforme necessário:

   * Estilo CSS para links internos:

      * **Nome** `cssInternal`
      * **Tipo** `String`
      * **Valor** do nome da classe CSS (sem um &#39;.&#39; anterior; for example, `cssClass` instead of `.cssClass`)
   * Estilo CSS para links externos

      * **Nome** `cssExternal`
      * **Tipo** `String`
      * **Valor** do nome da classe CSS (sem um &#39;.&#39; anterior; for example, `cssClass` instead of `.cssClass`)
   * Matriz de **[!UICONTROL protocolos]** válidos, incluindo `https://`, `https://`, `file://``mailto:`e outros,

      * **Nome** `protocols`
      * **Tipo** `String[]`
      * **Valor**(s) um ou mais protocolos
   * **defaultProtocol** (propriedade do tipo **String**): Protocolo a ser usado se o usuário não especificou um explicitamente.

      * **Nome** `defaultProtocol`
      * **Tipo** `String`
      * **Valores** de um ou mais protocolos padrão
   * Definição de como tratar o atributo de público alvo de um link. Criar um nó:

      * **Nome** `targetConfig`
      * **Tipo** `nt:unstructured`

      No nó `targetConfig`: defina as propriedades necessárias:

      * Especifique o modo de público alvo:

         * **Nome** `mode`
         * **Tipo** `String`)
         * **Valor**(es) :

            * `auto`: significa que é escolhido um público alvo automático

               (especificado pela `targetExternal` propriedade para links externos ou `targetInternal` para links internos).

            * `manual`: não aplicável neste contexto
            * `blank`: não aplicável neste contexto
      * O público alvo para links internos:

         * **Nome** `targetInternal`
         * **Tipo** `String`
         * **Valor** do público alvo para links internos (use apenas quando &quot;mode is `auto`)
      * O público alvo para links externos:

         * **Nome** `targetExternal`
         * **Tipo** `String`
         * **Valor** do público alvo para links externos (usado apenas quando o modo está `auto`).








1. Salve todas as alterações.
