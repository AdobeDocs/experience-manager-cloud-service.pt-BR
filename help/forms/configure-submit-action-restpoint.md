---
Title: How to configure submit to Rest Endpoint submit action for an Adaptive Form?
Description: Discover the steps to set up Rest Endpoint when submitting an Adaptive Form.
keywords: Endpoint REST do AEM Forms, Enviar para endpoint REST, Dados do Post para URL REST, Configurar ação de endpoint REST
feature: Adaptive Forms, Core Components
exl-id: 58c63ba6-aec5-4961-a70a-265990ab9cc8
title: "Como configurar uma ação enviar para um formulário adaptável?"
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Configurar um formulário adaptável para a ação de envio do ponto de extremidade REST

Use a ação **[!UICONTROL Enviar para o Ponto de Extremidade REST]** para postar os dados enviados em uma URL REST. A URL pode ser de um servidor interno (o servidor no qual o formulário é renderizado) ou externo.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md).

## Vantagens

Algumas das vantagens de configurar a ação de envio **[!UICONTROL Enviar para o endpoint REST]** para o Adaptive Forms são:

* Ele permite a integração perfeita de dados de formulário com sistemas e serviços externos por meio de APIs RESTful.
* Ele oferece flexibilidade para lidar com envios de dados do Adaptive Forms, oferecendo suporte a estruturas de dados dinâmicas e complexas.
* Ele oferece suporte ao mapeamento dinâmico de campos de formulário para parâmetros no URL do endpoint REST, permitindo envios de dados adaptáveis e personalizáveis.


## Configurar ação de envio Enviar para Ponto de Extremidade REST {#steps-to-configure-submit-to-restendpoint-submit-action}

Para configurar a ação de envio:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique na guia **[!UICONTROL Envio]**.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[!UICONTROL Enviar para o ponto de extremidade Rest]**.
   ![Configuração de ação de Enviar para o ponto de extremidade Rest](/help/forms/assets/submit-action-restendpoint.png)

   Para publicar dados em um servidor interno, forneça o caminho do recurso. Os dados são publicados no caminho do recurso. Por exemplo, `/content/restEndPoint`. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.

   Para publicar dados em um servidor externo, forneça um URL. O formato da URL é `https://host:port/path_to_rest_end_point`. Configure o caminho para lidar com a solicitação POST de forma anônima.

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

   Você também pode **[!UICONTROL Habilitar a solicitação POST]** e fornecer uma URL para publicar a solicitação. Para enviar dados ao servidor AEM que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor AEM. Por exemplo, `/content/forms/af/SampleForm.html`. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

1. Clique em **[!UICONTROL Concluído]**.

## Práticas recomendadas

* Ao postar dados em um servidor externo, verifique se o URL é seguro e configure o caminho para lidar com a solicitação POST anonimamente para proteger informações confidenciais.
* Para passar os campos como parâmetros em um URL REST, todos os campos devem ter nomes de elemento diferentes, mesmo se os campos forem colocados em painéis diferentes.

## Artigos relacionados

{{af-submit-action}}
