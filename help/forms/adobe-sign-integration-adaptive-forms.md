---
title: Como integrar o Adobe Acrobat Sign com o AEM Forms?
description: Saiba como configurar o Adobe Acrobat Sign para [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms, Acrobat Sign
role: Admin, User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 67d8de3cda921dcaeaac47e64828abbe6abe943f
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 1%

---

# Conectar [!DNL AEM Forms] as a Cloud Service com [!DNL Adobe Acrobat Sign] {#integrate-adobe-sign-with-aem-forms}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms.html#adobe-acrobat-sign-for-government) |
| AEM as a Cloud Service | Este artigo |

[!DNL Adobe Acrobat Sign] permite fluxos de trabalho de assinatura eletrônica para fluxos de trabalho adaptáveis do Forms e AEM. As assinaturas eletrônicas melhoram os fluxos de trabalho para processar documentos para áreas jurídicas, de vendas, de folha de pagamento, de gerenciamento de recursos humanos e muito mais.

Em um [!DNL Adobe Acrobat Sign] e Adaptive Forms, um usuário preenche um Formulário adaptável para solicitar um serviço. Por exemplo, um aplicativo de cartão de crédito e um formulário de benefícios para o cidadão. Quando um usuário preenche, envia e assina o formulário de aplicativo, ele é enviado ao provedor de serviços para que seja tomada uma nova ação. O provedor de serviços analisa o aplicativo e usa [!DNL Adobe Acrobat Sign] para marcar o pedido como aprovado. O AEM Forms é compatível com Adobe Acrobat Sign e Adobe Acrobat Sign Solutions para o governo. Dependendo da sua licença e dos requisitos, você pode integrar ou conectar o AEM Forms a qualquer uma das soluções:

* [Conectar o AEM Forms com o Adobe Acrobat Sign](#adobe-sign)
* [Conectar o AEM Forms com o Adobe Acrobat Sign Solutions para o governo](#adobe-acrobat-sign-for-government)

## Conectar o AEM Forms com o Adobe Acrobat Sign {#adobe-sign}

Para conectar **[!DNL AEM Forms]** com **[!DNL Adobe Acrobat Sign]**, configure o software e as contas listados na seção de pré-requisitos e configure o Adobe Sign Cloud Service nas instâncias do Autor e de Publicação as a Cloud Service do Forms:

### Pré-requisitos para conectar o AEM Forms ao Adobe Acrobat Sign {#prerequisites-for-adobe-sign}

Você precisa da seguinte configuração para integrar [!DNL Adobe Acrobat Sign] com [!DNL AEM Forms]:

1. Um ativo [Conta de desenvolvedor do Adobe Acrobat Sign](https://acrobat.adobe.com/us/en/sign/developer-form.html).
1. Um [aplicativo da API do Adobe Acrobat Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
1. Credenciais (ID do cliente e segredo do cliente) de [!DNL Adobe Acrobat Sign] aplicativo da API.
1. (Somente para autenticação baseada em ID do governo) [Habilitar o método de autenticação](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) para autenticação da ID do governo.

### Conectar instâncias do Autor e de publicação do AEM Forms com o Adobe Acrobat Sign {#configure-adobe-sign-with-aem-forms}

Depois que os pré-requisitos estiverem em vigor, execute as seguintes etapas para configurar [!DNL Adobe Acrobat Sign] com [!DNL AEM Forms] nas instâncias do Autor.

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. No **[!UICONTROL Navegador de configuração]** selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, ative **[!UICONTROL Configurações da nuvem]** e selecione **[!UICONTROL Criar]**. Ele cria um contêiner de configuração para armazenar Cloud Service. Verifique se o nome da pasta não contém nenhum espaço.
1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** e abra o container de configuração criado na etapa anterior.

   >[!NOTE]
   >
   >Ao criar um Formulário adaptável, especifique o nome do contêiner na **[!UICONTROL Contêiner de configuração]** campo.

1. Na página de configuração, selecione **[!UICONTROL Criar]** para criar [!DNL Adobe Acrobat Sign] configuração no AEM Forms.
1. No **[!UICONTROL Geral]** guia do **[!UICONTROL Criar configuração do Adobe Acrobat Sign]** página, especifique um **[!UICONTROL Nome]** para a configuração e selecione **[!UICONTROL Próxima]**. Opcionalmente, é possível especificar um **[!UICONTROL Título]** e navegue para selecionar um **[!UICONTROL Miniatura]** para a configuração.

1. Agora é possível **[!UICONTROL Selecionar solução]** para selecionar [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions](assets/adobe-sign-solution.png)

<!--

[create URL](#create-a-redirect-url-for-your-aem-instance)
 -->

1. Copie o URL presente na janela atual do navegador para um bloco de notas e remova a parte `/ui#/aem` do URL. O URL modificado é então necessário para configurar o [!DNL Adobe Acrobat Sign] aplicativo com [!DNL AEM Forms], em uma etapa posterior. Selecione **[!UICONTROL Próximo]**.

1. No **[!UICONTROL Configurações]** guia,
   * o **[!UICONTROL URL do OAuth]** contém o URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/public/oauth/v2`

     Por exemplo:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * o **[!UICONTROL URL do token de acesso]** contém o URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/oauth/v2/token`

     Por exemplo:
     `https://api.na1.echosign.com/oauth/v2/token`

   em que:

   **na1** refere-se ao fragmento de banco de dados padrão. Você pode modificar o valor do fragmento de banco de dados. Certifique-se de que o [!DNL  Adobe Acrobat Sign] As configurações de nuvem apontam para a variável [corrigir fragmento](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   >* Mantenha a **Criar configuração do Adobe Acrobat Sign** página aberta. Não feche. Você pode recuperar **ID do cliente** e **Segredo do cliente** após definir as configurações de OAuth para o [!DNL Adobe Acrobat Sign] conforme descrito nas próximas etapas.
   > * Depois de fazer logon na conta da Adobe Sign, navegue até **[!UICONTROL API do Acrobat Sign]** > **[!UICONTROL Informações da API]** > **[!UICONTROL Documentação de Métodos da API REST]** > **[!UICONTROL Token de acesso OAuth]** para acessar informações relacionadas ao URL do OAuth e ao URL do token de acesso do Adobe Sign.

1. Defina as configurações de OAuth para o [!DNL Adobe Acrobat Sign] aplicativo:

   1. Abra uma janela do navegador e faça logon no [!DNL Adobe Acrobat Sign] conta de desenvolvedor.
   1. Selecione o aplicativo configurado para [!DNL AEM Forms]e selecione **[!UICONTROL Configurar OAuth para Aplicativo]**.
   1. No **[!UICONTROL URL de redirecionamento]** adicione o URL copiado em uma etapa anterior (Etapa 8) e clique em **[!UICONTROL Salvar]**.
   1. Habilite o seguinte Escopo para o [!DNL Adobe Acrobat Sign] e clique em **[!UICONTROL Salvar]**.

   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   Para obter informações passo a passo sobre como definir as configurações de OAuth para um [!DNL Adobe Acrobat Sign] e obter as chaves, consulte [Definir configurações de oAuth para o aplicativo](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentação do desenvolvedor.

   ![Configuração do OAuth](/help/forms/assets/oauthconfig-new.png)

1. Volte para o **[!UICONTROL Criar configuração do Adobe Acrobat Sign]** página. No **[!UICONTROL Configurações]** especifique a variável [**[!UICONTROL ID do cliente]** (também conhecido como ID do aplicativo) e **[!UICONTROL Segredo do cliente]**]. Use o [ID do cliente e segredo do cliente do aplicativo Adobe Acrobat Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) criado na etapa anterior.

1. Selecione o **[!UICONTROL Ativar Adobe Acrobat Sign para anexos]** opção para anexar arquivos anexados a um Formulário adaptável aos arquivos correspondentes [!DNL Adobe Acrobat Sign] documento enviado para assinatura.

1. Selecionar **[!UICONTROL Conectar-se ao Adobe Acrobat Sign]**. Quando solicitado a fornecer credenciais, forneça **nome de usuário** e **senha** da conta usada ao criar [!DNL Adobe Acrobat Sign] aplicação. Quando solicitado a confirmar, acesse para `your developer account`, Clique em **[!UICONTROL Permitir acesso]**. Se as credenciais estiverem corretas e você permitir [!DNL AEM Forms] para acessar o [!DNL Adobe Acrobat Sign] conta de desenvolvedor, uma mensagem de sucesso semelhante à seguinte é exibida.

   ![Êxito na configuração da nuvem do Adobe Acrobat Sign](assets/adobe-sign-cloud-configuration-success.png)

1. Selecionar **[!UICONTROL Criar]** para criar o [!DNL Adobe Acrobat Sign] configuração.

1. Selecione a configuração e clique em **[!UICONTROL Publish]**, selecione a configuração e clique em **[!UICONTROL Publish]**. Ele replica a configuração nos ambientes de publicação correspondentes.

1. Repita todas as etapas acima nas instâncias de desenvolvedor, preparo e produção (qualquer uma que tenha restado) para concluir a configuração [!DNL Adobe Acrobat Sign] com [!DNL AEM Forms] para o seu ambiente.

Agora, você pode [usar adicionar campos do Adobe Acrobat Sign a um formulário adaptável](working-with-adobe-sign.md). Adicione o contêiner de configuração usado para o Cloud Service a todo o Forms adaptável que está sendo habilitado para [!DNL Adobe Acrobat Sign]. Você pode especificar um contêiner de configuração nas propriedades de um Formulário adaptável.

>[!NOTE]
>
> Para configurar a sandbox da Adobe Sign, você pode seguir as mesmas etapas de configuração descritas em [Adobe Sign](#adobe-sign).

## Conectar o AEM Forms com o Adobe Acrobat Sign Solutions para o governo {#adobe-acrobat-sign-for-government}

A conexão do AEM Forms com o Adobe Acrobat Sign Solutions para o governo é um processo de várias etapas. Envolve:

* Criação de um URL de redirecionamento para suas instâncias do AEM
* Compartilhamento do URL de redirecionamento e escopos com a equipe do Adobe Sign Solutions for Government
* Recebimento de credenciais da equipe do Adobe Sign
* Usar as credenciais recebidas para conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government

![Fluxo de trabalho do Adobe Sign Government](/help/forms/assets/adobe-acrobat-sign-govt-workflow.png)


O AEM Forms as a Cloud Service fornece ambientes de desenvolvimento, preparo e produção. Você pode começar com a conexão do seu ambiente de desenvolvimento para com o Adobe Acrobat Sign Solutions for Government e conectar os ambientes de preparo e produção posteriormente.

### Antes de começar {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Antes de começar a conectar o AEM Forms com a solução da Adobe Acrobat Sign, verifique se [Adobe Acrobat Sign Solutions para o governo](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) conta provisionada.


### Conecte o AEM Forms as a Cloud Service com o Adobe Acrobat Sign Solutions for Government {#connect-adobe-acrobat-sign-for-government}

#### Criar um URL de redirecionamento para sua instância do AEM

1. Na instância do autor as a Cloud Service do Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. No **[!UICONTROL Navegador de configuração]** selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, ative **[!UICONTROL Configurações da nuvem]** e selecione **[!UICONTROL Criar]**. Ele cria um contêiner de configuração para armazenar Cloud Service. Verifique se o nome da pasta não contém nenhum espaço.
1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** e abra o container de configuração criado na etapa anterior. Ao criar um Formulário adaptável, especifique o nome do contêiner na **[!UICONTROL Contêiner de configuração]** campo.
1. Na página de configuração, selecione **[!UICONTROL Criar]** para criar [!DNL Adobe Acrobat Sign] configuração no AEM Forms.
1. Copie o URL da janela atual do navegador para um bloco de notas e remova `/ui#/aem` do URL. Esse URL é chamado de `re-direct URL`.
Na próxima seção, você compartilhará o `re-direct URL` e `Scopes` com a equipe do Adobe Sign e solicite credenciais (ID do cliente e Segredo do cliente).

#### Compartilhar a URL de redirecionamento e os escopos com a equipe do Adobe Sign e receber credenciais

A equipe de soluções da Adobe Acrobat Sign para o governo exige a `re-direct URL` e os escopos específicos a serem ativados para que o aplicativo Adobe Acrobat Sign (listado abaixo) gere credenciais (ID do cliente e Segredo do cliente) que permitem conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government.

Compartilhe o `scopes` (listadas abaixo) e o `re-direct URL` criou e anotou a última etapa da seção anterior com seu representante de soluções para o governo da Adobe Acrobat Sign ([Membro da equipe do Adobe Professional Services](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password)).

**_Escopos_**

* [!DNL aggrement_read]
* [!DNL aggrement_write]
* [!DNL aggrement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

O representante gera e compartilha credenciais com você. Na próxima seção, use as credenciais (ID do cliente e Segredo do cliente) para conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government.

#### Use as credenciais recebidas para conectar o AEM Forms ao Adobe Acrobat Sign Solutions for Government

1. Abra o `re-direct URL` no navegador. Você criou e anotou o `re-direct URL` na última etapa do [criar um URL de redirecionamento na sua instância do AEM](#create-a-redirect-url-for-your-aem-instance) seção.

1. No **[!UICONTROL Geral]** guia do **[!UICONTROL Criar configuração do Adobe Sign]** página, especifique um **[!UICONTROL Nome]** para a configuração e selecione **[!UICONTROL Próxima]**. Opcionalmente, é possível especificar um **[!UICONTROL Título]** e navegue para selecionar um **[!UICONTROL Miniatura]** para a configuração. Clique em **[!UICONTROL Avançar]**.

1. No **[!UICONTROL Configurações]** guia do **[!UICONTROL Criar configuração do Adobe Sign]** página, para o **[!UICONTROL Selecionar solução]** selecione [!DNL Adobe Acrobat Sign Solutions for Government].


   ![Adobe Acrobat Sign Solutions para o governo](assets/adobe-sign-for-govt.png)

1. No **[!UICONTROL E-mail]** especifique o endereço de email associado à sua conta do Adobe Acrobat Sign Solutions for Government.

1. No **[!UICONTROL Configurações]** guia,
   * o **[!UICONTROL URL do OAuth]** contém o URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     Por exemplo:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * o **[!UICONTROL URL do token de acesso]** contém o URL padrão que inclui o fragmento de banco de dados do Adobe Sign. O formato do URL é:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     Por exemplo:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   em que:

   **na1** refere-se ao fragmento de banco de dados padrão. Você pode modificar o valor do fragmento de banco de dados. Certifique-se de que o [!DNL  Adobe Acrobat Sign] As configurações de nuvem apontam para a variável [corrigir fragmento](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   > * Depois de fazer logon na conta da Adobe Sign, navegue até **[!UICONTROL API do Acrobat Sign]** > **[!UICONTROL Informações da API]** > **[!UICONTROL Documentação de Métodos da API REST]** > **[!UICONTROL Token de acesso OAuth]** para acessar informações relacionadas ao URL do Adobe Sign oAuth e ao URL do token de acesso.

1. Usar as credenciais compartilhadas pela Adobe Acrobat Sign para o representante de soluções do governo ([Membro da equipe do Adobe Professional Services]) na seção anterior como [**[!UICONTROL ID do cliente]** e **[!UICONTROL Segredo do cliente]**].

1. Selecione o **[!UICONTROL Ativar Adobe Acrobat Sign para anexos]** opção para anexar arquivos anexados a um Formulário adaptável aos arquivos correspondentes [!DNL Adobe Acrobat Sign] documento enviado para assinatura.

1. Selecionar **[!UICONTROL Conectar-se ao Adobe Sign]**. Quando as credenciais forem solicitadas, forneça o nome de usuário e a senha da conta usada ao criar [!DNL Adobe Acrobat Sign] aplicação. Quando for solicitado que você confirme o acesso de `your developer account`, Clique em **[!UICONTROL Permitir acesso]**. Se as credenciais estiverem corretas e você permitir [!DNL AEM Forms] para acessar o [!DNL Adobe Acrobat Sign] conta de desenvolvedor, uma mensagem de sucesso semelhante à seguinte é exibida.

   ![Êxito na configuração da nuvem do Adobe Acrobat Sign](assets/adobe-sign-cloud-configuration-success.png)

   <!-- > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. -->

1. Selecionar **[!UICONTROL Criar]** para criar a configuração.

1. Selecione a configuração e clique em **[!UICONTROL Publish]**, selecione a configuração e clique em **[!UICONTROL Publish]**. Ele replica a configuração nos ambientes de publicação correspondentes.

1. Repita todas as etapas acima nas instâncias de desenvolvedor, preparo e produção (qualquer uma que tenha restado) para concluir a configuração [!DNL Adobe Acrobat Sign Solutions for Government] com [!DNL AEM Forms] para o seu ambiente.

Agora, você pode [usar a opção adicionar campos do Adobe Acrobat Sign em um Formulário adaptável](working-with-adobe-sign.md) ou [Fluxo de trabalho do AEM](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Adicione o contêiner de configuração usado para a configuração do Cloud Service a todo o Forms adaptável que está sendo habilitado para [!DNL Adobe Acrobat Sign]. Você pode especificar um contêiner de configuração nas propriedades de um Formulário adaptável.

## Configurar [!DNL Adobe Acrobat Sign] scheduler para sincronizar o status de assinatura {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

O AEM Forms as a Cloud Service fornece um serviço de scheduler que verifica o status dos signatários em intervalos definidos. Os cenários nos quais você configura o serviço scheduler:

* Se você usar [Enviar o formulário (depois que cada recipient concluir a cerimônia de assinatura)](/help/forms/working-with-adobe-sign.md#select-adobe-sign-cloud-service-and-signing-order) para assinar um documento, o formulário é enviado somente após todos os signatários terem assinado o formulário.
* Se você usar o [Etapa de assinatura em um fluxo de trabalho do AEM](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step) para assinar um documento, a etapa assinar aguarda todos os signatários assinarem o documento antes de prosseguir para a próxima etapa do fluxo de trabalho.

Por padrão, a variável [!DNL Adobe Acrobat Sign] Os serviços do scheduler verificam (pesquisa) a resposta do assinante a cada 24 horas. Você pode alterar o intervalo padrão do seu ambiente.

Para alterar o intervalo padrão, especifique um [expressão CRON](https://en.wikipedia.org/wiki/Cron#CRON_expression) para o **sign.status.exp** propriedade do **Serviço de configuração do Adobe Acrobat Sign** configuração.

Por exemplo, para executar o serviço de configuração diariamente às 00:00, defina a **sign.status.exp** propriedade do **Serviço de configuração do Adobe Acrobat Sign** configuração a ser especificada `0 0 0 1/1 * ? *`. O arquivo JSON a seguir exibe a amostra para executar o serviço de configuração diariamente às 00:00:

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

Para definir valores de uma configuração, [Gerar configurações de OSGi usando o SDK do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart), e [implantar a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) para a instância do Cloud Service.


>[!MORELIKETHIS]
>
>* [Assinatura eletrônica de um formulário usando assinaturas escritas](/help/forms/signing-forms-using-scribble.md)
>* [Práticas recomendadas para usar o Adobe Acrobat Sign com o Adaptive Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)