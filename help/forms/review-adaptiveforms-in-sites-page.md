---
title: Como enviar um formulário adaptável para revisão? Como gerenciar revisões para um formulário adaptável do aem?
description: A revisão é um mecanismo que permite ao revisor executar tarefas diferentes para formulários adaptáveis usando a etapa Atribuir tarefa.
feature: Adaptive Forms
hide: true
hidefromtoc: true
role: User
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---


# Criar e gerenciar revisões para um Formulário adaptável {#review-step-forms-aem-sites-page}

Usando a [Etapa de atribuição](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?lang=pt-BR#assign-task-step) do fluxo de trabalho do AEM, o revisor revisa o formulário enviado e executa a ação nele. Para revisar o formulário enviado usando a etapa Atribuir tarefa, siga estas etapas:

1. [Criar um fluxo de trabalho do AEM](#create-an-aem-workflow)
1. [Configurar a ação de envio do contêiner de Formulário adaptável](#configure-submit-action)
1. [Enviar um formulário adaptável após a revisão](#submit-af-after-review)

## Criar um fluxo de trabalho do AEM {#create-an-aem-workflow}

1. Abra a instância do autor no modo de edição.
1. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]** > **[!UICONTROL Criar]** > **[!UICONTROL Criar Modelo]**
1. Especifique o Título do fluxo de trabalho e adicione a etapa **[Atribuir tarefa]**
1. Selecione ![settings_icon](assets/settings_icon.png) na barra de ações. A caixa de diálogo **[!UICONTROL Atribuir tarefa]** é aberta.
1. Abra a guia [!UICONTROL Formulário e Documento], abra o menu suspenso [!UICONTROL Pré-preenchido] e especifique:

   * Selecione o arquivo de dados de entrada usando
   * Selecione os anexos de entrada usando

   ![Etapa de revisão](/help/forms/assets/assigntask-review1.gif)

1. Abra a guia **[!UICONTROL Destinatário]**, abra o menu suspenso [!UICONTROL Pré-preenchido] e especifique **[!UICONTROL Opções de atribuição]**:

   ![Etapa de revisão](/help/forms/assets/review-assignstep.png)

1. Clique em **[!UICONTROL Concluído]** para salvar as alterações.

## Configurar ação de envio {#configure-submit-action}

Agora, configure a ação Enviar de um componente de Contêiner de formulário adaptável na página do site:

1. Vá para a página do site.
1. Selecione ![settings_icon](assets/settings_icon.png) de um contêiner de Formulário adaptável. A caixa de diálogo **[!UICONTROL Contêiner de formulário adaptável]** é aberta.
1. Abra a guia **[!UICONTROL Envio]** e especifique **[!UICONTROL Enviar Ação]** para [Invocar um fluxo de trabalho do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=pt-BR#invoke-an-aem-workflow)

1. Clique em [Concluído] para salvar as configurações.

![submissiontab-reviewstep](/help/forms/assets/submissiontab-reviewstep.gif)

## Enviar um formulário adaptável após revisão {#submit-af-after-review}

Para revisar e confirmar o Formulário adaptável enviado:

1. Ir para [!UICONTROL Ferramentas] > [!UICONTROL Fluxo de Trabalho] > [!UICONTROL Instâncias]
1. Na Caixa de entrada, é possível ver que uma instância está sendo criada.
1. Selecione a instância e clique em [!UICONTROL Abrir].
1. Agora é possível ver o formulário enviado.

O revisor executa ações diferentes, pois:

* **Enviar**: o revisor conclui o formulário e o envia para processamento adicional.
* **Salvar**: o revisor salva o formulário em seu estado atual sem enviá-lo.
* **Redefinir**: o revisor apaga todas as alterações feitas no formulário e o restaura ao seu estado original.
* **Delegar**: o revisor transfere a propriedade do formulário para outra pessoa para outras ações ou revisões.
