---
Title: How to integrate Marketo Engage with AEM Forms using Form wizard?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms using form wizard.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 1fcba628-ffd8-416a-a8b5-76b35d4aabd4
source-git-commit: ce4646d8db1870f8ec85faddeb4e0a6a04f4c46e
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 4%

---

# Integrar um formulário adaptável ao Marketo Engage

<span class="preview"> O recurso está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

![Fluxo de trabalho](/help/forms/assets/workflow-marketo-4.png)

Depois de criar a configuração do serviço de nuvem para integrar o Marketo Engage com o AEM Forms, você pode configurar um Formulário adaptável para integrar com o [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home).

É possível conectar o Marketo Engage a um formulário adaptável usando o assistente de formulários, que simplifica o processo de configuração orientando você em cada etapa. Ele inclui a seleção de modelos, estilos e campos de dados, bem como a configuração do mapeamento de dados para garantir que o formulário esteja pronto para se comunicar com o Marketo Engage após a criação. Usando o assistente de formulário, você também pode configurar o Formulário adaptável para enviar dados diretamente para o Adobe Marketo Engage no envio.

## Considerações sobre a configuração da fonte de dados do Marketo Engage para formulários

Considerações ao configurar a fonte de dados do Marketo Engage para formulários são:

* Não é possível conectar o Edge Delivery Services Forms ao Marketo Engage.

## Pré-requisito para conectar o Marketo Engage com formulários

Pré-requisito para conectar o Marketo Engage com formulários:

* Crie a [configuração do Cloud Service para integrar o Marketo Engage com formulários](/help/forms/integrate-form-to-marketo-engage.md).

## Como configurar o novo Formulário adaptável para integrar com o Marketo Engage?

