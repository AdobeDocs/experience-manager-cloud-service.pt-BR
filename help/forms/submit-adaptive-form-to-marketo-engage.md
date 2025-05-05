---
Title: How to configure submit action to Marketo Engage for forms?
Description: Learn how to configure the submit action of Adaptive Form to send data to Marketo Engage.
Keywords: Submit data to Marketo engage, Configure submit action as Submit to Marketo Engage
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 0683564b-1ac4-42b4-bc08-101c4fdef286
source-git-commit: e46c5afac945620cc44e9064956848acecc786bf
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 6%

---

# Configurar a ação de envio para o Marketo Engage para formulários existentes

<span class="preview"> O recurso está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

![Fluxo de trabalho](/help/forms/assets/workflow-marketo-3.png)

O editor Adaptive Forms fornece a ação de envio **Enviar para o Marketo Engage** para enviar dados Adaptive Forms ao Adobe Marketo Engage para processamento. Você pode configurar um Formulário adaptável existente para enviar dados ao [Adobe Marketo Engage](https://experienceleague.adobe.com/pt-br/docs/marketo/using/home) no envio.

Várias ações de envio prontas para uso para manipular envios de formulários estão disponíveis. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md).

## Consideração ao configurar a ação de envio para Marketo Engage para o formulário

* Verifique se o Formulário adaptável está configurado com a fonte de dados Marketo Engage para enviar dados para o Marketo Engage no envio do formulário. No entanto, você pode alterar a ação de envio para alternativas, por exemplo, **Enviar para o OneDrive** ou **Enviar para o SharePoint**, mesmo se o formulário estiver configurado com o esquema de dados Marketo Engage.

## Pré-requisito para configurar a ação de envio para o Marketo Engage para o formulário existente

Pré-requisito para configurar a ação de envio no Marketo Engage:

* Configure a fonte de dados [Marketo Engage para o Formulário adaptável](/help/forms/use-marketo-engage-data-source-in-form.md) e associe os elementos de formulário com campos Marketo Engage.

## Como configurar a ação de envio para o Marketo Engage para formulários existentes?

>[!VIDEO](https://video.tv.adobe.com/v/3442866/submit-action-marketo-engage-marketo-aem-aem-forms-engage)

Você pode configurar a ação de envio de um Formulário adaptável para enviar dados ao Adobe Marketo Engage. Para configurar a ação de envio para o Marketo Engage, execute as seguintes etapas:

1. Abra o Formulário adaptável para edição.
2. Abra a Árvore de conteúdo e selecione o **[!UICONTROL Contêiner do guia]**.
3. Clique no ícone de propriedades do Contêiner de formulário adaptável ![propriedades do Contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável para configurar a ação de envio é aberta.
4. Abra a guia **[!UICONTROL Envio]** e selecione uma ação de envio como **Enviar para o Marketo Engage**.
5. Clique em **[!UICONTROL Concluído]**.

![Ação de envio do Marketo](/help/forms/assets/marketo-engage-submit-action.png){width=50%, height=50%}


Após configurar a ação de envio para o Formulário adaptável como **Enviar para o Marketo Engage**, você pode enviar dados para o Adobe Marketo Engage para processamento. Os dados podem ser usados para analisar e otimizar campanhas de marketing, automatizar emails de acompanhamento e acionar workflows com base em envios de formulários.

## Perguntas frequentes

**P: É possível alterar a ação de envio para formulários configurados para se conectarem ao esquema Marketo Engage?**
**A:** Por padrão, a ação **Enviar para o Marketo** é selecionada quando um formulário é configurado para se conectar ao esquema Marketo Engage. No entanto, você pode alterar a ação de envio dos formulários, se necessário.

## Próxima etapa

Você também pode conectar um Formulário adaptável à [biblioteca do Munchkin](https://experienceleague.adobe.com/pt-br/docs/marketo/using/product-docs/administration/setup/munchkin) para rastrear o número de visitas, cliques e envios de formulários.

## Artigos relacionados

{{af-submit-action}}

## Consulte também:

{{marketo-engage-see-also}}
