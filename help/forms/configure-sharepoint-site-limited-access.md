---
title: Como configurar um site do SharePoint com acesso limitado usando o escopo de autorização?
description: Saiba como configurar o SharePoint Site com acesso limitado usando o escopo de autorização.
keywords: Como configurar o SharePoint Site com acesso limitado?, Configurar o SharePoint com acesso limitado, Usar escopo de autorização para limitar o acesso ao SharePoint Site.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 3230bab2-c1aa-409d-9f01-c42cf88b1135
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 2%

---

# Configurar o site do SharePoint com acesso limitado usando o escopo de autorização

<span class="preview"> O recurso está disponível no programa de adoção antecipada. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

O objetivo do acesso limitado ou restrito é aprimorar o gerenciamento de segurança, permitindo que os administradores controlem o acesso do usuário a um site específico do SharePoint ou a um grupo do SharePoint Sites. O nível de permissão é útil quando você precisa conceder a um usuário ou grupo acesso a um Site específico sem permitir que ele visualize outros Sites da SharePoint não permitidos.

## Vantagens de configurar o SharePoint Site com acesso limitado

Vantagens de fornecer acesso limitado ao SharePoint Site:

* **Segurança avançada**: ao limitar o acesso, você pode garantir que somente as pessoas autorizadas tenham a capacidade de exibir ou manipular informações confidenciais, reduzindo o risco de acesso não autorizado.

* **Princípio do menor privilégio**: fornece aos usuários os níveis mínimos de acesso — ou permissões — necessários para executar suas funções de trabalho. Isso minimiza a exposição de cada usuário a partes confidenciais da rede, o que pode proteger contra possíveis ameaças internas.

* **Proteção de dados**: o acesso restrito ajuda a proteger dados críticos contra exposição. Ele garante que somente os usuários que precisam ver os dados possam acessá-los, o que é essencial para cumprir as regulamentações de proteção de dados.

* **Prevenção contra perda acidental de dados**: com menos pessoas capazes de modificar o conteúdo, as chances de exclusões acidentais ou alterações de dados importantes são significativamente reduzidas.

* **Fluxo de Dados Controlado**: ajuda a controlar o fluxo de informações dentro e fora da organização, garantindo que os dados não acabem em mãos erradas.

## Configurar o SharePoint com acesso limitado usando o escopo de autorização

Siga as etapas abaixo para configurar o SharePoint Sites com acesso limitado usando escopos de autorização:

1. [Crie um aplicativo com o ](#create-an-application-with-the-limited-permission-in-the-azure-portal)
1. [Definir o escopo de autorização na instância do AEM](#set-the-authorization-scope-at-aem-instance)

### Criar um aplicativo com a permissão limitada no portal do Azure

Crie um aplicativo no [portal do Microsoft Azure](https://portal.azure.com/#home) com o escopo de permissão `Sites.Selected` na API gráfica do Microsoft.

![Site selecionado do SharePoint](/help/forms/assets/sharepoint-selected-site.png)

Para obter informações sobre como recuperar `Client ID`, `Client Secret` e `Tenant ID` para `OAuth URL`, consulte a [Documentação da Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).

* No portal do Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Substitua `[author-instance]` pela URL da sua instância de Autor.
* Adicione o escopo de permissões `offline_access` e `Sites.Selected` na API gráfica do Microsoft para fornecer acesso restrito aos sites.
* Para URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substitua `<tenant-id>` pelo `tenant-id` do seu aplicativo no portal do Microsoft® Azure.

Para usar a permissão de API `Sites.Selected`, é necessário um aplicativo registrado no portal do Azure com as permissões apropriadas definidas para o SharePoint Online Sites. Essa configuração garante que o aplicativo tenha a autorização necessária para interagir com o site do SharePoint dentro do escopo definido, fornecendo assim o acesso limitado necessário.

Consulte o [artigo do blog - Desenvolver aplicativos que usam Sites.Permissões selecionadas para sites SPO](https://techcommunity.microsoft.com/t5/microsoft-sharepoint-blog/develop-applications-that-use-sites-selected-permissions-for-spo/ba-p/3790476) para obter instruções sobre como desenvolver aplicativos que usam `Sites.Selected` permissões para o SharePoint Online Sites.

### Definir o escopo de autorização na instância do AEM

Para fornecer acesso limitado a um site do Microsoft SharePoint, é essencial definir o escopo de autorização corretamente. Para definir o escopo de autorização e conectar o AEM Forms ao seu armazenamento Microsoft® SharePoint:

1. Vá para sua instância do **AEM Forms Author** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Após selecionar o **[!UICONTROL Microsoft® SharePoint]**, você será redirecionado para o **[!UICONTROL Navegador SharePoint]**.
1. Selecione um **Contêiner de Configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]** > **[!UICONTROL Biblioteca de Documentos da SharePoint]** na lista suspensa. O assistente de configuração do SharePoint é exibido.

   ![Acesso Limitado ao Site do SharePoint](/help/forms/assets/sharepoint-doc-library-limited-scopes.png)

1. Especifique o **[!UICONTROL Título]**, **[!UICONTROL ID do Cliente]** e **[!UICONTROL Segredo do Cliente]**. Para obter informações sobre como recuperar a ID e o Segredo do Cliente, consulte a [Documentação da Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).

1. Use a URL do OAuth como `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substitua `<tenant-id>` pelo `tenant-id` do seu aplicativo no portal do Microsoft® Azure.

   >[!NOTE]
   >
   > O campo **segredo do cliente** é obrigatório ou opcional, depende da configuração do aplicativo do Azure Ative Diretory. Se o aplicativo estiver configurado para usar um segredo do cliente, é obrigatório fornecer o segredo do cliente.

1. Adicione o `offline_access Sites.Selected` no campo `Authorization Scope`. Ao adicionar o escopo `offline_access Sites.Selected` no campo de caixa de texto `Authorization Scope`, a caixa de texto `SharePoint Site ID` fica visível na tela.

1. Especifique a ID do site do SharePoint. Para saber como recuperar a ID do Site do SharePoint, consulte a seção [Bytes extras](#extra-bytes).

1. Clique em **[!UICONTROL Verificar Conexão do Site]**. Em uma conexão bem-sucedida, a mensagem `Connection Successful` é exibida.

1. Agora, selecione **Site do SharePoint** > **Biblioteca de Documentos** > **Pasta do SharePoint** para salvar os dados.

   >[!NOTE]
   >
   >* Por padrão, `forms-ootb-storage-adaptive-forms-submission` está presente no site do SharePoint selecionado.
   >* Crie uma pasta como `forms-ootb-storage-adaptive-forms-submission`, se ainda não estiver presente na biblioteca `Documents` do Site do SharePoint selecionado clicando em **Criar Pasta**.

Agora, você pode usar esta [configuração do SharePoint Sites para a ação de envio em um Formulário adaptável](/help/forms/configure-submit-action-sharepoint.md#use-sharepoint-document-library-configuration-in-an-adaptive-form-use-sharepoint-configuartion-in-af).

## Bytes extras

Para recuperar o valor de `SharePoint Site ID`:

1. Vá para as [APIs do Microsoft Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer).
1. No painel esquerdo, em `SharePoint Sites` APIs, clique em `Search for a SharePoint site by keyword`.
1. Substitua o espaço reservado `contoso` pelo nome real do site do SharePoint para buscar a ID do site correspondente.

   ![ID da Biblioteca de Documentos da SharePoint](/help/forms/assets/sharepoint-site-id.png)

Ao clicar no botão `Run Query`, a ID do Site é exibida na tela.
