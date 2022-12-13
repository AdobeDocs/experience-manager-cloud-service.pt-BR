---
title: Criar a estrutura de conteúdo para seu aplicativo
description: Saiba como criar a estrutura que serve como base para todo o seu conteúdo sem periféricos usando modelos de Fragmento de conteúdo AEM.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: 6204830f30c28daba3ff87ba60acd0150847b523
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 1%

---

# Criar a estrutura de conteúdo para seu aplicativo {#content-structure}

Os fragmentos de conteúdo permitem projetar, criar, preparar e publicar conteúdo independente de página. Usando-os, você pode preparar um conteúdo pronto para uso em vários locais e em vários canais, ideal para entrega sem interface. Os modelos de Fragmento de conteúdo são usados para definir a estrutura desse conteúdo e são a primeira coisa que você precisa criar para gerenciar o conteúdo sem periféricos.

Para ajudá-lo a entender como isso é feito, esse módulo de Ensaios de AEM o orienta pelo processo com um tour interativo e rápido, criando primeiro o modelo e adicionando sua estrutura. O presente documento constitui um complemento da viagem no interior do produto, que abrange as mesmas etapas e vincula-se, se for caso disso, a recursos adicionais.

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_br_test"
>title="Iniciar o editor de modelo"
>abstract="A criação de um modelo de fragmento de conteúdo começa com a criação de um item de modelo no fluxo de trabalho de administração de modelo, em seguida, com a adição de elementos de estrutura a ele, usando o editor de modelo de fragmento de conteúdo.<br><br>Clique abaixo para iniciar o recurso em uma nova guia e siga este documento de aprendizagem para criar seu primeiro fragmento de conteúdo."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_newline_test"
>title="Iniciar o editor de modelo"
>abstract="A criação de um modelo de fragmento de conteúdo começa com a criação de um item de modelo no fluxo de trabalho de administração de modelo, em seguida, com a adição de elementos de estrutura a ele, usando o editor de modelo de fragmento de conteúdo.\n\nClique abaixo para iniciar o recurso em uma nova guia e siga este documento de aprendizagem para criar seu primeiro fragmento de conteúdo."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Criar a estrutura de conteúdo para seu aplicativo"
>abstract="Ao seguir nossa série de guias interativos, você aprenderá a criar a estrutura (também conhecida como o modelo de fragmento de conteúdo) que serve como base para todo o seu conteúdo sem periféricos."

## O console Modelo do Fragmento de conteúdo {#content-fragment-model-console}

Você inicia no console modelos do Fragmento de conteúdo . O console Modelos do Fragmento de conteúdo pode ser considerado como sua biblioteca de modelos. Use o console para criar novos modelos e gerenciar os modelos existentes. Seu console começa vazio, então vamos criar um novo modelo!

![O console do modelo de Fragmento de conteúdo](assets/content-structure/content-fragment-model-console.png)

Se você quiser navegar até o console do modelo de Fragmento de conteúdo fora da orientação no aplicativo, ele será encontrado usando o ícone Adobe no canto superior esquerdo da página. Isso abre a navegação global do AEM. Aqui, você escolhe o **Ferramentas** e depois **Geral** -> **Modelos de fragmentos do conteúdo**.

