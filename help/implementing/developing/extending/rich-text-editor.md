---
title: Configure o Editor de Rich Text para criar conteúdo [!DNL Adobe Experience Manager] em um Cloud Service.
description: Configure o Editor de Rich Text para criar conteúdo [!DNL Adobe Experience Manager] em um Cloud Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 739dde6f9a6a7f4fe773e27e53f23a395f2881dc
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 0%

---


# Configure the Rich Text Editor {#configure-the-rich-text-editor}

O Editor de Rich Text (RTE) fornece aos autores uma ampla variedade de funcionalidades para editar conteúdo de texto. Ícones, caixas de seleção, barra de ferramentas e menus são fornecidos para uma experiência de edição de texto WYSIWYG. Os administradores configuram o RTE para ativar, desativar e estender os recursos disponíveis nos componentes de criação. Veja como os autores [usam o RTE para criar](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md) conteúdo da Web.

Os conceitos e as etapas do RTE necessários para configurá-lo estão listados abaixo.

| Compreender conceitos do RTE | Ativar recursos necessários | Configurar funcionalidades individuais |
|---|---|---|
| [Entenda a interface](#understand-rte-ui) | [Entender e definir locais de configuração](#understand-the-configuration-paths-and-locations) | [Configurar plug-ins](#enable-rte-functionalities-by-activating-plug-ins) |
| [Tipos de modos de edição](#editingmodes) | [Ativar plug-ins](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin) | [Definir propriedades de recursos](#aboutplugins) |
| [Sobre plug-ins](#aboutplugins) | [Configurar barras de ferramentas RTE](#dialogfullscreen) | [Configurar os modos de colagem](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles) |

## Compreender a interface do usuário disponível para autores {#understand-rte-ui}

A interface do RTE oferta um design [](/help/sites-cloud/authoring/features/responsive-layout.md) responsivo para o ambiente de criação. A interface foi projetada para uso em dispositivos de toque e desktop.

![Barra de ferramentas do Editor de Rich Text](assets/rte-toolbar-full-screen-mode.png)

*Figura: Barra de ferramentas do Editor de Rich Text com todas as opções disponíveis ativadas.*

A barra de ferramentas fornece as opções para a experiência de criação WYSIWYG. [!DNL Experience Manager] os administradores podem configurar as opções disponíveis na barra de ferramentas da interface. Por padrão, um conjunto abrangente de opções de edição está disponível em [!DNL Experience Manager]. Os desenvolvedores podem personalizar [!DNL Experience Manager] para adicionar mais opções de edição.

## Vários modos de edição {#editingmodes}

Os autores podem criar e editar conteúdo textual usando [!DNL Experience Manager] os diferentes modos de componentes. As opções da barra de ferramentas para criação e formatação de conteúdo e a experiência do usuário dos componentes habilitados para RTE em diferentes modos de edição variam com base nas configurações do RTE.

| Modo de edição | Área de edição | Recursos recomendados a serem ativados |
|--- |--- |--- |
| Inline | Edição no local para edições rápidas e secundárias; Formatar sem abrir uma caixa de diálogo. | Recursos mínimos de RTE. |
| RTE em tela cheia | Abrange a página inteira. | Todos os recursos RTE necessários. |
| Caixa de diálogo | Caixa de diálogo na parte superior do conteúdo da página, mas não cobre a página inteira. | Ativar recursos de forma judicial. |
| Diálogo em tela cheia | Igual ao modo de tela cheia; contém campos da caixa de diálogo ao lado do RTE. | Todos os recursos RTE necessários. |

>[!NOTE]
>
>O recurso de edição de origem não está disponível no modo de edição em linha. Não é possível arrastar imagens no modo de tela cheia. Todos os outros recursos funcionam em todos os modos.

### Edição em linha {#inline-editing}

Para editar o conteúdo em uma página, abra o conteúdo com um duplo lento e clique em . Uma barra de ferramentas compacta com opções básicas é apresentada.

![Edição em linha com opções básicas na barra de ferramentas](assets/inline-editing-mode-basic-options.png)

*Figura: Edição embutida com opções básicas na barra de ferramentas.*

### Full-screen editing {#full-screen-editing}

[!DNL Experience Manager] os componentes podem ser abertos na visualização de tela cheia que oculta o conteúdo da página e ocupa a tela disponível. Considere a edição em tela cheia de uma versão detalhada da edição em linha, já que ela oferta mais opções de edição. Para abri-lo, clique em ![Ícone para abrir o RTE em tela](assets/rte_fullscreen.png)cheia, na barra de ferramentas compacta, ao usar o modo de edição em linha.

No modo de tela cheia da caixa de diálogo, juntamente com uma barra de ferramentas RTE detalhada, as opções e os componentes disponíveis em uma caixa de diálogo também estão disponíveis. É aplicável somente para uma caixa de diálogo que contém o RTE junto com outros componentes.

![A barra de ferramentas RTE detalhada ao editar no modo de tela cheia](assets/rte-toolbar-full-screen-mode.png)

*Figura: A barra de ferramentas RTE detalhada ao editar no modo de tela cheia.*

### Edição de diálogo {#dialog-editing}

Quando um componente é clicado em duplo, uma caixa de diálogo é aberta para edição do conteúdo. A caixa de diálogo é aberta na parte superior da página existente. Em alguns cenários específicos, a caixa de diálogo é aberta como uma janela pop-up. Por exemplo, quando um componente de Texto faz parte de uma coluna em um layout de página com várias colunas e a área disponível para a caixa de diálogo é menor.

![Modo de edição de diálogo](assets/dialog_editing_modetouchui.png)

*Figura: Modo de edição de diálogo.*

## Sobre plug-ins RTE e os recursos associados {#aboutplugins}

A funcionalidade é disponibilizada por meio de uma série de plug-ins, cada um com:

* Uma `features` propriedade que é,

   * Usado para ativar ou desativar a funcionalidade básica desse plug-in.
   * Configurado usando um procedimento padronizado.

* Quando apropriado, mais propriedades e opções exigem configuração especializada.

Os recursos básicos do RTE são ativados ou desativados pelo valor da `features` propriedade em um nó específico ao plug-in adequado.

A tabela a seguir lista os plug-ins atuais, mostrando:

* IDs de plug-in com um link para a documentação da API. A ID é usada como o nome do nó ao [ativar um plug-in](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valores permitidos para a `features` propriedade.
* Uma descrição da funcionalidade fornecida pelo plug-in.

| ID do plug-in | feições | Descrição |
|--- |--- |--- |
| editar | `cut`, `copy`, `paste-default`, `paste-plaintext`, `paste-wordhtml` | [Corte, copie e, os três modos](/help/implementing/developing/extending/configure-rich-text-editor-plug-ins.md#textstyles)de colagem. |
| [findreplace](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | `find`, `replace` | Localize e substitua. |
| [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | `bold`, `italic`, `underline` | [Formatação](configure-rich-text-editor-plug-ins.md#textstyles)de texto básica. |
| [imagem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | `image` | Suporte básico a imagens (arraste do conteúdo ou do Localizador de conteúdo). Dependendo do navegador, o suporte tem comportamentos diferentes para autores |
| [teclas](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) | - | Para definir esse valor, consulte o tamanho [da](configure-rich-text-editor-plug-ins.md#tabsize)guia. |
| [justify](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | `justifyleft`, `justifycenter`, `justifyright` | Alinhamento de parágrafo. |
| [links](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | `modifylink`, `unlink`, `anchor` | [Hiperlinks e âncoras](configure-rich-text-editor-plug-ins.md#linkstyles). |
| [listas](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | `ordered`, `unordered`, `indent`, `outdent` | Este plug-in controla tanto o [recuo quanto o lista](configure-rich-text-editor-plug-ins.md#indentmargin); incluindo listas aninhadas. |
| [miscelânea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | `specialchars`, `sourceedit` | Ferramentas diversas permitem que os autores digitem caracteres [](configure-rich-text-editor-plug-ins.md#spchar) especiais ou editem a fonte HTML. Além disso, você pode adicionar um [intervalo de caracteres](configure-rich-text-editor-plug-ins.md#definerangechar) especiais se desejar definir sua própria lista. |
| Paraformat | `paraformat` | Os formatos de parágrafo padrão são Parágrafo, Cabeçalho 1, Cabeçalho 2 e Cabeçalho 3 (`<p>`, `<h1>`, `<h2>`e `<h3>`). É possível [adicionar mais formatos](configure-rich-text-editor-plug-ins.md#paraformats) de parágrafo ou estender a lista. |
| verificação ortográfica | `checktext` | [Verificador ortográfico](configure-rich-text-editor-plug-ins.md#adddict)com reconhecimento de idioma. |
| estilos | `styles` | Suporte para estilização usando uma classe CSS. [Adicione novos estilos](configure-rich-text-editor-plug-ins.md#textstyles) de texto se desejar adicionar (ou estender) seu próprio intervalo de estilos para uso com texto. |
| subsobrescrito | `subscript`, `superscript` | Extensões para os formatos básicos, adicionando sub-script e super-script. |
| tabela | `table`, `removetable`, `insertrow`, `removerow`, `insertcolumn`, `removecolumn`, `cellprops`, `mergecells`, `splitcell`, `selectrow`, `selectcolumns` | Consulte [configurar estilos](configure-rich-text-editor-plug-ins.md#tablestyles) de tabela para adicionar seus próprios estilos para tabelas inteiras ou células individuais. |
| desfazer | `undo`, `redo` | Tamanho do histórico das operações [desfazer e refazer](configure-rich-text-editor-plug-ins.md#undohistory) . |

>[!NOTE]
>
>O plug-in de tela cheia não é suportado no modo de diálogo. Use a configuração `dialogFullScreen` para configurar a barra de ferramentas para o modo de tela cheia.

## Entenda os caminhos e locais de configuração {#understand-the-configuration-paths-and-locations}

O [modo de edição do RTE e a interface](#editingmodes) fornecida aos autores decidem o local dos detalhes de configuração quando você está [ativando os plug-ins](configure-rich-text-editor-plug-ins.md#activateplugin)do RTE. Os locais são:

* Modo em linha: `cq:editConfig/cq:inplaceEditing`.
* Modo de tela cheia: `cq:editConfig/cq:inplaceEditing`.
* Modo de diálogo: `cq:dialog`.
* Modo de diálogo de tela cheia: `cq:dialog`.

>[!NOTE]
>
>Não nomeie o nó `cq:inplaceEditing` como `config`. No `cq:inplaceEditing` nó, defina as seguintes propriedades:
>
>* **Nome**: `configPath`
>* **Tipo**: `String`
>* **Valor**: caminho do nó que contém a configuração real

>
>
Não nomeie o nó de configuração RTE como `config`. Caso contrário, as configurações do RTE terão efeito apenas para os administradores e não para os usuários do grupo `content-author`.

Configure as seguintes propriedades que se aplicam ao modo de edição de Diálogo:

* `useFixedInlineToolbar`: É possível corrigir a barra de ferramentas do RTE em vez de flutuar. Defina essa propriedade Booliana definida no nó RTE com sling:resourceType= `cq/gui/components/authoring/dialog/richtext` como `True`. Quando essa propriedade é definida como `True`, a edição de rich text é iniciada no `foundation-contentloaded` evento. Para evitar isso, defina a propriedade `customStart` como `True` e dispare o `rte-start` evento para a edição do RTE do start. Quando essa propriedade é `true`, o RTE não start ao clicar e esse é o comportamento padrão.

* `customStart`: Defina essa propriedade Booliana definida no nó RTE como `True`, para controlar quando start o RTE acionando o evento `rte-start`.

* `rte-start`: Acionar esse evento no RTE, quando `contenteditable-div` a edição do ERT do start for ativada. Funciona apenas se `customStart` tiver sido definido como `true`.

Quando o RTE for usado na caixa de diálogo habilitada para toque, defina a propriedade `useFixedInlineToolbar` para `true` evitar problemas.

## Ativar funcionalidades do RTE ativando plug-ins {#enable-rte-functionalities-by-activating-plug-ins}

As funcionalidades do RTE são disponibilizadas por meio de uma série de plug-ins, cada um com a propriedade features. Você pode configurar a propriedade features para ativar ou desativar os vários recursos de cada plug-in.

Para obter configurações detalhadas dos plug-ins RTE, consulte [como ativar e configurar os plug-ins](configure-rich-text-editor-plug-ins.md)RTE.

<!-- TBD ENGREVIEW: To confirm if the sample works in CS or not?
**Sample**: Download [this sample configuration](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) that illustrates how to configure RTE. In this package all the features are enabled. -->

O componente [de texto Componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) principais permite que editores de modelo configurem muitos plug-ins RTE usando a interface do usuário como políticas de conteúdo, eliminando a necessidade de configuração técnica. As políticas de conteúdo podem funcionar com configurações de interface do usuário do RTE, conforme descrito neste documento. Para obter mais informações, consulte [criar modelos](/help/sites-cloud/authoring/features/templates.md) de página e a documentação [do desenvolvedor dos Componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html)principais.

>Para fins de referência, os componentes de Texto padrão (fornecidos como parte de uma instalação padrão) podem ser encontrados em:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`

>
>
Para criar seu próprio componente de texto, copie o componente acima em vez de editar esses componentes.

## Configurar a barra de ferramentas RTE {#dialogfullscreen}

[!DNL Experience Manager] permite que você configure a interface para o Editor de Rich Text de forma diferente para os diferentes modos de edição. As configurações padrão são fornecidas abaixo. É possível substituir esses padrões com base em seus requisitos. Personalize apenas os recursos da barra de ferramentas que deseja fornecer aos seus autores. Não é necessário especificar todas as configurações da barra de ferramentas.

Para configurar a barra de ferramentas para `dialogFullScreen`, use a seguinte configuração de amostra.

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

Diferentes configurações da interface do usuário são usadas para o modo em linha e para o modo de tela cheia. A propriedade da barra de ferramentas especifica a opção da barra de ferramentas.

Por exemplo, se a opção for ela mesma um recurso (por exemplo, `Bold`), ela será especificada como `PluginName#FeatureName` (por exemplo, `links#modifylink`).

Se a opção for pop-over (contendo alguns recursos de um plug-in), ela será especificada como `#PluginName` (por exemplo, `#format`).

Os separadores (`|`) entre um grupo de opções podem ser especificados com `-`.

O nó pop-up no modo em linha ou em tela cheia contém uma lista dos pop-ups que estão sendo usados. Cada nó filho sob o `popovers` nó é nomeado após o plug-in (por exemplo, formato). Ele tem uma propriedade &quot;items&quot; que contém uma lista de recursos do plug-in (por exemplo, format#bold).

## Configurações e políticas de conteúdo da interface do usuário do RTE {#rtecontentpolicies}

Os administradores podem controlar as opções de RTE usando políticas de conteúdo, digamos, em vez de fazer a configuração conforme descrito acima. As políticas de conteúdo definem as propriedades de design de um componente quando usadas como parte de um modelo [](/help/sites-cloud/authoring/features/templates.md)editável. Por exemplo, se um componente de texto que usa o RTE for usado com um modelo editável, a política de conteúdo poderá definir que a opção em negrito esteja disponível e algumas opções de formatação de parágrafo estarão disponíveis. As políticas de conteúdo são reutilizáveis e podem ser aplicadas em vários modelos.

As opções disponíveis no RTE fluem downstream das configurações da interface do usuário para as políticas de conteúdo.

* As configurações da interface do usuário definem quais opções estão disponíveis para as políticas de conteúdo.
* Se a configuração da interface do usuário do RTE tiver sido removida ou não ativar um item, a política de conteúdo não poderá configurá-lo.
* Um autor tem acesso apenas à funcionalidade que é disponibilizada pelas configurações da interface do usuário e pelas políticas de conteúdo.

Como exemplo, você pode ver a documentação [do Componente principal de](https://docs.adobe.com/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor)texto.

## Personalizar o mapeamento entre ícones e comandos da barra de ferramentas {#iconstoolbar}

Você pode personalizar o mapeamento entre os ícones Corais exibidos na barra de ferramentas RTE e os comandos disponíveis. Não é possível usar outros ícones além dos ícones Corais.

1. Crie um nó com o nome `icons` em `uiSettings/cui`.

1. Crie nós para ícones individuais abaixo dele.
1. Em cada um dos nós de ícone individuais, especifique um ícone Coral e um comando para mapear para o ícone.

Abaixo está um trecho de amostra para mapear o comando `Bold` para o ícone Coral chamado `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## Limitações conhecidas {#known-limitations}

[!DNL Experience Manager] O recurso RTE tem as seguintes limitações:

* Os recursos do RTE são suportados apenas em caixas de diálogo de [!DNL Experience Manager] componentes. O RTE não é compatível com assistentes ou formulários básicos.

* [!DNL Experience Manager] não funciona em dispositivos híbridos. <!-- TBD: Check. This is not mentioned in Known Issue /help/release-notes/known-issues.md-->

* Não nomeie o nó de configuração RTE `config`. Caso contrário, a configuração do RTE entrará em vigor somente para os administradores e não para os usuários do grupo `content-author`.

* O RTE não suporta a incorporação de conteúdo em um quadro incorporado ou em um iframe.

## Best practices and tips {#best-practices-and-tips}

* Para uma caixa de diálogo flutuante, ative apenas os plug-ins sem uma caixa de diálogo pop-up. Plug-ins sem pop-up são menores e são mais adequados para uma caixa de diálogo flutuante.
* Ative os plug-ins com pop-up maior, como o plug- `Paste` -in, somente no modo de diálogo de tela cheia ou no modo de tela cheia. Plug-ins com pop-up grande precisam de mais espaço físico na tela para fornecer uma boa experiência de criação.
* Se você estiver usando plug-ins personalizados para CoralUI3 RTE, use a `rte.coralui3` biblioteca.

>[!MORELIKETHIS]
>
>* [Configurar plug-ins RTE](configure-rich-text-editor-plug-ins.md)
>* [Usar o Editor de Rich Text para criação](/help/sites-cloud/authoring/fundamentals/rich-text-editor.md)
>* [Configurar o RTE para sites acessíveis](rte-accessible-content.md)
>* [Amostra do tutorial para criar um componente composto de vários campos](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

