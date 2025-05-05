---
Title: How to integrate AEM workflow with an Adaptive Form?
Description: Explore the process of automated workflow initiation with AEM Forms Submit Action.
keywords: Fluxo de trabalho do AEM, Integrar formulário adaptável ao fluxo de trabalho do AEM, Chamar ação de envio do fluxo de trabalho do AEM
feature: Adaptive Forms, Core Components
exl-id: b7788e3d-acd8-4867-b232-f9767cf6b2f5
title: Como configurar uma ação enviar para um formulário adaptável?
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# Integrar o formulário adaptável de AEM ao fluxo de trabalho de AEM: simplificando os processos de negócios

A Ação de Envio **[!UICONTROL Chamar um Fluxo de Trabalho de AEM]** associa um Formulário adaptável a um Fluxo de Trabalho de AEM. Quando um formulário é enviado, o fluxo de trabalho associado é iniciado automaticamente na instância do Autor. É possível salvar os arquivos de dados, anexos e Documentos de Registro no local da carga útil do fluxo de trabalho ou em uma variável. Se o workflow estiver marcado para armazenamento de dados externo e configurado para um armazenamento de dados externo, então somente a opção de variável estará disponível. É possível selecionar na lista de variáveis disponíveis para o modelo de fluxo de trabalho. Se o workflow estiver marcado para armazenamento de dados externo em um estágio posterior e não no momento da criação do workflow, verifique se as configurações de variável necessárias estão em vigor.

>[!NOTE]
>
>  Saiba como [criar um modelo de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=pt-BR#extending-aem) para definir a série de etapas executadas quando um usuário inicia o fluxo de trabalho. Você também pode definir propriedades do modelo, como se o fluxo de trabalho é transitório ou usa vários recursos.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md).

## Vantagens

Algumas das vantagens de integrar o fluxo de trabalho do AEM ao Adaptive Forms são:

* A integração do fluxo de trabalho AEM permite a automação de processos comerciais complexos que envolvem envios de formulários.
* O fluxo de trabalho do AEM suporta lógica condicional, permitindo assim decisões dinâmicas baseadas em dados de formulário ou fatores externos.
* O fluxo de trabalho do AEM roteia tarefas com base em regras e condições predefinidas, garantindo que as tarefas sejam atribuídas aos indivíduos ou grupos corretos.

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## Integrar o fluxo de trabalho do AEM ao Forms adaptável {#steps-to-integrate-workflow-with-af}

Para configurar o processo automatizado com o [Fluxo de Trabalho do AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=pt-BR#extending-aem) para um Formulário adaptável, execute as seguintes etapas:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique na guia **[!UICONTROL Envio]**.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[!UICONTROL Chamar um Fluxo de Trabalho do AEM]**.
   ![Configuração de ação de Enviar Email](/help/forms/assets/configure-invoke-aem-workflow.png)

1. Selecione o modelo de fluxo de trabalho na lista suspensa **[!UICONTROL Modelo de fluxo de trabalho]**.
1. Selecione a opção na lista suspensa **[!UICONTROL Armazenar arquivo de dados usando]**.

   **Arquivo de dados**: contém dados enviados para o Formulário adaptável. Você pode usar a opção **[!UICONTROL Caminho do Arquivo de Dados]** para especificar o nome do arquivo e o caminho do arquivo relativo à carga. Por exemplo, o caminho `/addresschange/data.xml` cria uma pasta chamada `addresschange` e a coloca em relação à carga. Você também pode especificar apenas `data.xml` para enviar apenas dados enviados sem criar uma hierarquia de pastas. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

1. Selecione a opção na lista suspensa **[!UICONTROL Armazenar anexos usando]**.

   **Anexos**: você pode usar a opção **[!UICONTROL Caminho do Anexo]** para especificar o nome da pasta para armazenar os anexos carregados no Formulário Adaptável. A pasta é criada em relação à carga útil. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

1. Selecione a opção na lista suspensa **[!UICONTROL Documentos de registro usando]**.

   **Documento de Registro**: contém o Documento de Registro gerado para o Formulário Adaptável. Você pode usar a opção **[!UICONTROL Caminho do Documento de Registro]** para especificar o nome do arquivo do Documento de Registro e o caminho do arquivo relativo à carga útil. Por exemplo, o caminho `/addresschange/DoR.pdf` cria uma pasta chamada `addresschange` relativa à carga e coloca a `DoR.pdf` relativa à carga. Você também pode especificar apenas `DoR.pdf` para salvar apenas o documento de registro sem criar uma hierarquia de pastas. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.
1. Clique em **[!UICONTROL Concluído]**.

>[!NOTE]
>
> Saiba mais sobre os [Fluxos de trabalho AEM centrados no Forms - Referência de etapa para automatizar processos comerciais](/help/forms/aem-forms-workflow-step-reference.md).

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## Artigos relacionados

{{af-submit-action}}
