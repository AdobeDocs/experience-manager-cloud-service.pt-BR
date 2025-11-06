---
title: Gerenciar Mapeamentos de Domínio
description: Saiba mais sobre como usar o Cloud Manager para editar e atualizar, ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 7%

---

# Gerenciar Mapeamentos de Domínio {#manage-domain-mappings}

Saiba mais sobre como usar o Cloud Manager para editar ou excluir configurações de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.

## Editar uma configuração de CDN na página Mapeamentos do domínio {#edit-domain-mapping}

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

1. Na caixa de diálogo **Editar Mapeamento de Domínio**, defina uma ou mais das opções na respectiva lista suspensa.

   As opções exibidas na caixa de diálogo dependem se você está usando uma **CDN gerenciada pela Adobe** ou um **Outro provedor de CDN** (CDN gerenciada pelo cliente).

1. Clique em **Atualizar**.


## Disponibilidade para ativação: definir configurações de DNS para um domínio personalizado {#go-live-readiness}

Para que um domínio personalizado possa veicular o tráfego, é necessário concluir a configuração de DNS com o provedor de DNS. Depois de implantar um mapeamento de domínio e clicar em **Ativar**, o Cloud Manager exibe uma caixa de diálogo que o orienta pelo processo de configuração de registros DNS. Você tem a opção de entrar em funcionamento adicionando um tipo de registro CNAME ou um tipo de registro A.

<!-- See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record). -->

**Para configurar a preparação para ativação:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.
1. No menu do lado esquerdo, em **Serviços**, clique em ![Ícone da rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mapeamentos de Domínio**.
1. Na tabela Mapeamentos do Domínio, clique em **Ativar** próximo ao final de uma linha que corresponde a um CDN cuja preparação para ativação você deseja configurar.

   ![Caixa de diálogo de preparação para ativação](/help/implementing/cloud-manager/assets/domain-mappings-go-live-readiness.png)

1. Na caixa de diálogo **Disponibilidade para ativação**, siga um destes procedimentos:

   | Opção | Etapas |
   | --- | --- |
   | Configuração do REGISTRO A | Recomendado para domínios raiz como `example.com`<br><ol><li>Faça logon no portal do provedor de serviços DNS.<li>Vá até a seção Registros DNS.<li>Crie um registro A para apontar para todos os endereços IP listados.</li></ol> |
   | Configurar CNAME | Recomendado para domínios personalizados como `www.example.com`<br><ol><li>Faça logon no portal do provedor de serviços DMS.<li>Vá até a seção Registros DNS.<li>Mapa `cdn.adobeaemcloud.com` (registro CNAME) no registro DNS do provedor de serviços DNS (seu domínio personalizado). Esse mapeamento garante que as solicitações recebidas no domínio personalizado sejam redirecionadas para o CDN da Adobe.</li></ol> |

1. Na caixa de diálogo **Disponibilidade para ativação**, clique em **OK** para salvar o registro.

   Aguarde a propagação do DNS; pode levar de alguns minutos a algumas horas.

   Quando a coluna **[!UICONTROL Status]** na tabela Mapeamentos de Domínio é atualizada para **[!UICONTROL Verificado]**, o domínio personalizado está pronto para uso. Talvez seja necessário clicar em ![Ícone Atualizar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) para atualizar o status.

## Excluir uma configuração de CDN {#delete-cdn}

Ao excluir uma configuração de CDN gerenciada pela Adobe ou gerenciada pelo cliente no Cloud Manager, as configurações de roteamento e certificado SSL do domínio associado são removidas. O domínio não usa mais a CDN para entrega de tráfego e quaisquer aprimoramentos de segurança ou desempenho fornecidos pela CDN são perdidos. Você pode enfrentar uma interrupção do serviço até que uma nova configuração seja definida, seja adicionando novamente o CDN excluído ou adicionando um novo.

O usuário deve ser membro da função **Proprietário da empresa** ou **Gerente de implantação** para concluir esta tarefa.

**Para excluir uma configuração CDN:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. No menu do lado esquerdo, em **Serviços**, clique em ![Ícone da rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mapeamentos de Domínio**.

1. Na tabela Mapeamentos do Domínio, clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) no final de uma linha que corresponde a um CDN que você deseja remover e clique em **Excluir**.

1. Na caixa de diálogo **Excluir mapeamento de domínio**, clique em **Excluir**.

1. Clique em **Excluir** novamente para confirmar a remoção do CDN do site.


## Excluir uma configuração de CDN da página Ambientes

As etapas para excluir uma configuração CDN da página **Ambientes** são quase as mesmas de [excluir uma configuração CDN da página Mapeamentos de Domínio](#edit-cdn), mas o ponto de entrada é diferente.

**Para excluir uma configuração CDN da página Ambientes:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. No menu do lado esquerdo, clique em ![Ícone de dados](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambientes**.

1. Na página **Ambientes**, selecione um ambiente de interesse.

1. Na página de detalhes do ambiente, no agrupamento **Mapeamentos do Domínio**, clique no ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) que corresponde à configuração de CDN que você deseja remover e clique em **Excluir**.

1. Na caixa de diálogo **Excluir mapeamento de domínio**, clique em **Excluir**.

1. Clique em **Excluir** novamente para confirmar a remoção do CDN do site.
