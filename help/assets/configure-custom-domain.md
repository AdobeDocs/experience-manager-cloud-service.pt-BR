---
title: Configurar domínio personalizado para camada de publicação
description: Saiba como configurar um domínio personalizado para o nível de publicação no Adobe Cloud Manager.
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---


# Configurar domínio personalizado para camada de publicação{#configure-custom-domain}

No Adobe Cloud Manager, você pode destacar seu site adicionando um domínio personalizado. Embora o AEM as a Cloud Service venha com um domínio padrão, você pode personalizá-lo de acordo com suas necessidades.
<!-- For example, AEM sites can use `sites.custom_domain.com`, and the AEM publish domain can be accessed via `assets.custom_domain.com`. Additionally, getting an SSL certificate for assets.pmi.com with a SAN entry for `delivery.custom_domain.com` improves security and trustworthiness. -->

## Antes de começar

* Você deve ter um certificado TLS ou SSL multisSAN (Nome alternativo da entidade).
* O certificado SSL deve ter SANs distintas em relação ao certificado mapeado para o nível de publicação no mesmo domínio.
* A política de certificado deve seguir a Validação Estendida (EV) ou a Validação da Organização (OV), e não a política de Validação de Domínio (DV).


## Adicionar domínio personalizado

Para configurar um domínio personalizado para o nível de publicação, siga estas etapas:

1. Ir para **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Visão geral do programa]** > **[!UICONTROL Certificados SSL]**e adicione seu certificado SSL.
   ![imagem](/help/assets/assets/ssl-certificate.png)
Saiba como adicionar [Certificado SSL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) no Adobe Cloud Manager.

1. Depois de adicionar o certificado SSL, adicione um domínio personalizado. Clique em **[!UICONTROL Configurações do domínio]** e especifique o domínio personalizado em relação ao **[!UICONTROL Serviço de publicação]** opção.
   <br> Saiba mais sobre [domínio personalizado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=en).

1. Adicione dois registros CNAME no registro DNS correspondente aos domínios de publicação.
   <br> A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.

1. Registre um caso de suporte para facilitar a configuração do domínio personalizado, garantindo que ele seja direcionado para o nível de entrega.

>[!NOTE]
>
> Adicione o domínio personalizado à lista de URLs de redirecionamento permitidos no cliente IMS para o seletor de ativos.<br>Coordene com a respectiva equipe de Adobe para executar essa tarefa fornecendo a cadeia de caracteres do domínio personalizado.
