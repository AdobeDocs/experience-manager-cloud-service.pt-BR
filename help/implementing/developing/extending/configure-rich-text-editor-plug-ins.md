---
title: Configurar os plug-ins do Editor de Rich Text no [!DNL Adobe Experience Manager].
description: Saiba como configurar o [!DNL Adobe Experience Manager] Plug-ins do Editor de Rich Text.
contentOwner: AG
mini-toc-levels: 1
exl-id: 91619662-e865-47d1-8bec-0739f402353a
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '4303'
ht-degree: 2%

---

# Configurar os plug-ins do Editor de Rich Text {#configure-the-rich-text-editor-plug-ins}

As funcionalidades do RTE são disponibilizadas por meio de uma série de plug-ins, cada um com a propriedade de recursos. É possível configurar a propriedade de recursos para ativar ou desativar um ou mais recursos de RTE. Este artigo descreve como configurar especificamente os plug-ins do RTE.

Para obter detalhes sobre as outras configurações do RTE, consulte [configurar Rich Text Editor](/help/implementing/developing/extending/rich-text-editor.md).

>[!NOTE]
>
>Ao trabalhar com o CRXDE Lite, é recomendável salvar as alterações regularmente usando [!UICONTROL Salvar tudo] opção.

## Ativar um plug-in e configurar a propriedade de recursos {#activateplugin}

Para ativar um plug-in, siga estas etapas. Algumas etapas são necessárias somente quando você configura um plug-in pela primeira vez, pois os nós correspondentes não existem.

Por padrão, `format`, `link`, `list`, `justify`, e `control` plug-ins e todos os seus recursos estão ativados no RTE.

>[!NOTE]
>
>Os respectivos `rtePlugins` o nó é chamado de `<rtePlugins-node>` para evitar a duplicação neste artigo.

