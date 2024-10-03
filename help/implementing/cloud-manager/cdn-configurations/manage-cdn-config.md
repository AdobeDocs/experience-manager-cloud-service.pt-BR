---
title: Gerenciar configurações de CDN
description: Saiba mais sobre como usar o Cloud Manager para editar e atualizar, ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ff8c7fb21b4d8bcf395d28c194a7351281eef45b
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 6%

---


# Gerenciar configurações de CDN (Content Delivery Network) {#manage-cdn-configurations}

Saiba mais sobre como usar o Cloud Manager para editar e atualizar, ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.

## Editar uma configuração de CDN {#edit-cdn}

No Adobe Cloud Manager, talvez você queira editar uma configuração de CDN, incluindo a camada de ambiente (Publish ou Pré-visualização) e o certificado SSL, por vários motivos.

* **Alterações de ambiente**: ajustar a camada ajuda a corresponder as configurações de CDN com o ambiente correto, seja para produção em tempo real (Publish) ou teste (Pré-visualização).
* **Aprimoramentos de segurança**: a seleção de um certificado SSL diferente pode ser necessária ao atualizar certificados ou atender às necessidades de conformidade e segurança.
* **Otimização do desempenho**: a edição da configuração garante as configurações corretas de CDN para fornecer conteúdo com base nas necessidades operacionais em constante mudança.

É possível editar uma configuração sem remover totalmente a configuração existente. As alterações se aplicam ao ambiente selecionado - por exemplo, preparo ou produção - e podem afetar como o conteúdo é entregue e protegido.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para editar uma configuração de CDN:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. No painel lateral, em **Serviços**, clique em ![Ícone de rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Configurações de CDN**.
1. Na tabela **Configurações de CDN**, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cuja configuração de CDN você deseja atualizar.

   ![Editando uma configuração de CDN](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. No menu suspenso, clique em **Editar**.
1. Na caixa de diálogo **Editar configuração da CDN**, defina uma ou mais das opções na respectiva lista suspensa.

   As opções exibidas na caixa de diálogo podem variar, dependendo se você estiver usando um CDN gerenciado por Adobe ou um CDN gerenciado pelo cliente.

1. Clique em **Atualizar**.

   O status da CDN editada é atualizado na tabela **Configurações de CDN** para refletir as alterações feitas.

<!-- ## ALTERNATE METHOD FOR EDITING A CDN CONFIGURATION from the Environments page
    
    The steps for adding a custom domain name from the **Environments** page are the same as when [adding a custom domain name from the Domain Settings page](#adding-cdn-settings), but the entry point differs. Follow these steps to add a custom domain name from the **Environments** page.
    
    1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate organization and program.
    
    1. Navigate to the **Environments Detail** detail page for the environment of interest.
    
       ![Entering domain name on the Environment Details page](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)
    
    1. Use the **Domain Names** table to submit the custom domain name.
    
       1. Enter the custom domain name.
       1. Select the SSL certificate associated with this name from the drop-down list.
       1. Click ![Add icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Add**.
    
       ![Add a custom domain name](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)
    
    1. The **Add domain name** dialog box opens to the **Domain Name** tab. Continue as you would for [adding a custom domain name from the Domain Settings page](#adding-cdn-settings). -->

## Excluir uma configuração de CDN {#delete-cdn}

Ao excluir uma configuração de CDN gerenciada por Adobe ou gerenciada pelo cliente no Adobe Cloud Manager, as configurações de roteamento e certificado SSL do domínio associado são removidas. O domínio não usa mais a CDN para entrega de tráfego e quaisquer aprimoramentos de segurança ou desempenho fornecidos pela CDN são perdidos. Você pode enfrentar uma interrupção do serviço até que uma nova configuração seja definida, seja adicionando novamente o CDN excluído ou adicionando um novo.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para excluir uma configuração CDN:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. No painel de navegação esquerdo, em **Serviços**, clique em **Configurações de CDN**.

1. Na tabela Configurações de CDN, clique nas reticências no final de uma linha cujo CDN você deseja remover.

   ![Excluindo uma configuração de CDN](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. Clique em **Excluir**.
1. Clique em **Excluir** novamente para confirmar a remoção do CDN do site.


