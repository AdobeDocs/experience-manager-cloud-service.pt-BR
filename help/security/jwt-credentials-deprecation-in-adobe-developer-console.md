---
title: Descontinuação de credenciais JWT no console do Adobe Developer
description: Saiba mais sobre o impacto da descontinuação de credenciais JWT no Console do Adobe Developer no AEM.
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
source-git-commit: f183e1999e29ee7f25f2d427d0b2273d244e4632
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Descontinuação de credenciais JWT no console do Adobe Developer {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>Clientes do AEM 6.5 devem fazer referência a [este artigo](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console) para obter mais informações.

Clientes do Adobe usam [Console do Adobe Developer](https://developer.adobe.com/console) para gerar credenciais que permitem o acesso a várias APIs. Os clientes selecionam entre vários tipos de credenciais, que variam de servidor para servidor do OAuth a aplicativo de página única. Um desses tipos de credenciais, as credenciais da Conta de serviço (JWT), foi descontinuado em favor das credenciais de Servidor para Servidor do OAuth. As credenciais da Nova conta de serviço (JWT) não podem ser criadas em ou após 3 de junho de 2024, e as credenciais JWT existentes não funcionarão em ou após 27 de janeiro de 2025. Você pode [leia sobre a descontinuação](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Este artigo fornece contexto adicional sobre como o AEM as a Cloud Service deve lidar com a desativação.

O principal argumento é que o AEM agora oferece suporte às novas credenciais de servidor para servidor do OAuth para o AEM as a Cloud Service. Você pode ter recebido um email com instruções para migrar suas credenciais do JWT e essa migração pode ser feita agora.

As seções abaixo listam os cenários em que os clientes devem (ou em alguns casos não) substituir suas credenciais da Conta de serviço (JWT) por credenciais de Servidor para Servidor OAuth, agora que o AEM oferece suporte a eles. [Saiba como](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) para migrar as credenciais.

>[!NOTE]
>
>A variável [**AEM** Console do desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (observe o **AEM** no nome, que o distingue da variável **Adobe** Developer Console) fornece um utilitário para gerar [Tokens JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) usado para APIs de servidor para servidor. Essas credenciais não foram substituídas e podem continuar sendo usadas.

## Integração do AEM a outras soluções da Adobe {#integrating-aem-with-other-adobe-solutions}

**Ação**: migrar sua configuração como AEM agora oferece suporte às credenciais OAuth.

**Versões relevantes do AEM**: AEM AS A CLOUD SERVICE

Os clientes do AEM usam o AEM para configurar integrações com muitas outras soluções de Adobe. Por exemplo, Adobe Target, Adobe Analytics e outros.

Consulte [Configuração de integrações IMS para o AEM as a Cloud Service](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) para obter detalhes sobre como:

* criar configurações com credenciais do OAuth
* migrar configurações, que foram criadas com credenciais JWT, para usar credenciais OAuth

## APIs do Cloud Manager {#cloud-manager-apis}

**Ação**: migre suas credenciais JWT para as credenciais OAuth, que agora são compatíveis com o Cloud Manager.

**Versões relevantes do AEM**: AEM AS A CLOUD SERVICE

Os clientes criam projetos do Adobe Developer Console para que possam invocar [APIs do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). As credenciais no projeto do Adobe Developer devem ser migradas para o tipo de credencial servidor para servidor OAuth antes que as credenciais do JWT obsoletas expirem em janeiro de 2025.

## Projetos gerados automaticamente {#autogen-projects}

**Ação**: não migre porque o Adobe migrará em seu nome.

**Versões relevantes do AEM**: AEM as a Cloud Service.

Quando o Cloud Manager provisiona ambientes as a Cloud Service AEM, ele gera automaticamente um projeto do Adobe Developer Console com credenciais JWT. Esse projeto está marcado como somente leitura, como ilustrado na captura de tela abaixo. Os clientes não podem e não devem tentar migrar esses projetos para credenciais de servidor para servidor do OAuth. Em vez disso, o Adobe migrará esses projetos por conta própria, antes que as credenciais deixem de ser utilizáveis.

![Projetos gerados automaticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)
