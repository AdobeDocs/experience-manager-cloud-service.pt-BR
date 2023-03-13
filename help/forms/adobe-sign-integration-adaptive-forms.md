---
title: Como integrar o Adobe Sign com o AEM Forms?
description: Saiba como configurar o Adobe Sign para [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 7b233d95e27325a7edb22948669f6c0d96e1f380
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 1%

---

# Integrar [!DNL Adobe Sign] com [!DNL AEM Forms] as a Cloud Service  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] habilita fluxos de trabalho de assinatura eletrônica para o Adaptive Forms. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas jurídicas, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muito mais.

Em um [!DNL Adobe Sign] e Adaptive Forms, um usuário preenche um Formulário adaptável para solicitar um serviço. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que seja tomada uma nova ação. O provedor de serviços analisa o aplicativo e usa [!DNL Adobe Sign] para marcar o pedido como aprovado. Para habilitar workflows de assinatura eletrônica semelhantes, é possível integrar [!DNL Adobe Sign] com [!DNL AEM Forms].

Para usar [!DNL Adobe Sign] com [!DNL AEM Forms], configurar [!DNL Adobe Sign] nos serviços em nuvem AEM:

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para integrar [!DNL Adobe Sign] com [!DNL AEM Forms]:

* Um ativo [Conta de desenvolvedor do Adobe Sign](https://acrobat.adobe.com/us/en/sign/developer-form.html).
* Um [aplicativo da API do Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenciais (ID do cliente e segredo do cliente) de [!DNL Adobe Sign] aplicativo da API.
* Uso [chave criptográfica idêntica](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#make-sure-you-properly-replicate-encryption-keys-when-needed) para instâncias de criação e publicação.
* (Somente para autenticação com base em ID do governo) [Habilitar o método de autenticação](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) para autenticação da ID do governo.

## Configurar o [!DNL Adobe Sign] com o [!DNL AEM Forms] {#configure-adobe-sign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para configurar [!DNL Adobe Sign] com [!DNL AEM Forms] nas instâncias do Autor.

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. No **[!UICONTROL Navegador de configuração]** página, toque em **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, ative **[!UICONTROL Configurações da nuvem]** e toque em **[!UICONTROL Criar]**. Ele cria um contêiner de configuração para armazenar Cloud Services. Verifique se o nome da pasta não contém nenhum espaço.
1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e abra o container de configuração criado na etapa anterior.

   >[!NOTE]
   >
   >Ao criar um Formulário adaptável, especifique o nome do contêiner na **[!UICONTROL Contêiner de configuração]** campo.

1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar [!DNL Adobe Sign] configuração no AEM Forms.
1. No **[!UICONTROL Geral]** guia do **[!UICONTROL Criar configuração do Adobe Sign]** página, especifique um **[!UICONTROL Nome]** para a configuração e toque em **[!UICONTROL Próxima]**. Opcionalmente, é possível especificar um **[!UICONTROL Título]** e navegue para selecionar um **[!UICONTROL Miniatura]** para a configuração.

1. Copie o URL na janela atual do navegador para um bloco de notas. O URL é necessário para configurar o [!DNL Adobe Sign] aplicativo com [!DNL AEM Forms] em uma etapa posterior. Toque **[!UICONTROL Próxima]**.

1. No **[!UICONTROL Configurações]** , a guia **[!UICONTROL URL do OAuth]** contém o URL padrão. O formato do URL é:

   `https://<shard>/public/oAuth/v2`

   Por exemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   em que:

   **na1** refere-se ao fragmento de banco de dados padrão. Você pode modificar o valor do fragmento de banco de dados. Certifique-se de que o [!DNL  Adobe Sign] As configurações de nuvem apontam para a variável [corrigir fragmento](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Se você criar outro [!DNL Adobe Sign] para um recurso ou componente do Adobe Experience Manager, verifique se todas as [!DNL Adobe Sign] As configurações de nuvem apontam para o mesmo fragmento.

   >[!NOTE]
   >
   > Mantenha a **Criar configuração do Adobe Sign** página aberta. Não feche. Você pode recuperar **ID do cliente** e **Segredo do cliente** após definir as configurações de OAuth para o [!DNL Adobe Sign] conforme descrito nas próximas etapas.


1. Defina as configurações de OAuth para o [!DNL Adobe Sign] aplicativo:

   1. Abra uma janela do navegador e faça logon no [!DNL Adobe Sign] conta de desenvolvedor.
   1. Selecione o aplicativo configurado para [!DNL AEM Forms]e toque em **[!UICONTROL Configurar OAuth para Aplicativo]**.
   1. No **[!UICONTROL URL de redirecionamento]** adicione o URL copiado em uma etapa anterior (Etapa 7) e clique em **[!UICONTROL Salvar]**.
   1. Habilite o seguinte Escopo para o [!DNL Adobe Sign] e clique em **[!UICONTROL Salvar]**.
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   Para obter informações passo a passo sobre como definir as configurações de OAuth para um [!DNL Adobe Sign] e obter as chaves, consulte [Definir configurações de oAuth para o aplicativo](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentação do desenvolvedor.

   ![Configuração do OAuth](assets/oauthconfig_new.png)

1. Volte para o **[!UICONTROL Criar configuração do Adobe Sign]** página. No **[!UICONTROL Configurações]** especifique a variável [**[!UICONTROL ID do cliente]** (também conhecido como ID do aplicativo) e **[!UICONTROL Segredo do cliente]**]. Use o [ID do cliente e segredo do cliente do aplicativo Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) criado na etapa anterior.

1. Selecione o **[!UICONTROL Ativar Adobe Sign para anexos]** opção para anexar arquivos anexados a um Formulário adaptável aos arquivos correspondentes [!DNL Adobe Sign] documento enviado para assinatura.

1. Toque **[!UICONTROL Conectar-se ao Adobe Sign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Sign] aplicação. Quando for solicitado que você confirme o acesso de `your developer account`, Clique em **[!UICONTROL Permitir acesso]**. Se as credenciais estiverem corretas e você permitir [!DNL AEM Forms] para acessar o [!DNL Adobe Sign] conta de desenvolvedor, uma mensagem de sucesso semelhante à seguinte é exibida.

   ![Êxito na configuração da nuvem do Adobe Sign](assets/adobe-sign-cloud-configuration-success.png)

1. Toque **[!UICONTROL Criar]** para criar o [!DNL Adobe Sign] configuração.

1. Selecione a configuração e clique em **[!UICONTROL Publish]**, selecione a configuração e clique em **[!UICONTROL Publish]**. Ele replica a configuração nos ambientes de publicação correspondentes.

1. Repita todas as etapas acima nas instâncias de desenvolvedor, preparo e produção (qualquer uma que tenha restado) para concluir a configuração [!DNL Adobe Sign] com [!DNL AEM Forms] para o seu ambiente.

Agora, você pode [usar adicionar campos do Adobe Sign a um formulário adaptável](working-with-adobe-sign.md). Adicione o contêiner de configuração usado para o Cloud Service a todo o Forms adaptável que está sendo habilitado para [!DNL Adobe Sign]. Você pode especificar um contêiner de configuração nas propriedades de um Formulário adaptável.

## (Somente para fluxos de trabalho do AEM) Configurar [!DNL Adobe Sign] scheduler para sincronizar o status de assinatura {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Quando você usa [!DNL Adobe Sign] Etapa do fluxo de trabalho para Assinar um Formulário adaptável, o formulário pode ser passado entre os signatários um após o outro ou pode ser enviado para todos os signatários simultaneamente, dependendo da configuração da etapa do fluxo de trabalho. [!DNL Adobe Sign] Os Forms adaptáveis ativados são enviados ao Experience Manager Forms Server somente depois que todos os signatários concluírem o processo de assinatura.

Por padrão, a variável [!DNL Adobe Sign] Os serviços do scheduler verificam (pesquisa) a resposta do assinante a cada 24 horas. Você pode alterar o intervalo padrão do seu ambiente.

Para alterar o intervalo padrão, especifique um [expressão CRON](https://en.wikipedia.org/wiki/Cron#CRON_expression) para o **sign.status.exp** propriedade do **Serviço de configuração do Adobe Sign** configuração.

Por exemplo, para executar o serviço de configuração diariamente às 00:00, defina a **sign.status.exp** propriedade do **Serviço de configuração do Adobe Sign** configuração a ser especificada `0 0 0 1/1 * ? *`. O arquivo JSON a seguir exibe a amostra para executar o serviço de configuração diariamente às 00:00:

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

Para definir valores de uma configuração, [Gerar configurações de OSGi usando o SDK do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart), e [implantar a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) para a instância do Cloud Service.

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## Artigos relacionados {#related-articles}

* [Uso do Adobe Sign em um formulário adaptável](working-with-adobe-sign.md)

* [Práticas recomendadas para usar o Adobe Sign com o Adaptive Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