1. Usando o CRXDE Lite, localize o componente de texto para o seu projeto.
1. Criar o nó principal de `<rtePlugins-node>` se não existir, antes de configurar plug-ins do RTE:

   * Dependendo do componente, os nós principais são:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * um nó de configuração alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`

   * São do tipo: **jcr:primaryType** `cq:Widget`
   * Ambos têm a seguinte propriedade:

      * **Nome** `name`
      * **Tipo** `String`
      * **Valor** `./text`

1. Dependendo da interface que você está configurando para o, crie um nó `<rtePlugins-node>`, se não existir:

   * **Nome** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Abaixo disso, crie um nó para cada plug-in que você deseja ativar:

   * **Tipo** `nt:unstructured`
   * **Nome** a ID do plug-in do plug-in necessária

Depois de ativar um plug-in, siga estas diretrizes para configurar o `features` propriedade.

| | Habilitar todos os recursos | Habilite alguns recursos específicos. | Desative todos os recursos. |
|---|---|---|---|
| Nome | recursos | recursos | recursos |
| Tipo | String | `String` (várias sequências de caracteres; defina Tipo como `String` e clique em `Multi` in CRXDE Lite) | String |
| Valor | `*` (um asterisco) | Defina para um ou mais valores de recurso. | - |

## Entender o plug-in findreplace {#findreplace}

A variável `findreplace` não precisa de nenhuma configuração. Funciona imediatamente.

Ao usar a funcionalidade de substituição, a cadeia de caracteres de substituição a ser substituída deve ser inserida ao mesmo tempo que a cadeia de caracteres de localização. No entanto, você ainda pode clicar em localizar para procurar a cadeia de caracteres antes de substituí-la. Se a cadeia de caracteres de substituição for inserida após clicar em localizar, a pesquisa será redefinida para o início do texto.

A caixa de diálogo localizar e substituir se torna transparente quando a localização é clicada, e se torna opaca ao clicar em substituir. O comportamento permite que o autor revise o texto a ser substituído. Se os usuários clicarem em substituir tudo, a caixa de diálogo será fechada e exibirá o número de substituições feitas.

## Configurar os modos de colagem {#pastemodes}

Ao usar o RTE, os autores podem colar o conteúdo em um dos três modos a seguir:

* **Modo do navegador**: cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode apresentar marcação indesejada.

* **Modo de texto sem formatação**: cole o conteúdo da área de transferência como texto simples. Ele remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir no [!DNL Experience Manager] componente.

* **Modo MS Word**: Cole o texto, incluindo tabelas, com formatação ao copiar do MS Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou o MS Excel, e ela retém apenas formatação parcial.

### Configurar opções de Colagem disponíveis na barra de ferramentas do RTE  {#configure-paste-options-available-on-the-rte-toolbar}

Você pode fornecer alguns, todos ou nenhum desses três ícones aos autores na barra de ferramentas do RTE:

* **[!UICONTROL Colar (Ctrl+V)]**: pode ser pré-configurado para corresponder a um dos três modos de Colagem descritos acima.

* **[!UICONTROL Colar como texto]**: oferece a funcionalidade de modo de texto simples.

* **[!UICONTROL Colar do Word]**: fornece a funcionalidade do modo MS Word.

Para configurar o RTE para exibir os ícones necessários, siga estas etapas.

1. Navegue até o componente, por exemplo, `/apps/<myProject>/components/text`.
1. Navegue até o nó `rtePlugins/edit`. Consulte [ativar um plug-in](#activateplugin) se o nó não existir.
1. Crie o `features` propriedade no `edit` e adicione um ou mais recursos. Salve todas as alterações.

### Configurar o comportamento do ícone e do atalho Colar (Ctrl+V) {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Você pode pré-configurar o comportamento do **[!UICONTROL Colar (Ctrl+V)]** ícone, usando as etapas a seguir. Essa configuração também define o comportamento do atalho de teclado Ctrl+V que os autores usam para colar conteúdo.

A configuração permite os três tipos de casos de uso a seguir:

* Cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode apresentar marcação indesejada. Configurado usando `browser` abaixo.

* Cole o conteúdo da área de transferência como texto simples. Ele remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir no [!DNL Experience Manager] componente. Configurado usando `plaintext` abaixo.

* Cole o texto, incluindo tabelas, com formatação ao copiar do MS Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou o MS Excel, e ela retém apenas formatação parcial. Configurado usando `wordhtml` abaixo.

1. Em seu componente, navegue até `<rtePlugins-node>/edit` nó. Crie os nós se eles não existirem. Para obter mais informações, consulte [ativar um plug-in](#activateplugin).
1. No `edit` nó criar uma propriedade usando os seguintes detalhes:

   * **Nome** `defaultPasteMode`
   * **Tipo** `String`
   * **Valor** é um dos modos de colagem necessários do `browser`, `plaintext`ou `wordhtml` modos.

### Configurar os formatos permitidos ao colar o conteúdo {#pasteformats}

O comando colar-como-Microsoft-Word`paste-wordhtml`) pode ser configurado ainda mais para que você possa permitir explicitamente alguns estilos ao colar [!DNL Experience Manager] de outro programa, como [!DNL Microsoft Word].

Por exemplo, se apenas os formatos e as listas em negrito forem permitidos ao colar em [!DNL Experience Manager], você pode filtrar os outros formatos. Isso é chamado de filtragem de colagem configurável, que pode ser feito para:

* [Texto](#pastemodes)
* [Links](#linkstyles)

Para links, você também pode definir os protocolos que são aceitos automaticamente.

Para configurar quais formatos são permitidos ao colar texto em [!DNL Experience Manager] de outro programa:

1. No componente, navegue até o nó `<rtePlugins-node>/edit`. Crie os nós se o nó não existir. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie um nó sob o `edit` nó para manter as regras de colagem de HTML:

   * **Nome** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Criar um nó em `htmlPasteRules`, para manter os detalhes dos formatos básicos permitidos:

   * **Nome** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Para controlar os formatos individuais aceitos, crie uma ou mais das seguintes propriedades no `allowBasics` nó:

   * **Nome** `bold`
   * **Nome** `italic`
   * **Nome** `underline`
   * **Nome** `anchor` (para links e âncoras nomeadas)
   * **Nome** `image`

   Todas as propriedades são de **Tipo** `Boolean`, de modo que, no caso **Valor** você pode marcar ou remover a marca de seleção para ativar ou desativar a funcionalidade.

   >[!NOTE]
   >
   >Se não estiver definido explicitamente, o valor padrão true é usado e o formato é aceito.

1. Outros formatos também podem ser definidos usando uma variedade de outras propriedades ou nós, também aplicados à `htmlPasteRules` nó:

| Propriedade | Tipo | Descrição |
|--- |--- |--- |
| `allowBlockTags` | `String` | Define a lista de tags de bloqueio permitidas. Algumas tags de bloco possíveis incluem títulos (h1, h2, h3), parágrafos (p), listas (ol, ul), tabelas (tabela). |
| `fallbackBlockTag` | `String` | Define a tag de bloco usada para qualquer bloco com uma tag de bloco não incluída em `allowBlockTags`. Normalmente, `p` suficiente. |
| `table` | `nt:unstructured` | Define o comportamento ao colar tabelas. Esse nó deve ter a propriedade allow (type Boolean) para definir se a colagem de tabelas é permitida. Se allow for definido como false, você deverá especificar a propriedade ignoreMode (tipo String) para definir como o conteúdo da tabela colada é tratado. Os valores válidos para ignoreMode são `remove` para remover o conteúdo da tabela e `paragraph` para transformar células de tabela em parágrafos. |
| `list` | `nt:unstructured` | Define o comportamento ao colar listas. É necessário ter a propriedade `allow` (tipo Booleano) para definir se a colagem de listas é permitida. Se `allow` está definida como `false`, especifique a propriedade `ignoreMode` (tipo `String`) para definir como lidar com qualquer conteúdo de lista colado. Os valores válidos para ignoreMode são `remove` que remove o conteúdo da lista e `paragraph` que transforma itens de lista em parágrafos. |

Um exemplo de um válido `htmlPasteRules` está abaixo:

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

Os autores podem aplicar Estilos para alterar a aparência de uma parte do texto. Os estilos são baseados em classes CSS que você predefine na sua folha de estilos CSS. O conteúdo estilizado é delimitado por `span` tags usando o `class` para fazer referência à classe CSS. Por exemplo:

`<span class=monospaced>Monospaced Text Here</span>`

Quando o plug-in Estilos é ativado pela primeira vez, nenhum estilo padrão está disponível. A lista pop-up está vazia. Para fornecer estilos aos autores, faça o seguinte:

* Ative o seletor suspenso Estilo.
* Especifique um ou mais locais das folhas de estilos.
* Especifique os estilos individuais que podem ser selecionados na lista pop-up de estilos.

Para reconfigurações posteriores, digamos adicionar mais estilos, siga apenas as instruções para fazer referência a uma nova folha de estilos e especificar os estilos adicionais.

>[!NOTE]
>
>Os estilos também podem ser definidos para [tabelas ou células de tabela](configure-rich-text-editor-plug-ins.md#tablestyles). Essas configurações exigem procedimentos separados.

### Ativar a lista suspensa de seletores Estilo {#styleselectorlist}

Isso é feito ativando o plug-in de estilos.

1. No componente, navegue até o nó `<rtePlugins-node>/styles`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` propriedade no `styles` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

