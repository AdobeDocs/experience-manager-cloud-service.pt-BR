---
title: Como configurar uma ação enviar para um formulário adaptável?
description: Um Formulário adaptável fornece várias Ações de envio. Uma Ação de envio define como um Formulário adaptável é processado após o envio. Você pode usar as Ações de envio integradas ou criar as suas próprias ações.
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 7%

---


# Enviar ações compatíveis com o Adaptive Forms

Formulários adaptáveis fornecem uma experiência envolvente, responsiva, dinâmica e adaptável. Eles fornecem uma interface de usuário intuitiva e um conjunto de componentes prontos para uso para projetar e gerenciar formulários com eficiência. Você pode configurar várias ações de envio para enviar dados de formulário para serviços como OneDrive, SharePoint, Workfront Fusion e muito mais.

Uma ação de envio é disparada quando um usuário clica no botão **[!UICONTROL Enviar]** em um Formulário adaptável. O Forms as a Cloud Service fornece várias ações de envio prontas para uso. As ações de envio integradas permitem:

* Enviar dados de formulário por email sem esforço
* Inicie fluxos do Microsoft® Power Automate ou fluxos de trabalho do AEM ao transmitir os dados.
* Transmita diretamente os dados do formulário para o Microsoft® SharePoint Server, Microsoft® Azure Blob Storage ou Microsoft® OneDrive.
* Envie os dados com facilidade para uma fonte de dados configurada usando o Modelo de dados de formulário (FDM).
* Envie convenientemente os dados para um endpoint REST.

## Enviar ações compatíveis com o Adaptive Forms

O AEM Forms oferece as seguintes ações de envio prontas para uso:

