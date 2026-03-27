---
title: Fluxo de trabalho de envio para interface do usuário associada — IC Generate PDF Output
description: Entenda como o envio e o fluxo de trabalho funcionam para a Interface do usuário associada e siga um exemplo de fluxo de trabalho que gera o PDF a partir do JSON de IC (Comunicação interativa).
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: a1b2c3d4-e5f6-4a7b-8c9d-0e1f2a3b4c5d
source-git-commit: a41459520feb03594212b91e68cfd8e2b1e610c4
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Fluxo de trabalho de envio para Associar interface

>[!NOTE]
>
> O recurso de comunicação interativa está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

Este artigo explica como o envio e o fluxo de trabalho funcionam quando você habilita um fluxo de trabalho para a Interface do usuário associada. Em seguida, ele mostra como configurar um fluxo de trabalho de envio. A apresentação usa como exemplo a geração de um PDF a partir da carga da IC (Comunicação interativa); você pode adaptar as etapas para outros tipos de fluxo de trabalho.

<!--## Submission and workflow behavior {#submission-and-workflow-behavior}

When you enable **Configure Workflow for Update** for an Associate UI, submissions from the Associate UI can trigger an AEM workflow. The following explains where workflows run, who uses which environment, and how to plan for data and access.

### Where workflows run

AEM workflows always run on the **Author** instance. It does not matter whether the person submitting is an author or an associate—the workflow runs on Author. Plan your user groups and where you store workflow data with this in mind.

### Where associates use the Associate UI

Customer-facing associates use the Associate UI on the **Publish** instance only. You publish the Interactive Communication and expose the Associate UI through your Publish environment (for example, via your application or dispatcher). Associates do not use the Author instance. For step-by-step integration and how to invoke the Associate UI on the Publish instance, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).

### When an author submits from the Author instance

Authors can open the Associate UI on the Author instance—for example, to test the Interactive Communication or to submit on behalf of a customer. When they submit, the request is handled on Author and the workflow runs there. For this to work, the author must be in both **forms-associates** (to access the Associate UI) and **workflow-users** (to run the workflow).

### When an associate submits from the Publish instance

Associates open the Associate UI on the Publish instance, using the integration you set up. When they submit, the submission is sent to the Author instance and the workflow runs on Author. Associates sign in on Publish (for example, via [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) and do not need access to Author. To set up how associates open the Associate UI on Publish, see [Integrate Associate UI in Your Application](/help/forms/interactive-communication/invoke-associate-ui.md).-->

## Configurar um fluxo de trabalho de envio

As etapas a seguir mostram como criar um fluxo de trabalho que é executado quando os usuários enviam a partir da Interface do usuário associada. Aqui usamos **renderização da IC para o PDF** como exemplo, com a etapa **IC Renderização da PDF Output** predefinida. Quando um usuário envia a partir da interface do usuário Associate, a carga é enviada para o fluxo de trabalho. Esta etapa usa o **communicationDom** (IC-JSON) da carga para produzir a PDF.

### Estrutura de carga útil

O workflow recebe uma carga JSON. O campo **communicationDom** contém o IC-JSON usado para geração do PDF. A etapa **IC Renderizar Saída do PDF** a usa como entrada do modelo.

| Texto | Descrição |
|-------|-------------|
| communicationDom | IC-JSON para geração do PDF |
| auditMetadata | Informações de auditoria |
| submitData | Dados de formulário enviados (JSON) |
| prefillData | Preencher dados previamente (JSON) |
| referenciador, cookies, queryString, clientIP, userAgent, formSubmitter | Solicitar metadados |

### Criar o modelo de fluxo de trabalho

1. **Básico**: crie um modelo de fluxo de trabalho (por exemplo, adicione um fluxo de trabalho como **pdfrenderworkflow**).

   ![Guia Básico do modelo de fluxo de trabalho](/help/forms/assets/associate-ui-add-workflow.png)

1. **Variáveis:** adicione variáveis que correspondem à carga e à etapa: **communicationDom** (JSON), **auditMetadata** (JSON), **outputDocument** (Documento).

   ![Variáveis de fluxo de trabalho](/help/forms/assets/associate-ui-add-variables.png)

1. **Etapa:** Adicionar a etapa **IC Renderizar PDF Output**.
   ![Adicionar etapa do fluxo de trabalho](/help/forms/assets/associate-ui-add-step.png)

1. Em sua guia **Input**, defina **Select template (JsonObject)** como **Variable** → **communicationDom**. Salve a etapa e o modelo.

   ![Saída de Renderização de PDF IC — guia Entrada](/help/forms/assets/associate-ui-input-variable.png)

1. Em sua guia **Saída**, defina **Selecionar modelo (JsonObject)** como **Variável** → **communicationDom**. Salve a etapa e o modelo.

   ![Tela e variáveis de fluxo de trabalho](/help/forms/assets/assocaite-ui-output-variable.png)

### Vincular o fluxo de trabalho à interface do usuário associada

Em [Habilitar e configurar a Interface do Usuário Associada](/help/forms/interactive-communication/enable-configure-associate-ui.md), habilite a Exibição Associada e, no **Fluxo de Trabalho**, defina o **Configurar Fluxo de Trabalho para Atualização** como Ativado e selecione este modelo de fluxo de trabalho. Publique a IC e [integre a Interface do Usuário Associada](/help/forms/interactive-communication/invoke-associate-ui.md) para que os envios acionem esse fluxo de trabalho.

![Configurações de Comunicação Interativa - Configuração de fluxo de trabalho para Interface do Usuário Associada](/help/forms/assets/associate-ui-configure-workflow.png)

Quando **Externalizar o armazenamento de dados do fluxo de trabalho** estiver habilitado, configure o externalizador para que os dados do fluxo de trabalho sejam armazenados em seu armazenamento externo (por exemplo, Azure). Consulte [Externalizar dados de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html).

## Consulte também:

- [Associar a interface no Editor de comunicação interativa](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Habilitar e configurar a Interface do Usuário Associada para Comunicações Interativas](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [Integrar a interface do usuário do Associate no seu aplicativo](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Externalizar dados de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/create-aem-workflow/externalize-workflow.html)
