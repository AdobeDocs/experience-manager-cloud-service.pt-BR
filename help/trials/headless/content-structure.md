---
title: Criar a estrutura de conteúdo do seu aplicativo
description: Saiba como criar a estrutura que serve como base para todo o seu conteúdo headless usando os modelos de fragmento de conteúdo do AEM.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: 6464b90e607d3de87d103c744b8e7c0ba9ed2178
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 93%

---


# Criar a estrutura de conteúdo do seu aplicativo {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Criar a estrutura de conteúdo para seu aplicativo"
>abstract="Ao acompanhar essa série de guias interativos, você aprenderá a criar a estrutura (também conhecida como o modelo de fragmento de conteúdo) que serve como base para todo o seu conteúdo headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Iniciar o console de modelo"
>abstract="Vamos explorar como criar um esquema reutilizável, chamado de modelo de fragmento de conteúdo, para o seu conteúdo no Adobe Experience Manager as a Cloud Service. Assista ao vídeo para entender por que essa é uma etapa importante. <br><br>Inicie esse módulo em uma nova guia clicando no botão abaixo e, em seguida, siga este guia."
>additional-url="https://video.tv.adobe.com/v/3413261?captions=por_br" text="Vídeo de introdução à estrutura de conteúdo"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Parabéns. Você aprendeu a criar um modelo de fragmento de conteúdo para representar a estrutura dos seus dados headless e deu o primeiro passo para fornecer conteúdo omnicanal de maneira dimensionada e padrão."
>abstract=""

## Criar um modelo {#create-model}

O console do modelo de Fragmento de conteúdo é aberto em uma nova guia. Considere o console do modelo do Fragmento de conteúdo como a biblioteca de modelos, onde você cria novos modelos e gerencia os modelos existentes.

1. Clique no botão **Criar** na parte superior direita da tela para começar a criar um modelo de fragmento de conteúdo.

1. O assistente de criação de modelos é iniciado para orientar você. Forneça as informações obrigatórias.

   * **Título do modelo**: trata-se de uma breve descrição do modelo, que geralmente indica a sua finalidade.
   * **Ativar modelo**: essa opção está marcada por padrão e deve permanecer assim para que você possa criar fragmentos de conteúdo com base nesse modelo.

1. Depois que os campos obrigatórios forem preenchidos, clique em **Criar** no canto superior esquerdo para criar o modelo.

1. A caixa de diálogo de **Sucesso** confirmará que o modelo foi criado. Clique em **Abrir** na caixa de diálogo para abrir o novo modelo de fragmento de conteúdo no editor em uma nova guia. Em seguida, prossiga para a próxima etapa para adicionar campos de dados ao modelo.

![Etapas dois e três da criação de um modelo de fragmento de conteúdo](assets/do-not-localize/create-model-2-3.png)

## Adicionar campos ao modelo {#configure-model}

Antes de usar o modelo, é necessário definir a estrutura dos dados. O editor de modelos de fragmento de conteúdo é onde você configura os tipos de dados e as propriedades que definem o conteúdo do modelo.

1. Arraste um campo do painel **Tipos de dados** à direita do editor e solte-o no modelo de fragmento de conteúdo.

1. Depois que um tipo de dados for inserido, a coluna **Tipos de dados** será alterada automaticamente para a guia **Propriedades**, onde é possível definir os detalhes do tipo de dados que você acabou de inserir.

1. Depois de adicionar todos os campos necessários para o modelo de fragmento de conteúdo, clique em **Salvar** na parte superior direita da janela.

1. O modelo será salvo e você retornará ao console de modelos de fragmento de conteúdo.

![Etapas um, dois e três da adição de campos ao modelo](assets/do-not-localize/define-model-fields-1-2-3.png)