1. Salve todas as alterações.

>[!NOTE]
>
>Quando o plug-in Estilos estiver ativado, a lista suspensa Estilo será exibida na caixa de diálogo de edição. No entanto, a lista fica vazia, pois nenhum estilo é configurado.

### Especificar o local da folha de estilos {#locationofstylesheet}

Em seguida, especifique o(s) local(is) da(s) folha(s) de estilos que deseja referenciar:

1. Navegue até o nó raiz do componente de texto, por exemplo, `/apps/<myProject>/components/text`.
1. Adicionar a propriedade `externalStyleSheets` ao nó principal de `<rtePlugins-node>`:

   * **Nome** `externalStyleSheets`
   * **Tipo** `String[]` (várias cadeias de caracteres; clique em **Multi** no CRXDE)
   * **Valores** O caminho e o nome de arquivo de cada folha de estilos que você deseja incluir. Usar caminhos do repositório.

   >[!NOTE]
   >
   >É possível adicionar referências a folhas de estilos adicionais posteriormente.

1. Salve todas as alterações.

Ao usar o RTE em uma caixa de diálogo (interface clássica), é possível especificar folhas de estilos otimizadas para edição de rich text. Devido a restrições técnicas, o contexto CSS é perdido no editor, portanto, você pode emular esse contexto para melhorar a experiência WYSIWYG.

O Editor de Rich Text usa um elemento DOM do container com uma ID de `CQrte` que fornecem estilos diferentes para exibir e editar:

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

