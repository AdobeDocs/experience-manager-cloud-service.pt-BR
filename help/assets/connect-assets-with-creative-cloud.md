---
title: Conectar o AEM Assets à Creative Cloud
description: Saiba como configurar e conectar o AEM Assets à Creative Cloud. Conecte-se a um direito de Creative Cloud que é provisionado para uma organização IMS diferente para usar facilmente as integrações de Creative Cloud mais recentes no AEM Assets, incluindo Bibliotecas Expressas e Creative Cloud.
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
feature: Collaboration
role: User
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 75%

---

# Conectar o AEM Assets à Creative Cloud  {#cross-org-entitlements}

A Experience Manager Assets tem a capacidade de se conectar a um direito de Creative Cloud que é provisionado para uma organização IMS diferente para usar facilmente as integrações de Creative Cloud mais recentes na AEM Assets, incluindo as Bibliotecas Express e Creative Cloud.

Se seus produtos da Creative Cloud e o AEM Assets forem provisionados para organizações IMS separadas, você poderá se conectar a uma organização diferente da Creative Cloud para executar fluxos de trabalho integrados entre as duas soluções.

## Pré-requisitos {#prerequisites}

* Direitos de administração do Experience Manager Assets

* Direito ativo à Creative Cloud para a mesma ID de usuário usada na Creative Cloud e no Experience Manager. Os direitos a IDs pessoais e federadas que utilizam o mesmo endereço de email são tratados como IDs de usuário diferentes.

## Conectar-se a uma nova organização da Creative Cloud {#connect-to-creative-cloud-org}

Para se conectar a uma nova organização da Creative Cloud, execute as seguintes etapas:

1. Navegue até **[!UICONTROL Configurações]** >; **[!UICONTROL Creative Cloud]**.

1. Selecione a nova organização da Creative Cloud usando a lista suspensa **[!UICONTROL Selecionar nova ID de organização da Creative Cloud]**. A lista exibe todas as organizações às quais você tem acesso. Selecione a organização com direitos da Creative Cloud ativos.

1. Clique em **[!UICONTROL Alternar organizações]** para alterar para a nova organização.

   ![Direitos entre organizações](assets/cross-org-entitlements.png)

## Limitações {#limitations}

* Você pode conectar o AEM Assets a uma organização da Creative Cloud de cada vez. Não é possível conectar-se a várias organizações da Creative Cloud ao mesmo tempo.

* A organização da Creative Cloud à qual você se conecta no AEM Assets se aplica a todos os usuários em sua organização.
