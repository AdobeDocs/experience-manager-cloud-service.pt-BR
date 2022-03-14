---
title: Configure os plug-ins do Editor de Rich Text em [!DNL Adobe Experience Manager].
description: Saiba como configurar o [!DNL Adobe Experience Manager] Plug-ins do Editor de Rich Text.
contentOwner: AG
mini-toc-levels: 1
exl-id: 91619662-e865-47d1-8bec-0739f402353a
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '4301'
ht-degree: 4%

---

# Configurar os plug-ins do Editor de Rich Text {#configure-the-rich-text-editor-plug-ins}

As funcionalidades do RTE são disponibilizadas por meio de uma série de plug-ins, cada um com a propriedade features . Você pode configurar a propriedade de recursos para ativar ou desativar, um ou mais recursos do RTE. Este artigo descreve como configurar especificamente os plug-ins do RTE.

Para obter detalhes sobre as outras configurações do RTE, consulte [configurar o Editor de Rich Text](/help/implementing/developing/extending/rich-text-editor.md).

>[!NOTE]
>
>Ao trabalhar com o CRXDE Lite, é recomendável salvar as alterações regularmente usando [!UICONTROL Salvar tudo] opção.

## Ativar um plug-in e configurar a propriedade recursos {#activateplugin}

Para ativar um plug-in, siga estas etapas. Algumas etapas são necessárias apenas quando você configura um plug-in pela primeira vez, pois os nós correspondentes não existem.

Por padrão, `format`, `link`, `list`, `justify`e `control` os plug-ins e todos os seus recursos são ativados no RTE.

>[!NOTE]
>
>Os respectivos `rtePlugins` nó é referido como `<rtePlugins-node>` para evitar a duplicação neste artigo.