>[!TIP]
>
>Se você quiser saber mais sobre navegação no AEM, consulte o [Seção Recursos adicionais](#additional-resources) deste documento para obter mais informações sobre AEM manuseio básico.

## Criar um modelo {#create-model}

Quando estiver no console do modelo de Fragmento de conteúdo , você poderá criar um novo modelo para representar seu próprio conteúdo sem cabeçalho.

1. No console do modelo de Fragmento de conteúdo, clique no link **Criar** na parte superior direita da tela para começar a criar um modelo de Fragmento de conteúdo .

1. O assistente Criar modelo é iniciado, o que o orienta pela criação de um modelo de Fragmento de conteúdo.

   ![Assistente do modelo de Fragmento de conteúdo](assets/content-structure/model-wizard.png)

   Forneça as informações obrigatórias.

   * **Título do modelo** - Trata-se de uma breve descrição do modelo e indica normalmente a sua finalidade.
   * **Ativar modelo** - Essa opção é marcada por padrão e deve ser marcada para poder criar Fragmentos de conteúdo posteriormente com base nesse modelo.

   Você também pode optar por adicionar um maior **Descrição** ao modelo, bem como **Tags** para categorizá-lo e diferenciá-lo posteriormente para seus usuários no console modelo do Fragmento de conteúdo .

   >[!TIP]
   >
   >Se você estiver interessado em como as tags podem organizar seu conteúdo, consulte o [Seção Recursos adicionais](#additional-resources) deste documento para obter mais informações sobre marcação em AEM.

1. Depois que os campos obrigatórios forem preenchidos, clique em **Criar** no canto superior esquerdo para criar o modelo.

1. O **Sucesso** confirmará que o modelo foi criado.

   ![Caixa de diálogo de sucesso para criar um novo modelo de Fragmento de conteúdo](assets/content-structure/success.png)

1. Antes de usar o modelo, também é necessário definir a estrutura de seus dados. Clique em **Abrir** na caixa de diálogo para abri-la e continuar definindo o modelo.

## Adicionar campos ao modelo {#configure-model}

O modelo de Fragmento de conteúdo é essencialmente um esquema dos Fragmentos de conteúdo. Ou seja, define quais campos/tipos de dados o modelo contém.

![O editor de modelo de Fragmento de conteúdo](assets/content-structure/model-editor.png)

Usando o editor de modelo de Fragmento de conteúdo , é possível definir campos para o modelo de Fragmento de conteúdo usando uma interface de arrastar e soltar.

1. Arraste um campo do **Tipos de dados** painel à direita da tela e solte-o no modelo de Fragmento de conteúdo . Há vários tipos de dados para escolher, como um texto de linha única, texto de várias linhas, número e referências a outros fragmentos.

   ![Adicionar um tipo de dados](assets/content-structure/drop-fields.png)

   >[!TIP]
   >
   >Se quiser obter mais informações sobre os tipos de dados disponíveis, consulte [Seção Recursos adicionais](#additional-resources) deste documento para obter a documentação detalhada dos modelos de Fragmento de conteúdo .

1. Depois que um tipo de dados é colocado, a variável **Tipos de dados** alterada automaticamente para **Propriedades** , onde é possível definir os detalhes do tipo de dados que acabou de colocar.

   ![A guia Propriedades do campo de dados](assets/content-structure/data-type-properties.png)

   As propriedades do modelo podem incluir o nome do campo, o tipo de campo, o comprimento do campo, se for obrigatório, etc.

1. Use o **Propriedades** guia do tipo de dados selecionado para definir propriedades como valor padrão, comprimento máximo, se for um campo obrigatório, etc.

   >[!TIP]
   >
   >Se desejar mais informações sobre as propriedades disponíveis, consulte a [Seção Recursos adicionais](#additional-resources) deste documento para obter a documentação detalhada dos modelos de Fragmento de conteúdo .

1. Depois de adicionar todos os campos necessários para o modelo do Fragmento de conteúdo , clique em **Salvar** na parte superior direita da janela.

1. Isso salva o modelo e retorna ao console do modelo de Fragmento de conteúdo , onde é possível adicionar mais modelos necessários.

![Módulo concluído](assets/content-structure/content-fragment-model-console-populated.png)

## Você aprendeu a criar um modelo de fragmento de conteúdo {#conclusion}

Neste módulo, você aprendeu a criar um modelo de Fragmento de conteúdo para representar a estrutura de seus dados sem periféricos. Primeiro, você criou o modelo e o preencheu com tipos de dados e suas propriedades relacionadas, definindo um schema para seu conteúdo sem cabeçalho.

Agora que você tem seu próprio modelo de Fragmento de conteúdo , pode usar o modelo para criar Fragmentos de conteúdo. O módulo [Criar novo conteúdo](create-content.md) detalhes para usar o novo modelo de Fragmento de conteúdo para criar conteúdo sem cabeçalho.

Você pode retornar à sua tela inicial de avaliação clicando em **Soluções** botão na parte superior direita da barra de navegação e selecionando **Experience Manager**.

![Ir para casa](assets/content-structure/home.png)

## Recursos adicionais {#additional-resources}

Para obter mais informações sobre Fragmentos de conteúdo e AEM, considere revisar esta documentação adicional.

* [Manuseio básico](/help/sites-cloud/authoring/getting-started/basic-handling.md) - Documentação sobre como navegar e usar AEM para novos usuários
* [Uso de tags](/help/sites-cloud/authoring/features/tags.md) - Documentação sobre como usar tags no AEM para organizar o conteúdo
* [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) - Visão geral dos fragmentos de conteúdo e links para concluir a documentação sobre os fragmentos de conteúdo
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md) - Documentação completa sobre modelos de Fragmento de conteúdo
* [Modelos de fragmentos do conteúdo - Tipos de dados](/help/assets/content-fragments/content-fragments-models.md#data-types) - Detalhes sobre os vários tipos de dados disponíveis para modelos de Fragmento de conteúdo
* [Modelos de fragmentos do conteúdo - Propriedades](/help/assets/content-fragments/content-fragments-models.md#data-types) - Detalhes sobre as várias propriedades disponíveis para os tipos de dados de modelos de Fragmento de conteúdo
