---
Title: How to use forms submission service for submitting forms?
Description: Learn how to use forms submission service for submitting forms.
Keywords: Use form submission service, Submit form using form submission service
feature: Edge Delivery Services
Role: User, Developer
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: 42db7e5d4896a4a488643cb54f0b77cf4db86f3e
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 0%

---

# Serviço de envio de Forms com o Edge Delivery Services Forms

O serviço de Envio do Forms permite armazenar dados dos envios de formulários em qualquer planilha, como OneDrive, SharePoint ou Google Sheets, permitindo que você acesse e gerencie facilmente os dados de formulários em sua plataforma de planilha preferida.

![Serviço de envio do Forms](/help/forms/assets/form-submission-service.png)

## Vantagens de usar o serviço de envio do Forms

Algumas vantagens de usar o Serviço de envio do Forms com planilhas são:

* **Integração direta**: você pode configurar formulários para enviar dados diretamente para uma planilha especificada, eliminando a necessidade de transferência manual de dados.
* **Estrutura de dados**: ao configurar o envio, você pode mapear campos de formulário para colunas de planilha correspondentes para armazenamento de dados organizado.
* **Controle de acesso**: você pode aproveitar as permissões existentes para controlar quem pode acessar e modificar os dados de formulário enviados, dependendo do serviço de planilha escolhido.

## Pré-requisitos

Abaixo estão os pré-requisitos para usar o serviço de Envio do Forms:

* Certifique-se de que o projeto AEM tenha o Bloco de formulário adaptável mais recente.
* Incluir na lista de permissões Verifique se o repositório foi adicionado ao arquivo para usar o serviço de envio do Forms. mailto:aem-forms-ea@adobe.com com o nome da organização do GitHub e o nome do repositório para adicioná-los ao arquivo de inclui na lista de permissões para usar o serviço de envio do Forms.

## Configurar o serviço de envio do Forms

Criar novo projeto AEM configurado com o Bloco Forms adaptável. Consulte o artigo [Introdução - Tutorial do desenvolvedor](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial) para saber como criar um novo projeto de AEM. Atualize o arquivo `fstab.yaml` em seu projeto. Substitua a referência existente pelo caminho para a pasta que você compartilhou com o `forms@adobe.com`.

