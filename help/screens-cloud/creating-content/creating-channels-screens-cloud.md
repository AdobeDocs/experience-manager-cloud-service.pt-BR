---
title: Criação e gerenciamento de canais no as a Cloud Service do Screens
description: Esta página descreve como criar e gerenciar canais no Screens as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 7%

---

# Criação e gerenciamento de um canal no Screens as a Cloud Service {#creating-channels-screens-cloud}

Depois de criar um Projeto do AEM Screens, você deve criar canais.
***Canais***, exibir uma sequência de conteúdo (imagens e vídeos), um site ou um aplicativo de página única.

## Objetivo {#objective}

Este documento ajuda você a entender a criação e o gerenciamento de canais para seu projeto do AEM Screens no Provedor de conteúdo do Screens. Após a leitura, você deve:

* saiba como criar canais para o Provedor de conteúdo do Screens
* gerenciar e editar conteúdo em seus canais

## Etapas para criar um novo canal de sequência no Screens as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Pré-requisitos**
>Antes de iniciar esta seção do Guia, reveja [Criação e gerenciamento de projetos no Screens as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Siga as etapas abaixo para criar um novo canal de sequência no Screens as a Cloud Service:

1. Navegue até o Provedor de conteúdo do Screens.

1. Navegue até o projeto do AEM Screens, como *FirstDigitalExperience*.

1. Selecione o **Canais** pasta do seu projeto, como **FirstDigitalExperience** —> **Canais** e clique em **Criar** na barra de ações.

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Selecione o modelo, como **Canal de sequência** do **Criar** e clique em **Próximo**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > O **Criar** O assistente fornece diferentes tipos de modelos ao criar um canal. Consulte a seção [Modelos disponíveis](#available-templates) no Assistente de criação para obter mais detalhes.

1. Insira o nome do canal de sequência, como **LoopingChannelOne** e clique em **Criar**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   Agora você verá um **LoopingChannelOne** na pasta Canais no projeto do AEM Screens.

   Depois de criar o canal, agora é possível adicionar conteúdo ao canal. Consulte [Adicionar conteúdo a um canal](#add-content) para saber como adicionar ativos (imagens/vídeos) ao seu canal.

## Gerenciamento de um canal {#managing-channels}

Você pode editar, exibir propriedades e o painel, copiar, visualizar e excluir um canal.

Navegue até o canal no seu projeto e selecione o canal , conforme mostrado na figura abaixo. Agora é possível selecionar as opções, como editar o canal, visualizar propriedades, visualizar conteúdo, gerenciar a publicação ou excluir o canal na barra de ações.

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### Adicionar conteúdo a um canal {#add-content}

Para adicionar ou editar conteúdo em um canal, siga as etapas abaixo:

1. Selecione o canal que deseja editar, conforme mostrado na figura abaixo. Clique em **Editar** no canto superior esquerdo da barra de ações para abrir o editor.

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. O editor permite adicionar ativos/componentes ao seu canal que você deseja publicar.

1. Arraste e solte os ativos do painel lateral esquerdo e adicione-os ao editor.

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Clique em **Visualizar** para visualizar o conteúdo do seu canal.
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Modelos disponíveis no Assistente de criação {#available-templates}

Os seguintes modelos estão disponíveis ao usar o **Criar** assistente de canal:

| Modelos disponíveis | Descrição |
|--- |--- |
| Pasta de canais | Permite criar uma pasta para armazenar uma coleção de canais. |
| Canal de sequência | Permite criar um canal que reproduz os componentes sequencialmente (um por um em uma apresentação de slides). |
| Canal de tela dividida da barra L esquerda ou direita | Permite que os autores de conteúdo visualizem diferentes tipos de ativos em zonas de tamanho apropriado. |


## O que vem a seguir {#whats-next}

Agora, que você configurou um canal do AEM Screens em seu projeto, é necessário publicar seu canal. Consulte [Canais de publicação no Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/manage-publish.html?lang=en) antes de gerenciar seus players no Provedor de serviços do Screens.
