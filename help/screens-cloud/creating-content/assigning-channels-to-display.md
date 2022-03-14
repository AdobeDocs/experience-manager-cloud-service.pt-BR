---
title: Atribuir canal a uma exibição no Screens as a Cloud Service
description: Esta página descreve como atribuir um canal a uma exibição no Screens as a Cloud Service.
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 19%

---

# Atribuir canal a uma exibição no Screens as a Cloud Service {#assign-channel-displays-screens-cloud}

Quando a configuração do projeto for concluída, você deverá atribuir o canal a uma exibição para visualizar o conteúdo.

## Objetivo {#objective}

Este documento ajuda você a entender como atribuir um canal a uma exibição, uma vez que a exibição esteja pronta e tenha adicionado conteúdo ao seu canal e publicado-o. Após a leitura, você deve ser capaz de entender como atribuir um canal a uma exibição do Provedor de serviços do Screens.

## Pré-requisitos {#prerequisites}

Antes de executar as etapas abaixo para atribuir um canal a uma exibição, é necessário concluir o aprendizado:

* Criação e gerenciamento de exibições
* Criação e gerenciamento de canais

## Etapas para atribuir um canal a uma exibição {#assign-channel-to-display}

Siga as etapas abaixo para atribuir um canal a uma exibição:

1. Navegue até o Provedor de serviços do Screens e selecione **Exibições** no painel de navegação esquerdo.

1. Clique em **Atribuir canal** para a exibição.

   ![imagem](/help/screens-cloud/assets/display/assignchannel-1.png)

1. Preencha os seguintes campos de **Atribuir um canal** caixa de diálogo.

   ![imagem](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. Selecione o nome do canal no menu suspenso .
   1. Escolha a prioridade .

      >[!NOTE]
      >A prioridade é usada para ordenar as atribuições, no caso de várias delas corresponderem aos critérios de reprodução. A atribuição com o valor mais alto sempre terá precedência sobre aquelas com valores mais baixos. Por exemplo, se houver dois canais, A e B, em que A tem uma prioridade de 1 e B tem uma prioridade de 2, o canal B será exibido, pois tem uma prioridade mais alta que A.
   1. Selecione a data inicial e a data final de **Ativation**.

1. Clique em **+ Adicionar recorrência** para adicionar um agendamento de recorrência ao seu canal.

   ![imagem](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >Você pode adicionar várias programações recorrentes ao seu canal. Os agendamentos de recorrência apresentam o DayParting, que permite definir um agendamento global com vários canais em execução em horários específicos do dia e reutilizar essa configuração para todas as suas exibições de uma só vez.

   Você pode definir as seguintes opções:

   * **Nome**: Título do seu agendamento de recorrência.
   * **Repetir**: Escolha se o agendamento é executado Diariamente, Semanalmente, Mensalmente ou Anualmente.
   * **Iniciar**: A hora de início da sua programação.
   * **End**: A hora de término da sua programação. Você pode defini-lo por tempo ou duração.
   * **Hora**: O agendamento terminará em um horário especificado.
   * **Duração**: O agendamento é executado por uma duração específica em horas ou minutos.

1. Clique em **Criar** e agora você verá que um canal é atribuído para essa exibição, como mostrado na figura abaixo.

   ![imagem](/help/screens-cloud/assets/display/assignchannel-3.png)


## O que vem a seguir {#whats-next}

Agora que você atribuiu o canal a uma exibição, deve continuar sua jornada as a Cloud Service do Screens ao próxima revisar o documento [Instalar e configurar o player do Screens para AEM as a Cloud Service](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
