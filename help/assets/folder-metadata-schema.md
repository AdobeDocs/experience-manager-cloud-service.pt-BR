---
title: Esquema de metadados de pasta
description: Saiba como criar esquema de metadados para pastas de ativos no [!DNL Experience Manager Assets]
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: c86760ed-169d-40f7-91a4-8aee449b286c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 9%

---

# Esquema de metadados de pasta {#folder-metadata-schema}

O [!DNL Adobe Experience Manager Assets] permite criar esquemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta.

## Adicionar um formulário de esquema de metadados de pasta {#add-a-folder-metadata-schema-form}

Use o editor do Forms de Esquema de metadados de pasta para criar e editar esquemas de metadados para pastas.

1. Selecione o logotipo [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de Metadados de Pasta]**.
1. Na página Forms do Esquema de Metadados da Pasta, selecione **[!UICONTROL Criar]**.
1. Especifique um nome para o formulário e selecione **[!UICONTROL Criar]**. O novo formulário de esquema é listado na página Schema Forms.

## Editar formulários de esquema de metadados de pasta {#edit-folder-metadata-schema-forms}

É possível editar um formulário de esquema de metadados recém-adicionado ou existente, que inclui o seguinte:

* Guias
* Itens de formulário em guias.

Você pode mapear/configurar esses itens de formulário para um campo em um nó de metadados no repositório do CRX. Você pode adicionar novas guias ou itens de formulário ao formulário de esquema de metadados.

1. Na página Forms de esquema, selecione o formulário criado e o ícone **[!UICONTROL Editar]** na barra de ferramentas.
1. Na página Editor de Esquema de Metadados de Pasta, selecione o ícone **[!UICONTROL +]** para adicionar uma guia ao formulário. Para renomear a guia, selecione o nome padrão e especifique o novo nome em **[!UICONTROL Configurações]**.

   ![guia_personalizada](assets/custom_tab.png)

   Para adicionar mais guias, selecione o ícone **[!UICONTROL +]**. Selecione **[!UICONTROL X]** para excluir uma guia.

1. Na guia ativa, adicione um ou mais componentes da guia **[!UICONTROL Criar Formulário]**.

   ![adicionando_componentes](assets/adding_components.png)

   Se você criar várias guias, selecione uma guia específica para adicionar componentes.

1. Para configurar um componente, selecione-o e modifique suas propriedades na guia **[!UICONTROL Configurações]**.

   Se necessário, exclua um componente da guia **[!UICONTROL Configurações]**.

   ![configurar_propriedades](assets/configure_properties.png)

1. Selecione **[!UICONTROL Salvar]** na barra de ferramentas para salvar as alterações.

### Componentes para criar formulários {#components-to-build-forms}

A guia **[!UICONTROL Criar Formulário]** lista itens de formulário que você usa no formulário de esquema de metadados da pasta. A guia **[!UICONTROL Configurações]** exibe os atributos para cada item selecionado na guia **[!UICONTROL Formulário de compilação]**. Aqui está uma lista dos itens de formulário disponíveis na guia **[!UICONTROL Criar Formulário]**:

<table>
 <tbody>
  <tr>
   <td><p><strong>Nome do componente</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>Cabeçalho da seção</p> </td>
   <td><p> Adicione um cabeçalho de seção para obter uma lista de componentes comuns.</p> </td>
  </tr>
  <tr>
   <td><p>Texto em linha única</p> </td>
   <td><p> Adicione uma propriedade de texto de linha única. Ele é armazenado como uma string.</p> </td>
  </tr>
  <tr>
   <td><p>Texto multivalor</p> </td>
   <td><p> Adicione uma propriedade de texto de vários valores. Ele é armazenado como uma matriz de sequência.</p> </td>
  </tr>
  <tr>
   <td><p>Número</p> </td>
   <td><p> Adiciona um componente de número.</p> </td>
  </tr>
  <tr>
   <td><p>Data</p> </td>
   <td><p> Adiciona um componente de data.</p> </td>
  </tr>
  <tr>
   <td><p>Lista suspensa</p> </td>
   <td><p> Adiciona uma lista suspensa.</p> </td>
  </tr>
  <tr>
   <td><p>Tags padrão</p> </td>
   <td><p> Adicione uma tag. </p> </td>
  </tr>
  <tr>
   <td><p>Campo oculto</p> </td>
   <td><p> Adicione um campo oculto. Ele é enviado como um parâmetro POST quando o ativo é salvo.</p> </td>
  </tr>
 </tbody>
</table>

### Edição de itens de formulário {#editing-form-items}

Para editar as propriedades dos itens de formulário, selecione o componente e edite todas ou um subconjunto das seguintes propriedades na guia **[!UICONTROL Configurações]**. É recomendável mapear apenas um campo para uma determinada propriedade no esquema de metadados. Caso contrário, o campo adicionado mais recente mapeado para a propriedade será escolhido pelo sistema.

