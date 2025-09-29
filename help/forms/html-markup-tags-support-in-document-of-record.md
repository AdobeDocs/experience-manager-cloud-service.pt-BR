---
title: Tags de marcação do HTML compatíveis no documento de registro
description: O guia de referência para tags de marcação do HTML agora é compatível com a geração de documentos de registro, incluindo considerações sobre acessibilidade e comportamento de renderização
feature: Adaptive Forms
role: Developer, User
exl-id: 8481b0dc-aae7-4bd2-acfe-1f1b6d747683
source-git-commit: 1794ed6cac612ee4600c2f8e1ced18c6130b64a2
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 7%

---


# Tags de marcação do HTML compatíveis no documento de registro

## O que esta referência abrange?

O AEM Forms agora é compatível com tags de marcação do HTML em campos de rich text ao gerar PDFs do Documento de registro (DoR). Este guia explica quais tags de marcação do HTML você pode usar com segurança no Adaptive Forms e como elas são renderizadas nos documentos gerados.

Se você adicionar conteúdo de rich text (como formatação em negrito, listas ou links) aos formulários, é importante entender quais tags são compatíveis e quais podem ser as limitações. Essa referência ajuda a escolher as tags apropriadas para garantir que o conteúdo seja exibido corretamente e permaneça acessível no Documento de registro.

## Antes de começar

### Pré-requisitos

Familiarize-se com:

- Sintaxe básica de marcação do HTML
- [Fundamentos do documento de registro](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- Princípios de acessibilidade e diretrizes da WCAG
- Requisitos de acessibilidade do PDF
- Componentes de formulário adaptável que aceitam marcação HTML

### Considerações

O Documento de registro (DoR) pode ser um PDF com tags, o que ajuda a garantir a acessibilidade e a estrutura adequada para tecnologias assistivas. Para habilitar a saída do PDF marcada, [defina a propriedade XCI `config/present/pdf/tagged` como `true`](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Depois de gerar sua PDF, é importante verificar se as tags de acessibilidade foram aplicadas corretamente. Você pode usar o [Adobe Acrobat para verificar as marcas de acessibilidade](https://helpx.adobe.com/in/acrobat/using/create-verify-pdf-accessibility.html) e garantir que seu documento atenda aos padrões de acessibilidade.

### Novidades

O suporte a rich text no Documento de registro é um aprimoramento recente. Anteriormente, o conteúdo rich text aparecia como texto simples em documentos gerados. Esse novo recurso permite que o conteúdo formatado seja renderizado corretamente nas saídas do PDF.

## Referência de suporte a tags do HTML

### Tags totalmente compatíveis

Essas tags são totalmente compatíveis com a criação adequada de nós de acessibilidade:

| Tag do HTML | Descrição | Suporte ao documento de registro | Acessibilidade | Exemplo |
|----------|-------------|-------------|---------------|---------|
| `<p>` | Parágrafo | Sim | Totalmente suportado - Corrigir nó `<P>` | `<p>This is a paragraph.</p>` |
| `<br/>` | Quebra de linha | Sim | Totalmente suportado - no nó `<P>` | `<p>Line 1<br/>Line 2</p>` |
| `<b>` | Texto em Negrito | Sim | Totalmente suportado - no nó `<P>` | `<b>bold text</b>` |
| `<i>` | Texto em itálico | Sim | Totalmente suportado - no nó `<P>` | `<i>italic text</i>` |
| `<span>` | Contêiner genérico incorporado | Sim | em elementos de bloco | `<span>styled text</span>` |
| `<sub>` | Subscrito | Sim | Totalmente compatível - dentro de elementos de bloco | `H<sub>2</sub>O` |
| `<sup>` | Sobrescrito | Sim | Totalmente compatível - Dentro dos elementos de bloco | `E=mc<sup>2</sup>` |
| `<a>` | Hiperlink | Sim | Suporte limitado - precisa de aninhamento adequado | `<a href="url">link text</a>` |


#### Listar problema de acessibilidade

A renderização da lista atual cria `<P>` nós em vez da estrutura de lista adequada:

```
Current: <P>1. First item
Current: <P>2. Second item

Expected: <L>
Expected:   <LI>
Expected:     <LBL>1.
Expected:     <LBody>First item
```

### Tags não compatíveis

Essas tags não são compatíveis e não serão renderizadas corretamente:

| Tag do HTML | Descrição | Solução alternativa |
|----------|-------------|---------------------|
| `<h1>` - `<h6>` | Tags de cabeçalho | Usar marcas `<p>` estilizadas ou cabeçalhos em nível de design |
| `<img>` | Imagens | Usar campos de imagem separados ou modelos de design |
| `<code>` | Blocos de código | Usar fontes monospace com estilo `<span>` |
| `<blockquote>` | Cotações em bloco | Usar marcas `<p>` estilizadas com recuo |
| `<table>` | Tabelas | Usar componentes da tabela de formulários adaptáveis |

## Exemplos de código

### Formatação básica de texto

```html
<!--  Supported - renders correctly -->
<p>This paragraph contains <b>bold text</b> and <i>italic text</i>.</p>

<!--  Supported - combined formatting -->
<p>This text is <i><b>bold and italic</b></i>.</p>

<!--  Unsupported - headings don't work -->
<h1>This won't render as a heading</h1>
```

### Listas

```html
<!-- ⚠️ Partially supported - renders but not accessible -->
<ol>
  <li>First numbered item</li>
  <li>Second numbered item</li>
</ol>

<ul>
  <li>First bullet point</li>
  <li>Second bullet point</li>
</ul>
```

### Links

```html
<!--  Supported - but must be within block elements -->
<p>Visit our <a href="https://example.com">website</a> for more information.</p>

<!--  Incorrect - link not properly nested -->
<a href="https://example.com">Standalone link</a>
```

### Notação científica

```html
<!--  Supported - but limited accessibility -->
<p>Water formula: H<sub>2</sub>O</p>
<p>Einstein's equation: E=mc<sup>2</sup></p>
```

## Conteúdo relacionado


- [Gerar documento de registro para Formulários adaptáveis](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- [Gerar documento de registro dos Componentes principais](/help/forms/generate-document-of-record-core-components.md)
- [Documento de personalização do modelo de registro](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record)

