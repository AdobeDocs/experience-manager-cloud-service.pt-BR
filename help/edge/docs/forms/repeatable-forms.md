---
title: Adicionar seções repetíveis a um formulário
description: Adicionar seções repetíveis a um formulário EDS
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# Adicionar seções repetíveis a um formulário

O bloco adaptável do Forms fornece a capacidade de adicionar ou fazer uma seção ou um componente de um formulário repetível. Isso permite que os usuários insiram informações várias vezes para o mesmo tipo de dados, facilitando a coleta de informações, como experiência de trabalho ou histórico educacional.

Por exemplo, considere um formulário usado para coletar informações sobre a experiência profissional de uma pessoa. Você pode ter uma seção repetível para capturar detalhes de cada tarefa anterior. A seção repetível normalmente contém campos como nome da empresa, título do cargo, datas de emprego e responsabilidades do cargo. O usuário pode adicionar várias instâncias da seção repetível para inserir informações sobre cada cargo que manteve.

No final deste artigo, você aprenderá a:

* [Criar uma seção repetível em um formulário](#add-repeatable-sections-to-a-form)
* [Definir o número mínimo ou máximo de repetições em um formulário](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## Criar uma seção repetível

A criação de uma seção repetível em um formulário oferece aos usuários a capacidade de inserir várias instâncias do mesmo conjunto de dados, permitindo a coleta eficiente de informações repetitivas. Para criar uma seção repetível em um formulário:

1. Vá para a pasta do projeto do Edge Deliver no Microsoft SharePoint ou Google Workspace e abra a planilha.

1. Adicionar um campo de formulário com a propriedade `type` definida como `fieldset`
1. Especifique `Name` do campo. A propriedade name é usada para criar uma seção repetível.
1. Habilite a repetibilidade definindo `repeatable` como `true`.
1. Especifique um `label` descritivo para o campo. Ele serve como o cabeçalho da seção repetível.

   Consulte a imagem abaixo para obter uma ilustração de uma seção de histórico de emprego em um formulário de requisição de cargo.

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. Para cada campo que você deseja incluir na seção, defina sua propriedade `Fieldset` com o mesmo nome que você escolheu na etapa 3.

   Por exemplo, designe `experience` na propriedade Fieldset de todos os campos relevantes a serem incluídos na seção `employment history`.

   ![exemplo de um campo de seção repetível e suas propriedades](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar e publicar a planilha. A seção repetível é adicionada ao formulário.

   Abaixo da seção repetível, os usuários encontram um botão intuitivo **Adicionar**, que facilita a adição de várias seções com facilidade.

   ![seção repetível, botão Adicionar, para adicionar várias seções ](/help/edge/assets/repeatable-section-example.png)


## Definindo Repetições Mínimas e Máximas

No design do formulário, é benéfico definir repetições mínimas e máximas para seções repetíveis. Ao fazer isso, você estabelece controle e consistência e, ao mesmo tempo, orienta os usuários com eficiência. Para definir o número mínimo ou máximo de repetições:

1. Vá para a pasta do projeto do Edge Deliver no Microsoft SharePoint ou Google Workspace e abra a planilha.

1. Para um campo de `type` `fieldset` e propriedade `repeatable` definida como `true`:

   * defina a propriedade `min` para especificar o número mínimo de vezes que a seção pode ser repetida.

   * defina a propriedade `max` para especificar o número máximo de vezes que a seção pode ser repetida.

   ![Defina as propriedades min e max para especificar o número de vezes que a seção pode ser repetida](/help/edge/assets/repeatable-section-set-min-max.png)

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para visualizar e publicar a planilha.

   Ao adicionar uma seção repetível, os usuários encontram um ícone intuitivo **Excluir**, facilitando a remoção de seções repetíveis. Depois de adicionadas, essas seções não podem ser diminuídas para menos instâncias do que o especificado pela propriedade `min`. Isso garante a adesão ao requisito mínimo definido para o preenchimento do formulário.

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Forms Block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Services project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-SharePoint)._" 


To add repeatable sections in Edge Delivery:

1. [Author a form using Microsoft Excel](#author-form)
2. [Preview and publish the form](#preview-form)

### Author a form using Microsoft Excel {#author-form}

1. Go to your Edge Deliver project folder on Microsoft SharePoint or Google Workspace and open your spreadsheet. For example, open an a spreadsheet named `loan-application.xlsx`.

1. Add a new columns labeled `Repeatable` to the sheet contaning your form fields. By default, the `shared-default` sheet contains the form fields.  

1. Add new columns labeled as `Repeatable`, `Min`, and `Max` in your Microsoft Excel file.
1. Specify the value for the `Repeatable` column as `True` for the fieldset that you want to make repeatable.
1. Specify the values for the `Min` and `Max` columns. The `Min` value represents the minimum number of occurrences for which the panel repeats, while the `Max` value represents the maximum number of occurrences for which the panel repeats.
1. Save your Microsoft Excel file.
     
>[!NOTE]
>
> Here is the [Loan application](/help/forms/assets/loan-application.xlsx) excel sheet for your reference. 

### Preview/Publish the form using your Edge Delivery Service

1. Open or create new document file in a Microsft SharePoint Site to embed the Excel sheet  in it using a `Form Block`. For example, open the `index` file and add a `Form Block`.
2. Open the command prompt, navigate to your AEM Edge Delivery project directory on your local machine, and execute the command as `aem up`.

The form is accessible at `https://localhost:3000`, where clicking the `Add` button adds new repeatable section for entering co-applicant details. You can also delete the the repeatable section by clicking the `Delete` button. 

>[!NOTE]
>
> If you encounter a "Page Not Found" error while accessing your form at localhost, add the directory name of the Microsoft SharePoint Site in front of the URL where your form is located. For example, `http://localhost:3000/<dir-name>/`

-->


## Consulte também:

{{see-more-forms-eds}}