1. Localize o componente de texto do seu projeto usando o CRXDE Lite.
1. Crie o nó pai de `<rtePlugins-node>` se não existir, antes de configurar qualquer plug-in do RTE:

   * Dependendo do seu componente, os nós principais são:

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * um nó de configuração alternativo: `.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * São do tipo: **jcr:primaryType** `cq:Widget`
   * Ambos têm a seguinte propriedade:

      * **Nome** `name`
      * **Tipo** `String`
      * **Valor** `./text`


1. Dependendo da interface para a qual você está configurando, crie um nó `<rtePlugins-node>`, se não existir:

   * **Nome** `rtePlugins`
   * **Tipo** `nt:unstructured`

1. Abaixo, crie um nó para cada plug-in que deseja ativar:

   * **Tipo** `nt:unstructured`
   * **Nome** a ID do plug-in do plug-in necessário

Depois de ativar um plug-in, siga estas diretrizes para configurar o `features` propriedade.

|  | Habilitar todos os recursos | Ative alguns recursos específicos. | Desative todos os recursos. |
|---|---|---|---|
| Nome | recursos | recursos | recursos |
| Tipo | Sequência de caracteres | `String` (multi-string; definir Tipo como `String` e clique em `Multi` em CRXDE Lite) | Sequência de caracteres |
| Valor | `*` (um asterisco) | Defina para um ou mais valores de recurso. | - |

## Entender o plug-in findreplace {#findreplace}

O `findreplace` O plug-in não precisa de configuração. Funciona imediatamente.

Ao usar a funcionalidade de substituição, a cadeia de caracteres de substituição a ser substituída deve ser inserida ao mesmo tempo que a cadeia de caracteres de localização. No entanto, você ainda pode clicar em localizar para procurar a cadeia de caracteres antes de substituí-la. Se a cadeia de caracteres de substituição for inserida após clicar em localizar, a pesquisa será redefinida para o início do texto.

A caixa de diálogo localizar e substituir se torna transparente quando a localização é clicada, e se torna opaca ao clicar em substituir. O comportamento permite que o autor revise o texto a ser substituído. Se os usuários clicarem em substituir tudo, a caixa de diálogo será fechada e exibirá o número de substituições feitas.

## Configurar os modos de colagem {#pastemodes}

Ao usar o RTE, os autores podem colar o conteúdo em um dos três modos a seguir:

* **Modo de navegador**: Cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode introduzir uma marcação indesejada.

* **Modo de texto sem formatação**: Cole o conteúdo da área de transferência como texto sem formatação. Remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir em [!DNL Experience Manager] componente.

* **Modo MS Word**: Cole o texto, incluindo tabelas, com formatação ao copiar do MS Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou MS Excel, e manter apenas a formatação parcial.

### Configurar as opções de Colar disponíveis na barra de ferramentas do RTE  {#configure-paste-options-available-on-the-rte-toolbar}

É possível fornecer alguns, todos ou nenhum desses três ícones aos autores na barra de ferramentas do RTE:

* **[!UICONTROL Colar (Ctrl+V)]**: Pode ser pré-configurado para corresponder a um dos três modos Colar acima.

* **[!UICONTROL Colar como texto]**: Fornece a funcionalidade do modo de texto simples.

* **[!UICONTROL Colar do Word]**: Fornece a funcionalidade do modo MS Word.

Para configurar o RTE para exibir os ícones necessários, siga essas etapas.

1. Por exemplo, navegue até o seu componente `/apps/<myProject>/components/text`.
1. Navegar até o nó `rtePlugins/edit`. Consulte [ativar um plug-in](#activateplugin) se o nó não existir.
1. Crie o `features` na `edit` e adicione um ou mais recursos. Salve todas as alterações.

### Configure o comportamento do ícone e do atalho Colar (Ctrl+V) {#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}

Você pode pré-configurar o comportamento do **[!UICONTROL Colar (Ctrl+V)]** usando as etapas a seguir. Essa configuração também define o comportamento do atalho de teclado Ctrl+V que os Autores usam para colar o conteúdo.

A configuração permite os três tipos de casos de uso a seguir:

* Cole o texto usando a implementação de colagem padrão do navegador. Não é um método recomendado, pois pode introduzir uma marcação indesejada. Configurado usando `browser` abaixo.

* Cole o conteúdo da área de transferência como texto sem formatação. Remove todos os elementos de estilo e formatação do conteúdo copiado antes de inserir em [!DNL Experience Manager] componente. Configurado usando `plaintext` abaixo.

* Cole o texto, incluindo tabelas, com formatação ao copiar do MS Word. Não há suporte para copiar e colar texto de outra fonte, como uma página da Web ou MS Excel, e manter apenas a formatação parcial. Configurado usando `wordhtml` abaixo.

1. No seu componente, navegue até `<rtePlugins-node>/edit` nó . Crie os nós se eles não existirem. Para obter mais informações, consulte [ativar um plug-in](#activateplugin).
1. No `edit` nó crie uma propriedade usando os seguintes detalhes:

   * **Nome** `defaultPasteMode`
   * **Tipo** `String`
   * **Valor** é um dos modos de colagem necessários de `browser`, `plaintext`ou `wordhtml` modos.

### Configurar os formatos permitidos ao colar o conteúdo {#pasteformats}

A palavra colar como Microsoft (`paste-wordhtml`) pode ser configurado mais detalhadamente, para que você possa permitir explicitamente alguns estilos ao colar em [!DNL Experience Manager] de outro programa, como [!DNL Microsoft Word].

Por exemplo, se somente formatos em negrito e listas forem permitidos ao colar em [!DNL Experience Manager], é possível filtrar os outros formatos. Isso é chamado de filtragem de colagem configurável, que pode ser feita para ambos:

* [Texto](#pastemodes)
* [Links](#linkstyles)

Para links, também é possível definir os protocolos que são aceitos automaticamente.

Para configurar quais formatos são permitidos ao colar texto em [!DNL Experience Manager] de outro programa:

1. No seu componente, navegue até o nó `<rtePlugins-node>/edit`. Crie os nós se o nó não existir. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie um nó no `edit` nó para manter as regras de HTML paste:

   * **Nome** `htmlPasteRules`
   * **Tipo** `nt:unstructured`

1. Criar um nó em `htmlPasteRules`, para conter detalhes dos formatos básicos permitidos:

   * **Nome** `allowBasics`
   * **Tipo** `nt:unstructured`

1. Para controlar os formatos individuais aceitos, crie uma ou mais das seguintes propriedades na `allowBasics` nó:

   * **Nome** `bold`
   * **Nome** `italic`
   * **Nome** `underline`
   * **Nome** `anchor` (para links e âncoras nomeadas)
   * **Nome** `image`

   Todas as propriedades são de **Tipo** `Boolean`, de acordo com as **Valor** você pode selecionar ou remover a marca de seleção para ativar ou desativar a funcionalidade.

   >[!NOTE]
   >
   >Se não estiver definido explicitamente, o valor padrão de true será usado e o formato será aceito.

1. Outros formatos também podem ser definidos usando uma variedade de outras propriedades ou nós, também aplicados à função `htmlPasteRules` nó:

| Propriedade | Tipo | Descrição |
|--- |--- |--- |
| `allowBlockTags` | `String` | Define a lista de tags de bloco permitidas. Algumas tags de bloco possíveis incluem títulos (h1, h2, h3), parágrafos (p), listas (ol, ul), tabelas (tabela). |
| `fallbackBlockTag` | `String` | Define a tag de bloco usada para qualquer bloco que tenha uma tag de bloco não incluída em `allowBlockTags`. Geralmente, `p` suficiente. |
| `table` | `nt:unstructured` | Define o comportamento ao colar tabelas. Esse nó deve ter a propriedade allow (type Boolean) para definir se colar tabelas é permitido. Se allow estiver definido como false, você deverá especificar a propriedade ignoreMode (type String) para definir como o conteúdo da tabela colada é manipulado. Valores válidos para ignoreMode são `remove` para remover o conteúdo da tabela e `paragraph` para transformar células da tabela em parágrafos. |
| `list` | `nt:unstructured` | Define o comportamento ao colar listas. Deve ter a propriedade `allow` (digite Boolean) para definir se a colagem de listas é permitida. If `allow` está definida como `false`, especifique a propriedade `ignoreMode` (tipo `String`) para definir como lidar com qualquer conteúdo da lista colada. Os valores válidos para ignoreMode são `remove` que remove o conteúdo da lista e `paragraph` que transforma itens de lista em parágrafos. |

Um exemplo de um `htmlPasteRules` A estrutura é abaixo:

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

Os autores podem aplicar Estilos para alterar a aparência de uma parte do texto. Os estilos são baseados em classes CSS predefinidas na folha de estilos CSS. O conteúdo estilizado é delimitado em `span` tags que usam o `class` atributo para se referir à classe CSS. Por exemplo:

`<span class=monospaced>Monospaced Text Here</span>`

Quando o plug-in Estilos é ativado pela primeira vez, nenhum Estilo padrão está disponível. A lista pop-up está vazia. Para fornecer estilos aos autores, faça o seguinte:

* Habilite o seletor suspenso Estilo .
* Especifique um ou mais locais das folhas de estilos.
* Especifique os estilos individuais que podem ser selecionados na lista pop-up de estilo.

Para reconfigurações posteriores, digamos para adicionar mais estilos, siga apenas as instruções para fazer referência a uma nova folha de estilos e especificar os estilos adicionais.

>[!NOTE]
>
>Os estilos também podem ser definidos para [tabelas ou células de tabela](configure-rich-text-editor-plug-ins.md#tablestyles). Essas configurações exigem procedimentos separados.

### Ativar a lista suspensa Seletor de estilo {#styleselectorlist}

Isso é feito ativando o plug-in de estilos.

1. No seu componente, navegue até o nó `<rtePlugins-node>/styles`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` na `styles` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

