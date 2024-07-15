---
title: Como configurar o Conector de armazenamento unificado (USC) para AEM Forms?
description: Saiba como gerenciar o Conector de armazenamento unificado (USC) para AEM Forms. Use o Conector de armazenamento unificado (USC) para conectar o AEM Forms a armazenamentos de dados externos.
role: Admin, Developer, User
feature: Adaptive Forms, Workflow
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---

# Gerenciar o Conector de armazenamento unificado (USC) para AEM Forms {#manage-unified-storage-connector}

Você pode usar o Conector de armazenamento unificado (USC) para conectar o AEM Forms a armazenamentos de dados externos.

Por exemplo, é possível preencher valores para campos em um formulário adaptável e enviá-lo para um fluxo de trabalho do AEM. Você pode configurar ainda mais os fluxos de trabalho do AEM para armazenar dados em um armazenamento externo, como o servidor de armazenamento do Microsoft Azure. Use o Conector de armazenamento unificado (USC) para criar uma conexão entre os fluxos de trabalho do AEM e o armazenamento externo.

## Conectar fluxos de trabalho do AEM a um servidor de armazenamento do Microsoft Azure {#connect-workflows-with-azure}

Crie uma configuração de armazenamento do Azure e consulte essa configuração usando o Conector de armazenamento unificado (USC). Em seguida, você pode configurar modelos de Fluxo de Trabalho do AEM para externalizar o armazenamento de dados e conectá-los a um servidor de armazenamento do Azure.

### Criar configuração de armazenamento [!DNL Azure] {#create-azure-storage-configuration}

Antes de executar essas etapas, verifique se você tem uma conta de armazenamento [!DNL Azure] e uma chave de acesso para autorizar o acesso à conta de armazenamento [!DNL Azure].

Execute as seguintes etapas para criar uma configuração de armazenamento do [!DNL Azure]:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Armazenamento do Azure]**.
1. Selecione uma pasta para criar a configuração e selecione **[!UICONTROL Criar]**.
1. Especifique um título para a configuração no campo **[!UICONTROL Título]**.
1. Especifique o nome da conta de armazenamento [!DNL Azure] no campo **[!UICONTROL Conta de Armazenamento do Azure]**.
1. Especifique a chave para acessar a conta de armazenamento do Azure no campo **[!UICONTROL Chave de Acesso do Azure]** e selecione **[!UICONTROL Salvar]**.

### Configurar o Conector de armazenamento unificado (USC) para fluxos de trabalho do AEM {#configure-unified-storage-connector-workflows}

Execute as seguintes etapas para configurar o Unified Storage Connector (USC) para fluxos de trabalho de AEM:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de Armazenamento Unificado]**.

1. Na seção **[!UICONTROL Fluxo de Trabalho]**, selecione **[!UICONTROL Azure]** na lista suspensa Armazenamento.
1. Especifique o [caminho de configuração para a configuração de armazenamento do Azure](#create-azure-storage-configuration) no campo **[!UICONTROL Caminho de Configuração de Armazenamento]**.
1. Selecione **[!UICONTROL Publish]** e **[!UICONTROL Salvar]** para salvar a configuração.

### Configurar um modelo de fluxo de trabalho do AEM para armazenamento de dados externo {#configure-workflow-external-data-storage}

Execute as seguintes etapas para configurar um modelo de fluxo de trabalho de AEM para um armazenamento de dados externo:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Selecione um nome de modelo e selecione **[!UICONTROL Editar]**.
1. Selecione o ícone Informações da página e selecione **[!UICONTROL Abrir propriedades]**.
1. Selecione **[!UICONTROL Externalizar armazenamento de dados do fluxo de trabalho]**.
1. Selecione **[!UICONTROL Salvar e fechar]** para salvar as propriedades.

>[!NOTE]
>
>As opções para salvar a etapa Atribuir tarefa como rascunho e recuperar o histórico da etapa Atribuir tarefa são desativadas ao configurar um modelo de fluxo de trabalho AEM para armazenamento de dados externo.

### Diretrizes para fluxos de trabalho do AEM para armazenamento de dados externo {#guidelines-workflows-external-data-storage}

Estas são as diretrizes quando você está usando fluxos de trabalho do AEM e armazenando dados em armazenamentos de dados externos, como o servidor de armazenamento do Microsoft Azure:

* Use variáveis para armazenar dados enquanto define arquivos de dados de entrada e saída e anexos em etapas de modelo de fluxo de trabalho. Não selecione as opções **[!UICONTROL Relativo à Carga]** e **[!UICONTROL Disponível em um caminho absoluto]**. As opções **[!UICONTROL Relativo à carga]** e **[!UICONTROL Disponível em um caminho absoluto]** não são exibidas automaticamente depois que você [configura um modelo de fluxo de trabalho do AEM para armazenamento de dados externo](#configure-workflow-external-data-storage).

* Use variáveis para armazenar arquivos de dados e anexos ao enviar um formulário adaptável a um fluxo de trabalho do AEM. Não selecione a opção **[!UICONTROL Relativo à carga]** ao enviar um formulário adaptável a um fluxo de trabalho do AEM. A opção **[!UICONTROL Relativo à carga]** não é exibida automaticamente depois que você [configura um modelo de fluxo de trabalho do AEM para armazenamento de dados externo](#configure-workflow-external-data-storage).

* Não use uma etapa personalizada de fluxo de trabalho do AEM em um modelo de fluxo de trabalho para armazenar dados no repositório CRX DE.

* Ao [configurar um modelo de Fluxo de Trabalho do AEM para armazenamento de dados externo](#configure-workflow-external-data-storage), não crie colunas personalizadas para a Caixa de Entrada do AEM, pois os valores das colunas personalizadas não serão obtidos se o item de trabalho na Caixa de Entrada do AEM pertencer a um fluxo de trabalho marcado para armazenamento externo.

>[!MORELIKETHIS]
>
>* [Configurar fontes de dados para o AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurar o armazenamento do Azure para o AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrar o Microsoft Dynamics 365 e o Salesforce ao Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>  [Adicionar o Portal Forms a uma página do AEM Sites](/help/forms/configure-forms-portal.md)
