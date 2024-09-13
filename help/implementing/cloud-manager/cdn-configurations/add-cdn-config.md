---
title: Adicionar uma configuração de CDN
description: Saiba como adicionar uma configuração de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 6%

---


# Adicionar uma configuração de CDN {#add-cdn}

Para vincular um domínio a um certificado SSL no CDN gerenciado por Adobe em seu programa, você deve adicionar uma configuração de CDN (Content Delivery Network).

Para CDNs gerenciadas por Adobe, ao usar certificados DV, somente sites com validação ACME são permitidos.

>[!IMPORTANT]
>
>Você [adicionou um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) e [adicionou um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md), respectivamente? Caso contrário, você deve concluir essas duas tarefas antes de adicionar uma configuração de CDN.

**Para adicionar uma configuração de CDN:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Dependendo do caso de uso, siga um destes procedimentos:

   | Caso de uso | Etapas |
   | --- | --- |
   | Quero adicionar uma configuração de CDN a um site do Edge Delivery *existente* no Cloud Manager | a. No painel de navegação esquerdo, em **Serviços**, clique em **Edge Delivery Sites**.<br>b. Na tabela Edge Delivery, no final de uma linha que não tem um domínio associado a ela, clique nas reticências.<br>c Clique em **Configurar CDN**.  ![Clique em Configurar CDN para um site do Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-config-cdn.png) |
   | Quero adicionar uma configuração de CDN no Cloud Manager | a. No painel de navegação esquerdo, em **Serviços**, clique em **Configurações de CDN**.<br>b. Próximo ao canto superior direito da página Configurações de CDN, clique em **Adicionar**. |

1. Na caixa de diálogo **Configurar CDN**, na lista suspensa **Origem**, selecione uma das seguintes opções:

   ![Caixa de diálogo Configurar CDN](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

   | Origem | Descrição |
   | --- | --- |
   | Sites | Selecione um site do Edge Delivery. |
   | Ambiente | Selecione um ambiente de Cloud Service específico que você deseja direcionar dentro da configuração do AEM.<br>Na lista suspensa **Camada**, selecione uma das seguintes opções:<br>· Selecione **Publish** para direcionar um ambiente de produção dinâmico, em que o conteúdo seja entregue aos usuários finais.<br>· Selecione **Visualizar** para ambientes de preparo ou não produção nos quais você testa as alterações antes de elas entrarem em funcionamento. |

1. Selecione o tipo de CDN e a configuração associada ao selecionar uma das seguintes opções:

   | Tipo de CDN | Detalhes da configuração |
   | --- | --- |
   | CDN gerenciada pela Adobe | Em **Detalhes de configuração**, faça o seguinte:<br>a. Na lista suspensa **Domínio**, selecione o nome de domínio que deseja usar.<br>Não há domínios verificados disponíveis na lista suspensa? Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br>b. Na lista suspensa **Certificado SSL**, selecione um certificado que deseja usar.<br>Não há certificados SSL disponíveis na lista suspensa? Consulte [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
   | Outro provedor de CDN | Selecione essa opção se estiver usando seu próprio provedor de CDN e não o CDN gerenciado por Adobe que está disponível para você.<br>Em **Detalhes da configuração**, na lista suspensa **Domínio**, selecione o nome de domínio que deseja usar.<br>Não há domínios verificados disponíveis na lista suspensa? Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |

1. Clique em **Salvar**.
