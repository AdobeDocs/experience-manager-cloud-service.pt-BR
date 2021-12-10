---
title: Criação de ajuda no contexto para campos de formulário
seo-title: Authoring in-context help for form fields
description: O AEM Forms permite adicionar ajuda contextual aos campos e painéis do Formulário adaptável, como texto ou mídia avançada, incluindo vídeos.
seo-description: AEM Forms allows you to add in-context help to Adaptive Form fields and panels, as text or rich media, including videos.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 1%

---


# Criação de ajuda no contexto para campos de formulário{#authoring-in-context-help-for-form-fields}

## Introdução {#introduction}

Há situações em que os usuários finais que preenchem um formulário não têm certeza de como preencher os detalhes em um campo de formulário específico. Para solucionar esses problemas, o Adaptive Forms oferece suporte para adicionar texto ou ajuda rich in-context a um campo de formulário. Ajuda a melhorar a experiência de preenchimento do formulário e evita qualquer ambiguidade para os usuários finais.

Este artigo discute como os autores de formulários podem adicionar ajuda no contexto durante a criação do Adaptive Forms.

## Adicionar ajuda no contexto {#add-in-context-help}

Você pode especificar a ajuda no contexto usando as seguintes opções na seção Conteúdo da Ajuda da guia propriedades na barra lateral.

* [Descrição curta](authoring-in-field-help.md#p-short-description-p)
* [Descrição longa](authoring-in-field-help.md#p-long-description-p)

![Ajuda no contexto para campos de formulário](assets/descriptions.png)

>[!NOTE]
>
>Descrição longa substitui a Descrição curta. Se você especificou ambos, somente Descrição longa será exibida.

### Descrição curta {#short-description}

O campo Short description é destinado a fornecer dicas rápidas e curtas sobre o preenchimento de um campo de formulário. O texto especificado no campo Short description é exibido como uma dica de ferramenta ao passar o mouse sobre o campo.

![Descrição curta para adicionar ajuda no contexto para campos de formulário](assets/tooltip.png)

>[!NOTE]
>
>Selecionar **Sempre mostrar descrição curta** para exibir permanentemente o texto de ajuda abaixo do campo.

![Ajuda permanente curta no contexto abaixo do campo](assets/short1.png)

### Descrição longa {#long-description}

Você pode usar o campo Long description para especificar texto longo ou incorporar conteúdo de mídia avançada, incluindo vídeos, como ajuda de contexto. Por exemplo, a imagem a seguir mostra como você pode incorporar um vídeo como ajuda de contexto.

![Adicionar mídia avançada como ajuda no contexto para campos de formulário](assets/long-descriptions.png)

Adicionar descrição longa exibe uma **?** ícone ao lado do campo . Clicar no ícone exibe o conteúdo adicionado na seção de descrição longa.

![Exemplo de ajuda em contexto da mídia avançada](assets/photoshop.png)

### Ajuda no nível do painel {#panel-level-help}

Além da ajuda em contexto para campos de formulário, você pode especificar a ajuda em um nível de painel na guia Conteúdo da Ajuda da caixa de diálogo Editar painel.

![Adicionar ajuda no contexto para um painel de formulário](assets/panel-level-help.png)

A adição de ajuda para o painel exibe uma **?** ícone ao lado da descrição do painel. Clicar no ícone exibe o conteúdo adicionado na seção Conteúdo da Ajuda da caixa de diálogo de edição do painel.

![Exemplo de ajuda no contexto no nível do painel de formulário](assets/photoshop-1.png)

