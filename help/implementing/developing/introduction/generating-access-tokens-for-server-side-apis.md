---
title: Geração de tokens de acesso para APIs do lado do servidor
description: Saiba como facilitar a comunicação entre um servidor de terceiros e AEM as a Cloud Service gerando um token JWT seguro
exl-id: 20deaf8f-328e-4cbf-ac68-0a6dd4ebf0c9
source-git-commit: 41458eb1fba12e8ef45a32d3bb6fc5dd732f78ec
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 1%

---

# Geração de tokens de acesso para APIs do lado do servidor {#generating-access-tokens-for-server-side-apis}

>[!AVAILABILITY]
>
>O Adobe está lançando gradualmente os novos recursos de credenciais e de revogação de credenciais descritos neste artigo. Se, ao verificar a guia integrações no console do desenvolvedor de AEM de sua organização, você perceber que a tela é diferente das capturas de tela abaixo, significa que as novas alterações ainda não foram implementadas em sua organização. Nesse caso, consulte o [documentação herdada](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis-legacy.md).

Algumas arquiteturas dependem de fazer chamadas para AEM as a Cloud Service de um aplicativo hospedado em um servidor fora de AEM infraestrutura. Por exemplo, um aplicativo móvel que chama um servidor, que faz solicitações de API para AEM as a Cloud Service.

