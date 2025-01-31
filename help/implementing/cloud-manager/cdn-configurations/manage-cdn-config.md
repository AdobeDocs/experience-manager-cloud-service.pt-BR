---
title: Gerenciar Mapeamentos de Domínio
description: Saiba mais sobre como usar o Cloud Manager para editar e atualizar, ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: 1683d53491e06ebe2dfcc96184ce251539ecf732
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 8%

---

# Gerenciar Mapeamentos de Domínio {#manage-cdn-configurations}

Saiba mais sobre como usar o Cloud Manager para editar ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.

## Editar uma configuração de CDN na página Mapeamentos do domínio {#edit-cdn}

No Adobe Cloud Manager, talvez você queira editar uma configuração de CDN (Content Delivery Network), incluindo a camada de ambiente (Publish ou Preview) e o certificado SSL, por vários motivos.

* **Alterações de ambiente**: ajustar a camada ajuda a corresponder as configurações de CDN com o ambiente correto, seja para produção em tempo real (Publish) ou teste (Pré-visualização).
* **Aprimoramentos de segurança**: a seleção de um certificado SSL diferente pode ser necessária ao atualizar certificados ou atender às necessidades de conformidade e segurança.
* **Otimização do desempenho**: a edição da configuração garante as configurações corretas de CDN para fornecer conteúdo com base nas necessidades operacionais em constante mudança.

É possível editar uma configuração sem remover totalmente a configuração existente. As alterações se aplicam ao ambiente selecionado - por exemplo, preparo ou produção - e podem afetar como o conteúdo é entregue e protegido.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para editar uma configuração de CDN na página Mapeamentos de Domínio:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. No menu do lado esquerdo, em **Serviços**, clique em ![Ícone da rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mapeamentos de Domínio**.
1. Na tabela **Mapeamentos de Domínio**, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha cuja configuração de CDN você deseja atualizar.

1. No menu suspenso, clique em **Editar**.

1. Na caixa de diálogo **Editar configuração da CDN**, defina uma ou mais das opções na respectiva lista suspensa.

   As opções exibidas na caixa de diálogo dependem se você está usando um **CDN gerenciado por Adobe** ou um **Outro provedor de CDN** (CDN gerenciado pelo cliente).

1. Clique em **Atualizar**.

   O status da CDN editada é atualizado na tabela **Mapeamentos de Domínio** para refletir as alterações feitas.


## Editar uma configuração de CDN na página Ambientes

As etapas para editar uma configuração de CDN na página **Ambientes** são quase as mesmas de [editar uma configuração de CDN na página Mapeamentos de Domínio](#edit-cdn), mas o ponto de entrada é diferente.

**Para editar uma configuração de CDN na página Ambientes:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. No menu do lado esquerdo, clique em ![Ícone de dados](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambientes**.

1. Na página **Ambientes**, selecione um ambiente de interesse.

1. Na página de detalhes do ambiente, no agrupamento Mapeamentos do Domínio, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) que corresponde à configuração de CDN que você deseja editar.

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

1. No menu do lado esquerdo, em **Serviços**, clique em ![Ícone da rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mapeamentos de Domínio**.

1. Na tabela Mapeamentos do Domínio, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha que corresponde a um CDN que você deseja remover e clique em **Excluir**.

1. Na caixa de diálogo **Excluir configuração da CDN**, clique em **Excluir**.

1. Clique em **Excluir** novamente para confirmar a remoção do CDN do site.


## Excluir uma configuração de CDN da página Ambientes

As etapas para excluir uma configuração CDN da página **Ambientes** são quase as mesmas de [excluir uma configuração CDN da página Mapeamentos de Domínio](#edit-cdn), mas o ponto de entrada é diferente.

**Para excluir uma configuração CDN da página Ambientes:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. No menu do lado esquerdo, clique em ![Ícone de dados](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambientes**.

1. Na página **Ambientes**, selecione um ambiente de interesse.

1. Na página de detalhes do ambiente, no agrupamento **Mapeamentos do Domínio**, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) que corresponde à configuração de CDN que você deseja remover e clique em **Excluir**.

1. Na caixa de diálogo **Excluir configuração da CDN**, clique em **Excluir**.

1. Clique em **Excluir** novamente para confirmar a remoção do CDN do site.
