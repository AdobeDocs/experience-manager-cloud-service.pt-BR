---
title: Criação de representações de vídeo no Screens as a Cloud Service
description: Esta página descreve como criar representações de vídeo no Screens as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: cf1e2717342ca4e00780428d6ccf264bd8eca371
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Criação de representações de vídeo no Screens as a Cloud Service {#creating-screens-video-renditions}

## Introdução {#introduction}

Esta seção descreve como criar representações de vídeo usadas em reprodutores do Screens.

>[!IMPORTANT]
>As etapas destacadas nesta seção devem ser configuradas se você estiver planejando usar vídeos nos canais do Screens.

## Etapas para criar representações de vídeo no Screens as a Cloud Service {#steps-creating-screens-video-renditions}

Siga as etapas abaixo para criar representações de vídeo no Screens as a Cloud Service do provedor de conteúdo do Screens:

1. Navegue até o canal no Provedor de conteúdo do Screens.

   >[!NOTE]
   >Consulte [Utilização do provedor de conteúdo do Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) para obter mais detalhes.

1. Clique na seção Ferramentas na barra de navegação esquerda e clique em **Assets** e clique em **Processamento de perfis**.

   ![Clique em Processar perfis](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Clique em **Criar** para criar um novo perfil de processamento.

   ![Clique em Criar](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Insira o **Nome**, como **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Navegue até **Vídeo** para adicionar uma codificação de vídeo e clique em **Adicionar novo**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Insira o **Nome da codificação** como , **screens-fullhd** e a variável **Taxa de bits** as **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Use o nome Codificação que começa com &quot;telas-&quot;; somente essas representações de vídeo são consideradas para reproduzir a experiência de vídeo no Screens as a Cloud Service. Insira a taxa de bits que funciona em seus vídeos (2500 kbps para vídeo de 720 px e 5000 kbps para 1080 px).

   >[!NOTE]
   >Várias representações de vídeo podem ser adicionadas com variação de largura/altura/taxa de bits para que seus vídeos funcionem. Todas as telas e representações são baixadas pelos dispositivos do Screens, mesmo que o dispositivo reproduza apenas a representação de vídeo.

1. Clique em **Salvar**.

1. Selecione o perfil de Processamento e clique em **Aplicar perfil às pastas**.

   ![Aplicar perfil à pasta](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Selecione as pastas onde os vídeos do Screens são mantidos e clique em **Aplicar**.

   ![Clique em Aplicar](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* É possível criar vários perfis de processamento e aplicá-los às pastas correspondentes, para que os vídeos dessas pastas obtenham as representações de vídeo específicas.
   >* Ao fazer upload de qualquer vídeo para a pasta na qual o perfil de processamento é aplicado, os vídeos são processados e as representações configuradas são criadas, que são usadas ainda mais pelos dispositivos do Screens para reproduzir os vídeos.
