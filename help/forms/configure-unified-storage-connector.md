---
title: Como configurar o Conector de armazenamento unificado (USC) para AEM Forms?
description: Saiba como gerenciar o Conector de armazenamento unificado (USC) para AEM Forms. Use o Conector de armazenamento unificado (USC) para conectar o AEM Forms a armazenamentos de dados externos.
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: c33f59cb56decf1e5bbbe0b5bb084e906585e702
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Gerenciar o Conector de armazenamento unificado (USC) para AEM Forms {#manage-unified-storage-connector}

Você pode usar o Conector de armazenamento unificado (USC) para conectar o AEM Forms a armazenamentos de dados externos.

Por exemplo, é possível preencher valores para campos em um formulário adaptável e enviá-lo para um fluxo de trabalho do AEM. Você pode configurar ainda mais os fluxos de trabalho do AEM para armazenar dados em um armazenamento externo, como o servidor de armazenamento do Microsoft Azure. Use o Conector de armazenamento unificado (USC) para criar uma conexão entre os fluxos de trabalho do AEM e o armazenamento externo.

## Conectar fluxos de trabalho do AEM a um servidor de armazenamento do Microsoft Azure {#connect-workflows-with-azure}

Crie uma configuração de armazenamento do Azure e consulte essa configuração usando o Conector de armazenamento unificado (USC). Em seguida, você pode configurar modelos de Fluxo de Trabalho do AEM para externalizar o armazenamento de dados e conectá-los a um servidor de armazenamento do Azure.

### Criar [!DNL Azure] configuração de armazenamento {#create-azure-storage-configuration}

Antes de executar essas etapas, verifique se você tem uma [!DNL Azure] conta de armazenamento e uma chave de acesso para autorizar o acesso à [!DNL Azure] conta de armazenamento.

Execute as seguintes etapas para criar um [!DNL Azure] configuração de armazenamento:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Armazenamento do Azure]**.
1. Selecione uma pasta para criar a configuração e toque em **[!UICONTROL Criar]**.
1. Especifique um título para a configuração no campo **[!UICONTROL Título]** campo.
1. Especifique o nome do [!DNL Azure] conta de armazenamento na **[!UICONTROL Conta de armazenamento do Azure]** campo.
1. Especifique a chave para acessar a conta de armazenamento do Azure no **[!UICONTROL Chave de Acesso do Azure]** e toque em **[!UICONTROL Salvar]**.

### Configurar o Conector de armazenamento unificado (USC) para fluxos de trabalho do AEM {#configure-unified-storage-connector-workflows}

Execute as seguintes etapas para configurar o Unified Storage Connector (USC) para fluxos de trabalho de AEM:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de armazenamento unificado]**.

1. No **[!UICONTROL Fluxo de trabalho]** seção, Selecionar **[!UICONTROL Azure]** na lista suspensa Armazenamento.
1. Especifique a [caminho de configuração para a configuração de armazenamento do Azure](#create-azure-storage-configuration) no **[!UICONTROL Caminho de configuração de armazenamento]** campo.
1. Toque **[!UICONTROL Publish]** e toque em **[!UICONTROL Salvar]** para salvar a configuração.

### Configurar um modelo de fluxo de trabalho do AEM para armazenamento de dados externo {#configure-workflow-external-data-storage}

Execute as seguintes etapas para configurar um modelo de fluxo de trabalho de AEM para um armazenamento de dados externo:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Selecione um nome de modelo e toque em **[!UICONTROL Editar]**.
1. Toque no ícone Informações da página e em **[!UICONTROL Abrir propriedades]**.
1. Selecionar **[!UICONTROL Externalizar o armazenamento de dados do fluxo de trabalho]**.
1. Toque **[!UICONTROL Salvar e fechar]** para salvar as propriedades.

>[!NOTE]
>
>As opções para salvar a etapa Atribuir tarefa como rascunho e recuperar o histórico da etapa Atribuir tarefa são desativadas ao configurar um modelo de fluxo de trabalho AEM para armazenamento de dados externo.

### Diretrizes para fluxos de trabalho do AEM para armazenamento de dados externo {#guidelines-workflows-external-data-storage}

Estas são as diretrizes quando você está usando fluxos de trabalho do AEM e armazenando dados em armazenamentos de dados externos, como o servidor de armazenamento do Microsoft Azure:

* Use variáveis para armazenar dados enquanto define arquivos de dados de entrada e saída e anexos em etapas de modelo de fluxo de trabalho. Não selecionar **[!UICONTROL Relativo à carga útil]** e **[!UICONTROL Disponível em um caminho absoluto]** opções. A variável **[!UICONTROL Relativo à carga útil]** e **[!UICONTROL Disponível em um caminho absoluto]** opções não são exibidas automaticamente depois que você [configurar um modelo de fluxo de trabalho do AEM para armazenamento de dados externo](#configure-workflow-external-data-storage).

* Use variáveis para armazenar arquivos de dados e anexos ao enviar um formulário adaptável a um fluxo de trabalho do AEM. Não selecionar **[!UICONTROL Relativo à carga útil]** ao enviar um formulário adaptável a um fluxo de trabalho de AEM. A variável **[!UICONTROL Relativo à carga útil]** não são exibidos automaticamente depois que você [configurar um modelo de fluxo de trabalho do AEM para armazenamento de dados externo](#configure-workflow-external-data-storage).

* Não use uma etapa personalizada do fluxo de trabalho do AEM em um modelo de fluxo de trabalho para armazenar dados no repositório CRX DE.

* Quando você [configurar um modelo de fluxo de trabalho do AEM para armazenamento de dados externo](#configure-workflow-external-data-storage), não crie colunas personalizadas para a Caixa de entrada do AEM, pois os valores das colunas personalizadas não serão buscados se o item de trabalho na Caixa de entrada do AEM pertencer a um fluxo de trabalho marcado para armazenamento externo.

>[!MORELIKETHIS]
>
>* [Configurar fontes de dados para o AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurar o armazenamento do Azure para o AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrar o Microsoft Dynamics 365 e Salesforce ao Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>  [Adicionar o Forms Portal a uma página do AEM Sites](/help/forms/configure-forms-portal.md)
