---
title: Instalação e configuração de players no Screens as a Cloud Service
description: Esta página descreve como instalar e configurar players no Screens as a Cloud Service.
exl-id: a022738a-c543-4629-a244-f70fa294fe7f
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Instalação e configuração de players no Screens as a Cloud Service {#installing-players-screens-cloud}

Esta seção descreve como instalar reprodutores do AEM Screens que estão registrados em instâncias AEM locais. Além disso, você deve fazer uma redefinição de fábrica do reprodutor existente e, em seguida, registrar o novo reprodutor no AEM Screens as a Cloud Service.

## Objetivo {#objective}

Este documento ajuda você a entender como configurar seu reprodutor antes de registrá-lo. Depois de ler, você será capaz de entender o seguinte:

* de onde instalar os reprodutores
* como atualizar o reprodutor para o modo Nuvem

## Etapas para definir o reprodutor para o modo Nuvem {#cloud-mode-setup}

Depois de baixar o player mais recente em [Downloads do AEM Screens Player](https://download.macromedia.com/screens/), você estará pronto para atualizar seu player para o modo Nuvem.

Siga as etapas abaixo para atualizar seu reprodutor:

1. Abra o AEM Screens player.

   >[!NOTE]
   >Você pode optar por testar com dispositivos de hardware dedicados ou com uma extensão da Web no seu próprio reprodutor.

1. Clique na guia **Configuração** e clique no botão **Para Fábrica** na opção **Redefinir**.

   ![imagem](/help/screens-cloud/assets/player/installplayer-2.png)

1. Clique em **Confirmar** para redefinir o player.

1. Novamente na guia **Configuração** e clique no botão **Alterar para Modo de Nuvem** na opção **Alternar Modo de Execução**.

   ![imagem](/help/screens-cloud/assets/player/installplayer-1.png)

1. Clique em **Confirmar** que avisa ao alternar para o modo de nuvem para cancelar o registro do reprodutor.

## Monitoramento básico de reprodução {#playback-monitoring}

O player relata várias métricas de reprodução a cada `ping` que assume o padrão de 30 segundos. Com base nessas métricas, o Adobe pode detectar vários casos de borda, como experiência travada, tela em branco e problemas de agendamento. Essa detecção nos permite compreender e solucionar problemas no dispositivo e, portanto, agiliza uma investigação e medidas corretivas com você.

O monitoramento básico da reprodução em um reprodutor AEM Screens permite:

* Monitorar remotamente se um player estiver reproduzindo conteúdo corretamente.

* Melhore a reatividade para telas em branco ou experiências com falha no campo.

* Diminui o risco de mostrar uma experiência quebrada ao usuário.

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
>|isContentRendering {boolean}|true se a GPU puder confirmar que está reproduzindo conteúdo real (com base na análise de pixels)|

### Limitações {#limitations}

Algumas limitações do monitoramento básico de reprodução estão listadas abaixo:

* O reprodutor relata seu próprio estado de reprodução ao servidor, portanto, requer uma conexão ativa.

* A propriedade `isContentRendering` que verifica a GPU usa muitos recursos para ser habilitada por padrão e requer aceitação explícita das preferências do reprodutor. É recomendável não usá-lo com vídeos em produção.

* Esse recurso é compatível apenas com canais de sequência e ainda não abrange o caso de uso de canais interativos (SPA).

* As métricas ainda não estão totalmente expostas aos clientes; o Adobe está trabalhando para ativar, em breve, um mecanismo de geração de relatórios e alerta semelhante ao painel de controle.

## O que vem a seguir {#whats-next}

Agora que você instalou e configurou o reprodutor no modo Nuvem, continue a as a Cloud Service jornada do Screens. Consulte [Registrando players no Screens as a Cloud Service](/help/screens-cloud/managing-players-registration/registering-players-screens-cloud.md) do provedor de serviços da Screens.
