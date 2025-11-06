---
title: Como configurar dados do Marketo Engage para o Adaptive Forms?
description: Saiba como usar o esquema do Marketo Engage no Adaptive Forms.
keywords: Usar a fonte de dados do Marketo Engage no Adaptive Forms, Como conectar uma fonte de dados de instância do Marketo com o formulário? , Conectar um formulário ao Marketo.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 5%

---

# Configurar fonte de dados do Marketo Engage para o Adaptive Forms existente

<span class="preview"> O recurso está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

![Fluxo de trabalho](/help/forms/assets/workflow-marketo-2.png)

Depois de criar a configuração do Cloud Service para integrar o Marketo Engage com o AEM Forms existente, você pode configurar a fonte de dados para formulários.

A configuração da integração de dados permite que os usuários se conectem a várias fontes de dados ou esquemas. Integrar com a fonte de dados do Marketo Engage e usá-la em diferentes formulários facilita as operações nesses dados. Para explorar as fontes de dados prontas para uso com suporte para um Formulário adaptável, consulte o artigo [Configurar fontes de dados](/help/forms/configure-data-sources.md).

## Pré-requisito para usar a fonte de dados do Marketo Engage para formulários

Pré-requisito para usar a fonte de dados do Marketo Engage com formulários:

* Crie a [configuração do Cloud Service para integrar o Marketo Engage com formulários](/help/forms/integrate-form-to-marketo-engage.md).

## Como configurar o formulário adaptável existente para a fonte de dados do Marketo Engage?

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

<span> Este vídeo se aplica somente aos Componentes principais. Para Componentes UE/Foundation, consulte o artigo.</span>

>[!BEGINTABS]

>[!TAB Componente de base]

Para configurar um formulário adaptável com base nos componentes de base com a fonte de dados do Marketo Engage, execute as seguintes etapas:

1. Faça logon na sua instância de Autor do [!DNL Experience Manager Forms].
1. Abra o Formulário adaptável para edição e navegue até a seção **[!UICONTROL Modelo de Dados]** das propriedades do Contêiner de Formulário Adaptável e selecione um modelo de formulário como **Conector**.
1. Selecione o **[!UICONTROL Conector]** na lista suspensa.
1. Depois de selecionar o **[!UICONTROL Conector]**, você pode selecionar a configuração da nuvem.

   ![Selecionar Marketo Connector](/help/forms/assets/select-marketo-connector-af1.png){width=50%, height=50%}

   Com base na configuração selecionada do Marketo Engage, os elementos de formulário são exibidos na guia **[!UICONTROL Objetos do Modelo de Dados]** do **[!UICONTROL Navegador de Conteúdo]** na barra lateral. Você pode arrastar e soltar esses elementos para criar o Formulário adaptável.

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-af1.png){width=50%, height=50%}

1. Clique em **[!UICONTROL Concluído]**.

Como alternativa, você também pode editar as propriedades do Formulário adaptável para alterar sua configuração associada.

O Formulário adaptável agora está configurado com a fonte de dados da instância conectada do Marketo Engage. Agora, configure-a para enviar dados ao Adobe Marketo Engage.

>[!TAB Componente principal]

Para configurar um formulário adaptável com base nos Componentes principais com a fonte de dados do Marketo Engage, execute as seguintes etapas:

1. Faça logon na sua instância de Autor do [!DNL Experience Manager Forms].

1. Abra o Formulário adaptável para edição.
1. Abra a Árvore de conteúdo e selecione o **[!UICONTROL Contêiner do guia]**.
1. Clique no ícone de propriedades do Contêiner de formulário adaptável ![propriedades do Contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável para configurar a fonte de dados é aberta.
1. Abra a guia **[!UICONTROL Modelo de Dados]** e selecione um modelo de formulário como **Conector**.
1. Selecione o **[!UICONTROL Conector]** na lista suspensa.

1. Depois de selecionar o **[!UICONTROL Conector]**, você pode selecionar a configuração da nuvem.

   ![Selecionar Marketo Connector](/help/forms/assets/select-marketo-connector.png){width=50%, height=50%}

   Com base na configuração selecionada do Marketo Engage, os elementos de formulário são exibidos na guia **[!UICONTROL Objetos do Modelo de Dados]** do **[!UICONTROL Navegador de Conteúdo]** na barra lateral. Você pode arrastar e soltar esses elementos para criar o Formulário adaptável.

   ![Marketo Data Source](/help/forms/assets/marketo-engage-data-source.png){width=50%, height=50%}

1. Clique em **[!UICONTROL Concluído]**.

Como alternativa, você também pode editar as propriedades do Formulário adaptável para alterar sua configuração associada.

O Formulário adaptável agora está configurado com a fonte de dados da instância conectada do Marketo Engage. Agora, configure-a para enviar dados ao Adobe Marketo Engage.

>[!TAB Universal Editor]

Para configurar um Formulário adaptável criado no Universal Editor com a fonte de dados do Marketo Engage, execute as seguintes etapas:

1. Abra as propriedades do formulário para edição.
1. Selecione o **[!UICONTROL Modelo de formulário]**.
1. Selecione **Conector** do **[!UICONTROL Modelo de formulário]**.
1. Depois de selecionar o **[!UICONTROL Conector]**, você pode selecionar a configuração da nuvem.

   ![Selecionar Marketo Connector](/help/forms/assets/select-marketo-connector-ue.png)

1. Clique em **[!UICONTROL Salvar e fechar]**.

Com base na configuração selecionada do Marketo Engage, os elementos de formulário são exibidos na guia **[!UICONTROL Fonte de Dados]** do Navegador de Conteúdo no Painel Propriedades. Você pode arrastar e soltar esses elementos para criar o Formulário adaptável.

![Marketo Data Source](/help/forms/assets/marketo-engage-data-source-ue.png)

O formulário agora está configurado com a fonte de dados da instância conectada do Marketo Engage. Agora, configure-a para enviar dados ao Adobe Marketo Engage.

>[!ENDTABS]

## Perguntas frequentes

**P: O que acontece quando você altera o conector do formulário?**\
**A:** Se você alterar o conector do formulário, as associações existentes se tornarão inválidas.

**P: Quais são as três operações disponíveis no Serviço de Chamada do Editor de Regras para formulários integrados com o Marketo Engage?**

**A:** As três operações prontas para uso disponíveis no **Invoke Service** para formulários integrados com o Marketo Engage são:

* Sincronizar lead
* Obter lead por ID
* Obter cliente em potencial por tipo de filtro

## Próxima etapa

Agora, você configurou a fonte de dados do Marketo Engage para o Adaptive Forms. Em seguida, você pode [configurar um Formulário adaptável para enviar dados ao Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md).

## Artigos relacionados

{{af-submit-action}}

## Consulte também:

{{marketo-engage-see-also}}
