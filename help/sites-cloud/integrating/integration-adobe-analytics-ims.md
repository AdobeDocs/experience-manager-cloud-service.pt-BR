---
title: Configuração do IMS para uso na integração com o Adobe Analytics
description: Saiba mais sobre a Configuração IMS para usar ao integrar com o Adobe Analytics
exl-id: 12bd1573-373a-4001-be71-c8f155ef6896
source-git-commit: 0030b0f6f17dd66229f681e9c513786de4fe10a2
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 5%

---

# Configuração do IMS para uso na integração com o Adobe Analytics {#ims-configuration-for-integration-with-adobe-analytics}

A integração do Adobe Experience Manager as a Cloud Service (AEMaaCS) com o Adobe Analytics por meio da API do Analytics Standard requer a configuração do Adobe IMS (Identity Management System). A configuração é realizada com o Console do desenvolvedor do Adobe.

>[!NOTE]
>
>O suporte para a API 2.0 do Adobe Analytics Standard é novo no AEMaaCS 2022.2.0. Essa versão da API é compatível com a autenticação IMS.
>
>A seleção da API é orientada pelo método de autenticação usado para a integração do AEM/Analytics.
>
>Outras informações estão também disponíveis no [Migração para as APIs 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## Pré-requisitos {#prerequisites}

Antes de iniciar este procedimento:

* [Suporte a Adobe](https://helpx.adobe.com/br/contact/enterprise-support.ec.html) precisa provisionar sua conta para:

   * Console Adobe
   * Console do desenvolvedor da Adobe
   * Adobe Analytics e
   * Adobe IMS (Sistema Identity Management)

* O Administrador de sistema da sua organização deve usar o Admin Console para adicionar os desenvolvedores necessários em sua organização aos perfis de produto relevantes.

   * Isso fornece aos desenvolvedores específicos permissões para ativar integrações usando o Console do desenvolvedor do Adobe.
   * Para obter mais detalhes, consulte [Gerenciar desenvolvedores](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuração de um IMS - Geração de uma chave pública {#configuring-ims-generating-a-public-key}

O primeiro estágio da configuração é criar uma Configuração IMS no AEM e gerar a Chave pública.

1. Em AEM abra o **Ferramentas** menu.
1. No **Segurança** seção selecionar **Configurações do Adobe IMS**.
1. Selecionar **Criar** para abrir o **Configuração de conta técnica do Adobe IMS**.
1. Uso da lista suspensa em **Configuração na nuvem**, selecione **Adobe Analytics**.
1. Ativar **Criar novo certificado** e insira um novo alias.
1. Confirme com **Criar certificado**.

   ![Criar certificado](assets/integrate-analytics-ims-01.png)

1. Selecionar **Baixar** ou **Baixar chave pública**) para baixar o arquivo na unidade local, de modo que ele esteja pronto para uso quando [configuração do IMS para integração do Adobe Analytics com o AEM](#configuring-ims-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >Mantenha essa configuração aberta, ela será necessária novamente quando [Concluir a configuração IMS no AEM](#completing-the-ims-configuration-in-aem).

   ![Baixar certificado](assets/integrate-analytics-ims-02.png)

## Configuração do IMS para integração do Adobe Analytics com o AEM {#configuring-ims-adobe-analytics-integration-with-aem}

Usando o Console Adobe Developer, é necessário criar um Projeto (integração) com o Adobe Analytics (para AEM usar) e, em seguida, atribuir os privilégios necessários.

### Criação do projeto {#creating-the-project}

Abra o Console do Adobe Developer para criar um Projeto com o Adobe Analytics que AEM usará:

1. Abra o Console do desenvolvedor do Adobe para Projetos:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. Quaisquer projetos que você tiver serão mostrados. Selecionar **Criar novo projeto** - a localização e utilização dependerão:

   * Se você ainda não tiver um projeto, **Criar novo projeto** será central, inferior.
      ![Criar novo projeto - Primeiro projeto](assets/integration-analytics-ims-02.png)
   * Caso já tenha projetos existentes, eles serão listados e **Criar novo projeto** estará no canto superior direito.
      ![Criar novo projeto - Vários projetos](assets/integration-analytics-ims-03.png)


1. Selecionar **Adicionar ao projeto** seguida de **API**:

   ![Introdução ao novo projeto](assets/integration-analytics-ims-10.png)

1. Selecionar **Adobe Analytics**, em seguida **Próximo**:

   >[!NOTE]
   >
   >Se você estiver inscrito no Adobe Analytics, mas não o vir listado, verifique a variável [Pré-requisitos](#prerequisites).

   ![Adicionar uma API](assets/integration-analytics-ims-12.png)

1. Selecionar **Conta de serviço (JWT)** como o tipo de autenticação, continue com **Próximo**:

   ![Selecionar tipo de autenticação](assets/integration-analytics-ims-12a.png)

1. **Fazer upload de sua chave pública** e quando terminar, continue com **Próximo**:

   ![Fazer upload de sua chave pública](assets/integration-analytics-ims-13.png)

1. Revise as credenciais e continue com **Próximo**:

   ![Revisar credenciais](assets/integration-analytics-ims-15.png)

1. Selecione os perfis de produto necessários e continue com **Salvar API configurada**:

   ![Selecionar perfis de produto necessários](assets/integration-analytics-ims-16.png)

1. A configuração será confirmada.

### Atribuir privilégios à integração {#assigning-privileges-to-the-integration}

Agora, você deve atribuir os privilégios necessários à integração:

1. Abra o Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Navegar para **Produtos** (barra de ferramentas superior), em seguida, selecione **Adobe Analytics - &lt;*your-tenant-id*>** (no painel esquerdo).
1. Selecionar **Perfis de produto**, seu espaço de trabalho necessário na lista apresentada. Por exemplo, Espaço de trabalho padrão.
1. Selecionar **Credenciais da API**, em seguida, a configuração de integração necessária.
1. Selecionar **Editor** como **Função do produto**; em vez de **Observador**.

## Detalhes armazenados para o Projeto de integração do Console do Desenvolvedor do Adobe {#details-stored-for-the-ims-integration-project}

No console Adobe Developer - Projetos, é possível ver uma lista de todos os seus projetos de integração:

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

Selecione uma entrada de projeto específica para mostrar mais detalhes sobre a configuração. Dentre elas:

* Visão geral do projeto
* Insights
* Credenciais
   * Conta de serviço (JWT)
      * Detalhes da credencial
      * Gerar JWT
* APIS
   * Por exemplo, Adobe Analytics

Alguns deles, você precisará concluir a integração do Adobe Analytics no AEM com base no IMS.

## Concluir a configuração IMS no AEM {#completing-the-ims-configuration-in-aem}

Ao retornar para AEM é possível concluir a configuração do IMS adicionando valores necessários da integração IMS para o Analytics:

1. Retorne ao [Configuração IMS aberta no AEM](#configuring-ims-generating-a-public-key).
1. Selecione **Próximo**.

1. Aqui você pode usar o [detalhes da configuração do projeto no Adobe Developer Console](#details-stored-for-the-ims-integration-project):

   * **Título**: Seu texto.
   * **Servidor de autorização**: Copie/cole no `aud` da **Carga** seção abaixo, por exemplo `https://ims-na1.adobelogin.com` no exemplo abaixo
   * **Chave da API**: Copie isso do **Credenciais** da seção [Visão geral do projeto](#details-stored-for-the-ims-integration-project)
   * **Segredo do cliente**: Gere isso no [Guia Segredo do cliente da seção Conta de serviço (JWT)](#details-stored-for-the-ims-integration-project)e copiar
   * **Carga**: Copie isso do [Guia Gerar JWT da seção Conta de Serviço (JWT)](#details-stored-for-the-ims-integration-project)

   ![Detalhes da configuração do AEM IMS](assets/integrate-analytics-ims-10.png)

1. Confirme com **Criar**.

1. Sua configuração do Adobe Analytics será exibida no console AEM.

   ![Configuração IMS](assets/integrate-analytics-ims-11.png)

## Confirmação da configuração IMS {#confirming-the-ims-configuration}

Para confirmar que a configuração está funcionando como esperado:

1. Abrir:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por exemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Selecione sua configuração.
1. Selecionar **Verificar integridade** na barra de ferramentas, seguida por **Verificar**.

   ![Configuração IMS - Verificar integridade](assets/integrate-analytics-ims-12.png)

1. Se bem-sucedido, você verá uma mensagem de confirmação.

## Concluir a integração com o Adobe Analytics {#complete-the-integration-with-adobe-analytics}

Agora você pode usar essa configuração IMS para concluir a [integração com o Adobe Analytics](/help/sites-cloud/integrating/integrating-adobe-analytics.md).

<!--
## Configuring the Adobe Analytics Cloud Service {#configuring-the-adobe-analytics-cloud-service}

The configuration can now be referenced for a Cloud Service to use the Analytics Standard API:

1. Open the **Tools** menu. Then, within the **Cloud Services** section, select **Legacy Cloud Services**.
1. Scroll down to **Adobe Analytics** and select **Configure now**.

   The **Create Configuration** dialog will open.

1. Enter a **Title** and, if you want, a **Name** (if left blank this will be generated from the title).

   You can also select the required template (if more than one is available).

1. Confirm with **Create**.

   The **Edit Component** dialog will open.

1. Enter the details in the **Analytics Settings** tab:

    * **Authentication**: IMS

    * **IMS Configuration**: select the name of the IMS Configuration

1. Click **Connect to Analytics** to initialize the connection with Adobe Analytics.

   If the connection is successful, the message **Connection successful** is displayed.

1. Select **OK** on the message.

1. Complete other parameters as required, followed by **OK** on the dialog to confirm the configuration.

1. You can now proceed to [Adding an Analytics Framework](/help/sites-administering/adobeanalytics-connect.md) to configure parameters that will be sent to Adobe Analytics. 
-->
