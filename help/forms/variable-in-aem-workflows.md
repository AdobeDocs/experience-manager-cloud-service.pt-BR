---
title: Como adicionar variáveis nas etapas do fluxo de trabalho do AEM?
description: Saiba como criar uma variável, definir um valor para a variável e usá-lo no [!DNL AEM Forms] Etapas do workflow.
exl-id: d9139ea9-2f86-476c-8767-b36766790f2c
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2060'
ht-degree: 0%

---

# Variáveis em fluxos de trabalho AEM centrados no Forms {#variables-in-aem-forms-workflows}

Uma variável em um modelo de fluxo de trabalho é uma maneira de armazenar um valor com base em seu tipo de dados. É possível usar o nome da variável em qualquer etapa do fluxo de trabalho para recuperar o valor armazenado na variável. Você também pode usar nomes de variáveis para definir expressões para tomar decisões de roteamento.

Em modelos de fluxo de trabalho do AEM, é possível:

* [Criar uma variável](variable-in-aem-workflows.md#create-a-variable) de um tipo de dados com base no tipo de informações que você deseja armazenar nele.
* [Definir um valor para a variável](variable-in-aem-workflows.md#set-a-variable) usando a etapa de fluxo de trabalho Definir variável.
* [Usar a variável](variable-in-aem-workflows.md#use-a-variable) em todos [!DNL AEM Forms] Etapas do workflow para recuperar o valor armazenado e as etapas OU Split e Goto para definir uma expressão de roteamento.

O vídeo a seguir demonstra como criar, definir e usar variáveis em modelos de fluxo de trabalho do AEM:

>[!VIDEO](assets/variables_introduction_1_1.mp4)

As variáveis são uma extensão do atual [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interface. Você pode usar [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) no ECMAScript para acessar metadados salvos usando variáveis.

## Criar uma variável {#create-a-variable}

Você cria variáveis usando a seção Variáveis disponível no sidekick do modelo de fluxo de trabalho. As variáveis de fluxo de trabalho do AEM são compatíveis com os seguintes tipos de dados:

* **Tipos de dados primitivos**: Longo, Duplo, Booleano, Data e String
* **Tipos de dados complexos**: [Documento](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html), [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html), [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)e instância do modelo de dados de formulário.

>[!NOTE]
>
>Os fluxos de trabalho são compatíveis apenas com o formato ISO8601 para variáveis do tipo Date.

Use o tipo de dados ArrayList para criar coleções de variáveis. Você pode criar uma variável ArrayList para todos os tipos de dados primitivos e complexos. Por exemplo, crie uma variável ArrayList e selecione String como subtipo para armazenar vários valores de string usando a variável.

Para criar uma variável:

1. Em uma instância do AEM, navegue até Ferramentas ![Ícone de martelo](assets/hammer-icon.svg) > Workflow > Modelos.
1. Toque **[!UICONTROL Criar]** e especifique o título e um nome opcional para o modelo de workflow. Selecione o modelo e toque em **[!UICONTROL Editar]**.
1. Toque no ícone de variáveis disponível no sidekick do modelo de fluxo de trabalho e toque em **[!UICONTROL Adicionar variável]**.

   ![Adicionar variável](assets/variables_add_variable_new.png)

1. Na caixa de diálogo Adicionar variável, especifique o nome e selecione o tipo da variável.
1. Selecione o tipo de dados na **[!UICONTROL Tipo]** e especifique os seguintes valores:

   * Tipo de dados primitivo - Especifique um valor padrão opcional para a variável.
   * JSON ou XML - especifique um caminho de esquema JSON ou XML opcional. O sistema valida o caminho do esquema enquanto mapeia e armazena as propriedades disponíveis nesse esquema para outra variável.
   * Modelo de dados de formulário - especifique um caminho de Modelo de dados de formulário.
   * ArrayList - Especifique um subtipo para a coleção.

1. Especifique uma descrição opcional para a variável e toque em ![done_icon](assets/Smock_Checkmark_18_N.svg) para salvar as alterações. A variável é exibida na lista disponível no painel esquerdo.

Ao criar variáveis, considere as seguintes práticas:

* Crie quantas variáveis um fluxo de trabalho exigir. No entanto, para conservar recursos do banco de dados, use o número mínimo de variáveis necessárias e reutilize variáveis quando possível.
* As variáveis fazem distinção entre maiúsculas e minúsculas. Certifique-se de fazer referência a variáveis usando a mesma capitalização no fluxo de trabalho.
* Evite usar caracteres especiais no nome da variável

## Definir uma variável {#set-a-variable}

Você pode usar a etapa Definir variável para definir o valor de uma variável e a ordem na qual os valores são definidos. A variável é definida na ordem em que os mapeamentos de variável são listados na etapa Definir variável.

As alterações nos valores da variável afetam somente a instância do processo na qual a alteração ocorre. Por exemplo, quando um workflow é iniciado e os dados variáveis são alterados, as alterações afetam somente essa instância do workflow. As alterações não afetam outras instâncias do fluxo de trabalho que foram iniciadas anteriormente ou são iniciadas posteriormente.

Dependendo do tipo de dados da variável, você pode usar as seguintes opções para definir o valor de uma variável:

* **Literal:** Use a opção quando souber o valor exato a ser especificado. Você também pode usar a opção para especificar um JSON no formato de uma string.

* **Expressão:** Use a opção quando o valor a ser usado for calculado com base em uma expressão. A expressão é criada no editor de expressão fornecido.

* **Anotação JSON Dot:** Use a opção para recuperar um valor de uma variável do tipo JSON ou FDM.
* **XPATH:** Use a opção para recuperar um valor de uma variável do tipo XML.

* **Relativo à carga:** Use a opção quando o valor a ser salvo na variável estiver disponível em um caminho relativo à carga.

* **Caminho absoluto:** Use a opção quando o valor a ser salvo na variável estiver disponível em um caminho absoluto.

Você também pode atualizar elementos específicos de uma variável do tipo JSON ou XML usando a notação JSON DOT ou XPATH.

### Adicionar mapeamento entre variáveis {#add-mapping-between-variables}

Para adicionar mapeamento entre variáveis:

1. Na página de edição do fluxo de trabalho, toque no ícone Etapas disponível no sidekick do modelo de fluxo de trabalho.
1. Arraste e solte a variável **[!UICONTROL Definir variável]** etapa para o editor de workflow, toque na etapa e selecione ![configure_icon](assets/Smock_Wrench_18_N.svg) (Configurar).
1. Na caixa de diálogo Definir variável, selecione **[!UICONTROL Mapeamento]** > **[!UICONTROL Adicionar mapeamento]**.
1. No **Mapear variável** , selecione a variável para armazenar dados, selecione o modo de mapeamento e especifique um valor para armazenar na variável. Os modos de mapeamento variam de acordo com o tipo de variável.
1. Mapeie mais variáveis para criar uma expressão significativa. Toque ![done_icon](assets/Smock_Checkmark_18_N.svg) para salvar as alterações.

### Exemplo 1: consultar uma variável XML para definir o valor de uma variável de string {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Selecione uma variável do tipo XML para armazenar um arquivo XML. Consulte a variável XML para definir o valor de uma variável de string para a propriedade disponível no arquivo XML. Uso **Especificar XPATH para a variável XML** para definir a propriedade a ser armazenada na variável da string.

Neste exemplo, selecione um **formdata** Variável XML para armazenar o **cc-app.xml** arquivo. Consulte o **formdata** para definir o valor para a variável **endereço de email** variável de string para armazenar o valor do **emailAddress** propriedade disponível na **cc-app.xml** arquivo.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Definir o valor de uma variável")

### Exemplo 2: usar uma expressão para armazenar valor com base em outras variáveis {#example2}

Use uma expressão para calcular a soma das variáveis e armazenar o resultado em uma variável.

Neste exemplo, use o editor de expressão para definir uma expressão para calcular a soma de **assetscost** e **balanceamount** variáveis e armazenam o resultado em **valor total** variável.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Usar editor de expressão {#use-expression-editor}

Também é possível usar expressões para calcular o valor de uma variável no tempo de execução. As variáveis fornecem um editor de expressão para definir expressões.

Use o editor de expressão para:

* Defina o valor das variáveis usando outras variáveis de fluxo de trabalho, números ou expressões matemáticas.
* Usar variáveis de fluxo de trabalho, string, número ou uma expressão em uma expressão matemática
* Adicione condições para definir valores de variáveis.
* Adicione operadores entre condições.

![Editor de expressão](assets/variables_expression_editor_new.png)

Tem como base o editor de regras do Adaptive Forms com as seguintes alterações. Editor de regras em variáveis:

* Não suporta funções.
* Não fornece uma interface para exibir um resumo das regras
* Não tem editor de código.
* Não suporta a ativação e desativação do valor de um objeto.
* Não suporta a configuração da propriedade de um objeto.
* Não há suporte para a chamada de um serviço Web.

Para obter mais informações, consulte [Editor de regras do Forms adaptável](rule-editor.md).

## Usar uma variável {#use-a-variable}

Você pode usar variáveis para recuperar entradas e saídas ou salvar o resultado de uma etapa. O editor de workflow fornece dois tipos de etapas de workflow:

* Etapas do fluxo de trabalho com suporte para variáveis
* Etapas de fluxo de trabalho sem suporte para variáveis

### Etapas do fluxo de trabalho com suporte para variáveis {#workflow-steps-with-support-for-variables}

A etapa Ir para, OU a etapa Dividir e todas as [!DNL AEM Forms] As etapas de fluxo de trabalho são compatíveis com variáveis.

#### OU Etapa de divisão {#or-split-step}

A divisão OR cria uma divisão no fluxo de trabalho, depois da qual apenas uma ramificação fica ativa. Essa etapa permite introduzir caminhos de processamento condicional no fluxo de trabalho. Adicione etapas do fluxo de trabalho a cada ramificação, conforme necessário.

Você pode definir a expressão de roteamento para uma ramificação usando uma definição de regra, um script ECMA ou um script externo.

Você pode usar variáveis para definir a expressão de roteamento usando o editor de expressão. Para obter mais informações sobre o uso de expressões de roteamento para a etapa de Divisão OR, consulte [OU Etapa de divisão](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem#or-split).

Neste exemplo, antes de definir a expressão de roteamento, use [exemplo 2](variable-in-aem-workflows.md#example2) para definir o valor de **valor total** variável. A ramificação 1 estará ativa se o valor de **valor total** for maior que 50000. Da mesma forma, é possível definir uma regra para tornar a Ramificação 2 ativa se o valor de **valor total** for inferior a 50000.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

Da mesma forma, selecione um caminho de script externo ou especifique o script ECMA para expressões de roteamento para avaliar a ramificação ativa. Toque **[!UICONTROL Renomear ramificação]** para especificar um nome alternativo para a ramificação.

<!-- For more examples, see [Create a workflow model](aem-forms-workflow.md#create-a-workflow-model). -->

#### Etapa Ir para {#go-to-step}

A variável **Etapa Ir para** permite especificar a próxima etapa no modelo de fluxo de trabalho a ser executada, dependendo do resultado de uma expressão de roteamento.

Semelhante à etapa OU Split, você pode definir a expressão de roteamento para a etapa Ir para usando uma definição de regra, um script ECMA ou um script externo.

Você pode usar variáveis para definir a expressão de roteamento usando o editor de expressão. Para obter mais informações sobre o uso de expressões de roteamento para a etapa Ir para, consulte [Etapa Ir para](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem#goto-step).

![Regra Ir para](assets/variables_goto_rule1_new.png)

Neste exemplo, a etapa Ir para especifica Verificar Aplicação de Cartão de Crédito como a próxima etapa se o valor para a **ação realizada** é igual a **Precisa de mais informações**.

Para obter mais exemplos sobre como usar a definição de regra na etapa Ir para, consulte [Simulação de um loop For](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem#simulateforloop).

#### Etapas de fluxo de trabalho centradas na Forms {#forms-workflow-centric-workflow-steps}

Todos [!DNL AEM Forms] As etapas de fluxo de trabalho são compatíveis com variáveis. Para obter mais informações, consulte [Fluxo de trabalho centrado no Forms no OSGi](aem-forms-workflow-step-reference.md).

### Etapas de fluxo de trabalho sem suporte para variáveis {#workflow-steps-without-support-for-variables}

Você pode usar [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) para acessar variáveis em etapas de fluxo de trabalho que não aceitam variáveis.

#### Recuperar o valor da variável {#retrieve-the-variable-value}

Use as seguintes APIs no Script ECMA para recuperar valores para variáveis existentes com base no tipo de dados:

| Tipo de dados variável | API |
|---|---|
| Primitiva (Longa, Dupla, Booleana, Data e String) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| Documento | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData().getMetaDataMap().get(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.Document.class); |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| Modelo de dados do formulário | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |


**Exemplo**

Recupere o valor do tipo de dados string usando a seguinte API:

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Atualizar o valor da variável {#update-the-variable-value}

Use a seguinte API no Script ECMA para atualizar o valor de uma variável:

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Exemplo**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

Atualiza o valor para o **salário** para 50000.

### Definir variáveis para chamar workflows {#apiinvokeworkflow}

Você pode usar uma API para definir variáveis e passá-las para chamar instâncias de fluxo de trabalho.

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) usa model, wfData e metaData como argumentos. Use MetaDataMap para definir o valor da variável.

Nessa API, a variável **variableName** está definida como **value** usar metaData.put(variableName, value);

```javascript
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**Exemplo**

Inicializar o **doc** objeto de documento a um caminho (&quot;a/b/c&quot;) e defina o valor do **docVar** ao caminho armazenado no objeto do documento.

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## Editar uma variável {#edit-a-variable}

1. Na página Editar fluxo de trabalho, toque no ícone Variáveis disponível no sidekick do modelo de fluxo de trabalho. A seção Variáveis, no painel esquerdo, exibe todas as variáveis existentes.
1. Toque no ![editar](assets/edit.svg) (Editar) ícone ao lado do nome da variável que você deseja editar.
1. Edite as informações da variável e toque ![done_icon](assets/Smock_Checkmark_18_N.svg) para salvar as alterações. Não é possível editar o **[!UICONTROL Nome]** e **[!UICONTROL Tipo]** para uma variável.

## Excluir uma variável {#delete-a-variable}

Antes de excluir a variável, remova todas as referências da variável do fluxo de trabalho. Verifique se a variável não está sendo usada no fluxo de trabalho.

Para excluir uma variável:

1. Na página Editar fluxo de trabalho, toque no ícone Variáveis disponível no sidekick do modelo de fluxo de trabalho. A seção Variáveis, no painel esquerdo, exibe todas as variáveis existentes.
1. Toque no ícone Excluir ao lado do nome da variável que você deseja excluir.
1. Toque ![done_icon](assets/Smock_Checkmark_18_N.svg) para confirmar e excluir a variável.

## Referências {#references}

Para obter mais exemplos sobre o uso de variáveis no [!DNL AEM Forms] Etapas do workflow, consulte [Variáveis em fluxos de trabalho de AEM](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html).
