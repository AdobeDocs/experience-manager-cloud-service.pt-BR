---
title: Criação e gerenciamento de canais no as a Cloud Service do Screens
description: Esta página descreve como criar e gerenciar canais no Screens as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: afcee8019c9b59f3eb1fdcabd569272eeea76dab
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 4%

---

# Criação e gerenciamento de um canal no Screens as a Cloud Service {#creating-channels-screens-cloud}

Depois de criar um Projeto do AEM Screens, você deve criar canais.
***Canais***, exibir uma sequência de conteúdo (imagens e vídeos), um site ou um aplicativo de página única.

## Objetivo {#objective}

Este documento ajuda você a entender a criação e o gerenciamento de canais para seu projeto do AEM Screens no Provedor de conteúdo do Screens. Após a leitura, você deve:

* saiba como criar canais para o Provedor de conteúdo do Screens
* gerenciar e editar conteúdo em seus canais
* agendamento de ativação para seus canais

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

## Usar detalhes de atribuição padrão para canais {#default-channels}

Esse recurso permite definir um agendamento de ativação padrão para um canal e usá-lo por padrão para cada atribuição para uma exibição. Isso fornece um método para que a definição de agendamento complicada não precise ser repetida.

### Criar detalhes de atribuição padrão para um canal {#create-default}

1. Navegue até a página de detalhes do canal que deseja configurar.
1. Localize a variável **Detalhes da atribuição padrão** bloco na página.

   ![imagem](/help/screens-cloud/assets/display/Assignment1.png)

1. Clique em **Definir detalhes padrão**.
1. Configure os detalhes da atribuição padrão, incluindo prioridade, datas de início e término, bem como padrões de recorrência para o canal, e clique em **Atribuir**.

   ![imagem](/help/screens-cloud/assets/display/Assignments2.png)

1. Observe que os detalhes da atribuição são mostrados no **Detalhes da atribuição padrão** mosaico:

   ![imagem](/help/screens-cloud/assets/display/Assignments3.png)

Este bloco exibe as seguintes informações:
* Prioridade padrão do canal na exibição.
* Datas de início e término da ativação quando o canal é agendado para reprodução.
* Visualização sintética da recorrência (por hora/dia/semana/mês/ano, bem como nome dado à recorrência).

### Usar os detalhes da atribuição padrão ao atribuir a uma exibição {#default-display}

Os canais com detalhes de atribuição padrão podem ser atribuídos a exibições da mesma forma que os canais regulares, com a opção adicionada para aproveitar os detalhes de atribuição padrão em vez de definir manualmente os personalizados de cada vez.

1. Navegue até a página de detalhes de exibição à qual deseja atribuir o canal e clique no botão **Atribuir canal**.
como alternativa, selecione a exibição desejada na exibição de inventário e clique no botão **Atribuir canal**.
1. A caixa de diálogo Atribuição de canal é aberta.

   ![imagem](/help/screens-cloud/assets/display/Assignments4.png)

1. Selecione o canal desejado que tem os detalhes padrão da atribuição no seletor de canais.
1. Observe as alterações na caixa de diálogo de atribuição de canal para permitir que você escolha os detalhes padrão da atribuição ou selecione os personalizados:

   ![imagem](/help/screens-cloud/assets/display/Assignments5.png)

1. Clique em **Atribuir** para finalizar a atribuição ou clique em **Definir detalhes de atribuição personalizada** se preferir substituir os padrões por alguns outros valores no contexto dessa exibição específica.

   ![imagem](/help/screens-cloud/assets/display/Assignments6.png)

1. Observe que **Canais atribuídos** O bloco é atualizado com a nova atribuição:

   ![imagem](/help/screens-cloud/assets/display/Assignments7.png)

1. Observe que os canais terão um ícone diferente, dependendo se estiverem usando agendamentos personalizados (ícone de Relógio) ou herdando os detalhes padrão (ícone do relógio do Mundo), e clicar neles mostrará os detalhes do agendamento.
1. Observe também que as ações disponíveis para cada tipo serão diferentes.

   ![imagem](/help/screens-cloud/assets/display/Assignments8.png)

**Observação:** Uma atribuição de canal que aproveita os detalhes padrão da atribuição não será editável no contexto da exibição.

* Se precisar alterá-la para uma atribuição personalizada, primeiro será necessário removê-la e depois adicioná-la novamente usando a **Definir detalhes de atribuição personalizada** opção.
* Se precisar alterar as propriedades dos detalhes da atribuição padrão, será necessário fazer isso diretamente na página de detalhes do canal.

### Remover detalhes da atribuição padrão de um canal {#remove-display}

1. Navegue até a página de detalhes do canal que deseja remover os detalhes padrão da atribuição.
1. Localize a variável **Detalhes da atribuição padrão** bloco na página
1. Clique no botão **Remover padrão**.

   ![imagem](/help/screens-cloud/assets/display/Assignments9.png)

1. Uma caixa de diálogo de confirmação será exibida e os detalhes corresponderão a uma das seguintes condições:
   **a.** Canal não é usado em nenhuma exibição.

   ![imagem](/help/screens-cloud/assets/display/Assignments10.png)

**b.** Canal é usado em uma única exibição.

![imagem](/help/screens-cloud/assets/display/Assignment11.png)

**c.** O canal é usado em várias exibições.

![imagem](/help/screens-cloud/assets/display/Assignments12.png)

1. Clique no botão *Remover* para validar a alteração.

**Observação:** Remover os detalhes da atribuição padrão de um canal removerá as atribuições correspondentes em todas as exibições que estavam usando.
Como consequência, isso pode levar a telas em branco se não houver conteúdo alternativo para reproduzir nessas telas.

## O que vem a seguir {#whats-next}

Agora, que você configurou um canal do AEM Screens em seu projeto, é necessário publicar seu canal. Consulte [Canais de publicação no Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/manage-publish.html?lang=en) antes de gerenciar seus players no Provedor de serviços do Screens.
