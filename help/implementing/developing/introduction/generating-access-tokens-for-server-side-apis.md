---
title: Geração de Tokens de acesso para APIs do servidor
description: Saiba como facilitar a comunicação entre um servidor de terceiros e o AEM como Cloud Service gerando um token JWT seguro
translation-type: tm+mt
source-git-commit: a29eda3347502a3a498c2f40ed2e46cda59b2a24
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---


# Introdução {#introduction}

>[!IMPORTANT]
>
>Este recurso ainda não está disponível. Consulte as [Notas de versão](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter uma lista atualizada dos recursos.

Algumas arquiteturas dependem de fazer chamadas para AEM como Cloud Service de um aplicativo hospedado em um servidor fora da infraestrutura AEM. Por exemplo, um aplicativo móvel que chama um servidor, que faz solicitações de API para AEM como Cloud Service.

O fluxo de servidor para servidor é descrito abaixo, juntamente com um fluxo simplificado para desenvolvimento. O AEM como Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) é usado para gerar tokens necessários para o processo de autenticação.

## O fluxo de servidor para servidor {#the-server-to-server-flow}

Um usuário com uma função de administrador organizacional IMS pode gerar um AEM como uma credencial de Cloud Service, que pode ser recuperada subsequentemente por um usuário com o AEM como uma função de administrador de Ambiente e deve ser instalada no servidor e precisa ser tratada cuidadosamente como uma chave secreta. Esse arquivo de formato JSON contém todos os dados necessários para integrar um AEM como uma API Cloud Service. Os dados são usados para criar um token JWT assinado, que é trocado com IMS para um token de acesso IMS. Esse token de acesso pode ser usado como um token de autenticação do Portador para fazer solicitações para AEM como Cloud Service.

O fluxo de servidor para servidor envolve as seguintes etapas:

* Obtenha o AEM como credenciais de Cloud Service no Developer Console
* Instale o AEM como credenciais Cloud Service em um servidor que não seja AEM e faça chamadas para AEM
* Gerar um token JWT e trocar esse token por um token de acesso usando as APIs IMS do Adobe
* Chamar a API AEM com o token de acesso como um token de autenticação do portador
* Defina as permissões apropriadas para o usuário da conta técnica no ambiente AEM

### Obtenha o AEM como credenciais de Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Os usuários com acesso ao AEM como um console de desenvolvedor do Cloud Service verão a guia integrações no Developer Console de um determinado ambiente, bem como dois botões. Um usuário com a função de administrador de Ambiente AEM pode clicar no botão **Obter Credenciais de Serviço** para exibir o json de credenciais de serviço, que conterá todas as informações necessárias para o servidor não AEM, incluindo a id do cliente, o segredo do cliente, a chave privada, o certificado e a configuração para as camadas de autor e publicação do ambiente, independentemente da seleção do pod.

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

>[!IMPORTANT]
>
>Um administrador de organização IMS (normalmente o mesmo usuário que forneceu o ambiente pelo Gerenciador de nuvem) deve primeiro acessar o Console do desenvolvedor e clicar no botão **Obter credenciais de serviço** para que as credenciais sejam geradas e recuperadas posteriormente por um usuário com permissões de administrador para o AEM como um ambiente Cloud Service. Se o administrador da organização IMS não tiver feito isso, uma mensagem informará a eles que eles precisam da função Administrador da organização IMS.

### Instale as credenciais de serviço AEM em um servidor não AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

O aplicativo não AEM fazendo chamadas para AEM deve poder acessar o AEM como credenciais de Cloud Service, tratando-o como um segredo.

### Gerar um token JWT e trocá-lo por um Token de acesso{#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Use as credenciais para criar um JWT em uma chamada para o serviço IMS Adobe a fim de recuperar um token de acesso, que é válido por 24 horas.

