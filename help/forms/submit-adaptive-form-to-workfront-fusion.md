---
title: Integração do Adobe Workfront Fusion com o envio do AEM Forms
description: O Adobe Workfront Fusion permite que você se concentre em novas tarefas, em vez de tarefas repetitivas. Você pode conectar o Adobe Workfront Fusion a um Formulário adaptável usando o Envio de formulário.
keywords: Enviar um formulário adaptável para o Adobe Workfront Fusion, Integração do Adobe Workfront Fusion com o AEM Forms Submission, Adobe Workfront Fusion com o AEM Forms, Workfront Fusion com o AEM Forms, Conectar o Workfront Fusion ao AEM Forms, AEM Forms e Workfront Fusion, Como conectar o Workfront Fusion com o AEM Forms?, Conectar o Workfront Fusion a um formulário
topic-tags: author, developer
feature: Adaptive Forms
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: 975f767e75a268a1638227ae20a533f82724c80a
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Enviar um formulário adaptável ao Adobe Workfront Fusion

<span class="preview"> O recurso está disponível no programa Early Adoter. Você pode escrever para aem-forms-early-adopter-program@adobe.com a partir de sua ID de e-mail oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso. </span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) O automatiza o processo de repetição das mesmas tarefas, como workflows de aprovação de documentos, filtragem e classificação de email, permitindo que você se concentre em novas tarefas, em vez de tarefas recorrentes. O Adobe Workfront Fusion inclui vários cenários. Um cenário consiste em uma série de módulos que executam a transferência de dados entre aplicativos e serviços da Web. Em um cenário, você adiciona várias etapas (módulos) para automatizar uma tarefa.

Por exemplo, usando o Workfront Fusion, você pode criar um cenário para coletar dados com o Formulário adaptável, processar os dados e enviá-los a um armazenamento de dados para arquivamento. Depois que um cenário é configurado, o Workfront Fusion executa automaticamente as tarefas sempre que um usuário preenche um formulário, atualizando o armazenamento de dados perfeitamente.

## Vantagens de usar o Adobe Workfront Fusion{#advatages-of-workfront-fusion}

Algumas das vantagens de usar o Adobe Workfront Fusion com o AEM Forms:

- Envio de dados capturados com o Adaptive Forms para um cenário do Workfront Fusion
- Automatização de tarefas menos propensas a erros.
- Personalização de requisitos específicos para uma organização que não estão diretamente incluídos no Workfront.
- Lógica simples de manipulação e decisões diretas, por exemplo, instruções if/then.

## Pré-requisitos para integrar o AEM Forms com o Adobe Workfront Fusion {#prerequisites}

Os pré-requisitos necessários para conectar o Workfront Fusion ao AEM Forms são:

