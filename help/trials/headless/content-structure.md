---
title: Criar a estrutura de conteúdo do seu aplicativo
description: Saiba como usar os modelos de fragmento de conteúdo do AEM para criar sua estrutura de conteúdo, que serve como base para seu conteúdo headless.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
feature: Headless
role: Admin, User, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 98%

---


# Criar a estrutura de conteúdo do seu aplicativo {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Criar a estrutura de conteúdo para seu aplicativo"
>abstract="Ao acompanhar essa série de guias interativos, você aprenderá a criar uma estrutura (também conhecida como o modelo de Fragmento de conteúdo) que servirá como toda a base para o seu conteúdo headless."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Iniciar o console de modelo"
>abstract="Vamos explorar como criar um esquema reutilizável, chamado de modelo de fragmento de conteúdo, para o seu conteúdo no Adobe Experience Manager as a Cloud Service. Assista ao vídeo para entender por que essa etapa é importante. <br><br>Neste módulo de aprendizagem, você usará um site de viagem como exemplo e criará um modelo que representa uma viagem.<br><br>Inicie esse módulo em uma nova guia clicando no botão abaixo e, em seguida, siga este guia."
>additional-url="https://video.tv.adobe.com/v/3413261?captions=por_br" text="Vídeo de introdução à estrutura de conteúdo"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Parabéns. Você aprendeu a criar um modelo de fragmento de conteúdo para representar a estrutura dos seus dados headless e deu o primeiro passo para fornecer conteúdo omnicanal de maneira dimensionada e padrão."
>abstract=""

## Criar um modelo {#create-model}

O console de modelos de fragmento de conteúdo é aberto em uma nova guia. Considere o console do modelo de fragmento de conteúdo como sua biblioteca de modelos, onde você cria e gerencia modelos.

No exemplo, você cria um modelo que representa a estrutura de dados de uma viagem que é apresentada em um site de viagens. Uma viagem que usa esse modelo é chamada de **Aventura**.

1. No canto superior direito da tela, clique em **Criar** para começar a criar um modelo de fragmento de conteúdo.

1. O assistente Criar modelo o orienta na criação do modelo. Forneça as informações obrigatórias.

   * **Título do modelo**: uma breve descrição do modelo, que geralmente indica sua finalidade. Você pode chamar o novo modelo de `Adventure`.
   * **Habilitar modelo**: essa opção está marcada por padrão e deve permanecer assim para que você possa criar fragmentos de conteúdo com base nesse modelo.

1. Depois que os campos obrigatórios forem preenchidos, clique em **Criar** no canto superior direito para criar o modelo.

1. A caixa de diálogo **Sucesso** confirma que o modelo foi criado. Clique em **Abrir** na caixa de diálogo para abrir o novo modelo de fragmento de conteúdo no editor em uma nova guia. Em seguida, prossiga para a próxima etapa para adicionar campos de dados ao seu modelo.

![Etapas dois e três da criação de um modelo de fragmento de conteúdo](assets/do-not-localize/create-model.png)

## Usar o Editor de modelos {#configure-model}

Agora temos um modelo chamado **Aventura**, mas sem detalhes como duração, destino e atividades. Antes de poder usar o modelo, é necessário definir a estrutura dos dados.

O editor de modelos de fragmento de conteúdo é onde você configura os tipos de dados e as propriedades que definem o conteúdo do modelo.

>[!TIP]
>
>É importante seguir os esquemas de nomenclatura nas instruções a seguir, pois esses nomes específicos são mencionados nos módulos posteriores.

1. Arraste um campo **Texto em linha única** do painel **Tipos de dados** à direita do editor e solte-o no modelo de fragmento de conteúdo.

1. Depois que um tipo de dados é inserido, a coluna **Tipos de dados** muda automaticamente para a guia **Propriedades**, onde é possível definir os detalhes do tipo de dados inserido. Para esse primeiro campo, armazene o título da viagem ou aventura. Insira as seguintes propriedades.

   * **Renderizar como:** **Campo de texto** - Ao criar uma aventura, esse campo armazena o título da aventura.
   * **Rótulo do campo:** `Title` - O rótulo que é exibido para esse campo ao criar uma aventura.

1. Após definir as propriedades do campo, você pode voltar para a guia **Tipos de dados** no painel direito e arrastar e soltar outros campos.

Dessa forma, é possível adicionar quantos campos forem necessários ao seu modelo para dar suporte a qualquer estrutura de dados necessária. Os tipos de campos de dados variam, mas o processo de adicioná-los ao modelo permanece o mesmo.

Avance para a próxima seção e adicione os campos necessários para concluir e salvar o modelo **Aventura**

![Etapas um, dois e três da adição de campos ao modelo](assets/do-not-localize/define-model-fields.png)

## Adicionar campos ao modelo {#additional-fields}

Já existe um campo para o título da aventura. Agora é necessário adicionar campos para capturar a descrição, o preço e uma imagem representativa da aventura.

>[!TIP]
>
>O modelo **Aventura** é baseado no site de amostra do WKND para AEM. Você pode [visitar o site da WKND aqui](https://wknd.site/us/en/adventures/yosemite-backpacking.html) para ver o conteúdo que usa o modelo **Adventure**.

Siga as mesmas etapas descritas acima para acrescentar esses campos adicionais. A única diferença são as propriedades que devem ser definidas.

1. Adicione um campo para armazenar a descrição da aventura arrastando e soltando um campo **Texto de várias linhas** e insira as seguintes propriedades:

   * **Renderizar como:** **Área de texto** - Ao criar uma aventura, esse campo armazena uma breve descrição da viagem.
   * **Rótulo do campo:** `Description` - O rótulo que é exibido para esse campo ao criar uma aventura.

1. Adicione um campo para armazenar o preço da aventura arrastando e soltando um campo **Texto de linha única** e insira as seguintes propriedades:

   * **Renderizar como:** **Campo de texto** - Ao criar uma aventura, esse campo armazena o preço da viagem.
   * **Rótulo do campo:** `Price` - O rótulo que é exibido para esse campo ao criar uma aventura.

1. Adicione um campo para armazenar uma imagem que represente a viagem. As imagens no AEM são armazenadas como outro tipo de conteúdo chamado **Ativos**. Para criar um campo para eles, arraste e solte um campo **Referência de conteúdo** que faz referência ao ativo da imagem.

   * **Renderizar como:** **Referência de conteúdo** - Ao criar uma aventura, esse campo aponta para o ativo de imagem que representa essa viagem.
   * **Rótulo do campo:** `Image` - O rótulo que é exibido para esse campo ao criar uma aventura.
   * **Caminho raiz:** `/content/dam/aem-demo-assets/en` - especifica um caminho de ponto de partida ao navegar por ativos com o Seletor de ativos.

1. Após adicionar os campos necessários para o modelo de fragmento de conteúdo, clique em **Salvar** na parte superior direita da janela.

1. O modelo será salvo e você retornará ao console de modelos de fragmento de conteúdo.
