---
title: Integração do Adobe Workfront Fusion com o envio do AEM Forms
description: O Adobe Workfront Fusion permite que você se concentre em novas tarefas, em vez de tarefas repetitivas. Você pode conectar o Adobe Workfront Fusion a um Formulário adaptável usando o Envio de formulário.
keywords: Enviar um formulário adaptável para o Adobe Workfront Fusion, Integração do Adobe Workfront Fusion com o AEM Forms Submission, Adobe Workfront Fusion com o AEM Forms, Workfront Fusion com o AEM Forms, Conectar o Workfront Fusion ao AEM Forms, AEM Forms e Workfront Fusion, Como conectar o Workfront Fusion com o AEM Forms?, Conectar o Workfront Fusion a um formulário
topic-tags: author, developer
feature: Adaptive Forms
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: 559b4afa975dcd2204cd06c95f19ed38da00033e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 2%

---

# Enviar um formulário adaptável ao Adobe Workfront Fusion

<span class="preview"> O recurso está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-ea@adobe.com da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

O [Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) automatiza o processo de repetição das mesmas tarefas, como fluxos de trabalho de aprovação de documentos, filtragem e classificação de email, permitindo que você se concentre em novas tarefas em vez de tarefas recorrentes. O Adobe Workfront Fusion inclui vários cenários. Um cenário consiste em uma série de módulos que executam a transferência de dados entre aplicativos e serviços da Web. Em um cenário, você adiciona várias etapas (módulos) para automatizar uma tarefa.

Por exemplo, usando o Workfront Fusion, você pode criar um cenário para coletar dados com o Formulário adaptável, processar os dados e enviá-los a um armazenamento de dados para arquivamento. Depois que um cenário é configurado, o Workfront Fusion executa automaticamente as tarefas sempre que um usuário preenche um formulário, atualizando o armazenamento de dados perfeitamente.

O AEM Forms as a Cloud Service fornece um conector OOTB para conectar e enviar um Formulário adaptável ao Adobe Workfront Fusion. O envio de um formulário para o Adobe Workfront Fusion pode oferecer várias vantagens:
* Ela permitia a transferência contínua de dados de envios de formulários para fluxos de trabalho do Workfront Fusion.
* Ele ajuda a automatizar várias tarefas acionadas por envios de formulários. Isso pode incluir iniciar projetos, atribuir tarefas a membros específicos da equipe, enviar notificações e atualizar status do projeto — tudo sem intervenção manual.
* Todos os envios de formulários capturados no Workfront Fusion fornecem uma única fonte da verdade sobre as informações relacionadas ao projeto


<!--  AEM as a Cloud Service offers various out of the box submit actions for handling form submissions. You can learn more about these options in the [Adaptive Form Submit Action](/help/forms/configure-submit-actions-core-components.md)  article.-->

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

## Pré-requisitos para integrar o AEM Forms com o Adobe Workfront Fusion {#prerequisites}

Para estabelecer uma conexão entre o Workfront Fusion e o AEM Forms, é necessário o seguinte:

