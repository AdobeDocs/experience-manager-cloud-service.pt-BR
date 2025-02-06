---
title: Modelos para Criar Páginas Editáveis com o Editor Universal
description: Saiba como criar modelos que podem ser usados para criar páginas editáveis com o Universal Editor, economizando tempo e garantindo identidade visual consistente.
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: f0d60086-e92e-4492-ad50-bef84fed2a82
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 2%

---


# Modelos para Criar Páginas Editáveis com o Editor Universal {#page-templates}

Saiba como criar modelos que podem ser usados para criar páginas editáveis com o Universal Editor, economizando tempo e garantindo identidade visual consistente.

>[!NOTE]
>
>[Os modelos também estão disponíveis para criar páginas editáveis com o Editor de páginas](/help/sites-cloud/authoring/page-editor/templates.md).

## O que são modelos de página? {#what-are}

As diretrizes de marca e marketing geralmente ditam layouts específicos para suas páginas de conteúdo. Geralmente, também é uma realidade prática que muitas de suas páginas compartilharão a mesma estrutura e layout. Para economizar o tempo dos autores de conteúdo, as páginas podem ser criadas a partir de modelos.

Os modelos de página servem como cópias mestras dos layouts de página. Ao criar uma página a partir de um modelo, o conteúdo inicial do modelo é copiado para a nova página, ajudando a predefinir o layout básico e o conteúdo da página para o autor de conteúdo, economizando tempo.

## Ativação de modelos de página {#enabling-templates}

Para usar modelos para criar páginas editáveis com o Universal Editor, você deve ativar a opção.

Primeiro, ative modelos editáveis para a configuração do site.

1. Use o console **Sites** e [selecione a raiz do site](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources).
1. Depois que a raiz do site for selecionada, toque ou clique no ícone [**Propriedades**](/help/sites-cloud/authoring/sites-console/page-properties.md) na barra de ferramentas.
1. Na guia **Avançado** da caixa de diálogo de propriedades, anote o valor no campo **Configuração da Nuvem**.
1. Na navegação principal, escolha **Ferramentas** -> **Geral** -> **Navegador de Configuração**.
1. No **[Navegador de Configuração](/help/implementing/developing/introduction/configurations.md)**, selecione a configuração anotada na etapa anterior e toque ou clique em **Propriedades** na barra de ferramentas.
1. Na janela **Propriedades de Configuração**, marque a opção **Modelos Editáveis**.
1. Toque ou clique em **Salvar e fechar**.

Quando a configuração estiver ativada, você deve permitir modelos para o site.

1. Use o console **Sites** e [selecione a raiz do site](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources).
1. Depois que a raiz do site for selecionada, toque ou clique no ícone [**Propriedades**](/help/sites-cloud/authoring/sites-console/page-properties.md) na barra de ferramentas.
1. Na guia **Avançado** da caixa de diálogo de propriedades na seção **Configurações de Modelo**, toque ou clique no botão **Adicionar**.
1. No novo campo vazio que aparece em **Modelos permitidos**, adicione o caminho `/conf/<site>/settings/wcm/templates/.*`.
1. Toque ou clique em **Salvar e fechar**.

Agora você pode usar modelos para criar páginas para o seu site. Esta tarefa só deve ser feita uma vez em cada site/configuração em que você deseja usar modelos ao criar páginas editáveis com o Editor universal.

## Criação de um novo modelo {#create-new}

Você pode [criar uma nova página](/help/sites-cloud/authoring/sites-console/creating-pages.md) para servir como modelo ou usar uma página existente como base de um modelo.

1. Use o console **Sites** para [navegar até a página nova ou existente](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) que deseja usar como modelo e toque ou clique nela para selecioná-la.

1. Depois que a página for selecionada, toque ou clique no ícone [**Propriedades**](/help/sites-cloud/authoring/sites-console/page-properties.md) na barra de ferramentas.

1. Na guia **Avançado** da caixa de diálogo de propriedades na seção **Configurações de Modelo**, selecione o alternador **Usar Página como Modelo**.

1. Toque ou clique em **Salvar e fechar**.

Sua nova página agora pode ser usada como modelo ao criar novas páginas.

## Criar uma página a partir de um modelo {#creating-from-template}

A criação de uma página a partir de um modelo que é editável com o Editor Universal tem o mesmo fluxo de trabalho que [a criação de qualquer outra página](/help/sites-cloud/authoring/sites-console/creating-pages.md).

1. Use o console **Sites** para [navegar até o local](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) onde deseja criar a nova página.

1. Toque ou clique em **Criar** -> **Página**.

1. Na guia **Modelo** do assistente **Criar página**, você pode selecionar em qual modelo deseja basear sua nova página. Toque ou clique no modelo desejado para selecioná-lo e, em seguida, toque ou clique em **Avançar**.

Conclua o assistente como faria para qualquer outra página e crie sua nova página com base no modelo selecionado.

## Páginas e modelos {#pages-vs-templates}

Os modelos de página definem apenas o conteúdo inicial das páginas. As páginas são totalmente editáveis com o Universal Editor.

* As páginas criadas a partir de modelos de páginas são cópias independentes do modelo.
* Se o modelo for alterado, as páginas existentes baseadas nesse modelo não serão alteradas.
* O autor de conteúdo pode modificar e atualizar o conteúdo da página resultante conforme necessário, sem restrições do modelo.

## Modelos editáveis {#editable-templates}

As páginas criadas com o [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md) também podem ser baseadas em modelos. Os modelos usados para criar páginas para o Editor Universal e o Editor de Páginas usam os [modelos editáveis](/help/implementing/developing/components/templates.md) do AEM.

Os modelos usados para criar páginas editáveis com o Editor de páginas usam todos os recursos dos modelos editáveis. Os modelos usados para criar páginas editáveis com o Editor universal usam somente o recurso de conteúdo inicial.
