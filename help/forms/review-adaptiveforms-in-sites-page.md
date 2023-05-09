---
title: Criação e gerenciamento de revisões do Adaptive Forms incorporado ou criado na página Sites
seo-title: Review is a mechanism that allows reviewer to perform different tasks for adaptive forms using Assign Task step
description: A revisão é um mecanismo que permite ao revisor executar tarefas diferentes para formulários adaptáveis usando a etapa Atribuir tarefa
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: daeb407e27b9f1d390fe40151ca16ec0196712e6
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 4%

---


# Etapa de revisão do Forms na página do site {#review-step-forms-aem-sites-page}

Usar o [Atribuir etapa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) do fluxo de trabalho de AEM, o revisor revisa o formulário enviado e executa uma ação sobre ele. Para revisar o formulário enviado usando a etapa Atribuir tarefa , siga estas etapas:

1. [Criar um fluxo de trabalho AEM](#create-an-aem-workflow)
1. [Configurar a ação de envio do contêiner do Formulário adaptável](#configure-submit-action)
1. [Enviar um formulário adaptável após a revisão](#submit-af-after-review)

## Criar um fluxo de trabalho AEM {#create-an-aem-workflow}

1. Abra a instância do autor no modo de edição.
1. Ir para **[!UICONTROL Ferramentas]** >  **[!UICONTROL Fluxo de trabalho]** >  **[!UICONTROL Modelos]** > **[!UICONTROL Criar]** > **[!UICONTROL Criar modelo]**
1. Especifique o Título do fluxo de trabalho e adicione o **[Atribuir tarefa]** step
1. Toque ![settings_icon](assets/settings_icon.png) na barra de ações. O **[!UICONTROL Atribuir tarefa]** será aberta.
1. Abrir [!UICONTROL Formulário e documento] e abra [!UICONTROL Pré-preenchido] e especifique:

   * Selecione o arquivo de dados de entrada usando
   * Selecione os anexos de entrada usando

   ![Etapa de revisão](/help/forms/assets/assigntask-review1.gif)

1. Abrir **[!UICONTROL Destinatário]** e abra [!UICONTROL Pré-preenchido] e especificar **[!UICONTROL Atribuir opções]**:

   ![Etapa de revisão](/help/forms/assets/review-assignstep.png)

1. Clique em **[!UICONTROL Concluído]** para salvar as alterações.

## Configurar ação de envio {#configure-submit-action}

Agora, configure a ação Enviar de um componente Contêiner de formulário adaptável na página do site :

1. Vá para a página do Site.
1. Toque ![settings_icon](assets/settings_icon.png) de um contêiner de Formulário adaptável. O **[!UICONTROL Contêiner de formulário adaptável]** será aberta.
1. Abra o **[!UICONTROL Submissão]** e especifique **[!UICONTROL Enviar ação]** para [Chamar um fluxo de trabalho AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. Clique em [Concluído] para salvar as configurações.

![submissiontab-revisewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## Enviar um formulário adaptável após a revisão {#submit-af-after-review}

Para revisar e confirmar o formulário adaptável enviado:

1. Ir para [!UICONTROL Ferramentas] >  [!UICONTROL Fluxo de trabalho] >  [!UICONTROL Instâncias]
1. Na Caixa de entrada, você pode ver que uma instância está sendo criada.
1. Selecione a instância e clique em [!UICONTROL Abrir].
1. Agora, é possível ver o formulário enviado.

O revisor executa ações diferentes como:

* **Enviar**: O revisor conclui o formulário e o envia para processamento adicional.
* **Salvar**: O revisor salva o formulário em seu estado atual sem enviá-lo.
* **Redefinir**: O revisor limpa todas as alterações feitas no formulário e o restaura em seu estado original.
* **Delegar**: O revisor transfere a propriedade do formulário para outra pessoa para nova ação ou revisão.
