---
title: Como configurar uma ação enviar para um formulário adaptável?
description: Um Formulário adaptável fornece várias Ações de envio. Uma Ação de envio define como um Formulário adaptável é processado após o envio. Você pode usar as Ações de envio integradas ou criar as suas próprias ações.
keywords: como selecionar a ação enviar para um formulário adaptável, conectar um formulário adaptável à lista do sharepoint, conectar um formulário adaptável à biblioteca de documentos do sharepoint, conectar um formulário adaptável ao modelo de dados de formulário (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 8%

---


# Ações de envio para o Edge Delivery Services Forms

| Versão | Link do artigo |
|---------|-----------------------------|
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=pt-BR) |
| AEM as a Cloud Service (Componentes de base) | [Clique aqui](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (Componentes principais) | [Clique aqui](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Este artigo |

As Ações de envio definem o que acontece quando um usuário envia um formulário, como armazenar dados, acionar workflows ou integrar a sistemas de terceiros. O tipo de ações de envio que você pode configurar depende do método de criação usado para criar o Edge Delivery Services Forms.

Você pode criar o Edge Delivery Services Forms usando o [Editor Universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) ou a criação do [Forms Baseado em Documentos](/help/edge/docs/forms/overview.md) e configurar os formulários com ações de envio diferentes.

## Ações de envio para o Forms criadas no Editor universal

As seguintes ações de envio são suportadas pelo [Adaptive Forms criado no Universal Editor](/help/edge/docs/forms/universal-editor/create-forms.md):

* [Enviar e-mail](/help/forms/configure-submit-action-send-email.md)
* [Chamar um fluxo do Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Enviar para o SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Chamar Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Enviar usando o Modelo de dados de formulário (FDM)](/help/forms/using-form-data-model.md)
* [Enviar para o Armazenamento de blob do Azure](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Enviar para Ponto de Extremidade REST](/help/forms/configure-submit-action-restpoint.md)
* [Enviar para o OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Chamar um fluxo de trabalho do AEM](/help/forms/configure-submit-action-workflow.md)
* [Enviar ao Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Enviar para o Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [Enviar para planilha](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

É possível configurar a ação de envio para formulários criados no Universal Editor usando a guia **Envio** da extensão **Editar Propriedades do Formulário**.

<!--**How to Configure Submit Action for Forms authored in Universal Editor?**
You can configure the submit action for forms created in the Universal Editor using the **Submission** tab of the **Edit Form Properties** extension.

![Form properties icon](/help/forms/assets/ue-form-properties-icon.png)

![Universal Editor Form Properties](/help/forms/assets/ue-form-properties.png)-->

>[!NOTE]
>
> * Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
> * Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.

## Ações de Envio para o Forms Baseado em Documento

O Forms baseado em documento suporta o envio somente para planilhas. Para saber como configurar sua planilha para receber dados enviados, consulte o artigo [Configurar suas Planilhas do Google ou arquivos do Microsoft Excel para começar a aceitar dados](/help/edge/docs/forms/submit-forms.md).

## Consulte também {#see-also}

{{af-submit-action}}

