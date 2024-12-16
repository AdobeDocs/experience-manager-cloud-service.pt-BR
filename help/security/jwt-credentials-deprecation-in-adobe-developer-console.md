---
title: Descontinuação de credenciais JWT no Adobe Developer Console
description: Saiba mais sobre o impacto da descontinuação de credenciais JWT no Adobe Developer Console no AEM.
exl-id: 7c811081-484c-41f7-a289-4e9a10a837b3
feature: Security
role: Admin
source-git-commit: 18e9daad8bec6749d493994264792c0cd3b55d15
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# Descontinuação de credenciais JWT no Adobe Developer Console {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
>
>Clientes do AEM 6.5 devem consultar [a documentação comparável do AEM 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/jwt-credentials-deprecation-in-adobe-developer-console) para obter mais informações.

Os clientes do Adobe usam o [Adobe Developer Console](https://developer.adobe.com/console) para gerar credenciais que habilitam o acesso a várias APIs. Os clientes selecionam entre vários tipos de credenciais, que variam de servidor para servidor do OAuth a aplicativo de página única. Um desses tipos de credenciais, as credenciais da Conta de serviço (JWT), foi descontinuado em favor das credenciais de Servidor para Servidor do OAuth. As credenciais da Nova conta de serviço (JWT) não podem ser criadas em ou após 3 de junho de 2024, e as credenciais JWT existentes não funcionarão em ou após 27 de janeiro de 2025. Você pode [ler sobre a descontinuação](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Este artigo fornece contexto adicional sobre como o AEM as a Cloud Service deve lidar com a desativação.

O principal argumento é que o AEM agora oferece suporte às novas credenciais OAuth de servidor para servidor para o AEM as a Cloud Service. Você pode ter recebido um email com instruções para migrar suas credenciais do JWT e essa migração pode ser feita agora.

As seções abaixo listam os cenários em que os clientes devem (ou em alguns casos não) substituir suas credenciais da Conta de serviço (JWT) por credenciais de Servidor para Servidor OAuth, agora que o AEM oferece suporte a eles. [Leia como](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) migrar as credenciais.

>[!NOTE]
>
>O [**AEM** Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) (observe o **AEM** no nome, que o distingue do **Adobe** Developer Console) fornece um utilitário para gerar [tokens JWT](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) usados para APIs de servidor para servidor. Essas credenciais não foram substituídas e podem continuar sendo usadas.

## Integração do AEM a outras soluções da Adobe {#integrating-aem-with-other-adobe-solutions}

**Ação**: migrar sua configuração como AEM agora dá suporte a credenciais OAuth.

**Versões relevantes do AEM**: AEM as a Cloud Service

Os clientes do AEM usam o AEM para configurar integrações com muitas outras soluções de Adobe. Por exemplo, Adobe Target, Adobe Analytics e outros.

Consulte [Configuração de integrações IMS para AEM as a Cloud Service](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) para obter detalhes sobre como:

* criar configurações com credenciais do OAuth
* migrar configurações, que foram criadas com credenciais JWT, para usar credenciais OAuth

## APIs do Cloud Manager {#cloud-manager-apis}

**Ação**: migrar as credenciais do JWT para as credenciais do OAuth, para as quais a Cloud Manager agora oferece suporte.

**Versões relevantes do AEM**: AEM as a Cloud Service

Os clientes criam projetos do Adobe Developer Console para que possam invocar [APIs do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). As credenciais no projeto do Adobe Developer devem ser migradas para o tipo de credencial servidor para servidor OAuth antes que as credenciais do JWT obsoletas expirem em janeiro de 2025.

## Projetos gerados automaticamente {#autogen-projects}

**Ação**: não migrar porque o Adobe migrará em seu nome.

**Versões relevantes do AEM**: AEM as a Cloud Service.

Quando o Cloud Manager provisiona ambientes do AEM as a Cloud Service, ele gera automaticamente um projeto do Adobe Developer Console com credenciais JWT. Esse projeto está marcado como somente leitura, como ilustrado na captura de tela abaixo. Os clientes não podem e não devem tentar migrar esses projetos para credenciais de servidor para servidor do OAuth. Em vez disso, o Adobe migrará esses projetos por conta própria, antes que as credenciais deixem de ser utilizáveis.

![Projetos gerados automaticamente](/help/security/assets/jwt-deprecation-autogen-projects.png)

## Perguntas frequentes sobre projetos gerados automaticamente {#autogen-projects-faqs}

Esta seção fornece respostas às perguntas mais frequentes sobre a descontinuação de credenciais JWT para projetos gerados automaticamente no AEM as a Cloud Service.

**Como faço para quais projetos são gerados automaticamente?**

Navegue até o Adobe Developer Console | seção Projetos.  Os projetos gerados automaticamente pelo AEM as a Cloud Service terão um ícone de bloqueio com identificador &quot;Gerado automaticamente&quot;.  Os projetos gerados automaticamente seguem o formato AEM-p#####-e###### e são criados pelo usuário da conta técnica.

![Projetos Gerados Automaticamente](/help/security/assets/jwt-alert.png)

**E se encontrarmos problemas com nossos projetos gerados automaticamente?**

Entre em contato com o [Atendimento ao cliente do Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).

**Devo migrar nossos projetos gerados automaticamente?**

Nenhuma ação é necessária, pois o Adobe migrará gerado automaticamente em seu nome para ambientes com AEM versão 17258 (agosto de 2024) e superior.

**Quais são as linhas de tempo para migração de projetos gerados automaticamente?**

O Adobe iniciará uma abordagem de migração em fases no primeiro trimestre de 2025, começando com ambientes de desenvolvimento.

**Como nossa instância do AEM as a Cloud Service será afetada se tivermos uma versão do AEM mais antiga que a versão do AEM 17258 (24 de agosto)?**

As integrações de projeto geradas automaticamente deixarão de funcionar se não forem migradas para o OAuth até junho de 2025.

Para garantir uma transição sem problemas, os clientes devem entrar em contato com o [Atendimento ao cliente do Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html) imediatamente e iniciar o processo de atualização para a [versão mais recente do AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/maintenance/latest). Isso proporcionará tempo suficiente para testes de regressão e permitirá que o Adobe gerencie a migração de projetos com eficiência.

**Posso atualizar para uma versão do OAuth com suporte sem atualizar minha versão do AEM as a Cloud Service AEM?**

Não. Para garantir uma transição sem problemas, os clientes devem entrar em contato com o [Atendimento ao cliente do Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html) imediatamente e iniciar o processo de atualização para a [versão mais recente do AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/maintenance/latest). Isso proporcionará tempo suficiente para testes de regressão e permitirá que o Adobe gerencie a migração de projetos com eficiência.