As credenciais de serviço da AEM CS podem ser trocadas por um token de acesso usando bibliotecas de clientes projetadas para esse fim. As bibliotecas do cliente são do repositório público do Adobe [](https://github.com/adobe/aemcs-api-client-lib), que contém orientações mais detalhadas e informações mais recentes.

```
/*jshint node:true */
"use strict";

const fs = require('fs');
const exchange = require("@adobe/aemcs-api-client-lib");

const jsonfile = "aemcs-service-credentials.json";

var config = JSON.parse(fs.readFileSync(jsonfile, 'utf8'));
exchange(config).then(accessToken => {
    // output the access token in json form including when it will expire.
    console.log(JSON.stringify(accessToken,null,2));
}).catch(e => {
    console.log("Failed to exchange for access token ",e);
});
```

A mesma troca pode ser executada em qualquer idioma capaz de gerar um token JWT assinado com o formato correto e chamar as APIs IMS Token Exchange.

O token de acesso definirá quando expirará, que é normalmente de 12 horas. Há um código de amostra no repositório git para gerenciar um token de acesso e atualizá-lo antes de expirar.

### Chamando a API AEM {#calling-the-aem-api}

Faça as chamadas apropriadas de API de servidor para servidor para um AEM como ambiente, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`. Por exemplo, usando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Defina as permissões apropriadas para o usuário da conta técnica em AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Depois que o usuário da conta técnica é criado no AEM (isso ocorre após a primeira solicitação com o token de acesso correspondente), o usuário da conta técnica deve ter permissão **no** AEM.

Observe que, por padrão, no serviço Autor de AEM, o usuário da conta técnica é adicionado ao grupo de usuários Contribuidores que fornece AEM de acesso de leitura.

Este usuário de conta técnica no AEM pode ser privatizado ainda mais com permissões usando os métodos habituais.

## Fluxo do desenvolvedor {#developer-flow}

Os desenvolvedores provavelmente desejarão testar usando uma instância de desenvolvimento de seu aplicativo não AEM (em execução em seu laptop ou hospedado) que faz solicitações para um AEM de desenvolvimento como um ambiente dev. No entanto, como os desenvolvedores não têm necessariamente permissões de função de administrador IMS, não podemos assumir que eles podem gerar o portador JWT descrito no fluxo regular de servidor para servidor. Dessa forma, fornecemos um mecanismo para um desenvolvedor gerar um token de acesso diretamente que pode ser usado em solicitações para AEM como ambientes Cloud Service a que eles têm acesso.

Consulte a documentação [Diretrizes do desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obter informações sobre as permissões necessárias para usar o AEM como um console do desenvolvedor de Cloud Service.

>[!NOTE]
>
>O token de acesso de desenvolvimento local é válido por 24 horas após o que deve ser regenerado utilizando o mesmo método.

Os desenvolvedores podem usar esse token para fazer chamadas de seu aplicativo de teste não AEM para um AEM como ambiente. Normalmente, o desenvolvedor usará esse token com o aplicativo que não é AEM em seu próprio laptop. Além disso, o AEM como uma nuvem normalmente é um ambiente que não é de produção.

O fluxo do desenvolvedor envolve as seguintes etapas:

* Gerar um token de acesso do Developer Console
* Chame o aplicativo AEM com o token de acesso.

Os desenvolvedores também podem fazer chamadas de API para um projeto AEM em execução em sua máquina local, caso em que um token de acesso não é necessário.

### Gerando o Token de acesso {#generating-the-access-token}

Clique no botão **Obter token de desenvolvimento local** no Developer Console para gerar um token de acesso.

### Chame AEM aplicativo com um Token de acesso {#call-the-aem-application-with-an-access-token}

Faça as chamadas apropriadas de API de servidor para servidor do aplicativo não AEM para um AEM como ambiente Cloud Service, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`.

## Revogação de Credenciais de Serviço {#service-credentials-revocation}

Envie uma solicitação ao suporte ao cliente se o token do portador JWT precisar ser revogado.