O fluxo de servidor para servidor é descrito abaixo, juntamente com um fluxo simplificado para desenvolvimento. O AEM as a Cloud Service [Console do desenvolvedor](development-guidelines.md#crxde-lite-and-developer-console) é usada para gerar tokens necessários para o processo de autenticação.

<!-- Alexandru: hiding this until the tutorials reflect the new UI

>[!NOTE]
>
>In addition to this documentation, you can also consult the tutorials on [Token-based authentication for AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication) and [Getting a Login Token for Integrations](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-getting-login-token-integrations.html). -->

## O fluxo de servidor para servidor {#the-server-to-server-flow}

Um usuário com uma função de administrador de organização IMS e que também é membro do Perfil de produto Usuários ou Administradores AEM no AEM Author, pode gerar um conjunto de credenciais as a Cloud Service AEM, cada uma delas é uma carga JSON que inclui um certificado (a chave pública), uma chave privada e uma conta técnica que consiste em um `clientId` e `clientSecret`. Essas credenciais podem ser recuperadas posteriormente por um usuário com a função de administrador do Ambiente as a Cloud Service AEM e devem ser instaladas em um servidor não AEM e tratadas cuidadosamente como uma chave secreta. Esse arquivo de formato JSON contém todos os dados necessários para integrar com uma AEM API as a Cloud Service. Os dados são usados para criar um token JWT assinado, que é trocado com o Adobe Identity Management Services (IMS) para um token de acesso IMS. Esse token de acesso pode ser usado como um token de autenticação Portador para fazer solicitações para AEM as a Cloud Service. O certificado nas credenciais expira após um ano por padrão, mas pode ser atualizado quando necessário, conforme descrito [here](#refresh-credentials).

O fluxo de servidor para servidor envolve as seguintes etapas:

* Busque as credenciais as a Cloud Service do AEM no Console do desenvolvedor
* Instale as credenciais as a Cloud Service AEM em um servidor não AEM que faz chamadas para AEM
* Gere um token JWT e troque esse token de acesso usando as APIs IMS do Adobe
* Chamar a API de AEM com o token de acesso como um token de autenticação do portador
* Defina as permissões apropriadas para o usuário da conta técnica no ambiente AEM

### Buscar as credenciais as a Cloud Service AEM {#fetch-the-aem-as-a-cloud-service-credentials}

Os usuários com acesso ao console do desenvolvedor AEM as a Cloud Service verão a guia integrações no Console do desenvolvedor para um certo ambiente. Um usuário com a função de administrador AEM Ambiente as a Cloud Service pode criar, exibir ou gerenciar credenciais.

Clicar no **Criar nova conta técnica** , será criado um novo conjunto de credenciais que inclui id do cliente, segredo do cliente, chave privada, certificado e configuração para os níveis de criação e publicação do ambiente, independentemente da seleção do pod.

![Criação de uma nova conta técnica](/help/implementing/developing/introduction/assets/s2s-createtechaccount.png)

Uma nova guia do navegador será aberta exibindo as credenciais. Use essa visualização para baixar as credenciais pressionando o ícone de download ao lado do título do status:

![Baixar credenciais](/help/implementing/developing/introduction/assets/s2s-credentialdownload.png)

Depois que as credenciais forem criadas, elas serão exibidas sob a variável **Contas técnicas** na guia no **Integrações** seção:

![Exibir credenciais](/help/implementing/developing/introduction/assets/s2s-viewcredentials.png)

Posteriormente, os usuários podem exibir as credenciais usando a ação Exibir . Além disso, conforme descrito posteriormente no artigo, os usuários podem modificar as credenciais da mesma conta técnica criando uma nova chave privada ou certificado, para casos em que o certificado precisa ser renovado ou revogado.

Os usuários com a função AEM Administrador do ambiente as a Cloud Service poderão, posteriormente, criar novas credenciais para contas técnicas adicionais. Isso é útil quando diferentes APIs têm requisitos de acesso diferentes. Por exemplo, ler versus ler-gravar.

>[!NOTE]
>
>Os clientes podem criar até 10 contas técnicas, incluindo aquelas que já foram excluídas.

>[!IMPORTANT]
>
>Um administrador da organização do IMS (normalmente o mesmo usuário que provisionou o ambiente pelo Cloud Manager), que também deve ser membro do Perfil de produto AEM Usuários ou Administradores AEM no AEM Author, deve primeiro acessar o Console do desenvolvedor e clicar no **Criar nova conta técnica** para que as credenciais sejam geradas e recuperadas posteriormente por um usuário com permissões de administrador no ambiente as a Cloud Service do AEM. Se o administrador da organização IMS não tiver feito isso, uma mensagem informará que ele precisa da função IMS org Administrator.

### Instalar as credenciais do serviço de AEM em um servidor não AEM {#install-the-aem-service-credentials-on-a-non-aem-server}

O aplicativo que faz chamadas para AEM deve poder acessar as credenciais as a Cloud Service AEM, tratando-as como um segredo.

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

>[!NOTE]
>Se houver várias credenciais, certifique-se de fazer referência ao arquivo json apropriado para a chamada da API para AEM que será invocada posteriormente.

### Chamar a API AEM {#calling-the-aem-api}

Faça as chamadas de API de servidor para servidor apropriadas em um ambiente as a Cloud Service AEM, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`. Por exemplo, usando `curl`:

```curlc
curl -H "Authorization: Bearer <your_ims_access_token>" https://author-p123123-e23423423.adobeaemcloud.com/content/dam.json
```

### Defina as permissões apropriadas para o usuário da conta técnica no AEM {#set-the-appropriate-permissions-for-the-technical-account-user-in-aem}

Primeiro, um novo perfil de produto precisa ser criado na Adobe Admin Console. Você pode fazer isso seguindo estas etapas:

1. Acesse a Adobe Admin Console em [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/)
1. Pressione a tecla **Gerenciar** sob o **Produtos e serviços** à esquerda.
1. Selecionar **AEM as a Cloud Service**
1. Pressione a tecla **Novo perfil** botão

   ![Novo perfil](/help/implementing/developing/introduction/assets/s2s-newproductprofile.png)

1. Nomeie o perfil e pressione **Salvar**

   ![Salvar perfil](/help/implementing/developing/introduction/assets/s2s-saveprofile.png)

1. Selecione o perfil que você acabou de criar na lista de perfis
1. Pressione a tecla **Adicionar usuário** botão

   ![Adicionar usuário](/help/implementing/developing/introduction/assets/s2s-addusers.png)

1. Adicionar a conta técnica que acabou de criar (neste caso `84b2c3a2-d60a-40dc-84cb-e16b786c1673@techacct.adobe.com`) e pressione **Salvar**

   ![Adicionar conta técnica](/help/implementing/developing/introduction/assets/s2s-addtechaccount.png)

1. Aguarde 10 minutos para que as alterações entrem em vigor e faça uma chamada de API para AEM com um token de acesso gerado a partir da nova credencial. Como um comando cURL, ele seria representado de forma semelhante a este exemplo:

   `curl -H "Authorization: Bearer <access_token>" https://author-pXXXXX-eXXXXX.adobeaemcloud.net/content/dam.json `


Depois de fazer a chamada da API, o perfil de produto será exibido como um grupo de usuários na instância de autor AEM as a Cloud Service, com a conta técnica apropriada como membro desse grupo.

Para verificar isso, é necessário:

1. Faça logon na instância do autor
1. Ir para **Ferramentas** - **Segurança** e clique no botão **Grupos** cartão
1. Localize o nome do perfil que você criou na lista de grupos e clique nele:

   ![Perfil de grupo](/help/implementing/developing/introduction/assets/s2s-groupprofile.png)

1. Na janela a seguir, passe para a guia **Membros** e verifique se a conta técnica está listada corretamente:

   ![Guia Membros](/help/implementing/developing/introduction/assets/s2s-techaccountmembers.png)


Como alternativa, você também pode verificar se a conta técnica aparece na lista de usuários executando as etapas abaixo na instância do autor:

1. Ir para **Ferramentas** - **Segurança** - **Usuários**
1. Verifique se sua conta técnica é a lista de usuários e clique nela
1. Clique no botão **Grupos** para verificar se o usuário faz parte do grupo que corresponde ao seu perfil de produto. Esse usuário também é membro de um punhado de outros grupos, incluindo Contribuidores:

   ![Associação de Grupo](/help/implementing/developing/introduction/assets/s2s-groupmembership.png)

>[!NOTE]
>
>Antes de meados de 2023, antes de ser possível criar várias credenciais, os clientes não eram guiados para criar um perfil de produto no Admin Console do Adobe e, portanto, a conta técnica não era associada a um grupo diferente de &quot;Contribuidores&quot; na instância as a Cloud Service do AEM. Por uma questão de consistência, é recomendável que, para essa conta técnica, você crie um novo perfil de produto na Adobe Admin Console, conforme descrito acima, e adicione a conta técnica existente a esse grupo.

<u>**Definir as permissões do grupo apropriado**</u>

Por fim, configure o grupo com as permissões apropriadas necessárias para chamar ou bloquear suas APIs adequadamente. Você pode fazer isso ao:

1. Fazer logon na instância apropriada do autor e acessar **Configurações** - **Segurança** - **Permissões**
1. Procure o nome do grupo correspondente ao perfil do produto no painel esquerdo (neste caso, APIs somente leitura) e clique nele:

   ![Procurar Grupo](/help/implementing/developing/introduction/assets/s2s-searchforgroup.png)

1. Clique no botão Editar na seguinte janela:

   ![Editar permissões](/help/implementing/developing/introduction/assets/s2s-editpermissions.png) 

1. Modifique as permissões adequadamente e clique em **Salvar**

   ![Confirmar edição de permissões](/help/implementing/developing/introduction/assets/s2s-confirmeditpermissions.png)

>[!INFO]
>
>Saiba mais sobre o Adobe Identity Management System (IMS) e AEM usuários e grupos consultando o [documentação](/help/security/ims-support.md).

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

1. Vá para o **Token local** under **Integrações**
1. Clique no botão **Obter Token de Desenvolvimento Local** no Console do desenvolvedor para gerar um token de acesso.

### Chame o aplicativo AEM com um token de acesso {#call-the-aem-application-with-an-access-token}

Faça as chamadas de API de servidor para servidor apropriadas do aplicativo que não é AEM para um ambiente as a Cloud Service AEM, incluindo o token de acesso no cabeçalho. Portanto, para o cabeçalho &quot;Autorização&quot;, use o valor `"Bearer <access_token>"`.

## Atualizar Credenciais {#refresh-credentials}

Por padrão, as credenciais as a Cloud Service AEM expiram após um ano. Para garantir a continuidade do serviço, os desenvolvedores têm a opção de atualizar as credenciais, estendendo sua disponibilidade por mais um ano.

Para isso, é possível:

* Use o **Adicionar certificado** botão abaixo **Integrações** - **Contas técnicas** no Console do desenvolvedor, como mostrado abaixo

   ![Atualização de Credenciais](/help/implementing/developing/introduction/assets/s2s-credentialrefresh.png)

* Depois de pressionar o botão, um conjunto de credenciais que inclui um novo certificado será gerado. Instale as novas credenciais em seu servidor off-AEM e verifique se a conectividade está conforme o esperado, sem remover as credenciais antigas 
* Certifique-se de que as novas credenciais sejam usadas em vez das antigas ao gerar o token de acesso
* Como opção, revogue (e exclua) o certificado anterior para que ele não possa mais ser usado para autenticar com AEM as a Cloud Service.

## Revogação de credenciais {#credentials-revocation}

Se a chave privada estiver comprometida, será necessário criar credenciais com um novo certificado e uma nova chave privada. Depois que seu aplicativo usar as novas credenciais para gerar tokens de acesso, você poderá revogar e excluir os certificados antigos.

Você pode fazer isso seguindo estas etapas:

1. Primeiro, adicione a nova chave. Isso gerará credenciais com uma nova chave privada e um novo certificado. A nova chave privada será marcada na interface do usuário como **atual** e serão, portanto, utilizadas para todas as novas credenciais para esta conta técnica a partir de agora. Observe que as credenciais associadas às chaves privadas mais antigas ainda serão válidas até serem revogadas. Para fazer isso, pressione os três pontos (**...**) na sua conta técnica atual e pressione **Adicionar nova chave privada**:

   ![Adicionar nova chave privada](/help/implementing/developing/introduction/assets/s2s-addnewprivatekey.png)

1. Press **Adicionar** no prompt a seguir:

   ![Confirmar adição de nova chave privada](/help/implementing/developing/introduction/assets/s2s-addprivatekeyconfirm.png)

   Uma nova guia de navegação com os novos componentes será aberta e a interface do usuário será atualizada para mostrar ambas as chaves privadas, com a nova marcada como **atual**:

   ![Chaves privadas na interface do usuário](/help/implementing/developing/introduction/assets/s2s-twokeys.png)

1. Instale as novas credenciais no servidor que não é o AEM e verifique se a conectividade funciona conforme o esperado. Consulte a [Seção Fluxo de servidor para servidor](#the-server-to-server-flow) para obter detalhes sobre como fazer isso
1. Revogue o certificado antigo. Você pode fazer isso selecionando os três pontos (**...**&#x200B;à direita do certificado e pressionando **Revogar**:

   ![Revogar certificado](/help/implementing/developing/introduction/assets/s2s-revokecert.png)

   Em seguida, confirme a revogação no prompt a seguir pressionando a tecla **Revogar** botão:

   ![Revogar confirmação de certificado](/help/implementing/developing/introduction/assets/s2s-revokecertificateconfirmation.png)

1. Finalmente, exclua o certificado comprometido.
