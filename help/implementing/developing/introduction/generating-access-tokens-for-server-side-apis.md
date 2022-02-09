---
title: Geração de tokens de acesso para APIs do lado do servidor
description: Saiba como facilitar a comunicação entre um servidor de terceiros e AEM as a Cloud Service gerando um token JWT seguro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: c4f4ce968c17db1f1185ce7be9cad833eaf0b91b
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 0%

---

# Introdução {#introduction}

Algumas arquiteturas dependem de fazer chamadas para AEM as a Cloud Service de um aplicativo hospedado em um servidor fora de AEM infraestrutura. Por exemplo, um aplicativo móvel que chama um servidor, que faz solicitações de API para AEM as a Cloud Service.

O fluxo de servidor para servidor é descrito abaixo, juntamente com um fluxo simplificado para desenvolvimento. O AEM as a Cloud Service [Console do desenvolvedor](development-guidelines.md#crxde-lite-and-developer-console) é usada para gerar tokens necessários para o processo de autenticação.

>[!NOTE]
>
>Além dessa documentação, você também pode consultar o tutorial sobre [Autenticação por token para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

## O fluxo de servidor para servidor {#the-server-to-server-flow}

Um usuário com uma função de administrador de organização IMS e que também seja membro do Perfil de produto Usuários ou Administradores de AEM no Autor do AEM pode gerar uma credencial as a Cloud Service AEM. Essa credencial pode ser recuperada posteriormente por um usuário com a função de administrador do Ambiente as a Cloud Service AEM e deve ser instalada no servidor e precisa ser tratada cuidadosamente como uma chave secreta. Esse arquivo de formato JSON contém todos os dados necessários para integrar com uma AEM API as a Cloud Service. Os dados são usados para criar um token JWT assinado, que é trocado por IMS para um token de acesso IMS. Esse token de acesso pode ser usado como um token de autenticação Portador para fazer solicitações para AEM as a Cloud Service. As credenciais expiram após um ano por padrão, mas podem ser atualizadas quando necessário, conforme descrito [here](#refresh-credentials).

O fluxo de servidor para servidor envolve as seguintes etapas:

* Busque as credenciais as a Cloud Service do AEM no Console do desenvolvedor
* Instale as credenciais as a Cloud Service AEM em um servidor não AEM que faz chamadas para AEM
* Gere um token JWT e troque esse token de acesso usando as APIs IMS do Adobe
* Chamar a API de AEM com o token de acesso como um token de autenticação do portador
* Defina as permissões apropriadas para o usuário da conta técnica no ambiente AEM

### Buscar as credenciais as a Cloud Service AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Os usuários com acesso ao console do desenvolvedor AEM as a Cloud Service verão a guia integrações no Console do desenvolvedor para um certo ambiente, bem como dois botões. Um usuário com a função de administrador AEM Ambiente as a Cloud Service pode clicar no botão **Gerar Credenciais de Serviço** para gerar e exibir o json de credenciais de serviço, que conterá todas as informações necessárias para o servidor não AEM, incluindo id do cliente, segredo do cliente, chave privada, certificado e configuração para os níveis de criação e publicação do ambiente, independentemente da seleção do pod.

![Geração de JWT](assets/JWTtoken3.png)

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

Depois de serem geradas, as credenciais podem ser recuperadas em uma data posterior, pressionando a tecla **Obter Credenciais de Serviço** no mesmo local.

>[!IMPORTANT]
>
>Um administrador da organização do IMS (normalmente o mesmo usuário que provisionou o ambiente pelo Cloud Manager), que também deve ser membro do Perfil de produto AEM Usuários ou Administradores AEM no AEM Author, deve primeiro acessar o Console do desenvolvedor e clicar no **Gerar Credenciais de Serviço** para que as credenciais sejam geradas e recuperadas posteriormente por um usuário com permissões de administrador no ambiente as a Cloud Service do AEM. Se o administrador da organização IMS não tiver feito isso, uma mensagem informará que ele precisa da função IMS org Administrator.

### Instalar as credenciais do serviço de AEM em um servidor não AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

O aplicativo que não é AEM e faz chamadas para AEM deve poder acessar as credenciais as a Cloud Service do AEM, tratando-o como um segredo.

### Gere um token JWT e troque-o por um token de acesso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Use o token JWT em uma chamada para recuperar o serviço IMS para recuperar um token de acesso, que é válido por 24 horas.

As Credenciais do serviço da CS AEM podem ser trocadas por um token de acesso usando bibliotecas de clientes projetadas para essa finalidade. As bibliotecas de clientes estão disponíveis em [Repositório GitHub](https://github.com/adobe/aemcs-api-client-lib), que contém orientações mais detalhadas e informações mais recentes.

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

A mesma troca pode ser executada em qualquer idioma capaz de gerar um token JWT assinado com o formato correto e chamar as APIs do IMS Token Exchange.

O token de acesso definirá quando expirar, que normalmente é de 24 horas. Existe um código de amostra no repositório Git para gerenciar um token de acesso e atualizá-lo antes que ele expire.

### Chamar a API AEM {#calling-the-aem-api}

Faça as chamadas de API de servidor para servidor apropriadas em um ambiente as a Cloud Service AEM, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`. Por exemplo, usando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Defina as permissões apropriadas para o usuário da conta técnica no AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Depois que o usuário da conta técnica é criado no AEM (isso ocorre após a primeira solicitação com o token de acesso correspondente), o usuário da conta técnica deve ter permissão adequada **em** AEM.

Observe que, por padrão, no serviço Autor do AEM, o usuário da conta técnica é adicionado ao grupo de usuários Contribuidores , que fornece AEM de acesso de leitura.

Este usuário da conta técnica no AEM pode receber permissões usando os métodos habituais.

## Fluxo do desenvolvedor {#developer-flow}

Os desenvolvedores provavelmente desejarão testar usando uma instância de desenvolvimento de seu aplicativo não AEM (em execução no laptop ou hospedado) que faz solicitações para um ambiente de desenvolvimento AEM desenvolvimento as a Cloud Service. No entanto, como os desenvolvedores não têm necessariamente permissões de função de administrador IMS, não podemos assumir que podem gerar o portador JWT descrito no fluxo regular de servidor para servidor. Dessa forma, fornecemos um mecanismo para um desenvolvedor gerar um token de acesso diretamente que pode ser usado em solicitações para AEM ambientes as a Cloud Service aos quais ele tem acesso.

Consulte a [Documentação das diretrizes do desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obter informações sobre as permissões necessárias para usar o console de desenvolvedor AEM as a Cloud Service.

>[!NOTE]
>
>O token de acesso de desenvolvimento local é válido por um máximo de 24 horas depois do qual deve ser gerado novamente usando o mesmo método.

Os desenvolvedores podem usar esse token para fazer chamadas de seu aplicativo de teste que não seja AEM para um ambiente AEM as a Cloud Service. Normalmente, o desenvolvedor usará esse token com o aplicativo que não é AEM em seu próprio laptop. Além disso, o AEM as a Cloud normalmente é um ambiente de não produção.

O fluxo do desenvolvedor envolve as seguintes etapas:

* Gerar um token de acesso pelo Console do desenvolvedor
* Chame o aplicativo AEM com o token de acesso.

Os desenvolvedores também podem fazer chamadas de API para um projeto AEM em execução em sua máquina local, caso em que um token de acesso não é necessário.

### Geração do token de acesso {#generating-the-access-token}

Clique no botão **Obter Token de Desenvolvimento Local** no Console do desenvolvedor para gerar um token de acesso.

### Chame e AEM aplicativo com um token de acesso {#call-the-aem-application-with-an-access-token}

Faça as chamadas de API de servidor para servidor apropriadas do aplicativo que não é AEM para um ambiente as a Cloud Service AEM, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`.

## Atualizar Credenciais {#refresh-credentials}

Por padrão, as credenciais as a Cloud Service AEM expiram após um ano. Para garantir a continuidade do serviço, os desenvolvedores têm a opção de atualizar as credenciais, estendendo sua disponibilidade por mais um ano.

Para fazer isso, é possível usar a variável **Atualizar Credenciais do Serviço** do botão **Integrações** no Console do desenvolvedor, conforme mostrado abaixo.

![Atualização de Credenciais](assets/credential-refresh.png)

Depois de pressionar o botão, um novo conjunto de credenciais será gerado. Você pode atualizar seu armazenamento secreto com as novas credenciais e validar que elas funcionam como deveriam.

>[!NOTE]
>
> Depois de clicar no botão **Atualizar Credenciais do Serviço** , as credenciais antigas permanecem registradas até expirarem, mas somente o conjunto mais recente está disponível para ser visualizado no Console do desenvolvedor a qualquer momento.

## Revogação de Credenciais de Serviço {#service-credentials-revocation}

Se as credenciais precisarem ser revogadas, você precisará enviar uma solicitação ao suporte ao cliente usando estas etapas:

1. Desative o usuário da conta técnica do Adobe Admin Console na interface do usuário:
   * No Cloud Manager, pressione a **...** ao lado do ambiente. Isso abrirá a página de perfis de produto
   * Agora, clique no botão **Usuários AEM** , para mostrar uma lista dos usuários
   * Clique no botão **Credenciais da API** , em seguida, encontre o usuário da conta técnica apropriada e exclua-a
2. Entre em contato com o suporte ao cliente e solicite que as credenciais de serviço para esse ambiente específico sejam excluídas
3. Por fim, você pode gerar as credenciais novamente, conforme descrito nesta documentação. Verifique também se o novo usuário da conta técnica criado tem as permissões apropriadas.
