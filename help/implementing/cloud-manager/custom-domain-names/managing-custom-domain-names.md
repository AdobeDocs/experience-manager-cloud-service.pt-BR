---
title: Gerenciar nomes de domínio personalizados
description: Saiba como usar o Cloud Manager para exibir, atualizar, substituir e excluir nomes de domínio personalizados.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 17%

---


# Gerenciar nomes de domínio personalizados {#managing-custom-domain-names}

O Cloud Manager permite editar, atualizar, substituir, verificar e excluir nomes de domínio personalizados.

## Editar uma configuração personalizada de nome de domínio {#view-and-update}

No Adobe Cloud Manager, talvez você queira editar uma configuração de nome de domínio personalizada pelos seguintes motivos:

* **Alternar ambientes**: para aplicar a configuração correta, dependendo se você está disponibilizando conteúdo para usuários finais (Publicação) ou usuários internos (Autor).
* **Atualizações de segurança**: para atualizar para um certificado SSL mais recente para fins de segurança avançada ou conformidade.
* **Alterando estratégia de implantação**: para garantir que o certificado SSL correto seja aplicado a um ambiente específico para criptografia e acesso ao site adequados.

**Para editar uma configuração personalizada de nome de domínio:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, selecione o programa.

1. No canto superior esquerdo da página, clique em ![Mostrar ícone de menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para exibir o menu do lado esquerdo.

1. No cabeçalho **Serviços**, clique em ![Ícone da rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mapeamentos de Domínio**.

1. Na página **Mapeamentos do Domínio**, clique em ![Mostrar ícone do menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) ao final de uma linha cujo CDN você deseja editar.

1. Clique em **Editar**.

1. Na caixa de diálogo **Editar configuração de domínio**, faça o seguinte:

   * Na lista suspensa **Camada**, selecione a camada (Publicação ou Visualização) que deseja usar.
   * Na lista suspensa **Certificado SSL**, selecione o certificado SSL que deseja usar.

1. Clique em **Atualizar**.


## Atualizar um certificado SSL de nome de domínio personalizado {#update-cert}

Siga as mesmas etapas acima para atualizar um certificado SSL de nome de domínio personalizado.

>[!NOTE]
>
>O certificado SSL deve ser válido, [já configurado](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), e conter o nome de domínio personalizado que você está atualizando.


## Verificar um nome de domínio personalizado {#verify-custom-domain-name}

Consulte também [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até a página **Configurações de Domínio** a partir da tela **Visão Geral**.

1. Identifique a linha do nome de domínio personalizado que deseja verificar.

1. Clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) na extremidade direita da linha.

1. No menu suspenso, clique em **Verificar**.

1. Na caixa de diálogo **Verificar domínio**, em **Que tipo de certificado você pretende usar com este domínio?**, selecione uma das seguintes opções:

   | Opção Tipo de certificado | Descrição |
   | --- | --- |
   | Certificado SSL gerenciado pela Adobe (DV) | Selecione esse tipo de certificado se quiser usar um certificado DV (Domain Validation). Essa opção é ideal para a maioria dos casos, fornecendo validação básica de domínio. O Adobe gerencia e renova o certificado automaticamente. |
   | Certificado SSL gerenciado pelo cliente (OV/EV) | Selecione esse tipo de certificado se pretender usar um certificado SSL EV/OV para proteger o domínio. Essa opção oferece segurança aprimorada com OV (Validação da Organização) ou EV (Validação Estendida). Use se uma verificação mais rigorosa, níveis de confiança mais altos ou controle personalizado dos certificados for necessário. |

1. Na caixa de diálogo **Verificar domínio**, com base no tipo de certificado selecionado, siga um destes procedimentos:

   | Se você selecionou o tipo de certificado | Descrição |
   | --- | ---  |
   | Certificado gerenciado pela Adobe | a. Conclua as [etapas de certificado gerenciado pela Adobe](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-steps). Quando você concluir as etapas na caixa de diálogo **Verificar domínio**, clique em **Verificar**.<ul><li>A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.</li><li>A Cloud Manager verifica a propriedade do nome de domínio e atualiza o status na tabela **Configurações de Domínio**. Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.</li>![Verificar status do domínio](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. Agora você está pronto para [adicionar um certificado SSL gerenciado pela Adobe](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert).</li></ul> |
   | Certificado gerenciado pelo cliente | a. Clique em **OK**.<br>b. Agora você está pronto para [adicionar um certificado SSL gerenciado pelo cliente (OV/EV)](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert).<br>Depois de adicionar o certificado, seu nome de domínio é marcado como verificado na tabela **Configurações de Domínio**. Consulte [Verificar o status do nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais detalhes.</li></ul><br>![Verificar domínio para um certificado EV/OV gerenciado pelo cliente](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |


## Excluir um nome de domínio personalizado de todos os ambientes associados {#deleting}

Um usuário com a função de **Proprietário da empresa** ou **Gerente de implantação** pode usar o Cloud Manager para excluir um nome de domínio personalizado.

### Excluir um nome de domínio personalizado de todos os ambientes associados {#delete-cdn-all}

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriados.

1. Navegue até a página **Configurações de Domínio** a partir da tela **Visão Geral**.

1. Identifique a linha do nome de domínio personalizado que deseja excluir.

1. Clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) na extremidade direita da linha.

1. Selecione **Excluir**.

1. Confirme seu envio.


### Excluir um nome de domínio personalizado de um ambiente específico {#delete-cdn-specific}

>[!WARNING]
>
>Remova os registros DNS do domínio com seu provedor de DNS *antes* de excluir o domínio no Cloud Manager. Entradas de DNS abandonadas (pendentes) podem ser sequestradas e representar um risco de segurança.

**Para excluir um nome de domínio personalizado de um ambiente específico:**

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione a organização e o programa apropriado.

1. Acesse a tela **Ambientes** a partir da página **Visão geral**.

1. Na página **Ambientes**, navegue até uma tela de detalhes do ambiente de interesse.

1. Na tabela Mapeamentos de domínio, identifique a linha do nome de domínio personalizado que deseja excluir.

1. Clique em ![Mais ícone](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) na extremidade direita da linha.

1. Selecione **Excluir**.

1. Confirme seu envio.
