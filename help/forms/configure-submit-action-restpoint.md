---
title: Como configurar a ação de envio Enviar para Ponto de Extremidade Rest para um Formulário adaptável?
description: Descubra as etapas para configurar o Ponto de extremidade Rest ao enviar um Formulário adaptável.
keywords: Endpoint REST do AEM Forms, Enviar para endpoint REST, Postar dados no URL REST, Configurar ação de endpoint REST
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
exl-id: 58c63ba6-aec5-4961-a70a-265990ab9cc8
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 1%

---

# Configurar um formulário adaptável para a ação de envio do ponto de extremidade REST

<span class="preview"> A capacidade de especificar o Ponto de Extremidade REST usando a configuração é um Programa de Adoção Antecipada e se aplica somente aos Componentes Principais e ao Edge Delivery Services Forms. Você pode escrever para `aem-forms-ea@adobe.com` a partir de sua ID de email oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso. </span>

Use a ação **[!UICONTROL Enviar para o Ponto de Extremidade REST]** para postar os dados enviados em uma URL REST. A URL pode ser de um servidor interno (o servidor no qual o formulário é renderizado) ou externo.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/aem-forms-submit-action.md).

## Vantagens

Algumas das vantagens de configurar a ação de envio **[!UICONTROL Enviar para o endpoint REST]** para o Adaptive Forms são:

* Ele permite a integração perfeita de dados de formulário com sistemas e serviços externos por meio de APIs RESTful.
* Ele oferece flexibilidade para lidar com envios de dados do Adaptive Forms, oferecendo suporte a estruturas de dados dinâmicas e complexas.
* Ele oferece suporte ao mapeamento dinâmico de campos de formulário para parâmetros no URL do endpoint REST, permitindo envios de dados adaptáveis e personalizáveis.


## Configurar ação de envio Enviar para Ponto de Extremidade REST {#steps-to-configure-submit-to-restendpoint-submit-action}

>[!BEGINTABS]

>[!TAB Componente de base]

Para configurar uma ação de envio com base na especificação da API aberta do Swagger para o formulário adaptável com base nos componentes de base, são:

1. Abra o Formulário adaptável para edição e navegue até a seção **[!UICONTROL Envio]** das propriedades do Contêiner de formulário adaptável.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[!UICONTROL Enviar para o ponto de extremidade Rest]**.

   ![Configuração de ação de Enviar para o ponto de extremidade Rest](/help/forms/assets/submit-action-restendpoint.png)

   Para publicar dados em um servidor interno, forneça o caminho do recurso. Os dados são publicados no caminho do recurso. Por exemplo, `/content/restEndPoint`. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.
Essa opção permite inserir diretamente o endpoint REST de destino.
Para publicar dados em um servidor externo, forneça um URL. O formato da URL é `https://host:port/path_to_rest_end_point`. Certifique-se de configurar o caminho para lidar com a solicitação POST de forma anônima.
   ![Mapeamento para valores de campo passados como parâmetros da Página de Agradecimento](assets/post-enabled-actionconfig.png)

   No exemplo acima, as informações inseridas pelo usuário em `textbox` são capturadas usando o parâmetro `param1`. A sintaxe para publicar dados capturados usando `param1` é:

   `String data=request.getParameter("param1");`

   Da mesma forma, os parâmetros que você usa para lançar dados XML e anexos são `dataXml` e `attachments`.

   Por exemplo, você usa esses dois parâmetros no script para analisar dados para um ponto final rest. Você usa a seguinte sintaxe para armazenar e analisar os dados:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   Neste exemplo, `data` armazena os dados XML e `att` armazena os dados de anexo.
A Ação de Envio **[!UICONTROL Enviar para o ponto de extremidade REST]** envia os dados preenchidos no formulário para uma página de confirmação configurada como parte da solicitação HTTP GET. Você pode adicionar o nome do campo a ser solicitado. O formato da solicitação é:
   `{fieldName}={request parameter name}`

   Como mostrado na imagem abaixo, `param1` e `param2` são passados como parâmetros com valores copiados dos campos **caixa de texto** e **caixa numérica** para a próxima ação.

   ![Configurando Ação De Envio De Ponto De Extremidade Rest](assets/action-config.png)

   Você também pode **[!UICONTROL Habilitar a solicitação POST]** e fornecer uma URL para publicar a solicitação. Para enviar dados ao servidor do AEM que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor do AEM. Por exemplo, `/content/forms/af/SampleForm.html`. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

