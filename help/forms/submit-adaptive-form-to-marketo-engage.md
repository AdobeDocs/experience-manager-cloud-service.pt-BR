---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: ce4646d8db1870f8ec85faddeb4e0a6a04f4c46e
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 5%

---

# Configurar a ação de envio para o Marketo Engage para formulários existentes

<span class="preview"> O recurso está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

![Fluxo de trabalho](/help/forms/assets/workflow-marketo-3.png)

O editor Adaptive Forms fornece a ação de envio **Enviar para o Marketo Engage** para enviar dados Adaptive Forms ao Adobe Marketo Engage para processamento. Você pode configurar um Formulário adaptável existente para enviar dados ao [Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home) no envio.

Várias ações de envio prontas para uso para manipular envios de formulários estão disponíveis. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md).

## Consideração ao configurar a ação de envio ao Marketo Engage para o formulário

* Verifique se o Formulário adaptável está configurado com a fonte de dados do Marketo Engage para enviar dados para o Marketo Engage no envio do formulário. No entanto, você pode alterar a ação de envio para alternativas, por exemplo, **Enviar para o OneDrive** ou **Enviar para o SharePoint**, mesmo se o formulário estiver configurado com o esquema de dados do Marketo Engage.

## Pré-requisito para configurar a ação de envio no Marketo Engage para o formulário existente

Pré-requisito para configurar a ação de envio para o Marketo Engage:

* Configure a [fonte de dados do Marketo Engage para o Formulário adaptável](/help/forms/use-marketo-engage-data-source-in-form.md) e associe os elementos de formulário aos campos do Marketo Engage.

## Como configurar a ação de envio para o Marketo Engage para formulários existentes?

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

>[!BEGINTABS]

>[!TAB Componente de base]

Você pode configurar a ação de envio de um Formulário adaptável com base nos Componentes de base para enviar dados ao Adobe Marketo Engage. Para configurar a ação de envio para o Marketo Engage, execute as seguintes etapas:

1. Faça logon na sua instância de Autor do [!DNL Experience Manager Forms].
1. Abra o Formulário adaptável para edição e navegue até a seção **[!UICONTROL Envio]** das propriedades do Contêiner de formulário adaptável e selecione uma ação de envio como **Enviar para o Marketo Engage**.
1. Clique em **[!UICONTROL Concluído]**.

![Ação de envio do Marketo](/help/forms/assets/marketo-engage-submit-action-af.png){width=50%, height=50%}

Depois de configurar a ação de envio para o Formulário adaptável como **Enviar para o Marketo Engage**, você pode enviar dados para o Adobe Marketo Engage para processamento. Os dados podem ser usados para analisar e otimizar campanhas de marketing, automatizar emails de acompanhamento e acionar workflows com base em envios de formulários.

>[!TAB Componente principal]

Você pode configurar a ação de envio de um Formulário adaptável com base nos Componentes principais para enviar dados ao Adobe Marketo Engage. Para configurar a ação de envio para o Marketo Engage, execute as seguintes etapas:

1. Abra o Formulário adaptável para edição.
1. Abra a Árvore de conteúdo e selecione o **[!UICONTROL Contêiner do guia]**.
1. Clique no ícone de propriedades do Contêiner de formulário adaptável ![propriedades do Contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável para configurar a ação de envio é aberta.
1. Abra a guia **[!UICONTROL Envio]** e selecione uma ação de envio como **Enviar para o Marketo Engage**.
1. Clique em **[!UICONTROL Concluído]**.

![Ação de envio do Marketo](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}

Depois de configurar a ação de envio para o Formulário adaptável como **Enviar para o Marketo Engage**, você pode enviar dados para o Adobe Marketo Engage para processamento. Os dados podem ser usados para analisar e otimizar campanhas de marketing, automatizar emails de acompanhamento e acionar workflows com base em envios de formulários.

>[!TAB Editor Universal]

Você pode configurar a ação de envio de um Formulário adaptável criado no Universal Editor para enviar dados ao Adobe Marketo Engage. Para configurar a ação de envio para o Marketo Engage, execute as seguintes etapas:

1. Abra o Formulário adaptável para edição.
1. Clique na extensão **Editar propriedades do formulário** no editor.
A caixa de diálogo **Propriedades do Formulário** é exibida.

   >[!NOTE]
   >
   > * Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
   > * Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.

1. Clique na guia **Envio** e selecione a ação de envio **[!UICONTROL Enviar para o Marketo Engage]**.

   ![Ação de envio do Marketo](/help/forms/assets/marketo-engage-submit-action-ue.png)

1. Clique em **[!UICONTROL Salvar e fechar]**.

Depois de configurar a ação de envio para o Formulário adaptável como **Enviar para o Marketo Engage**, você pode enviar dados para o Adobe Marketo Engage para processamento. Os dados podem ser usados para analisar e otimizar campanhas de marketing, automatizar emails de acompanhamento e acionar workflows com base em envios de formulários.

>[!ENDTABS]

## Perguntas frequentes

**P: É possível alterar a ação de envio para formulários configurados para se conectarem ao esquema do Marketo Engage?**
**A:** Por padrão, a ação **Enviar para o Marketo** é selecionada quando um formulário é configurado para se conectar ao esquema do Marketo Engage. No entanto, você pode alterar a ação de envio dos formulários, se necessário.

## Próxima etapa

Você também pode conectar um Formulário adaptável à [biblioteca do Munchkin](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin) para rastrear o número de visitas, cliques e envios de formulários.

## Artigos relacionados

{{af-submit-action}}

## Consulte também:

{{marketo-engage-see-also}}
