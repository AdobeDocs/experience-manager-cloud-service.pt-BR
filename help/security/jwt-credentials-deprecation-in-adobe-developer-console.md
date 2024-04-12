---
title: Descontinuação de credenciais JWT no console do Adobe Developer
description: Saiba mais sobre o impacto da descontinuação de credenciais JWT no Console do Adobe Developer no AEM
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: b8749f7b907e098d23c1cda57930b835f03e3580
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Descontinuação de credenciais JWT no console do Adobe Developer {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>Clientes do AEM 6.5 devem fazer referência a [este artigo](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console) para obter mais informações.

Clientes do Adobe usam [Console do Adobe Developer](https://developer.adobe.com/console) para gerar credenciais que permitem o acesso a várias APIs. Os clientes selecionam entre vários tipos de credenciais, que variam de servidor para servidor do OAuth a aplicativo de página única. Um desses tipos de credenciais, as credenciais da Conta de serviço (JWT), foi descontinuado em favor das credenciais de Servidor para Servidor do OAuth. As credenciais da Nova conta de serviço (JWT) não podem ser criadas em ou após 3 de junho de 2024, e as credenciais JWT existentes não funcionarão em ou após 27 de janeiro de 2025. Você pode [leia sobre a descontinuação](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Este artigo fornece contexto adicional sobre como o AEM as a Cloud Service deve lidar com a desativação.

O principal argumento neste momento é que os recursos de AEM ainda não oferecem suporte às novas credenciais de servidor para servidor do OAuth. O apoio virá em breve — até o final de abril de 2024 por meio de uma liberação de AEM para AEM as a Cloud Service. Você pode ter recebido um email com instruções para migrar suas credenciais do JWT, mas tenha certeza de que pode e deve adiar a migração das credenciais até que o AEM ofereça suporte ao novo tipo de credencial servidor para servidor OAuth.

As seções abaixo listam os cenários em que os clientes devem (ou, em alguns casos, não) substituir suas credenciais da Conta de serviço (JWT) por credenciais de Servidor para Servidor OAuth, uma vez que o AEM ofereça suporte a eles no final de abril. [Saiba como](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) para substituir as credenciais no futuro.

>[!NOTE]
>
>A variável [**AEM** Console do desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (observe o **AEM** no nome, que o distingue da variável **Adobe** Developer Console) fornece um utilitário para gerar [Tokens JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) usado para APIs de servidor para servidor. Essas credenciais não foram substituídas e podem continuar sendo usadas.


## Integração do AEM a outras soluções da Adobe {#integrating-aem-with-other-adobe-solutions}

**Ação**: aguarde para migrar até depois do final de abril de 2024, quando o AEM permitir (este artigo será atualizado nesse momento)

**Versões relevantes do AEM**: AEM AS A CLOUD SERVICE

Os clientes do AEM usam a interface do autor do AEM para configurar integrações com todas as outras soluções de Adobe. Por exemplo, Adobe Target, Adobe Analytics, Adobe Launch, AFCS e muito mais.

![Integração do AEM a outras soluções](/help/security/assets/jwt-deprecation.png)

Como exemplo, aqui estão [as instruções](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=en) para configurar a integração com o Adobe Target. A chave de API na variável [Concluir a configuração do IMS no AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) A seção deve ser migrada para o tipo de credencial servidor para servidor OAuth, assim que o AEM oferecer suporte a essas credenciais no final de abril. Essas instruções serão atualizadas e revisadas no final de abril para ajudar você a aplicar as novas credenciais de servidor para servidor do OAuth.

## APIs do Cloud Manager {#cloud-manager-apis}

**Ação**: aguarde para migrar até depois do final de abril de 2024, quando o AEM permitir (este artigo será atualizado nesse momento).

**Versões relevantes do AEM**: AEM AS A CLOUD SERVICE

Os clientes criam projetos do Adobe Developer Console para que possam invocar [APIs do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). As credenciais no projeto do Adobe Developer devem ser migradas para o tipo de credencial de servidor para servidor OAuth, depois que o AEM e o Cloud Manager forem compatíveis.

## Projetos gerados automaticamente {#autogen-projects}

**Ação**: não migrar, pois o Adobe migrará em seu nome.

**Versões relevantes do AEM**: AEM as a Cloud Service.

Quando o Cloud Manager provisiona ambientes as a Cloud Service AEM, ele gera automaticamente um projeto do Adobe Developer Console com credenciais JWT. Esse projeto está marcado como somente leitura, como ilustrado na captura de tela abaixo. Os clientes não podem e não devem tentar migrar esses projetos para credenciais de servidor para servidor OAuth. Em vez disso, o Adobe migrará esses projetos por conta própria, antes que as credenciais não possam mais ser usadas.

![Projetos gerados automaticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)
