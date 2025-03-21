---
title: Gerenciar  [!DNL Adobe Stock] ativos no [!DNL Assets].
description: Pesquise, busque, licencie e gerencie  [!DNL Adobe Stock] ativos no  [!DNL Adobe Experience Manager]. Use os ativos licenciados como qualquer outro ativo digital.
contentOwner: Vishabh Gupta
feature: Adobe Stock
role: Admin, User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 4%

---

# Usar [!DNL Adobe Stock] ativos em [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/aem-assets-adobe-stock.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

O serviço [!DNL Adobe Stock] fornece aos designers e empresas acesso a milhões de fotos, vetores, ilustrações, vídeos, modelos e ativos 3D de alta qualidade, com curadoria e isentos de royalties para todos os seus projetos criativos.

A oferta [!DNL Adobe Stock] para corporações, por padrão, inclui direitos de compartilhamento em toda a organização. Depois que um ativo é licenciado por um usuário da organização, outros usuários da organização podem identificar, baixar e usar esse ativo sem precisar licenciá-lo novamente. Depois que um ativo é licenciado pela sua organização, o direito de usá-lo é perpétuo.

As organizações podem integrar seu plano corporativo [!DNL Adobe Stock] ao [!DNL Experience Manager Assets] para garantir que os ativos licenciados estejam amplamente disponíveis para seus projetos criativos e de marketing, com os poderosos recursos de gerenciamento de ativos do [!DNL Experience Manager]. Os usuários do [!DNL Experience Manager] podem rapidamente encontrar, visualizar e licenciar os ativos do Adobe Stock que são salvos no [!DNL Experience Manager], sem sair da interface do [!DNL Experience Manager].

## Integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

O [!DNL Experience Manager Assets] fornece aos usuários a capacidade de pesquisar, visualizar, salvar e licenciar ativos do [!DNL Adobe Stock] diretamente do [!DNL Experience Manager].

**Pré-requisitos**

A integração exige:

