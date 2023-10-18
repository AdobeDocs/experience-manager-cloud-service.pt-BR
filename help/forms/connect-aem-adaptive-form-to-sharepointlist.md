---
title: Como conectar o formulário adaptável AEM à lista do Microsoft® SharePoint?
description: Conecte um formulário adaptável à lista Microsoft® SharePoint. Saiba como configurar a lista Microsoft® SharePoint e criar um Modelo de dados de formulário usando a configuração. Além disso, você aprenderá a integrar o FDM ao seu Formulário adaptável.
role: User, Developer
keywords: conectar o Formulário adaptável do AEM à Lista do Microsoft SharePoint, conectar o Formulário adaptável à Lista do Microsoft SharePoint, integrar o Formulário adaptável à Lista do Microsoft SharePoint, integrar o Formulário adaptável à Lista do AEM, enviar dados de um Formulário adaptável à Lista do Microsoft, enviar fluxo de trabalho para a Lista do SharePoint SharePoint AEM SharePoint.
source-git-commit: 0f8aed76af4d2640094a76f2805f73a0a619e33f
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---


# Conectar um formulário adaptável à lista Microsoft® SharePoint

<span class="preview"> Esse é um recurso de pré-lançamento acessível por meio de nossa [canal de pré-lançamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

**Microsoft® SharePoint**: O Microsoft® SharePoint habilita a colaboração fornecendo sites de equipe dinâmicos e eficientes para todas as equipes, departamentos e divisões. Ele é usado para armazenar, organizar, compartilhar e acessar informações de qualquer dispositivo usando qualquer navegador da Web, por exemplo, Microsoft® Edge, Internet Explorer, Chrome ou Firefox. Os dois principais componentes do **Microsoft® SharePoint** são:

* **Biblioteca de documentos Microsoft® SharePoint**: A Biblioteca de documentos da Microsoft® SharePoint exibe uma lista de arquivos e pastas, juntamente com suas informações principais, como a data da última modificação e o proprietário de um arquivo. Esse recurso facilita a organização e a navegação de arquivos.
Para obter instruções sobre como integrar uma **Biblioteca de documentos Microsoft® SharePoint** com um Formulário adaptável, consulte a [Ação de envio do formulário adaptável](/help/forms/configuring-submit-actions.md#submit-to-sharepoint) artigo.

* **Lista Microsoft® SharePoint**: a Lista do Microsoft® SharePoint é uma coleção de dados. É possível adicionar colunas para diferentes tipos de dados e criar visualizações para exibir dados de maneira eficaz. É possível agrupar, filtrar, classificar e formatar as listas facilmente.

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

## Pré-requisitos para conectar um formulário adaptável à lista Microsoft® SharePoint {#prerequisites}

Antes de conectar um formulário adaptável à lista Microsoft® SharePoint, execute as seguintes etapas:

1. [Configurar a lista Microsoft® SharePoint](/help/forms/configure-data-sources.md#configure-microsoft-sharepoint-list)
1. [Criar um modelo de dados de formulário usando a configuração da lista do Microsoft® SharePoint](/help/forms/create-form-data-models.md)
1. [Configurar o modelo de dados do formulário para recuperar e enviar dados](/help/forms/work-with-form-data-model.md#configure-services)
1. [Criação de um Formulário adaptável](/help/forms/creating-adaptive-form-core-components.md)

Agora é possível:

* [Conectar a lista Microsoft® SharePoint a um formulário adaptável](#connect-an-adaptive-form-to-microsoft-sharepoint-list-connect-af-sharepoint-list)
* [Conectar a lista do Microsoft® SharePoint a um fluxo de trabalho do AEM](#connect-sharepoint-list-workflow)

## Conectar um formulário adaptável à lista Microsoft® SharePoint {#connect-af-sharepoint-list}

Para integrar a Lista de SharePoint Microsoft® ao seu Formulário adaptável [configurar um formulário adaptável para usar um modelo de dados de formulário](/help/forms/creating-adaptive-form-core-components.md#configure-a-schema-or-form-data-model-for-an-adaptive-formconfigure-schema-or-data-model-for-form)

Depois de configurar um formulário adaptável para usar um modelo de dados de formulário, você pode:

* [Configurar a ação Enviar usando um Modelo de dados de formulário](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)
* [Configurar o Editor de regras para chamar um Modelo de dados de formulário](/help/forms/rule-editor.md#invoke-form-data-model-service-invoke)

## Conectar a lista do Microsoft® SharePoint a um fluxo de trabalho do AEM {#connect-sharepoint-list-workflow}

Para integrar a Lista do Microsoft® SharePoint a um fluxo de trabalho para AEM:

1. [Criar um fluxo de trabalho para chamar um modelo de dados de formulário](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=pt-BR)

   <!--
    To create a new workflow with the editor, perform the following steps:
    1.  Go to your **AEM Forms Author** instance > **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
    1.  Click **[!UICONTROL Create]** > **[!UICONTROL Create Model]**. The Add Workflow Model dialog appears. 
    1. Specify **[!UICONTROL Title]** and **[!UICONTROL Name (optional)]**.
    1. Click **[!UICONTROL Done]**. The new model is listed in the Workflow Models console.
    1. Select your new workflow, then use **[!UICONTROL Edit]** to open it for configuration.
    1. Add **[!UICONTROL Invoke Form Data Model Service]** step to your workflow.
    1. Confirm the changes with Sync (editor toolbar) to generate the runtime model.
    -->

1. [Configurar a ação Enviar para invocar um fluxo de trabalho do AEM](/help/forms/configuring-submit-actions.md#invoke-an-aem-workflow)


Saiba como [usar o fluxo de trabalho do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/workflow/use-workflow.html) para colaborar, gerenciar e processar conteúdo em um Formulário adaptável.

## Práticas recomendadas {#best-practices}

<!-- * For storing data in a tabular format or implementing data permissions, it is advisable to use Microsoft® SharePoint List rather than Microsoft® SharePoint Document Library. -->
* Na Lista do Microsoft® SharePoint, os seguintes tipos de coluna não são suportados:
   * coluna de imagem
   * coluna de metadados
   * coluna de pessoa
   * coluna de dados externos

## Consulte também {#see-also}

* [Criar um formulário adaptável baseado em um componente principal](/help/forms/creating-adaptive-form-core-components.md)
* [Configurar fontes de dados](/help/forms/configuring-submit-actions.md)
* [Criar modelo de dados de formulário](/help/forms/create-form-data-models.md)
* [Usar workflows AEM centrados na Forms - referência de etapa para automatizar processos de negócios](/help/forms/aem-forms-workflow-step-reference.md)

## Informações adicionais

* [Criar ou adicionar um formulário adaptável a uma página do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Incorporar um formulário adaptável a uma página do AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)
* [Criar, usar e personalizar temas em um Formulário adaptável](/help/forms/using-themes-in-core-components.md)

>[!MORELIKETHIS]
>
>* [Criar uma ação enviar personalizada para o Forms adaptável](/help/forms/custom-submit-action-form.md)





