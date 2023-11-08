---
title: Gerenciar ativos digitais
description: Saiba como detectar ativos duplicados
contentOwner: KK
mini-toc-levels: 3
feature: Asset Management,Publishing,Collaboration,Asset Processing
role: User,Architect,Admin
source-git-commit: bd0981b262f645653723f1b35d871808506d47ba
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 4%

---


# Detectar ativos duplicados {#detect-duplicate-assets}

Se um usuário do DAM carregar um ou mais ativos que já existem no repositório, [!DNL Experience Manager] O detecta a duplicação e notifica o usuário. A detecção de duplicatas está desativada por padrão, pois pode ter impacto no desempenho, dependendo do tamanho do repositório e do número de ativos carregados.

Para ativar o recurso:

1. Navegue até **[!UICONTROL Ferramentas > Ativos > Configurações de ativos]**.

1. Clique em **[!UICONTROL Detector de duplicação de ativo]**.

1. No [!UICONTROL Página do Detector de duplicação de ativos], clique em **[!UICONTROL Ativado]**.

   `dam:sha1` O valor do campo Detectar metadados garante que ativos duplicados sejam detectados mesmo se os nomes de arquivo forem diferentes.

1. Clique em **[!UICONTROL Salvar]**.

   ![Detector de duplicação de ativo](assets/asset-duplication-detector.png)

>[!NOTE]
>
>Se você configurou o Detector de duplicação usando `/apps/example/config.author/com.adobe.cq.assetcompute.impl.assetprocessor.AssetDuplicationDetector.cfg.json` arquivo de configuração (configuração OSGi), você pode continuar a usá-lo, no entanto, o Adobe recomenda o uso do novo método.


Depois de ativado, o Experience Manager envia notificações de ativos duplicados para a Caixa de entrada do Experience Manager. É um resultado agregado para várias duplicatas. Os usuários podem optar por remover os ativos com base nos resultados.

![Notificação da caixa de entrada para ativos duplicados](assets/duplicate-detect-inbox-notification.png)

>[!NOTE]
>
>Ao fazer upload de ativos no repositório, o Experience Manager detecta a duplicação e notifica sobre os primeiros 100 ativos duplicados.

