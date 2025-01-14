---
Title: How to configure Marketo Engage data for Adaptive Forms?
Description: Learn how to use Marketo Engage schema in Adaptive Forms.
Keywords: Use Marketo Engage data source in Adaptive Forms, How to connect a Marketo instance data source with form? , Connect a form to Marketo.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: e46c5afac945620cc44e9064956848acecc786bf
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 6%

---

# Configurar fonte de dados do Marketo Engage para o Adaptive Forms existente

<span class="preview"> O recurso está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

![Fluxo de trabalho](/help/forms/assets/workflow-marketo-2.png)

Depois de criar a configuração do Cloud Service para integrar o Marketo Engage com o AEM Forms existente, você pode configurar a fonte de dados para formulários.

A configuração da integração de dados permite que os usuários se conectem a várias fontes de dados ou esquemas. Integrar com a fonte de dados do Marketo Engage e usá-la em diferentes formulários facilita as operações nesses dados. Para explorar as fontes de dados prontas para uso com suporte para um Formulário adaptável, consulte o artigo [Configurar fontes de dados](/help/forms/configure-data-sources.md).

## Considerações sobre a configuração da fonte de dados do Marketo Engage para formulários

Considerações ao configurar a fonte de dados do Marketo Engage para formulários são:

* Não é possível conectar o Edge Delivery Services Forms com o Marketo Engage.

## Pré-requisito para usar a fonte de dados do Marketo Engage para formulários

Pré-requisito para usar a fonte de dados do Marketo Engage com formulários:

* Crie a [configuração do Cloud Service para integrar o Marketo Engage aos formulários](/help/forms/integrate-form-to-marketo-engage.md).

## Como configurar o formulário adaptável existente para a fonte de dados Marketo Engage?

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

Para configurar um Formulário adaptável com a fonte de dados Marketo Engage, execute as seguintes etapas:
1. Faça logon na sua instância de Autor do [!DNL Experience Manager Forms].

2. Abra o Formulário adaptável para edição.
3. Abra a Árvore de conteúdo e selecione o **[!UICONTROL Contêiner do guia]**.
4. Clique no ícone de propriedades do Contêiner de formulário adaptável ![propriedades do Contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável para configurar a fonte de dados é aberta.
5. Abra a guia **[!UICONTROL Modelo de Dados]** e selecione um modelo de formulário como **Conector**.
6. Selecione o **[!UICONTROL Conector]** na lista suspensa.

7. Depois de selecionar o **[!UICONTROL Conector]**, você pode selecionar a configuração da nuvem.

   ![Selecionar Marketo Connector](/help/forms/assets/select-marketo-connector.png)

   Com base na configuração de Marketo Engage selecionada, os elementos de formulário são exibidos na guia **[!UICONTROL Objetos do modelo de dados]** do **[!UICONTROL Navegador de conteúdo]** na barra lateral. Você pode arrastar e soltar esses elementos para criar o Formulário adaptável.

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source.png)

8. Clique em **[!UICONTROL Concluído]**.

Como alternativa, você também pode editar as propriedades do Formulário adaptável para alterar sua configuração associada.

O Formulário adaptável agora está configurado com a fonte de dados da instância de Marketo Engage conectada. Agora, configure-a para enviar dados ao Adobe Marketo Engage.

## Perguntas frequentes

**P: O que acontece quando você altera o conector do formulário?**\
**A:** Se você alterar o conector do formulário, as associações existentes se tornarão inválidas.

**P: Quais são as três operações disponíveis no Serviço de Chamada do Editor de Regras para formulários integrados com o Marketo Engage?**\
**A:** As três operações prontas para uso disponíveis no **Invoke Service** para formulários integrados com Marketo Engage são:
* Sincronizar lead
* Obter lead por ID
* Obter cliente em potencial por tipo de filtro

## Próxima etapa

Agora, você configurou a fonte de dados Marketo Engage para o Adaptive Forms. Em seguida, você pode [configurar um Formulário adaptável para enviar dados ao Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md).

## Artigos relacionados

{{af-submit-action}}

## Consulte também:

{{marketo-engage-see-also}}
