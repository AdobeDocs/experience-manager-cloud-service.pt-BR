---
title: Configurar um domínio personalizado para a camada do Publish
description: Saiba como configurar um domínio personalizado para o nível de publicação no Adobe Cloud Manager.
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 5%

---

# Configurar um domínio personalizado para o nível de publicação{#configure-custom-domain}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>O Dynamic Media com guia de recursos OpenAPI agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia de Recursos do Dynamic Media com OpenAPI]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

No Adobe Cloud Manager, você pode destacar seu site adicionando um domínio personalizado. Embora o AEM as a Cloud Service venha com um domínio padrão, você pode personalizá-lo de acordo com suas necessidades.

## Antes de começar

* Você deve ter um certificado TLS ou SSL multisSAN (Nome alternativo da entidade).
* O certificado SSL deve ter SANs distintas em relação ao certificado mapeado para o nível de publicação no mesmo domínio.
* A política de certificado deve seguir a Validação Estendida (EV) ou a Validação da Organização (OV), e não a política de Validação de Domínio (DV).


## Configurar um domínio personalizado para o nível de publicação

1. Acesse **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Visão geral do programa]** > **[!UICONTROL Certificados SSL]** e adicione seu certificado SSL.
   ![imagem](/help/assets/assets/ssl-certificate.png)
Saiba como adicionar o [certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) ao Adobe Cloud Manager.

1. Depois de adicionar o certificado SSL, adicione um domínio personalizado. Clique em **[!UICONTROL Configurações de Domínio]** e especifique o domínio personalizado em relação à opção de **[!UICONTROL serviço do Publish]**.
Saiba mais sobre [domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Adicione dois [registros CNAME](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) no registro DNS correspondente aos domínios de publicação.
A verificação de DNS pode levar algumas horas para ser processada devido a atrasos de propagação de DNS.

1. Registre um caso de suporte para facilitar a configuração do domínio personalizado, garantindo que ele seja direcionado para o nível de entrega.

>[!NOTE]
>
Adicione o domínio personalizado à lista de URLs de redirecionamento permitidos. A lista está no cliente IMS para o seletor de ativos.<br>Coordene com a respectiva equipe de Adobe para executar esta tarefa fornecendo a cadeia de caracteres do domínio personalizado.
