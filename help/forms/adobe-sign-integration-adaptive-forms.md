---
title: Como integrar o Adobe Sign com o AEM Forms?
description: Saiba como configurar o Adobe Sign para [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 00dced631aa293630f923ee1e94f321bbf4cddb9
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 1%

---

# Integrar [!DNL Adobe Sign] com [!DNL AEM Forms] as a Cloud Service  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] habilita fluxos de trabalho de assinatura eletrônica para o Adaptive Forms. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas legais, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muitas outras.

Em um [!DNL Adobe Sign] e Adaptive Forms , um usuário preenche um formulário adaptável para se candidatar a um serviço. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que você possa realizar mais ações. O provedor de serviços revisa o aplicativo e os usos [!DNL Adobe Sign] para assinalar o pedido aprovado. Para ativar workflows semelhantes de assinatura eletrônica, é possível integrar [!DNL Adobe Sign] com [!DNL AEM Forms].

Para usar [!DNL Adobe Sign] com [!DNL AEM Forms], configurar [!DNL Adobe Sign] no AEM Cloud Services:

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para integrar [!DNL Adobe Sign] com [!DNL AEM Forms]:

* Uma atividade [Conta de desenvolvedor do Adobe Sign](https://acrobat.adobe.com/us/en/sign/developer-form.html).
* Um [Aplicativo de API do Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenciais (ID do cliente e Segredo do cliente) de [!DNL Adobe Sign] Aplicativo de API.
* Use [chave de criptografia idêntica](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#make-sure-you-properly-replicate-encryption-keys-when-needed) para instâncias de criação e publicação.
* (Somente para autenticação baseada em ID do governo) [Habilitar o método de autenticação](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) para autenticação de ID de governo.

## Configurar o[!DNL Adobe Sign] com o [!DNL AEM Forms] {#configure-adobe-sign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para configurar [!DNL Adobe Sign] com [!DNL AEM Forms] nas instâncias de Autor.

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. No **[!UICONTROL Navegador de configuração]** página, toque em **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, habilite **[!UICONTROL Configurações da nuvem]** e toque em **[!UICONTROL Criar]**. Ele cria um contêiner de configuração para armazenar Cloud Services. Certifique-se de que o nome da pasta não contenha espaço.
1. Navegar para **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e abra o contêiner de configuração criado na etapa anterior.

   >[!NOTE]
   >
   >Ao criar um Formulário adaptável, especifique o nome do contêiner na **[!UICONTROL Contêiner de configuração]** campo.

1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar [!DNL Adobe Sign] na AEM Forms.
1. No **[!UICONTROL Geral]** da guia **[!UICONTROL Criar configuração do Adobe Sign]** especifique um **[!UICONTROL Nome]** para a configuração, e toque em **[!UICONTROL Próximo]**. Como opção, você pode especificar uma **[!UICONTROL Título]** e navegue para selecionar uma **[!UICONTROL Miniatura]** para a configuração.

1. Copie o URL na janela atual do navegador para um bloco de notas. O URL é necessário para configurar [!DNL Adobe Sign] aplicativo com [!DNL AEM Forms] em uma etapa posterior.

1. Defina as configurações de OAuth para a variável [!DNL Adobe Sign] aplicativo:

   1. Abra uma janela do navegador e faça logon em sua [!DNL Adobe Sign] conta do desenvolvedor.
   1. Selecione o aplicativo configurado para [!DNL AEM Forms]e toque em **[!UICONTROL Configurar o OAuth para aplicativo]**.
   1. No **[!UICONTROL Redirecionar URL]** , adicione o URL copiado na etapa anterior e clique em **[!UICONTROL Salvar]**.
   1. Ative as seguintes configurações de OAuth para o [!DNL Adobe Sign] e clique em **[!UICONTROL Salvar]**.
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   Para obter informações passo a passo sobre a configuração do OAuth para um [!DNL Adobe Sign] e obtenha as chaves, consulte [Definir configurações de oAuth para o aplicativo](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentação do desenvolvedor.

   ![Configuração OAuth](assets/oauthconfig_new.png)

1. Volte para o **[!UICONTROL Criar configuração do Adobe Sign]** página. No **[!UICONTROL Configurações]** , a variável **[!UICONTROL URL de OAuth]** menciona o URL padrão. O formato do URL é:

   `https://<shard>/public/oAuth/v2`

   Por exemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   em que:

   **na1** refere-se ao compartilhamento de banco de dados padrão. Você pode modificar o valor do compartilhamento de banco de dados. Certifique-se de que [!DNL Adobe Sign] As Configurações de nuvem apontam para a [Shard correto](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Se você criar outro [!DNL Adobe Sign] para um recurso ou componente do Adobe Experience Manager, verifique se todas as [!DNL Adobe Sign] As Configurações de nuvem apontam para o mesmo compartilhamento.

1. Especifique a **[!UICONTROL ID do cliente]** (também referido como ID do pedido) e **[!UICONTROL Segredo do cliente]**. Use a ID do cliente e o Segredo do cliente do aplicativo Adobe Sign criados na etapa anterior.

1. Selecione o **[!UICONTROL Ativar o Adobe Sign para anexos]** opção para anexar arquivos anexados a um formulário adaptável ao formulário correspondente [!DNL Adobe Sign] documento enviado para assinatura.

1. Toque **[!UICONTROL Conectar-se ao Adobe Sign]**. Quando solicitado a fornecer credenciais, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Sign] aplicativo. Quando solicitado a confirmar o acesso para `your developer account`, Clique em **[!UICONTROL Permitir acesso]**. Se as credenciais estiverem corretas e você permitir [!DNL AEM Forms] para acessar seu [!DNL Adobe Sign] conta do desenvolvedor, é exibida uma mensagem de sucesso semelhante à seguinte.

   ![Êxito na configuração da Adobe Sign Cloud](assets/adobe-sign-cloud-configuration-success.png)

1. Toque **[!UICONTROL Criar]** para criar o [!DNL Adobe Sign] configuração.

1. Selecione a configuração e clique em **[!UICONTROL Publicar]**, selecione a configuração e clique em **[!UICONTROL Publicar]**. Ele replica a configuração em ambientes de publicação correspondentes.

1. Repita todas as etapas acima nas instâncias de desenvolvedor, estágio e produção (o que restar) para concluir a configuração [!DNL Adobe Sign] com [!DNL AEM Forms] para seu ambiente.

Agora, você pode [usar adicionar campos Adobe Sign a um formulário adaptável](working-with-adobe-sign.md). Certifique-se de adicionar o contêiner de configuração usado para o Cloud Service a todo o Adaptive Forms que está sendo ativado para [!DNL Adobe Sign]. É possível especificar um contêiner de configuração a partir das propriedades de um formulário adaptável.

## (Somente para fluxos de trabalho de AEM) Configurar [!DNL Adobe Sign] agendador para sincronizar o status de assinatura {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Ao utilizar [!DNL Adobe Sign] Etapa do fluxo de trabalho para Assinar um formulário adaptável, o formulário pode ser passado entre signatários um após o outro ou pode ser enviado a todos os signatários simultaneamente, dependendo da etapa de configuração do fluxo de trabalho. [!DNL Adobe Sign] ativado O Adaptive Forms é enviado para o Experience Manager Forms Server somente depois que todos os signatários concluírem o processo de assinatura.

Por padrão, a variável [!DNL Adobe Sign] As verificações de serviços do agendador (pesquisas) respondem ao assinante após cada 24 horas. Você pode alterar o intervalo padrão do seu ambiente.

Para alterar o intervalo padrão, especifique um [expressão cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) para **sign.status.exp** da **Serviço de configuração do Adobe Sign** configuração.

Por exemplo, para executar o serviço de configuração diariamente às 00:00, defina a variável **sign.status.exp** da **Serviço de configuração do Adobe Sign** configuração para especificar `0 0 0 1/1 * ? *`. O arquivo JSON a seguir exibe a amostra para executar o serviço de configuração diariamente às 00:00:

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

Para definir valores de uma configuração, [Gerar configurações de OSGi usando o SDK AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)e [implantar a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) para a instância do Cloud Service.

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## Artigos relacionados {#related-articles}

* [Uso do Adobe Sign em um formulário adaptável](working-with-adobe-sign.md)

* [Práticas recomendadas para usar o Adobe Sign com o Adaptive Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
