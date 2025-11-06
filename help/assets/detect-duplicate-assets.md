---
title: Detectar ativos duplicados de  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Saiba como detectar ativos duplicados
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management, Publishing,Collaboration, Asset Processing
role: User, Developer, Admin
exl-id: 40f63933-4f4e-4318-8d42-4b5c9b01f7cd
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 7%

---


# Detectar ativos duplicados {#detect-duplicate-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

Se um usuário do DAM carregar um ou mais ativos que já existem no repositório, [!DNL Experience Manager] detectará a duplicação e notificará o usuário. A detecção de duplicatas está desativada por padrão, pois pode ter impacto no desempenho, dependendo do tamanho do repositório e do número de ativos carregados.

Para ativar o recurso:

1. Navegue até **[!UICONTROL Ferramentas > Assets > Configurações do Assets]**.

1. Clique em **[!UICONTROL Detector de duplicação de ativos]**.

1. Na página [!UICONTROL Detector de duplicação de ativos], clique em **[!UICONTROL Habilitado]**.

   O valor `dam:sha1` do campo Detectar metadados garante que os ativos duplicados sejam detectados mesmo que os nomes de arquivo sejam diferentes.

1. Clique em **[!UICONTROL Salvar]**.

   ![Detector de duplicação de ativos](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Se você tiver configurado o Detector de Duplicação usando o arquivo de configuração `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` (configuração OSGi), poderá continuar a usá-lo. No entanto, a Adobe recomenda usar o novo método.


Depois de ativado, o Experience Manager envia notificações de ativos duplicados para a Caixa de entrada do Experience Manager. É um resultado agregado para várias duplicatas. Os usuários podem optar por remover os ativos com base nos resultados.

![Notificação da Caixa de entrada para ativos duplicados](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Ao fazer upload de ativos no repositório, o Experience Manager detecta a duplicação e notifica sobre os primeiros 100 ativos duplicados.
