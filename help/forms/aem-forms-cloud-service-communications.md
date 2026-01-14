---
title: Como usar o Forms as a Cloud Service para unir dados com modelos XDP e PDF ou gerar saída nos formatos PCL, ZPL e PostScript?
description: Mesclar dados automaticamente com modelos XDP e PDF ou gerar saída nos formatos PCL, ZPL e PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
feature: Adaptive Forms,APIs & Integrations
role: Admin, Developer, User
source-git-commit: 43b648eb3984867fda35ee04de10b78dd836b481
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 6%

---


# Usar processamento síncrono {#sync-processing-introduction}

Forms as a Cloud Service - As APIs de comunicações permitem criar, montar e fornecer comunicações personalizadas e orientadas à marca, como correspondências comerciais, documentos, declarações, cartas de processamento de solicitações, avisos de benefícios, cartas de processamento de solicitações, faturas mensais e kits de boas-vindas. Você pode usar APIs de comunicações para combinar um modelo (XFA ou PDF) com os dados do cliente para gerar documentos nos formatos PDF, PS, PCL, DPL, IPL e ZPL.

Considere um cenário em que você tem um ou mais modelos e vários registros de dados XML para cada modelo. Você pode usar APIs de comunicações para gerar um documento de impressão para cada registro. <!-- You can also combine the records into a single document. --> O resultado é um documento não interativo do PDF. Um documento não interativo do PDF não permite que os usuários insiram dados em seus campos.

Forms as a Cloud Service - Comunicações fornece APIs sob demanda e em lote (APIs assíncronas) para a geração agendada de documentos:

* As APIs síncronas são adequadas para casos de uso de geração de documento de registro único, latência baixa e sob demanda. Essas APIs são mais adequadas para casos de uso baseados em ações do usuário. Por exemplo, gerar um documento após um usuário preencher um formulário.

* As APIs em lote (APIs assíncronas) são adequadas para casos de uso programados de alta taxa de transferência na geração de vários documentos. Essas APIs geram documentos em lotes. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito e demonstrativos de benefícios gerados todo mês.

## Usar operações síncronas {#batch-operations}

Uma operação síncrona é um processo de geração de documentos de maneira linear. Essas APIs são classificadas como APIs de locatário único e APIs de vários locatários:

### APIs de locatário único

* APIs de geração de documentos
* APIs de manipulação de documentos

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### Autenticar uma API de locatário único

As operações de API de locatário único oferecem suporte a dois tipos de autenticação:

* **Autenticação básica**: a autenticação básica é um esquema de autenticação simples incorporado ao protocolo HTTP. O cliente envia solicitações HTTP com o cabeçalho de Autorização que contém a palavra Básico seguida por um espaço e um nome de usuário de cadeia de caracteres codificado em base64 :password. Por exemplo, para autorizar como administrador / administrador, o cliente envia o nome de usuário [ da cadeia de caracteres codificada em ]base64 Básico: [senha da cadeia de caracteres codificada em base64].

