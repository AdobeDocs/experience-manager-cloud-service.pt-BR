---
title: Criação e gerenciamento de canais no Screens as a Cloud Service
description: Esta página descreve como criar e gerenciar canais no Screens as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 1%

---

# Criação e gerenciamento de um canal no Screens as a Cloud Service {#creating-channels-screens-cloud}

Depois de criar um projeto do AEM Screens, você deve criar canais.
***Canais***, exiba uma sequência de conteúdo (imagens e vídeos), um site ou um aplicativo de página única.

## Objetivo {#objective}

Este documento ajuda você a entender a criação e o gerenciamento de canais para o seu projeto do AEM Screens no Provedor de conteúdo do Screens. Depois de ler, você deverá:

* entender como criar canais para o Provedor de conteúdo do Screens
* gerencie e edite o conteúdo em seus canais
* gerencie a atribuição e o agendamento de ativação para seus canais no [Provedor de Serviços Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=en)

## Etapas para criar um novo canal de sequência no Screens as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Pré-requisitos**
>Antes de iniciar esta seção do Guia, leia [Criação e Gerenciamento de Projetos no Screens as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Siga as etapas abaixo para criar um canal de sequência no Screens as a Cloud Service:

1. Navegue até Provedor de conteúdo do Screens.

1. Navegue até o projeto do AEM Screens, como *FirstDigitalExperience*.

1. Selecione a pasta **Canais** do seu projeto, como **FirstDigitalExperience** —> **Canais** e clique em **Criar** na barra de ações.

   ![channel-create1](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Selecione o modelo, como, **Canal de sequência** no assistente **Criar** e clique em **Avançar**.

   ![channel-create2](/help/screens-cloud/assets/create-content/channel-create2.png)

   >[!NOTE]
   > O assistente **Criar** fornece diferentes tipos de modelos ao criar um canal. Consulte [Modelos Disponíveis](#available-templates) no Assistente de Criação para obter mais detalhes.

1. Insira o nome do canal de sequência, como **LoopingChannelOne** e clique em **Criar**.

   ![channel-create3](/help/screens-cloud/assets/create-content/channel-create3.png)

   Você verá agora um **LoopingChannelOne** na pasta Canais do projeto AEM Screens.

   Depois de criar o canal, você pode adicionar conteúdo ao seu canal. Consulte [Adicionar conteúdo a um canal](#add-content) para saber como adicionar ativos (imagens/vídeos) ao seu canal.

## Gerenciamento de um canal {#managing-channels}

É possível editar, exibir propriedades e painel, copiar, visualizar e excluir um canal.

Navegue até o canal no seu projeto e selecione o canal, conforme mostrado na figura abaixo. Agora é possível selecionar as opções, como editar o canal, exibir propriedades, visualizar conteúdo, gerenciar publicação ou excluir o canal da barra de ações.

![channelprop1](/help/screens-cloud/assets/create-content/channelprop1.png)

### Adicionar conteúdo a um canal {#add-content}

Para adicionar ou editar conteúdo em um canal, siga as etapas abaixo:

1. Selecione o canal que deseja editar, conforme mostrado na figura abaixo. Clique em **Editar** no canto superior esquerdo da barra de ações para abrir o editor.

   ![editar-canal1](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. O editor permite adicionar ativos/componentes ao canal que você deseja publicar.

1. Arraste e solte os ativos do painel do lado esquerdo e adicione-os ao editor.

   ![editar-canal2](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Clique em **Visualizar** para visualizar o conteúdo do seu canal.
   >![edit-channelpreview](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Modelos disponíveis no Assistente de criação {#available-templates}

Os seguintes modelos estão disponíveis durante o uso do assistente de canal **Criar**:

| Modelos disponíveis | Descrição |
|--- |--- |
| Pasta de canais | Permite criar uma pasta para armazenar a coleção de canais. |
| Canal de sequência | Permite criar um canal que reproduz os componentes sequencialmente (um por um em uma apresentação de slides). |
| Canal de tela dividida em L à esquerda ou à direita | Permite que os autores de conteúdo visualizem diferentes tipos de ativos em zonas de tamanho adequado. |

## Usar detalhes de atribuição padrão para canais {#default-channels}

Esse recurso permite definir um agendamento de ativação padrão para um canal e usá-lo por padrão para cada atribuição de uma exibição. Isso fornece um método para que a complicada definição de agendamento não precise ser repetida.

1. Navegue até o [Provedor de Serviços da Screens](https://experience.adobe.com/screens).

### Criar detalhes de atribuição padrão para um canal {#create-default}

1. Navegue até a página de detalhes do canal que deseja configurar.
1. Localize o bloco **Detalhes da atribuição padrão** na página.

   ![imagem](/help/screens-cloud/assets/display/Assignment1.png)

1. Clique em **Definir detalhes padrão**.
1. Configure os detalhes da atribuição padrão, incluindo prioridade, datas de início e término e padrões de recorrência do canal, e clique em **Atribuir**.

   ![imagem](/help/screens-cloud/assets/display/Assignments2.png)

1. Observe que os detalhes da atribuição são mostrados no bloco **Detalhes da atribuição padrão**:

   ![imagem](/help/screens-cloud/assets/display/Assignments3.png)

Esse bloco exibe as seguintes informações:

* Prioridade padrão do canal na exibição.
* Datas de início e término da ativação quando o canal está agendado para reprodução.
* Visualização sintética da recorrência (por hora/dia/semana/mês/ano e nome dado a essa recorrência).

### Usar os detalhes de atribuição padrão ao atribuir a uma exibição {#default-display}

Os canais com detalhes de atribuição padrão podem ser atribuídos a exibições da mesma forma que os canais normais, com a opção adicionada de usar os detalhes de atribuição padrão em vez de definir manualmente os personalizados a cada vez.

1. Navegue até a página de detalhes de exibição à qual deseja atribuir o canal e clique em **Atribuir canal**.
como alternativa, selecione a exibição desejada na exibição [inventário](https://experience.adobe.com/screens/displays) e clique em **Atribuir canal**.
1. A caixa de diálogo de atribuição de canal é aberta.

   ![imagem](/help/screens-cloud/assets/display/Assignments4.png)

1. Selecione o canal desejado que tem os detalhes de atribuição padrão no seletor de canais.
1. Observe que a caixa de diálogo de atribuição de canal muda para permitir que você escolha os detalhes de atribuição padrão ou selecione detalhes personalizados:

   ![imagem](/help/screens-cloud/assets/display/Assignments5.png)

1. Clique em **Atribuir** para finalizar a atribuição ou clique em **Definir detalhes da atribuição personalizada** se preferir substituir os padrões por alguns outros valores no contexto dessa exibição específica.

   ![imagem](/help/screens-cloud/assets/display/Assignments6.png)

1. Observe que o bloco **Canais atribuídos** foi atualizado com a nova atribuição:

   ![imagem](/help/screens-cloud/assets/display/Assignments7.png)

1. Observe que os canais terão um ícone diferente dependendo se estiverem usando agendamentos personalizados (ícone de Relógio) ou herdando os detalhes padrão (ícone de Relógio mundial) e clicar neles mostrará os detalhes de agendamento.
1. Observe também que as ações disponíveis para cada tipo serão diferentes.

   ![imagem](/help/screens-cloud/assets/display/Assignments8.png)

**Observação:** uma atribuição de canal que usa os detalhes de atribuição padrão não será editável no contexto da exibição.

* Se você precisar alterá-la para uma atribuição personalizada, primeiro remova-a e depois adicione-a novamente usando a opção **Definir detalhes de atribuição personalizada**.
* Se precisar alterar as propriedades dos detalhes da atribuição padrão, faça isso diretamente na página de detalhes do canal.

### Remover detalhes de atribuição padrão de um canal {#remove-display}

1. Navegue até a página de detalhes do canal para o qual deseja remover os detalhes da atribuição padrão.
1. Localize o bloco **Detalhes da atribuição padrão** na página
1. Clique em **Remover padrão**.

   ![imagem](/help/screens-cloud/assets/display/Assignments9.png)

1. Uma caixa de diálogo de confirmação é exibida e os detalhes correspondem a uma das seguintes condições:
   O canal **a.** não é usado em nenhuma exibição.

   ![imagem](/help/screens-cloud/assets/display/Assignments10.png)

**b.** Canal usado em uma única exibição.

![imagem](/help/screens-cloud/assets/display/Assignment11.png)

**c.** Canal usado em várias exibições.

![imagem](/help/screens-cloud/assets/display/Assignments12.png)

1. Clique em *Remover* para validar a alteração.

**Observação:** a remoção dos detalhes de atribuição padrão de um canal removerá as atribuições correspondentes em todas as exibições que estavam usando esse canal.
Como consequência, isso pode resultar em telas em branco se não houver nenhum conteúdo alternativo a ser reproduzido nessas exibições.

## O que vem a seguir {#whats-next}

Agora, que você configurou um canal do AEM Screens em seu projeto, é necessário publicar seu canal. Consulte [Canais de publicação no Screens as a Cloud Service](manage-publish.md) antes de gerenciar seus players do Provedor de serviços da Screens.
