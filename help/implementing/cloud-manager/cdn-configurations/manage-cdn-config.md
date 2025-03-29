---
title: Gerenciar Mapeamentos de Domínio
description: Saiba mais sobre como usar o Cloud Manager para editar e atualizar, ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: 41155a724f48ad28a12aac615a3e9a13bb3afa26
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 8%

---

# Gerenciar Mapeamentos de Domínio {#manage-cdn-configurations}

Saiba mais sobre como usar o Cloud Manager para editar ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.

## Editar uma configuração de CDN na página Mapeamentos do domínio {#edit-cdn}

No Adobe Cloud Manager, você pode editar uma configuração de CDN (Content Delivery Network), incluindo a camada de ambiente (Publicação ou Pré-visualização) e o certificado SSL, por vários motivos.

* **Alterações de ambiente**: ajustar a camada ajuda a corresponder as configurações de CDN com o ambiente correto, seja para produção em tempo real (Publicação) ou teste (Visualização).
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

   As opções exibidas na caixa de diálogo dependem se você está usando uma **CDN gerenciada pela Adobe** ou um **Outro provedor de CDN** (CDN gerenciada pelo cliente).

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

   As opções exibidas na caixa de diálogo dependem se você está usando uma **CDN gerenciada pela Adobe** ou um **Outro provedor de CDN** (CDN gerenciada pelo cliente).

1. Clique em **Atualizar**.

<!-- 
## Go live readiness: Configure DNS settings for a custom domain {#go-live-readiness} 

Before a custom domain can serve traffic in Adobe Cloud Manager, you must complete DNS configuration with your DNS provider. After deploying a domain mapping and clicking **Go live**, Cloud Manager displays a dialog box that guides you through the DNS record setup process. You have the option to go live by adding either a CNAME record type or an A record type representing Fastly's IPs, simplifying domain routing. This ability eliminates the restriction of relying solely on CNAME records for domain setup with Fastly.

MAYBE There is support for A record types to improve Go Live readiness for domains using CDN configurations in AEM Cloud Manager. MAYBE

See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record).

**To configure Go live readiness:**

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate organization and program.

1. In the left side menu, under **Services**, click ![Social network icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Domain Mappings**.

1. In the Domain Mappings table, click **Go live** near the end of a row that corresponds to a CDN whose Go Live readiness you want to configure. 

1. In the Go live readiness dialog box, do one of the following:

    | Configure  | Steps |
    | --- | --- |
    | A RECORD | Recommended for root domains like `example.com`<br><ol><li>Log in to your DNS service provider's portal.<li>Go to the DNS Records section.<li>Create an A record to point to all the listed IP addresses.<li>In the Go live readiness dialog box, click **OK**.<li>In the Domain Mappings table, under the **Status** column, click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg).<br>The status is updated to **Verified** when the resolution is complete.</li></ol> |
    | CNAME | Recommended for custom domains like `www.example.com`<br><ol><li>Log in to your DMS service provider's portal.<li>Go to the DNS Records section.<li>Map [cdn.adobeaemcloud.com](http://cdn.adobeaemcloud.com/) (CNAME record) in the DNS record of the DNS service provider (your custom domain). This mapping ensures that requests received at the custom domain are redirected to Adobe's CDN.<li>In the **Go live readiness** dialog box, click **OK** to save the record.<br>Wait for DNS propogation (may take several minutes to a few hours). When the **[!UICONTROL Status]** column in the Domamin Mappings table updates to **[!UICONTROL Verified]**, the custom domain is ready to use. You may need to click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) to refresh the status.</li></ol> | 
    
-->

## Excluir uma configuração de CDN {#delete-cdn}

Ao excluir uma configuração de CDN gerenciada pela Adobe ou gerenciada pelo cliente no Cloud Manager, as configurações de roteamento e certificado SSL do domínio associado são removidas. O domínio não usa mais a CDN para entrega de tráfego e quaisquer aprimoramentos de segurança ou desempenho fornecidos pela CDN são perdidos. Você pode enfrentar uma interrupção do serviço até que uma nova configuração seja definida, seja adicionando novamente o CDN excluído ou adicionando um novo.

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