- Um válido [Licença do Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html).
- Um usuário do AEM com direito de acesso [Console de Desenvolvimento](https://my.cloudmanager.adobe.com/) para [recuperar as credenciais de serviço](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).

## Integrar o AEM Forms com o Adobe Workfront Fusion

Para conectar [Workfront fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) para criar um formulário, execute as seguintes etapas:

### 1. Criar um cenário do Workfront {#workflow-scenario}

Para criar um cenário do Workfront:
1. Entre no seu [Conta do Workfront Fusion](https://app-qa.workfrontfusion.com/).
1. Clique em **[!UICONTROL Cenários]** ![Ícone Compartilhar](/help/forms/assets/Smock_ShareAndroid_18_N.svg) no painel esquerdo.
1. Clique em **[!UICONTROL Criar um novo cenário]** no canto superior direito da página. Uma página para criar um novo cenário é exibida na tela.
1. Selecionar **[!UICONTROL Novo cenário]** no canto superior esquerdo da página e digite um nome adequado para o cenário.
1. Clique no ponto de interrogação e certifique-se de adicionar o primeiro módulo como **[!UICONTROL AEM Forms]**.

   ![Adicionar um módulo AEM Forms](/help/forms/assets/workfront-aemforms.png)

   A variável **[!UICONTROL Aguardar eventos de formulário]** é exibida.

   >[!NOTE]
   >
   > É obrigatório adicionar o primeiro módulo como **[!UICONTROL AEM Forms]**.

1. Selecione o **[!UICONTROL Aguardar eventos de formulário]** e uma janela para adicionar um webhook será exibida.

#### 1.1 Adicionar um webhook {#add-webhook}

![Adicionar um webhook](/help/forms/assets/workfront-add-webhook.png)

Para adicionar um webhook:

1. Clique em **[!UICONTROL Adicionar]** e uma **[!UICONTROL Adicionar um webhook]** é exibida.
1. Especifique um nome de webhook.

   >[!NOTE]
   >
   > É recomendável escolher cuidadosamente o nome do webhook, pois o nome do webhook especificado aparece na instância do AEM.

1. Clique em **[!UICONTROL Adicionar]** para adicionar uma nova conexão. A variável **[!UICONTROL Criar uma conexão]** é exibida.

#### 1.2 Adicionar uma conexão a um webhook {#add-connection}

![Adicionar uma conexão](/help/forms/assets/workfront-add-connection.png)

Para adicionar uma conexão:

1. Especificar um **[!UICONTROL Nome da conexão]** no **[!UICONTROL Criar uma conexão]** caixa de diálogo.

1. Selecionar **Ambiente** e **Tipo** na lista suspensa.

1. Insira o **URL da instância**.

   >[!NOTE]
   >
   > O URL da instância é o endereço exclusivo da Web que aponta para uma instância específica do AEM Forms.

   Você pode recuperar a variável [credenciais de serviço do Console do desenvolvedor](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html) necessário para criar uma conexão.

1. Substituir `ims-na1.adobelogin.com` no **Endpoint IMS** com o valor de **imsEndpoint** das credenciais de serviço no Console do desenvolvedor.

   >[!NOTE]
   >
   > Manter o `https://` no **Endpoint IMS** caixa de texto ao adicionar o `imsEndpoint` URL.

1. Especifique os seguintes valores na variável **[!UICONTROL Criar uma conexão]** caixa de diálogo:
   - Especificar **ID do cliente** com valor de **clientId** das credenciais de serviço no Console do desenvolvedor.
   - Especificar **Segredo do cliente** com valor de **clientSecret** das credenciais de serviço no Console do desenvolvedor.
   - Especificar **ID da conta técnica**  com valor de **id** das credenciais de serviço no Console do desenvolvedor.
   - Especificar **ID da organização**  com valor de **org** das credenciais de serviço no Console do desenvolvedor.
   - **Metaescopos**  com valor de **metascópios** das credenciais de serviço no Console do desenvolvedor.
   - **Chaves privadas**  com valor de **privateKey** das credenciais de serviço no Console do desenvolvedor.

   >[!NOTE]
   >
   >- Para **Chave privada**, remover `\r\n` do seu valor.
   >  Por exemplo, se o valor da chave privada for:
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`, depois de remover o `\r\n` na chave privada, a chave seria semelhante ao seguinte, com ambos os valores aparecendo em uma linha separada:
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >- Você também tem a opção de recuperar uma chave privada ou certificado do arquivo selecionando o **Extract** botão.

1. Clique em **Continuar**.

   A conexão criada começa a aparecer na lista suspensa do **[!UICONTROL Conexão]** no **[!UICONTROL Adicionar um webhook]** caixa de diálogo.

1. Selecione a conexão criada **[!UICONTROL Conexão]** na lista suspensa.
1. Clique em **[!UICONTROL Salvar]**.
1. Clique em **[!UICONTROL OK]** e salve as alterações do cenário.

#### 1.3 Ativar o cenário do Workfront {#activate-scenario}

Para ativar o cenário:

1. Clique em **[!UICONTROL Cenários]** ![Ícone Compartilhar](/help/forms/assets/Smock_ShareAndroid_18_N.svg) no painel esquerdo.
1. Clique em **[!UICONTROL Cenário inativo]** guia.
1. Clique em **LIGADO/DESLIGADO** botão de alternância para o seu cenário do AEM Forms.

Depois de clicar no botão de alternância, o cenário do Workfront começa a aparecer no **[!UICONTROL Cenário ativo]** guia.

>[!NOTE]
>
> Caso você não ative o cenário do Workfront, ele não detectará o envio do formulário e a configuração da ação de envio para o Workfront resultará em um envio com falha.

### 2. Configurar a ação de envio de um Formulário adaptável do Workfront Fusion

É possível configurar a ação de envio do Workfront Fusion para:
- [Novo Forms adaptável](#new-af-submit-action)
- [Formulários adaptáveis existentes](#existing-af-submit-action)

#### Configurar a ação de envio do novo Formulário adaptável para o Workfront Fusion {#new-af-submit-action}

Para configurar a ação de envio do novo Formulário adaptável para o Workfront Fusion:

1. Faça logon na instância do AEM.
1. Ir para **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]** > **[!UICONTROL Criar]** > **[!UICONTROL Formulário adaptável]**. A variável **[!UICONTROL Criar formulário]** é exibido.
1. Selecione um modelo de formulário adaptável na **[!UICONTROL Origem]** guia.
1. Selecione um tema no **[!UICONTROL Estilo]** guia.

   ![Enviar ação para o Workfront Fusion](/help/forms/assets/workfront-scenario-new-af.png)

1. Selecione o **[!UICONTROL Chamar um cenário do Workfront Fusion]** do **[!UICONTROL Envio]** guia.
1. Selecione o webhook criado na **[!UICONTROL Opções]** na guia **[!UICONTROL Propriedades]** janela.

   >[!NOTE]
   >
   > O nome do webhook do cenário do Workfront aparece no campo **Opções** lista suspensa.

1. Clique em **[!UICONTROL Criar]**.
1. Especifique o nome do novo Formulário adaptável e clique em **[!UICONTROL Criar]**.

#### Configurar a ação de envio do Formulário adaptável existente para o Workfront Fusion {#existing-af-submit-action}

Para configurar a ação de envio do Formulário adaptável existente para o Workfront Fusion:

1. Faça logon na instância do AEM.
1. Ir para **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Selecione um formulário adaptável e abra-o no modo de edição.
1. Abra o Navegador de conteúdo e selecione a variável **[!UICONTROL Contêiner do guia]** componente do seu Formulário adaptável.
1. Clique nas propriedades do Container do guia ![Propriedades do guia](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável é aberta.

   ![Enviar ação para o Workfront Fusion](/help/forms/assets/workfront-scenario-existing-af.png)

1. Abra o **[!UICONTROL Envio]** guia.
1. Selecione o **[!UICONTROL Enviar ação]** as **[!UICONTROL Chamar um cenário do Workfront Fusion]**
1. Selecionar **[!UICONTROL Cenário do Workfront Fusion]** na lista suspensa.
1. Clique em **[!UICONTROL Concluído]**.

## Práticas recomendadas {#best-practices}

- É recomendável escolher o nome do webhook com cuidado, pois não há como obter o nome do cenário na instância do AEM. No caso, você alterar o nome do webhook no futuro, ele não será refletido na lista suspensa de ação de envio do AEM Forms.
- Um cenário pode ter vários links de webhook, mas, por vez, apenas um link de webhook está ativo. É recomendável excluir o webhook desvinculado, para que ele não apareça na lista suspensa de ação de envio do AEM Forms.

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->
