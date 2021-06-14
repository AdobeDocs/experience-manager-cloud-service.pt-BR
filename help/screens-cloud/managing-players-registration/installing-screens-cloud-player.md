---
title: Instalar players no Screens como um Cloud Service
description: Esta página descreve como instalar players no Screens como um Cloud Service.
hide: true
hidefromtoc: true
index: false
source-git-commit: c65eeaf74ddfd81d37eb7090b84c8bf6f876dc72
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 1%

---


# Instalar players no Screens como um Cloud Service {#installing-players-screens-cloud}

A seção abaixo descreve como instalar players do AEM Screens registrados em instâncias de AEM locais. Além disso, você deve fazer uma redefinição de fábrica do reprodutor existente e registrar o reprodutor novo no AEM Screens como um Cloud Service.

## Objetivo {#objective}

Este documento ajuda você a entender como configurar o reprodutor antes de registrar os reprodutores. Após a leitura, você deve entender:

* onde instalar os players
* como atualizar o reprodutor para o modo Cloud

## Etapas para definir o reprodutor para o modo de nuvem {#cloud-mode-setup}

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

## O que vem a seguir {#whats-next}

Agora, que você instalou seus players e configurou as configurações necessárias, deve continuar seu Screens como uma jornada de Cloud Service, revisando o documento **Criação do reprodutor do provedor de serviços do Screens** em seguida.