---
title: Criar um formulário usando a criação com base em documentos para o Serviço de entrega de borda do AEM Forms
description: Formas perfeitas de artesanato, rápido!  o AEM Forms Edge Delivery + criação baseada em documentos = velocidade incrível e formulários compatíveis com SEO para usuários e mecanismos de pesquisa mais satisfeitos.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# Criar um formulário usando a criação com base em documentos para o Serviço de entrega de borda do AEM Forms

Na era digital de hoje, criar formulários amigáveis é essencial para qualquer organização. A criação com base em documento do AEM Forms Edge Delivery permite criar formulários usando ferramentas familiares, como o Word ou o Google Docs.Esses formulários enviam dados diretamente para um arquivo do Microsoft Excel ou do Google Sheets, permitindo que você use um ecossistema vibrante e APIs robustas do Google Sheets, do Microsoft Excel e do Microsoft Sharepoint para processar facilmente os dados enviados ou iniciar um fluxo de trabalho empresarial existente.

Este guia aborda:

* Preparação da planilha: saiba como configurar um arquivo do Excel ou Google Sheets para coleta de dados e adicionar campos de formulário a ele.
* Enviar dados para sua planilha: saiba como enviar dados para sua planilha usando solicitações POST.
* Publicar o formulário: integre o formulário à página do AEM Sites ou publique-o como uma página independente.

Seja você um novato ou um profissional, este guia permite que você crie formas belas e funcionais que os usuários adoram. Vamos desbloquear a criação de formulários eficiente - mergulhe agora!

## Antes de começar

`WIP`

## Prepare sua planilha para receber dados

1. Crie uma Pasta de Trabalho do Microsoft Excel ou uma Planilha do Google em qualquer lugar no diretório do projeto de Entrega da borda do AEM no Microsoft OneDrive ou no Google Drive. Este documento usa uma Planilha do Google chamada `contact-us.xlsx`, localizado na raiz de um projeto Adobe Experience Manager (AEM).

1. Verifique se o usuário do AEM (por exemplo helix@adobe.com) configurado para seu projeto tem permissões de edição para a planilha.

1. Abra a pasta de trabalho criada e altere o nome da planilha padrão para &quot;entrada&quot;.

   >[!NOTE]
   >
   > Se a planilha &quot;de entrada&quot; não existir, o AEM não enviará dados para essa pasta de trabalho.

1. Visualize a planilha no sidekick.

   >[!NOTE]
   >
   >Mesmo que você tenha visualizado a planilha antes, é necessário visualizá-la novamente depois de criar a planilha &quot;de entrada&quot; pela primeira vez.

1. Prepare a planilha adicionando cabeçalhos que correspondam aos dados inseridos. O exemplo a seguir exibe campos para um formulário &quot;contact-us&quot;:

   ![Campos de um formulário de contato conosco](/help/edge/assets/contact-us-form-excel-sheet-fields.png)

   Você pode fazer isso manualmente ou usando uma solicitação POST para a rota do formulário no serviço de Admin AEM. O serviço de administração examinará os dados no corpo da POST e gerará os cabeçalhos, tabelas e planilhas apropriados necessários para assimilar dados com eficiência e aproveitar ao máximo o serviço de formulários.

   Para entender como formatar a solicitação POST para configurar sua planilha, consulte o [Documentação da API de administração](https://www.hlx.live/docs/admin.html#tag/form). Além disso, consulte o exemplo fornecido abaixo:

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
   
   {"rowCount":2,"columns":["Email","Name","Subject","Message","Phone","Company","Country","PreferredContactMethod","SubscribeToNewsletter"]}%
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

A solicitação POST acima fornece dados de amostra, incluindo campos de formulário e seus respectivos valores de amostra. Esses dados são usados pelo serviço de Administração para configurar o formulário.

Embora o serviço de Administração tenha recomendado a configuração da sua planilha, se preferir criar os cabeçalhos manualmente, consulte o documento intitulado [Configuração Manual do Forms Sheet](https://www.hlx.live/docs/manual-forms-sheet-setup).

Ao enviar a solicitação do POST para o serviço de administração, você observará as seguintes alterações em sua pasta de trabalho:

* Uma nova planilha chamada &quot;padrão compartilhado&quot; é adicionada à Pasta de trabalho do Excel ou à Planilha do Google. Os dados presentes na planilha &quot;padrão compartilhado&quot; são recuperados ao fazer uma solicitação GET para a planilha. Esta planilha serve como um local ideal para usar fórmulas de planilha para resumir os dados recebidos, tornando-os propícios ao consumo em outros contextos.

  Em nenhuma circunstância a folha &quot;padrão compartilhado&quot; deve conter informações de identificação pessoal ou dados confidenciais que você não esteja familiarizado com o acesso público.

* Uma planilha chamada &quot;Slack&quot; é adicionada à sua pasta de trabalho do Excel ou planilha do Google. Nesta planilha, você pode configurar notificações automáticas para um canal de Slack designado sempre que novos dados forem assimilados em sua planilha. Atualmente, o AEM suporta notificações exclusivamente para a organização AEM Engineering Slack e a organização Adobe Enterprise Support.

   1. Para configurar notificações de Slack, digite a &quot;teamId&quot; do espaço de trabalho do Slack e o &quot;channel name&quot; ou &quot;ID&quot;. Você também pode pedir ao slack-bot (com o comando debug) o &quot;teamId&quot; e a &quot;channel ID&quot;. É preferível usar a &quot;ID do canal&quot; em vez do &quot;nome do canal&quot;, pois ela sobrevive à renomeação de canais.

      >[!NOTE]
      >
      > Formulários mais antigos não tinham a coluna &quot;teamId&quot;. A &quot;teamId&quot; foi incluída na coluna do canal, separada por um &quot;#&quot; ou &quot;/&quot;.

   1. Insira qualquer título que desejar e em campos insira os nomes dos campos que deseja ver na notificação Slack. Cada cabeçalho deve ser separado por vírgula (por exemplo, nome, email).

Agora a planilha está configurada para receber dados e você pode enviar solicitações de POST diretamente para ela usando hlx.page, hlx.live ou seu domínio de produção.


## Enviar dados para sua planilha {#send-data-to-your-sheet}

Depois que a planilha é definida para receber dados, você pode enviar solicitações de POST diretamente para ela usando hlx.page, hlx.live ou seu domínio de produção para enviar dados.

```JSON
POST https://branch–repo–owner.hlx.(page|live)/email-form
POST https://my-domain.com/email-form
```

>[!NOTE]
>
> O URL não deve ter a extensão .json. Você deve publicar a planilha para que as operações de POST funcionem em .live ou no domínio de produção.

### Formatação de dados para o EDS Forms

Há algumas maneiras diferentes de formatar os dados de formulário no corpo do POST.

* Matriz de pares nome-valor:

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
              { "name": "message", "value": "I have some questions about your products." },
              { "name": "phone", "value": "123-456-7890" },
              { "name": "company", "value": "Example Inc." },
              { "name": "country", "value": "United States" },
              { "name": "preferred_contact_method", "value": "Email" },
              { "name": "newsletter_subscribe", "value": true }
              ]
          }'
  
* Objeto com pares chave:valor

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

* `x-www-form-urlencoded` corpo (`content-type` o cabeçalho deve ser definido como `application/x-www-form-urlencoded`) &#39;firstname=bruce&amp;lastname=banner&amp;email=bruce%40example.com&#39;



