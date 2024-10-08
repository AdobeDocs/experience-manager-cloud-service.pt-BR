---
title: Como adicionar texto de ajuda para campos do AEM Adaptive Forms?
description: O AEM Forms permite adicionar ajuda em contexto aos campos e painéis do Formulário adaptável, como texto ou mídia avançada, incluindo vídeos.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: d661f869f1264e4a2317692ab6fd22263c89e072
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# Criação da ajuda em contexto para campos de formulário{#authoring-in-context-help-for-form-fields}

## Introdução {#introduction}

Há situações em que os usuários finais que preenchem um formulário não têm certeza de como preencher detalhes em um campo de formulário específico. Para resolver esses problemas, o Adaptive Forms oferece suporte para adicionar texto ou ajuda rica em contexto a um campo de formulário. Isso ajuda a melhorar a experiência de preenchimento de formulário e evita qualquer ambiguidade para os usuários finais.

Este artigo discute como os autores de formulários podem adicionar ajuda em contexto ao criarem o Forms adaptável.

## Adicionar ajuda em contexto {#add-in-context-help}

Você pode especificar a ajuda em contexto usando as seguintes opções na seção Conteúdo da Ajuda da guia de propriedades na barra lateral.

* [Descrição curta](authoring-in-field-help.md#p-short-description-p)
* [Descrição longa](authoring-in-field-help.md#p-long-description-p)

![Ajuda em contexto para campos de formulário](assets/descriptions.png)

>[!NOTE]
>
>A descrição longa substitui a descrição curta. Se você tiver especificado ambos, somente a descrição Longa será exibida.

### Descrição curta {#short-description}

O campo Short description fornece dicas rápidas e curtas sobre o preenchimento de um campo de formulário. O texto especificado no campo Descrição curta é exibido como uma dica de ferramenta ao passar o mouse sobre o campo.

![Breve descrição para adicionar ajuda em contexto para campos de formulário](assets/tooltip.png)

>[!NOTE]
>
>Selecione **Sempre mostrar descrição curta** para exibir permanentemente o texto de ajuda abaixo do campo.

![Ajuda contextual curta permanente abaixo do campo](assets/short1.png)

### Descrição longa {#long-description}

Você pode usar o campo Descrição longa para especificar texto longo ou incorporar conteúdo de mídia avançada, incluindo vídeos, como ajuda no contexto. Por exemplo, a imagem a seguir mostra como é possível incorporar um vídeo como ajuda em contexto.

![Adicionando mídia avançada como ajuda em contexto para campos de formulário](assets/long-descriptions.png)

Adicionar descrição longa exibe um **?Ícone** ao lado do campo. Clicar no ícone exibe o conteúdo adicionado na seção de descrição longa.

![Exemplo de ajuda em contexto de mídia avançada](assets/photoshop.png)

### Ajuda no nível do painel {#panel-level-help}

Além da ajuda em contexto para campos de formulário, você pode especificar a ajuda em nível de painel na guia Conteúdo da ajuda da caixa de diálogo de edição do painel.

![Adicionando ajuda em contexto para um painel de formulário](assets/panel-level-help.png)

Adicionar ajuda para o painel exibe um **?Ícone** ao lado da descrição do painel. Clicar no ícone exibe o conteúdo adicionado na seção Conteúdo da ajuda da caixa de diálogo de edição do painel.

![Exemplo de ajuda em contexto no nível do painel do formulário](assets/photoshop-1.png)