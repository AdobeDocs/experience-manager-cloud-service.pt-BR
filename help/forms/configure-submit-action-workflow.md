---
Title: How to integrate AEM workflow with an Adaptive Form?
Description: Explore the process of automated workflow initiation with AEM Forms Submit Action.
keywords: Fluxo de trabalho do AEM, Integrar formulário adaptável ao fluxo de trabalho do AEM, Chamar ação de envio do fluxo de trabalho do AEM
feature: Adaptive Forms, Core Components
source-git-commit: 95af49839d206f67ac02116730229f5b0531c5bb
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---


# Integrar o formulário adaptável de AEM ao fluxo de trabalho de AEM: simplificando os processos de negócios

A variável **[!UICONTROL Chamar um fluxo de trabalho de AEM]** A ação enviar associa um formulário adaptável a um fluxo de trabalho de AEM. Quando um formulário é enviado, o fluxo de trabalho associado é iniciado automaticamente na instância do Autor. É possível salvar os arquivos de dados, anexos e Documentos de Registro no local da carga útil do fluxo de trabalho ou em uma variável. Se o workflow estiver marcado para armazenamento de dados externo e configurado para um armazenamento de dados externo, então somente a opção de variável estará disponível. É possível selecionar na lista de variáveis disponíveis para o modelo de fluxo de trabalho. Se o workflow estiver marcado para armazenamento de dados externo em um estágio posterior e não no momento da criação do workflow, verifique se as configurações de variável necessárias estão em vigor.

>[!NOTE]
>
>  Saiba como [criar um modelo de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem) para definir a série de etapas executadas quando um usuário inicia o workflow. Você também pode definir propriedades do modelo, como se o fluxo de trabalho é transitório ou usa vários recursos.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções na [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md)  artigo.

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

Para configurar o processo automatizado com o [Fluxo de trabalho do AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem) para um Formulário adaptável, execute as seguintes etapas:

1. Abra o Navegador de conteúdo e selecione a variável **[!UICONTROL Contêiner do guia]** componente do seu Formulário adaptável.
1. Clique nas propriedades do Container do guia ![Propriedades do guia](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique em  **[!UICONTROL Envio]** guia.
1. No **[!UICONTROL Ação de envio]** selecione **[!UICONTROL Chamar um fluxo de trabalho de AEM]** .
   ![Configuração de ação de Enviar email](/help/forms/assets/configure-invoke-aem-workflow.png)

1. Selecione o modelo de fluxo de trabalho na **[!UICONTROL Modelo de fluxo de trabalho]** lista suspensa.
1. Selecione a opção no **[!UICONTROL Armazenar arquivo de dados usando]** lista suspensa.

   **Arquivo de dados**: contém dados enviados para o Formulário adaptável. Você pode usar o **[!UICONTROL Caminho do arquivo de dados]** opção para especificar o nome do arquivo e o caminho do arquivo relativo à carga útil. Por exemplo, a variável `/addresschange/data.xml` caminho cria uma pasta chamada `addresschange` e o coloca em relação à carga útil. Também é possível especificar somente `data.xml` para enviar somente dados enviados sem criar uma hierarquia de pastas. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

1. Selecione a opção no **[!UICONTROL Armazenar anexos usando]** lista suspensa.

   **Anexos**: Você pode usar o **[!UICONTROL Caminho do anexo]** opção para especificar o nome da pasta para armazenar os anexos carregados no Formulário adaptável. A pasta é criada em relação à carga útil. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

1. Selecione a opção no **[!UICONTROL Documentos de registro usando]** lista suspensa.

   **Documento do registro**: contém o Documento de registro gerado para o Formulário adaptável. Você pode usar o **[!UICONTROL Caminho do documento de registro]** opção para especificar o nome do documento de registro e o caminho do arquivo relativo à carga útil. Por exemplo, a variável `/addresschange/DoR.pdf` caminho cria uma pasta chamada `addresschange` relativo à carga útil e coloca o `DoR.pdf` em relação à carga útil. Também é possível especificar somente `DoR.pdf` para salvar somente o Documento de registro sem criar uma hierarquia de pastas. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.
1. Clique em **[!UICONTROL Concluído]**.

>[!NOTE]
>
> Saiba mais sobre [Workflows AEM centrados na Forms - referência de etapa para automatizar processos de negócios](/help/forms/aem-forms-workflow-step-reference.md).

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## Artigos relacionados

{{af-submit-action}}