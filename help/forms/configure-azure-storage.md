---
title: Como configurar o armazenamento do Azure?
description: Saiba como integrar formulários ao servidor de armazenamento do Azure.
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# Configurar armazenamento do[!DNL Azure] {#configure-azure-storage}


![integração de dados](assets/data-integeration.png)

[[!DNL Experience Manager Forms] Integração de dados](data-integration.md) fornece um [!DNL Azure] configuração de armazenamento para integrar formulários com o [!DNL Azure] serviços de armazenamento. O modelo de dados de formulário pode ser usado para criar o Forms adaptável que interage com o [!DNL Azure] servidor para habilitar workflows de negócios. Por exemplo:

* Gravar dados em [!DNL Azure] no envio do Formulário adaptável.
* Gravar dados em [!DNL Azure] por meio de entidades personalizadas definidas no Modelo de dados de formulário e vice-versa.
* Query [!DNL Azure] servidor para dados e pré-popular o Adaptive Forms.
* Ler dados de [!DNL Azure] servidor.

## Criar [!DNL Azure] configuração de armazenamento {#create-azure-storage-configuration}

Antes de executar essas etapas, verifique se você tem uma [!DNL Azure] conta de armazenamento e uma chave de acesso para autorizar o acesso à [!DNL Azure] conta de armazenamento.

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Armazenamento do Azure]**.
1. Selecione uma pasta para criar a configuração e toque em **[!UICONTROL Criar]**.
1. Especifique um título para a configuração no campo **[!UICONTROL Título]** campo.
1. Especifique o nome do [!DNL Azure] conta de armazenamento na **[!UICONTROL Conta de armazenamento do Azure]** campo.
1. Especifique a chave para acessar a conta de armazenamento do Azure no **[!UICONTROL Chave de Acesso do Azure]** e toque em **[!UICONTROL Salvar]**.

## Criar modelo de dados do formulário {#create-azure-form-data-model}

Depois de criar o [!DNL Azure] configuração de armazenamento, você pode [criar o modelo de dados do formulário](create-form-data-models.md). Especifique a pasta que contém o [!DNL Azure] configuração no **[!UICONTROL Configuração da fonte de dados]** ao criar o modelo de dados de formulário. Em seguida, você pode selecionar a configuração na lista de configurações que existem no nome da pasta especificada.

### Adicionar [!DNL Azure] serviços para o modelo de dados do formulário {#add-azure-services}

Depois de criar o modelo de dados de formulário e os objetos de modelo de dados, você pode adicionar [!DNL Azure] para o Modelo de dados do formulário.

Para adicionar [!DNL Azure] serviços:

1. No modo Editar, selecione os serviços na **[!UICONTROL Serviços]** no painel esquerdo e toque em **[!UICONTROL Adicionar selecionado]**. Os serviços selecionados são exibidos no **[!UICONTROL Serviços]** do Modelo de dados do formulário.

   ![Adicionar serviços selecionados](assets/select-services.png)

1. No **[!UICONTROL Serviços]** , selecione o serviço e **[!UICONTROL Editar propriedades]**. Com base no serviço, defina os objetos de modelo de entrada ou saída do serviço.

1. Toque **[!UICONTROL Salvar]** para salvar o modelo de dados do formulário.

   A tabela a seguir descreve as opções disponíveis [!DNL Azure] serviços:

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

1. No **[!UICONTROL Modelo]** , selecione a propriedade do objeto de modelo de dados e toque em **[!UICONTROL Editar propriedades]**.
1. Alterne a **[!UICONTROL Chave de pesquisa]** alternar para o estado ATIVADO. Essa opção está disponível somente para tipos de dados primários.
1. Toque **[!UICONTROL Concluído]** e toque em **[!UICONTROL Salvar]** para salvar o modelo de dados do formulário.

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