Você pode [configurar o Serviço de Envio do Forms manualmente](#configuring-the-forms-submission-service-manually) ou [configurar o Serviço de Envio do Forms usando a API](#configuring-the-forms-submission-service-using-api).

### Configuração manual do serviço de envio do Forms

![Fluxo de trabalho do serviço de envio de formulários](/help/forms/assets/forms-submission-service-workflow.png)

#### 1. Criar um formulário usando uma definição de formulário

Crie um formulário usando o Google Sheets ou o Microsoft Excel. Para saber como criar um formulário usando uma definição de formulário no Microsoft Excel ou no Google Sheets, [clique aqui](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms).

A captura de tela abaixo exibe a definição de formulário usada para criar o formulário:

![Definição de Formulário](/help/forms/assets/form-submission-definition.png)

#### 2. Ative a planilha para aceitar os dados.

Depois de criar e visualizar o formulário, ative a planilha correspondente para começar a receber dados. adicione uma nova planilha como `incoming`. Você pode [habilitar manualmente a planilha para aceitar os dados](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/submit-forms#manually-enable-the-spreadsheet-to-accept-data).

![Planilha de entrada](/help/forms/assets/form-submission-incoming-sheet.png)

>[!WARNING]
>
> Se a planilha `incoming` não existir, o AEM não enviará dados para esta pasta de trabalho.

#### 3. Compartilhe a planilha e gere um link.

Para compartilhar a planilha com a conta `forms@adobe.com` e gerar um link, execute as seguintes etapas:

1. No Excel ou Google Sheets, clique no botão **Compartilhar** no canto superior direito.
1. Adicione a conta do `forms@adobe.com` e
clique no ícone de olho, selecione o acesso **Editar** e clique em **Enviar**.

   ![Compartilhar planilha de entrada](/help/forms/assets/form-submission-share-incoming.png)

1. Para copiar o link da planilha, clique no botão **Compartilhar** no canto superior direito e selecione **Copiar Link**.

   ![Copiar link da planilha de entrada](/help/forms/assets/form-submission-copy-link.png)

#### 4. Vincule a planilha na definição do formulário

Para configurar o serviço de Envio do Forms com o Google Sheets ou o Microsoft Excel, execute as seguintes etapas:

1. Abra a planilha que contém a definição de formulário.
1. Na linha correspondente ao campo **Enviar**, cole o link da planilha copiada na coluna **Ação**.

   ![Vincular uma planilha](/help/forms/assets/form-submission-sheet-linking.png)

1. Visualize e publique a planilha usando o [AEM Sidekick](https://www.aem.live/docs/sidekick) com o serviço de Envio de Formulário atualizado.

>[!NOTE]
>
> Consulte a [planilha](/help/forms/assets/spreadsheet.xlsx) para usar o serviço de Envio do Forms.

### Configuração do serviço de envio do Forms usando a API

Você também pode enviar uma solicitação **POST** ao formulário para atualizar a folha `incoming` com os dados.

>[!NOTE]
>
> * Se a planilha `incoming` não existir, o AEM não enviará dados para esta pasta de trabalho.
> * Compartilhe a planilha `incoming` com a Adobe Experience Manager `forms@adobe.com` e conceda acesso de edição.
> * Visualize e publique a planilha `incoming` no sidekick.

Para entender como formatar a solicitação POST para configurar sua planilha, consulte a [documentação sobre APIs](https://main--afb--adobe.hlx.page/docs/index.html#/paths/~1%7Bid%7D/post). Você pode observar o exemplo fornecido abaixo:

Você pode usar ferramentas como curl ou Postman para executar essa solicitação de POST, conforme demonstrado abaixo.

* **Usando o Postman**:

Por exemplo, envie a solicitação abaixo no Postman após substituir:
* `{id}` com sua ID de formulário
* `site or repository` com seu repositório GitHub ou nome do site
* `organization` com seu nome de usuário do GitHub

  ```json
  POST 'https://forms.adobe.com/adobe/forms/af/submit/{id}' \
  --header 'Content-Type: application/json' \
  --header 'x-adobe-routing: tier=live,bucket=main--[site/repository]--[organization]' \
  --data '{
      "data": {
          "startDate": "2025-01-10",
          "endDate": "2025-01-25",
          "destination": "Australia",
          "class": "First Class",
          "budget": "2000",
          "amount": "1000000",
          "name": "Mary",
          "age": "35",
          "subscribe": null,
          "email": "mary@gmail.com"
              }
          }'
  ```

Clicar no botão **Enviar** no Postman retorna uma resposta `201 Created`, e a planilha `incoming` é atualizada com os dados enviados.

![tela do carteiro](/help/forms/assets/postman-api.png)

* **Usando o comando Curl**:

Por exemplo, execute o comando abaixo no terminal ou no prompt de comando após substituir:
* `{id}` com sua ID de formulário
* `site or repository` com seu repositório GitHub ou nome do site
* `organization` com seu nome de usuário do GitHub


>[!BEGINTABS]

>[!TAB Para macOS]

    &quot;json
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; \
    —header &quot;Content-Type: application/json&quot; \
    —header &quot;x-adobe-routing: tier=live,bucket=main—[site/repository]—[organization]&quot; \
    —data &#39;{
    &quot;data&quot;: {
    &quot;startDate&quot;: &quot;2025-01-10&quot;,
    &quot;endDate&quot;: &quot;2025-01-25&quot;,
    &quot;destino&quot;: &quot;Austrália&quot;,
    &quot;classe&quot;: &quot;Primeira Classe&quot;,
    &quot;orçamento&quot;: &quot;2000&quot;,
    &quot;valor&quot;: &quot;100000&quot;,
    &quot;nome&quot;: &quot;Joe&quot;,
    &quot;idade&quot;: &quot;35&quot;,
    &quot;assinatura&quot;: nulo,
    &quot;email&quot;: &quot;mary@gmail.com&quot;
    }
    &#39;
    
    &quot;

>[!TAB Para SO Windows]

    &quot;json
    
    curl -X POST &quot;https://forms.adobe.com/adobe/forms/af/submit/{id}&quot; ^
    —header &quot;Content-Type: application/json&quot; ^
    —header &quot;x-adobe-routing: tier=live,bucket=main—[site/repository]—[organization]&quot; ^
    —data &quot;{\&quot;data\&quot;: {\&quot;startDate\&quot;: \&quot;2025-01-10\&quot;, \&quot;endDate\&quot;: \&quot;2025-01-25\&quot;, \&quot;destino\&quot;: \&quot;Austrália\&quot;, \&quot;classe\&quot;: \&quot;Primeira classe\&quot;, \&quot;orçamento\&quot;: \&quot;2000\&quot;, \&quot;valor\&quot;: \&quot;1000000\&quot;, \&quot;nome\&quot;: \&quot;Joe\&quot;, \&quot;idade\&quot;: \&quot;35\&quot;, \&quot;assinatura\&quot;: nulo, \&quot;email\&quot;: \&quot;mary@gmail.com\&quot;} 7}&quot;
    
    &quot;

>[!ENDTABS]

A solicitação POST mencionada acima atualiza a folha `incoming` com a resposta abaixo:

```json
    < HTTP/1.1 201 Created
    < Connection: keep-alive
    < Content-Length: 0
    < X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
    < X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
    < Accept-Ranges: bytes
    < Date: Fri, 10 Jan 2025 13:06:10 GMT
    < Via: 1.1 varnish
    < Access-Control-Allow-Origin: *
    < X-Served-By: cache-del21750-DEL
    < X-Cache: MISS
    < X-Cache-Hits: 0
    < X-Timer: S1736514370.704084,VS0,VE1234
```

A tela abaixo exibe a captura de tela da planilha `incoming` atualizada pelo envio de dados usando a API:

![planilha atualizada](/help/forms/assets/updated-sheet.png)

## Consulte também:

{{see-more-forms-eds}}
