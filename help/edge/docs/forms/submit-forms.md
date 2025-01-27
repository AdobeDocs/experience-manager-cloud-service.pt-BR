---
title: Preparar sua planilha para aceitar dados
description: Crie formulários poderosos mais rápido usando planilhas e campos de bloco adaptáveis do Forms!
feature: Edge Delivery Services
exl-id: 0643aee5-3a7f-449f-b086-ed637ae53b5a
role: Admin, Architect, Developer
source-git-commit: 552779d9d1cee2ae9f233cabc2405eb6416c41bc
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Configurar seus arquivos do Google Sheets ou do Microsoft Excel para começar a aceitar dados


Depois que você tiver [criado e visualizado o formulário](/help/edge/docs/forms/create-forms.md), será hora de habilitar a planilha correspondente para começar a receber dados. Você pode

* [Habilitar manualmente a planilha para aceitar os dados](#manually-enable-the-spreadsheet-to-accept-data)
* [Usar APIs de administrador para permitir que uma planilha aceite dados](#use-admin-apis-to-enable-a-spreadsheet-to-accept-data)

![Ecossistema de criação baseado em documentos](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)


<!--

>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

## Habilitar manualmente a planilha para aceitar dados

Para permitir que a planilha aceite dados

1. Abra a planilha que tem seu formulário e anexe uma nova planilha, renomeando-a para `incoming`. Por exemplo, a [consulta](/help/edge/assets/enquiry.xlsx) da pasta de trabalho do Microsoft Excel.

   >[!WARNING]
   >
   > Se a planilha `incoming` não estiver presente, o AEM não enviará dados para a planilha.

1. Nesta planilha, insira uma tabela chamada &quot;input_form&quot;. Selecione o número de colunas necessárias para corresponder aos nomes dos campos de formulário. Em seguida, na barra de ferramentas, vá para Insert > Table e clique em OK.

1. Altere o nome da tabela para &quot;input_form&quot;. No Microsoft Excel, para alterar o nome da tabela, selecione a tabela e clique em Design da tabela.

1. Em seguida, adicione os nomes dos campos de formulário como cabeçalhos da tabela. Para garantir que os campos sejam exatamente os mesmos, é possível copiá-los e colá-los na planilha &quot;shared-aem&quot;.  Na planilha &quot;shared-aem&quot;, selecione e copie as IDs de formulário listadas na coluna &quot;Name&quot;, exceto para o campo submit.

1. Na planilha de &quot;entrada&quot;, selecione Colar especial > Transpor linhas para colunas para copiar as IDs de campo como cabeçalhos de coluna nesta nova planilha. Keep only os campos cujos dados precisam capturar outros podem ser ignorados.

   Cada valor na coluna `Name` da folha `shared-aem`, excluindo o botão enviar, pode servir como um cabeçalho na folha `incoming`. Por exemplo, considere a seguinte imagem que ilustra cabeçalhos para um formulário de &quot;consulta&quot;:

   ![Campos de um formulário contact-us](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. Use a extensão [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar as atualizações de formulário. Sua planilha está pronta para aceitar os envios de formulários recebidos.

   >[!NOTE]
   >
   >Mesmo que você tenha visualizado a planilha antes, você deve visualizá-la novamente depois de criar a planilha `incoming` pela primeira vez.


Depois que os nomes de campos forem adicionados à planilha `incoming`, o formulário estará pronto para aceitar envios. Você pode visualizar o formulário e enviar dados para a planilha usando-o.

Depois que a planilha estiver configurada para receber dados, você poderá [visualizar o formulário](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) <!--or [use POST requests](#use-admin-apis-to-send-data-to-your-sheet)--> para começar a enviar dados para a planilha.

>[!WARNING]
>
>  Nunca as folhas do &quot;aem compartilhado&quot; devem conter informações pessoalmente identificáveis ou dados confidenciais que você não se sinta confortável em acessar publicamente.


## Usar APIs de administrador para permitir que uma planilha aceite dados

Você também pode enviar uma solicitação POST para o formulário para permitir que ele aceite dados e configure cabeçalhos para a folha `incoming`. Ao receber o pedido de POST, o serviço analisa o corpo do pedido e gera de forma autônoma os cabeçalhos e folhas essenciais necessários para a assimilação de dados.

Para usar APIs de administrador para permitir que uma planilha aceite dados:


1. Abra a pasta de trabalho criada e altere o nome da planilha padrão para `incoming`.

   >[!WARNING]
   >
   > Se a planilha `incoming` não existir, o AEM não enviará dados para esta pasta de trabalho.

1. Visualize a planilha no sidekick.

   >[!NOTE]
   >
   >Mesmo que você tenha visualizado a planilha antes, você deve visualizá-la novamente depois de criar a planilha `incoming` pela primeira vez.

1. Envie a solicitação POST para gerar os cabeçalhos apropriados na planilha `incoming` e adicione as planilhas `shared-default` à planilha, se ela ainda não existir.

   Para entender como formatar a solicitação POST para configurar sua planilha, consulte a [Documentação da API de Administração](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). Você pode observar o exemplo fornecido abaixo:

   **Solicitação**

   ```JSON
   POST 'https://admin.aem.page/form/{owner}/{repo}/{branch}/contact-us.json' \
   --header 'Content-Type: application/json' \
   --data '{
       "data": {
           "Email": "john@wknd.com",
           "Name": "John",
           "Subject": "Regarding Product Inquiry",
           "Message": "I have some questions about your products.",
           "Phone": "123-456-7890",
           "Company": "Adobe Inc.",
           "Country": "United States",
           "PreferredContactMethod": "Email",
           "SubscribeToNewsletter": true
       }
   }'
   ```


   **Resposta**

   ```JSON
   HTTP/2 200 
   content-type: application/json
   x-invocation-id: 1b3bd30a-8cfb-4f85-a662-4b1f7cf367c5
   cache-control: no-store, private, must-revalidate
   accept-ranges: bytes
   date: Sat, 10 Feb 2024 09:26:48 GMT
   via: 1.1 varnish
   x-served-by: cache-del21736-DEL
   x-cache: MISS
   x-cache-hits: 0
   x-timer: S1707557205.094883,VS0,VE3799
   strict-transport-security: max-age=31557600
   content-length: 138
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country",      "PreferredContactMethod","SubscribeToNewsletter"]}%
   ```

   Você pode usar ferramentas como curl ou Postman para executar essa solicitação de POST, conforme demonstrado abaixo:

   ```JSON
   curl -s -i -X POST 'https://admin.aem.page/form/wkndform/wefinance/main/contact-us.json' \
       --header 'Content-Type: application/json' \
       --data '{
           "data": {
               "Email": "john@wknd.com",
               "Name": "John",
               "Subject": "Regarding Product Inquiry",
               "Message": "I have some questions about your products.",
               "Phone": "123-456-7890",
               "Company": "Wknd Inc.",
               "Country": "United States",
               "PreferredContactMethod": "Email",
               "SubscribeToNewsletter": true
       }
   }'
   ```

   A solicitação POST mencionada acima fornece dados de amostra, incluindo campos de formulário e seus respectivos valores de amostra. Esses dados são usados pelo serviço de Administração para configurar o formulário.

   O formulário agora está habilitado para aceitar dados. Você também observa as seguintes alterações na planilha:

## Alterações automáticas na planilha quando ela estiver ativada para aceitar dados.

Depois que a planilha é definida para receber dados, você observa as seguintes alterações em sua planilha:

Uma planilha chamada &quot;Slack&quot; é adicionada à sua Pasta de trabalho do Excel ou Planilha do Google. Nesta planilha, você pode configurar notificações automáticas para um canal de Slack designado sempre que novos dados forem assimilados em sua planilha. Atualmente, o AEM suporta notificações exclusivamente para a organização AEM Engineering Slack e a organização Adobe Enterprise Support.

1. Para configurar notificações de Slack, digite a &quot;teamId&quot; do espaço de trabalho do Slack e o &quot;channel name&quot; ou &quot;ID&quot;. Você também pode pedir ao slack-bot (com o comando debug) o &quot;teamId&quot; e a &quot;channel ID&quot;. É preferível usar a &quot;ID do canal&quot; em vez do &quot;nome do canal&quot;, pois ela sobrevive à renomeação de canais.

   >[!NOTE]
   >
   > Formulários mais antigos não tinham a coluna &quot;teamId&quot;. A &quot;teamId&quot; foi incluída na coluna do canal, separada por um &quot;#&quot; ou &quot;/&quot;.

1. Insira qualquer título que desejar e em campos insira os nomes dos campos que deseja ver na notificação Slack. Cada cabeçalho deve ser separado por vírgula (por exemplo, nome, email).

   >[!WARNING]
   >
   >  Nunca as planilhas de &quot;padrão compartilhado&quot; devem conter informações pessoalmente identificáveis ou dados confidenciais que você não se sinta confortável em acessar publicamente.



<!--
## Send data to your sheet {#send-data-to-your-sheet}

After the sheet is set to receive data, you can [preview the form using Adaptive Forms Block](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) or [use Admin APIs](#use-admin-apis-to-send-data-to-your-sheet) to start sending data to the sheet.

### Use Admin APIs to send data to your sheet

You can send POST requests directly to your form using aem.page, aem.live, or your production domain, to send data. 


```JSON

POST https://branch–repo–owner.aem.(page|live)/email-form
POST https://my-domain.com/email-form

```

>[!NOTE] 
>
> The URL should not have the .json extension. You must publish the sheet for POST operations to function on `.live` or on the production domain.

#### Formatting the form data

There are a few different ways that you can format the form data in the POST body. You can use: 

* array of `name:value` pairs: 
    
    ```JSON
    
    {
      "data": [
        { "name": "name", "value": "Clark Kent" },
        { "name": "email", "value": "superman@example.com" },
        { "name": "subject", "value": "Regarding Product Inquiry" },
        { "name": "message", "value": "I have some questions about your products." },
        { "name": "phone", "value": "123-456-7890" },
        { "name": "company", "value": "Example Inc." },
        { "name": "country", "value": "United States" },
        { "name": "preferred_contact_method", "value": "Email" },
        { "name": "newsletter_subscribe", "value": true }
      ]
    }

    ```

    For example

    ```JSON

    curl -s -i -X POST 'https://main--wefinance--wkndform.aem.page/contact-us' \
        --header 'Content-Type: application/json' \
        --data '{
        "data": [
            { "name": "name", "value": "Clark Kent" },
            { "name": "email", "value": "superman@example.com" },
            { "name": "subject", "value": "Regarding Product Inquiry" },
            { "name": "message", "value": "I have some questions about your        products." },
            { "name": "phone", "value": "123-456-7890" },
            { "name": "company", "value": "Example Inc." },
            { "name": "country", "value": "United States" },
            { "name": "preferred_contact_method", "value": "Email" },
            { "name": "newsletter_subscribe", "value": true }
        ]
    }'

    ```



* an object with `key:value` pairs:

    ```JSON

        {
          "data": {
            "name": "Jessica Jones",
            "email": "jj@example.com",
            "subject": "Regarding Product Inquiry",
            "message": "I have some questions about your products.",
            "phone": "123-456-7890",
            "company": "Example Inc.",
            "country": "United States",
            "preferred_contact_method": "Email",
            "newsletter_subscribe": true
          }
        }

    ```

    For example,

    ```JSON

    curl -s -i -X POST 'https://admin.aem.page/form/wkndform/wefinance/main/contact-us.json' \
    --header 'Content-Type: application/json' \
    --data '{
        "data": {
            "Email": "khushwant@wknd.com",
            "Name": "khushwant",
            "Subject": "Regarding Product Inquiry",
            "Message": "I have some questions about your products.",
            "Phone": "123-456-7890",
            "Company": "Adobe Inc.",
            "Country": "United States",
            "PreferredContactMethod": "Email",
            "SubscribeToNewsletter": true
        }
    }'

    ```

* URL encoded (`x-www-form-urlencoded`) body (with `content-type` header set to `application/x-www-form-urlencoded`)

    ```Shell

    'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'

    ```

    For example, if your project's repository is named "wefinance", it's located under the account owner "wkndform", and you're using the "main" branch.,

    ```Shell

    curl -s -i -X POST \
      -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
      https://main--wefinance--wkndform.aem.live/contact-us

    ```
-->

Em seguida, você pode [personalizar a mensagem de agradecimento](/help/edge/docs/forms/thank-you-page-form.md).

## Consulte também:

{{see-more-forms-eds}}
