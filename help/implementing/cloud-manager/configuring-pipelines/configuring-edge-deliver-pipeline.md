---
title: Adicionar um pipeline de Edge Delivery
description: Saiba como adicionar um pipeline do Edge Delivery para criar e implantar seu código em ambientes de produção.
index: true
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Primeiros usuários" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: cc3023f0451e0b1d852c497714d6b46fdaed5cfe
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Adicionar um pipeline do Edge Delivery {#configure-edge-delivery-pipeline}

Saiba como configurar pipelines de produção para compilar e implantar seu código em ambientes de produção. Um pipeline de produção primeiro implanta o código no ambiente de preparo. Na aprovação, ele implanta o mesmo código no ambiente de produção.

Um usuário deve ter a função **[Gerente de implantação](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar um pipeline do Edge Delivery.

>[!NOTE]
>
>Os recursos descritos neste artigo só estão disponíveis por meio do programa dos primeiros usuários. Para obter mais detalhes e se inscrever como participante antecipado, consulte [Traga seu próprio Git](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket).