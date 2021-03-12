---
title: Suporte a cookies do mesmo site para Adobe Experience Manager as a Cloud Service
description: Suporte a cookies do mesmo site para Adobe Experience Manager as a Cloud Service
translation-type: tm+mt
source-git-commit: e51d9c3e4691fb58f3c4b6a2565cc8cad2a1acb0
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Suporte a cookies do mesmo site para Adobe Experience Manager as a Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

Desde a versão 80, Chrome e posterior Safari, introduziu um novo modelo para segurança de cookies. Esse modo foi projetado para introduzir controles de segurança sobre a disponibilidade de cookies para sites de terceiros, por meio de uma configuração chamada `SameSite`. Para obter informações mais detalhadas, consulte este [artigo](https://web.dev/samesite-cookies-explained/).

O valor padrão dessa configuração (`SameSite=Lax`) pode fazer com que a autenticação entre instâncias ou serviços AEM não funcione. Isso ocorre porque os domínios ou as estruturas de URL desses serviços podem não se enquadrar nas restrições dessa política de cookie.

Para contornar isso, você precisa definir o atributo de cookie SameSite como `None` para o token de logon.

Você pode fazer isso seguindo as etapas abaixo:

1. Instale uma versão do Início rápido do SDK AEM localmente
1. Vá para o Console da Web em `http://serveraddress:serverport/system/console/configMgr`
1. Procure e clique em **Manipulador de Autenticação de Token do Adobe Granite**
1. Defina o atributo **SameSite para o cookie de token de login** como `None`, conforme mostrado na imagem abaixo
   ![samesite](/help/security/assets/samesite1.png)
1. Clique em Salvar
1. Gere as configurações de formato JSON para essa configuração específica seguindo as etapas descritas em [Gerar configurações OSGi usando o Início rápido do SDK AEM](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. Aplique as configurações seguindo as etapas na documentação [Formato da API do Cloud Manager para Configuração de Propriedades](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi .
