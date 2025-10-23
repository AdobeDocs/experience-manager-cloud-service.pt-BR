---
title: Como integrar um formulário adaptável com o Microsoft&reg; Power Automate?
description: Integrar um formulário adaptável com o Microsoft&reg; Power Automate.
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
keywords: conecte formulários do AEM para automatizar o poder, automatizar o poder AEM Forms, integrar automatizar o poder ao Adaptive Forms, enviar dados do Adaptive Forms para o Power Automate
feature: Adaptive Forms, Foundation Components, Core Components, Edge Delivery Services
role: Admin, User, Developer
source-git-commit: 03f92d950744e653e4ef509bac3c3b4709477e41
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 5%

---


# Conecte um formulário adaptável com o Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/forms-microsoft-power-automate-integration) |
| AEM as a Cloud Service | Este artigo |

<span class="preview"> Se você estiver no GovCloud e precisar se conectar a um locatário do GCC (Government Cloud Computing), envie um email em seu endereço oficial para aem-forms-ea@adobe.com para solicitar acesso por meio do Early Adoter Program. </span>

Você pode configurar um Formulário adaptável para executar um fluxo da nuvem do Microsoft® Power Automate no envio. O formulário adaptável configurado envia dados capturados, anexos e documentos de registro para processamento no fluxo da nuvem do Power Automate. Ele ajuda você a criar uma experiência personalizada de captura de dados, aproveitando o poder do Microsoft® Power Automate para criar lógicas de negócios sobre dados capturados e automatizar os fluxos de trabalho do cliente.

O editor Forms adaptável fornece a **ação de envio Chamar um fluxo do Microsoft® Power Automate** para enviar dados de formulários adaptáveis, anexos e Documentos de Registro para o fluxo da nuvem do Power Automate.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/aem-forms-submit-action.md).


## Vantagens

Estes são alguns exemplos do que você pode fazer após integrar um formulário adaptável ao Microsoft® Power Automate:

* Usar dados adaptáveis do Forms em processos de negócios do Power Automate
* Use o Power Automate para enviar dados capturados para mais de 500 fontes de dados ou qualquer API disponível publicamente
* Realizar cálculos complexos em dados capturados
* Salve os dados do Forms adaptável em sistemas de armazenamento em uma programação predefinida

## Pré-requisitos

Os seguintes itens são necessários para conectar um Formulário adaptável com o Microsoft® Power Automate:

* Licença do Microsoft® Power Automate Premium.
* Fluxo do Microsoft® [Power Automate](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) com o acionador `When an HTTP request is received` para aceitar os dados de envio do Formulário adaptável.
* Um usuário do Experience Manager com privilégios de [Forms Author](/help/forms/forms-groups-privileges-tasks.md) e [Forms Admin](/help/forms/forms-groups-privileges-tasks.md)
* A conta usada para conectar ao Microsoft® Power Automate é proprietária do fluxo do Power Automate configurado para receber dados do Formulário adaptável

## Conecte sua instância do Forms as a Cloud Service com o Microsoft® Power Automate {#connect-forms-server-with-power-automate}

Execute as seguintes ações para conectar sua instância do Forms as a Cloud Service com o Microsoft® Power Automate:

