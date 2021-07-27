---
title: Criação de representações de vídeo do Screens no Screens as a Cloud Service
description: Esta página descreve como criar Representações de vídeo do Screens no Screens como um Cloud Service.
source-git-commit: 0badd4209b35b4c8cdfa765a08b5d9db749f52b5
workflow-type: tm+mt
source-wordcount: '333'
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

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Insira o **Encoding Name** como , **screens-fullhd** e o **Bitrate** como **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Certifique-se de usar o nome Codificação que começa com &quot;screens-&quot;. Somente essas representações de vídeo serão consideradas para reproduzir a experiência de vídeo no Screens como Cloud Service. Insira a taxa de bits que funciona em seus vídeos (2500kbps para vídeo de 720px e 5000 kbps para 1080px).

   >[!NOTE]
   >Várias representações de vídeo podem ser adicionadas com largura/altura/taxa de bits variável para trabalhar com seus vídeos. Lembre-se de que todas as representações de tela serão baixadas pelos dispositivos do Screens, mesmo que o dispositivo reproduza apenas a representação de vídeo.

1. Clique em **Salvar**.

1. Selecione o Perfil de processamento e clique em **Aplicar perfil à(s) pasta(s)**.

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Selecione as pastas onde os vídeos do Screens são mantidos e clique em **Aplicar**.

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* Você pode criar vários perfis de processamento e aplicá-los às pastas correspondentes, para que os vídeos nessas pastas obtenham as representações de vídeo específicas.
   >* Ao fazer o upload de qualquer vídeo para a pasta na qual o Perfil de processamento é aplicado, os vídeos são processados e as representações configuradas são criadas, que são mais usadas pelos dispositivos Screens para reproduzir os vídeos.