1. Salve todas as alterações.

>[!NOTE]
>
>Quando o plug-in Estilos estiver ativado, a lista suspensa Estilo será exibida na caixa de diálogo de edição. No entanto, a lista está vazia, pois nenhum Estilo está configurado.

### Especificar a localização da folha de estilos {#locationofstylesheet}

Em seguida, especifique a(s) localização(ões) da(s) folha(s) de estilos que deseja referenciar:

1. Navegue até o nó raiz do seu componente de texto, por exemplo `/apps/<myProject>/components/text`.
1. Adicionar a propriedade `externalStyleSheets` ao nó pai de `<rtePlugins-node>`:

   * **Nome** `externalStyleSheets`
   * **Tipo** `String[]` (multi-string; click **Multi** no CRXDE)
   * **Valor(es)** O caminho e o nome de arquivo de cada folha de estilos que deseja incluir. Use caminhos do repositório.

   >[!NOTE]
   >
   >É possível adicionar referências a folhas de estilos adicionais a qualquer momento.

1. Salve todas as alterações.

Ao usar o RTE em uma caixa de diálogo (interface clássica), você pode especificar folhas de estilos otimizadas para edição de rich text. Devido a restrições técnicas, o contexto de CSS é perdido no editor, para que você possa emular esse contexto para melhorar a experiência de WYSIWYG.