1. [Criar uma Microsoft](#ms-power-automate-application)
1. [Criar Microsoft](#microsoft-power-automate-dataverse-cloud-configuration)
1. [Criar Microsoft](#create-microsoft-power-automate-flow-cloud-configuration)
1. [Publicar Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### Criar Aplicativo do Ative Diretory do Microsoft® Azure {#ms-power-automate-application}

1. Faça logon no [Portal do Azure](https://portal.azure.com/).
1. Selecione [!UICONTROL Azure Ative Diretory] na navegação à esquerda.
1. Na página Diretório padrão, selecione [!UICONTROL Registros de aplicativo] no painel esquerdo.
1. Na página Registros do aplicativo, clique em Novos registros.
1. Especifique Nome, Tipos de conta suportados e URI de redirecionamento na página. No URI de redirecionamento, especifique o seguinte e clique em Salvar.
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Registrar um Aplicativo do Azure Ative Diretory](assets/power-automate-application.png)

   >[!NOTE]
   >Você também pode especificar URIs de redirecionamento adicionais, se necessário, na página Autenticação.
   > Para os tipos de conta suportados, selecione um único locatário, vários locatários ou Conta pessoal da Microsoft®, dependendo do seu caso de uso


1. Na página Autenticação, ative as seguintes opções e clique em Salvar.


   * Tokens de acesso (usados para fluxos implícitos)
   * Tokens de ID (usados para fluxos implícitos e híbridos)

1. Na página de permissões da API, clique em `Add a permission`.

1. Em APIs Microsoft®, selecione o `Power Automate` e selecione as seguintes permissões.
   * Flows.Manage.All
   * Flows.Read.All
   * Permissão GCC (opcional se quiser se conectar a um locatário GCC (Government Cloud Computing))
Clique em `Add permissions` para salvar as permissões.
1. Na página de permissões da API, clique em `Add a permission`. Selecione as APIs que minha organização usa e pesquise `DataVerse` e habilite `user_impersonation` Clique em `Add` permissões.
1. (Opcional) Na página Certificados e segredos, clique em Novo segredo de cliente. Na tela Adicionar um segredo do cliente, forneça uma descrição e um período para o segredo expirar e clique em Adicionar. Uma sequência secreta é gerada.
1. Anote a [URL de ambiente do Dynamics](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests) específica da sua organização.

### Criar configuração de nuvem do Microsoft® Power Automate Dataverse {#microsoft-power-automate-dataverse-cloud-configuration}

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Geral]** > **[!UICONTROL Navegador de Configuração]**.
1. Na página **[!UICONTROL Navegador de Configuração]**, selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo **[!UICONTROL Criar Configuração]**, especifique um **[!UICONTROL Título]** para a configuração, habilite as **[!UICONTROL Configurações de Nuvem]** e selecione **[!UICONTROL Criar]**. Ele cria um contêiner de configuração para armazenar os Serviços em nuvem. Verifique se o nome da pasta não contém nenhum espaço.
1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** e abra o contêiner de configuração criado na etapa anterior.


   >[!NOTE]
   >
   >Ao criar um Formulário adaptável, especifique o nome do contêiner no campo **[!UICONTROL Contêiner de configuração]**.

1. Na página de configuração, selecione **[!UICONTROL Criar]** para criar a configuração [!DNL Microsoft® Power Automate Flow Service] no AEM Forms.
1. Na página **[!UICONTROL Configurar Serviço Dataverse para o Microsoft® Power Automate]**, Especifique a **[!UICONTROL ID do Cliente]** (também conhecida como ID do Aplicativo), o **[!UICONTROL Segredo do Cliente]**, a **[!UICONTROL URL do OAuth]** e a **[!UICONTROL URL do Ambiente Dinâmico]**. Use a ID do Cliente, o Segredo do Cliente, a URL do OAuth e a URL do Ambiente Dinâmico do [Aplicativo do Microsoft® Azure Ative Diretory](#ms-power-automate-application) criados na seção anterior. Use a opção Endpoints na interface do usuário do aplicativo do Microsoft® Azure Ative Diretory para encontrar o URL do OAuth

   ![Use a opção Endpoints na interface do usuário do aplicativo Microsoft Power Automate para localizar a URL do OAuth](assets/endpoints.png)

1. Selecione **[!UICONTROL Conectar]**. Se solicitado, faça logon em sua conta do Microsoft® Azure. Selecione **[!UICONTROL Salvar]**.

### Criar configuração de nuvem do serviço de fluxo do Microsoft® Power Automate {#create-microsoft-power-automate-flow-cloud-configuration}

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Flow Service]** e abra o contêiner de configuração criado na seção anterior.


   >[!NOTE]
   >
   >Ao criar um Formulário adaptável, especifique o nome do contêiner no campo **[!UICONTROL Contêiner de configuração]**.

1. Na página de configuração, selecione **[!UICONTROL Criar]** para criar a configuração [!DNL Microsoft® Power Automate Flow Service] no AEM Forms.

1. (Opcional) Marque a caixa de seleção `Connect to Microsoft GCC` para se conectar ao locatário GCC.

   >[!NOTE]
   >
   > Caso queira se conectar a um locatário do GCC (Government Cloud Computing), selecione a permissão do GCC no Portal do Microsoft Azure.


   ![Configuração da nuvem do Power Automate](/help/forms/assets/power-automate.png)

1. Na página **[!UICONTROL Configurar Dataverse para o Microsoft® Power Automate]**, especifique a **[!UICONTROL ID do Cliente]** (também conhecida como ID do Aplicativo), o **[!UICONTROL Segredo do Cliente]**, o **[!UICONTROL URL do OAuth]** e o **[!UICONTROL URL do Ambiente Dinâmico]**. Use a ID do cliente, o Segredo do cliente, o URL do OAuth e a ID de ambiente do Dynamics. Use a opção Endpoints na interface do usuário do aplicativo do Microsoft® Azure Ative Diretory para localizar o URL do OAuth. Abra o link [Meus fluxos](https://us.flow.microsoft.com) e selecione Meus Fluxos para usar a ID listada na URL como ID de Ambiente do Dynamics.

1. Selecione **[!UICONTROL Conectar]**. Se solicitado, faça logon em sua conta do Microsoft® Azure. Selecione **[!UICONTROL Salvar]**.

### Publicar as configurações de nuvem do Microsoft® Power Automate Dataverse e do Microsoft® Power Automate Flow Service {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** e abra o contêiner de configuração criado na seção [Criar configuração do Microsoft® Power Automate Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration) anterior.
1. Selecione a configuração `dataverse` e selecione **[!UICONTROL Publicar]**.
1. Na página Publicar, selecione **[!UICONTROL Todas as configurações]** e selecione **[!UICONTROL Publicar]**. Publique as configurações de nuvem do Power Automate Dataverse e do Power Automate Flow Service.

Sua instância do Forms as a Cloud Service agora está conectada com o Microsoft® Power Automate. Agora é possível enviar dados do Adaptive Forms para um fluxo do Power Automate.

## Use a ação Chamar um fluxo do Microsoft® Power Automate para enviar dados a um fluxo do Power Automate {#use-the-invoke-microsoft-power-automate-flow-submit-action}

Depois de [Conectar sua instância do Forms as a Cloud Service com o Microsoft® Power Automate](#connect-forms-server-with-power-automate), execute a seguinte ação para configurar seu formulário adaptável para enviar dados capturados para um fluxo do Microsoft® no envio do formulário.

>[!BEGINTABS]

>[!TAB Componente de base]

1. Faça logon na instância do Autor, selecione o Formulário adaptável e clique em **[!UICONTROL Propriedades]**.
1. No Contêiner de Configuração, navegue e selecione o contêiner criado na seção [Criar configuração do Microsoft® Power Automate Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration) e selecione **[!UICONTROL Salvar e fechar]**.
1. Abra o Formulário adaptável para edição e navegue até a seção **[!UICONTROL Envio]** das propriedades do Contêiner de formulário adaptável.
1. No contêiner de propriedades, em **[!UICONTROL Enviar Ações]**, selecione a opção **[!UICONTROL Invocar um fluxo do Power Automate]** e selecione um **[!UICONTROL fluxo do Power Automate]**. Selecione o fluxo necessário e os dados do Adaptive Forms serão enviados a ele no envio.

   ![Configurar Ação de Envio](assets/submission.png)
1. Clique em **[!UICONTROL Concluído]**.

>[!NOTE]
>
> Antes de enviar o Formulário adaptável, verifique se o acionador `When an HTTP Request is received` com o Esquema JSON abaixo foi adicionado ao seu fluxo do Power Automate.

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

>[!TAB Componente principal]

1. Faça logon na instância do Autor, selecione o Formulário adaptável e clique em **[!UICONTROL Propriedades]**.
1. No Contêiner de Configuração, navegue e selecione o contêiner criado na seção [Criar configuração do Microsoft® Power Automate Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration) e selecione **[!UICONTROL Salvar e fechar]**.
1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique na guia **[!UICONTROL Envio]**.
1. Selecione a opção **[!UICONTROL Invocar um fluxo do Power Automate]** na lista suspensa Enviar ação e selecione um **[!UICONTROL fluxo do Power Automate]**. Selecione o fluxo necessário e os dados do Adaptive Forms serão enviados a ele no envio.

   ![Configurar Ação de Envio](/help/forms/assets/power-automate-cc.png)
1. Clique em **[!UICONTROL Concluído]**.

>[!NOTE]
>
> Antes de enviar o Formulário adaptável, verifique se o acionador `When an HTTP Request is received` com o Esquema JSON abaixo foi adicionado ao seu fluxo do Power Automate.

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

>[!TAB Universal Editor]

1. Faça logon na instância do Autor e selecione o Formulário adaptável.
1. No Contêiner de Configuração, navegue e selecione o contêiner criado na seção [Criar configuração do Microsoft® Power Automate Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration) e selecione **[!UICONTROL Salvar e fechar]**.
1. Abra o Formulário adaptável para edição.
1. Clique na extensão **Editar propriedades do formulário** no editor.
A caixa de diálogo **Propriedades do Formulário** é exibida.

   >[!NOTE]
   >
   > * Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
   > * Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.


1. Clique na guia **Envio** e selecione **[!UICONTROL Chamar um fluxo do Power Automate]** para enviar ação. Selecione o fluxo necessário e os dados do Adaptive Forms serão enviados a ele no envio.

   ![Configurar Ação de Envio](/help/forms/assets/power-automate-ue.png)
1. Clique em **[!UICONTROL Salvar&amp;Fechar]**.

>[!NOTE]
>
> Antes de enviar o Formulário adaptável, verifique se o acionador `When an HTTP Request is received` com o Esquema JSON abaixo foi adicionado ao seu fluxo do Power Automate.

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

>[!ENDTABS]

<!--
## See also

* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
* [Configure a Submit Action](configure-submit-actions-core-components.md)
* [Adobe Experience Manager Connector for Microsoft&reg; Power Automate](https://learn.microsoft.com/en-us/connectors/adobeexperiencemanag/)
* [Connect Adaptive Form to Microsoft&reg; Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)
-->


## Artigos relacionados

{{af-submit-action}}

<!--

>[!MORELIKETHIS]
>
>* [Connect Adaptive Form to Microsoft Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)

-->