### Especificar os estilos disponíveis na lista pop-up {#stylesindropdown}

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/styles`, conforme criado em [Ativação do seletor suspenso de estilo](#styleselectorlist).
1. No nó `styles`, crie um nó (também chamado de `styles`) para manter a lista disponibilizada:

   * **Nome** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Crie um nó sob o `styles` nó para representar um estilo individual:

   * **Nome**, você pode especificar o nome, mas ele deve ser adequado para o estilo
   * **Tipo** `nt:unstructured`

1. Adicionar a propriedade `cssName` neste nó para fazer referência à classe CSS:

   * **Nome** `cssName`
   * **Tipo** `String`
   * **Valor** O nome da classe CSS (sem um &#39;.&#39; precedente; por exemplo, `cssClass` em vez de `.cssClass`)

1. Adicionar a propriedade `text` para o mesmo nó; isso define o texto mostrado na caixa de seleção:

   * **Nome** `text`
   * **Tipo** `String`
   * **Valor** Descrição do estilo; aparece na caixa de seleção suspensa Estilo.

1. Salve as alterações.

   Repita as etapas acima para cada estilo necessário.

### Configurar o RTE para quebras de palavras ideais em japonês {#jpwordwrap}

Autores que usam [!DNL Experience Manager] para criar conteúdo no idioma japonês, é possível aplicar um estilo aos caracteres para evitar uma quebra de linha, pois essa quebra não é necessária. Isso permite que os autores deixem as frases serem quebradas na posição desejada. O estilo dessa funcionalidade é baseado na classe CSS, que é predefinida na folha de estilos CSS.

Para criar o estilo que os autores podem aplicar ao texto em japonês, siga estas etapas:

1. Crie um nó sob o nó estilos. Consulte [especificar um estilo](#stylesindropdown).
   * Nome: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Adicionar a propriedade `cssName` ao nó para fazer referência à classe CSS. Este nome de classe é um nome reservado para o recurso de quebra de linha em japonês.
   * Nome: `cssName`
   * Tipo: `String`
   * Valor: `jpn-word-wrap` (sem um precedente `.`)

1. Adicione o texto da propriedade ao mesmo nó. O valor é o nome do estilo que os autores veem ao selecionar o estilo.
   * Nome: `text`
*Tipo: `String`
   * Valor: `Japanese word-wrap`

1. Crie uma folha de estilos e especifique seu caminho. Consulte [especificar local da folha de estilos](#locationofstylesheet). Adicione o conteúdo a seguir à folha de estilos. Altere a cor do plano de fundo conforme desejado.

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![Folha de estilos para disponibilizar aos autores o recurso de quebra automática de linha em japonês](assets/rte_jpwordwrap_stylesheet.jpg)

## Configurar os formatos de parágrafo {#paraformats}

Qualquer texto criado no RTE é colocado em uma tag de bloco, sendo o padrão `<p>`. Ao ativar o `paraformat` especifique tags de bloco adicionais que podem ser atribuídas a parágrafos, usando uma lista suspensa de seleção. Os formatos de parágrafo determinam o tipo de parágrafo atribuindo a marca de formatação de bloco correta. O autor pode selecioná-los e atribuí-los usando o seletor de Formato. Os exemplos de tags de bloco incluem, entre outros, o parágrafo padrão &lt;p> e cabeçalhos &lt;h1>, &lt;h2>e assim por diante.

>[!CAUTION]
>
>Esse plug-in não é adequado para conteúdo com estrutura complexa, como listas ou tabelas.

>[!NOTE]
>
>Se uma tag de bloco, por exemplo, uma tag `<hr>` tag, não podem ser atribuídos a um parágrafo, não é um caso de uso válido para um `paraformat` plug-in.

Quando o plug-in Formatos de parágrafo é ativado pela primeira vez, nenhum Formato de parágrafo padrão está disponível. A lista pop-up está vazia. Para fornecer formatos de parágrafo aos autores, faça o seguinte:

* Ativar o [!UICONTROL Formato] lista do seletor pop-up.
* Especifique as tags de bloco que podem ser selecionadas como formatos de parágrafo no menu pop-up.

Para reconfigurações posteriores, digamos para adicionar mais formatos, siga apenas a parte relevante das instruções.

### Ativar o seletor suspenso Formatar {#formatselectorlist}

Para ativar o `paraformat` siga estas etapas:

1. No componente, navegue até o nó `<rtePlugins-node>/paraformat`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` propriedade no `paraformat` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

>[!NOTE]
>
>Se o plug-in não for configurado ainda mais, os formatos padrão ativados serão Parágrafo ( `<p>`), Cabeçalho 1 ( `<h1>`), Cabeçalho 2 ( `<h2>`), Cabeçalho 3 ( `<h3>`).

