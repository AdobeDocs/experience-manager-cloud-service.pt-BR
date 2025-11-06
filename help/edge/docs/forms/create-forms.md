---
title: Criar um formulário usando o bloco adaptável do Forms
description: Introdução ao Edge Delivery Services para AEM Forms. Formas perfeitas de artesanato, rápido! Criação baseada em documentos do AEM Forms Edge Delivery = velocidade incrível e formulários compatíveis com SEO para usuários e mecanismos de pesquisa mais satisfeitos.
feature: Edge Delivery Services
role: Admin, Developer
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Criar um formulário usando o bloco adaptável do Forms

>[!VIDEO](https://video.tv.adobe.com/v/3427881?quality=12&learn=on)

O AEM Forms Edge Delivery fornece um bloco, conhecido como Bloco do Adaptive Forms, para ajudar você a criar formulários facilmente para capturar e armazenar dados capturados. Você pode [criar um novo projeto do AEM pré-configurado com o Bloco do Adaptive Forms](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) ou [adicionar o Bloco do Adaptive Forms a um projeto existente do AEM](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project).

Esses formulários enviam dados diretamente para um arquivo do Microsoft Excel ou do Google Sheets, permitindo que você use um ecossistema vibrante e APIs robustas do Google Sheets, do Microsoft Excel e do Microsoft SharePoint para processar facilmente os dados enviados ou iniciar um fluxo de trabalho de negócios existente.

![Ecossistema de criação baseado em documentos](/help/edge/assets/document-based-authoring-workflow-create-form.png)


## Pré-requisitos

Antes de começar, verifique se você concluiu as seguintes etapas:

- Configure um [projeto do AEM usando o modelo do AEM Forms](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) [adicionou o Bloqueio do Adaptive Forms ao seu Projeto do AEM existente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) e clone o repositório do GitHub correspondente no computador local.
<!--In this document, the local folder of your Edge Delivery Services (EDS) project is referred as `[EDS Project repository]`.  -->
- Verifique se você tem acesso ao Google Sheets ou ao Microsoft SharePoint. Para configurar o Microsoft SharePoint como fonte de conteúdo, consulte [Como usar o SharePoint](https://www.aem.live/docs/setup-customer-sharepoint).



## Criar um formulário

<!--
+++ Step 1: Add the Adaptive Forms Block to your Edge Delivery Services (EDS) project.

The Adaptive  empowers users to create forms for an Edge Delivery Service Site. However, this block isn't included in the default AEM boilerplate (used to create an Edge Delivery Services project). To seamlessly integrate the Adaptive Forms Block into your Edge Delivery Services project:

1. **Clone the Adaptive Forms Block repository**: Clone the [Adaptive Forms Block repository](https://github.com/adobe-rnd/form-block) on your local machine. It contains the code to render the form on an EDS webpage. In this document, the local folder of your Forms Block repository is referred as `[Adaptive Forms Block repository]`.
2. **Locate the Adaptive Forms Block Repository:** Access the [Adaptive Forms Block repository]/blocks/src folder and copy its content. 

3. on your local machine and copy the `form` folder. 
4. **Paste the Adaptive Forms Block's code into your EDS Project:**
Navigate to the [EDS Project repository]/blocks/ folder on your local machine and create a 'form' folder. Paste the `[Adaptive Forms Block repository]/blocks/src content`, copied in perevious step to the `[EDS Project repository]/blocks/form` folder.
1. **Commit Changes to GitHub:** Check in the `[EDS Project repository]/blocks/form` folder and its underlying files to your Edge Delivery Services project on GitHub.

After completing these steps, the Adaptive Forms Block is successfully added to your Edge Delivery Services (EDS) project repository on GitHub. You can now create and add forms to a EDS Sites page.
 

**Troubleshooting GitHub build issues**

Ensure a smooth GitHub build process by addressing potential issues:

- **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file.

- **Handle Linting Errors:**
    Should you come across any linting errors, you can bypass them. Open the [EDS Project]/package.json file and modify the "lint" script from "lint": "npm run lint:js && npm run lint:css" to "lint": "echo 'skipping linting for now'". Save the file and commit the changes to your GitHub project. -->

+++ Etapa 1: Crie um formulário usando o Microsoft Excel ou a Planilha do Google.

Em vez de navegar por processos complexos, é possível criar um formulário sem esforço usando uma planilha. Você pode definir as linhas e colunas que compõem a estrutura do formulário. Cada linha representa um [campo de formulário](/help/edge/docs/forms/form-components.md#available-components) individual e os cabeçalhos de coluna definem as [propriedades de campo](/help/edge/docs/forms/form-components.md#components-properties) correspondentes.

Por exemplo, considere a seguinte planilha em que os campos de estrutura de tópicos de linhas de uma planilha [consulta](/help/edge/assets/enquiry.xlsx) e os cabeçalhos de coluna definem suas propriedades:

![Planilha de consulta](/help/edge/assets/enquiry-form-spreadsheet.png)

Para continuar com a criação do formulário:

1. Acesse a pasta do projeto do AEM Edge Delivery no Microsoft SharePoint ou no Google Drive.

1. Crie uma Pasta de trabalho do Microsoft Excel ou uma Planilha do Google em qualquer lugar no diretório do projeto do AEM Edge Delivery. Por exemplo, crie uma planilha com o nome `enquiry` no diretório do projeto AEM Edge Delivery no Google Drive.

   <!-- ![Sample Content on Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)-->

1. Verifique se a planilha está compartilhada com o usuário AEM apropriado (por exemplo, `forms@adobe.com`) [de acordo com as configurações especificadas para seu projeto](https://www.aem.live/docs/setup-customer-sharepoint). Conceda ao usuário permissão de edição para a planilha.

1. Abra a planilha criada e renomeie a planilha padrão como &quot;shared-aem&quot;.

   ![renomear planilha padrão como &quot;padrão compartilhado&quot;](/help/edge/assets/rename-sheet-to-shared-default.png)

   >[!IMPORTANT]
   >
   >**A planilha na qual o formulário foi criado tem restrições sobre o nome que pode ser dado a ele. Somente `helix-default` e `shared-aem` podem ser usados como nomes de planilha.**

1. Para adicionar os campos de formulário, insira linhas e cabeçalhos de coluna na planilha &quot;shared-aem&quot;. Cada linha deve representar um [campo de formulário](/help/edge/docs/forms/form-components.md#available-components), com cabeçalhos de coluna definindo o campo correspondente [propriedades](/help/edge/docs/forms/form-components.md#components-properties).


   Para um início rápido, considere copiar o conteúdo da [Planilha de consulta](/help/edge/assets/enquiry.xlsx) para a sua planilha. Depois de copiar o conteúdo, salve sua planilha.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. Use o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar a planilha.

   ![Usar AEM Sidekick para visualizar a planilha](/help/edge/assets/preview-form.png)

   Ao visualizar, novas guias do navegador exibem o conteúdo da planilha no formato JSON. Certifique-se de capturar a URL de visualização, pois ela é necessária para renderizar o formulário no próximo da seção. O formato do URL é o seguinte:


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form-path>/<form-file-name>.json
   ```

   - `<branch>` refere-se à ramificação do seu repositório GitHub.
   - `<repository>` indica seu repositório GitHub.
   - `<owner>` refere-se ao nome de usuário da sua conta GitHub que hospeda seu repositório GitHub.

   Por exemplo, se o repositório do seu projeto for chamado de &quot;wefinance&quot;, estiver localizado na conta &quot;wkndform&quot; e você estiver usando a ramificação &quot;main&quot;, o URL será semelhante ao seguinte:

`https://main--wefinance--wkndform.aem.page/enquiry.json`
&lt;!—(https://main--wefinance--wkndform.aem.page/enquiry.json)-->


+++

+++ Etapa 2: visualize o formulário usando a página do Edge Delivery Services.


Até agora, você preparou a estrutura do formulário. Agora, para visualizar o formulário:

1. Abra sua conta do Microsoft SharePoint ou Google Drive e navegue até o diretório do projeto do AEM Edge Delivery.



1. Abra um arquivo de documento (por exemplo, arquivo de índice) para incorporar o formulário. Como alternativa, você pode [criar um novo documento](/help/edge/assets/enquiry-form.docx).

1. Mova para o local desejado no documento onde você pretende adicionar o formulário.

1. Para criar um bloco de formulário para renderizar o formulário. Selecione Inserir > Tabela e crie uma tabela de uma coluna e duas linhas. Nomeie a tabela como &quot;Formulário&quot; e cole o URL de visualização na segunda linha. Verifique se o URL está formatado como um hiperlink, não como texto simples, como ilustrado abaixo:

   | Formulário |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |


   ![Adicionar bloco adaptável do Forms à sua página da Web](/help/edge/assets/enquiry-doc-to-embed-form.png)

   Esse bloco serve como um espaço reservado em que o formulário é incorporado. Na segunda linha do bloco, adicione a URL de visualização do arquivo `<form>.json` como um hiperlink.

   >[!IMPORTANT]
   >
   >
   > Verifique se o URL está formatado como um hiperlink em vez de ser exibido como texto simples.


1. Use o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar o documento. A página agora exibe o formulário. Por exemplo, este é o formulário baseado na [planilha de consulta](/help/edge/assets/enquiry-form.docx):


   [![Um exemplo de formulário EDS](/help/edge/assets/updated-form.png)](https://main--wefinance--wkndform.aem.page/enquiry-form)

   Agora, preencha o formulário e clique no botão enviar, você enfrenta um erro, semelhante ao seguinte, porque a planilha ainda não está definida para aceitar os dados.

   ![erro no envio do formulário](/help/edge/assets/form-error.png)

+++


## Próxima etapa

[Prepare sua planilha](/help/edge/docs/forms/submit-forms.md) para começar a aceitar dados no envio do formulário.