* **Autenticação baseada em token:** a autenticação baseada em token usa um token de acesso (token de autenticação do portador) para fazer solicitações ao Experience Manager as a Cloud Service. O AEM Forms as a Cloud Service fornece APIs para recuperar com segurança o token de acesso. Para recuperar e usar o token para autenticar uma solicitação:

   1. [Recupere a credencial do Experience Manager as a Cloud Service da Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [Instale a credencial do Experience Manager as a Cloud Service em seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (Servidor de Aplicativos, Servidor Web ou outros servidores que não sejam da AEM) configurados para enviar solicitações ao (efetuar chamadas) Cloud Service.
   1. [Gerar um token JWT e trocá-lo com APIs do Adobe IMS por um token de acesso](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. Execute a API do Experience Manager com o token de acesso como um token de autenticação de portador.
   1. [Defina as permissões apropriadas para o usuário da conta técnica no ambiente do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

  >[!NOTE]
  >
  >A Adobe recomenda usar a autenticação baseada em token em um ambiente de produção.

  >[!IMPORTANT]
  >
  > Para obter mais informações, consulte [Autenticação de servidor para servidor OAuth](/help/forms/oauth-api-authetication.md) e [Autenticação de servidor para servidor JWT](/help/forms/jwt-api-authentication.md).
<!-- 

### Authenticate a multi-tenant API

#### Authentication Headers

Every inbound HTTP API call to the multi-tenant API must contain these three headers:


* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

The values which should be sent in the `x-api-key` and `x-gw-ims-org-id` headers are provided in the Credentials details screen in the [Adobe Developer Console](https://developer.adobe.com/console). The value of the `x-api-key` header is the Client ID and the value for the `x-gw-ims-org-id` header is the Organization ID.

#### Configure Adobe Developer console to generate an access token

To set up authentication APIs, create a project in Adobe Developer Console and add Communication APIs to the project on Adobe Developer Console. The integration generates API Key, Client Secret, Payload (JWT):

1. Contact you Adobe Developer Console administrator. Ask the administrator to add as a developer.
1. Log in to `https://developer.adobe.com/console/`. Use your developer account that your administrator has provisioned to log in to Adobe Developer Console.
1. Select your organization from the top-right corner. If you do not know your organization, contact your administrator.
1. Select **[!UICONTROL Create new project]**. A screen to get started with your new project appears. Select **[!UICONTROL Add API]**. A screen with list of all the APIs enabled for your account appears.
1. Select **[!UICONTROL AEM Forms - Communications]** and select **[!UICONTROL Next]**. A screen to configure the API appears.
1. Select **[!UICONTROL OPTION 1 Generate a key pair]** and select **[!UICONTROL Generate keypair]**. It creates and downloads the configuration file. The downloaded configuration file contains all your app settings, along with the only copy of your private key. Adobe does not record your private key, make sure to securely store the downloaded file. Select **[!UICONTROL Next]**.
1. Select **[!UICONTROL Integrations - Cloud Service]** and select **[!UICONTROL Save configured API]**. Select **[!UICONTROL Service Account (JWT)]** to view the API Key, Client Secret, and other information required to access the APIs. You set to use the token to access the APIs.

#### Programmatically generate and use an access token

To programmatically generate an access token, generate a JSON Web Token (JWT) and exchange it with the Adobe Identity Management Service (IMS) for an access token.

Use the following keys, referred to as claims, to construct JWT JSON object:


* `exp`- the requested expiration of the access token, expressed as several seconds since January 1, 1970 GMT. For most use cases, this is a relatively small value. For example, 5 minutes, for five minutes from now, this value should be 1670923791.
* `iss` - the Organization ID from the Adobe Developer Console project, in the format org_ident@AdobeOrg.
* `sub` - the Technical Account ID from the Adobe Developer Console integration, in the format: id@techacct.adobe.com.
* `aud` - the Client ID from the Adobe Developer Console integration prepended with `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - set to the literal value `true`

This JSON object must be then base64 encoded and signed using the private key for the project. Finally, the encoded value is sent in the body of a POST request to `https://ims-na1.adobelogin.com/ims/exchange/jwt` along with the Client ID and Client Secret for the project.

##### Example

```JSON

    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache

```

#### Language Support for JWT

While it is possible to do the entire JWT generation and exchange process in custom code, it is more common to use a higher-level library to do so. A number of such libraries are listed on the [Adobe I/O JWT Documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

-->

### (Somente para APIs de geração de documento) Configurar ativos e permissões

Para usar APIs síncronas, é necessário o seguinte:

* Usuários com privilégios de administrador do Experience Manager
* Faça upload de modelos e outros ativos para sua instância do Experience Manager Forms Cloud Service

### (Somente para APIs de geração de documento) Faça upload de modelos e outros ativos para sua instância do Experience Manager

Uma organização normalmente tem vários modelos. Por exemplo, um modelo para demonstrativos de cartão de crédito, demonstrativos de benefícios e aplicações de reivindicação. Faça upload de todos esses modelos XDP e PDF para sua instância do Experience Manager. Para fazer upload de um modelo:

1. Abra sua instância do Experience Manager.
1. Vá até Forms > Forms e Documentos
1. Clique em Criar > Pasta e crie uma pasta. Abra a pasta.
1. Clique em Criar > Upload de arquivo e faça upload dos modelos.

### Chamar uma API

A [documentação de referência da API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) fornece informações detalhadas sobre todos os parâmetros, métodos de autenticação e vários serviços fornecidos por APIs. A documentação de referência da API também fornece o arquivo de definição de API no formato .yaml. Você pode baixar o arquivo .yaml e carregá-lo no [Postman](https://www.postman.com/) para verificar a funcionalidade das APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
> Saiba mais sobre as etapas detalhadas para chamar APIs de comunicação do AEM Forms. Consulte o artigo [Chamar APIs de comunicação do AEM Forms usando a autenticação de servidor para servidor OAuth](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md).

>[!MORELIKETHIS]
>
>* [Introdução às Comunicações do AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Arquitetura do AEM Forms as a Cloud Service para APIs de comunicação e Forms adaptável](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Processamento da comunicação - APIs síncronas](/help/forms/aem-forms-cloud-service-communications.md)
>* [Processamento de comunicação - APIs em lote](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [API de Comunicações do Forms - Tutorial](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)