O Editor de Rich Text usa um elemento DOM de contêiner com uma ID de `CQrte` que oferece estilos diferentes para exibir e editar:

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

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/styles`, como criado em [Ativação do seletor suspenso de estilo](#styleselectorlist).
1. No nó `styles`, crie um nó (também chamado de `styles`) para manter a lista que está sendo disponibilizada:

   * **Nome** `styles`
   * **Tipo** `cq:WidgetCollection`

1. Crie um nó no `styles` nó para representar um estilo individual:

   * **Nome**, é possível especificar o nome, mas ele deve ser adequado para o estilo
   * **Tipo** `nt:unstructured`

1. Adicionar a propriedade `cssName` para este nó para fazer referência à classe CSS:

   * **Nome** `cssName`
   * **Tipo** `String`
   * **Valor** O nome da classe CSS (sem um &#39;.&#39; anterior; por exemplo, `cssClass` em vez de `.cssClass`)

1. Adicionar a propriedade `text` no mesmo nó; isso define o texto mostrado na caixa de seleção:

   * **Nome** `text`
   * **Tipo** `String`
   * **Valor** Descrição do estilo; é exibida na caixa de seleção suspensa Estilo .

1. Salve as alterações.

   Repita as etapas acima para cada estilo necessário.

### Configurar o RTE para quebras de palavras ideais em japonês {#jpwordwrap}

Autores que usam [!DNL Experience Manager] para criar o conteúdo do idioma japonês, aplique um estilo aos caracteres para evitar quebras de linha, onde não é necessária uma quebra. Isso permite que os autores deixem as frases quebrarem na posição desejada. O estilo para essa funcionalidade é baseado na classe CSS predefinida na folha de estilos CSS.

Para criar o estilo que os autores podem aplicar ao texto em japonês, siga estas etapas:

1. Crie um nó no nó estilos . Consulte [especificar um estilo](#stylesindropdown).
   * Nome: `jpn-word-wrap`
   * Tipo: `nt:unstructure`

1. Adicionar a propriedade `cssName` ao nó para fazer referência à classe CSS. Este nome de classe é um nome reservado para o recurso de quebra automática de texto em japonês.
   * Nome: `cssName`
   * Tipo: `String`
   * Valor: `jpn-word-wrap` (sem `.`)

1. Adicione o texto da propriedade ao mesmo nó. O valor é o nome do estilo que os autores veem ao selecionar o estilo.
   * Nome: `text`
*Tipo: 
`String`
   * Valor: `Japanese word-wrap`

1. Crie uma folha de estilos e especifique seu caminho. Consulte [especificar a localização da folha de estilos](#locationofstylesheet). Adicione o seguinte conteúdo à folha de estilos. Altere a cor do plano de fundo conforme desejado.

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

Qualquer texto criado no RTE é colocado em uma tag de bloco, sendo o padrão `<p>`. Ao ativar a `paraformat` , você especifica tags de bloco adicionais que podem ser atribuídas a parágrafos, usando uma lista suspensa de seleção. Os formatos de parágrafo determinam o tipo de parágrafo atribuindo a tag de bloco correta. O autor pode selecioná-los e atribuí-los usando o seletor de Formato. As tags de bloco de exemplo incluem, entre outras, o parágrafo padrão &lt;p> e rubricas &lt;h1>, &lt;h2>e assim por diante.

>[!CAUTION]
>
>Esse plug-in não é adequado para conteúdo com estrutura complexa, como listas ou tabelas.

>[!NOTE]
>
>Se uma tag de bloco, por exemplo, uma `<hr>` , não pode ser atribuído a um parágrafo, não é um caso de uso válido para um `paraformat` plug-in.

Quando o plug-in Formatos de parágrafo é ativado pela primeira vez, nenhum Formatos de parágrafo padrão é disponibilizado. A lista pop-up está vazia. Para fornecer formatos de parágrafo aos autores, faça o seguinte:

* Ative o [!UICONTROL Formato] lista do seletor de pop-up.
* Especifique as tags de bloco que podem ser selecionadas como formatos de parágrafo no menu pop-up.

Para reconfigurações posteriores, digamos para adicionar mais formatos, siga apenas a parte relevante das instruções.

### Ativar o seletor suspenso Formato {#formatselectorlist}

Para ativar o `paraformat` siga estas etapas:

1. No seu componente, navegue até o nó `<rtePlugins-node>/paraformat`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` na `paraformat` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*` (asterisco)

>[!NOTE]
>
>Se o plug-in não for configurado mais, os formatos padrão que são ativados são Parágrafo ( `<p>`), Título 1 ( `<h1>`), Título 2 ( `<h2>`), Título 3 ( `<h3>`).

>[!CAUTION]
>
>Ao configurar os formatos de parágrafo do RTE, não remova a tag de parágrafo &lt;p> como uma opção de formatação. Se a variável `<p>` for removida, o autor de conteúdo não poderá selecionar a variável [!UICONTROL Formatos de parágrafo] mesmo se houver formatos adicionais configurados.

### Especificar os Formatos de Parágrafo disponíveis {#paraformatsindropdown}

Os formatos de parágrafo são disponibilizados para seleção por:

1. Na definição do componente, navegue até o nó `<rtePlugins-node>/paraformat`, como criado em [Ativação do seletor suspenso de formato](#styleselectorlist).
1. Em `paraformat` criar um nó, para manter a lista de formatos:

   * **Nome** `formats`
   * **Tipo** `cq:WidgetCollection`

1. Crie um nó no `formats` , mantém os detalhes de um formato individual:

   * **Nome**, é possível especificar o nome, mas ele deve ser adequado para o formato (por exemplo, myparágrafo, myheader1).
   * **Tipo** `nt:unstructured`

1. Nesse nó, adicione a propriedade para definir a tag de bloco usada:

   * **Nome** `tag`
   * **Tipo** `String`
   * **Valor** A marca de bloco do formato; por exemplo: p, h1, h2, etc.

      Não é necessário inserir os colchetes delimitadores.

1. Para que o mesmo nó adicione outra propriedade, para que o texto descritivo apareça na lista suspensa:

   * **Nome** `description`
   * **Tipo** `String`
   * **Valor** O texto descritivo desse formato; por exemplo, Parágrafo, Cabeçalho 1, Cabeçalho 2 e assim por diante. Este texto é exibido na lista de seleção Formato.

1. Salve as alterações.

   Repita as etapas para cada formato necessário.

>[!CAUTION]
Se você definir formatos personalizados, os formatos padrão (`<p>`, `<h1>`, `<h2>`e `<h3>`) são removidas. Recriar `<p>` como é o formato padrão.

## Configurar caracteres especiais {#spchar}

Em um [!DNL Experience Manager] instalação, quando a variável `misctools` está habilitado para caracteres especiais (`specialchars`) uma seleção por defeito é imediatamente disponibilizada para utilização; por exemplo, os símbolos de direitos autorais e de marcas registradas.

Você pode configurar o RTE para disponibilizar sua seleção de caracteres; definindo caracteres distintos ou uma sequência inteira.

>[!CAUTION]
Adicionar seus caracteres especiais substitui a seleção padrão. Se necessário, redefina esses caracteres em sua seleção.

### Definir um caractere único {#definesinglechar}

1. No seu componente, navegue até o nó `<rtePlugins-node>/misctools`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` na `misctools` nó:

   * **Nome** `features`
   * **Tipo** `String[]`
   * **Valor** `specialchars`

          ou `String / *` se estiver aplicando todos os recursos para este plug-in)