>[!CAUTION]
>
>Ao configurar os formatos de parágrafo do RTE, não remova a tag de parágrafo &lt;p> como uma opção de formatação. Se a variável `<p>` for removida, o autor de conteúdo não poderá selecionar a tag [!UICONTROL Formatos de parágrafo] mesmo se houver formatos adicionais configurados.

### Especificar os formatos de parágrafo disponíveis {#paraformatsindropdown}

Os formatos de parágrafo são disponibilizados para seleção por:

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/paraformat`, conforme criado em [Ativação do seletor suspenso de formato](#styleselectorlist).
1. No `paraformat` nó criar um nó, para manter a lista de formatos:

   * **Nome** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Crie um nó sob o `formats` nó, isso mantém os detalhes de um formato individual:

   * **Nome**, você pode especificar o nome, mas ele deve ser adequado para o formato (por exemplo, myParagraph, myheader1).
   * **Tipo** `nt:unstructured`

1. Neste nó, adicione a propriedade para definir a tag de bloqueio usada:

   * **Nome** `tag`
   * **Tipo** `String`
   * **Valor** A tag de bloco para o formato; por exemplo: p, h1, h2 e assim por diante.

     Não é necessário inserir os colchetes angulares delimitadores.

1. Para o mesmo nó, adicione outra propriedade para que o texto descritivo apareça na lista suspensa:

   * **Nome** `description`
   * **Tipo** `String`
   * **Valor** O texto descritivo desse formato; por exemplo, Parágrafo, Cabeçalho 1, Cabeçalho 2 e assim por diante. Esse texto é exibido na lista de seleção de Formato.

1. Salve as alterações.

   Repita as etapas para cada formato necessário.

>[!CAUTION]
>
Se você definir formatos personalizados, os formatos padrão (`<p>`, `<h1>`, `<h2>`, e `<h3>`) são removidos. Recriar `<p>` formato, pois é o formato padrão.

## Configurar caracteres especiais {#spchar}

Em um padrão [!DNL Experience Manager] instalação, quando a variável `misctools` está ativado para caracteres especiais (`specialchars`) uma seleção padrão é imediatamente disponibilizada para uso; por exemplo, os símbolos de copyright e marca registrada.

É possível configurar o RTE para disponibilizar a seleção de caracteres; definindo caracteres distintos ou uma sequência inteira.

>[!CAUTION]
>
A adição de caracteres especiais substitui a seleção padrão. Se necessário, redefina esses caracteres na sua seleção.

### Definir um caractere único {#definesinglechar}

1. No componente, navegue até o nó `<rtePlugins-node>/misctools`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` propriedade no `misctools` nó:

   * **Nome** `features`
   * **Tipo** `String[]`
   * **Valor** `specialchars`

         (ou `String / *` se estiver aplicando todos os recursos deste plug-in)

1. Em `misctools` crie um nó para manter as configurações de caracteres especiais:

   * **Nome** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. Em `specialCharsConfig` crie outro nó para conter a lista de caracteres:

   * **Nome** `chars`
   * **Tipo** `nt:unstructured`

1. Em `chars` adicione um nó para manter uma definição de caractere individual:

   * **Nome** você pode especificar o nome, mas ele deve refletir o caractere; por exemplo, half.
   * **Tipo** `nt:unstructured`

1. Para adicionar a este nó a seguinte propriedade:

   * **Nome** `entity`
   * **Tipo** `String`
   * **Valor** a representação HTML do caractere necessário; por exemplo, `&189;` para a fração metade.

1. Salve as alterações.

No CRXDE, depois que a propriedade é salva, o caractere representado é exibido. Veja abaixo o exemplo de metade. Repita as etapas acima para disponibilizar mais caracteres especiais aos autores.

![No CRXDE, adicione um único caractere a ser disponibilizado na barra de ferramentas do RTE](assets/chlimage_1-106.png "No CRXDE, adicione um único caractere a ser disponibilizado na barra de ferramentas do RTE")

### Definir um intervalo de caracteres {#definerangechar}

