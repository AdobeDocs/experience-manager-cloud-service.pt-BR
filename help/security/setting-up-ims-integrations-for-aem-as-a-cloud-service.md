---
title: Configuração de integrações do IMS para o AEM as a Cloud Service
description: Saiba como configurar integrações do IMS para o AEM as a Cloud Service
exl-id: 72fb1ea1-355c-4faa-a733-77bc7de75ed5
feature: Security
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---

# Configuração de integrações do IMS para o AEM as a Cloud Service {#setting-up-ims-integrations-for-aemaacs}

>[!NOTE]
>
>As configurações JWT provisionadas automaticamente não devem ser migradas manualmente, pois serão tratadas automaticamente pelo Adobe.

O Adobe Experience Manager (AEM) as a Cloud Service pode ser integrado a muitas outras soluções de Adobe. Por exemplo, Adobe Target, Adobe Analytics e outros.

As integrações usam uma integração IMS, configurada com S2S OAuth.

* Depois de criar:

   * [Credenciais na Developer Console](#credentials-in-the-developer-console)

* Em seguida, é possível:

   * Criar uma (nova) [configuração do OAuth](#creating-oauth-configuration)

   * [Migrar uma configuração JWT existente para uma configuração OAuth](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>Anteriormente, as configurações eram feitas com [Credenciais JWT que agora estão sujeitas a desativação no Adobe Developer Console](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md).
>
>Essas configurações não podem mais ser criadas ou atualizadas, mas podem ser migradas para configurações OAuth.

## Credenciais na Developer Console {#credentials-in-the-developer-console}

Como primeira etapa, é necessário configurar as credenciais do OAuth no Adobe Developer Console.

Para obter detalhes sobre como fazer isso, consulte a documentação do Developer Console, dependendo de suas necessidades:

* Visão geral:

   * [Autenticação de Servidor para Servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* Criação de uma nova credencial OAuth:

   * [Guia de implementação de credenciais de servidor para servidor do OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

* Migrar uma credencial JWT existente para uma credencial OAuth:

   * [Migrando da credencial de conta de serviço (JWT) para a credencial de servidor para servidor OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)

Por exemplo:

![Credencial OAuth na Developer Console](assets/ims-configuration-developer-console.png)

## Criação de uma configuração OAuth {#creating-oauth-configuration}

Para criar uma nova Integração do Adobe IMS usando o OAuth:

1. No AEM, navegue até **Ferramentas**, **Segurança**, **Integração do Adobe IMS**.

1. Selecione **Criar**.

1. Conclua a configuração com base nos detalhes da [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Por exemplo:

   ![Criar configuração OAuth](assets/ims-create-oauth-configuration.png)

1. **Salve** suas alterações.

## Migração de uma configuração JWT existente para uma configuração OAuth {#migrating-existing-JWT-configuration-to-oauth}

Para migrar uma Integração do Adobe IMS existente com base em credenciais JWT:

>[!NOTE]
>
>Este exemplo mostra uma Configuração IMS do Launch.

1. No AEM, navegue até **Ferramentas**, **Segurança**, **Integração do Adobe IMS**.

1. Selecione a configuração JWT que precisa ser migrada. As configurações JWT estão marcadas com o aviso **Credenciais JWT (obsoletas)**.

1. Selecionar **Propriedades**:

   ![Selecionar configuração JWT](assets/ims-migrate-jwt-select-configuration.png)

1. A configuração será aberta como somente leitura:

   ![Propriedades de Configuração - Somente Leitura](assets/ims-migrate-jwt-properties-read-only.png)

1. Selecione **OAuth** na lista suspensa **Tipo de Autenticação**:

   ![Selecionar tipo de autenticação](assets/ims-migrate-jwt-authentication-type.png)

1. As propriedades disponíveis serão atualizadas. Use os detalhes do Developer Console para concluí-los:

   ![Detalhes de OAuth completos](assets/ims-migrate-jwt-complete-oauth-details.png)

1. Use **Salvar e fechar** para manter suas atualizações.
Quando você retornar ao console, o aviso **Credenciais JWT (obsoletas)** desaparecerá.