* Uma [licença válida do Workfront e do Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html).
* Um usuário AEM com direito de acessar o [Dev Console](https://my.cloudmanager.adobe.com/) para [recuperar as credenciais de serviço](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).

## Integrar o AEM Forms com o Adobe Workfront Fusion

### 1. Criar um cenário do Workfront {#workflow-scenario}

Para criar um cenário do Workfront, execute as seguintes etapas:

1. [Criar um cenário](#create-scenario)
1. [Adicionar um gancho da Web a um cenário](#add-webhook)
1. [Adicionar uma conexão a um gancho da Web](#add-connection)

#### Criar um cenário {#create-scenario}

Para criar um cenário:
1. Entre na sua [conta do Workfront Fusion](https://app-qa.workfrontfusion.com/).
1. Clique em **[!UICONTROL Cenários]** ![Ícone Compartilhar](/help/forms/assets/Smock_ShareAndroid_18_N.svg) no painel esquerdo.
1. Clique em **[!UICONTROL Criar um novo cenário]** no canto superior direito da página. Uma página para criar um novo cenário é exibida na tela.
1. Selecione **[!UICONTROL Novo cenário]** no canto superior esquerdo da página e digite um nome adequado para o cenário.
1. Clique no ponto de interrogação e certifique-se de adicionar o primeiro módulo como **[!UICONTROL AEM Forms]**.

   ![Adicionar um módulo AEM Forms](/help/forms/assets/workfront-aemforms.png)

   A caixa de diálogo **[!UICONTROL Observar Eventos de Formulário]** é exibida.

   >[!NOTE]
   >
   > É obrigatório adicionar o primeiro módulo como **[!UICONTROL AEM Forms]**.

1. Selecione a caixa de diálogo **[!UICONTROL Observar Eventos de Formulário]** e uma janela para adicionar um webhook será exibida.

#### Adicionar um webhook {#add-webhook}

![Adicionar um webhook](/help/forms/assets/workfront-add-webhook.png)

Para adicionar um webhook:

1. Clique em **[!UICONTROL Adicionar]** e uma caixa de diálogo **[!UICONTROL Adicionar um webhook]** será exibida.
1. Especifique um nome de webhook.

   >[!NOTE]
   >
   > É recomendável escolher cuidadosamente o nome do webhook, pois o nome do webhook especificado aparece na instância do AEM.

1. Clique em **[!UICONTROL Adicionar]** para adicionar uma nova conexão. A caixa de diálogo **[!UICONTROL Criar uma Conexão]** é exibida.

#### Adicionar uma conexão a um webhook {#add-connection}

![Adicionar uma conexão](/help/forms/assets/workfront-add-connection.png)

Para adicionar uma conexão:

1. Especifique um **[!UICONTROL Nome da Conexão]** na caixa de diálogo **[!UICONTROL Criar uma Conexão]**.

1. Selecione **Ambiente** e **Tipo** na lista suspensa.

1. Insira a **URL da Instância**.

   >[!NOTE]
   >
   > O URL da instância é o endereço exclusivo da Web que aponta para uma instância específica do AEM Forms.

   Você pode recuperar as [credenciais de serviço do Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html) necessárias para criar uma conexão.

1. Substitua `ims-na1.adobelogin.com` no **ponto de extremidade IMS** pelo valor de **imsEndpoint** das credenciais de serviço no Console do desenvolvedor.

   >[!NOTE]
   >
   > Mantenha o `https://` na caixa de texto **Ponto de extremidade IMS** ao adicionar a URL `imsEndpoint`.

1. Especifique os seguintes valores na caixa de diálogo **[!UICONTROL Criar uma Conexão]**:
   * Especifique a **ID do Cliente** com o valor de **clientId** a partir das credenciais de serviço no console do Desenvolvedor.
   * Especifique **Segredo do Cliente** com o valor de **clientSecret** das credenciais de serviço no console do Desenvolvedor.
   * Especifique a **ID da Conta Técnica** com o valor de **id** das credenciais de serviço no Console do Desenvolvedor.
   * Especifique a **Org ID** com o valor de **org** das credenciais de serviço no console do Desenvolvedor.
   * **Metascopos** com o valor de **metascopes** das credenciais de serviço no Console do desenvolvedor.
   * **Private Keys** com o valor de **privateKey** das credenciais de serviço no console do Desenvolvedor.

   >[!NOTE]
   >
   >* Para **Chave privada**, remova `\r\n` de seu valor.
   >  Por exemplo, se o valor da chave privada for:
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`, depois de remover `\r\n` da chave privada, a chave terá esta aparência, com ambos os valores aparecendo em uma linha separada:
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* Você também tem a opção de recuperar uma chave privada ou um certificado do arquivo selecionando o botão **Extrair**.

1. Clique em **Continuar**.

   A conexão criada começa a aparecer na lista suspensa da **[!UICONTROL Conexão]** na caixa de diálogo **[!UICONTROL Adicionar um webhook]**.

1. Selecione a conexão criada **[!UICONTROL Connection]** na lista suspensa.
1. Clique em **[!UICONTROL Salvar]**.
1. Clique em **[!UICONTROL OK]** e salve as alterações do cenário.
1. Para ativar o cenário, clique no botão de alternância LIGAR/DESLIGAR no editor de cenários.

>[!NOTE]
>
> Caso você não ative o cenário do Workfront, ele não detectará o envio do formulário e a configuração da ação de envio para o Workfront resultará em um envio com falha.

### 2. Configurar a ação de envio de um Formulário adaptável do Workfront Fusion

É possível configurar a ação de envio do Workfront Fusion para:
* [Novo Forms adaptável](#new-af-submit-action)
* [Formulários adaptáveis existentes](#existing-af-submit-action)

#### Configurar a ação de envio do novo Formulário adaptável para o Workfront Fusion {#new-af-submit-action}

Para configurar a ação de envio do novo Formulário adaptável para o Workfront Fusion:

1. Faça logon na instância do AEM.
1. Vá para **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]** > **[!UICONTROL Criar]** > **[!UICONTROL Formulário adaptável]**. O assistente **[!UICONTROL Criar Formulário]** é exibido.
1. Selecione um modelo de formulário adaptável na guia **[!UICONTROL Source]**.
1. Selecione um tema na guia **[!UICONTROL Estilo]**.

   ![Enviar ação para o Workfront Fusion](/help/forms/assets/workfront-scenario-new-af.png)

1. Selecione o **[!UICONTROL Invocar um Cenário do Workfront Fusion]** na guia **[!UICONTROL Envio]**.
1. Selecione o webhook criado na guia **[!UICONTROL Opções]** da janela **[!UICONTROL Propriedades]**.

   >[!NOTE]
   >
   > O nome do webhook do cenário do Workfront aparece na lista suspensa **Opções**.

1. Clique em **[!UICONTROL Criar]**.
1. Especifique o nome do novo Formulário adaptável e clique em **[!UICONTROL Criar]**.

#### Configurar a ação de envio do Formulário adaptável existente para o Workfront Fusion {#existing-af-submit-action}

Para configurar a ação de envio do Formulário adaptável existente para o Workfront Fusion:

1. Faça logon na instância do AEM.
1. Ir para **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione um formulário adaptável e abra-o no modo de edição.
1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.

   ![Enviar ação para o Workfront Fusion](/help/forms/assets/workfront-scenario-existing-af.png)

1. Abra a guia **[!UICONTROL Envio]**.
1. Selecione a **[!UICONTROL Ação de envio]** como **[!UICONTROL Chamar um Cenário do Workfront Fusion]**
1. Selecione **[!UICONTROL Cenário do Workfront Fusion]** na lista suspensa.
1. Clique em **[!UICONTROL Concluído]**.

## Práticas recomendadas {#best-practices}

* É recomendável escolher o nome do webhook com cuidado, pois não há como obter o nome do cenário na instância do AEM. No caso, você alterar o nome do webhook no futuro, ele não será refletido na lista suspensa de ação de envio do AEM Forms.
* Um cenário pode ter vários links de webhook, mas, por vez, apenas um link de webhook está ativo. É recomendável excluir o webhook desvinculado, para que ele não apareça na lista suspensa de ação de envio do AEM Forms.

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## Artigos relacionados

{{af-submit-action}}