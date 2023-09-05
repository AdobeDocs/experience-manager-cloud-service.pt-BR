---
title: Suporte ao cookie Same Site para o Adobe Experience Manager as a Cloud Service
description: Suporte ao cookie Same Site para o Adobe Experience Manager as a Cloud Service
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: ht
source-wordcount: '283'
ht-degree: 100%

---

# Suporte ao cookie Same Site para o Adobe Experience Manager as a Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

Desde a versão 80, o Chrome e, mais tarde, o Safari introduziram um novo modelo para segurança de cookies. Esse modo é projetado para introduzir controles de segurança em torno da disponibilidade de cookies para sites de terceiros, por meio de uma configuração chamada `SameSite`. Para obter informações mais detalhadas, consulte este [artigo](https://web.dev/samesite-cookies-explained/).

O valor padrão dessa configuração (`SameSite=Lax`) pode fazer com que a autenticação entre instâncias ou serviços AEM não funcione. Isso ocorre porque os domínios ou as estruturas de URL desses serviços podem não se enquadrar nas restrições dessa política de cookie.

Para contornar isso, é preciso definir o atributo de cookie SameSite como `None` para o token de logon.

>[!CAUTION]
>
>A configuração `SameSite=None` só é aplicada se o protocolo for seguro (HTTPS).
>
>Se o protocolo não for seguro (HTTP), a configuração será ignorada e o servidor exibirá esta mensagem de AVISO:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

É possível adicionar a configuração seguindo as etapas abaixo:

1. Instale localmente uma versão do Quickstart do SDK do AEM
1. Vá para o Console da Web em `http://serveraddress:serverport/system/console/configMgr`
1. Pesquise e clique em **Manipulador de autenticação de token do Adobe Granite**
1. Defina o **atributo SameSite para o cookie de token de logon** para `None`, conforme mostrado na imagem abaixo
   ![samesite](/help/security/assets/samesite1.png)
1. Clique em Salvar
1. Gere as configurações de formato JSON para essa configuração específica seguindo as etapas descritas em [Gerar configurações OSGi usando o Quickstart do SDK do AEM](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. Aplique as configurações seguindo as etapas da documentação do OSGi [Formato de API do Cloud Manager para propriedades de configuração](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties).

Depois que esta configuração for atualizada e os usuários forem desconectados e conectados novamente, os cookies `login-token` têm o atributo `None` definido e são incluídos em solicitações entre sites.