* [Enviar e-mail](/help/forms/configure-submit-action-send-email.md)
* [Chamar um fluxo do Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Enviar para o SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Chamar um Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Enviar usando o Modelo de dados de formulário (FDM)](/help/forms/using-form-data-model.md)
* [Enviar para o Armazenamento de blob do Azure](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Enviar para endpoint REST](/help/forms/configure-submit-action-restpoint.md)
* [Enviar para o OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Chamar um fluxo de trabalho do AEM](/help/forms/configure-submit-action-workflow.md)
* [Enviar para Envolvimento da Marketo](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Enviar para o Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [Enviar para planilha](/help/forms/forms-submission-service.md)

Também é possível enviar um Formulário adaptável para outras configurações de armazenamento:

* [Conectar o formulário adaptável ao aplicativo do Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Conectar um formulário adaptável ao Microsoft](/help/forms/ms-dynamics-odata-configuration.md)

## Enviar Suporte De Ação Entre Tipos De Criação

A tabela abaixo mostra quais ações de envio são compatíveis com base no método de criação de formulário usado no AEM Forms:

| Ação de envio | [Componentes de base](/help/forms/configuring-submit-actions.md) | [Componentes principais](/help/forms/configure-submit-actions-core-components.md) | [Editor Universal](/help/forms/configure-submit-action-eds-forms.md#submit-actions-supported-by-adaptive-forms-created-in-universal-editor) | [Forms baseado em documento](/help/forms/configure-submit-action-eds-forms.md#supported-submit-actions-for-document-based-forms) |
|----------------------------|------------------------|------------------|------------------|------------------------|
| Enviar um e-mail | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Fluxo do Power Automate | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Enviar para o SharePoint | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Workfront Fusion | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Enviar usando FDM | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Enviar para o AEP | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Armazenamento Azure Blob | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Enviar para Ponto de Extremidade REST | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Enviar ao Marketo Engage | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Enviar para o OneDrive | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Chamar fluxo de trabalho de AEM | ✅ com suporte | ✅ com suporte | ✅ com suporte |                        |
| Enviar para planilha |                        |                  | ✅ com suporte | ✅ com suporte |


## Revalidação do lado do servidor no formulário adaptável

Normalmente, em qualquer sistema de captura de dados online, os desenvolvedores colocam algumas validações do JavaScript no lado do cliente para aplicar algumas regras de negócios. Mas em navegadores modernos, os usuários finais têm uma maneira de ignorar essas validações e fazer envios manualmente usando várias técnicas, como o Console DevTools do navegador da Web. Essas técnicas também são válidas para o Adaptive Forms. Um desenvolvedor de formulários pode criar várias lógicas de validação, mas tecnicamente, os usuários finais podem ignorar essas lógicas de validação e enviar dados inválidos para o servidor. Dados inválidos violariam as regras de negócios aplicadas por um autor de formulários.

O recurso de revalidação do lado do servidor também permite executar as validações que um autor do Adaptive Forms forneceu ao criar um Formulário adaptável no servidor. Isso evita qualquer possível comprometimento dos envios de dados e violações das regras de negócios representadas em termos de validações de formulário.


### O que validar no servidor?

Todas as validações de campo prontas para uso (OOTB) de um Formulário adaptável que são executadas novamente no servidor são:

* Obrigatório
* Cláusula de Imagem de Validação
* Expressão de validação

Use a **[!UICONTROL Revalidar no servidor]** em Contêiner de Formulário Adaptável na barra lateral para habilitar ou desabilitar a validação no servidor para o formulário atual.

![Habilitando A Validação No Lado Do Servidor](assets/revalidate-on-server.png)

**Habilitando A Validação No Lado Do Servidor**

Se o usuário final ignorar essas validações e enviar os formulários, o servidor executará novamente a validação. Se a validação falhar no final do servidor, a transação de envio será interrompida. O formulário original é apresentado ao usuário novamente. Os dados capturados e os dados enviados são apresentados ao usuário como um erro.

>[!NOTE]
>
>A validação do lado do servidor valida o modelo de formulário. É recomendável criar uma biblioteca do cliente separada para validações e não misturá-la com outras coisas, como o estilo do HTML e a manipulação de DOM na mesma biblioteca do cliente.

<!--### Supporting Custom functions in Validation Expressions {#supporting-custom-functions-in-validation-expressions-br}

At times, if there are **complex validation rules**, the exact validation script reside in custom functions and author calls these custom functions from field validation expression. To make this custom function library known and available while performing server-side validations, the form author can configure the name of AEM client library under the **[!UICONTROL Basic]** tab of Adaptive Form Container properties as shown below.

![Supporting Custom functions in Validation Expressions](assets/clientlib-cat.png)

Supporting Custom functions in Validation Expressions

Author can configure customJavaScript library per Adaptive Form. In the library, only keep the reusable functions, which have dependency on jquery and underscore.js third-party libraries.

Refer to the following articles to learn how to create custom functions for:

* [Adaptive Forms based on Foundation Components](/help/forms/rule-editor.md#custom-functions-in-rule-editor)
* [Adaptive Forms based on Core Components](/help/forms/create-and-use-custom-functions.md)
* [Adaptive Forms authored using Document-Based Authoring](/help/edge/docs/forms/rules-forms.md#create-a-custom-function)
* [Adaptive Forms created using the Universal Editor](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#create-a-custom-function)

## Error handling on Submit Action {#error-handling-on-submit-action}

As a part of AEM security and hardening guidelines, configure custom error pages such as 400.jsp, 404.jsp, and 500.jsp. These handlers are called, when on submitting a form 400, 404, or 500 errors appear. The handlers are also called when these error codes are triggered on the Publish node. You can also create JSP pages for other HTTP error codes.

When you prefill a form data model (FDM), or schema based Adaptive Form with XML or JSON data complaint to a schema that is data does not contain `<afData>`, `<afBoundData>`, and `</afUnboundData>` tags, then the data of unbounded fields of the Adaptive Form is lost. The schema can be an XML schema, JSON schema, or a Form Data Model (FDM). Unbounded fields are Adaptive Form fields without the `bindref` property.-->

## Consulte também

{{af-submit-action}}

