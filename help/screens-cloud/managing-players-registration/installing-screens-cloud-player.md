---
title: Instalação e configuração de players no Screens as a Cloud Service
description: Esta página descreve como instalar e configurar players no Screens as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 1%

---

# Instalação e configuração de players no Screens as a Cloud Service {#installing-players-screens-cloud}

Esta seção descreve como instalar reprodutores do AEM Screens que estão registrados em instâncias AEM locais. Além disso, você deve fazer uma redefinição de fábrica do reprodutor existente e, em seguida, registrar o novo reprodutor no AEM Screens as a Cloud Service.

## Objetivo {#objective}

Este documento ajuda você a entender como configurar seu reprodutor antes de registrá-lo. Depois de ler, você será capaz de entender o seguinte:

* de onde instalar os reprodutores
* como atualizar o reprodutor para o modo Nuvem

## Etapas para definir o reprodutor para o modo Nuvem {#cloud-mode-setup}

Depois de baixar o player mais recente de [Downloads do AEM Screens Player](https://download.macromedia.com/screens/), você está pronto para atualizar seu reprodutor para o modo Nuvem.

Siga as etapas abaixo para atualizar seu reprodutor:

1. Abra o AEM Screens player.

   >[!NOTE]
   >Você pode optar por testar com dispositivos de hardware dedicados ou com uma extensão da Web no seu próprio reprodutor.

1. Clique em **Configuração** e clique em **Para a fábrica** botão em **Redefinir** opção.

   ![imagem](/help/screens-cloud/assets/player/installplayer-2.png)

1. Clique em **Confirmar o** para redefinir seu reprodutor.

1. Novamente do **Configuração** e clique em **Alterar para o modo Nuvem** botão em **Alternar modo de execução** opção.

   ![imagem](/help/screens-cloud/assets/player/installplayer-1.png)

1. Clique em **Confirmar o** que avisa ao alternar para o modo de nuvem cancela o registro do reprodutor.

## Monitoramento básico de reprodução {#playback-monitoring}

O reprodutor relata várias métricas de reprodução com cada `ping` que o padrão é 30 segundos. Com base nessas métricas, o Adobe pode detectar vários casos de borda, como experiência travada, tela em branco e problemas de agendamento. Essa detecção nos permite compreender e solucionar problemas no dispositivo e, portanto, agiliza uma investigação e medidas corretivas com você.

O monitoramento básico da reprodução em um reprodutor AEM Screens permite:

* Monitorar remotamente se um player estiver reproduzindo conteúdo corretamente.

* Melhore a reatividade para telas em branco ou experiências com falha no campo.

* Diminui o risco de mostrar uma experiência quebrada ao usuário final.

### Noções básicas sobre propriedades {#understand-properties}

As seguintes propriedades estão incluídas em cada `ping`:

| Propriedade | Descrição |
|---|---|
| id {string} | o identificador do reprodutor |
| ativeChannel {string} | caminho de canal em execução no momento, ou nulo se nada estiver agendado |
| ativeElements {string} | string separada por vírgulas, elementos visíveis atualmente em todos os canais de sequência de reprodução (vários se houver um layout de várias zonas) |
| isDefaultContent {boolean} | true se o canal de reprodução for considerado um canal padrão ou de fallback (ou seja, tiver prioridade 1 e nenhum agendamento) |
| hasContentChanged {boolean} | true se o conteúdo foi alterado nos últimos 5 minutos; caso contrário, false |
| lastContentChange {string} | carimbo de data e hora da última alteração de conteúdo |

>[!NOTE]
>Como opção, você pode ativar uma propriedade mais avançada nas preferências do reprodutor (Ativar monitoramento de reprodução):
>|Propriedade|Descrição|
>|—|—|
>|isContentRendering {boolean}|true se a GPU puder confirmar que está reproduzindo o conteúdo real (com base na análise de pixels)|

### Limitações {#limitations}

Algumas limitações do monitoramento básico de reprodução estão listadas abaixo:

* O reprodutor relata seu próprio estado de reprodução ao servidor, portanto, requer uma conexão ativa.

* A variável `isContentRendering` propriedade que verifica se a GPU exige muitos recursos para ser habilitada por padrão e requer aceitação explícita das preferências do reprodutor. É recomendável não usá-lo com vídeos em produção.

* Esse recurso é compatível apenas com canais de sequência e ainda não abrange o caso de uso de canais interativos (SPA).

* As métricas ainda não estão totalmente expostas aos clientes; o Adobe está trabalhando para ativar, em breve, um mecanismo de geração de relatórios e alerta semelhante ao painel de controle.

## O que vem a seguir {#whats-next}

Agora que você instalou e configurou o reprodutor no modo Nuvem, continue sua jornada as a Cloud Service do Screens. Revisar o documento [Registro de players no Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) do provedor de serviços Screens.
