---
title: Como integrar o Salesforce usando o fluxo de credenciais do cliente OAuth 2.0 com o AEM Forms?
description: Saiba como integrar o Salesforce com o AEM Forms usando o fluxo de credenciais do cliente OAuth 2.0. Ele exibe etapas para a integração do AEM Forms Salesforce.
Keywords: Integration of Salesforce using OAuth 2.0 client credential flow, salesforce integration with oauth2 using client credential flow, salesforce and client credential integration, AEM Forms Salesforce integration
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2c2029ab-6fb4-41a6-846c-175c3a79d921
source-git-commit: 9eb15dda5f56938d686d0b863cb1ffa841f8228b
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# Integrar formulário adaptável com o Salesforce {#configure-salesforce-with-ouath-2.0-client-credential}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

A integração do Adobe Experience Manager (AEM) Forms com o Salesforce permite que as organizações simplifiquem os processos, conectando seus recursos de criação e gerenciamento de formulários à plataforma Salesforce. A conexão de um formulário adaptável com o Salesforce permite a troca perfeita de dados entre as duas plataformas. Quando os usuários enviam formulários, os dados são sincronizados com o Salesforce automaticamente. Ele garante que todas as informações do cliente estejam atualizadas e centralizadas no sistema.

Você pode usar as credenciais do cliente OAuth 2.0 para integrar o AEM Forms ao aplicativo Salesforce. As credenciais do cliente OAuth 2.0 são um método padrão e seguro para a comunicação direta sem envolvimento do usuário.

![Fluxo de trabalho ao definir a comunicação entre o AEM Forms e o aplicativo Salesforce](/help/forms/assets/salesforce-workflow.png)

O AEM Forms troca as credenciais do cliente (chave do consumidor e segredo do consumidor), definidas no aplicativo conectado do Salesforce, para obter um token de acesso.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md).

Há vários benefícios de usar credenciais de cliente OAuth 2.0 para autenticação em relação à autenticação de Fluxo de código de autorização:

* A autenticação de credenciais do cliente OAuth 2.0 permite mais de cinco conexões por usuário.
* A configuração da fonte de dados AEM continua trabalhando na desativação, alterações de acesso e atualização de senha para um usuário AEM.

## Pré-requisitos {#prerequisites}

Antes de definir a comunicação entre um aplicativo do Salesforce e um ambiente AEM:

* Crie um [Aplicativo conectado do Salesforce com fluxo de credenciais de cliente OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&type=5) e um usuário somente de API para sua organização e obtenha a chave do consumidor e o segredo do consumidor para o aplicativo.

* Verifique se o arquivo do Swagger está configurado corretamente para corresponder às APIs da sua organização. Como alternativa, você pode [criar um arquivo Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=pt-BR) do zero, personalizado para utilização em seu ambiente AEM.


## Configurar o aplicativo Salesforce usando o fluxo de credenciais do cliente OAuth 2.0 {#steps-to-create-aem-datasource-configuration}

Para conectar o formulário adaptável ao aplicativo Salesforce usando as configurações de autenticação de credencial do cliente OAuth 2.0, execute as seguintes etapas:

1. Faça logon na instância do Author.
1. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Fontes de Dados]**.
1. Selecione a pasta de configuração.
1. Clique em **[!UICONTROL Criar]** e a **[!UICONTROL Criar configuração do Data Source]** será exibida.
1. Especifique o **[!UICONTROL Título]** e selecione o **[!UICONTROL Tipo de Serviço]** como **[!UICONTROL Serviço RESTful]**.
1. Clique em **[!UICONTROL Avançar]**.
1. Selecione o **[!UICONTROL Swagger Source]** como **[!UICONTROL Arquivo].**

   >[!NOTE]
   >
   > Quando o arquivo swagger é selecionado, o Esquema, o Nome do host e o Caminho base são preenchidos automaticamente.

1. Carregue o arquivo do Swagger criado do computador local clicando em **[!UICONTROL Procurar]**.
1. Selecione o **[!UICONTROL Tipo de Autenticação]** como **[!UICONTROL OAuth 2.0]** e o painel **[!UICONTROL Configurações de Autenticação]** será exibido.
1. Selecione o **[!UICONTROL Tipo de Concessão]** como **[!UICONTROL Credencial do Cliente]**.
1. Especifique a **[!UICONTROL ID do Cliente]** e o **[!UICONTROL Segredo do Cliente]** obtidos do aplicativo conectado ao Salesforce.
1. Especifique a **[!UICONTROL URL do Token de Acesso]** no formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Cada organização tem seu próprio nome de domínio específico.

1. Clique em **[!UICONTROL Testar Conexão]**.
1. Se a conexão tiver êxito, clique no botão **[!UICONTROL Criar]**.


Após configurar o aplicativo Salesforce, você pode usar a configuração ao criar o modelo de dados de formulário (FDM). Para obter mais informações, consulte [Criar modelo de dados de formulário (FDM)](create-form-data-models.md). [Configure a Ação de Envio do Modelo de Dados de Formulário](/help/forms/using-form-data-model.md) para um Formulário Adaptável para enviar dados aos aplicativos do Salesforce.

Para obter mais informações sobre como criar e usar o Form Data Model (FDM) nos fluxos de trabalho de negócios, consulte [Integração de Dados](data-integration.md).

## Artigos relacionados

{{af-submit-action}}


