---
title: Como configurar uma ação enviar para um formulário adaptável?
description: Um Formulário adaptável fornece várias Ações de envio. Uma Ação de envio define como um Formulário adaptável é processado após o envio. Você pode usar as Ações de envio integradas ou criar as suas próprias ações.
keywords: como selecionar a ação enviar para um formulário adaptável, conectar um formulário adaptável à lista do sharepoint, conectar um formulário adaptável à biblioteca de documentos do sharepoint, conectar um formulário adaptável ao modelo de dados de formulário (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 6%

---

# Ação de envio do formulário adaptável

| Versão | Link do artigo |
|---------|-----------------------------|
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service (Componentes de base) | [Clique aqui](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (Componentes principais) | [Clique aqui](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Este artigo |


O envio de formulários é a etapa final crítica na jornada do usuário — é onde os dados coletados são processados e as ações são executadas. Este documento fornece um guia abrangente para configurar e gerenciar ações de envio para o Adaptive Forms no Universal Editor.

## O que você vai aprender

No final deste documento, você entenderá como:

- Configurar diferentes tipos de ações de envio para seus formulários
- Configurar envios de endpoint REST para integração com sistemas externos
- Configurar envios de email para respostas de formulário
- Implementar ações de envio personalizadas para necessidades comerciais específicas
- Lidar com cenários de erro e validação de formulário durante o envio

## Público-alvo

Este guia foi projetado para:

- **Desenvolvedores de formulários** implementando a lógica de envio
- **Integradores de sistemas** conectando formulários a sistemas back-end
- **Analistas de negócios** definindo fluxos de trabalho de formulário
- **Arquitetos técnicos** projetando processos de envio de formulário

## Ações de envio para o Forms criadas no Editor universal

As seguintes ações de envio são suportadas pelo [Adaptive Forms criado no Universal Editor](/help/edge/docs/forms/universal-editor/create-forms.md):

- [Enviar e-mail](/help/forms/configure-submit-action-send-email.md)
- [Chamar um fluxo do Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Enviar para o SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Chamar Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Enviar usando o Modelo de dados de formulário (FDM)](/help/forms/integrate-adaptive-form-with-fdm.md)
- [Enviar para o Armazenamento de blob do Azure](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Enviar para Ponto de Extremidade REST](/help/forms/configure-submit-action-restpoint.md)
- [Enviar para o OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Chamar um fluxo de trabalho do AEM](/help/forms/configure-submit-action-workflow.md)
- [Enviar ao Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
- [Enviar para o Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
- [Enviar para planilha](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

É possível configurar a ação de envio para formulários criados no Universal Editor usando a guia **Envio** da extensão **Editar Propriedades do Formulário**.

**Como configurar a ação enviar para o Forms criada no Universal Editor?**
É possível configurar a ação de envio para formulários criados no Universal Editor usando a guia **Envio** da extensão **Editar propriedades do formulário**.

![Ícone de propriedades do formulário](/help/forms/assets/ue-form-properties-icon.png)

![Assistente de Propriedades do Formulário](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

>[!NOTE]
>
> - Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
> - Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.
