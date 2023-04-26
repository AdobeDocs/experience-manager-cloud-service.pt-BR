---
title: Criar a estrutura de conteúdo do seu aplicativo
description: Saiba como usar AEM modelos de Fragmento de conteúdo para criar sua estrutura de conteúdo, que serve como base para seu conteúdo sem periféricos.
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: 7134951a588eae3ee0c7c11abea17a34eac21474
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 37%

---


# Criar a estrutura de conteúdo do seu aplicativo {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="Criar a estrutura de conteúdo para seu aplicativo"
>abstract="Ao seguir esta série de guias interativos, você aprenderá a criar uma estrutura (conhecida como modelo de Fragmento de conteúdo) que serve como a estrutura fundamental para seu conteúdo sem periféricos."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="Iniciar o console de modelo"
>abstract="Vamos explorar como criar um esquema reutilizável, chamado de modelo de fragmento de conteúdo, para o seu conteúdo no Adobe Experience Manager as a Cloud Service. Assista ao vídeo para entender por que essa é uma etapa importante. <br><br>Neste módulo de aprendizagem, usaremos um site de viagem como nosso exemplo e percorremos criando um modelo que representa uma viagem. Vamos consultar esse modelo em módulos posteriores, portanto, siga o esquema de nomenclatura fornecido.<br><br>Inicie esse módulo em uma nova guia clicando no botão abaixo e, em seguida, siga este guia."
>additional-url="https://video.tv.adobe.com/v/3413261?captions=por_br" text="Vídeo de introdução à estrutura de conteúdo"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="Parabéns. Você aprendeu a criar um modelo de fragmento de conteúdo para representar a estrutura dos seus dados headless e deu o primeiro passo para fornecer conteúdo omnicanal de maneira dimensionada e padrão."
>abstract=""

## Criar um modelo {#create-model}

O console de modelos de fragmento de conteúdo é aberto em uma nova guia. Considere o console de modelos de fragmento de conteúdo como uma biblioteca de modelos, onde você cria novos modelos e gerencia os modelos existentes.

Para nosso exemplo, criaremos um modelo que representa a estrutura de dados de uma viagem que está em um site de viagens. Faremos referência a uma viagem nesse modelo como uma **Aventura.**

1. Clique no botão **Criar** na parte superior direita da tela para começar a criar um modelo de fragmento de conteúdo.

1. O assistente Criar modelo é iniciado, o que o orienta pela criação do modelo. Forneça as informações obrigatórias.

   * **Título do modelo**: trata-se de uma breve descrição do modelo, que geralmente indica a sua finalidade. Chamaremos nosso novo modelo `Adventure`.
   * **Ativar modelo**: essa opção está marcada por padrão e deve permanecer assim para que você possa criar fragmentos de conteúdo com base nesse modelo.

1. Depois que os campos obrigatórios forem preenchidos, clique em **Criar** no canto superior esquerdo para criar o modelo.

1. A caixa de diálogo de **Sucesso** confirmará que o modelo foi criado. Clique em **Abrir** na caixa de diálogo para abrir o novo modelo de fragmento de conteúdo no editor em uma nova guia. Em seguida, prossiga para a próxima etapa para adicionar campos de dados ao modelo.

![Etapas dois e três da criação de um modelo de fragmento de conteúdo](assets/do-not-localize/create-model.png)

## Uso do Editor de modelo {#configure-model}

Agora temos um modelo chamado **Aventura** para representar viagens em um site de viagens, mas não tem detalhes como duração, destino, atividades etc. Antes de usar o modelo, é necessário definir a estrutura dos dados.

O editor de modelos de fragmento de conteúdo é onde você configura os tipos de dados e as propriedades que definem o conteúdo do modelo.

>[!TIP]
>
>Adicionaremos alguns campos importantes para a **Aventura**. Em módulos posteriores, usaremos e adicionaremos ao modelo, portanto, siga o esquema de nomenclatura conforme fornecido.

1. Arraste um **Texto de linha única** do campo **Tipos de dados** painel à direita do editor e solte-o no modelo de Fragmento de conteúdo .

1. Depois que um tipo de dados for inserido, a coluna **Tipos de dados** será alterada automaticamente para a guia **Propriedades**, onde é possível definir os detalhes do tipo de dados que você acabou de inserir. Para este primeiro campo, queremos armazenar o título da viagem ou aventura. Insira as seguintes propriedades.

   * **Renderizar como:** **Campo de texto** - Ao criar uma aventura, esse campo armazenará o título da aventura.
   * **Rótulo do campo:** `Title` - Esse é o rótulo exibido para esse campo ao criar uma nova aventura.

1. Depois de definir as propriedades do campo, você pode alternar de volta para a variável **Tipos de dados** no painel direito e adicione campos adicionais arrastando e soltando.

Dessa forma, você pode adicionar quantos campos forem necessários ao seu modelo para suportar qualquer tipo de estrutura de dados necessária. Os tipos de campos de dados variam, mas o processo de adicioná-los ao modelo permanece o mesmo.

Prossiga para a próxima seção para adicionar os campos necessários para concluir e salvar o **Aventura** modelo

![Etapas um, dois e três da adição de campos ao modelo](assets/do-not-localize/define-model-fields.png)

## Adicionar campos ao modelo {#additional-fields}

Você já tem um campo para o título da aventura. Agora, é necessário adicionar campos para capturar a descrição, o preço e uma imagem representativa da viagem.

>[!TIP]
>
>O **Aventura** O modelo é baseado no site de amostra WKND para AEM. Você pode [visite o site aqui](https://wknd.site/us/en/adventures/yosemite-backpacking.html) para saber mais sobre isso, se desejar, mas o conhecimento sobre isso não é necessário para esses módulos de aprendizagem.

Siga as mesmas etapas descritas acima para adicionar esses campos adicionais. A única diferença são as propriedades que você precisa definir.

1. Adicione um campo para armazenar a descrição da aventura, arrastando e soltando um **Texto de várias linhas** e insira as seguintes propriedades:

   * **Renderizar como:** **Área de texto** - Ao criar uma aventura, esse campo armazenará uma breve descrição da viagem.
   * **Rótulo do campo:** `Description` - Esse é o rótulo exibido para esse campo ao criar uma nova aventura.

1. Adicione um campo para armazenar o preço da aventura, arrastando e soltando um **Texto de linha única** e insira as seguintes propriedades:

   * **Renderizar como:** **Campo de texto** - Ao criar uma aventura, esse campo armazenará o preço da viagem.
   * **Rótulo do campo:** `Price` - Esse é o rótulo exibido para esse campo ao criar uma nova aventura.

1. Adicione um campo para armazenar uma imagem que represente a viagem. As imagens em AEM são armazenadas como outro tipo de conteúdo chamado **Ativos**. Assim, para criar um campo para eles, você precisa arrastar e soltar um **Referência de conteúdo** que referenciará o ativo da imagem.

   * **Renderizar como:** **Referência de conteúdo** - Ao criar uma aventura, esse campo apontará para o ativo de imagem que representa essa viagem.
   * **Rótulo do campo:** `Image` - Esse é o rótulo exibido para esse campo ao criar uma nova aventura.

1. Depois de adicionar todos os campos necessários para o modelo de fragmento de conteúdo, clique em **Salvar** na parte superior direita da janela.

1. O modelo será salvo e você retornará ao console de modelos de fragmento de conteúdo.
