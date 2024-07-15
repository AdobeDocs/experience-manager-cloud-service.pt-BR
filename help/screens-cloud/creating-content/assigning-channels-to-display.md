---
title: Atribuição de canal a uma exibição no Screens as a Cloud Service
description: Esta página descreve como atribuir um canal a uma exibição no Screens as a Cloud Service.
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---

# Atribuição de canal a uma exibição no Screens as a Cloud Service {#assign-channel-displays-screens-cloud}

Após a conclusão da configuração do projeto, é necessário atribuir o canal a uma exibição para exibir o conteúdo.

## Objetivo {#objective}

Este documento ajuda você a entender como atribuir um canal a uma exibição, quando a exibição estiver pronta e você tiver adicionado conteúdo ao canal e publicado. Depois de ler, você poderá entender como atribuir um canal a uma exibição do Provedor de serviços da Screens.

## Pré-requisitos {#prerequisites}

Antes de executar as etapas abaixo para atribuir um canal a uma exibição, é necessário que você tenha terminado de aprender:

* Criando e Gerenciando Exibições
* Criação e gerenciamento de canais

## Etapas para atribuir um canal a uma exibição {#assign-channel-to-display}

Siga as etapas abaixo para atribuir um canal a uma exibição:

1. Navegue até Provedor de Serviços da Screens e selecione **Exibições** no painel de navegação esquerdo.

1. Clique em **Atribuir canal** à exibição.

   ![imagem](/help/screens-cloud/assets/display/assignchannel-1.png)

1. Preencha os seguintes campos da caixa de diálogo **Atribuir um canal**.

   ![imagem](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. Selecione o nome do canal no menu suspenso.
   1. Escolha a prioridade.

      >[!NOTE]
      >A prioridade é usada para ordenar as atribuições caso várias correspondam aos critérios de reprodução. Aquele com o valor mais alto sempre tem prioridade sobre valores mais baixos. Por exemplo, se houver dois canais A e B. A tem uma prioridade 1 e B tem uma prioridade 2, então o canal B é exibido, pois tem uma prioridade mais alta que A.

   1. Selecione a data de início e a data de término em **Ativation**.

1. Clique em **+ Adicionar recorrência** para adicionar uma agenda de recorrência para seu canal.

   ![imagem](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >Você pode adicionar vários agendamentos recorrentes ao seu canal. Os cronogramas recorrentes introduzem o DayParting, que permite definir um cronograma global com vários canais em execução em horários específicos do dia e reutilizar o que está configurado para todas as exibições de uma só vez.

   É possível definir as seguintes opções:

   * **Nome**: título do cronograma recorrente.
   * **Repetir**: escolha se o agendamento é executado Diariamente, Semanalmente, Mensalmente ou Anualmente.
   * **Início**: a hora inicial da sua agenda.
   * **Fim**: a hora de término de seu cronograma. Você pode defini-lo por tempo ou duração.
   * **Hora**: a agenda termina em um horário especificado.
   * **Duração**: o agendamento é executado para uma duração de tempo específica em horas ou minutos.

1. Clique em **Criar**. Você pode ver que um canal é atribuído para essa exibição, como mostrado na figura abaixo.

   ![imagem](/help/screens-cloud/assets/display/assignchannel-3.png)


## O que vem a seguir {#whats-next}

Agora que você atribuiu o canal a uma exibição, deve continuar a as a Cloud Service jornada do Screens revisando o documento [Instalação e configuração do Screens Player para AEM as a Cloud Service](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md).