**[!UICONTROL Rótulo do Campo]**: o nome da propriedade de metadados exibida na página de propriedades da pasta.

**[!UICONTROL Mapear para a Propriedade]**: esta propriedade especifica o caminho relativo do nó de pasta no repositório do CRX onde ele é salvo. Ele começa com &quot;**./**&quot;, que indica que o caminho está sob o nó da pasta.

Veja a seguir exemplos de valores válidos para uma propriedade:

* `./jcr:content/metadata/dc:title`: armazena o valor no nó de metadados da pasta como a propriedade `dc:title`.

* `./jcr:created`: armazena a data e a hora de criação de um ativo. É uma propriedade protegida. Se você configurar essas propriedades, a Adobe recomenda marcá-las como [!UICONTROL Desabilitar Edição].

Para garantir que o componente seja exibido corretamente no formulário de esquema de metadados, não inclua um espaço no caminho da propriedade.

**[!UICONTROL Caminho JSON]**: use-o para especificar o caminho do arquivo JSON onde você especifica pares de valores chave para opções.

**[!UICONTROL Espaço reservado]**: use essa propriedade para especificar texto de espaço reservado relevante em relação à propriedade de metadados.

**[!UICONTROL Opções]**: use esta propriedade para especificar opções em uma lista.

**[!UICONTROL Descrição]**: use essa propriedade para adicionar uma descrição curta para o componente de metadados.

**[!UICONTROL Classe]**: classe de objeto à qual a propriedade está associada.

## Excluir formulários de esquema de metadados de pasta {#delete-folder-metadata-schema-forms}

Você pode deletar formulários de esquema de metadados de pasta da página Forms de Esquema de Metadados de Pasta. Para excluir um formulário, selecione-o e, em seguida, o ícone Excluir na barra de ferramentas.

![excluir_formulário](assets/delete_form.png)

## Atribuir um esquema de metadados de pasta {#assign-a-folder-metadata-schema}

Você pode atribuir um esquema de metadados de pasta a uma pasta na página Forms de Esquema de metadados de pasta ou ao criar uma pasta.

Se você configurar um esquema de metadados para uma pasta, o caminho para o formulário de esquema será armazenado na propriedade `folderMetadataSchema` do nó da pasta em .*/jcr:content*.

### Atribuir a um esquema a partir da página Esquema de metadados de pasta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Selecione o logotipo [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]**> **[!UICONTROL Esquemas de Metadados de Pasta]**.
1. Na página Forms do Esquema de Metadados da Pasta, selecione o formulário de esquema que deseja aplicar a uma pasta.
1. Na barra de ferramentas, selecione **[!UICONTROL Aplicar a Pastas]**.

1. Selecione a pasta na qual aplicar o esquema e selecione **[!UICONTROL Aplicar]**. Se um esquema de metadados já estiver aplicado à pasta, uma mensagem de aviso informará que você está prestes a substituir o esquema de metadados existente. Selecione **[!UICONTROL Substituir]**.
1. Abra as propriedades de metadados da pasta à qual você aplicou o esquema de metadados.

   ![propriedades_da_pasta](assets/folder_properties.png)

   Para exibir os campos de metadados da pasta, selecione a guia **[!UICONTROL Metadados da pasta]**.

   ![propriedades_de_metadados_de_pasta](assets/folder_metadata_properties.png)

### Atribuir um esquema ao criar uma pasta {#assign-a-schema-when-creating-a-folder}

Você pode atribuir um esquema de metadados de pasta ao criar uma pasta. Se existir pelo menos um esquema de metadados de pasta no sistema, uma lista extra será exibida na caixa de diálogo **[!UICONTROL Criar Pasta]**. Você pode selecionar o esquema desejado. Por padrão, nenhum schema está selecionado.

1. Na interface de usuário do [!DNL Experience Manager Assets], selecione **[!UICONTROL Criar]** na barra de ferramentas.
1. Especifique um título e nome para a pasta.
1. Na lista Esquema de metadados de pasta, selecione o esquema desejado. Em seguida, selecione **[!UICONTROL Criar]**.

   ![select_schema](assets/select_schema.png)

1. Abra as propriedades de metadados da pasta à qual você aplicou o esquema de metadados.
1. Para exibir os campos de metadados da pasta, selecione a guia **[!UICONTROL Metadados da pasta]**.

## Usar o esquema de metadados da pasta {#use-the-folder-metadata-schema}

Abra as propriedades de uma pasta configurada com um esquema de metadados de pasta. Uma guia **[!UICONTROL Metadados da pasta]** é exibida na página Propriedades da pasta. Para exibir o formulário de esquema de metadados da pasta, selecione essa guia.

Insira valores de metadados nos vários campos e selecione **[!UICONTROL Salvar]** para armazenar os valores. Os valores especificados são armazenados no nó da pasta no repositório do CRX.

![propriedades_de_metadados_da_pasta-1](assets/folder_metadata_properties-1.png)

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
