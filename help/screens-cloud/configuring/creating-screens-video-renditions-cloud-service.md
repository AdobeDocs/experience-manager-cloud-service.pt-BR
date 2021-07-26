---
title: Criação de representações de vídeo do Screens no Screens as a Cloud Service
description: Esta página descreve como criar Representações de vídeo do Screens no Screens como um Cloud Service.
source-git-commit: ec939ac6a91523a9ba64a555943eba8e6da071eb
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Criação de representações de vídeo do Screens no Screens as a Cloud Service {#creating-screens-video-renditions}

## Introdução {#introduction}

Este guia descreve como criar representações de vídeo usadas em players do Screens.

>[!IMPORTANT]
>As etapas destacadas nesta seção devem ser configuradas se você estiver planejando usar vídeos nos canais do Screens.

## Etapas para criar representações de vídeo do Screens no Screens como um Cloud Service {#steps-creating-screens-video-renditions}

1. Navegue até seu canal no Provedor de conteúdo do Screens.

   >[!NOTE]
   >Consulte [Uso do provedor de conteúdo do Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) para obter mais detalhes.

1. Clique na seção Ferramentas na barra de navegação esquerda, clique em **Ativos** e em **Perfis de processamento**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Clique em **Criar** para criar um novo perfil de processamento.

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Insira o **Name**, como **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Navegue até a guia **Vídeo** para adicionar uma codificação de vídeo e clique em **Adicionar Novo**.


   >[!IMPORTANT]
   >Certifique-se de usar o nome Codificação que começa com &quot;screens-&quot;. Somente essas representações de vídeo serão consideradas para reproduzir a experiência de vídeo no Screens as a Cloud Service. Insira a taxa de bits que se adapta aos seus vídeos (2500kbps para vídeo de 720px e 5000 kbps para 1080px)

   >[!NOTE]
   >Várias representações de vídeo podem ser adicionadas com largura/altura/taxa de bits variável para atender às suas necessidades, mas lembre-se de que todas as representações de tela serão baixadas pelos dispositivos do Screens, mesmo que a reprodução do dispositivo seja apenas a representação de vídeo.

1. Clique em Salvar

1. Selecione o Perfil de processamento e clique em &quot;Aplicar perfil às pastas&quot;

1. Selecione as pastas onde os vídeos do Screens são mantidos e clique em Aplicar

1. Você pode criar vários perfis de processamento e aplicá-los às pastas correspondentes, para que os vídeos nessas pastas obtenham as representações de vídeo específicas

1. Ao fazer o upload de qualquer vídeo para a pasta na qual o perfil de processamento é aplicado, os vídeos serão processados e as representações configuradas serão criadas, que serão usadas pelos dispositivos do Screens para reproduzir os vídeos.

