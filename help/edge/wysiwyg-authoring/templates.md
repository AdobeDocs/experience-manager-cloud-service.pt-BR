---
title: Uso de modelos de página com o editor universal
description: Saiba como criar e usar modelos de página com o Universal Editor.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 773ce75975f4dcc2c5310422bcc377b487ebec25
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---


# Uso de modelos de página com o editor universal {#page-templates}

Saiba como criar e usar modelos de página com o Universal Editor.

>[!NOTE]
>
>Esse recurso estará disponível em uma versão futura do AEM as a Cloud Service.

## O que são modelos de página? {#what-are}

As diretrizes de marca e marketing geralmente ditam layouts específicos para suas páginas de conteúdo. Geralmente, também é uma realidade prática que muitas de suas páginas compartilharão a mesma estrutura e layout. Para economizar o tempo dos autores de conteúdo, as páginas podem ser criadas a partir de modelos.

Os modelos de página servem como cópias mestras dos layouts de página. Ao criar uma página a partir de um modelo, o conteúdo do modelo é copiado para a nova página, ajudando a predefinir o layout e o conteúdo inicial da página para o autor de conteúdo, economizando tempo.

## Criação de um modelo de página {#creating}

Você pode criar um modelo de página criando uma nova página ou usando uma página existente para servir como modelo. Em ambos os casos, use o Console [**Sites**.](/help/sites-cloud/authoring/sites-console/introduction.md)

### Criação de um novo modelo {#create-new}

1. Use o console **Sites** para navegar até o local onde deseja criar a nova página que servirá como modelo e [crie a página como faria com qualquer outra.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. Depois que a página for criada e você retornar ao console, selecione a página e toque ou clique no ícone [**Propriedades**](/help/sites-cloud/authoring/sites-console/page-properties.md) na barra de ferramentas.

1. Na guia **Avançado** da caixa de diálogo de propriedades na seção **Configurações de Modelo**, selecione o alternador **Usar como Modelo**.

1. No campo **Nome do Modelo**, forneça um nome descritivo.

   * Esse é o nome que mostrará a criação de novas páginas de conteúdo e você selecionará um modelo no qual basear a nova página.

1. Toque ou clique em **Salvar e fechar**.

Sua nova página agora pode ser usada como modelo ao criar novas páginas.

### Usando uma página existente como modelo {#existing-page}

1. Use o console **Sites** para [navegar até o local da página](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) que você deseja usar como modelo.

1. Selecione a página e toque ou clique no ícone [**Propriedades**](/help/sites-cloud/authoring/sites-console/page-properties.md), na barra de ferramentas.

1. Na guia **Avançado** da caixa de diálogo de propriedades na seção **Configurações de Modelo**, selecione o alternador **Usar como Modelo**.

1. No campo **Nome do Modelo**, forneça um nome descritivo.

   * Esse é o nome que mostrará a criação de novas páginas de conteúdo e você selecionará um modelo no qual basear a nova página.

1. Toque ou clique em **Salvar e fechar**.

A página selecionada agora pode ser usada como modelo ao criar novas páginas.

## Criar uma página a partir de um modelo {#creating-from-template}

A criação de uma página a partir de um modelo para uso com o Editor Universal é o mesmo fluxo de trabalho que ocorreria ao [criar a página como você faria com qualquer outra.](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. Use o console **Sites** para [navegar até o local](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) onde deseja criar a nova página.

1. Toque ou clique em **Criar** -> **Página**.

1. Na guia **Modelo** do assistente **Criar página**, você pode selecionar em qual modelo deseja basear sua nova página. Toque ou clique no modelo desejado para selecioná-lo e, em seguida, toque ou clique em **Avançar**.

Conclua o assistente como faria para qualquer outra página e crie sua nova página com base no modelo selecionado.

## Editor universal e o editor de páginas {#page-vs-universal}

Os modelos de página para o Editor Universal resolvem o mesmo problema que [modelos de página para o Editor de Páginas AEM:](/help/sites-cloud/authoring/page-editor/templates.md) para poder reutilizar o conteúdo e criar páginas rapidamente com base em um conjunto de layouts predefinidos. No entanto, eles resolvem o problema de maneiras muito diferentes. Se você for um usuário do Editor de páginas, esteja ciente dessas diferenças.

* As páginas criadas a partir de modelos de páginas para o Universal Editor são cópias independentes do modelo.
* Portanto, se o modelo for alterado, as páginas resultantes não serão alteradas.
* O autor de conteúdo pode modificar e atualizar o conteúdo da página resultante conforme necessário, sem restrições do modelo.
