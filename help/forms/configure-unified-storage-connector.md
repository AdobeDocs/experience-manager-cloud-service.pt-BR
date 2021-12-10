---
title: Como configurar o Unified Storage Connector para AEM Forms?
description: Saiba como gerenciar o Unified Storage Connector para AEM Forms. Use o Conector de armazenamento unificado para conectar o AEM Forms a armazenamentos de dados externos.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# Gerenciar o conector de armazenamento unificado para AEM Forms {#manage-unified-storage-connector}

Você pode usar o Unified Storage Connector para conectar o AEM Forms a armazenamentos de dados externos.

Por exemplo, é possível preencher valores para campos em um formulário adaptável e enviá-los a um Fluxo de trabalho AEM. Você pode configurar AEM Workflows para armazenar dados em um armazenamento externo, como o servidor de armazenamento do Microsoft Azure. Use o Unified Storage Connector para criar uma conexão entre AEM Workflows e o armazenamento externo.

## Conecte AEM Workflows com um servidor de armazenamento do Microsoft Azure {#connect-workflows-with-azure}

Crie uma configuração de armazenamento do Azure e consulte-a usando o Conector de Armazenamento Unificado. Em seguida, você pode configurar AEM modelos de fluxo de trabalho para externalizar o armazenamento de dados para conectá-los a um servidor de armazenamento do Azure.

### Criar [!DNL Azure] configuração de armazenamento {#create-azure-storage-configuration}

Antes de executar essas etapas, verifique se você tem uma [!DNL Azure] conta de armazenamento e uma chave de acesso para autorizar o acesso ao [!DNL Azure] conta de armazenamento.

Execute as etapas a seguir para criar um [!DNL Azure] configuração de armazenamento:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Armazenamento do Azure]**.
1. Selecione uma pasta para criar a configuração e toque em **[!UICONTROL Criar]**.
1. Especifique um título para a configuração no **[!UICONTROL Título]** campo.
1. Especifique o nome da variável [!DNL Azure] conta de armazenamento na **[!UICONTROL Conta de Armazenamento do Azure]** campo.
1. Especifique a chave para acessar a conta de armazenamento do Azure no **[!UICONTROL Chave de Acesso do Azure]** campo e toque em **[!UICONTROL Salvar]**.

### Configurar o conector de armazenamento unificado para fluxos de trabalho de AEM {#configure-unified-storage-connector-workflows}

Execute as seguintes etapas para configurar o Unified Storage Connector para AEM Workflows:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de armazenamento unificado]**.

1. No **[!UICONTROL Fluxo de trabalho]** seção , selecione **[!UICONTROL Azure]** na lista suspensa Armazenamento .
1. Especifique a [caminho de configuração para a configuração de armazenamento do Azure](#create-azure-storage-configuration) no **[!UICONTROL Caminho de configuração de armazenamento]** campo.
1. Toque **[!UICONTROL Publicar]** em seguida, toque em **[!UICONTROL Salvar]** para salvar a configuração.

### Configurar um modelo de fluxo de trabalho AEM para armazenamento externo de dados {#configure-workflow-external-data-storage}

Execute as seguintes etapas para configurar um modelo de Fluxo de trabalho AEM para um armazenamento de dados externo:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Selecione um nome de modelo e toque em **[!UICONTROL Editar]**.
1. Toque no ícone Informações da página e toque em **[!UICONTROL Abrir propriedades]**.
1. Selecionar **[!UICONTROL Externalizar o armazenamento de dados do workflow]**.
1. Toque **[!UICONTROL Salvar e fechar]** para salvar as propriedades.

>[!NOTE]
>
>As opções para salvar a etapa Atribuir tarefa como rascunho e recuperar o histórico da etapa Atribuir tarefa não estão disponíveis ao configurar um modelo de fluxo de trabalho AEM para armazenamento de dados externo.

### Diretrizes para fluxos de trabalho de AEM para armazenamento externo de dados {#guidelines-workflows-external-data-storage}

A seguir estão as diretrizes ao usar AEM Workflows e armazenar dados em armazenamentos de dados externos, como o servidor de armazenamento do Microsoft Azure:

* Use variáveis para armazenar dados enquanto define arquivos de dados de entrada e saída e anexos em etapas do modelo de fluxo de trabalho. Não selecionar **[!UICONTROL Em relação à carga]** e **[!UICONTROL Disponível em um caminho absoluto]** opções. O **[!UICONTROL Em relação à carga]** e **Disponível em um caminho absoluto** as opções não são exibidas automaticamente após [configurar um modelo de fluxo de trabalho AEM para armazenamento externo de dados](#configure-workflow-external-data-storage).

* Use variáveis para armazenar arquivos de dados e anexos enquanto envia um formulário adaptável para um Fluxo de trabalho AEM. Não selecionar **[!UICONTROL Em relação à carga]** ao enviar um formulário adaptável para um Fluxo de trabalho AEM. O **[!UICONTROL Em relação à carga]** não será exibida automaticamente após [configurar um modelo de fluxo de trabalho AEM para armazenamento externo de dados](#configure-workflow-external-data-storage).

* Não use uma etapa personalizada AEM Workflow em um modelo de workflow para armazenar dados no repositório CRX DE.

* Quando você [configurar um modelo de fluxo de trabalho AEM para armazenamento externo de dados](#configure-workflow-external-data-storage), não crie colunas personalizadas para AEM Caixa de entrada com base nos dados de um fluxo de trabalho.
