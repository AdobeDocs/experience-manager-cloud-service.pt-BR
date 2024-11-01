---
title: Gerenciar sites do Edge Delivery no Cloud Manager
description: Saiba como adicionar uma configuração de CDN a um site do Edge Delivery ou excluir um site do Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f64a551bc18b53d0026736ece2a44e48cd0cfb4c
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Gerenciar o site do Edge Delivery no Cloud Manager {#manage-edge-delivery-sites}

Saiba como gerenciar sites do Edge Delivery no Cloud Manager adicionando uma configuração de CDN a um site existente. Ou exclua um site do Edge Delivery.

## Adicionar uma configuração de CDN a um site existente do Edge Delivery {#add-cdn-to-edge-delivery-site}

Consulte [Adicionar uma configuração de CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Renomear um site do Edge Delivery (#rename-edge-delivery-site)

No Adobe Cloud Manager, talvez você queira renomear um site do Edge Delivery por vários motivos:

* **Clareza e organização**: descrever melhor a finalidade do site ou seu ambiente associado (por exemplo, produção, preparo).
* **Evitando confusão**: se vários sites estiverem em uso, renomeá-los pode ajudar a diferenciá-los facilmente, reduzindo a chance de aplicar configurações ou atualizações ao site errado.
* **Padronização**: para seguir uma convenção de nomenclatura consistente que se alinhe às diretrizes de sua organização para facilitar o gerenciamento e a auditoria.

**Para renomear um site do Edge Delivery:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa com o Edge Delivery Services configurado, ao qual você deseja adicionar um site do Edge Delivery.
1. Siga um destes procedimentos:

   * Na página **Visão geral do programa**, clique na guia **Edge Delivery**. Na tabela do site do Edge Delivery, clique nas reticências no final de uma linha cujo site você deseja renomear.
Clique em **Renomear**.
   * No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo. No cabeçalho **Serviços**, clique em ![ícone de páginas da Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**.
Na tabela de sites do Edge Delivery, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cujo site você deseja renomear. Clique em **Renomear**.

1. Na caixa de diálogo **Editar Site do Edge Delivery**, no campo de texto **Nome do Site**, digite o novo nome do site.

1. Clique em **Editar**.

## Excluir um site do Edge Delivery {#delete-edge-delivery-site}

Se você excluir um site do Edge Delivery Services, todas as configurações de CDN associadas também serão removidas. Essa ação interrompe a conexão entre domínios personalizados e o site. Para obter mais detalhes, consulte Configurações de CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Para excluir um site do Edge Delivery:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione o programa apropriado.
1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa com o Edge Delivery Services configurado, ao qual você deseja adicionar um site do Edge Delivery.
1. Siga um destes procedimentos:

   * Na página **Visão geral do programa**, clique na guia **Edge Delivery**. Na tabela de sites do Edge Delivery, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cujo site você deseja remover.
Clique em ![Excluir site do Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Excluir** e em **Excluir** novamente para confirmar a remoção do site.

     ![Adicionar site do Edge Delivery na guia Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo. No cabeçalho **Serviços**, clique em ![Página da Web dos sites do Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sites do Edge Delivery**.
Na tabela de sites do Edge Delivery, clique no ícone ![Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cujo site você deseja remover. Clique em ![Excluir site do Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Excluir** e em **Excluir** novamente para confirmar a remoção do site.

     ![Adicionar site do Edge Delivery pelo botão Sites do Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Registrar um tíquete de suporte {#eds-support-ticket}

{{support-ticket}}


