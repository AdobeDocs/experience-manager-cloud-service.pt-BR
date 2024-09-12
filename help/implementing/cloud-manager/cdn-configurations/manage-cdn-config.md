---
title: Gerenciar configurações de CDN
description: Saiba mais sobre como usar o Cloud Manager para editar e atualizar, ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 70f99cfb2cd00278d9ebbb7972ef455af7a87a1b
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 8%

---


# Gerenciar configurações de CDN {#manage-cdn-configurations}

Saiba mais sobre como usar o Cloud Manager para editar e atualizar, ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.

## Editar uma configuração de CDN {#edit-cdn}

Ao editar uma configuração de CDN, você pode ajustar configurações como a camada do ambiente (Publish ou Pré-visualização) ou certificados SSL, sem remover totalmente a configuração existente. As alterações se aplicam ao ambiente selecionado - por exemplo, preparo ou produção - e podem afetar como o conteúdo é entregue e protegido.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para editar uma configuração de CDN:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. No painel de navegação esquerdo, em **Serviços**, clique em **Configurações de CDN**.

1. Na tabela **Configurações de CDN**, clique nas reticências ao final de uma linha cujo CDN você deseja atualizar.

   ![Editando uma configuração de CDN](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. Clique em **Editar**.

1. Na caixa de diálogo **Editar CDN**, defina uma ou mais das opções na respectiva lista suspensa.

   As opções exibidas na caixa de diálogo podem variar dependendo se você estiver usando um CDN gerenciado por Adobe ou um CDN gerenciado pelo cliente.

1. Clique em **Atualizar**.

   O status da CDN editada é atualizado na tabela **Configurações de CDN** para refletir as alterações feitas.


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