>[!VIDEO](https://video.tv.adobe.com/v/3442867/marketo-aem-marketo-engage-engage-aem-forms)

>[!BEGINTABS]

>[!TAB Componente de base]

Para configurar o novo Formulário adaptável com base nos Componentes de base para integrar com o Marketo Engage, execute as seguintes etapas:

1. Selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

   ![Selecionar Forms e Documentos](/help/forms/assets/select-forms.png)

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O assistente de criação de formulários é aberto.

   ![Selecionar AF](/help/forms/assets/select-create-forms.png)

1. Na guia **[!UICONTROL Source]**, selecione um modelo

   ![Selecionar Modelos](/help/forms/assets/select-template-af1.png)

1. No **[!UICONTROL Estilo]**, selecione o tema.

   ![Selecionar tema](/help/forms/assets/select-form-theme-af1.png)
1. Na guia **[!UICONTROL Dados]**, selecione um modelo de dados como **Marketo Engage**.
1. Selecione a **[!UICONTROL Configuração da nuvem]** na lista suspensa que aparece no painel direito da tela.
Por padrão, todos os campos da configuração associada são exibidos. O assistente oferece a conveniência de permitir que você escolha seletivamente quais campos devem ser incluídos no Formulário adaptável usando caixas de seleção.

   ![Selecionar modelo de dados](/help/forms/assets/select-marketo-data-af1.png)

1. Na guia **[!UICONTROL Envio]**, selecione a ação de envio como **[!UICONTROL Enviar para o Marketo]**.

   Ao selecionar o modelo de dados como **Marketo Engage**, a ação de envio como **Enviar para o Marketo** será selecionada automaticamente. Você pode selecionar uma ação de envio diferente da guia **[!UICONTROL Envio]**. A guia **[!UICONTROL Envio]** exibe todas as ações de envio disponíveis.

   ![Enviar para o envolvimento da Marketo](/help/forms/assets/select-marketo-engage.png)

1. Selecione **[!UICONTROL Criar]**. Especifique o título, o nome e o local para salvar o Formulário adaptável.

   ![Criar formulário](/help/forms/assets/create-marketo-form.png)

1. Selecione **[!UICONTROL Criar]**.

O Formulário adaptável agora está configurado para se conectar com a instância do Marketo Engage. Como alternativa, você também pode editar as propriedades do Formulário adaptável para alterar sua configuração associada

>[!TAB Componente principal]

Para configurar o novo Formulário adaptável com base nos Componentes principais para integrar com o Marketo Engage, execute as seguintes etapas:

1. Selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

   ![Selecionar Forms e Documentos](/help/forms/assets/select-forms.png)

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O assistente de criação de formulários é aberto.

   ![Selecionar AF](/help/forms/assets/select-create-forms.png)

1. Na guia **[!UICONTROL Source]**, selecione um modelo

   ![Selecionar Modelos](/help/forms/assets/select-template.png)

1. No **[!UICONTROL Estilo]**, selecione o tema.

   ![Selecionar tema](/help/forms/assets/select-form-theme.png)


1. Na guia **[!UICONTROL Dados]**, selecione um modelo de dados como **Marketo Engage**.

1. Selecione a **[!UICONTROL Configuração da nuvem]** na lista suspensa que aparece no painel direito da tela.
Por padrão, todos os campos da configuração associada são exibidos. O assistente oferece a conveniência de permitir que você escolha seletivamente quais campos devem ser incluídos no Formulário adaptável usando caixas de seleção.

   ![Selecionar modelo de dados](/help/forms/assets/select-marketo-data.png)

1. Na guia **[!UICONTROL Envio]**, selecione a ação de envio como **[!UICONTROL Enviar para o Marketo]**.

   Ao selecionar o modelo de dados como **Marketo Engage**, a ação de envio como **Enviar para o Marketo** será selecionada automaticamente. Você pode selecionar uma ação de envio diferente da guia **[!UICONTROL Envio]**. A guia **[!UICONTROL Envio]** exibe todas as ações de envio disponíveis.

   ![Enviar para o envolvimento da Marketo](/help/forms/assets/select-marketo-engage.png)

1. Selecione **[!UICONTROL Criar]**. Especifique o título, o nome e o local para salvar o Formulário adaptável.

   ![Criar formulário](/help/forms/assets/create-marketo-form.png)

1. Selecione **[!UICONTROL Criar]**.

O Formulário adaptável agora está configurado para se conectar com a instância do Marketo Engage. Como alternativa, você também pode editar as propriedades do Formulário adaptável para alterar sua configuração associada.

>[!TAB Editor Universal]

Para configurar o novo Formulário adaptável criado no Editor universal para integração com o Marketo Engage, execute as seguintes etapas:

1. Selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

   ![Selecionar Forms e Documentos](/help/forms/assets/select-forms.png)

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O assistente de criação de formulários é aberto.

   ![Selecionar AF](/help/forms/assets/select-create-forms.png)

1. Na guia **[!UICONTROL Source]**, selecione um modelo

   ![Selecionar Modelos](/help/forms/assets/select-template-ue.png)

1. Na guia **[!UICONTROL Dados]**, selecione um modelo de dados como **Marketo Engage**.

1. Selecione a **[!UICONTROL Configuração da nuvem]** na lista suspensa que aparece no painel direito da tela.
Por padrão, todos os campos da configuração associada são exibidos. O assistente oferece a conveniência de permitir que você escolha seletivamente quais campos devem ser incluídos no Formulário adaptável usando caixas de seleção.

   ![Selecionar modelo de dados](/help/forms/assets/select-marketo-data-ue.png)

1. Na guia **[!UICONTROL Envio]**, selecione a ação de envio como **[!UICONTROL Enviar para o Marketo]**.

   Ao selecionar o modelo de dados como **Marketo Engage**, a ação de envio como **Enviar para o Marketo** será selecionada automaticamente. Você pode selecionar uma ação de envio diferente da guia **[!UICONTROL Envio]**. A guia **[!UICONTROL Envio]** exibe todas as ações de envio disponíveis.

   ![Enviar para o envolvimento da Marketo](/help/forms/assets/select-marketo-engage-ue.png)

1. Selecione **[!UICONTROL Criar]**. Especifique o título, o nome e o local para salvar o Formulário adaptável.

   ![Criar formulário](/help/forms/assets/create-marketo-form.png)

1. Selecione **[!UICONTROL Criar]**.

O Formulário adaptável agora está configurado para se conectar com a instância do Marketo Engage. Como alternativa, você também pode editar as propriedades do Formulário adaptável para alterar sua configuração associada.

>[!ENDTABS]

## Perguntas frequentes

**P: É possível alterar a ação de envio para formulários configurados para se conectarem ao esquema do Marketo Engage?**
**A:** Por padrão, a ação **Enviar para o Marketo** é selecionada quando um formulário é configurado para se conectar ao esquema do Marketo Engage. No entanto, você pode alterar a ação de envio dos formulários, se necessário.


**P: O que acontece quando você altera o conector do formulário?**\
**A:** Se você alterar o conector do formulário, as associações existentes se tornarão inválidas.

**P: Quais são as três operações disponíveis no Serviço de Chamada do Editor de Regras para formulários integrados com o Marketo Engage?**\
**A:** As três operações prontas para uso disponíveis no **Invoke Service** para formulários integrados com o Marketo Engage são:

* Sincronizar lead
* Obter lead por ID
* Obter cliente em potencial por tipo de filtro

## Próxima etapa

Você também pode conectar um Formulário adaptável à [biblioteca do Munchkin](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin) para rastrear o número de visitas, cliques e envios de formulários.

## Artigos relacionados

{{af-submit-action}}

## Consulte também:

{{marketo-engage-see-also}}
