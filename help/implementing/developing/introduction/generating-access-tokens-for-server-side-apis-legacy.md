---
title: Geração de tokens de acesso para APIs do lado do servidor (herdado)
description: Saiba como facilitar a comunicação entre um servidor de terceiros e o AEM as a Cloud Service gerando um token JWT seguro
hidefromtoc: true
exl-id: 6561870c-cbfe-40ef-9efc-ea75c88c4ed7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 0%

---

# Geração de tokens de acesso para APIs do lado do servidor (herdado) {#generating-access-tokens-for-server-side-apis-legacy}

Algumas arquiteturas dependem de fazer chamadas para o AEM as a Cloud Service a partir de um aplicativo hospedado em um servidor fora da infraestrutura AEM. Por exemplo, um aplicativo móvel que chama um servidor, que faz solicitações de API para o AEM as a Cloud Service.

O fluxo de servidor para servidor é descrito abaixo, juntamente com um fluxo simplificado para desenvolvimento. O AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) é usado para gerar tokens necessários para o processo de autenticação.

<!-- ERROR: Not Found (HTTP error 404)
>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## O fluxo de servidor para servidor {#the-server-to-server-flow}

Um usuário com uma função de administrador da organização IMS e que também é membro do Perfil de produto Usuários do AEM ou Administradores do AEM no AEM Author pode gerar uma credencial do AEM as a Cloud Service. Essa credencial pode ser recuperada posteriormente por um usuário com a função de administrador do Ambiente AEM as a Cloud Service e deve ser instalada no servidor e precisa ser tratada cuidadosamente como uma chave secreta. Esse arquivo de formato JSON contém todos os dados necessários para integrar a uma API do AEM as a Cloud Service. Os dados são usados para criar um token JWT assinado, que é substituído pelo IMS por um token de acesso IMS. Esse token de acesso pode ser usado como um token de autenticação de portador para fazer solicitações à AEM as a Cloud Service. As credenciais expiram após um ano por padrão, mas podem ser atualizadas quando necessário. Consulte [Atualizar Credenciais](#refresh-credentials).

O fluxo de servidor para servidor envolve as seguintes etapas:

* Buscar as credenciais para o AEM as a Cloud Service na Developer Console
* Instalar as credenciais do AEM as a Cloud Service em um servidor não AEM que faça chamadas para o AEM
* Gere um token JWT e troque-o por um token de acesso usando APIs IMS do Adobe
* Chamada da API AEM com o token de acesso como um token de autenticação de portador
* Definir as permissões apropriadas para o usuário da conta técnica no ambiente AEM

### Buscar as credenciais do AEM as a Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Os usuários com acesso ao console do desenvolvedor do AEM as a Cloud Service veem a guia Integrações no Developer Console para um determinado ambiente e dois botões. Um usuário com a função de administrador Ambiente AEM as a Cloud Service pode clicar no botão **Gerar Credenciais de Serviço** para gerar e exibir as credenciais de serviço json. O json contém todas as informações necessárias para o servidor não-AEM, incluindo id do cliente, segredo do cliente, chave privada, certificado e configuração para os níveis de criação e publicação do ambiente, independentemente da seleção do pod.

![Geração JWT](assets/JWTtoken3.png)

A saída é semelhante ao seguinte:

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

Após serem geradas, as credenciais podem ser recuperadas posteriormente pressionando o botão **Obter Credenciais de Serviço** no mesmo local.

>[!IMPORTANT]
>
>Um administrador de organização IMS — geralmente o usuário que provisionou o ambiente por meio do Cloud Manager — que também deve ser membro do Perfil de produto Usuários do AEM ou Administradores do AEM AEM no Author acessa o Developer Console. Em seguida, eles devem clicar no botão **Gerar credenciais de serviço** para que as credenciais sejam geradas e recuperadas posteriormente por um usuário com permissões de administrador para o ambiente do AEM as a Cloud Service. Se o administrador da organização IMS não tiver feito essa tarefa, uma mensagem informará que ele precisa da função de Administrador da organização IMS.

### Instalar as credenciais do serviço AEM em um servidor não AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

O aplicativo não AEM que faz chamadas para AEM deve ser capaz de acessar as credenciais do AEM as a Cloud Service, tratando-o como um segredo.

### Gerar um token JWT e trocá-lo por um token de acesso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Use as credenciais para criar um token JWT em uma chamada para o serviço IMS Adobe para recuperar um token de acesso, que é válido por 24 horas.

As Credenciais de Serviço AEM CS podem ser trocadas por um token de acesso usando bibliotecas de clientes criadas para essa finalidade. Adobe As bibliotecas de clientes estão disponíveis no [repositório GitHub público](https://github.com/adobe/aemcs-api-client-lib), que contém orientações mais detalhadas e informações mais recentes.

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

A mesma troca pode ser executada em qualquer linguagem capaz de gerar um token JWT assinado com o formato correto e chamar as APIs IMS Token Exchange.

O token de acesso define quando expira, o que geralmente é de 24 horas. Há um código de amostra no repositório Git para gerenciar um token de acesso e atualizá-lo antes que ele expire.

### Chamar a API do AEM {#calling-the-aem-api}

Fazer as chamadas de API de servidor para servidor apropriadas para um ambiente do AEM as a Cloud Service, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`. Por exemplo, usando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Definir as permissões apropriadas para o usuário da conta técnica no AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Depois que o usuário da conta técnica é criado no AEM (ocorre após a primeira solicitação com o token de acesso correspondente), o usuário da conta técnica deve receber a permissão adequada de **in** AEM.

Por padrão, no serviço do Autor AEM, o usuário da conta técnica é adicionado ao grupo de usuários Colaboradores, que fornece acesso de leitura ao AEM.

Esse usuário técnico da conta no AEM pode ser provisionado ainda mais com permissões usando os métodos usuais.

## Fluxo do desenvolvedor {#developer-flow}

Os desenvolvedores devem testar usando uma instância de desenvolvimento de seu aplicativo não AEM (em execução no laptop ou hospedado) que faça solicitações a um ambiente de desenvolvimento AEM as a Cloud Service. No entanto, como os desenvolvedores não têm necessariamente permissões de função de administrador do IMS, o Adobe não pode supor que podem gerar o portador JWT descrito no fluxo regular de servidor para servidor. Dessa forma, o Adobe fornece um mecanismo para que um desenvolvedor gere um token de acesso diretamente que possa ser usado em solicitações para um ambiente AEM as a Cloud Service ao qual tenha acesso.

Consulte a [documentação das Diretrizes do desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obter informações sobre as permissões necessárias para usar o console do desenvolvedor do AEM as a Cloud Service.

>[!NOTE]
>
>O token de acesso de desenvolvimento local é válido por no máximo 24 horas após as quais deve ser gerado novamente usando o mesmo método.

Os desenvolvedores podem usar esse token para fazer chamadas de seu aplicativo de teste não-AEM para um ambiente AEM as a Cloud Service. Normalmente, o desenvolvedor usa esse token com o aplicativo não-AEM em seu próprio notebook. Além disso, o AEM as a Cloud normalmente é um ambiente de não produção.

O fluxo do desenvolvedor envolve as seguintes etapas:

* Gerar um token de acesso pela Developer Console
* Chame o aplicativo AEM com o token de acesso.

Os desenvolvedores também podem fazer chamadas de API para um projeto AEM em execução em sua máquina local, caso em que um token de acesso não é necessário.

### Gerar o token de acesso {#generating-the-access-token}

Para gerar um token de acesso, no Developer Console, clique em **Obter token de desenvolvimento local**.

### Chame, depois, o aplicativo AEM com um token de acesso {#call-the-aem-application-with-an-access-token}

Fazer as chamadas de API de servidor para servidor apropriadas do aplicativo não-AEM para um ambiente AEM as a Cloud Service, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`.

## Atualizar credenciais {#refresh-credentials}

Por padrão, a credencial no AEM as a Cloud Service expira após um ano. Para garantir a continuidade do serviço, os desenvolvedores têm a opção de atualizar as credenciais, estendendo sua disponibilidade por mais um ano. Use **Atualizar Credenciais de Serviço** a partir da guia **Integrações** na Developer Console, conforme mostrado abaixo.

![Atualização de credencial](assets/credential-refresh.png)

Depois de pressionar o botão, um novo conjunto de credenciais é gerado. Você pode atualizar seu armazenamento secreto com as novas credenciais e validar se elas funcionam como deveriam.

>[!NOTE]
>
> Depois de clicar no botão **Atualizar Credenciais de Serviço**, as credenciais antigas permanecem registradas até que expirem, mas somente o conjunto mais recente está disponível para ser visto do Developer Console a qualquer momento.

## Revogação de Credenciais de Serviço {#service-credentials-revocation}

Se as credenciais precisarem ser revogadas, você deverá enviar uma solicitação ao suporte ao cliente usando estas etapas:

1. Desative o usuário da conta técnica para o Adobe Admin Console na interface do usuário do:
   * No Cloud Manager, pressione o botão **...** ao lado do seu ambiente. Esta ação abre a página de perfis de produto
   * Agora clique no perfil **Usuários de AEM** para mostrar uma lista dos usuários
   * Clique na guia **Credenciais da API**, localize o usuário da conta técnica apropriado e exclua-o
2. Entre em contato com o suporte ao cliente e solicite a exclusão das credenciais de serviço desse ambiente específico
3. Por fim, você pode gerar as credenciais novamente, conforme descrito nesta documentação. Verifique também se o novo usuário da conta técnica criado tem as permissões apropriadas.
