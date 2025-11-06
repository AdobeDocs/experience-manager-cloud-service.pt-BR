---
title: Saiba mais sobre criação de Modelos de fragmento de conteúdo no AEM
description: Saiba mais sobre os conceitos e os mecanismos de modelagem de conteúdo para seu Headless CMS usando Modelos de fragmentos de conteúdo.
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 61%

---

# Saiba mais sobre criação de Modelos de fragmento de conteúdo no AEM {#architect-headless-content-fragment-models}

## A história até agora {#story-so-far}

No início da [Jornada do autor de conteúdo do AEM Headless](overview.md), o artigo [Noções básicas da modelagem de conteúdo para headless com AEM](basics.md) abordou os conceitos básicos e a terminologia relevantes à criação para headless.

Este artigo se baseia nesses princípios para que você entenda como criar seus próprios modelos de fragmento de conteúdo para seu projeto do AEM Headless.

## Objetivo {#objective}

* **Público-alvo**: iniciante
* **Objetivo**: os conceitos e mecanismos de modelagem de conteúdo para o seu CMS headless usando Modelos de fragmentos de conteúdo.

## Criar Modelos de fragmentos do conteúdo {#creating-content-fragment-models}

Em seguida, os modelos de fragmentos de conteúdo podem ser criados e a estrutura definida.

1. No Console de fragmentos de conteúdo, selecione o painel para Modelos de fragmentos de conteúdo.

1. Navegue até a pasta apropriada à sua configuração ou subconfiguração.

1. Use **Criar** para abrir a caixa de diálogo **Novo modelo de fragmento de conteúdo**.

   ![Título e descrição](/help/sites-cloud/administering/content-fragments/assets/cf-managing-content-fragment-models-create.png)

1. Preencha os detalhes

1. Use **Criar** para salvar o modelo vazio ou **Criar e abrir**.

## Definição de Modelos de fragmentos de conteúdo {#defining-content-fragment-models}

Ao abrir um novo modelo pela primeira vez, você verá um espaço em branco grande (bastante) no meio, uma longa lista de **Tipos de Dados** à esquerda e **Propriedades** (vazias no início, como estão para o campo selecionado) à direita:

![Modelo vazio](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-empty-model.png)

Então, o que deve ser feito?

Você pode:

* Arraste um tipo de dados do painel esquerdo para o local necessário para um campo no painel central.
* Selecione o ícone + por um Tipo de dados para adicioná-lo à parte inferior da lista de campos.
* Selecione Adicionar no painel central e, em seguida, o tipo de dados necessário na lista suspensa resultante para adicionar um campo à parte inferior da lista.

Você já está definindo seu modelo!

Após adicionar um tipo de dados, você deve definir a variável **Propriedades** para esse campo. Essas propriedades dependem do tipo que está sendo usado. Por exemplo:

![Propriedades de dados](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-field-properties.png)

### Autores de conteúdo {#your-content-authors}

Autores(as) de conteúdo não veem os tipos de dados e propriedades reais usados para criar seus modelos. Isso significa que talvez seja necessário fornecer ajuda e informações sobre como eles preenchem campos específicos. Para obter informações básicas, use o Rótulo do campo e o Valor padrão, mas em casos mais complexos talvez seja necessário considerar a documentação específica do projeto.

>[!NOTE]
>
>Consulte Recursos adicionais - Modelos de fragmento de conteúdo.

## Gerenciamento de Modelos de fragmentos de conteúdo {#managing-content-fragment-models}

<!-- needs more details -->

O gerenciamento dos modelos de fragmentos de conteúdo envolve:

* Habilitá-los (ou desabilitá-los): isso os torna disponíveis para autores ao criar Fragmentos de conteúdo.
* Excluir — a exclusão é sempre necessária, mas você precisa estar ciente da exclusão de um modelo que já é usado para fragmentos de conteúdo; em particular, fragmentos que já foram publicados.

## Publicação {#publishing}

<!-- needs more details -->

Os modelos de fragmento de conteúdo precisam ser publicados quando/antes de qualquer fragmento de conteúdo dependente ser publicado.

>[!NOTE]
>
>Se um autor tentar publicar um fragmento de conteúdo cujo modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado com o fragmento.

Assim que um modelo é publicado, ele é *bloqueado* em um modo SOMENTE LEITURA no autor. Isso tem como objetivo impedir alterações que resultariam em erros nos esquemas e consultas existentes da GraphQL, especialmente no ambiente de publicação. É indicado no console por **Bloqueado**.

Quando o modelo está **Bloqueado** (no modo SOMENTE LEITURA ), é possível visualizar o conteúdo e a estrutura dos modelos, mas você não pode editá-los diretamente; embora seja possível gerenciar modelos **Bloqueados** a partir do console ou do editor de modelo.

## O que vem a seguir {#whats-next}

Agora que você aprendeu as noções básicas, o próximo passo é começar a criar seus próprios Modelos de fragmentos de conteúdo.

## Recursos adicionais {#additional-resources}

* [Conceitos de criação](/help/sites-cloud/authoring/author-publish.md)

* [Manuseio básico](/help/sites-cloud/authoring/basic-handling.md): esta página se baseia principalmente no console do **Sites**, mas muitos/a maioria dos recursos também são relevantes para navegar e executar ações em **Modelos de fragmentos de conteúdo** dentro do console **Geral**.

* [Trabalho com fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)

   * [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [Definição do Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

      * [Habilitar ou desabilitar um Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#enabling-disabling-a-content-fragment-model)

      * [Permitir Modelos de fragmentos de conteúdo na pasta de Ativos](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder)

      * [Exclusão de um Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#deleting-a-content-fragment-model)

      * [Publicação de um Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model)

      * [Desfazer a publicação de um Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#unpublishing-a-content-fragment-model)

      * [Modelos de fragmentos do conteúdo bloqueados](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#locked-content-fragment-models)

* Guias de introdução

   * [Criação de configuração headless de Modelos de fragmentos do conteúdo](/help/headless/setup/create-content-model.md)