* Um [!DNL Experience Manager Assets] ativo e em execução como uma instância de [!DNL Cloud Service]
* Um [plano [!DNL Adobe Stock] da empresa](https://stockenterprise.adobe.com/)
* Um usuário com permissões no Admin Console para o perfil de produto padrão do Stock
* Um usuário com permissões para o perfil do Developer Access para criar integração no Adobe Developer Console

Um plano da empresa [!DNL Adobe Stock],

* Fornece direitos de produto para [!DNL Adobe Stock] (Estoques conectados ao Experience Manager)
* Créditos comprados em [!DNL Adobe Admin Console] para o seu direito a ações
* Habilita a autenticação da Conta de Serviço (JWT) no [!DNL Adobe Developer Console] para seu direito de estoque
* Habilita o gerenciamento global de créditos e licenciamento a partir de [!DNL Adobe Admin Console]

Dentro do direito, um perfil de produto padrão para [!DNL Adobe Stock] existe em [!DNL Admin Console]. Vários perfis podem ser criados, e esses perfis determinam quem pode licenciar os ativos do Stock. Um usuário com acesso direto ao perfil de produto pode acessar o [https://stock.adobe.com/](https://stock.adobe.com/) e licenciar os ativos do Stock. Já há outro método de usar o Developer Access para criar uma integração (API). Esta integração autentica a comunicação entre [!DNL Experience Manager Assets] e [!DNL Adobe Stock].

>[!NOTE]
>
>A autenticação da conta de serviço do Stock (JWT) vem com o direito do Enterprise Stock.
>
>A integração não oferece suporte à autenticação Oauth para o direito do Enterprise Stock.


<!--
### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->
<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel. To access the panel from Experience Manager home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

-->

## Etapas para integrar [!DNL Experience Manager] e [!DNL Adobe Stock] {#integration-steps}

Para integrar [!DNL Experience Manager] e [!DNL Adobe Stock], execute as seguintes etapas na sequência listada:

1. [Obter certificado público](#public-certificate)

   Em [!DNL Experience Manager], crie uma conta IMS e gere um certificado público (chave pública).

1. [Criar conexão de conta de serviço (JWT)](#createnewintegration)

   Em [!DNL Adobe Developer Console], crie um projeto para sua organização [!DNL Adobe Stock]. No projeto, configure uma API usando a chave pública para criar uma conexão de conta de serviço (JWT). Obtenha as credenciais da conta de serviço e as informações de carga JWT.

1. [Configurar conta IMS](#create-ims-account-configuration)

   Em [!DNL Experience Manager], configure a conta IMS usando as credenciais da conta de serviço e a carga JWT.

1. [Configurar o serviço em nuvem](#configure-the-cloud-service)

   No [!DNL Experience Manager], configure um serviço de nuvem [!DNL Adobe Stock] usando a conta IMS.


### Criar uma configuração IMS {#create-an-ims-configuration}

A configuração IMS autentica sua instância do autor [!DNL Experience Manager Assets] com o direito [!DNL Adobe Stock].

A configuração IMS inclui duas etapas:

* [Obter certificado público](#public-certificate)
* [Configurar conta IMS](#create-ims-account-configuration)

### Obter certificado público {#public-certificate}

A chave pública (certificado) autentica seu perfil de produto no Adobe Developer Console.

1. Faça logon na instância da nuvem do [!DNL Experience Manager Assets].

1. No painel **[!UICONTROL Ferramentas]**, navegue até **[!UICONTROL Segurança]** > **[!UICONTROL Configurações do Adobe IMS]**.

1. Na página Configurações do Adobe IMS, clique em **[!UICONTROL Criar]**. A página **[!UICONTROL Configuração de conta técnica do Adobe IMS]** é aberta.

1. Na guia **[!UICONTROL Certificado]**, selecione **[!UICONTROL Adobe Stock]** na lista suspensa **[!UICONTROL Solução da nuvem]**.

1. Você pode criar um certificado ou reutilizar um certificado existente para a configuração.

   Para criar um certificado, marque a caixa de seleção **[!UICONTROL Criar novo certificado]** e especifique um **alias** para a chave pública. O alias atua como nome da chave pública.

1. Clique em **[!UICONTROL Criar certificado]**. Em seguida, clique em **[!UICONTROL OK]** para gerar a chave pública.

1. Clique no ícone **[!UICONTROL Baixar Chave pública]** e salve o arquivo de chave pública (.crt) no computador. A chave pública é usada posteriormente para configurar a API do locatário do Brand Portal e gerar credenciais de conta de serviço no Adobe Developer Console.

   Clique em **[!UICONTROL Avançar]**.

   ![gerar-certificado](assets/stock-integration-ims-account.png)

1. Na guia **Conta**, a conta do Adobe IMS é criada e requer as credenciais da conta de serviço.

   Abra uma nova guia e [crie uma conexão de conta de serviço (JWT) no Adobe Developer Console](#createnewintegration).

### Criar conexão de conta de serviço (JWT) {#createnewintegration}

No Adobe Developer Console, os projetos e as APIs são configurados no nível da organização. Configurar uma API cria uma conexão de conta de serviço (JWT). Há dois métodos para configurar a API: gerar um par de chaves (chaves privadas e públicas) ou carregar uma chave pública. Neste exemplo, as credenciais da conta de serviço são geradas fazendo upload da chave pública.

Para gerar as credenciais da conta de serviço e a carga JWT:

1. Faça logon no Adobe Developer Console com privilégios de administrador do sistema. A URL padrão é [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Verifique se você selecionou a organização IMS correta (Direito de estoque) na lista suspensa (Organização).

1. Clique em **[!UICONTROL Criar novo projeto]**. Um projeto em branco com um nome gerado pelo sistema é criado para sua organização.

   Clique em **[!UICONTROL Editar projeto]**. Atualize o **[!UICONTROL Título do Projeto]** e a **[!UICONTROL Descrição]** e clique em **[!UICONTROL Salvar]**.

1. Na guia **[!UICONTROL Visão geral do projeto]**, clique em **[!UICONTROL Adicionar API]**.

1. Na **[!UICONTROL janela Adicionar uma API]**, selecione **[!UICONTROL Adobe Stock]**. Clique em **[!UICONTROL Avançar]**.

1. Na janela **[!UICONTROL Configurar API]**, selecione a autenticação **[!UICONTROL Conta de Serviço (JWT)]**. Clique em **[!UICONTROL Avançar]**.

   ![criar-credenciais-jwt](assets/aem-stock-jwt.png)

1. Clique em **[!UICONTROL Carregar sua chave pública]**. Clique em **[!UICONTROL Selecionar um Arquivo]** e carregue a chave pública (arquivo .crt) baixada na seção [obter certificado público](#public-certificate). Clique em **[!UICONTROL Avançar]**.

1. Verifique a chave pública e clique em **[!UICONTROL Avançar]**.

1. Selecione o perfil de produto padrão **[!UICONTROL Adobe Stock]** e clique em **[!UICONTROL Salvar API configurada]**.

1. Após configurar a API, você é redirecionado para a página Visão geral da API. Na navegação à esquerda, em **[!UICONTROL Credenciais]**, clique na opção **[!UICONTROL Conta de Serviço (JWT)]**. Aqui, você pode visualizar as credenciais e executar ações como gerar tokens JWT, copiar detalhes da credencial e recuperar segredo do cliente.

1. Na guia **[!UICONTROL Credenciais do Cliente]**, copie a **[!UICONTROL ID do cliente]**.

   Clique em **[!UICONTROL Recuperar segredo do cliente]** e copie o **[!UICONTROL segredo do cliente]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navegue até a guia **[!UICONTROL Gerar JWT]** e copie as informações da **[!UICONTROL Carga JWT]**.

Agora você pode usar a ID do cliente (chave de API), o segredo do cliente e a carga JWT para [configurar a conta IMS](#create-ims-account-configuration) em [!DNL Experience Manager Assets].

### Configurar conta IMS {#create-ims-account-configuration}

Você deve ter as [credenciais de certificado](#public-certificate) e [conta de serviço (JWT)](#createnewintegration) para configurar a conta IMS.

Para configurar a conta IMS:

1. Abra a Configuração IMS e navegue até a guia **[!UICONTROL Conta]**. Você manteve a página aberta enquanto [obtinha o certificado público](#public-certificate).

1. Especifique um **[!UICONTROL Título]** para a conta IMS.

   No campo **[!UICONTROL Servidor de Autorização]**, digite a URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Insira a ID do cliente no campo **[!UICONTROL Chave da API]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL Carga]** (carga JWT) copiados ao [criar a conexão da conta de serviço (JWT)](#createnewintegration).

1. Clique em **[!UICONTROL Criar]**. Uma configuração de conta IMS é criada.

   ![configurar-ims-account](assets/aem-stock-ims-config.png)

1. Selecione a configuração da conta IMS e clique em **[!UICONTROL Verificar integridade]**.

   Clique em **[!UICONTROL Verificar]** na caixa de diálogo. Na configuração bem-sucedida, aparece uma mensagem informando que o *token foi recuperado com êxito*.

   ![verificação de integridade](assets/aem-stock-healthcheck.png)


### Configurar o serviço em nuvem {#configure-the-cloud-service}

Para configurar o serviço de nuvem [!DNL Adobe Stock]:

1. Na interface de usuário do [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços da Nuvem]** > **[!UICONTROL Adobe Stock]**.

1. Na página [!DNL Adobe Stock Configurations], clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração de nuvem.

   Selecione a configuração IMS criada ao [configurar a conta IMS](#create-ims-account-configuration).

   Selecione seu local na lista suspensa.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Clique em **[!UICONTROL Salvar e fechar]**.

   Sua instância de autor [!DNL Experience Manager Assets] agora está integrada com [!DNL Adobe Stock]. Você pode criar várias configurações do [!DNL Adobe Stock] (por exemplo, configurações baseadas em localidade). Agora você pode acessar, pesquisar e licenciar os ativos do [!DNL Adobe Stock] na interface do usuário do [!DNL Experience Manager].

   ![ativos-de-estoque-pesquisa](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >Neste estágio da integração, somente os administradores podem acessar os ativos do [!DNL Adobe Stock], pesquisar ativos do Stock (usando omnisearch) e licenciar os ativos do [!DNL Adobe Stock].
   >
   >Os administradores podem adicionar usuários ou grupos ao serviço de nuvem [!DNL Adobe Stock] e conceder permissões a esses usuários não administradores no [!DNL Experience Manager] para acessar a configuração do Stock.

1. Para adicionar usuários ou grupos, selecione a configuração de nuvem [!DNL Adobe Stock] e clique em **[!UICONTROL Propriedades]**.

1. Pesquise para adicionar os usuários ou grupos aos quais você atribuiu permissões para acessar a configuração do Adobe Stock. Consulte [atribuir permissões ao grupo de usuários](#assign-permissions-to-group).


## Atribuir permissões ao grupo de usuários {#assign-permissions-to-group}

Os administradores podem criar grupos de usuários e conceder permissões a determinados usuários ou grupos para acessar o serviço de nuvem [!DNL Adobe Stock].

A seguir estão as permissões necessárias para que um usuário pesquise e licencie ativos do Adobe Stock:

* Configurar o caminho: `/conf/global/settings/stock`
* Privilégios: `jcr:read`
* Tipo de Permissão: `Allow`

Você pode criar um grupo de usuários ou atribuir permissões a um grupo de usuários existente. As permissões podem ser atribuídas pela interface [!DNL Experience Manager Assets] ou pelo Console [!DNL User Admin].

**Para fornecer acesso a um grupo de usuários a partir de [!DNL Experience Manager]:**

1. Na interface de usuário do [!DNL Experience Manager], navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Grupos]**. Criar um grupo de usuários para [!DNL Adobe Stock].

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Permissões]**.

1. Procure o grupo de usuários no painel esquerdo e adicione a nova **[!UICONTROL Entrada de Controle de Acesso (ACE)]** para o Adobe Stock.

   * Configurar o caminho: `/conf/global/settings/stock`
   * Privilégios: `jcr:read`
   * Tipo de Permissão: `Allow`

   Clique em **[!UICONTROL Adicionar]**.

   ![permissões de usuário](assets/aem-stock-user-permissions.png)

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços na Nuvem]** > **[!UICONTROL Adobe Stock]**. Selecione a configuração de nuvem [!DNL Adobe Stock] e clique em **[!UICONTROL Propriedades]**.

1. Adicione o grupo de usuários criado à configuração [!DNL Adobe Stock]. Clique em **[!UICONTROL Salvar e fechar]**.

   ![atribuir-usuário](assets/aem-stock-adduser.png)

**Para fornecer acesso a um usuário a partir de [!DNL User Admin Console]:**

1. Abra o Admin Console do Usuário [!DNL Experience Manager]. A URL padrão é `http://localhost:4502/userdamin`.

1. No painel esquerdo, pesquise pelo usuário inserindo o `user_id` ou `name`. Clique duas vezes para abrir as propriedades do usuário.

1. Navegue até a guia **[!UICONTROL Permissões]** e permita `read` permissões para a configuração de nuvem [!DNL Adobe Stock]: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Se a configuração da nuvem não for permitida, o usuário só poderá acessar o **[!UICONTROL Assets]** na interface [!DNL Experience Manager].
   >
   >Para permitir o acesso aos ativos do [!UICONTROL Assets] e do [!DNL Adobe Stock], verifique se a configuração da nuvem é permitida para o usuário.

1. Clique em **[!UICONTROL Salvar]** para atualizar as permissões.

   ![atribuir-usuário-em-usuário-administrador](assets/aem-stock-user-admin-console.png)

1. Adicione o usuário ou grupo à configuração de nuvem [!DNL Adobe Stock].


## Acessar ativos do Adobe Stock {#access-stock-assets}

Um usuário não administrador com permissões para a configuração de nuvem do [!DNL Adobe Stock] pode pesquisar e licenciar os ativos do [!DNL Adobe Stock] na interface do [!DNL Experience Manager].

O usuário precisa executar uma etapa extra para ativar a configuração de nuvem [!DNL Adobe Stock] antes de acessar [!DNL Adobe Stock] ativos. É uma atividade única. Se o usuário tiver permissões atribuídas em várias configurações de nuvem do [!DNL Adobe Stock], ele poderá selecionar a configuração desejada nas **[!UICONTROL Preferências do Usuário]**.

Para ativar a configuração de nuvem do [!DNL Adobe Stock]:

1. Faça logon em [!DNL Experience Manager].

1. Clique no ícone do usuário no canto superior direito e em **[!UICONTROL Minhas preferências]**. A janela **[!UICONTROL Preferências do Usuário]** é aberta.

1. Selecione a **[!UICONTROL Configuração do Stock]** desejada na lista suspensa e clique em **[!UICONTROL Aceitar]** para ativar a configuração.

   ![preferências-usuário](assets/aem-stock-preferences.png)

1. Navegue até **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**. Agora você pode exibir, pesquisar e licenciar [!DNL Adobe Stock] ativos.

A tabela a seguir explica como as permissões de usuário funcionam ao acessar os ativos do [!DNL Adobe Stock]:

| Usuário | Grupo | Permissões | Aceitar a configuração do Stock nas Preferências do Usuário | Acessar o Assets | Acessar o Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| admin | N/A | Todos | N/A | Sim | Sim |
| test-doc1 | Usuário do DAM | /conf/global/settings/stock/cloud-config | Sim | Sim | Sim |
| test-doc1 | Usuário do DAM | /conf/global/settings/stock/cloud-config | Não | Erro: falha ao carregar dados | Não |
| test-doc1 | Usuário do DAM | **permitir**: /conf/global/settings/stock **negar**: /cloud-config | A configuração do Stock não está visível | Sim | Não |

## Usar e gerenciar [!DNL Adobe Stock] ativos em [!DNL Experience Manager] {#usemanage}

Usando este recurso, as organizações podem permitir que seus usuários trabalhem usando os ativos do [!DNL Adobe Stock] no [!DNL Experience Manager Assets]. Na interface de usuário do [!DNL Experience Manager], os usuários podem pesquisar [!DNL Adobe Stock] ativos e licenciar os ativos necessários.

Depois que um ativo [!DNL Adobe Stock] é licenciado em [!DNL Experience Manager], ele pode ser usado e gerenciado como um ativo típico. No [!DNL Experience Manager], os usuários podem pesquisar e visualizar os ativos; copiar e publicar os ativos; compartilhar os ativos no [!DNL Brand Portal]; acessar e usar os ativos por meio do aplicativo de desktop do [!DNL Experience Manager]; e assim por diante.

![Pesquise por [!DNL Adobe Stock] ativos e filtre os resultados do seu espaço de trabalho [!DNL Adobe Experience Manager]](assets/adobe-stock-search-results-workspace.png)

**A.** Pesquise ativos semelhantes aos ativos cuja ID [!DNL Adobe Stock] é fornecida. **B.** Pesquise ativos que correspondem à seleção de forma ou orientação. **C.** Pesquise por um dos tipos de ativos com suporte **D.** Abra ou recolha o painel de filtros **E.** Licencie e salve o ativo selecionado em [!DNL Experience Manager] **F.** Salve o ativo em [!DNL Experience Manager] com a marca d&#39;água **G.** Explore ativos no site [!DNL Adobe Stock] que sejam semelhantes ao ativo selecionado **H.** Exiba os ativos selecionados no site [!DNL Adobe Stock] **I.** Número de ativos selecionados dos resultados da pesquisa **J.** Alternar entre exibição de Cartão e exibição de Lista

### Localizar ativos {#find-assets}

Seus usuários do [!DNL Experience Manager], podem pesquisar por ativos no [!DNL Experience Manager] e no [!DNL Adobe Stock]. Quando o local de pesquisa não está limitado a [!DNL Adobe Stock], os resultados da pesquisa de [!DNL Experience Manager] e [!DNL Adobe Stock] são exibidos.

* Para pesquisar por [!DNL Adobe Stock] ativos, clique em **[!UICONTROL Navegação]** > **[!UICONTROL Assets]** > **[!UICONTROL Pesquisar Adobe Stock]**.

* Para pesquisar ativos em [!DNL Adobe Stock] e [!DNL Experience Manager Assets], clique em pesquisar ![pesquisar](assets/do-not-localize/search_icon.png).

Como alternativa, comece digitando `Location: Adobe Stock` na barra de pesquisa para selecionar [!DNL Adobe Stock] ativos. O [!DNL Experience Manager] oferece recursos de filtragem avançados nos ativos pesquisados, permitindo que os usuários definam rapidamente os ativos necessários usando filtros, como tipos de ativos com suporte, orientação de imagem e estado licenciado.

>[!NOTE]
>
>Assets pesquisados a partir de [!DNL Adobe Stock] são exibidos em [!DNL Experience Manager]. [!DNL Adobe Stock] ativos são buscados e armazenados no repositório do [!DNL Experience Manager] somente depois que um usuário [salva um ativo](/help/assets/aem-assets-adobe-stock.md#saveassets) ou [licencia e salva um ativo](/help/assets/aem-assets-adobe-stock.md#licenseassets). Os Assets que já estão armazenados em [!DNL Experience Manager] são exibidos e destacados para facilitar a referência e o acesso. Além disso, os ativos [!DNL Stock] são salvos com alguns metadados adicionais para indicar a origem como [!DNL Stock].

![Filtros de pesquisa em [!DNL Experience Manager] e realçou [!DNL Adobe Stock] ativos nos resultados da pesquisa](assets/aem-search-filters2.jpg)

### Salvar e exibir os ativos necessários {#saveassets}

Selecione um ativo que você deseja salvar em [!DNL Experience Manager]. Clique em [!UICONTROL Salvar] na barra de ferramentas na parte superior e forneça o nome e o local do ativo. Os ativos não licenciados são salvos localmente com uma marca d&#39;água.

Na próxima vez em que você pesquisar ativos, os ativos salvos serão destacados com uma medalha, para indicar que esses ativos estão disponíveis em [!DNL Experience Manager Assets].

>[!NOTE]
>
>Os ativos adicionados recentemente exibem um selo Novo em vez de um selo Licenciado.

### Ativos de licença {#licenseassets}

Os usuários podem licenciar [!DNL Adobe Stock] ativos usando a cota do plano corporativo [!DNL Adobe Stock]. Ao licenciar um ativo, ele é salvo sem uma marca d&#39;água e está disponível para pesquisa e uso no [!DNL Experience Manager Assets].

![Caixa de diálogo para licenciar e salvar [!DNL Adobe Stock] ativos em [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Acessar propriedades de metadados e ativos {#access-metadata-and-asset-properties}

Os usuários podem acessar e visualizar os metadados, incluindo as propriedades de metadados [!DNL Adobe Stock] dos ativos salvos em [!DNL Experience Manager], e adicionar **[!UICONTROL Referências de licença]** para um ativo. No entanto, as atualizações da referência de licença não são sincronizadas entre o site [!DNL Experience Manager] e o site [!DNL Adobe Stock].

Os usuários podem ver as propriedades de ativos licenciados e não licenciados.

![Exibir e acessar metadados e referências de licença de ativos salvos](assets/metadata_properties.jpg)


## Limitações conhecidas {#known-limitations}

* A **funcionalidade para restringir usuários de licenciamento não está funcionando corretamente**: todos os usuários com `read` permissões para a configuração de estoque podem pesquisar e licenciar os ativos do [!DNL Adobe Stock].

* **Usuários não administradores precisam ativar manualmente a [!DNL Adobe Stock] configuração de nuvem**: na janela **[!UICONTROL Preferências do Usuário]**, a **[!UICONTROL Configuração do Stock]** mostra a configuração de nuvem [!DNL Adobe Stock] como habilitada, mas não funciona para um usuário não administrador. O usuário precisa clicar no botão **[!UICONTROL Aceitar]** para ativar a configuração do Stock. Na ausência desta etapa, o sistema reflete uma mensagem de erro ao acessar o **[!UICONTROL Assets]**.

* **O aviso de imagem editorial não é exibido**: ao licenciar uma imagem, os usuários não podem verificar se uma imagem é Somente para Uso Editorial. Para evitar possíveis usos indevidos, os administradores podem desativar o acesso a ativos editoriais do Admin Console.

* **Tipo de licença incorreto exibido**: é possível que um tipo de licença incorreto seja exibido em [!DNL Experience Manager] para um ativo. Os usuários podem fazer logon no site [!DNL Adobe Stock] para ver o tipo de licença.

* **Os campos de referência e os metadados não estão sincronizados**: quando um usuário atualiza um campo de referência de licença, as informações de referência de licença são atualizadas em [!DNL Experience Manager], mas não no site [!DNL Adobe Stock]. Da mesma forma, se o usuário atualizar os campos de referência no site [!DNL Adobe Stock], as atualizações não serão sincronizadas em [!DNL Experience Manager].

<!--
## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations users can work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.
-->

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

<!--
### Find assets {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* To search for assets across [!DNL Adobe Stock] and [!DNL Experience Manager Assets], click search ![search](assets/do-not-localize/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select [!DNL Adobe Stock] assets. [!DNL Experience Manager] offers advanced filtering capabilities on the searched assets, allowing users to quickly zero-in on the required assets using filters, such as types of supported assets, image orientation, and licensed state.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] assets are fetched and stored in [!DNL Experience Manager] repository only after a user either [saves an asset](/help/assets/aem-assets-adobe-stock.md#saveassets) or [licenses and saves an asset](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Search filters in Experience Manager and highlighted Adobe Stock assets in search results](assets/aem-search-filters2.jpg)

*Figure: Search filters in [!DNL Experience Manager] and highlighted [!DNL Adobe Stock] assets in search results.*

### Save and view the required assets {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. The unlicensed assets are saved locally with a watermark.

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>The recently added assets display a New badge instead of Licensed badge.

### License assets {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Dialog to license and save Adobe Stock assets in Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figure: Dialog to license and save [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets].*

### Access metadata and asset properties {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Users can see the properties for both, licensed and unlicensed assets.

![View and access metadata and license references of saved assets](assets/metadata_properties.jpg)

*Figure: View and access metadata and license references of saved assets.*

## Known limitations {#known-limitations}

* **Editorial image warning is not displayed**: When licensing an image, users cannot check if an image is Editorial Use Only. To prevent possible misuse, the administrators can turn off the access to editorial assets from the Admin Console.

* **Wrong license type is displayed**: It is possible that an incorrect license type is displayed in [!DNL Experience Manager] for an asset. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Reference fields and metadata are not synced**: When a user updates a license reference field, the license reference information is updated in [!DNL Experience Manager] but not on the [!DNL Adobe Stock] website. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].
-->

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Tutorial em vídeo sobre o uso de ativos do Adobe Stock com o Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [ajuda do plano da empresa Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [PERGUNTAS FREQUENTES SOBRE O Adobe Stock](https://helpx.adobe.com/stock/faq.html)
