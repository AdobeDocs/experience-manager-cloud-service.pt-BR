---
title: Gerenciar sites do Edge Delivery no Cloud Manager
description: Saiba como adicionar uma configuração de CDN a um site do Edge Delivery ou excluir um site do Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Gerenciar o site do Edge Delivery no Cloud Manager {#manage-edge-delivery-sites}

Saiba como gerenciar sites do Edge Delivery no Cloud Manager adicionando uma configuração de CDN a um site existente. Ou exclua um site do Edge Delivery.

## Adicionar uma configuração de CDN a um site existente do Edge Delivery {#add-cdn-to-edge-delivery-site}

Consulte [Adicionar uma configuração de CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Excluir um site do Edge Delivery {#delete-edge-delivery-site}

Se você excluir um site do Edge Delivery Services, todas as configurações de CDN associadas também serão removidas. Essa ação interrompe a conexão entre domínios personalizados e o site. Para obter mais detalhes, consulte Configurações de CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Para excluir um site do Edge Delivery:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa com o Edge Delivery Services configurado, ao qual você deseja adicionar um site do Edge Delivery.
1. Siga um destes procedimentos:
   * Na página **Visão geral do programa**, clique na guia **Edge Delivery**. Na tabela do site do Edge Delivery, clique nas reticências no final de uma linha cujo site você deseja remover.
Clique em **Excluir** e em **Excluir** novamente para confirmar a remoção do site.

     ![Adicionar site do Edge Delivery na guia Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * No canto superior esquerdo da página, clique no ícone de hambúrguer para exibir o menu de navegação esquerdo. No cabeçalho **Serviços**, clique em **Sites do Edge Delivery**.
Na tabela do site do Edge Delivery, clique nas reticências no final de uma linha cujo site você deseja remover. Clique em **Excluir** e em **Excluir** novamente para confirmar a remoção do site.


     ![Adicionar site do Edge Delivery pelo botão Sites do Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)