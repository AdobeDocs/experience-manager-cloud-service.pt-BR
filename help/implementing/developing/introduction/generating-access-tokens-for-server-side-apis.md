---
title: Geração de tokens de acesso para APIs do lado do servidor
description: Saiba como facilitar a comunicação entre um servidor de terceiros e o AEM as a Cloud Service gerando um token JWT seguro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '2089'
ht-degree: 0%

---

# Geração de tokens de acesso para APIs do lado do servidor {#generating-access-tokens-for-server-side-apis}

Algumas arquiteturas dependem de fazer chamadas para o AEM as a Cloud Service de um aplicativo hospedado em um servidor fora da infraestrutura do AEM. Por exemplo, um aplicativo móvel que chama um servidor, o que então faz solicitações de API ao AEM as a Cloud Service.

O fluxo de servidor para servidor é descrito abaixo, juntamente com um fluxo simplificado para desenvolvimento. O AS A CLOUD SERVICE AEM [Console do desenvolvedor](development-guidelines.md#crxde-lite-and-developer-console) é usado para gerar tokens necessários para o processo de autenticação.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## O fluxo de servidor para servidor {#the-server-to-server-flow}

Usuários com uma função de administrador da organização IMS e que são membros do Perfil de produto Usuários do AEM ou Administradores do AEM no autor do AEM AEM podem gerar um conjunto de credenciais do as a Cloud Service. Cada credencial é uma carga JSON que inclui um certificado (a chave pública), uma chave privada e uma conta técnica que consiste em uma `clientId` e `clientSecret`. Essas credenciais podem ser recuperadas posteriormente por um usuário com a função de administrador do Ambiente as a Cloud Service AEM e devem ser instaladas em um servidor sem AEM e tratadas cuidadosamente como uma chave secreta. Esse arquivo de formato JSON contém todos os dados necessários para integrar com uma API AEM as a Cloud Service. Os dados são usados para criar um token JWT assinado, que é substituído pelo Adobe Identity Management Services (IMS) por um token de acesso IMS. Esse token de acesso pode ser usado como um token de autenticação de portador para fazer solicitações ao AEM as a Cloud Service. O certificado nas credenciais expira após um ano por padrão, mas elas podem ser atualizadas quando necessário, conforme descrito [aqui](#refresh-credentials).

O fluxo de servidor para servidor envolve as seguintes etapas:

* Busque as credenciais do AEM as a Cloud Service no Console do desenvolvedor
* Instale as credenciais do AEM as a Cloud Service em um servidor não-AEM que faz chamadas para o AEM
* Gere um token JWT e troque-o por um token de acesso usando APIs IMS do Adobe
* Chamada da API AEM com o token de acesso como um token de autenticação de portador
* Definir as permissões apropriadas para o usuário da conta técnica no ambiente AEM

### Buscar as credenciais as a Cloud Service do AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Os usuários com acesso ao console do desenvolvedor AEM as a Cloud Service verão a guia Integrações no Console do desenvolvedor para um determinado ambiente. Um usuário com a função de administrador Ambiente as a Cloud Service AEM pode criar, exibir ou gerenciar credenciais.

Clicando **Criar nova conta técnica**, um conjunto de credenciais é criado e inclui a id do cliente, o segredo do cliente, a chave privada, o certificado e a configuração para os níveis de criação e publicação do ambiente, independentemente da seleção do pod.

![Criação de uma nova conta técnica](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

Uma nova guia do navegador é aberta, exibindo as credenciais. Você pode usar essa visualização para baixar as credenciais pressionando o ícone de download ao lado do título do status:

![Baixar credenciais](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

Depois que as credenciais forem criadas, elas aparecerão sob o **Contas técnicas** na guia **Integrações** seção:

![Exibir credenciais](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Os usuários podem exibir as credenciais posteriormente usando a ação Exibir. Além disso, conforme descrito posteriormente neste artigo, os usuários podem editar as credenciais para a mesma conta técnica. Eles fazem essa edição criando uma chave privada ou certificado, para casos em que o certificado deve ser renovado ou revogado.

Usuários com a função de Administrador de ambiente as a Cloud Service do AEM podem criar credenciais posteriormente para contas técnicas adicionais. Essa capacidade é útil quando APIs diferentes têm requisitos de acesso diferentes. Por exemplo, leitura versus leitura-gravação.

>[!NOTE]
>
>Os clientes podem criar até dez contas técnicas, incluindo aquelas já excluídas.

>[!IMPORTANT]
>
>Um administrador de organização IMS (normalmente o mesmo usuário que provisionou o ambiente por meio do Cloud Manager), que também é membro do Perfil de produto Usuários de AEM ou Administradores de AEM no AEM Author, deve acessar primeiro o Console do desenvolvedor. Em seguida, clique em **Criar nova conta técnica** para que as credenciais sejam geradas e recuperadas posteriormente por um usuário com permissões de administrador do ambiente as a Cloud Service do AEM. Se o administrador da organização IMS ainda não tiver criado a conta técnica, uma mensagem informará que ele precisa da função de Administrador da organização IMS.

### Instalar as credenciais do serviço AEM em um servidor não AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

O aplicativo que faz chamadas para AEM deve ser capaz de acessar as credenciais para AEM as a Cloud Service, tratando-o como um segredo.

### Gerar um token JWT e trocá-lo por um token de acesso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Use as credenciais para criar um token JWT em uma chamada para o serviço IMS Adobe para recuperar um token de acesso, que é válido por 24 horas.

As Credenciais de Serviço AEM CS podem ser trocadas por um token de acesso usando bibliotecas de clientes criadas para essa finalidade. As bibliotecas de clientes estão disponíveis no [Repositório GitHub público do Adobe](https://github.com/adobe/aemcs-api-client-lib), que contém orientações mais detalhadas e informações mais recentes.

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

>[!NOTE]
>Se houver várias credenciais, faça referência ao arquivo json apropriado para a chamada de API para AEM que será invocada posteriormente.

### Chamar a API do AEM {#calling-the-aem-api}

Fazer as chamadas apropriadas da API de servidor para servidor para um ambiente AEM as a Cloud Service, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`. Por exemplo, usando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Definir as permissões apropriadas para o usuário da conta técnica no AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Primeiro, um novo perfil de produto deve ser criado no Adobe Admin Console.

1. Acesse a Adobe Admin Console em [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).
1. Pressione a **Gerenciar** no link **Produtos e serviços** à esquerda.
1. Selecionar **AEM as a Cloud Service**.
1. Pressione a **Novo perfil** botão.

   ![Novo perfil](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Nomeie o perfil e pressione **Salvar**.

   ![Salvar perfil](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Selecione o perfil que você criou na lista de perfis.
1. Selecionar **Adicionar usuário**.

   ![Adicionar usuário](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Adicione a conta técnica que você criou (neste caso, `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) e clique em **Salvar**.

   ![Adicionar conta técnica](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. Aguarde 10 minutos para que as alterações entrem em vigor e faça uma chamada de API para AEM com um token de acesso gerado a partir da nova credencial. Como um comando cURL, ele seria representado de forma semelhante a este exemplo:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


Depois de fazer a chamada de API, o perfil de produto aparece como um grupo de usuários na instância de autor do AEM as a Cloud Service, com a conta técnica apropriada como membro desse grupo.

Para verificar essas informações, faça o seguinte:

1. Faça logon na instância de criação.
1. Ir para **Ferramentas** > **Segurança** e, em seguida, clique na guia **Grupos** cartão.
1. Localize o nome do perfil criado na lista de grupos e clique nele:

   ![Perfil do grupo](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. Na janela a seguir, alterne para o **Membros** e verifique se a conta técnica está listada corretamente lá:

   ![Guia Membros](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


Como alternativa, você também pode verificar se a conta técnica aparece na lista do usuário executando as etapas abaixo na instância do autor:

1. Ir para **Ferramentas** > **Segurança** > **Usuários**.
1. Verifique se sua conta técnica é a lista de usuários e selecione-a.
1. Clique em **Grupos** para verificar se o usuário faz parte do grupo que corresponde ao perfil do produto. Esse usuário também é membro de alguns outros grupos, incluindo Contribuidores:

   ![Associação de grupo](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Antes de meados de 2023, antes que fosse possível criar várias credenciais, os clientes não eram orientados a criar um perfil de produto no Adobe Admin Console. Dessa forma, a conta técnica não estava associada a um grupo diferente de &quot;Contribuidores&quot; na instância as a Cloud Service do AEM. Por uma questão de consistência, é recomendável que, para essa conta técnica, você crie um perfil de produto no Adobe Admin Console conforme descrito acima e adicione a conta técnica existente a esse grupo.

<u>**Definir as permissões de grupo apropriadas**</u>

Por fim, configure o grupo com as permissões apropriadas necessárias para que você possa chamar ou bloquear suas APIs adequadamente.

1. Faça logon na instância de autor apropriada e navegue até **Configurações** > **Segurança** > **Permissões**
1. Procure o nome do grupo correspondente ao perfil do produto no painel esquerdo (nesse caso, APIs somente leitura) e selecione-o:

   ![Pesquisar por grupo](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Clique no botão Edit na seguinte janela:

   ![Editar permissões](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Modifique as permissões adequadamente e clique em **Salvar**

   ![Confirmar edição de permissões](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Saiba mais sobre o Sistema Adobe Identity Management (IMS) e os usuários e grupos de AEM. Consulte a [documentação](/help/security/ims-support.md).

## Fluxo do desenvolvedor {#developer-flow}

Os desenvolvedores provavelmente desejam testar usando uma instância de desenvolvimento de seu aplicativo não AEM (em execução no laptop ou hospedado) que faz solicitações a um ambiente de desenvolvimento as a Cloud Service AEM. No entanto, como os desenvolvedores não têm necessariamente permissões de função de administrador do IMS, o Adobe não pode supor que podem gerar o portador JWT descrito no fluxo regular de servidor para servidor. Portanto, o Adobe fornece um mecanismo para que um desenvolvedor gere um token de acesso diretamente que pode ser usado em solicitações a ambientes no AEM as a Cloud Service aos quais ele tem acesso.

Consulte a [Documentação das Diretrizes do desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obter informações sobre as permissões necessárias para usar o console do desenvolvedor do AEM as a Cloud Service.

>[!NOTE]
>
>O token de acesso de desenvolvimento local é válido por no máximo 24 horas após as quais deve ser gerado novamente usando o mesmo método.

Os desenvolvedores podem usar esse token para fazer chamadas de seu aplicativo de teste não-AEM para um ambiente as a Cloud Service AEM. Normalmente, o desenvolvedor usa esse token com o aplicativo não-AEM em seu próprio notebook. Além disso, o AEM as a Cloud normalmente é um ambiente de não produção.

O fluxo do desenvolvedor envolve as seguintes etapas:

* Gerar um token de acesso no Console do desenvolvedor
* Chame o aplicativo AEM com o token de acesso.

Os desenvolvedores também podem fazer chamadas de API para um projeto AEM em execução em sua máquina local, caso em que um token de acesso não é necessário.

### Gerar o token de acesso {#generating-the-access-token}

1. Vá para a **Token local** em **Integrações**
1. Clique em **Obter token de desenvolvimento local** no Console do desenvolvedor, para que você possa gerar um token de acesso.

### Chamar o aplicativo AEM com um token de acesso {#call-the-aem-application-with-an-access-token}

Fazer as chamadas de API de servidor para servidor apropriadas do aplicativo não-AEM para um ambiente AEM as a Cloud Service, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`.

## Atualizar credenciais {#refresh-credentials}

Por padrão, as credenciais no AEM as a Cloud Service expiram após um ano. Para garantir a continuidade do serviço, os desenvolvedores têm a opção de atualizar as credenciais, estendendo sua disponibilidade por mais um ano.

Para obter essa extensão de atualização, faça o seguinte:

* Use o **Adicionar certificado** botão em **Integrações** - **Contas técnicas** no Console do desenvolvedor, conforme mostrado abaixo

  ![Atualização de credencial](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* Depois de pressionar o botão, um conjunto de credenciais que inclui um novo certificado é gerado. Instale as novas credenciais em seu servidor off-AEM e verifique se a conectividade foi a esperada, sem remover as credenciais antigas.
* Certifique-se de que as novas credenciais sejam usadas em vez das antigas ao gerar o token de acesso.
* Opcionalmente, revogue (e exclua) o certificado anterior para que ele não possa mais ser usado para autenticação com o AEM as a Cloud Service.

## Revogação de credenciais {#credentials-revocation}

Se a chave privada estiver comprometida, você deverá criar credenciais com um novo certificado e uma nova chave privada. Depois que sua aplicação usar as novas credenciais para gerar tokens de acesso, você poderá revogar e deletar os certificados antigos fazendo o seguinte:

1. Primeiro, adicione a nova chave. Essa chave gera credenciais com uma nova chave privada e um novo certificado. A nova chave privada está marcada na interface como **atual** e, portanto, é usado para todas as novas credenciais para essa conta técnica a partir de agora. As credenciais associadas às chaves privadas mais antigas ainda serão válidas até serem revogadas. Para obter essa revogação, selecione os três pontos (**..**) na sua conta técnica atual, em seguida selecione **Adicionar nova chave privada**:

   ![Adicionar nova chave privada](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Selecionar **Adicionar** no prompt a seguir:

   ![Confirmar adição de nova chave privada](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   Uma nova guia de navegação com as novas credenciais é aberta e a interface de usuário é atualizada para mostrar as duas chaves privadas com a nova marcada como **atual**:

   ![Chaves privadas na interface](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. Instale as novas credenciais no servidor não AEM e verifique se a conectividade funciona conforme esperado. Consulte [Seção Fluxo de Servidor para Servidor](#the-server-to-server-flow) para obter detalhes.
1. Revogue o certificado antigo selecionando os três pontos (**..**&#x200B;à direita do certificado e selecionando **Revogar**:

   ![Revogar certificado](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   Em seguida, confirme a revogação no prompt a seguir pressionando a tecla **Revogar** botão:

   ![Revogar confirmação do certificado](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Por fim, exclua o certificado comprometido.