1. Em `misctools` crie um nó para manter as configurações de caracteres especiais:

   * **Nome** `specialCharsConfig`
   * **Tipo** `nt:unstructured`

1. Em `specialCharsConfig` crie outro nó para manter a lista de caracteres:

   * **Nome** `chars`
   * **Tipo** `nt:unstructured`

1. Em `chars` adicione um nó para manter uma definição de caractere individual:

   * **Nome** é possível especificar o nome, mas ele deve refletir o caractere; por exemplo, metade.
   * **Tipo** `nt:unstructured`

1. Para esse nó, adicione a seguinte propriedade:

   * **Nome** `entity`
   * **Tipo** `String`
   * **Valor** Representação HTML do caráter requerido; por exemplo, `&189;` para a fração de metade.

1. Salve as alterações.

No CRXDE, depois que a propriedade é salva, o caractere representado é exibido. Veja abaixo o exemplo da metade. Repita as etapas acima para disponibilizar caracteres mais especiais para os autores.

![No CRXDE, adicione um único caractere a ser disponibilizado na barra de ferramentas do RTE](assets/chlimage_1-106.png "No CRXDE, adicione um único caractere a ser disponibilizado na barra de ferramentas do RTE")

### Definir um intervalo de caracteres {#definerangechar}

1. Use os passos 1 a 3 de [Definir um caractere único](#definesinglechar).
1. Em `chars` adicione um nó para manter a definição do intervalo de caracteres:

   * **Nome** é possível especificar o nome, mas ele deve refletir o intervalo de caracteres; por exemplo, lápis.
   * **Tipo** `nt:unstructured`

1. Nesse nó (nomeado de acordo com o intervalo de caracteres especial), adicione as duas propriedades a seguir:

   * **Nome** `rangeStart`

      **Tipo** `Long`
      **Valor** o [Unicode](https://unicode.org/) representação (decimal) do primeiro caractere no intervalo

   * **Nome** `rangeEnd`

      **Tipo** `Long`
      **Valor** o [Unicode](https://unicode.org/) representação (decimal) do último caractere no intervalo

1. Salve as alterações.

   Por exemplo, definir um intervalo de 9998 - 10000 fornece os seguintes caracteres.

   ![No CRXDE, defina um intervalo de caracteres a serem disponibilizados no RTE](assets/chlimage_1-107.png)

   *Figura: No CRXDE, defina um intervalo de caracteres a serem disponibilizados no RTE*

   ![Caracteres especiais disponíveis no RTE são exibidos para os autores em uma janela pop-up](assets/rtepencil.png "Caracteres especiais disponíveis no RTE são exibidos para os autores em uma janela pop-up")

## Configurar estilos de tabela {#tablestyles}

Os estilos normalmente são aplicados no texto, mas um conjunto separado de Estilos também pode ser aplicado em uma tabela ou em algumas células da tabela. Esses Estilos estão disponíveis para os autores na caixa do seletor Estilo na caixa de diálogo Propriedades da célula ou Propriedades da tabela . Os estilos estão disponíveis ao editar uma tabela em um componente de Texto (ou derivado) e não no componente de Tabela padrão.

>[!NOTE]
Você pode definir estilos para tabelas e células somente para a interface clássica.

>[!NOTE]
Copiar e colar tabelas no componente RTE ou dele depende do navegador. Não é compatível imediatamente com todos os navegadores. Você pode obter resultados variados dependendo da estrutura da tabela e do navegador. Por exemplo, ao copiar e colar uma tabela em um componente RTE no Mozilla Firefox na interface clássica e na interface de toque, o layout da tabela não é preservado.

1. No componente, navegue até o nó `<rtePlugins-node>/table`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. Crie o `features` na `table` nó:

   * **Nome** `features`
   * **Tipo** `String`
   * **Valor** `*`

   >[!NOTE]
   Se não quiser ativar todos os recursos da tabela, é possível criar a variável `features` propriedade como:
   * **Tipo** `String[]`
   * **Valor** s) Uma ou ambas, conforme exigido:
      * `table` para permitir a edição de propriedades de tabela; incluindo os estilos.
      * `cellprops` para permitir a edição de propriedades da célula, incluindo os estilos.


1. Defina o local das folhas de estilos CSS para referenciá-las. Consulte [Especificação do local da folha de estilos](#locationofstylesheet) já que isso é o mesmo que definir [estilos para texto](#textstyles). O local pode ser definido se você tiver definido outros estilos.
1. Em `table` crie os seguintes nós conforme necessário:

   * Para definir estilos para a tabela inteira (disponível em **[!UICONTROL Propriedades da tabela]**):

      * **Nome** `tableStyles`
      * **Tipo** `cq:WidgetCollection`
   * Definição de estilos para células individuais (disponível em **[!UICONTROL Propriedades da célula]**),

      * **Nome** `cellStyles`
      * **Tipo** `cq:WidgetCollection`


1. Crie um nó (na guia `tableStyles` ou `cellStyles` (conforme apropriado) para representar um estilo individual,

   * **Nome** é possível especificar o nome, mas ele deve refletir o estilo.
   * **Tipo** `nt:unstructured`

1. Nesse nó, crie as propriedades:

   * Para definir o estilo CSS referenciado,

      * **Nome** `cssName`
      * **Tipo** `String`
      * **Valor** o nome da classe CSS (sem uma `.`, por exemplo, `cssClass` em vez de `.cssClass`)
   * Para definir um texto descritivo a ser exibido no seletor pop-up,

      * **Nome** `text`
      * **Tipo** `String`
      * **Valor** o texto a ser exibido na lista de seleção


1. Salve todas as alterações.

Repita as etapas acima para cada estilo necessário.

### Configurar cabeçalhos ocultos em tabelas para acessibilidade {#hiddenheader}

Às vezes, é possível criar tabelas de dados sem texto visual em um cabeçalho de coluna, supondo que a finalidade do cabeçalho seja implícita pelo relacionamento visual da coluna com outras colunas. Nesse caso, é necessário fornecer texto interno oculto na célula do cabeçalho para permitir que leitores de tela e outras tecnologias de assistência ajudem os leitores com várias necessidades a entender a finalidade da coluna.

Para aprimorar a acessibilidade em tais cenários, o RTE suporta células de cabeçalho ocultas. Além disso, ele fornece configurações relacionadas a cabeçalhos ocultos em tabelas. Essas configurações permitem aplicar estilos de CSS em cabeçalhos ocultos nos modos de edição e visualização. Para ajudar os autores a identificar cabeçalhos ocultos no modo de edição, inclua os seguintes parâmetros no código:

* `hiddenHeaderEditingCSS`: Especifica o nome da classe CSS aplicada na célula de cabeçalho oculta, quando o RTE é editado.
* `hiddenHeaderEditingStyle`: Especifica uma sequência de estilo que é aplicada na célula de cabeçalho oculta quando o RTE é editado.

Se você especificar o CSS e a sequência de estilo no código, a classe CSS terá prioridade sobre a sequência de estilo e poderá substituir qualquer alteração de configuração feita pela sequência de estilo.

Para ajudar os autores a aplicar o CSS em cabeçalhos ocultos no modo de visualização, é possível incluir os seguintes parâmetros no código:

* `hiddenHeaderClassName`: Especifica o nome da classe CSS aplicada na célula do cabeçalho oculta no modo de visualização.
* `hiddenHeaderStyle`: Especifica uma sequência de estilo que é aplicada na célula do cabeçalho oculto no modo de visualização.

Se você especificar o CSS e a sequência de estilo no código, a classe CSS terá prioridade sobre a sequência de estilo e poderá substituir qualquer alteração de configuração feita pela sequência de estilo.

## Adicionar dicionários para o verificador de ortografia {#adddict}

Quando o plug-in de verificação ortográfica é ativado, o RTE usa dicionários para cada idioma apropriado. Estes são então selecionados de acordo com o idioma do site, tirando a propriedade de idioma da subárvore ou extraindo o idioma do URL; por exemplo. o `/en/` a ramificação é verificada em inglês, a `/de/` ramificação como alemã.

>[!NOTE]
A mensagem &quot;Falha na verificação ortográfica&quot;. é visto se uma verificação está sendo tentada para um idioma que não está instalado.

Uma instalação padrão do Experience Manager inclui os dicionários para:

* Inglês Americano (en_us)
* Inglês britânico (en_gb)

>[!NOTE]
Os dicionários padrão estão localizados em `/libs/cq/spellchecker/dictionaries`, juntamente com os arquivos ReadMe apropriados. Não modifique os arquivos.

Para adicionar mais dicionários, se necessário, siga estas etapas.

1. Navegar até a página [https://extensions.openoffice.org/](https://extensions.openoffice.org/).
1. Selecione o idioma necessário e baixe o arquivo ZIP com as definições de ortografia. Extraia o conteúdo do arquivo no seu sistema de arquivos.

   >[!CAUTION]
   Somente os dicionários na `MySpell` são compatíveis com o formato OpenOffice.org v2.0.1 ou anterior. Como os dicionários agora são arquivos de arquivamento, recomenda-se verificar o arquivo após o download.

1. Localize os arquivos .aff e .dic . Mantenha o nome do arquivo em minúsculas. Por exemplo, `de_de.aff` e `de_de.dic`.
1. Carregue os arquivos .aff e .dic no repositório em `/apps/cq/spellchecker/dictionaries`.

>[!NOTE]
O verificador ortográfico do RTE está disponível sob demanda. Ele não é executado automaticamente à medida que você começa a digitar o texto.
Para executar o verificador ortográfico, toque/clique no botão Verificador ortográfico na barra de ferramentas. O RTE verifica a ortografia das palavras e realça as palavras com ortografia incorreta.
Se você incorporar qualquer alteração sugerida pelo verificador ortográfico, o estado do texto será alterado e as palavras com ortografia incorreta não serão mais destacadas. Para executar o verificador ortográfico, toque/clique no botão Verificador ortográfico novamente.

## Configure o tamanho do histórico para ações de desfazer e refazer {#undohistory}

O RTE permite que os autores desfaçam ou refaçam algumas últimas edições. Por padrão, 50 edições são armazenadas no histórico. Você pode configurar esse valor conforme necessário.

1. No componente, navegue até o nó `<rtePlugins-node>/undo`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `undo` nó criar a propriedade :

   * **Nome** `maxUndoSteps`
   * **Tipo** `Long`
   * **Valor** o número de etapas do comando desfazer que você deseja salvar no histórico. O padrão é 50. Use `0` para desabilitar completamente desfazer/refazer.

1. Salve as alterações.

## Configurar o tamanho da guia {#tabsize}

Quando o caractere de tabulação é pressionado dentro de qualquer texto, um número predefinido de espaços é inserido; por padrão, há três espaços sem quebra e um espaço.

Para definir o tamanho da guia:

1. No seu componente, navegue até o nó `<rtePlugins-node>/keys`. Crie os nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `keys` nó criar a propriedade :

   * **Nome** `tabSize`
   * **Tipo** `String`
   * **Valor** o número de caracteres de espaço a serem usados para o tabulador.

1. Salve as alterações.

## Definir margem de recuo {#indentmargin}

Quando o recuo estiver ativado (padrão), é possível definir o tamanho do recuo:

>[!NOTE]
O tamanho do travessão é aplicado somente aos parágrafos (blocos) do texto; não afeta o recuo das listas reais.

1. No componente, navegue até o nó `<rtePlugins-node>/lists`. Crie esses nós se eles não existirem. Para obter mais detalhes, consulte [ativar um plug-in](#activateplugin).
1. No `lists` nó criar o `identSize` parâmetro:

   * **Nome**: `identSize`
   * **Tipo**: `Long`
   * **Valor**: número de pixels necessários para a margem de recuo.

## Configurar a altura do espaço editável {#editablespace}

Você pode definir a altura do espaço editável mostrado na caixa de diálogo do componente. A configuração só é aplicável ao usar o RTE em uma caixa de diálogo. A configuração não altera a altura da janela de diálogo.

1. No `../items/text` , na definição da caixa de diálogo do componente, crie uma propriedade :

   * **Nome** `height`
   * **Tipo** `Long`
   * **Valor** a altura da tela de edição em pixels.

1. Salve as alterações.

## Configurar estilos e protocolos para links {#linkstyles}

Ao adicionar links em [!DNL Experience Manager], é possível definir os estilos de CSS a serem usados e os protocolos a serem aceitos automaticamente. Para configurar como os links são adicionados em [!DNL Experience Manager] em outro programa, defina as regras de HTML.

1. Localize o componente de texto do seu projeto usando o CRXDE Lite.
1. Crie um nó no mesmo nível que `<rtePlugins-node>`, ou seja, crie o nó sob o nó pai de `<rtePlugins-node>`:

   * **Nome** `htmlRules`
   * **Tipo** `nt:unstructured`

   >[!NOTE]
   O `../items/text` O nó tem a propriedade :
   * **Nome** `xtype`
   * **Tipo** `String`
   * **Valor** `richtext`

   A localização da variável `../items/text` pode variar, dependendo da estrutura da caixa de diálogo. Dois exemplos são `/apps/myProject>/components/text/dialog/items/text` e `/apps/<myProject>/components/text/dialog/items/panel/items/text`.

1. Em `htmlRules`, crie um nó .

   * **Nome** `links`
   * **Tipo** `nt:unstructured`

1. Em `links` nó defina as propriedades conforme necessário:

   * Estilo CSS para links internos:

      * **Nome** `cssInternal`
      * **Tipo** `String`
      * **Valor** o nome da classe CSS (sem um &#39;.&#39; anterior; por exemplo, `cssClass` em vez de `.cssClass`)
   * Estilo CSS para links externos

      * **Nome** `cssExternal`
      * **Tipo** `String`
      * **Valor** o nome da classe CSS (sem um &#39;.&#39; anterior; por exemplo, `cssClass` em vez de `.cssClass`)
   * Matriz válida **[!UICONTROL protocolos]** incluindo `https://`, `https://`, `file://`, `mailto:`e outros,

      * **Nome** `protocols`
      * **Tipo** `String[]`
      * **Valor**(s) um ou mais protocolos
   * **defaultProtocol** (propriedade do tipo **String**): Protocolo a ser usado se o usuário não especificou um explicitamente.

      * **Nome** `defaultProtocol`
      * **Tipo** `String`
      * **Valor**(s) um ou mais protocolos padrão
   * Definição de como lidar com o atributo target de um link. Criar um nó:

      * **Nome** `targetConfig`
      * **Tipo** `nt:unstructured`

      No nó `targetConfig`: defina as propriedades necessárias:

      * Especifique o modo de destino:

         * **Nome** `mode`
         * **Tipo** `String`)
         * **Valor** s) :

            * `auto`: significa que um objetivo automático é escolhido

               (especificado pelo `targetExternal` propriedade de links externos ou `targetInternal` para links internos).

            * `manual`: não aplicável neste contexto
            * `blank`: não aplicável neste contexto
      * O target para links internos:

         * **Nome** `targetInternal`
         * **Tipo** `String`
         * **Valor** o target para links internos (use somente quando o modo estiver `auto`)
      * O target para links externos:

         * **Nome** `targetExternal`
         * **Tipo** `String`
         * **Valor** o target para links externos (usado somente quando o modo é `auto`).








1. Salve todas as alterações.
