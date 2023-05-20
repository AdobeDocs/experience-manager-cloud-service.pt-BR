---
title: Criar a estrutura de conteúdo do seu aplicativo
description: Saiba como usar modelos de Fragmento de conteúdo AEM para criar sua estrutura de conteúdo, que serve como base para seu conteúdo headless.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: ac94981e477e1fe8b883460ed9be009b4c1c088d
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 42%

---


# Criar a estrutura de conteúdo do seu aplicativo {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Criar a estrutura de conteúdo para seu aplicativo"
>abstract="Ao acompanhar essa série de guias interativos, você aprenderá a criar a estrutura (também conhecida como o modelo de fragmento de conteúdo) que serve como base para todo o seu conteúdo headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Iniciar o console de modelo"
>abstract="Vamos explorar como criar um esquema reutilizável, chamado de modelo de fragmento de conteúdo, para o seu conteúdo no Adobe Experience Manager as a Cloud Service. Assista ao vídeo para entender por que essa é uma etapa importante. <br><br>Neste módulo de aprendizagem, usaremos um site de viagem como exemplo e ensinaremos como criar um modelo que representa uma viagem.<br><br>Inicie esse módulo em uma nova guia clicando no botão abaixo e, em seguida, siga este guia."
>additional-url="https://video.tv.adobe.com/v/3413261?captions=por_br" text="Vídeo de introdução à estrutura de conteúdo"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Parabéns. Você aprendeu a criar um modelo de fragmento de conteúdo para representar a estrutura dos seus dados headless e deu o primeiro passo para fornecer conteúdo omnicanal de maneira dimensionada e padrão."
>abstract=""

## Criar um modelo {#create-model}

O console de modelos de fragmento de conteúdo é aberto em uma nova guia. Considere o console de modelos de fragmento de conteúdo como uma biblioteca de modelos, onde você cria novos modelos e gerencia os modelos existentes.

Para o nosso exemplo, criaremos um modelo que representa a estrutura de dados de uma viagem apresentada em um site de viagens. Nos referiremos a uma viagem usando esse modelo como um **Aventura**.

1. Clique no botão **Criar** na parte superior direita da tela para começar a criar um modelo de fragmento de conteúdo.

1. O assistente Criar modelo é iniciado, o que orienta você na criação do modelo. Forneça as informações obrigatórias.

   * **Título do modelo** - Este é um rótulo breve do modelo e geralmente indica a finalidade do modelo. Chamaremos nosso novo modelo de `Adventure`.
   * **Ativar modelo**: essa opção está marcada por padrão e deve permanecer assim para que você possa criar fragmentos de conteúdo com base nesse modelo.

1. Depois que os campos obrigatórios forem preenchidos, clique em **Criar** no canto superior esquerdo para criar o modelo.

1. A caixa de diálogo de **Sucesso** confirmará que o modelo foi criado. Clique em **Abrir** na caixa de diálogo para abrir o novo modelo de fragmento de conteúdo no editor em uma nova guia. Em seguida, prossiga para a próxima etapa para adicionar campos de dados ao modelo.

![Etapas dois e três da criação de um modelo de fragmento de conteúdo](assets/do-not-localize/create-model.png)

## Uso do Editor de modelos {#configure-model}

Agora temos um modelo chamado **Aventura**, mas não tem detalhes como duração, destino, atividades etc. Antes de usar o modelo, é necessário definir a estrutura dos dados.

O editor de modelos de fragmento de conteúdo é onde você configura os tipos de dados e as propriedades que definem o conteúdo do modelo.

>[!TIP]
>
>É importante seguir os esquemas de nomenclatura nas instruções a seguir, pois nos referiremos a esses nomes específicos em módulos posteriores.

1. Arraste um **Texto em linha única** do campo **Tipos de dados** à direita do editor e solte-o no modelo de Fragmento de conteúdo.

1. Depois que um tipo de dados for inserido, a coluna **Tipos de dados** será alterada automaticamente para a guia **Propriedades**, onde é possível definir os detalhes do tipo de dados que você acabou de inserir. Para este primeiro campo, queremos armazenar o título da viagem ou aventura. Insira as seguintes propriedades.

   * **Renderizar como:** **Campo de texto** - Quando você criar uma aventura, este campo armazenará o título da aventura.
   * **Rótulo do campo:** `Title` - Este é o rótulo exibido para este campo ao criar uma nova aventura.

1. Depois de definir as propriedades do campo, você pode voltar para a **Tipos de dados** no painel direito e adicione campos adicionais arrastando e soltando.

Dessa forma, você pode adicionar quantos campos forem necessários ao modelo para suportar qualquer tipo de estrutura de dados que precise. Os tipos de campos de dados variam, mas o processo de adicioná-los ao modelo permanece o mesmo.

Continue na próxima seção para adicionar os campos necessários para preencher e salvar a **Aventura** modelo

![Etapas um, dois e três da adição de campos ao modelo](assets/do-not-localize/define-model-fields.png)

## Adicionar campos ao modelo {#additional-fields}

Você já tem um campo para o título da aventura. Agora é necessário adicionar campos para capturar a descrição, o preço e uma imagem representativa da aventura.

>[!TIP]
>
>A variável **Aventura** modelo é baseado no site de amostra WKND para AEM. Você pode [visite o site aqui](https://wknd.site/us/en/adventures/yosemite-backpacking.html) para ver o conteúdo que usa o **Aventura** modelo.

Siga as mesmas etapas descritas acima para adicionar esses campos adicionais. A única diferença são as propriedades que você precisa definir.

1. Adicione um campo para armazenar a descrição da aventura arrastando e soltando uma **Texto multilinha** e insira as seguintes propriedades:

   * **Renderizar como:** **Área de texto** - Quando você criar uma aventura, este campo armazenará uma breve descrição da viagem.
   * **Rótulo do campo:** `Description` - Este é o rótulo exibido para este campo ao criar uma nova aventura.

1. Adicione um campo para armazenar o preço da aventura arrastando e soltando um **Texto em linha única** e insira as seguintes propriedades:

   * **Renderizar como:** **Campo de texto** - Quando você criar uma aventura, este campo armazenará o preço da viagem.
   * **Rótulo do campo:** `Price` - Este é o rótulo exibido para este campo ao criar uma nova aventura.

1. Adicione um campo para armazenar uma imagem que representa a viagem. As imagens no AEM são armazenadas como outro tipo de conteúdo chamado **Assets**. Portanto, para criar um campo para eles, é necessário arrastar e soltar um **Referência de conteúdo** que fará referência ao ativo da imagem.

   * **Renderizar como:** **Referência de conteúdo** - Ao criar uma aventura, esse campo apontará para o ativo de imagem que representa essa viagem.
   * **Rótulo do campo:** `Image` - Este é o rótulo exibido para este campo ao criar uma nova aventura.

1. Depois de adicionar todos os campos necessários para o modelo de fragmento de conteúdo, clique em **Salvar** na parte superior direita da janela.

1. O modelo será salvo e você retornará ao console de modelos de fragmento de conteúdo.
