---
title: Criação de representações de vídeo no as a Cloud Service Screens
description: Esta página descreve como criar representações de vídeo no Screens as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Criação de representações de vídeo no as a Cloud Service Screens {#creating-screens-video-renditions}

## Introdução {#introduction}

Esta seção descreve como criar representações de vídeo usadas em players do Screens.

>[!IMPORTANT]
>As etapas destacadas nesta seção devem ser configuradas, se você estiver planejando usar vídeos nos canais do Screens.

## Etapas para criar representações de vídeo no as a Cloud Service do Screens {#steps-creating-screens-video-renditions}

Siga as etapas abaixo para criar representações de vídeo no Screens as a Cloud Service do Provedor de conteúdo do Screens:

1. Navegue até seu canal no Provedor de conteúdo do Screens.

   >[!NOTE]
   >Consulte [Uso do provedor de conteúdo do Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) para obter mais detalhes.

1. Clique na seção Ferramentas na barra de navegação esquerda e clique em **Ativos** e clique em **Processando perfis**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Clique em **Criar** para criar um novo perfil de processamento.

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Insira o **Nome**, como **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Navegar para **Vídeo** para adicionar uma codificação de vídeo e clique em **Adicionar novo**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Insira o **Nome da codificação** como , **screens-fullhd** e **Taxa de bits** as **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Certifique-se de usar o nome Codificação que começa com &quot;screens-&quot;. Somente essas representações de vídeo serão consideradas para reproduzir a experiência de vídeo no Screens as a Cloud Service. Insira a taxa de bits que funciona em seus vídeos (2500kbps para vídeo de 720px e 5000 kbps para 1080px).

   >[!NOTE]
   >Várias representações de vídeo podem ser adicionadas com largura/altura/taxa de bits variável para trabalhar com seus vídeos. Lembre-se de que todas as representações de tela serão baixadas pelos dispositivos do Screens, mesmo que o dispositivo reproduza apenas a representação de vídeo.

1. Clique em **Salvar**.

1. Selecione o Perfil de processamento e clique em **Aplicar perfil às pastas**.

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Selecione as pastas onde os vídeos do Screens são mantidos e clique em **Aplicar**.

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* Você pode criar vários perfis de processamento e aplicá-los às pastas correspondentes, para que os vídeos nessas pastas obtenham as representações de vídeo específicas.
   >* Ao fazer o upload de qualquer vídeo para a pasta na qual o Perfil de processamento é aplicado, os vídeos são processados e as representações configuradas são criadas, que são mais usadas pelos dispositivos Screens para reproduzir os vídeos.

