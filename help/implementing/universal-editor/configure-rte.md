---
title: Configuração do RTE para o Editor universal
description: Entenda como você pode configurar o editor de rich text (RTE) no Editor universal.
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: edcba16831a40bd03c1413b33794268b6466d822
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Configuração do RTE para o Editor universal {#configure-rte}

Entenda como você pode configurar o editor de rich text (RTE) no Editor universal.

## Visão geral {#overview}

O Editor universal fornece um editor de rich text (RTE) no local e no painel de propriedades para permitir que os autores apliquem alterações de formatação à medida que editam seu texto.

Este RTE é configurável com o uso de [filtros de componente.](/help/implementing/universal-editor/filtering.md) Este documento descreve quais opções de configuração estão disponíveis junto com exemplos.

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

### Opções de direcionamento de link {#link-target}

A opção `hideTarget` para links controla se o atributo `target` está incluído em links gerados e se a caixa de diálogo para criação de links inclui um campo para seleção de destino.

#### `hideTarget: false` (default) {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

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
