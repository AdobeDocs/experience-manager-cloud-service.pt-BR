---
title: Como configurar o armazenamento do Azure?
description: Saiba como integrar formulários ao servidor de armazenamento do Azure.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---

# Configurar armazenamento do [!DNL Azure] {#configure-azure-storage}


![integração de dados](assets/data-integeration.png)

A [[!DNL Experience Manager Forms] Integração de Dados](data-integration.md) fornece uma configuração de armazenamento [!DNL Azure] para integrar formulários com serviços de armazenamento [!DNL Azure]. O Modelo de Dados de Formulário (FDM) pode ser usado para criar o Forms Adaptável que interage com o servidor [!DNL Azure] para habilitar fluxos de trabalho de negócios. Por exemplo:

* Gravar dados em [!DNL Azure] no envio do Formulário Adaptável.
* Grave dados em [!DNL Azure] por meio de entidades personalizadas definidas no Modelo de Dados de Formulário (FDM) e vice-versa.
* Consulte o servidor [!DNL Azure] para obter dados e popular previamente o Forms Adaptável.
* Ler dados do servidor [!DNL Azure].

## Criar configuração de armazenamento [!DNL Azure] {#create-azure-storage-configuration}

Antes de executar essas etapas, verifique se você tem uma conta de armazenamento [!DNL Azure] e uma chave de acesso para autorizar o acesso à conta de armazenamento [!DNL Azure].

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Armazenamento do Azure]**.
1. Selecione uma pasta para criar a configuração e selecione **[!UICONTROL Criar]**.
1. Especifique um título para a configuração no campo **[!UICONTROL Título]**.
1. Especifique o nome da conta de armazenamento [!DNL Azure] no campo **[!UICONTROL Conta de Armazenamento do Azure]**.
1. Especifique a chave para acessar a conta de armazenamento do Azure no campo **[!UICONTROL Chave de Acesso do Azure]** e selecione **[!UICONTROL Salvar]**.

## Criar modelo de dados do formulário {#create-azure-form-data-model}

Depois de criar a configuração de armazenamento [!DNL Azure], você pode [criar o Modelo de Dados de Formulário](create-form-data-models.md). Especifique a pasta que contém a configuração [!DNL Azure] no campo **[!UICONTROL Configuração do Data Source]** ao criar o Modelo de Dados de Formulário (FDM). Em seguida, você pode selecionar a configuração na lista de configurações que existem no nome da pasta especificada.

### Adicionar serviços do [!DNL Azure] ao modelo de dados de formulário {#add-azure-services}

Depois de criar o Modelo de dados de formulário (FDM) e objetos de modelo de dados, você pode adicionar [!DNL Azure] serviços ao Modelo de dados de formulário (FDM).

Para adicionar serviços do [!DNL Azure]:

1. No modo de Edição, selecione os serviços na seção **[!UICONTROL Serviços]** no painel esquerdo e selecione **[!UICONTROL Adicionar Selecionados]**. Os serviços selecionados são exibidos na guia **[!UICONTROL Serviços]** do Form Data Model (FDM).

   ![Adicionar Serviços Selecionados](assets/select-services.png)

1. Na guia **[!UICONTROL Serviços]**, selecione o serviço e **[!UICONTROL Editar Propriedades]**. Com base no serviço, defina os objetos de modelo de entrada ou saída do serviço.

1. Selecione **[!UICONTROL Salvar]** para salvar o modelo de dados de formulário (FDM).

   A tabela a seguir descreve os serviços [!DNL Azure] disponíveis:

   <table>
    <tbody>
     <tr>
      <th><strong>Nome do serviço</strong></th>
      <th><strong>Descrição</strong></th>
     </tr>
     <tr>
      <td>Obter Blob do Azure</td>
      <td>Recuperar dados armazenados como um Blob no armazenamento do Azure usando uma ID ou um nome</td>
     </tr>
     <tr>
      <td>Obter Blob com URL de binários do Azure</td>
      <td>Recupere dados armazenados como um Blob com URL para binários no armazenamento do Azure usando uma ID ou um nome</td>
     </tr>
     <tr>
      <td>Salvar Blob no Azure</td>
      <td>Use uma ID de blob para salvar dados no armazenamento do Azure</td>
     </tr>
     <tr>
      <td>Atualizar blob no Azure</td>
      <td>Usar uma ID de blob para atualizar dados no armazenamento do Azure</td>
     </tr>
     <tr>
      <td>Recuperar lista de IDs de blob do Azure</td>
      <td>Recupere uma lista de IDs de blob do Azure com base no número definido na solicitação de entrada.</td>
     </tr>
     <tr>
      <td>Recuperar URLs SAS para Blobs do Azure</td>
      <td>Recupere URLs SAS para Blobs do Azure com base nas IDs de Blob na solicitação de entrada.</td>
     </tr>
     <tr>
      <td>Excluir Blob do Azure</td>
      <td>Usar uma ID de blob para excluir dados do armazenamento do Azure</td>
     </tr>
    </tbody>
   </table>

### Definir uma propriedade do objeto de modelo de dados como uma chave de pesquisa {#define-data-model-object-as-metadata}

Para definir uma propriedade de objeto de modelo de dados como uma chave de pesquisa:

1. Na guia **[!UICONTROL Modelo]**, selecione a propriedade do objeto de modelo de dados e selecione **[!UICONTROL Editar Propriedades]**.
1. Alterne a opção de alternância **[!UICONTROL Chave de Pesquisa]** para o estado ATIVADO. Essa opção está disponível somente para tipos de dados primários.
1. Selecione **[!UICONTROL Concluído]** e **[!UICONTROL Salvar]** para salvar o Modelo de Dados de Formulário (FDM).

Depois de definir as propriedades do objeto de modelo de dados como chaves de pesquisa, os valores de hash são armazenados nas tags de índice do Azure e os valores codificados na Base64 são armazenados nos metadados do Azure.

>[!NOTE]
>
>Somente 10 chaves de pesquisa são permitidas por entidade do Azure, pois o Azure permite apenas 10 tags por Blob, e o valor de propriedades marcado como chaves de pesquisa é armazenado nas tags de índice do Azure após o hash.

<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->