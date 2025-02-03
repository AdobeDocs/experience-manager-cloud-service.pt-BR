---
title: Adicionar uma configuração de CDN
description: Saiba como adicionar uma configuração de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: 70ee0ca9e7bb37abc6b82413fc02e37347893011
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 6%

---


# Adicionar uma configuração de CDN {#add-cdn}

Para vincular um domínio a um certificado SSL no CDN gerenciado por Adobe em seu programa, você deve adicionar uma configuração de CDN (Content Delivery Network).

Para CDNs gerenciados por Adobe, ao usar um certificado SSL DV, somente sites com validação ACME são permitidos.

>[!IMPORTANT]
>
>Você [adicionou um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) e [adicionou um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md), respectivamente? Caso contrário, você deve concluir essas duas tarefas antes de adicionar uma configuração de CDN.

Consulte também [CDN gerenciado por Adobe](https://www.aem.live/docs/byo-cdn-adobe-managed).

**Para adicionar uma configuração de CDN:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Dependendo do caso de uso, siga um destes procedimentos:

   | Caso de uso | Etapas |
   | --- | --- |
   | Quero adicionar uma configuração de CDN a um site do Edge Delivery *existente* no Cloud Manager | a. No menu do lado esquerdo, em **Serviços**, clique em ![ícone Páginas da Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sites do Edge Delivery**.<br>b. Na tabela do Edge Delivery, ao final de uma linha que não tem um domínio associado a ela, clique em ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).<br>c Clique em **Configurar CDN**. |
   | Quero adicionar uma configuração de CDN no Cloud Manager | a. No menu do lado esquerdo, em **Serviços**, clique em ![Ícone da rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mapeamentos de Domínio**.<br>b. Próximo ao canto superior direito da página Mapeamentos de Domínio, clique em **Adicionar**. |

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