1. Clique em **[!UICONTROL Concluído]**.

>[!TAB Componente principal]

Para configurar ações de envio com base na especificação da API aberta do Swagger para o formulário adaptável com base nos Componentes principais, são:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique na guia **[!UICONTROL Envio]**.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[!UICONTROL Enviar para o ponto de extremidade Rest]**.

   ![Configurando Ponto De Extremidade Rest](assets/rest-service-endpoint-config.png)

   Para publicar dados em um servidor interno, forneça o caminho do recurso. Os dados são publicados no caminho do recurso. Por exemplo, `/content/restEndPoint`. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.

   Há duas opções para especificar o endpoint REST:

   +++URL

   Essa opção permite inserir diretamente o endpoint REST de destino.
Para publicar dados em um servidor externo, forneça um URL. O formato da URL é `https://host:port/path_to_rest_end_point`. Certifique-se de configurar o caminho para lidar com a solicitação POST de forma anônima.

   ![Mapeamento para valores de campo passados como parâmetros da Página de Agradecimento](assets/post-enabled-actionconfig.png)

   No exemplo acima, as informações inseridas pelo usuário em `textbox` são capturadas usando o parâmetro `param1`. A sintaxe para publicar dados capturados usando `param1` é:

   `String data=request.getParameter("param1");`

   Da mesma forma, os parâmetros que você usa para lançar dados XML e anexos são `dataXml` e `attachments`.

   Por exemplo, você usa esses dois parâmetros no script para analisar dados para um ponto final rest. Você usa a seguinte sintaxe para armazenar e analisar os dados:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   Neste exemplo, `data` armazena os dados XML e `att` armazena os dados de anexo.

   A Ação de Envio **[!UICONTROL Enviar para o ponto de extremidade REST]** envia os dados preenchidos no formulário para uma página de confirmação configurada como parte da solicitação HTTP GET. Você pode adicionar o nome do campo a ser solicitado. O formato da solicitação é:

   `{fieldName}={request parameter name}`

   Como mostrado na imagem abaixo, `param1` e `param2` são passados como parâmetros com valores copiados dos campos **caixa de texto** e **caixa numérica** para a próxima ação.

   ![Configurando Ação De Envio De Ponto De Extremidade Rest](assets/action-config.png)

   Você também pode **[!UICONTROL Habilitar a solicitação POST]** e fornecer uma URL para publicar a solicitação. Para enviar dados ao servidor do AEM que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor do AEM. Por exemplo, `/content/forms/af/SampleForm.html`. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

   +++

   +++Configuração

   Essa opção permite adicionar uma configuração HTTP predefinida gerenciada pelo Navegador de configuração do AEM. Você pode selecionar a Configuração criada para seu Tipo de autenticação de ponto de extremidade REST de serviço e os Tipos de conteúdo. Para saber mais sobre Tipo de Autenticação e Tipos de Conteúdo, visite [configurar fontes de dados](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint)

   +++

1. Clique em **[!UICONTROL Concluído]**.

>[!TAB Universal Editor]

Para configurar ações de envio com base na especificação da API aberta do Swagger para o formulário adaptável criado no Universal Editor são:

1. Abra o Formulário adaptável para edição.
1. Clique na extensão **Editar propriedades do formulário** no editor.

   A caixa de diálogo **Propriedades do Formulário** é exibida.

   >[!NOTE]
   >
   > * Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
   > * Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.

1. Clique na guia **Envio** e selecione a ação de envio **[!UICONTROL Enviar para o ponto de extremidade Rest]**.

   Para publicar dados em um servidor interno, forneça o caminho do recurso. Os dados são publicados no caminho do recurso. Por exemplo, `/content/restEndPoint`. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.

   Há duas opções para especificar o endpoint REST:

   +++URL

   Essa opção permite inserir diretamente o endpoint REST de destino.
