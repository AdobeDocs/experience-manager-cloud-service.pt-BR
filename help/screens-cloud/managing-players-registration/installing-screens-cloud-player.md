---
title: Instalação e configuração de players no Screens as a Cloud Service
description: Esta página descreve como instalar e configurar players no Screens as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: 3367977496d3edad0f6f1e27e98eac95c791e870
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# Instalação e configuração de players no Screens as a Cloud Service {#installing-players-screens-cloud}

Esta seção descreve como instalar players do AEM Screens registrados em instâncias de AEM locais. Além disso, você deve fazer uma redefinição de fábrica do reprodutor existente e registrar o novo reprodutor no AEM Screens as a Cloud Service.

## Objetivo {#objective}

Este documento ajuda você a entender como configurar o reprodutor antes de registrar os reprodutores. Após a leitura, você deve entender:

* onde instalar os players
* como atualizar o reprodutor para o modo Cloud

## Etapas para definir o reprodutor para o modo Nuvem {#cloud-mode-setup}

Depois de baixar o reprodutor mais recente de [Downloads do AEM Screens Player](https://download.macromedia.com/screens/), agora você está pronto para atualizar seu reprodutor para o modo Cloud.

Siga as etapas abaixo para atualizar o player:

1. Abra o reprodutor AEM Screens.

   >[!NOTE]
   >Você pode optar por testar com dispositivos de hardware dedicados ou com uma extensão da Web em seu próprio player.

1. Clique no botão **Configuração** e clique em **Para Fábrica** botão abaixo **Redefinir** opção.

   ![imagem](/help/screens-cloud/assets/player/installplayer-2.png)

1. Clique em **Confirmar** para redefinir o reprodutor.

1. Novamente na **Configuração** e clique em **Alterar para o modo Nuvem** botão abaixo **Alternar modo de execução** opção.

   ![imagem](/help/screens-cloud/assets/player/installplayer-1.png)

1. Clique em **Confirmar** que é solicitado ao alternar para o modo de nuvem, cancelará o registro do reprodutor.

## Monitoramento básico da reprodução {#playback-monitoring}

O reprodutor relata várias métricas de reprodução com cada `ping` que assume o padrão de 30 segundos. Com base nessas métricas, podemos detectar vários casos de borda, como experiência paralisada, tela em branco e problemas de agendamento. Isso nos permite entender e solucionar problemas no dispositivo e, portanto, acelerar uma investigação e medidas corretivas.

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

* O `isContentRendering` A propriedade que verifica a GPU atualmente usa muitos recursos para ser ativada por padrão e requer aceitação explícita das preferências do reprodutor. É recomendável não usá-lo juntamente com vídeos em produção.

* Esse recurso é compatível apenas para canais de sequência e ainda não cobre o caso de uso dos canais interativos (SPA).

* As métricas ainda não estão totalmente expostas aos nossos clientes, estamos trabalhando duro para ativar o mecanismo de relatório e alerta semelhante ao painel em um futuro próximo.

## O que vem a seguir {#whats-next}

Agora que você instalou e configurou o reprodutor para o modo Nuvem, deve continuar sua jornada as a Cloud Service do Screens ao próxima revisar o documento, [Registrando Players no Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) do Provedor de serviços do Screens.
