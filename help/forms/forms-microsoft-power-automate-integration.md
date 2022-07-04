---
title: Integrar um formulário adaptável ao Microsoft® Power Automate
description: Integre um formulário adaptável ao Microsoft® Power Automate.
hide: true
hidefromtoc: true
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
source-git-commit: ccc4d487cb180273284276cf9cdf18680a3efcb8
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 0%

---

# Conecte um formulário adaptável com o Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

Você pode configurar um Formulário adaptável para executar um fluxo da Microsoft® Power Automate Cloud no envio. O formulário adaptável configurado envia dados capturados, anexos e documentos de registro para o Power Automate Cloud Flow para processamento. Ele ajuda você a criar uma experiência personalizada de captura de dados, aproveitando o poder do Microsoft® Power Automate para criar lógicas comerciais sobre dados capturados e automatizar os fluxos de trabalho do cliente. Estes são alguns exemplos do que você pode fazer após integrar um formulário adaptável com o Microsoft® Power Automate:

* Usar dados adaptáveis do Forms em processos comerciais do Power Automated
* Use o Power Automate para enviar dados capturados para mais de 500 fontes de dados ou qualquer API disponível publicamente
* Executar cálculos complexos em dados capturados
* Salve os dados adaptáveis do Forms em sistemas de armazenamento em um agendamento predefinido

O editor adaptável de Forms fornece o **Chamar um fluxo do Microsoft® Power Automate** enviar ação para enviar dados de formulários adaptáveis, anexos e documentos de registro são enviados para o Fluxo do Power Automate Cloud. Para usar a ação Enviar para enviar dados capturados para o Microsoft® Power Automate, [Conecte sua instância as a Cloud Service do Forms com o Microsoft® Power Automate](forms-microsoft-power-automate-integration.md#connect-forms-server-with-power-automate)

## Pré-requisitos

Os seguintes itens são necessários para conectar um Formulário adaptável com o Microsoft® Power Automate:

* Licença do Microsoft® Power Automate Premium.
* Microsoft® [Fluxo do Power Automated](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) com o `When an HTTP request is received` acionador para aceitar os dados de envio do formulário adaptável.


* Um usuário do Experience Manager com privilégios de autor e administrador do Forms.
* Certifique-se de que a conta usada para se conectar ao Power Automate é o proprietário do fluxo do Power Automate.


## Conecte sua instância as a Cloud Service do Forms com o Microsoft® Power Automate {#connect-forms-server-with-power-automate}

Execute as seguintes ações para conectar sua instância as a Cloud Service do Forms com o Microsoft® Power Automate:

1. Criar um aplicativo do Microsoft® Azure Ative Diretory
1. Crie a configuração da nuvem Microsoft® Power Automate Dataverse.
1. Criar configuração na nuvem do serviço de fluxo do Microsoft® Power Automated
1. Publique a configuração da nuvem do Microsoft® Power Automate Dataverse.

### Criar o aplicativo Microsoft® Azure Ative Diretory {#ms-power-automate-application}

1. Faça logon em [Portal do Azure](https://portal.azure.com/).
1. Selecionar [!UICONTROL Ative Diretory do Azure] no painel de navegação esquerdo.
1. Na página Default diretory , selecione [!UICONTROL Registros do aplicativo] no painel esquerdo.
1. Na página Registros do aplicativo , clique em Novos registros.
1. Especifique Nome, Tipos de conta compatíveis e URI de redirecionamento na página. No URI de redirecionamento, especifique o seguinte e clique em Salvar.
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Registrar um Aplicativo do Azure Ative Diretory](assets/power-automate-application.png)

   >[!NOTE]
   >Você também pode especificar URIs de redirecionamento adicionais, se necessário, na página Autenticação .
   > Para tipos de conta compatíveis, selecione um único locatário, vários locatários ou Conta pessoal do Microsoft, dependendo do seu caso de uso


1. Na página Autenticação , ative as seguintes opções e clique em Salvar.


   * Tokens de acesso (usados para fluxos implícitos)
   * Tokens de ID (usados para fluxos implícitos e híbridos)

1. Na página Permissões da API , clique em Adicionar uma permissão.
1. Em APIs Microsoft®, selecione Serviço de fluxo e selecione as seguintes permissões.
   * Flows.Manage.All
   * Flows.Read.All

   Clique em Adicionar permissões para salvar as permissões.
1. Na página Permissões da API , clique em Adicionar uma permissão. Selecionar APIs que minha organização usa e pesquisar `DataVerse`.
1. Ative user_impersonation e clique em Adicionar permissões.
1. (Opcional) Na página Certificados e segredos, clique em Novo segredo do cliente. Na tela Adicionar um segredo do cliente , forneça uma descrição e um período de tempo para o segredo expirar e clique em Adicionar. Uma cadeia de caracteres secreta é gerada.
1. Mantenha uma nota específica de sua organização [URL do ambiente dinâmico](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### Criar configuração de nuvem do Microsoft® Power Automated Dataverse {#microsoft-power-automate-dataverse-cloud-configuration}

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de configuração]**.
1. No **[!UICONTROL Navegador de configuração]** página, toque em **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um **[!UICONTROL Título]** para a configuração, habilite **[!UICONTROL Configurações da nuvem]** e toque em **[!UICONTROL Criar]**. Ele cria um contêiner de configuração para armazenar Cloud Services. Certifique-se de que o nome da pasta não contenha espaço.
1. Navegar para **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data averse do Microsoft® Power Automated]** e abra o contêiner de configuração criado na etapa anterior.

   >[!NOTE]
   >
   >Ao criar um Formulário adaptável, especifique o nome do contêiner na **[!UICONTROL Contêiner de configuração]** campo.
