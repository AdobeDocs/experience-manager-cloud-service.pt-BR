---
title: Certificados validados por domínio (DV)
description: Saiba como gerenciar certificados de domínio validado (DV) no Cloud Manager.
source-git-commit: 5baeb4012e5aa82a8cd8710b18d9164583ede0bd
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 6%

---


# Certificados validados por domínio (DV) {#domain-validated-certificates}

Saiba como gerenciar certificados de domínio validado (DV) no Cloud Manager.

>[!NOTE]
>
>Este recurso só está disponível por meio do [programa de adoção antecipada.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Introdução {#introduction}

O Cloud Manager permite que você gere e gerencie por autoatendimento um certificado SSL de domínio validado (DV). Isso oferece a solução mais rápida, fácil e econômica para criar um site seguro para sua empresa online.

Certificados validados de domínio estão disponíveis para ambos [programas de sandbox e produção.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## Adicionar um domínio personalizado {#adding-domain}

Para adicionar um certificado de domínio validado (DV), primeiro você deve configurar o domínio personalizado. O processo é basicamente o mesmo que o detalhado no documento [Introdução a nomes de domínio personalizados.](/help/implementing/cloud-manager/custom-domain-names/introduction.md) No entanto, essa funcionalidade foi ligeiramente expandida.

1. Ao verificar o domínio, você pode optar por usar certificados gerenciados por Adobe ou gerenciados automaticamente com o domínio. Escolher **Certificado gerenciado Adobe** para adicionar um certificado DV posteriormente.

   ![Escolha o gerenciado por Adobe](assets/verify-domain-dialog.png)

1. Para usar um certificado gerenciado por Adobe, é necessário adicionar um registro CNAME ao DNS conforme descrito na **Verificar domínio** diálogo.

   ![Adicionar entrada CNAME](assets/verify-domain-dialog-adobe-managed.png)

1. Depois que o domínio for criado, toque ou clique no botão de reticências na lista de domínios e selecione **Verificar** para verificar o domínio.

   ![Verificar domínio](assets/verify-domain.png)

## Adicionar um certificado DV {#adding}

Depois que o domínio estiver configurado corretamente, para adicionar um certificado DV, toque ou clique no **Adicionar certificado SSL** na janela Certificados SSL.

![Adição de um certificado DC](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. Selecione a opção **Adobe gerenciado (DV)**.
1. Especifique o nome de domínio no **Selecionar domínios** lista suspensa.
1. Toque ou clique em **Salvar**.

Depois de adicionado com êxito, o certificado terá um status pendente com um sinal de aviso amarelo no nome na **Certificados SSL** janela.

![Certificado DV pendente](assets/pending-dv-certificate.png)

Após a emissão bem-sucedida, o certificado terá uma marca de seleção verde no nome **Certificados SSL** janela.

![Certificado DV emitido](assets/issued-dv-certificate.png)

Para obter mais informações sobre como adicionar certificados SSL e a janela Certificados SSL, consulte o documento [Adicionar um certificado SSL.](add-ssl-certificate.md)

## Adicionar configuração de CDN {#add-cdn}

Esta etapa deve ser concluída para configurar um domínio com um SSL usando o Fastly CDN.

Siga estas etapas para adicionar uma configuração de CDN usando o Cloud Manager.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. Selecione o **Configurações de CDN** e clique ou toque em **Adicionar** na barra de ferramentas.

1. No **Configurar CDN** forneça as informações necessárias.

   * Selecione o **Origem**. Pode ser:
      * Um ambiente de Cloud Service
      * Um site Edge Delivery Services
   * Selecione o tipo CDN.
   * Selecione o domínio.
   * Selecione o certificado SSL.
      * Necessário somente para CDNs gerenciadas por Adobe.

   ![Caixa de diálogo Configurar CDN](assets/configure-cdn-dialog.png)

>
>
>Para CDNs gerenciadas por Adobe, ao usar certificados DV, somente sites com validação ACME são permitidos.
