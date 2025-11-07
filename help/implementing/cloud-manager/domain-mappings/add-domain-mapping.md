---
title: Adicionar um mapeamento de domínio
description: Saiba como adicionar um mapeamento de domínio para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 3%

---


# Sobre a adição de um mapeamento de domínio {#add-domain-mapping}

Para vincular um domínio a um certificado SSL no CDN gerenciado pela Adobe em seu programa, você deve adicionar uma configuração de CDN (Content Delivery Network).

Para CDNs gerenciadas pela Adobe, ao usar um certificado SSL DV, somente sites com validação ACME são permitidos.

>[!IMPORTANT]
>
>Você [adicionou um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) e [adicionou um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md), respectivamente? Caso contrário, você deve concluir essas duas tarefas antes de adicionar uma configuração de CDN.

Consulte também [CDN gerenciada pela Adobe](https://www.aem.live/docs/byo-cdn-adobe-managed).

**Para adicionar um mapeamento de domínio:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Dependendo do caso de uso, siga um destes procedimentos:

   | Caso de uso | Etapas |
   | --- | --- |
   | Quero adicionar uma configuração de CDN a um site do Edge Delivery *existente* no Cloud Manager | a. No menu do lado esquerdo, em **Serviços**, clique em ![ícone Páginas da Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sites do Edge Delivery**.<br>b. Na tabela do Edge Delivery, ao final de uma linha que não tem um domínio associado a ela, clique em ![ícone Mais](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).<br>c Clique em **Configurar CDN**. |
   | Quero adicionar uma configuração de CDN no Cloud Manager | a. No menu do lado esquerdo, em **Serviços**, clique em ![Ícone da rede social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Mapeamentos de Domínio**.<br>b. Próximo ao canto superior direito da página Mapeamentos de Domínio, clique em **Adicionar**. |

1. Na caixa de diálogo **Mapear Domínio para CDN**, selecione o tipo de CDN e a configuração associada selecionando uma das seguintes opções:

   | Tipo de CDN | Detalhes da configuração |
   | --- | --- |
   | CDN gerenciada pela Adobe (Recomendado) | Em **Detalhes de configuração**, faça o seguinte:<br>a. Na lista suspensa **Domínio**, selecione o nome de domínio que deseja usar.<br>Não há domínios verificados disponíveis na lista suspensa? Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br>b.<!-- In the **SSL certificate** drop-down list, select a certificate that you want to use.<br>No SSL certificates available in the drop-down list? See [Add an SSL certificate](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).--> |
   | Outro provedor de CDN | Selecione essa opção se estiver usando seu próprio provedor de CDN e não o CDN gerenciado pela Adobe que está disponível para você.<br>Em **Detalhes da configuração**, na lista suspensa **Domínio**, selecione o nome de domínio que deseja usar.<br>Não há domínios verificados disponíveis na lista suspensa? Consulte [Adicionar um nome de domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |

   ![Caixa de diálogo Mapear Domínio para CDN com o botão de opção CDN gerenciado pela Adobe selecionado](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png)

   <!-- OLD IMAGE/UI (/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)-->

1. No campo **Domínio**, insira o nome de host voltado para o cliente que você deseja atender (por exemplo, `www.example.com`)
1. na lista suspensa **Origem**, selecione uma das seguintes opções:

   | Lista suspensa Origem | Descrição |
   | --- | --- |
   | Sites | Selecione um site do Edge Delivery. |
   | Ambiente | Selecione um ambiente Cloud Service específico que deseja direcionar na configuração do AEM.<br>Na lista suspensa **Camada**, selecione uma das seguintes opções:<br>· Selecione **Publicar** para direcionar um ambiente de produção dinâmico, em que o conteúdo é entregue aos usuários finais.<br>· Selecione **Visualizar** para ambientes de preparo ou não produção nos quais você testa as alterações antes de elas entrarem em funcionamento. |

1. Clique em **Salvar configuração**.

   A Adobe recomenda que você teste o mapeamento de domínio.

## Testar o mapeamento de domínio {#test-domain-mapping}

Você pode verificar se um novo mapeamento de domínio está ativo na CDN gerenciada pela Adobe sem esperar pela propagação de DNS público.

Execute um comando **curl** que substitua a resolução DNS e aponte diretamente para a borda CDN:

```bash
curl -svo /dev/null https://www.example.com \
--resolve www.example.com:443:151.101.3.10
```

* Substitua `www.example.com` pelo seu domínio.
* O endereço IP `151.101.3.10` é um dos IPs que podem ser usados para acessar o AEM Cloud Service. Consulte também [registro APEX](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-apex-record).

O sinalizador `--resolve` força a solicitação para o IP especificado e retorna êxito somente após o certificado e o roteamento para o seu domínio terem sido instalados corretamente.