Para publicar dados em um servidor externo, forneça um URL. O formato da URL é `https://host:port/path_to_rest_end_point`. Certifique-se de configurar o caminho para lidar com a solicitação POST de forma anônima.

   ![Mapeamento para valores de campo passados como parâmetros da Página de Agradecimento](assets/post-enabled-actionconfig.png)

   No exemplo acima, as informações inseridas pelo usuário em `textbox` são capturadas usando o parâmetro `param1`. A sintaxe para publicar dados capturados usando `param1` é:

   `String data=request.getParameter("param1");`

   Da mesma forma, os parâmetros que você usa para lançar dados XML e anexos são `dataXml` e `attachments`.

   Por exemplo, você usa esses dois parâmetros no script para analisar dados para um ponto final rest. Você usa a seguinte sintaxe para armazenar e analisar os dados:

   `String data=request.getParameter("dataXml");`
   `String att=request.getParameter("attachments");`

   Neste exemplo, `data` armazena os dados XML e `att` armazena os dados de anexo.

   A Ação de Envio **[!UICONTROL Enviar para o ponto de extremidade REST]** envia os dados preenchidos no formulário para uma página de confirmação configurada como parte da solicitação HTTP GET. Você pode adicionar o nome do campo a ser solicitado. O formato da solicitação é:

   `{fieldName}={request parameter name}`

   Como mostrado na imagem abaixo, `param1` e `param2` são passados como parâmetros com valores copiados dos campos **caixa de texto** e **caixa numérica** para a próxima ação.

   ![Configurando Ação De Envio De Ponto De Extremidade Rest](/help/forms/assets/submit-to-rest-endpoint-ue.png)

   Você também pode **[!UICONTROL Habilitar a solicitação POST]** e fornecer uma URL para publicar a solicitação. Para enviar dados ao servidor do AEM que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor do AEM. Por exemplo, `/content/forms/af/SampleForm.html`. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

   +++

   +++Configuração

   Essa opção permite adicionar uma configuração HTTP predefinida gerenciada pelo Navegador de configuração do AEM. Você pode selecionar a Configuração criada para seu Tipo de autenticação de ponto de extremidade REST de serviço e os Tipos de conteúdo. Para saber mais sobre Tipo de Autenticação e Tipos de Conteúdo, visite [configurar fontes de dados](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint)

   +++

1. Clique em **[!UICONTROL Salvar&amp;Fechar]**.

>[!ENDTABS]

<!-- ### Configure submit action based on Service Rest Endpoint {#config-service-endpoint-auth}



1. Open the Content browser, and select the **[!UICONTROL Guide Container]** component of your Adaptive Form.
2. Click the Guide Container properties ![Guide properties](/help/forms/assets/configure-icon.svg) icon. The Adaptive Form Container dialog box opens. 
3. Click the  **[!UICONTROL Submission]** tab. 
4. From the **[!UICONTROL Submit Action]** drop-down list, select **[!UICONTROL Submit to Rest endpoint]**.
5. Enable the POST request.
6. Specify the REST endpoint URL.
7. Select the Configuration you have created for your Service Rest Endpoint Authentication Type and the Content Types. To know more about Authentication Type and the Content Types, visit [configure data sources](/help/forms/configure-data-sources.md#configure-restful-services-using-service-endpoint-configure-restful-services-service-endpoint).
    ![Configuring Rest Endpoint](assets/rest-service-endpoint-config.png)
8. Click Done. -->



## Práticas recomendadas

* Ao postar dados em um servidor externo, verifique se o URL é seguro e configure o caminho para lidar com a solicitação POST anonimamente para proteger informações confidenciais.
* Para passar os campos como parâmetros em um URL REST, todos os campos devem ter nomes de elemento diferentes, mesmo se os campos forem colocados em painéis diferentes.

## Artigos relacionados

{{af-submit-action}}