1. Use as etapas 1 a 3 de [Definir um caractere único](#definesinglechar).
1. Em `chars` adicione um nó para manter a definição do intervalo de caracteres:

   * **Nome** você pode especificar o nome, mas ele deve refletir o intervalo de caracteres; por exemplo, lápis.
   * **Tipo** `nt:unstructured`

1. Nesse nó (nomeado de acordo com o intervalo de caracteres especiais), adicione as duas propriedades a seguir:

   * **Nome** `rangeStart`
     **Tipo** `Long`
     **Valor** o [Unicode](https://unicode.org/) representação (decimal) do primeiro caractere no intervalo

   * **Nome** `rangeEnd`
     **Tipo** `Long`
     **Valor** o [Unicode](https://unicode.org/) representação (decimal) do último caractere no intervalo

1. Salve as alterações.

   Por exemplo, definir um intervalo de 9998 - 10000 fornece os seguintes caracteres.

   ![No CRXDE, defina um intervalo de caracteres que serão disponibilizados no RTE](assets/chlimage_1-107.png)

   *Figura: no CRXDE, defina um intervalo de caracteres que serão disponibilizados no RTE*

   ![Caracteres especiais disponíveis no RTE são exibidos para os autores em uma janela pop-up](assets/rtepencil.png "Caracteres especiais disponíveis no RTE são exibidos para os autores em uma janela pop-up")

## Configurar estilos de tabela {#tablestyles}

Normalmente, os estilos são aplicados em texto, mas um conjunto separado de estilos também pode ser aplicado a uma tabela ou a algumas células da tabela. Esses Estilos estão disponíveis para os autores na caixa do seletor de estilo na caixa de diálogo Propriedades da célula ou Propriedades da tabela. Os estilos estão disponíveis ao editar uma tabela em um componente de Texto (ou derivativo) e não no componente de Tabela padrão.

>[!NOTE]
>
É possível definir estilos para tabelas e células somente para a interface clássica.

>[!NOTE]
>
Copiar e colar tabelas no componente de RTE ou a partir dele depende do navegador. Ele não é compatível imediatamente com todos os navegadores. É possível obter resultados variados dependendo da estrutura da tabela e do navegador. Por exemplo, ao copiar e colar uma tabela em um componente do RTE no Mozilla Firefox na interface clássica e na interface para toque, o layout da tabela não é preservado.

1. No componente, navegue até o nó `<rtePlugins-node>/table`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` propriedade no `table` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*`

   >[!NOTE]
   >
   Se você não quiser ativar todos os recursos da tabela, crie o `features` propriedade como:
   >
   * **Tipo** `String[]`
   >
   * **Valor** s) Uma ou ambas as condições, conforme exigido:
   * `table` para permitir a edição de propriedades de tabela, incluindo os estilos.
   * `cellprops` para permitir a edição de propriedades da célula, incluindo os estilos.

1. Defina o local das folhas de estilos CSS para referenciá-las. Consulte [Especificação da localização da sua folha de estilos](#locationofstylesheet) já que é o mesmo que ao definir [estilos de texto](#textstyles). O local pode ser definido se você tiver definido outros estilos.
1. No `table` crie os seguintes nós conforme necessário:

   * Para definir estilos para a tabela inteira (disponível em **[!UICONTROL Propriedades da tabela]**):

      * **Nome** `tableStyles`
      * **Tipo** `cq:WidgetCollection`

   * Para definir estilos para as células individuais (disponível em **[!UICONTROL Propriedades da célula]**),

      * **Nome** `cellStyles`
      * **Tipo** `cq:WidgetCollection`

1. Criar um nó (sob o `tableStyles` ou `cellStyles` conforme apropriado) para representar um estilo individual,

   * **Nome** você pode especificar o nome, mas ele deve refletir o estilo.
   * **Tipo** `nt:unstructured`

1. Neste nó, crie as propriedades:

   * Para definir o estilo CSS referenciado,

      * **Nome** `cssName`
      * **Tipo** `String`
      * **Valor** o nome da classe CSS (sem um precedente `.`, por exemplo, `cssClass` em vez de `.cssClass`)

   * Para definir um texto descritivo a ser exibido no seletor pop-up,

      * **Nome** `text`
      * **Tipo** `String`
      * **Valor** o texto a ser exibido na lista de seleção

1. Salve todas as alterações.

Repita as etapas acima para cada estilo necessário.

### Configurar cabeçalhos ocultos em tabelas para acessibilidade {#hiddenheader}

Às vezes, você pode criar tabelas de dados sem texto visual em um cabeçalho de coluna, supondo que a finalidade do cabeçalho esteja implícita no relacionamento visual da coluna com outras colunas. Nesse caso, é necessário fornecer texto interno oculto dentro da célula na célula de cabeçalho para permitir que os leitores de tela e outras tecnologias de assistência ajudem os leitores com várias necessidades a entender o propósito da coluna.

Para aprimorar a acessibilidade em tais cenários, o RTE oferece suporte a células de cabeçalho ocultas. Além disso, fornece definições de configuração relacionadas a cabeçalhos ocultos em tabelas. Essas configurações permitem aplicar estilos de CSS a cabeçalhos ocultos nos modos de edição e pré-visualização. Para ajudar os autores a identificar cabeçalhos ocultos no modo de edição, inclua os seguintes parâmetros no código:

* `hiddenHeaderEditingCSS`: especifica o nome da classe CSS aplicada na célula do cabeçalho oculto, quando o RTE é editado.
* `hiddenHeaderEditingStyle`: especifica uma cadeia de caracteres de estilo aplicada na célula do cabeçalho oculto quando o RTE é editado.

Se você especificar o CSS e a string de estilo no código, a classe CSS terá prioridade sobre a string de estilo e poderá substituir quaisquer alterações de configuração feitas pela string de estilo.

Para ajudar os autores a aplicarem o CSS em cabeçalhos ocultos no modo de visualização, você pode incluir os seguintes parâmetros no código:

* `hiddenHeaderClassName`: especifica o nome da classe CSS aplicada na célula do cabeçalho oculto no modo de visualização.
* `hiddenHeaderStyle`: Especifica uma cadeia de caracteres de Estilo que é aplicada na célula do cabeçalho oculto no modo de visualização.

Se você especificar o CSS e a string de estilo no código, a classe CSS terá prioridade sobre a string de estilo e poderá substituir quaisquer alterações de configuração feitas pela string de estilo.

## Adicionar dicionários para o verificador ortográfico {#adddict}

Quando o plug-in de verificação ortográfica é ativado, o RTE usa dicionários para cada idioma apropriado. Eles são selecionados de acordo com o idioma do site, pegando a propriedade language da subárvore ou extraindo o idioma do URL, por exemplo. o `/en/` for marcada como inglês, a variável `/de/` como alemão.

>[!NOTE]
>
A mensagem &quot;Falha na verificação ortográfica.&quot; é visto se for tentada uma verificação para um idioma que não está instalado.

Uma instalação de Experience Manager padrão inclui os dicionários para:

* Inglês Americano (en_us)
* Inglês Britânico (en_gb)

>[!NOTE]
>
Os dicionários padrão estão localizados em `/libs/cq/spellchecker/dictionaries`, juntamente com os arquivos ReadMe apropriados. Não modifique os arquivos.

Para adicionar mais dicionários, se necessário, siga estas etapas.

1. Navegue até a página [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. Selecione o idioma desejado e baixe o arquivo ZIP com as definições de ortografia. Extraia o conteúdo do arquivo morto em seu sistema de arquivos.

   >[!CAUTION]
   >
   Somente dicionários na `MySpell` formato para OpenOffice.org v2.0.1 ou anterior, são compatíveis. Como os dicionários agora são arquivos mortos, é recomendável verificar o arquivo após baixá-lo.

1. Localize os arquivos .aff e .dic. Mantenha o nome do arquivo em minúsculas. Por exemplo, `de_de.aff` e `de_de.dic`.
1. Carregue os arquivos .aff e .dic no repositório em `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
>
O verificador ortográfico RTE está disponível sob demanda. Ele não é executado automaticamente quando você começa a digitar o texto.
>
Para executar o verificador ortográfico, selecione o botão Verificador ortográfico na barra de ferramentas. O RTE verifica a ortografia das palavras e destaca palavras com erro de ortografia.
>
Se você incorporar qualquer alteração sugerida pelo verificador ortográfico, o estado do texto será alterado e as palavras com erro de ortografia não serão mais destacadas. Para executar o verificador ortográfico, selecione o botão Verificador ortográfico novamente.

## Configurar o tamanho do histórico das ações desfazer e refazer {#undohistory}

O RTE permite que os autores desfaçam ou refaçam algumas últimas edições. Por padrão, 50 edições são armazenadas no histórico. Você pode configurar esse valor conforme necessário.

1. No componente, navegue até o nó `<rtePlugins-node>/undo`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `undo` crie a propriedade:

   * **Nome** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valor** o número de etapas desfazer que você deseja salvar no histórico. O padrão é 50. Uso `0` para desativar completamente a opção desfazer/refazer.

1. Salve as alterações.

## Configurar o tamanho da guia {#tabsize}

Quando o caractere de tabulação é pressionado dentro de qualquer texto, um número predefinido de espaços é inserido; por padrão, são três espaços não-separáveis e um espaço.

Para definir o tamanho da guia:

1. No componente, navegue até o nó `<rtePlugins-node>/keys`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `keys` crie a propriedade:

   * **Nome** `tabSize`
   * **Tipo** `String`
   * **Valor** o número de caracteres de espaço a serem usados para o tabulador.

1. Salve as alterações.

## Definir margem de recuo {#indentmargin}

Quando o recuo está habilitado (padrão), você pode definir o tamanho do recuo:

>[!NOTE]
>
Este tamanho de recuo é aplicado somente a parágrafos (blocos) de texto; não afeta o recuo de listas reais.

1. No componente, navegue até o nó `<rtePlugins-node>/lists`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `lists` nó criar o `identSize` parâmetro:

   * **Nome**: `identSize`
   * **Tipo**: `Long`
   * **Valor**: número de pixels necessários para a margem de recuo.

## Configurar a altura do espaço editável {#editablespace}

Você pode definir a altura do espaço editável mostrado na caixa de diálogo do componente. A configuração só é aplicável ao usar o RTE em uma caixa de diálogo. A configuração não altera a altura da janela de diálogo.

1. No `../items/text` na definição de caixa de diálogo do componente, crie uma propriedade:

   * **Nome** `height`
   * **Tipo** `Long`
   * **Valor** a altura da tela de edição em pixels.

1. Salve as alterações.

## Configurar estilos e protocolos para links {#linkstyles}

Ao adicionar links em [!DNL Experience Manager], você pode definir os estilos CSS a serem usados e os protocolos a serem aceitos automaticamente. Para configurar como os links são adicionados em [!DNL Experience Manager] em outro programa, defina as regras de HTML.

1. Usando o CRXDE Lite, localize o componente de texto para o seu projeto.
1. Criar um nó no mesmo nível que `<rtePlugins-node>`, ou seja, crie o nó sob o nó principal de `<rtePlugins-node>`:

   * **Nome** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   >
   A variável `../items/text` O nó tem a propriedade:
   >
   * **Nome** `xtype`
   * **Tipo** `String`
   * **Valor** `richtext`
   >
   A localização do `../items/text` pode variar, dependendo da estrutura da caixa de diálogo. Dois exemplos são `/apps/myProject>/components/text/dialog/items/text` e `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Em `htmlRules`, crie um nó.

   * **Nome** `links`
   * **Tipo** `nt:unstructured`

1. No `links` defina as propriedades conforme necessário:

   * Estilo CSS para links internos:

      * **Nome** `cssInternal`
      * **Tipo** `String`
      * **Valor** o nome da classe CSS (sem um &#39;.&#39; precedente; por exemplo, `cssClass` em vez de `.cssClass`)

   * Estilo CSS para links externos

      * **Nome** `cssExternal`
      * **Tipo** `String`
      * **Valor** o nome da classe CSS (sem um &#39;.&#39; precedente; por exemplo, `cssClass` em vez de `.cssClass`)

   * Matriz de válida **[!UICONTROL protocolos]** incluindo `https://`, `https://`, `file://`, `mailto:`, e outros,

      * **Nome** `protocols`
      * **Tipo** `String[]`
      * **Valor** s) um ou mais protocolos

   * **defaultProtocol** (propriedade do tipo **String**): Protocolo a ser usado se o usuário não tiver especificado um explicitamente.

      * **Nome** `defaultProtocol`
      * **Tipo** `String`
      * **Valor**(s) um ou mais protocolos padrão

   * Definição de como lidar com o atributo de direcionamento de um link. Criar um nó:

      * **Nome** `targetConfig`
      * **Tipo** `nt:unstructured`

     No nó `targetConfig`: defina as propriedades necessárias:

      * Especifique o modo de destino:

         * **Nome** `mode`
         * **Tipo** `String`)
         * **Valor** s):

            * `auto`: significa que um target automático foi escolhido

              (especificado pelo `targetExternal` propriedade para links externos ou `targetInternal` para links internos).

            * `manual`: não aplicável neste contexto
            * `blank`: não aplicável neste contexto

      * O target para links internos:

         * **Nome** `targetInternal`
         * **Tipo** `String`
         * **Valor** o target para links internos (usar somente quando o modo for `auto`)

      * O target para links externos:

         * **Nome** `targetExternal`
         * **Tipo** `String`
         * **Valor** o target para links externos (usado somente quando o modo é `auto`).

1. Salve todas as alterações.
