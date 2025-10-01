---
title: Geração de tokens de acesso para APIs do lado do servidor
description: Saiba como facilitar a comunicação entre um servidor de terceiros e o AEM as a Cloud Service gerando um token JWT seguro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 22216d2c045b79b7da13f09ecbe1d56a91f604df
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 0%

---

# Geração de tokens de acesso para APIs do lado do servidor {#generating-access-tokens-for-server-side-apis}

Algumas arquiteturas dependem de fazer chamadas para o AEM as a Cloud Service a partir de um aplicativo hospedado em um servidor fora da infraestrutura do AEM. Por exemplo, um aplicativo móvel que chama um servidor, que faz solicitações de API para o AEM as a Cloud Service.

O fluxo de servidor para servidor é descrito abaixo, juntamente com um fluxo simplificado para desenvolvimento. O AEM as a Cloud Service [Developer Console](development-guidelines.md#crxde-lite-and-developer-console) é usado para gerar tokens necessários para o processo de autenticação.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=pt-BR#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## O fluxo de servidor para servidor {#the-server-to-server-flow}

Usuários com uma função de administrador da organização IMS e que são membros do Perfil de produto Usuários do AEM ou Administradores do AEM no AEM Author podem gerar um conjunto de credenciais do AEM as a Cloud Service. Cada credencial é uma carga JSON que inclui um certificado (a chave pública), uma chave privada e uma conta técnica que consiste em um `clientId` e `clientSecret`. Essas credenciais podem ser recuperadas posteriormente por um usuário com a função de administrador de ambiente do AEM as a Cloud Service e devem ser instaladas em um servidor que não seja da AEM e tratadas cuidadosamente como uma chave secreta. Esse arquivo de formato JSON contém todos os dados necessários para integrar a uma API do AEM as a Cloud Service. Os dados são usados para criar um token JWT assinado, que é substituído pelo Adobe Identity Management Services (IMS) por um token de acesso IMS. Esse token de acesso pode ser usado como um token de autenticação de portador para fazer solicitações à AEM as a Cloud Service. Por padrão, o certificado nas credenciais expira após um ano, mas elas podem ser atualizadas quando necessário. Consulte [Atualizar Credenciais](#refresh-credentials).

O fluxo de servidor para servidor envolve as seguintes etapas:

* Buscar as credenciais no AEM as a Cloud Service na Developer Console
* Instale as credenciais do AEM as a Cloud Service em um servidor que não seja da AEM que esteja fazendo chamadas para o AEM
* Gerar um token JWT e trocá-lo por um token de acesso usando as APIs IMS do Adobe
* Chamada da API do AEM com o token de acesso como um token de autenticação de portador
* Definir as permissões apropriadas para o usuário da conta técnica no ambiente do AEM

### Buscar as credenciais do AEM as a Cloud Service {#fetch-the-aem-as-a-cloud-service-credentials}

Os usuários com acesso ao console do desenvolvedor do AEM as a Cloud Service veem a guia Integrações no Developer Console para um determinado ambiente. Um usuário com a função de administrador do Ambiente AEM as a Cloud Service pode criar, exibir ou gerenciar credenciais.

Ao clicar em **Criar nova conta técnica**, é criado um conjunto de credenciais que inclui a ID do cliente, o segredo do cliente, a chave privada, o certificado e a configuração para os níveis de criação e publicação do ambiente, independentemente da seleção do pod.

![Criando uma nova Conta Técnica](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

Uma nova guia do navegador é aberta, exibindo as credenciais. Você pode usar essa visualização para baixar as credenciais pressionando o ícone de download ao lado do título do status:

![Baixar credenciais](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

Após as credenciais serem criadas, elas aparecerão na guia **Contas técnicas** na seção **Integrações**:

![Exibir Credenciais](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Os usuários podem exibir as credenciais posteriormente usando a ação Exibir. Além disso, conforme descrito posteriormente neste artigo, os usuários podem editar as credenciais para a mesma conta técnica. Eles fazem essa edição criando uma chave privada ou certificado, para casos em que o certificado deve ser renovado ou revogado.

Usuários com a função de Administrador de ambiente do AEM as a Cloud Service podem criar credenciais posteriormente para contas técnicas adicionais. Essa capacidade é útil quando APIs diferentes têm requisitos de acesso diferentes. Por exemplo, leitura versus leitura-gravação.

>[!NOTE]
>
>Os clientes podem criar até dez contas técnicas, incluindo aquelas já excluídas.

>[!IMPORTANT]
>
>Um administrador de organização IMS (normalmente o mesmo usuário que provisionou o ambiente por meio do Cloud Manager), que também é membro do Perfil de produto Usuários do AEM ou Administradores do AEM no AEM Author, deve acessar primeiro o Developer Console. Em seguida, clique em **Criar nova conta técnica** para que as credenciais sejam geradas e recuperadas posteriormente por um usuário com permissões de administrador para o ambiente do AEM as a Cloud Service. Se o administrador da organização IMS ainda não tiver criado a conta técnica, uma mensagem informará que ele precisa da função de Administrador da organização IMS.

### Instalar as credenciais de serviço do AEM em um servidor que não seja da AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

O aplicativo que faz chamadas para o AEM deve poder acessar as credenciais do AEM as a Cloud Service, tratando-o como um segredo.

### Gerar um token JWT e trocá-lo por um token de acesso {#generate-a-jwt-token-and-exchange-it-for-an-access-token}

Use as credenciais para criar um token JWT em uma chamada ao serviço IMS da Adobe para recuperar um token de acesso, válido por 24 horas.

As Credenciais do AEM CS Service podem ser trocadas por um token de acesso usando amostras de código projetadas para essa finalidade. O código de exemplo está disponível no [repositório público do GitHub da Adobe](https://github.com/adobe/aemcs-api-client-lib), que contém exemplos de código que você pode copiar e adaptar para seus próprios projetos. Observe que esse repositório contém exemplos de código para referência e não é mantido como uma dependência de biblioteca pronta para produção.

```
/*jshint node:true */
"use strict";

const fs = require('fs');
// Sample code adapted from Adobe's GitHub repository
const exchange = require("./your-local-aemcs-client"); // Copy and adapt the code from the GitHub repository

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
>Se houver várias credenciais, faça referência ao arquivo json apropriado para a chamada de API para o AEM que será invocada posteriormente.

### Chamada da API do AEM {#calling-the-aem-api}

Fazer as chamadas de API de servidor para servidor apropriadas para um ambiente do AEM as a Cloud Service, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`. Por exemplo, usando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Definir as permissões apropriadas para o usuário da conta técnica no AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Primeiro, um novo perfil de produto deve ser criado no Adobe Admin Console.

1. Vá para a Adobe Admin Console em [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).
1. Pressione o link **Gerenciar** na coluna **Produtos e Serviços** à esquerda.
1. Selecione **AEM as a Cloud Service**.
1. Pressione o botão **Novo Perfil**.

   ![Novo Perfil](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Nomeie o perfil e pressione **Salvar**.

   ![Salvar Perfil](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Selecione o perfil que você criou na lista de perfis.
1. Selecione **Adicionar Usuário**.

   ![Adicionar usuário](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Adicione a conta técnica que você criou (neste caso, `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) e clique em **Salvar**.

   ![Adicionar Conta Técnica](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. Aguarde 10 minutos para que as alterações entrem em vigor e faça uma chamada de API para o AEM com um token de acesso gerado a partir da nova credencial. Como um comando cURL, ele seria representado de forma semelhante a este exemplo:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


Depois de fazer a chamada de API, o perfil de produto aparece como um grupo de usuários na instância de autor do AEM as a Cloud Service, com a conta técnica apropriada como membro desse grupo.

Para verificar essas informações, faça o seguinte:

1. Faça logon na instância de criação.
1. Vá para **Ferramentas** > **Segurança** e clique no cartão **Grupos**.
1. Localize o nome do perfil criado na lista de grupos e clique nele:

   ![Perfil do Grupo](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. Na janela a seguir, alterne para a guia **Membros** e verifique se a conta técnica está listada corretamente lá:

   ![Guia Membros](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


Como alternativa, você também pode verificar se a conta técnica aparece na lista do usuário executando as etapas abaixo na instância do autor:

1. Vá para **Ferramentas** > **Segurança** > **Usuários**.
1. Verifique se sua conta técnica é a lista de usuários e selecione-a.
1. Clique na guia **Grupos** para verificar se o usuário faz parte do grupo que corresponde ao perfil do produto. Esse usuário também é membro de alguns outros grupos, incluindo Contribuidores:

   ![Associação de Grupo](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Antes de meados de 2023, antes que fosse possível criar várias credenciais, os clientes não eram orientados a criar um perfil de produto no Adobe Admin Console. Dessa forma, a conta técnica não estava associada a um grupo diferente de &quot;Contribuidores&quot; na instância do AEM as a Cloud Service. Por uma questão de consistência, é recomendável que, para essa conta técnica, você crie um perfil de produto no Adobe Admin Console conforme descrito acima e adicione a conta técnica existente a esse grupo.

<u>**Definir as Permissões de Grupo Apropriadas**</u>

Por fim, configure o grupo com as permissões apropriadas necessárias para que você possa chamar ou bloquear suas APIs adequadamente.

1. Faça logon na instância de autor apropriada e navegue até **Configurações** > **Segurança** > **Permissões**
1. Procure o nome do grupo correspondente ao perfil do produto no painel esquerdo (nesse caso, APIs somente leitura) e selecione-o:

   ![Pesquisar Grupo](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Clique no botão Edit na seguinte janela:

   ![Editar permissões](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Modifique as permissões adequadamente e clique em **Salvar**

   ![Confirmar edição de permissões](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Saiba mais sobre o Adobe Identity Management System (IMS) e os usuários e grupos da AEM. Consulte a [documentação](/help/security/ims-support.md).

## Fluxo do desenvolvedor {#developer-flow}

Os desenvolvedores provavelmente desejam testar usando uma instância de desenvolvimento de seu aplicativo que não seja da AEM (em execução no laptop ou hospedado) que faz solicitações a um ambiente de desenvolvimento do AEM as a Cloud Service. No entanto, como os desenvolvedores não têm necessariamente permissões de função de administrador do IMS, a Adobe não pode supor que podem gerar o portador JWT descrito no fluxo regular de servidor para servidor. Portanto, o Adobe fornece um mecanismo para que um desenvolvedor gere um token de acesso diretamente que pode ser usado em solicitações a ambientes no AEM as a Cloud Service aos quais ele tem acesso.

Consulte a [documentação das Diretrizes do desenvolvedor](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console) para obter informações sobre as permissões necessárias para usar o console do desenvolvedor do AEM as a Cloud Service.

>[!NOTE]
>
>O token de acesso de desenvolvimento local é válido por no máximo 24 horas após as quais deve ser gerado novamente usando o mesmo método.

Os desenvolvedores podem usar esse token para fazer chamadas de seus aplicativos de teste que não sejam da AEM para um ambiente AEM as a Cloud Service. Normalmente, o desenvolvedor usa esse token com o aplicativo que não é da AEM em seu próprio notebook. Além disso, o AEM as a Cloud normalmente é um ambiente de não produção.

O fluxo do desenvolvedor envolve as seguintes etapas:

* Gerar um token de acesso pela Developer Console
* Chame o aplicativo do AEM com o token de acesso.

Os desenvolvedores também podem fazer chamadas de API para um projeto do AEM em execução em sua máquina local, caso em que um token de acesso não é necessário.

### Gerar o token de acesso {#generating-the-access-token}

1. Vá para o **Token local** em **Integrações**
1. Clique em **Obter token de desenvolvimento local** na Developer Console para que você possa gerar um token de acesso.

### Chamar o aplicativo AEM com um token de acesso {#call-the-aem-application-with-an-access-token}

Fazer as chamadas de API de servidor para servidor apropriadas do aplicativo que não seja o AEM para um ambiente AEM as a Cloud Service, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`.

## Atualizar credenciais {#refresh-credentials}

Por padrão, as credenciais no AEM as a Cloud Service expiram após um ano. Para garantir a continuidade do serviço, os desenvolvedores têm a opção de atualizar as credenciais, estendendo sua disponibilidade por mais um ano.

Para obter essa extensão de atualização, faça o seguinte:

* Use o botão **Adicionar certificado** em **Integrações** - **Contas técnicas** na Developer Console, conforme mostrado abaixo

  ![Atualização de credencial](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* Depois de pressionar o botão, um conjunto de credenciais que inclui um novo certificado é gerado. Instale as novas credenciais em seu servidor fora do AEM e verifique se a conectividade está conforme o esperado, sem remover as credenciais antigas.
* Certifique-se de que as novas credenciais sejam usadas em vez das antigas ao gerar o token de acesso.
* Opcionalmente, revogue (e exclua) o certificado anterior para que ele não possa mais ser usado para autenticação com o AEM as a Cloud Service.

## Revogação de credenciais {#credentials-revocation}

Se a chave privada estiver comprometida, você deverá criar credenciais com um novo certificado e uma nova chave privada. Depois que sua aplicação usar as novas credenciais para gerar tokens de acesso, você poderá revogar e deletar os certificados antigos fazendo o seguinte:

1. Primeiro, adicione a nova chave. Essa chave gera credenciais com uma nova chave privada e um novo certificado. A nova chave privada está marcada na interface do usuário como **atual** e, portanto, é usada para todas as novas credenciais desta conta técnica a partir de agora. As credenciais associadas às chaves privadas mais antigas ainda serão válidas até serem revogadas. Para obter essa revogação, selecione os três pontos (**...**) na conta técnica atual e selecione **Adicionar nova chave privada**:

   ![Adicionar nova chave privada](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Selecione **Adicionar** no prompt a seguir:

   ![Confirmar adição de nova chave privada](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   Uma nova guia de navegação com as novas credenciais é aberta e a interface de usuário é atualizada para mostrar as duas chaves privadas com a nova marcada como **atual**:

   ![Chaves privadas na interface do usuário](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. Instale as novas credenciais no servidor que não seja da AEM e verifique se a conectividade funciona conforme o esperado. Consulte a [seção Fluxo de Servidor para Servidor](#the-server-to-server-flow) para obter detalhes.
1. Revogue o certificado antigo selecionando os três pontos (**...**) à direita do certificado e selecionando **Revogar**:

   ![Revogar certificado](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   Em seguida, confirme a revogação no prompt a seguir pressionando o botão **Revogar**:

   ![Revogar confirmação de certificado](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Por fim, exclua o certificado comprometido.
