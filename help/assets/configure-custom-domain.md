---
title: Configurar um domínio personalizado para a camada de publicação
description: Saiba como configurar um domínio personalizado para o nível de publicação no Adobe Cloud Manager.
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 6%

---

# Configurar um domínio personalizado para o nível de publicação{#configure-custom-domain}

No Adobe Cloud Manager, você pode destacar seu site adicionando um domínio personalizado. Embora o AEM as a Cloud Service venha com um domínio padrão, você pode personalizá-lo de acordo com suas necessidades.

## Antes de começar

* Você deve ter um certificado TLS ou SSL multisSAN (Nome alternativo da entidade).
* O certificado SSL deve ter SANs distintas em relação ao certificado mapeado para o nível de publicação no mesmo domínio.
* A política de certificado deve seguir a Validação Estendida (EV) ou a Validação da Organização (OV), e não a política de Validação de Domínio (DV).


## Configurar um domínio personalizado para o nível de publicação

1. Acesse **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Visão geral do programa]** > **[!UICONTROL Certificados SSL]** e adicione seu certificado SSL.
   ![imagem](/help/assets/assets/ssl-certificate.png)
Saiba como adicionar [certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) no Adobe Cloud Manager.

1. Depois de adicionar o certificado SSL, adicione um domínio personalizado. Clique em **[!UICONTROL Configurações de Domínio]** e especifique o domínio personalizado com base na opção **[!UICONTROL Serviço de publicação]**.
Saiba mais sobre [domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Adicione dois [registros CNAME](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) no registro DNS correspondente aos domínios de publicação.
A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.

1. Registre um caso de suporte para facilitar a configuração do domínio personalizado, garantindo que ele seja direcionado para o nível de entrega.

>[!NOTE]
>
>Adicione o domínio personalizado à lista de URLs de redirecionamento permitidos. A lista está no cliente IMS para o seletor de ativos.<br>Coordene com a respectiva equipe do Adobe para executar esta tarefa fornecendo a cadeia de caracteres de domínio personalizada.
