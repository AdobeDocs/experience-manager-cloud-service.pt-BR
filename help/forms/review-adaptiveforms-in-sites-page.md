---
title: Como enviar um formulário adaptável para revisão? Como gerenciar revisões para um formulário adaptável do aem?
description: A revisão é um mecanismo que permite ao revisor executar tarefas diferentes para formulários adaptáveis usando a etapa Atribuir tarefa.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 4%

---


# Criar e gerenciar revisões para um Formulário adaptável {#review-step-forms-aem-sites-page}

Usar o [Atribuir etapa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html#assign-task-step) do workflow AEM, o revisor revisa o formulário enviado e executa a ação nele. Para revisar o formulário enviado usando a etapa Atribuir tarefa, siga estas etapas:

1. [Criar um fluxo de trabalho do AEM](#create-an-aem-workflow)
1. [Configurar a ação de envio do contêiner de Formulário adaptável](#configure-submit-action)
1. [Enviar um formulário adaptável após revisão](#submit-af-after-review)

## Criar um fluxo de trabalho do AEM {#create-an-aem-workflow}

1. Abra a instância do autor no modo de edição.
1. Ir para **[!UICONTROL Ferramentas]** >  **[!UICONTROL Fluxo de trabalho]** >  **[!UICONTROL Modelos]** > **[!UICONTROL Criar]** > **[!UICONTROL Criar modelo]**
1. Especifique o Título do workflow e adicione o **[Atribuir tarefa]** etapa
1. Toque ![settings_icon](assets/settings_icon.png) na barra de ações. A variável **[!UICONTROL Atribuir tarefa]** será aberta.
1. Abertura [!UICONTROL Formulário e documento] e abrir [!UICONTROL Preenchido] e especifique:

   * Selecione o arquivo de dados de entrada usando
   * Selecione os anexos de entrada usando

   ![Etapa de revisão](/help/forms/assets/assigntask-review1.gif)

1. Abertura **[!UICONTROL Destinatário]** e abrir [!UICONTROL Preenchido] e especifique **[!UICONTROL Opções de atribuição]**:

   ![Etapa de revisão](/help/forms/assets/review-assignstep.png)

1. Clique em **[!UICONTROL Concluído]** para salvar as alterações.

## Configurar ação de envio {#configure-submit-action}

Agora, configure a ação Enviar de um componente de Contêiner de formulário adaptável na página do site:

1. Vá para a página do site.
1. Toque ![settings_icon](assets/settings_icon.png) de um contêiner de Formulário adaptável. A variável **[!UICONTROL Contêiner de formulário adaptável]** será aberta.
1. Abra o **[!UICONTROL Envio]** e especificar **[!UICONTROL Ação de envio]** para [Chamar um fluxo de trabalho de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=en#invoke-an-aem-workflow)

1. Clique em [Concluído] para salvar as configurações.

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## Enviar um formulário adaptável após revisão {#submit-af-after-review}

Para revisar e confirmar o Formulário adaptável enviado:

1. Ir para [!UICONTROL Ferramentas] >  [!UICONTROL Fluxo de trabalho] >  [!UICONTROL Instâncias]
1. Na Caixa de entrada, é possível ver que uma instância está sendo criada.
1. Selecione a instância e clique em [!UICONTROL Abertura].
1. Agora é possível ver o formulário enviado.

O revisor executa ações diferentes, pois:

* **Enviar**: O revisor preenche o formulário e o envia para processamento adicional.
* **Salvar**: O revisor salva o formulário em seu estado atual sem enviá-lo.
* **Redefinir**: O revisor apaga todas as alterações feitas no formulário e o restaura ao estado original.
* **Delegar**: o revisor transfere a propriedade do formulário para outra pessoa para ação ou revisão adicional.