1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar [!DNL Microsoft® Power Automate Flow Service] na AEM Forms.
1. No **[!UICONTROL Configurar o serviço de dados para o Microsoft® Power Automated]** Especifique a **[!UICONTROL ID do cliente]** (também designado por ID do pedido), **[!UICONTROL Segredo do cliente]**, **[!UICONTROL URL de OAuth]** e **[!UICONTROL URL do ambiente dinâmico]**. Use a ID do cliente, o Segredo do cliente, o URL OAuth e o URL do ambiente dinâmico de [Aplicativo Microsoft® Azure Ative Diretory](#ms-power-automate-application) você criou na seção anterior. Use a opção Endpoints na interface do usuário do aplicativo do Microsoft® Azure Ative Diretory para localizar o URL OAuth

![Use a opção Endpoints na interface do usuário do aplicativo Microsoft Power Automate para encontrar o URL OAuth](assets/endpoints.png)
Use a opção Endpoints na interface do usuário do aplicativo Microsoft® Power Automate para encontrar o URL OAuth

1. Toque **[!UICONTROL Connect]** . Se solicitado, faça logon em sua conta do Microsoft® Azure. Toque **[!UICONTROL Salvar]**.

### Criar a configuração da nuvem do Serviço de Fluxo do Microsoft® Power Automate.

1. Navegar para **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Serviço de Fluxo Microsoft® Power Automated]** e abra o contêiner de configuração criado na seção anterior.

   >[!NOTE]
   >
   >Ao criar um Formulário adaptável, especifique o nome do contêiner na **[!UICONTROL Contêiner de configuração]** campo.
1. Na página de configuração, toque em **[!UICONTROL Criar]** para criar [!DNL Microsoft® Power Automate Flow Service] na AEM Forms.
1. No **[!UICONTROL Configurar dataverse para o Microsoft® Power Automate]** Especifique a **[!UICONTROL ID do cliente]** (também designado por ID do pedido), **[!UICONTROL Segredo do cliente]**, **[!UICONTROL URL de OAuth]** e **[!UICONTROL URL do ambiente dinâmico]**. Use a ID do cliente, o Segredo do cliente, o URL OAuth e a ID do ambiente do Dynamics. Use a opção Endpoints na interface do usuário do aplicativo do Microsoft® Azure Ative Diretory para localizar o URL OAuth. Abra o [Meus fluxos](https://us.flow.microsoft.com) e toque em Meus fluxos , use a ID listada no URL como ID do ambiente dinâmico.
1. Toque **[!UICONTROL Connect]**. Se solicitado, faça logon em sua conta do Microsoft® Azure. Toque **[!UICONTROL Salvar]**.

### Publicar as configurações da nuvem do Microsoft® Power Automate Dataverse e do Microsoft® Power Automate Flow Service {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. Navegar para **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Data averse do Microsoft® Power Automated]** e abra o contêiner de configuração criado no anterior [Criar configuração de nuvem do Microsoft® Power Automated Dataverse](#microsoft-power-automate-dataverse-cloud-configuration) seção.
1. Selecione o `dataverse` configuração e toque em **[!UICONTROL Publicar]**.
1. Na página Publicar , selecione **[!UICONTROL Todas as configurações]** e tocar **[!UICONTROL Publicar]**. Publique as configurações da nuvem do Power Automate Dataverse e do Power Automate Flow Service.

Sua instância as a Cloud Service do Forms agora está conectada ao Microsoft® Power Automate. Agora é possível enviar dados do Adaptive Forms para um fluxo do Power Automate.

## Use a ação Chamar um fluxo do Microsoft® Power Automate para enviar dados para um fluxo do Power Automate {#use-the-invoke-microsoft-power-automate-flow-submit-action}

Depois de [Conecte sua instância as a Cloud Service do Forms com o Microsoft® Power Automate](#connect-forms-server-with-power-automate), execute a ação a seguir para configurar seu formulário adaptável para enviar dados capturados para um fluxo do Microsoft® no envio do formulário.

1. Faça logon na instância do autor, selecione o Formulário adaptável e clique em **[!UICONTROL Propriedades]**.
1. No Contêiner de configuração, procure e selecione o contêiner criado na seção [Criar configuração de nuvem do Microsoft® Power Automated Dataverse](#microsoft-power-automate-dataverse-cloud-configuration)e toque em **[!UICONTROL Salvar e fechar]**.
1. Abra o formulário adaptável para edição e navegue até **[!UICONTROL Submissão]** das propriedades do Contêiner de formulário adaptável.
1. No contêiner de propriedades, para **[!UICONTROL Enviar ações]** selecione o **[!UICONTROL Chamar um fluxo do Power Automate]** opção. Uma lista de fluxos disponíveis do Power Automate fica disponível **[!UICONTROL Fluxo do Power Automated]** opção. Selecione o fluxo necessário e os dados do Adaptive Forms são enviados para ele no envio.

![Configurar ação de envio](assets/submission.png)

>[!NOTE]
>
> Antes de enviar o formulário adaptável, verifique se `When an HTTP Request is received` O acionador com esquema JSON abaixo é adicionado ao seu fluxo do Power Automate.

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

