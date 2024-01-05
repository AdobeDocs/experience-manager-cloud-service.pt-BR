---
title: Processo de provisionamento - Visão geral
description: Processo de provisionamento - Visão geral
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 98%

---


# AEM as a Cloud Service: integração e acesso

Esta página lista os recursos de autoajuda sobre o processo de provisionamento do Experience Manager as a Cloud Service.

## Visão geral do processo de provisionamento do AEM as a Cloud Service

Esta seção contempla os artigos-chave com foco em:

* Acesso ao AEM as a Cloud Service
* Processo de integração e provisionamento do Adobe Experience Manager as a Cloud Service
* Ajuda e recursos


### Acesso ao AEM as a Cloud Service

Quando o provisionamento automático for concluído:

* Direitos de acesso concedidos – a Adobe criará uma organização no Identity Management System (IMS)
* O Administrador designado terá permissões de administrador por padrão
* O administrador poderá adicionar usuários e funções para membros de equipe adicionais por meio do Admin Console
* Revisar as permissões com base em funções para que os usuários determinem quais permissões devem ser atribuídas no Cloud Manager

![processoverview.jpg](assets/processOverview.jpg)


Para obter mais informações, consulte [Integração do Experience Manager as a Cloud Service na Experience League](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html).

### Recursos e links

* [Suporte IMS do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=pt-BR)
* [Permissões com base em funções no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html#what-is-required)
* [Acesso ao Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#getting-access)


## Processo de integração do Adobe Experience Manager as a Cloud Service

### 1. A ordem de compra aciona o provisionamento automático.

### 2. Integração das organizações no Adobe Admin Console:

![processoverview2.jpg](assets/processOverview2.jpg)

* Administrador do sistema:
   * Provisiona programas e ambientes do AEM.
   * Usa o Admin Console para tarefas administrativas.
   * Reivindica um domínio para confirme a propriedade do respectivo domínio.
   * Configura os diretórios do usuário.
   * Configuração do IDP.
* Administrador do AEM:
   * Gerencia grupos locais, permissões e privilégios.

### 3. Integração de usuários e gerenciamento do acesso no Admin Console:

![processoverview3.jpg](assets/processOverview3.jpg)

Três métodos para integrar usuários, dependendo do tamanho e da preferência:
* Criar usuários manualmente no Admin Console
* Fazer upload de um arquivo .csv
* Sincronizar usuários do Ative
Diretory da empresa

### 4. O administrador configura a organização e concede aos usuários e ao grupo acesso aos ambientes

## Ajuda e recursos

* [Primeiro logon - Cloud Service](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)
* [Configuração do acesso ao AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#accessing)
