---
title: Configurar domínio personalizado para camada de publicação
description: Saiba como configurar um domínio personalizado para o nível de publicação no Adobe Cloud Manager.
source-git-commit: f6c0e8e5c1d7391011ccad5aa2bad4a6ab7d10c3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 6%

---


# Configurar domínio personalizado para camada de publicação{#configure-custom-domain}

No Adobe Cloud Manager, você pode destacar seu site adicionando um domínio personalizado. Embora o AEM as a Cloud Service venha com um domínio padrão, você pode personalizá-lo de acordo com suas necessidades.

## Antes de começar

* Você deve ter um certificado TLS ou SSL multisSAN (Nome alternativo da entidade).
* O certificado SSL deve ter SANs distintas em relação ao certificado mapeado para o nível de publicação no mesmo domínio.
* A política de certificado deve seguir a Validação Estendida (EV) ou a Validação da Organização (OV), e não a política de Validação de Domínio (DV).


## Adicionar domínio personalizado

Para configurar um domínio personalizado para o nível de publicação, siga estas etapas:

1. Acesse **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Visão geral do programa]** > **[!UICONTROL Certificados SSL]** e adicione seu certificado SSL.
   ![imagem](/help/assets/assets/ssl-certificate.png)
Saiba como adicionar o [certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) ao Adobe Cloud Manager.

1. Depois de adicionar o certificado SSL, adicione um domínio personalizado. Clique em **[!UICONTROL Configurações de Domínio]** e especifique o domínio personalizado em relação à opção de **[!UICONTROL serviço do Publish]**.
Saiba mais sobre [domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Adicione 2 [registros CNAME](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) no registro DNS correspondente aos domínios de publicação.
A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.

1. Registre um caso de suporte para facilitar a configuração do domínio personalizado, garantindo que ele seja direcionado para o nível de entrega.

>[!NOTE]
>
> Adicione o domínio personalizado à lista de URLs de redirecionamento permitidos no cliente IMS para o seletor de ativos.<br>Coordene com a respectiva equipe de Adobe para executar esta tarefa fornecendo a cadeia de caracteres do domínio personalizado.
