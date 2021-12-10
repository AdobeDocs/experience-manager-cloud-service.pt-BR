---
title: Como configurar o armazenamento do Azure?
description: Saiba como integrar formulários ao servidor de armazenamento do Azure.
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 1%

---

# Configurar [!DNL Azure] armazenamento {#configure-azure-storage}

[[!DNL Experience Manager Forms] Integração de dados](data-integration.md) fornece uma [!DNL Azure] configuração de armazenamento para integrar formulários com o [!DNL Azure] serviços de armazenamento. O Modelo de dados de formulário pode ser usado para criar um Forms adaptável que interage com o [!DNL Azure] para ativar workflows de negócios. Por exemplo:

* Gravar dados em [!DNL Azure] no envio do formulário adaptável.
* Gravar dados em [!DNL Azure] por meio de entidades personalizadas definidas no Modelo de dados de formulário e vice-versa.
* Query [!DNL Azure] para dados e pré-preencher o Adaptive Forms.
* Ler dados de [!DNL Azure] servidor.

## Criar [!DNL Azure] configuração de armazenamento {#create-azure-storage-configuration}

Antes de executar essas etapas, verifique se você tem uma [!DNL Azure] conta de armazenamento e uma chave de acesso para autorizar o acesso ao [!DNL Azure] conta de armazenamento.

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Armazenamento do Azure]**.
1. Selecione uma pasta para criar a configuração e toque em **[!UICONTROL Criar]**.
1. Especifique um título para a configuração no **[!UICONTROL Título]** campo.
1. Especifique o nome da variável [!DNL Azure] conta de armazenamento na **[!UICONTROL Conta de Armazenamento do Azure]** campo.
1. Especifique a chave para acessar a conta de armazenamento do Azure no **[!UICONTROL Chave de Acesso do Azure]** campo e toque em **[!UICONTROL Salvar]**.

## Criar modelo de dados do formulário {#create-azure-form-data-model}

Depois de criar o [!DNL Azure] configuração de armazenamento, você pode [criar o Modelo de dados de formulário](create-form-data-models.md). Especifique a pasta que contém a [!DNL Azure] na configuração do **[!UICONTROL Configuração da Fonte de Dados]** ao criar o Modelo de dados de formulário. Em seguida, você pode selecionar a configuração na lista de configurações que existem no nome da pasta especificada.

### Adicionar [!DNL Azure] serviços para o Modelo de dados de formulário {#add-azure-services}

Depois de criar o Modelo de dados de formulário e os objetos de modelo de dados, é possível adicionar [!DNL Azure] para o Modelo de dados de formulário.

Para adicionar [!DNL Azure] serviços:

1. No modo Editar , selecione os serviços no **[!UICONTROL Serviços]** no painel esquerdo e toque em **[!UICONTROL Adicionar Selecionado]**. Os serviços selecionados são exibidos na **[!UICONTROL Serviços]** do Modelo de dados de formulário.

   ![Adicionar Serviços Selecionados](assets/select-services.png)

1. No **[!UICONTROL Serviços]** selecione o serviço e **[!UICONTROL Editar propriedades]**. Com base no serviço, defina os objetos do modelo de entrada ou saída para o serviço.

1. Toque **[!UICONTROL Salvar]** para salvar o modelo de dados de formulário.

   A tabela a seguir descreve os [!DNL Azure] serviços:

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
      <td>Obter Blob com URL binário do Azure</td>
      <td>Recuperar dados armazenados como um Blob com URL para binários no armazenamento do Azure usando uma ID ou um nome</td>
     </tr>
     <tr>
      <td>Salvar Blob no Azure</td>
      <td>Usar uma ID de blob para salvar dados no armazenamento do Azure</td>
     </tr>
     <tr>
      <td>Atualizar Blob no Azure</td>
      <td>Usar uma ID de blob para atualizar dados no armazenamento do Azure</td>
     </tr>
     <tr>
      <td>Recuperar lista de IDs de blob do Azure</td>
      <td>Recupere uma lista de IDs de blob do Azure com base no número definido na solicitação de entrada.</td>
     </tr>
     <tr>
      <td>Recuperar URLs SAS para Blobs do Azure</td>
      <td>Recupere URLs SAS para Blobs do Azure com base em IDs Blob na solicitação de entrada.</td>
     </tr>
     <tr>
      <td>Excluir Blob do Azure</td>
      <td>Usar uma ID de blob para excluir dados do armazenamento do Azure</td>
     </tr>
    </tbody>
   </table>

### Definir uma propriedade de objeto de modelo de dados como chave de pesquisa {#define-data-model-object-as-metadata}

Para definir uma propriedade de objeto de modelo de dados como uma chave de pesquisa:

1. No **[!UICONTROL Modelo]** selecione a propriedade de objeto do modelo de dados e toque em **[!UICONTROL Editar propriedades]**.
1. Alterne a **[!UICONTROL Chave de pesquisa]** alterne a opção para o estado ATIVADO. Essa opção está disponível somente para tipos de dados primários.
1. Toque **[!UICONTROL Concluído]** em seguida, toque em **[!UICONTROL Salvar]** para salvar o Modelo de dados de formulário.

Após definir as propriedades do objeto de modelo de dados como chaves de pesquisa, as chaves são salvas como metadados no armazenamento do Azure.
