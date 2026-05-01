---
title: Como enviar dados para um armazenamento de Lista do SharePoint no envio de um Formulário adaptável?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: Como conectar a lista do SharePoint para um formulário adaptável?, Enviar para o SharePoint, Criar uma configuração de lista do SharePoint, Usar a ação enviar Enviar para o SharePoint em um formulário adaptável, Conectar um formulário adaptável à lista do Microsoft&reg; SharePoint.
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="Aplicável ao AEM Forms)."
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 0e5045b87719781301d91874c7355eda9426beef
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 4%

---

# Conectar um formulário adaptável à lista Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

<span> Este vídeo se aplica somente aos Componentes principais. Para Componentes UE/Foundation, consulte o artigo.</span>

Para usar a ação enviar [!UICONTROL Enviar para a Lista do SharePoint] em um formulário adaptável:

1. [Criar uma Configuração de Lista do SharePoint](#1-create-a-sharepoint-list-configuration): ela conecta o AEM Forms ao Armazenamento de Lista do Microsoft® Sharepoint.
1. [Usar o Enviar usando o Modelo de Dados de Formulário (FDM) em um Formulário Adaptável](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm): ele conecta seu Formulário Adaptável ao Microsoft® SharePoint configurado.

## &#x200B;1. Criar uma configuração de lista do SharePoint

Para conectar o AEM Forms à sua lista do Microsoft® Sharepoint:

1. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços na Nuvem]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Selecione um **Contêiner de Configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]** > **[!UICONTROL Lista do SharePoint]** na lista suspensa. O assistente de configuração do SharePoint é exibido.
1. Especifique o **[!UICONTROL Título]**, **[!UICONTROL ID do Cliente]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL URL do OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente e a ID do locatário para a URL do OAuth, consulte a [Documentação da Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar os `Client ID` e `Client Secret` do seu aplicativo no portal Microsoft® Azure.
   * No portal Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Substitua `[author-instance]` pela URL da sua instância de Autor.
   * Adicione as permissões de API `offline_access` e `Sites.Manage.All` na guia **Microsoft® Graph** para fornecer permissões de leitura/gravação. Adicione a permissão `AllSites.Manage` na guia **Sharepoint** para interagir remotamente com os dados do SharePoint.
   * Usar URL do OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substitua `<tenant-id>` pelo `tenant-id` do seu aplicativo no portal Microsoft® Azure.

     >[!NOTE]
     >
     > O campo **segredo do cliente** é obrigatório ou opcional, depende da configuração do aplicativo do Azure Ative Diretory. Se o aplicativo estiver configurado para usar um segredo do cliente, é obrigatório fornecer o segredo do cliente.

1. Clique em **[!UICONTROL Conectar]**. Em uma conexão bem-sucedida, a mensagem `Connection Successful` é exibida.
1. Selecione **[!UICONTROL Site do SharePoint]** e **[!UICONTROL Lista do SharePoint]** na lista suspensa.
1. Selecione **[!UICONTROL Criar]** para criar a configuração de nuvem do Microsoft® SharePointList.

### Autenticação baseada em certificado {#certificate-based-authentication}

A autenticação baseada em certificado <span class="preview"> para a configuração da Lista do SharePoint está no Early Adoter Program. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

No assistente de configuração de lista do SharePoint:

1. Definir **[!UICONTROL Tipo de Autenticação]** como **Autenticação baseada em certificado**.
1. Especifique **[!UICONTROL Título]**, **[!UICONTROL ID do Cliente]**, **[!UICONTROL Alias do Certificado]**, **[!UICONTROL ID do Locatário]** e **[!UICONTROL Nome do Locatário]**.
1. Insira a **[!UICONTROL URL do Site do SharePoint]**, verifique a conexão do site se necessário e selecione a **[!UICONTROL Lista do SharePoint]**.
1. Clique em **[!UICONTROL Conectar]** para verificar a conexão e em **[!UICONTROL Salvar e Fechar]** para salvar a configuração.

A captura de tela abaixo exibe a configuração da Lista do SharePoint com **Autenticação baseada em certificado**:

![Configuração da Lista do SharePoint com autenticação baseada em certificado](/help/forms/assets/sharepoint-list-certificate-auth-configuration.png){width=50%, height=50%, align=center}

Para preparar o certificado para o AEM e o Microsoft Azure, execute as seguintes etapas no AEM e, em seguida, registre o certificado público no Microsoft Azure.

**No AEM**

1. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
1. Pesquise por **[!UICONTROL fd-cloudservice]**, selecione o usuário e clique em **[!UICONTROL Propriedades]**.
1. Abra a guia **[!UICONTROL Armazenamento de chaves]**. Se um armazenamento de chaves ainda não tiver sido criado, clique em **[!UICONTROL Criar Armazenamento de Chaves]** e conclua as solicitações para definir a senha do armazenamento de chaves.
1. Adicione a chave privada ao keystore: expanda **[!UICONTROL Adicionar chave privada do arquivo Keystore]** e carregue seu arquivo **.jks**.
1. Insira um **[!UICONTROL Alias]** que corresponda ao **[!UICONTROL Alias do Certificado]** na configuração da Lista do SharePoint, envie o material da chave e clique em **[!UICONTROL Salvar e Fechar]**.

A captura de tela exibe o keystore após a adição do certificado. O **[!UICONTROL Alias]** deve corresponder ao **[!UICONTROL Alias do Certificado]** na configuração de nuvem da Lista do SharePoint:

![fd-cloudservice user Keystore com alias do certificado](/help/forms/assets/fd-cloudservice-keystore-certificate.png){width=50%, height=50%, align=center}

**No Microsoft Azure**

1. Abra o registro do seu aplicativo e acesse **Certificados e segredos** > **Certificados**.
1. Selecione **Carregar certificado** e carregue o arquivo de certificado (chave pública) no qual o Azure deve confiar para o aplicativo.

A captura de tela exibe a guia **Certificados** no portal do Azure, onde você pode carregar o certificado para o registro do aplicativo:

![Certificados e segredos do registro do aplicativo Azure](/help/forms/assets/azure-app-registration-sharepoint-certificates.png){width=50%, height=50%, align=center}

## &#x200B;2. Usar o Enviar usando o Modelo de dados de formulário (FDM) em um formulário adaptável {#use-submit-using-fdm}

Você pode usar a configuração da Lista do SharePoint criada em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma Lista do SharePoint. Execute as seguintes etapas para usar uma Lista SharePoint em um Formulário adaptável como:

1. [Criar um modelo de dados de formulário (FDM) usando a configuração da Lista do Microsoft® SharePoint](/help/forms/create-form-data-models.md)
1. [Configurar o Modelo de dados de formulário (FDM) para recuperar e enviar dados](/help/forms/work-with-form-data-model.md#configure-services)
1. [Criação de um Formulário adaptável](/help/forms/creating-adaptive-form-core-components.md)
1. [Configurar a ação Enviar usando um Modelo de dados de formulário (FDM)](/help/forms/using-form-data-model.md)

Ao enviar o formulário, os dados são salvos no Armazenamento de Lista do Microsoft® Sharepoint especificado.

>[!NOTE]
>
> Na Lista do Microsoft® SharePoint, os seguintes tipos de coluna não são suportados:
>
> * coluna de imagem
> * coluna de metadados
> * coluna de pessoa
> * coluna de dados externos

## Artigos relacionados

{{af-submit-action}}
