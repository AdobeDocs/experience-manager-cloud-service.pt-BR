---
title: Adicionar uma configuração de CDN
description: Saiba como adicionar uma configuração de CDN para um site do Edge Delivery ou um ambiente do Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: dd696580758e7ab9a5427d47fda4275f9ad7997f
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 8%

---

# Adicionar uma configuração de CDN {#add-cdn}

A adição de uma configuração de CDN deve ser concluída para configurar um domínio com um SSL.

>
>
>Para CDNs gerenciadas por Adobe, ao usar certificados DV, somente sites com validação ACME são permitidos.

**Para adicionar uma configuração de CDN:**

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Clique em **Configurações de CDN**.

1. Próximo ao canto superior direito da página Configurações de CDN, clique em **Adicionar**.

   ![Caixa de diálogo Configurar CDN](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. Na caixa de diálogo **Configurar CDN**, forneça as informações necessárias.

   * Na lista suspensa **Origem**, siga um destes procedimentos:
      * **Sites:** selecione um site de Edge Delivery Services.
      * **Ambientes:** selecione um ambiente Cloud Service.
         * **Camada:** Selecione uma camada da Web do **Publish** ou do **Preview** para o ambiente selecionado.
   * Selecione seu tipo de CDN: **CDN gerenciado por Adobe** ou **Outro provedor de CDN**.
   * Selecione o domínio.
   * Selecione o certificado SSL. Necessário somente se você selecionou **CDN gerenciado por Adobe** como seu tipo de CDN.

1. Clique em **Salvar**.
