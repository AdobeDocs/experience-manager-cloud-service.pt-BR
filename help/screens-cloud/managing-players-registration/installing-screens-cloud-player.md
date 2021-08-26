---
title: Instalar e configurar players no Screens como um Cloud Service
description: Esta página descreve como instalar e configurar players no Screens como um Cloud Service.
source-git-commit: d5970e27773433c9e6e7175a103768ae591e87ba
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---


# Instalar e configurar players no Screens como um Cloud Service {#installing-players-screens-cloud}

Esta seção descreve como instalar players do AEM Screens registrados em instâncias de AEM locais. Além disso, você deve fazer uma redefinição de fábrica do reprodutor existente e registrar o novo reprodutor no AEM Screens como um Cloud Service.

## Objetivo {#objective}

Este documento ajuda você a entender como configurar o reprodutor antes de registrar os reprodutores. Após a leitura, você deve entender:

* onde instalar os players
* como atualizar o reprodutor para o modo Cloud

## Etapas para definir o reprodutor para o modo Nuvem {#cloud-mode-setup}

Depois de baixar o player mais recente em [Downloads do AEM Screens Player](https://download.macromedia.com/screens/), você está pronto para atualizar o player para o modo Cloud.

Siga as etapas abaixo para atualizar o player:

1. Abra o reprodutor AEM Screens.

   >[!NOTE]
   >Você pode optar por testar com dispositivos de hardware dedicados ou com uma extensão da Web em seu próprio player.

1. Clique na guia **Configuração** e clique no botão **Para fábrica** na opção **Redefinir**.

   ![imagem](/help/screens-cloud/assets/player/installplayer-2.png)

1. Clique em **Confirm** para redefinir o player.

1. Novamente na guia **Configuration** e clique no botão **Change to Cloud Mode** sob a opção **Toggle Runmode**.

   ![imagem](/help/screens-cloud/assets/player/installplayer-1.png)

1. Clique em **Confirm** que solicita que, ao alternar para o modo de nuvem, o registro do reprodutor seja cancelado.

## Monitoramento básico da reprodução {#playback-monitoring}

O reprodutor relata várias métricas de reprodução com cada `ping` padrão de 30 segundos. Com base nas métricas, você pode detectar vários casos de borda, como experiência paralisada, tela em branco e problemas de agendamento. Isso permite que você entenda e solucione problemas no dispositivo e, portanto, acelere uma investigação e medidas corretivas.

O monitoramento básico da reprodução em um reprodutor AEM Screens permite:

* Monitore remotamente, se um reprodutor estiver reproduzindo o conteúdo corretamente.

* Melhore a reatividade em telas em branco ou em experiências quebradas no campo .

* Diminui o risco de mostrar uma experiência quebrada para o usuário final.

### Como entender as propriedades {#understand-properties}

As seguintes propriedades estão incluídas em cada `ping`:

| Propriedade | Descrição |
|---|---|
| id {string} | o identificador do reprodutor |
| ativeChannel {string} | no momento, reproduzindo o caminho do canal, ou nulo se nada estiver agendado |
| ativeElements {string} | sequência separada por vírgulas, elementos atualmente visíveis em todos os canais de sequência de reprodução (vários no caso de um layout de várias zonas) |
| isDefaultContent {boolean} | true se o canal de reprodução for considerado um canal padrão ou de fallback (ou seja, tem prioridade 1 e sem agendamento) |
| hasContentChanged {boolean} | true se o conteúdo tiver sido alterado nos últimos 5 minutos; caso contrário, false |
| lastContentChange {string} | carimbo de data e hora da última alteração de conteúdo |

>[!NOTE]
>Como opção, uma propriedade mais avançada pode ser ativada nas preferências do reprodutor (Ativar monitoramento de reprodução), ou seja:
>|Propriedade|Descrição|
>|—|—|
>|isContentRendering {boolean}|true se a GPU puder confirmar que está reproduzindo conteúdo real (com base na análise de pixel)|

### Limitações           {#limitations}

Abaixo estão listadas algumas limitações do monitoramento básico da reprodução:

* O reprodutor relata seu próprio estado de reprodução no servidor para que ele exija uma conexão ativa.

* A propriedade `isContentRendering` que verifica a GPU atualmente consome muitos recursos para ser ativada por padrão e requer aceitação explícita das preferências do reprodutor. É recomendável não usá-lo junto com os vídeos.

* Esse recurso é compatível com canais de sequência.

## O que vem a seguir {#whats-next}

Agora, que você instalou e configurou o reprodutor para o modo Nuvem, você deve continuar seu Screens como uma jornada de Cloud Service, revisando o documento [Registrando Players no Screens como um Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) do Provedor de serviços do Screens.
