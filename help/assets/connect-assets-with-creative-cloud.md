---
title: Conectar o AEM Assets ao Creative Cloud
description: Saiba como configurar e conectar o AEM Assets ao Creative Cloud. Conecte-se a um direito de Creative Cloud que é provisionado para uma organização IMS diferente para usar facilmente as integrações de Creative Cloud mais recentes no AEM Assets, incluindo Bibliotecas Expressas e Creative Cloud.
source-git-commit: 8c0c01be301ccaeac4e658c16d63227e55b67fcf
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Conectar o AEM Assets ao Creative Cloud  {#cross-org-entitlements}

A Experience Manager Assets pode se conectar a um direito de Creative Cloud provisionado para uma organização IMS diferente para usar facilmente as integrações de Creative Cloud mais recentes na AEM Assets, incluindo as Bibliotecas Express e Creative Cloud.

Se seus produtos de Creative Cloud e AEM Assets forem provisionados para organizações IMS separadas, você poderá se conectar a uma organização de Creative Cloud diferente para executar workflows integrados entre as duas soluções.

## Pré-requisitos {#prerequisites}

* Direitos de administrador do Experience Manager Assets

* Direito ativo ao Creative Cloud para a mesma ID de usuário usada no Creative Cloud e Experience Manager. Os direitos a IDs pessoais e federadas com o mesmo endereço de email são tratados como IDs de usuário diferentes.

## Conectar a uma nova organização do Creative Cloud {#connect-to-creative-cloud-org}

Para se conectar a uma nova organização Creative Cloud, execute as seguintes etapas:

1. Navegue até **[!UICONTROL Configurações]** > **[!UICONTROL Creative Cloud]**.

1. Selecione a nova organização do Creative Cloud usando o **[!UICONTROL Selecionar nova ID da organização de Creative Cloud]** lista suspensa. A lista exibe todas as organizações às quais você tem acesso. Selecione a organização com direitos de Creative Cloud ativos.

1. Clique em **[!UICONTROL Alternar organizações]** para alternar para a nova organização.

   ![Direitos de Organização Cruzada](assets/cross-org-entitlements.png)

## Limitações {#limitations}

* Você pode conectar o AEM Assets a uma organização Creative Cloud de cada vez. Não há suporte para conexão com várias organizações Creative Cloud de cada vez.

* A organização Creative Cloud à qual você se conecta no AEM Assets se aplica a todos os usuários em sua organização.

