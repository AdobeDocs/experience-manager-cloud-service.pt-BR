---
title: Configuração do RTE para o Editor universal
description: Entenda como você pode configurar o editor de rich text (RTE) no Editor universal.
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: e1773cbc2293cd8afe29c3624b29d1e011ea7e10
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---

# Configuração do RTE para o Editor universal {#configure-rte}

Entenda como você pode configurar o editor de rich text (RTE) no Editor universal.

## Visão geral {#overview}

O Editor universal fornece um editor de rich text (RTE) no local e no painel de propriedades para permitir que os autores apliquem alterações de formatação à medida que editam seu texto.

Este RTE é configurável com o uso de [filtros de componente.](/help/implementing/universal-editor/filtering.md) Este documento descreve quais opções de configuração estão disponíveis junto com exemplos.

>[!NOTE]
>
>Quando você inicia um projeto do Universal Editor, todos os recursos de rich text compatíveis com o back-end (AEM com Edge Delivery ou implementação headless) são ativados automaticamente.
>
>* Você pode desativar as opções desnecessárias.
>* Ativar opções que não são compatíveis com seu tipo de projeto não é suportado.

## Estrutura de configuração {#structure}

A configuração do RTE consiste em duas partes:

* [`toolbar`](#toolbar): a configuração da barra de ferramentas controla quais opções de edição estão disponíveis na interface e como elas estão organizadas.
* [`actions`](#actions): a configuração de ações permite personalizar o comportamento e a aparência de ações de edição individuais.

Essas configurações podem ser definidas como parte de um [filtro de componente](/help/implementing/universal-editor/filtering.md) com a propriedade `rte`.

```json
[
  {
    "id": "richtext",
    "rte": {
      "toolbar": {
        // Toolbar configuration
      },
      "actions": {
        // Action-specific configurations
      }
    },
    "components": [
      "richtext"
    ]
  }
]
```

## Configuração da barra de ferramentas {#toolbar}

A configuração da barra de ferramentas controla quais opções de edição estão disponíveis na interface e como elas estão organizadas. Estas são as seções disponíveis

```json
{
  "toolbar": {
    // Text formatting options
    "format": ["bold", "italic", "underline", "strike"],
    // Text alignment options
    "alignment": ["left", "center", "right", "justify"],
    // Text direction options, right-to-left or left-to-right
    "direction": ["rtl", "ltr"],
    // Indentation controls
    "indentation": ["indent", "outdent"],
    // Block-level elements
    "blocks": ["paragraph", "h1", "h2", "h3", "h4", "h5", "h6", "code_block"],
    // List options
    "list": ["bullet_list", "ordered_list"],
    // Content insertion
    "insert": ["link", "unlink", "image"],
    // Superscript/subscript
    "sr_script": ["superscript", "subscript"],
    // Editor utilities
    "editor": ["removeformat"],
    // Section ordering (optional)
    "sections": ["format", "alignment", "list"]
  }
}
```

## Configuração de ações {#actions}

A configuração de ações permite personalizar o comportamento e a aparência de ações de edição individuais. Estas são as seções disponíveis.

### Ações de formato {#format}

As ações de formato são usadas para aplicar formatação e oferecer suporte à alternância de tags do HTML para escolher entre variantes semânticas. As seções a seguir estão disponíveis.

```json
{
  "actions": {
    "bold": {
      "tag": "strong",      // Use <strong> instead of <b>
      "shortcut": "Mod-B",  // Custom keyboard shortcut
      "label": "Make Bold"  // Custom button label 
    },
    "italic": {
      "tag": "em",          // Use <em> instead of <i>
      "shortcut": "Mod-I",
      "label": "Italicize"
    },
    "strike": {
      "tag": "del"          // Use <del> instead of <s>
    }
  }
}
```

### Ações da lista {#list}

As ações de lista oferecem suporte à quebra automática de conteúdo para controlar a estrutura do HTML. As seções a seguir estão disponíveis.

```json
{
  "actions": {
    "bullet_list": {
      "wrapInParagraphs": true,    // <ul><li><p>content</p></li></ul>
      "shortcut": "Mod-Shift-8",   // Custom shortcut
      "label": "Bullet List"       // Custom label
    },
    "ordered_list": {
      "wrapInParagraphs": false,   // <ol><li>content</li></ol> (default)
      "shortcut": "Mod-Shift-9"
    }
  }
}
```

### Ações do link {#link}

As ações de link oferecem suporte ao controle de atributo de destino para gerenciar o comportamento do link. As seções a seguir estão disponíveis.

```json
{
  "actions": {
    "link": {
      "hideTarget": false,       // Show target attribute options (default)
      "shortcut": "Mod-K",       // Custom keyboard shortcut
      "label": "Insert Link"     // Custom button label
    },
    "unlink": {
      "shortcut": "Mod-Shift-K", // Custom keyboard shortcut
      "label": "Remove Link"     // Custom button label
    }
  }
}
```

#### Opções de configuração de link {#link-options}

* `hideTarget`: `false` (padrão) - Incluir atributo de destino em links, permitindo `_self`, `_blank`, etc.
* `hideTarget`: `true` - Excluir totalmente o atributo de destino dos links

A ação `unlink` aparece somente quando o cursor é posicionado dentro de um link existente. Ela remove a formatação do link, preservando o conteúdo do texto.

### Ações da imagem {#image}

As ações de imagem oferecem suporte ao empacotamento de elementos de imagem para gerar marcação de imagem responsiva. As seções a seguir estão disponíveis.

```json
{
  "actions": {
    "image": {
      "wrapInPicture": false,     // Use <img> tag (default)
      "shortcut": "Mod-Shift-I",  // Custom keyboard shortcut
      "label": "Insert Image"     // Custom button label
    }
  }
}
```

#### Opções de configuração de imagem {#image-options}

* `wrapInPicture`: `false` (padrão) - Gerar elementos `<img>` simples
* `wrapInPicture`: `true` - Encapsular imagens em `<picture>` elementos para design responsivo

### Configuração de recuo {#indentation}

O recuo tem uma configuração de nível de recurso que controla o escopo do comportamento de recuo, além de configurações de ação individuais para atalhos e rótulos.

```json
{
  "actions": {
    // Feature-level configuration
    "indentation": {
      "scope": "all"  // Controls what content can be indented (default: "all")
    },

    // Individual action configurations
    "indent": {
      "shortcut": "Tab",           // Custom keyboard shortcut
      "label": "Increase Indent"   // Custom button label
    },
    "outdent": {
      "shortcut": "Shift-Tab",     // Custom keyboard shortcut
      "label": "Decrease Indent"   // Custom button label
    }
  }
}
```

#### Opções de Escopo de Recuo {#indentation-options}

* `scope`: `all` (padrão) - O recuo/recuo à esquerda se aplica a todo o conteúdo:
   * Listas: aninhar/aninhar itens de lista
   * Parágrafos e cabeçalhos: aumentar/diminuir o nível de recuo geral
* `scope`: `lists` - O recuo/recuo à esquerda se aplica somente aos itens da lista:
   * Listas: aninhar/aninhar itens de lista
   * Parágrafos e cabeçalhos: Nenhum recuo (botões desativados para esses)

>[!NOTE]
>
>O aninhamento de lista com as teclas Tab/Shift+Tab funciona independentemente das configurações gerais de recuo.

### Colar como texto {#paste-as-text}

A ação do editor `paste_text` habilita um fluxo de trabalho padrão de colagem como texto simples.

* **Atalho padrão:** Mod-Shift-v (Cmd+Shift+V no macOS, Ctrl+Shift+V no Windows/Linux)
* **Comportamento:** Cola de texto/sem formatação (a formatação de origem é ignorada)
   * Em listas, novas linhas criam novos itens de lista.

```json
{
  "toolbar": {
    "editor": ["removeformat", "paste_text"]
  },
  "actions": {
    "paste_text": {
      "shortcut": "Mod-Shift-v",
      "label": "Paste as Text"
    }
  }
}
```

### Outras ações {#other}

Todas as outras ações oferecem suporte à personalização básica. As seções a seguir estão disponíveis.

```json
{
  "actions": {
    "h1": {
      "shortcut": "Mod-Alt-1",
      "label": "Large Heading"
    },
    "paragraph": {
      "shortcut": "Mod-Alt-0",
      "label": "Normal Text"
    },
    "link": {
      "shortcut": "Mod-K",
      "label": "Insert Link",
      "hideTarget": false    // Show target attribute options (default: false)
    }
  }
}
```

## Exemplo completo {#example}

Veja a seguir um exemplo de uma configuração completa.

```json
[
  {
    "id": "richtext",
    "rte": {
      // Configure which tools appear in toolbar
      "toolbar": {
        "format": [
          "bold",
          "italic"
        ],
        "blocks": [
          "paragraph",
          "h1",
          "h2"
        ],
        "list": [
          "bullet_list",
          "ordered_list"
        ],
        "insert": [
          "link",
          "unlink"
        ],
        "sections": [
          "format",
          "blocks",
          "list",
          "insert"
        ]
      },
      // Customize individual action behavior
      "actions": {
        // Format actions with HTML tag choices
        "bold": {
          "tag": "strong",
          "shortcut": "Mod-B",
          "label": "Bold"
        },
        "italic": {
          "tag": "em",
          "shortcut": "Mod-I"
        },
        // List actions with content wrapping
        "bullet_list": {
          "wrapInParagraphs": true,
          "label": "Bullet List"
        },
        "ordered_list": {
          "wrapInParagraphs": false
        },
        // Link actions with target control
        "link": {
          "hideTarget": false,
          "shortcut": "Mod-K",
          "label": "Add Link"
        },
        "unlink": {
          "label": "Remove Link"
        },
        // Other actions with basic customization
        "h1": {
          "shortcut": "Mod-Alt-1",
          "label": "Main Heading"
        }
      }
    }
  }
]
```

## Detalhes da opção de ação {#action-details}

Várias opções têm detalhes adicionais que são importantes para ter em mente.

### `wrapInParagraphs` {#wrapInParagraphs}

A opção `wrapInParagraphs` para listas controla a estrutura do HTML.

#### `wrapInParagraphs: false` (default) {#wrapInParagraphs-false}

```html
<ul>
  <li>Simple text content</li>
  <li>Another item</li>
</ul>
```

#### `wrapInParagraphs: true` {#wrapInParagraphs-true}

```html
<ul>
  <li><p>Text wrapped in paragraphs</p></li>
  <li><p>Supports rich formatting within items</p></li>
</ul>
```

Use o `wrapInParagraphs: true` quando precisar:

* Formatação avançada nos itens da lista
* Vários parágrafos por item de lista
* Estilo consistente em nível de bloco

### `wrapInPicture`{#wrapinpicture}

A opção `wrapInPicture` para imagens controla a estrutura HTML gerada para o conteúdo da imagem.

#### wrapInPicture: falso (padrão) {#wrapinpicture-false}

```html
<img src="image.jpg" alt="Description" />
```

#### wrapInPicture: verdadeiro {#wrapinpicture-true}

```html
<picture>
  <img src="image.jpg" alt="Description" />
</picture>
```

Use o `wrapInPicture: true` quando precisar:

* Suporte de imagem responsiva com `<source>` elementos.
* Recursos de direção de arte.
* À prova de obsolescência para recursos de imagem avançados.
* Estrutura de elemento de imagem consistente.

>[!NOTE]
>
>Quando o `wrapInPicture: true` está habilitado, as imagens podem ser aprimoradas com elementos `<source>` adicionais para diferentes consultas de mídia e formatos, tornando-as mais flexíveis para oferecer design responsivo.

### Opções de direcionamento de link {#link-target}

A opção `hideTarget` para links controla se o atributo `target` está incluído em links gerados e se a caixa de diálogo para criação de links inclui um campo para seleção de destino.

#### `hideTarget: false` (default) {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

#### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### Desativação de links em imagens {#disableforimages}

A opção `disableForImages` para links controla se os usuários podem criar links em imagens e elementos de imagem. Isso se aplica aos elementos `<img>` embutidos e aos elementos `<picture>` de nível de bloco.

#### `disableForImages: false` (default) {#disableforimages-false}

Os usuários podem selecionar imagens e envolvê-las em links.

```html
<!-- Inline image with link -->
<a href="https://example.com">
  <img src="image.jpg" alt="Description" />
</a>

<!-- Block-level picture with link -->
<a href="https://example.com">
  <picture>
    <img src="image.jpg" alt="Description" />
  </picture>
</a>
```

#### disableForImages: true {#disableforimages-true}

O botão de link é desativado quando uma imagem ou imagem é selecionada. Os usuários só podem criar links em conteúdo de texto.

```html
<!-- Images remain standalone without links -->
<img src="image.jpg" alt="Description" />

<picture>
  <img src="image.jpg" alt="Description" />
</picture>

<!-- Links work normally on text -->
<a href="https://example.com">Link text</a>
```

Use `disableForImages: true` quando quiser:

* Mantenha a consistência visual evitando imagens vinculadas.
* Simplifique a estrutura do conteúdo separando imagens da navegação.
* Imponha políticas de conteúdo que restrinjam a vinculação de imagens.
* Reduza a complexidade de acessibilidade em seu conteúdo.

>[!NOTE]
>
>Essa configuração afeta apenas a capacidade de criar novos links em imagens. Ela não remove links existentes de imagens no conteúdo.

### Opções de tag {#tag}

As ações de formato permitem alternar entre variantes do HTML.

| Ação | Tag padrão | Tags alternativas | Caso de uso |
|---|---|---|---|
| `bold` | `<strong>` | `<b>` | Ênfase semântica vs. visual |
| `italic` | `<em>` | `<i>` | Estilo semântico vs. visual |
| `strike` | `<del>` | `<s>` | Exclusão visual vs. semântica |

Escolha as marcas semânticas (`<strong>`, `<em>`, `<del>`) para melhor acessibilidade e SEO.

### Atalhos de teclado {#keyboard-shortcuts}

Os atalhos usam o formato `Mod-Key`(s) onde:

* `Mod` = `Cmd` no Mac, `Ctrl` no Windows/Linux
* Exemplos: `Mod-B`, `Mod-Shift-8`, `Mod-Alt-1`
