---
title: Preparar sua planilha para aceitar dados
description: Crie formulários poderosos mais rápido usando planilhas e campos de bloco de formulário adaptável!
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d0c4f2f880ef7c11b11144502d30430336ac682e
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---


# Preparar sua planilha para aceitar dados

![Ecossistema de criação baseado em documentos](/help/edge/assets/document-based-authoring-workflow-enable-sheet-to-accept-data.png)

Depois de ter [criou e visualizou o formulário](/help/edge/docs/forms/create-forms.md), é hora de permitir que a planilha correspondente comece a receber dados.


<!-- 
>[!VIDEO](https://video.tv.adobe.com/v/3427489?quality=12&learn=on)

-->

Para ativar a planilha:

1. Abra a planilha que tem seu formulário e anexe uma nova planilha, renomeando-a para `incoming`.

   >[!WARNING]
   >
   > Se a variável `incoming` não estiver presente, o AEM não enviará dados para a planilha.

1. Espelhe os nomes de campos de formulário, os valores de `Name` na`shared-default` para os cabeçalhos no campo `incoming` planilha.

   Cada valor no `Name` coluna da `shared-default` planilha, com exceção do botão enviar, serve como cabeçalho na `incoming` planilha. Por exemplo, considere a seguinte imagem que ilustra cabeçalhos para um formulário &quot;contact-us&quot;:

   ![Campos de um formulário de contato conosco](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

1. Use o sidekick para visualizar a planilha.

   >[!NOTE]
   >
   >Mesmo que você tenha visualizado a planilha antes, é necessário visualizá-la novamente depois de criar a `incoming` pela primeira vez.


Depois que os nomes dos campos forem adicionados à `incoming` formulário fica pronto para aceitar envios. Você pode visualizar o formulário e enviar dados para a planilha usando-o.


Você também observa as seguintes alterações na planilha:

Uma planilha chamada &quot;Slack&quot; é adicionada à sua Pasta de trabalho do Excel ou Planilha do Google. Nesta planilha, você pode configurar notificações automáticas para um canal de Slack designado sempre que novos dados forem assimilados em sua planilha. Atualmente, o AEM suporta notificações exclusivamente para a organização AEM Engineering Slack e a organização Adobe Enterprise Support.

1. Para configurar notificações de Slack, digite a &quot;teamId&quot; do espaço de trabalho do Slack e o &quot;channel name&quot; ou &quot;ID&quot;. Você também pode pedir ao slack-bot (com o comando debug) o &quot;teamId&quot; e a &quot;channel ID&quot;. É preferível usar a &quot;ID do canal&quot; em vez do &quot;nome do canal&quot;, pois ela sobrevive à renomeação de canais.

   >[!NOTE]
   >
   > Formulários mais antigos não tinham a coluna &quot;teamId&quot;. A &quot;teamId&quot; foi incluída na coluna do canal, separada por um &quot;#&quot; ou &quot;/&quot;.

1. Insira qualquer título que desejar e em campos insira os nomes dos campos que deseja ver na notificação Slack. Cada cabeçalho deve ser separado por vírgula (por exemplo, nome, email).

   >[!WARNING]
   >
   >  Nunca as planilhas de &quot;padrão compartilhado&quot; devem conter informações pessoalmente identificáveis ou dados confidenciais que você não se sinta confortável em acessar publicamente.


## (Opcional) Use APIs de administrador para permitir que uma planilha aceite dados

Você também pode enviar uma solicitação POST para o formulário para permitir que ele aceite dados e configure cabeçalhos para o `incoming` planilha. Ao receber o pedido de POST, o serviço analisa o corpo do pedido e gera de forma autônoma os cabeçalhos e folhas essenciais necessários para a assimilação de dados.

Para usar APIs de administrador para permitir que uma planilha aceite dados:


1. Abra a pasta de trabalho criada e altere o nome da planilha padrão para `incoming`.

   >[!WARNING]
   >
   > Se a variável `incoming` a planilha não existe, o AEM não enviará dados para esta pasta de trabalho.

1. Visualize a planilha no sidekick.

   >[!NOTE]
   >
   >Mesmo que você tenha visualizado a planilha antes, é necessário visualizá-la novamente depois de criar a `incoming` pela primeira vez.

1. Envie a solicitação de POST para gerar os cabeçalhos apropriados no `incoming` e adicione a `shared-default` planilhas à sua planilha, se ela ainda não existir.

   Para entender como formatar a solicitação POST para configurar sua planilha, consulte o [Documentação da API de administração](https://www.aem.live/docs/admin.html#tag/authentication/operation/profile). Você pode observar o exemplo fornecido abaixo:

   **Solicitação**

   ```JSON
   POST 'https://admin.hlx.page/form/{owner}/{repo}/{branch}/contact-us.json' \
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
   curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
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

Uma planilha chamada &quot;Slack&quot; é adicionada à sua Pasta de trabalho do Excel ou Planilha do Google. Nesta planilha, você pode configurar notificações automáticas para um canal de Slack designado sempre que novos dados forem assimilados em sua planilha. Atualmente, o AEM suporta notificações exclusivamente para a organização AEM Engineering Slack e a organização Adobe Enterprise Support.

1. Para configurar notificações de Slack, digite a &quot;teamId&quot; do espaço de trabalho do Slack e o &quot;channel name&quot; ou &quot;ID&quot;. Você também pode pedir ao slack-bot (com o comando debug) o &quot;teamId&quot; e a &quot;channel ID&quot;. É preferível usar a &quot;ID do canal&quot; em vez do &quot;nome do canal&quot;, pois ela sobrevive à renomeação de canais.

   >[!NOTE]
   >
   > Formulários mais antigos não tinham a coluna &quot;teamId&quot;. A &quot;teamId&quot; foi incluída na coluna do canal, separada por um &quot;#&quot; ou &quot;/&quot;.

1. Insira qualquer título que desejar e em campos insira os nomes dos campos que deseja ver na notificação Slack. Cada cabeçalho deve ser separado por vírgula (por exemplo, nome, email).


A planilha agora está configurada para receber dados, você pode [visualizar o formulário usando o Bloco de formulário adaptável](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) ou [usar solicitações POST](#use-admin-apis-to-send-data-to-your-sheet) para começar a enviar dados para a planilha.

>[!WARNING]
>
>  Nunca as planilhas de &quot;padrão compartilhado&quot; devem conter informações pessoalmente identificáveis ou dados confidenciais que você não se sinta confortável em acessar publicamente.

## Enviar dados para sua planilha {#send-data-to-your-sheet}

Depois que a planilha for definida para receber dados, você poderá [visualizar o formulário usando o Bloco de formulário adaptável](/help/edge/docs/forms/create-forms.md#preview-the-form-using-your-edge-delivery-service-eds-page) ou [usar APIs de administrador](#use-admin-apis-to-send-data-to-your-sheet) para começar a enviar dados para a planilha.

### Use APIs de administrador para enviar dados para sua planilha

Você pode enviar solicitações de POST diretamente para o seu formulário usando hlx.page, hlx.live ou o seu domínio de produção para enviar dados.


```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> O URL não deve ter a extensão .json. Você deve publicar a planilha para que as operações de POST funcionem em `.live` ou no domínio de produção.

#### Formatação dos dados do formulário

Há algumas maneiras diferentes de formatar os dados de formulário no corpo do POST. Você pode usar:

* matriz de `name:value` pares:

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

  Por exemplo

  ```JSON
  curl -s -i -X POST 'https://main--portal--wkndforms.hlx.page/contact-us' \
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



* um objeto com `key:value` pares:

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

  Por exemplo,

  ```JSON
  curl -s -i -X POST 'https://admin.hlx.page/form/wkndforms/portal/main/contact-us.json' \
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

* Codificação de URL (`x-www-form-urlencoded`) corpo (com `content-type` cabeçalho definido como `application/x-www-form-urlencoded`)

  ```Shell
  'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&Message=I   +have+some+questions+about+your+products.&Phone=123-456-7890&Company=Adobe+Inc.&   Country=United+States&PreferredContactMethod=Email&SubscribeToNewsletter=true'
  ```

  Por exemplo,

  ```Shell
  curl -s -i -X POST \
    -d 'Email=kent%40wknd.com&Name=clark&Subject=Regarding+Product+Inquiry&   Message=I+have+some+questions+about+your+products.&Phone=123-456-7890& Company=Adobe+Inc.&Country=United+States&PreferredContactMethod=Email&   SubscribeToNewsletter=true' \
    https://main--portal--wkndforms.hlx.live/contact-us
  ```

Em seguida, você pode personalizar a mensagem de agradecimento, [configurar uma página de agradecimento](/help/edge/docs/forms/thank-you-page-form.md)ou [definir redirecionamentos](/help/edge/docs/forms/thank-you-page-form.md).

## Veja mais

* [Criar e visualizar um formulário](/help/edge/docs/forms/create-forms.md)
* [Ativar formulário para enviar dados](/help/edge/docs/forms/submit-forms.md)
* [Publicar um formulário na página de sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Adicionar validações a campos de formulário](/help/edge/docs/forms/validate-forms.md)
* [Alterar temas e estilo de formulário](/help/edge/docs/forms/style-theme-forms.md)
