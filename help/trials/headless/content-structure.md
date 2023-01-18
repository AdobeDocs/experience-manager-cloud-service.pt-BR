---
title: Criar a estrutura de conteúdo para seu aplicativo
description: Saiba como criar a estrutura que serve como base para todo o seu conteúdo sem periféricos usando modelos de Fragmento de conteúdo AEM.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Criar a estrutura de conteúdo para seu aplicativo {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Criar a estrutura de conteúdo para seu aplicativo"
>abstract="Ao seguir essa série de guias interativos, você aprenderá a criar uma estrutura (conhecida como modelo de Fragmento de conteúdo) que servirá de base para seu conteúdo sem periféricos."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Iniciar o console de modelo"
>abstract="Vamos explorar como criar um schema reutilizável, chamado de modelo de Fragmento de conteúdo, para seu conteúdo no Adobe Experience Manager as a Cloud Service. Assista ao vídeo para entender por que isso é um passo importante. <br><br>Inicie esse módulo em uma nova guia clicando no botão abaixo e depois siga este guia."
>additional-url="https://video.tv.adobe.com/v/3413261" text="Vídeo de introdução à estrutura de conteúdo"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Parabéns! Você aprendeu a criar um modelo de Fragmento de conteúdo para representar a estrutura de seus dados sem periféricos e deu o primeiro passo para fornecer conteúdo omnicanal de forma escalada e padrão."
>abstract=""

## Criar um modelo {#create-model}

Clicar no **Iniciar o console de modelo** acima abre o console Modelos de fragmento de conteúdo em uma nova guia.

![O console do modelo de Fragmento de conteúdo](assets/content-structure/content-fragment-model-console.png)

Considere o console do modelo de Fragmento de conteúdo como a biblioteca de modelos, onde você cria novos modelos e gerencia os modelos existentes. Seu console começa vazio, então vamos criar um novo modelo!

1. No console do modelo de Fragmento de conteúdo, clique no link **Criar** na parte superior direita da tela para começar a criar um modelo de Fragmento de conteúdo .

1. O assistente Criar modelo é iniciado, que o orienta.

   ![Assistente do modelo de Fragmento de conteúdo](assets/content-structure/model-wizard.png)

   Forneça as informações obrigatórias.

   * **Título do modelo** - Trata-se de uma breve descrição do modelo, que geralmente indica a finalidade do mesmo.
   * **Ativar modelo** - Essa opção é marcada por padrão e deve ser marcada para poder criar Fragmentos de conteúdo com base nesse modelo.

1. Depois que os campos obrigatórios forem preenchidos, clique em **Criar** no canto superior esquerdo para criar o modelo.

1. O **Sucesso** confirmará que o modelo foi criado.

   ![Caixa de diálogo de sucesso para criar um novo modelo de Fragmento de conteúdo](assets/content-structure/success.png)

## Adicionar campos ao modelo {#configure-model}

Antes de poder usar o modelo, é necessário definir a estrutura de seus dados.

1. Clique em **Abrir** no **Sucesso** na etapa anterior para abrir o novo modelo no editor de modelo de Fragmento de conteúdo , onde é possível definir os campos.

1. Arraste um campo do **Tipos de dados** painel à direita do editor e solte-o no modelo de Fragmento de conteúdo .

   ![Adicionar um tipo de dados](assets/content-structure/drop-fields.png)

1. Depois que um tipo de dados é colocado, a variável **Tipos de dados** alterada automaticamente para **Propriedades** , onde é possível definir os detalhes do tipo de dados que acabou de colocar.

   ![A guia Propriedades do campo de dados](assets/content-structure/data-type-properties.png)

1. Depois de adicionar todos os campos necessários para o modelo do Fragmento de conteúdo , clique em **Salvar** na parte superior direita da janela.

O modelo é salvo e você retorna ao console do modelo de Fragmento de conteúdo , onde é possível adicionar mais modelos, conforme necessário.

![Módulo concluído](assets/content-structure/content-fragment-model-console-populated.png)
