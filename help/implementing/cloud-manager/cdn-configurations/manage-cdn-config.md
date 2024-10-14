---
title: Gerenciar configurações de CDN
description: Saiba mais sobre como usar o Cloud Manager para editar e atualizar, ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 9%

---


# Gerenciar configurações de CDN {#manage-cdn-configurations}

Saiba mais sobre como usar o Cloud Manager para editar ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.

## Editar uma configuração de CDN na página Configurações de CDN {#edit-cdn}

No Adobe Cloud Manager, talvez você queira editar uma configuração de CDN (Content Delivery Network), incluindo a camada de ambiente (Publish ou Preview) e o certificado SSL, por vários motivos.

* **Alterações de ambiente**: ajustar a camada ajuda a corresponder as configurações de CDN com o ambiente correto, seja para produção em tempo real (Publish) ou teste (Pré-visualização).
* **Aprimoramentos de segurança**: a seleção de um certificado SSL diferente pode ser necessária ao atualizar certificados ou atender às necessidades de conformidade e segurança.
* **Otimização do desempenho**: a edição da configuração garante as configurações corretas de CDN para fornecer conteúdo com base nas necessidades operacionais em constante mudança.

É possível editar uma configuração sem remover totalmente a configuração existente. As alterações se aplicam ao ambiente selecionado - por exemplo, preparo ou produção - e podem afetar como o conteúdo é entregue e protegido.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para editar uma configuração de CDN na página Configurações de CDN:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. No menu à esquerda, em **Serviços**, clique em ![Ícone de rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Configurações de CDN**.
1. Na tabela **Configurações de CDN**, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cuja configuração de CDN você deseja atualizar.

   ![Editando uma configuração de CDN](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. No menu suspenso, clique em **Editar**.

1. Na caixa de diálogo **Editar configuração da CDN**, defina uma ou mais das opções na respectiva lista suspensa.

   As opções exibidas na caixa de diálogo dependem se você está usando um **CDN gerenciado por Adobe** ou um **Outro provedor de CDN** (CDN gerenciado pelo cliente).

1. Clique em **Atualizar**.

   O status da CDN editada é atualizado na tabela **Configurações de CDN** para refletir as alterações feitas.


## Editar uma configuração de CDN na página Ambientes

As etapas para editar uma configuração de CDN na página **Ambientes** são quase as mesmas de [editar uma configuração de CDN na página Configurações de CDN](#edit-cdn), mas o ponto de entrada é diferente.

**Para editar uma configuração de CDN na página Ambientes:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. No menu do lado esquerdo, clique em **Ambientes**.

1. Na página **Ambientes**, selecione um ambiente de interesse.

1. Na página de detalhes do ambiente, no agrupamento Configurações de CDN, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) que corresponde à configuração de CDN que você deseja editar.

   ![Inserção do nome de domínio na página Detalhes do ambiente](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)

1. No menu suspenso, clique em **Editar**.

1. Na caixa de diálogo **Editar Configuração da CDN**, defina uma ou mais das opções na respectiva lista suspensa.

As opções exibidas na caixa de diálogo dependem se você está usando um **CDN gerenciado por Adobe** ou um **Outro provedor de CDN** (CDN gerenciado pelo cliente).

1. Clique em **Atualizar**.


<!-- ## Go live readiness {#go-live-readiness} 

1. ADD STEPS -->


## Excluir uma configuração de CDN {#delete-cdn}

Ao excluir uma configuração de CDN gerenciada por Adobe ou gerenciada pelo cliente no Cloud Manager, as configurações de roteamento e certificado SSL do domínio associado são removidas. O domínio não usa mais a CDN para entrega de tráfego e quaisquer aprimoramentos de segurança ou desempenho fornecidos pela CDN são perdidos. Você pode enfrentar uma interrupção do serviço até que uma nova configuração seja definida, seja adicionando novamente o CDN excluído ou adicionando um novo.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para excluir uma configuração CDN:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. No menu à esquerda, em **Serviços**, clique em **Configurações de CDN**.

1. Na tabela Configurações de CDN, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha que corresponde a um CDN que você deseja remover e clique em **Excluir**.

   ![Excluindo uma configuração de CDN](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. Na caixa de diálogo **Excluir configuração da CDN**, clique em **Excluir**.

1. Clique em **Excluir** novamente para confirmar a remoção do CDN do site.


## Excluir uma configuração de CDN da página Ambientes

As etapas para excluir uma configuração CDN da página **Ambientes** são quase as mesmas de [excluir uma configuração CDN da página Configurações CDN](#edit-cdn), mas o ponto de entrada é diferente.

**Para excluir uma configuração CDN da página Ambientes:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. No menu do lado esquerdo, clique em **Ambientes**.

1. Na página **Ambientes**, selecione um ambiente de interesse.

1. Na página de detalhes do ambiente, no agrupamento **Configurações de CDN**, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) que corresponde à configuração de CDN que você deseja remover e clique em **Excluir**.

   ![Grupo de configuração de CDN em uma página de detalhes do ambiente](/help/implementing/cloud-manager/assets/cdn/environments-cdn-config.png)

1. Na caixa de diálogo **Excluir configuração da CDN**, clique em **Excluir**.

1. Clique em **Excluir** novamente para confirmar a remoção do CDN do site.


