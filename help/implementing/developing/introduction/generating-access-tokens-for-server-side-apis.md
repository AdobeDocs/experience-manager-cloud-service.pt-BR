---
title: Geração de Tokens de acesso para APIs do servidor
description: Saiba como facilitar a comunicação entre um servidor de terceiros e o AEM como Cloud Service gerando um token JWT seguro
translation-type: tm+mt
source-git-commit: 9a4cb6d981fdf5eea4d1b9c7ae9e3c99947d9745
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---


# Introdução {#introduction}

>[!IMPORTANT]
>
>Este recurso ainda não está disponível. Consulte as [Notas de versão](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter uma lista atualizada dos recursos.

Algumas arquiteturas dependem de fazer chamadas para AEM como Cloud Service de um aplicativo hospedado em um servidor fora da infraestrutura AEM. Por exemplo, um aplicativo móvel que chama um servidor, que faz solicitações de API para AEM como Cloud Service.

O fluxo de servidor para servidor é descrito abaixo, juntamente com um fluxo simplificado para desenvolvimento. O AEM como Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) é usado para gerar tokens necessários para o processo de autenticação.

## O fluxo de servidor para servidor {#the-server-to-server-flow}

Um usuário com a função de administrador pode gerar um token do portador JWT, que deve ser instalado no servidor e deve ser tratado com cuidado como uma chave secreta. O token do portador de JWT deve ser trocado com IMS para um token de acesso, que deve ser incluído na solicitação para AEM como Cloud Service.

O fluxo de servidor para servidor envolve as seguintes etapas:

* Gerar o token do portador JWT a partir do console do desenvolvedor
* Instale o token em um servidor não AEM fazendo chamadas para AEM
* Troque o token do portador JWT por um token de acesso usando as APIs Adobe IMS
* Chamando a API AEM

### Gerando o token do portador JWT {#generating-the-jwt-bearer-token}

Os usuários que têm a função de administrador de uma organização verão a guia integrações no console do desenvolvedor de um determinado ambiente, bem como dois botões. Clicar no botão **Obter Credenciais de Serviço** gerará a chave privada, o certificado e a configuração.

![Geração JWT](assets/JWTtoken3.png)

A saída será semelhante ao seguinte:

```
{
  "ok": true,
  "integration": {
    "imsEndpoint": "ims-na1.adobelogin.com",
    "metascopes": "ent_aem_cloud_sdk,ent_cloudmgr_sdk",
    "technicalAccount": {
      "clientId": "cm-p123-e1234",
      "clientSecret": "4AREDACTED17"
    },
    "email": "abcd@techacct.adobe.com",
    "id": "ABCDAE10A495E8C@techacct.adobe.com",
    "org": "1234@AdobeOrg",
    "privateKey": "-----BEGIN RSA PRIVATE KEY-----\r\REDACTED\r\n==\r\n-----END RSA PRIVATE KEY-----\r\n",
    "publicKey": "-----BEGIN CERTIFICATE-----\r\nREDACTED\r\n-----END CERTIFICATE-----\r\n"
  },
  "statusCode": 200
}
```

### Instale o token em um servidor não AEM {#install-the-token-on-a-non-aem-server}

O aplicativo não AEM fazendo chamadas para AEM deve instalar o token do portador JWT, tratando-o como um segredo.

### Troque o token JWT por um Token de acesso {#exchange-the-jwt-token-for-an-access-token}

Inclua o token JWT em uma chamada para o serviço IMS do Adobe para recuperar um token de acesso, que é válido por 24 horas.

### Chamando a API AEM {#calling-the-aem-api}

Faça as chamadas apropriadas de API de servidor para servidor para um AEM como ambiente, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`.

<!-- ### Code Samples {#code-samples}

https://git.corp.adobe.com/boston/skyline-api-client-lib (internal note: URL will change to public git repo before we publish) contains client libraries written in node.js that will exchange the JSON outputted by the developer console for an access token. -->

## Fluxo do desenvolvedor {#developer-flow}

Os desenvolvedores provavelmente desejarão testar usando uma instância de desenvolvimento de seu aplicativo não AEM (em execução em seu laptop ou hospedado) que faz solicitações para um AEM de desenvolvimento como um ambiente dev. No entanto, como os desenvolvedores não têm necessariamente acesso de função de administrador ao AEM como um ambiente de desenvolvimento de Cloud Service, não podemos assumir que eles possam gerar o portador JWT descrito no fluxo regular de servidor para servidor. Dessa forma, fornecemos um mecanismo para um desenvolvedor gerar um token de acesso diretamente que pode ser usado em solicitações para AEM como ambientes Cloud Service a que eles têm acesso. Consulte a documentação [Diretrizes do desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md) para obter informações sobre as permissões necessárias para usar o AEM como um console do desenvolvedor de Cloud Service.

>[!NOTE]
>
>O token é válido por 24 horas após o qual deve ser regenerado usando o mesmo método.

Os desenvolvedores podem usar esse token para fazer chamadas de seu aplicativo de teste não AEM para um AEM como ambiente. Normalmente, o desenvolvedor usará esse token com o aplicativo que não é AEM em seu próprio laptop. Além disso, o AEM como uma nuvem normalmente é um ambiente que não é de produção.

O fluxo do desenvolvedor envolve as seguintes etapas:

* Gerar um token de acesso do Developer Console
* Chame o aplicativo AEM com o token de acesso.

Os desenvolvedores também podem fazer chamadas de API para um projeto AEM em execução em sua máquina local, caso em que um token de acesso não é necessário.

### Gerando o Token de acesso {#generating-the-access-token}

Clique no botão **Obter token de desenvolvimento local** no Developer Console para gerar um token de acesso.

### Chame AEM aplicativo com um Token de acesso {#call-the-aem-application-with-an-access-token}

Faça as chamadas apropriadas de API de servidor para servidor do aplicativo não AEM para um AEM como ambiente Cloud Service, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`.

## Revogação do token do portador JWT {#jwt-bearer-token-revocation}

Envie uma solicitação ao suporte ao cliente se o token do portador JWT precisar ser revogado.